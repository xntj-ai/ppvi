# 字体系统方法论

## 为什么需要严格的字体层级

字体是界面中信息量最大的视觉元素。如果字体大小随意, 用户的眼睛无法建立扫描模式, 阅读效率断崖式下降。

严格的层级系统意味着: 用户看过一个页面后, 在所有页面都能用同样的扫描模式获取信息。

## 5 级字体系统(精简自原 6 级)

### 级别定义

```
Level 1 · Display    — 封面/首屏冲击力      96-120px   Bold (700)
Level 2 · Headline   — 区块标题/大数字       48-72px    Bold (700)
Level 3 · Subtitle   — 副标题/卡片标题       28-32px    SemiBold (600)
Level 4 · Body       — 正文/列表/描述        18-22px    Regular (400)
Level 5 · Caption    — 页码/时间戳/辅助      13-15px    Regular (400)
```

**为什么是 5 级**: 6 级实践中过满, 大字档(Headline 60-72 与 Title 42-52)跨度近用户会混淆。合并后跨级比例都 ≥1.4x, 视觉差异清晰。

### 单视图字号数量上限

**一个 artifact(页面/海报/报告)内同时出现的字号数量不超过 5 个**, 即用满 5 级即可。一个视图内通常用 3-4 个级别就够。

超过 5 个 → 层级崩溃, 用户不知道扫描重点。

### 跨级原则

- 相邻级别的字号比例 ≥ 1.4x(感知上明显不同)
  - 120 / 72 = 1.67 ✓
  - 72 / 32 = 2.25 ✓
  - 32 / 22 = 1.45 ✓
  - 22 / 15 = 1.47 ✓
- 同一级别在整个产品中保持一致(不因页面不同而变化)
- 强调用字重变化, 不用字号变化(同级内 Regular → SemiBold 做强调)

### Fluid 字号(防压缩字过小)

每一级用 `clamp()` 定义, 在容器收缩时优雅降级:

```css
:root {
  --fs-display:  clamp(64px, 4vw + 32px, 120px);
  --fs-headline: clamp(36px, 2.5vw + 24px, 72px);
  --fs-subtitle: clamp(24px, 1vw + 20px, 32px);
  --fs-body:     clamp(16px, 0.4vw + 14px, 22px);
  --fs-caption:  clamp(13px, 0.2vw + 12px, 15px);
}
```

**像素绝对下限**(再小就不可读):
- 中文 Body ≥ 16px(汉字笔画不糊的阈值)
- Caption ≥ 13px(信息可被识别的阈值)
- 移动端字号下限也不破 14px(系统字渲染优化最佳区)

详见 [responsive-layout.md](responsive-layout.md)

### 行高规则

```
Display/Headline:  line-height: 1.1 - 1.2  (大字紧凑)
Subtitle:          line-height: 1.3 - 1.4  (中字适中)
Body:              line-height: 1.6 - 1.8  (正文舒适)
Caption:           line-height: 1.4 - 1.5  (小字紧凑但可读)
```

## 三权重系统(替代"用满 9 个字重")

字重不是越多越好。三档已覆盖所有信息层级:

```
Read    400-450   — 正文阅读  (Body, Caption 默认)
Emphasize  510-550   — 强调突出  (同级内强调, 替代加粗或变色)
Announce  590-700   — 宣告呼喊  (Display, Headline 用)
```

**关键约束**:
- 同一段文字内, 至多出现 2 种字重(读 + 强调)
- 700 极少需要 — 大多数"加粗"用 510-550 已够
- 中文不用 300 Light(笔画太细, 屏幕不可读)

## 5 个 Hierarchy Vectors(层级建立的 5 个手段)

不只字号建立层级, 5 个维度可同时使用:

| Vector | 例子 |
|---|---|
| **Scale** 字号 | Display vs Body |
| **Weight** 字重 | 600 vs 400 |
| **Spacing** 间距 | 标题上下 32px 留白 vs Body 16px |
| **Tracking** 字距 | 标题 -0.02em 紧凑 vs ALL CAPS +0.08em |
| **Alignment** 对齐 | 标题左对齐 vs 数据居中 |

