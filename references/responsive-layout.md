# 响应式布局与中文换行

## 核心问题

PPVI 早期版本只定义了"间距 / 字号 / 颜色"等静态规则, 在窄屏 / 压缩容器下经常出现:

- 标题在不该断的位置硬换行(英文短语断裂、中文标点开头)
- 字号被 `vw` 单位压缩到无法阅读
- 卡片列宽度坍缩, 出现 1 字一行
- 容器查询缺失, 组件无法按自身宽度自适应

本文是 PPVI 在响应式场景的硬约束。

## 容器查询优先于媒体查询

**媒体查询 = 看视口**, 适合页面级布局。
**容器查询 = 看自己的父容器**, 适合组件级。组件不知道自己被放在哪里, 容器查询让它按"我能用多宽"决定样式。

```css
/* 标记父容器为查询容器 */
.card-wrapper {
  container-type: inline-size;
}

/* 组件按自己容器宽度响应, 而非视口 */
@container (max-width: 480px) {
  .card-title { font-size: 1.25rem; }
  .card-meta { display: none; }
}
```

PPVI 组件 MUST 用容器查询。媒体查询仅用于页面级 grid template 切换。

## 字号 fluid clamp(防压缩字小)

字号不应在断点处跳变, 应在区间内线性过渡。

```css
:root {
  /* Display 96-120 */
  --fs-display: clamp(64px, 4vw + 32px, 120px);

  /* Headline 48-72 */
  --fs-headline: clamp(36px, 2.5vw + 24px, 72px);

  /* Subtitle 28-32 */
  --fs-subtitle: clamp(24px, 1vw + 20px, 32px);

  /* Body 18-22(下限 18, 屏幕可读阈值) */
  --fs-body: clamp(16px, 0.4vw + 14px, 22px);

  /* Caption 13-15(下限 13, 不再小) */
  --fs-caption: clamp(13px, 0.2vw + 12px, 15px);
}
```

**关键约束**:
- 中文 Body 绝对下限 16px(再小笔画糊在一起不可读)
- Caption 绝对下限 13px(再小读起来累)
- clamp 上限要等于字号系统的上限, 避免大屏字过大

## 中文换行三件套

英文换行规则不适用中文。中文需要这套组合:

```css
.text-content {
  /* 中文不在词中断, 英文按词换行 */
  word-break: keep-all;

  /* 但允许过长 URL / 英文单词溢出处理 */
  overflow-wrap: anywhere;

  /* 标题平衡断行, 避免末行只有一个字 */
  text-wrap: balance;

  /* 段落首行不缩进(西文版式) */
  text-indent: 0;
}
```

**对标题专用**:`text-wrap: balance` 让浏览器自动平衡每行字数, 避免"末行孤字"。Chrome 114+ / Safari 17.4+ 支持。

**对长正文专用**:`text-wrap: pretty` 优化避头尾标点(逗号不在行首)。

## 标点避头尾

中文版式禁止行首出现 `, 。 、 ; : ! ? " " ' ' ) 】 》`。CSS 没原生支持, 必须用 JS 库或服务端预处理(`pangu.js`)。

简单近似:
```css
.cjk-content {
  text-wrap: pretty;  /* Chrome 117+ 自动避头尾 */
  hanging-punctuation: allow-end;  /* Safari only */
}
```

如果产物对版式要求高(如 print-ready 报告), 必须用 pangu.js 处理文本。

## Grid 防爆设计

多卡片网格在窄屏不应硬挤, 应自动减列。

```css
.card-grid {
  display: grid;
  gap: 24px;

  /* 列宽 minmax: 最小 280, 否则自动换行 */
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
}

/* 卡片本身防溢出 */
.card {
  min-width: 0;            /* 关键: 解除 grid item 默认 min-width: auto */
  min-inline-size: 16ch;   /* 但保底 16 字符宽 */
  overflow-wrap: anywhere;
}
```

**为什么需要 `min-width: 0`**: Grid item 默认 `min-width: auto`, 这会让内容(长 URL/长词)撑开列, 破坏 minmax。设 0 后才能真正按 minmax 截断。

## 卡片宽度兜底

```css
.card {
  /* 容器再小, 不低于 240px */
  min-width: min(240px, 100%);

  /* 容器再大, 不超过 480px(单卡片) */
  max-width: 480px;

  /* 卡片内文字防溢出 */
  > * {
    min-width: 0;
    overflow-wrap: anywhere;
  }
}
```

## 间距随容器缩放

```css
:root {
  --space-tight: clamp(8px, 1vw, 12px);
  --space-base: clamp(12px, 2vw, 16px);
  --space-loose: clamp(24px, 4vw, 32px);
  --space-section: clamp(32px, 6vw, 64px);
}
```

注意:间距用 `vw` 而非 `cqw`, 因为间距偏向页面级。

## 长内容容器(防超长滚动)

```css
.long-content {
  max-width: 65ch;   /* 行长 50-75 字符为佳 */
  margin-inline: auto;
}
```

**为什么 65ch**: 排版界共识。中文按"字"计算约 30-40 个汉字/行, 英文 50-75 字符/行, 这是大脑跳读的舒适区。

## 常见错误

- ❌ 用 `vw` 设字号不加 clamp — 极小屏字会缩到不可读
- ❌ 用媒体查询响应组件 — 组件不该关心视口
- ❌ 忘记 `min-width: 0` — Grid minmax 失效
- ❌ 中文用英文换行规则 — 出现"句首逗号"等版式问题
- ❌ 长 URL 没 `overflow-wrap: anywhere` — 撑爆容器
- ❌ 卡片 grid 不设 `min-width: 0` — 长内容把卡片撑大
- ❌ 用断点(@media)硬切字号 — 在断点处突然跳变, 用 clamp 渐变

## 调试响应式的快速方法

```css
/* 临时给所有容器加边框, 看哪个出现错误换行 */
* {
  outline: 1px solid rgba(255, 0, 0, 0.1);
}
```

DevTools → Inspect → Computed → `font-size` / `width`, 检查实际渲染值。

## 浏览器支持现状

| 特性 | Chrome | Safari | Firefox |
|---|---|---|---|
| Container queries | 105+ | 16+ | 110+ |
| `text-wrap: balance` | 114+ | 17.4+ | 121+ |
| `text-wrap: pretty` | 117+ | 不支持 | 不支持 |
| `clamp()` | 79+ | 13.1+ | 75+ |

需要兼容老浏览器时:容器查询用 `@supports` fallback 到媒体查询, balance/pretty 直接 graceful degrade(无效不影响功能)。