**规则**: 一个 dominant 元素(最重要的信息), 至少 2 个 vectors 同向工作才算"突出"。只靠字号大不够 — 配合字重 + 留白才稳。

**反模式**:
- **Flat hierarchy**: 所有元素同 size 同 weight, 看不出主次
- **Noise hierarchy**: 多个元素都用 Display + 700, 互相抢夺注意力

## Letter-Spacing(字距)

字距是隐性层级工具, 用错会破坏阅读节奏:

```
Display 48-72px+:   letter-spacing: -0.02em ~ -0.03em  (大字收紧)
Headline 32-48px:   letter-spacing: -0.01em ~ -0.02em
Subtitle 24-32px:   letter-spacing: 0  (默认)
Body 16-22px:       letter-spacing: 0  (默认)
Caption 13-15px:    letter-spacing: 0.01em ~ 0.02em  (小字微撑开提可读)
ALL CAPS 任意尺寸:   letter-spacing: 0.06em ~ 0.1em  (强制撑开, 否则字母粘连)
```

依据: Bringhurst《The Elements of Typographic Style》§3.2.7。

## 行长(Line Length)

正文行长直接决定阅读舒适度。

```css
.long-content {
  max-width: 65ch;       /* 50-75 字符是大脑跳读舒适区 */
}
```

中文按字符宽度计算约 30-40 个汉字/行。超过 → 换行追溯困难; 短于 → 频繁换行打断节奏。

## 字体配对策略

### 原则
- 标题字体: 有性格, 让人记住(衬线、手写、几何无衬线均可)
- 正文字体: 干净可读, 不抢注意力
- 两者在气质上互补而非冲突

### 经典配对思路

| 标题气质 | 标题字体方向 | 正文字体方向 |
|---|---|---|
| 优雅/奢华 | Playfair Display, Cormorant | Source Sans 3, Lato |
| 现代/科技 | Syne, Clash Display, Outfit | DM Sans, Geist |
| 温暖/人文 | Fraunces, Literata | Nunito, Work Sans |
| 力量/冲击 | Bebas Neue, Anton | Barlow, Open Sans |
| 独特/实验 | Space Grotesk, JetBrains Mono | IBM Plex Sans |

**注意**: 避免 Inter 作为唯一字体, 它已成 AI 网页的 tell(参见 SKILL.md 反模式)。

### 中英混排

- 英文字体优先声明, 中文字体兜底
- 中文正文: Noto Sans SC(Google) 或 思源黑体(Adobe)— 唯一免费且字重齐全
- 中文标题: 如需更有性格, 考虑 ZCOOL 系列或商用授权的方正字体
- `font-family: 'Playfair Display', 'Noto Sans SC', sans-serif;`

## 字体颜色层级

用透明度建立层级, 而非用不同 hex:

```
主要文字(标题/正文):  rgba(0,0,0, 0.87)  或 #222
次要文字(副标题/描述): rgba(0,0,0, 0.60)  或 #666
辅助文字(时间戳/页码): rgba(0,0,0, 0.38)  或 #999
禁用/占位文字:         rgba(0,0,0, 0.26)  或 #bbb
```

暗色主题反转:
```
主要文字: rgba(255,255,255, 0.87)
次要文字: rgba(255,255,255, 0.60)
辅助文字: rgba(255,255,255, 0.38)
```

## 常见错误

- ❌ 同一页面出现 6+ 种字号 — 层级崩溃
- ❌ 字号用 `vw` 但不加 clamp — 小屏字过小不可读
- ❌ 用全大写英文做长段落 — 可读性极差
- ❌ 字重只用 Regular 和 Bold — 缺中间层(510-550 是关键)
- ❌ 中文用 Light(300) 字重 — 笔画太细, 屏幕上不可读
- ❌ 行高统一用 1.5 — Display 级别大字 1.5 显得松散
- ❌ 一个标题加粗一个标题斜体, 一个加红色一个加大字号 — 层级 vectors 用太多, 互相抢夺
- ❌ 用 Inter 作为唯一字体 — AI 网页通用 tell, 缺辨识度
