# 玻璃拟态实操配方

## 玻璃效果的本质

玻璃拟态不是"加 blur"。它是用光学隐喻创造空间层次 — 让用户感知到"这个面板浮在内容上方"。

三个必要条件：
1. **半透明** — 能看到背后的东西（否则就是普通面板）
2. **模糊** — 背后的东西是虚化的（建立前后关系）
3. **背景有内容** — 纯色背景上做玻璃效果没意义（没东西可虚化）

## 三层架构

```
┌─────────────────────────────┐
│  Layer 3: 内容层              │  文字/图标，清晰锐利
│  ┌───────────────────────┐  │
│  │ Layer 2: 玻璃层         │  │  半透明 + 模糊 + 微噪点
│  └───────────────────────┘  │
│  Layer 1: 背景层              │  暗色/渐变/图片/纹理
└─────────────────────────────┘
```

## 实现配方

### 基础玻璃

```css
.glass-panel {
  /* 半透明底色 */
  background: rgba(255, 255, 255, 0.08);

  /* 模糊 — 核心效果 */
  backdrop-filter: blur(40px);
  -webkit-backdrop-filter: blur(40px);

  /* 边框增强玻璃边缘感 */
  border: 1px solid rgba(255, 255, 255, 0.12);

  /* 圆角 */
  border-radius: 16px;
}
```

### 进阶：多层渐变玻璃

```css
.glass-premium {
  background:
    linear-gradient(
      135deg,
      rgba(255, 255, 255, 0.12) 0%,
      rgba(255, 255, 255, 0.05) 50%,
      rgba(255, 255, 255, 0.02) 100%
    );
  backdrop-filter: blur(64px);
  -webkit-backdrop-filter: blur(64px);
  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: 16px;

  /* 顶部高光 — 模拟光源 */
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.1),
    0 8px 32px rgba(0, 0, 0, 0.3);
}
```

### 噪点纹理叠加

纯净的玻璃效果会显得"塑料感"。加微量噪点增加质感：

```css
.glass-textured::before {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: inherit;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.05'/%3E%3C/svg%3E");
  pointer-events: none;
  z-index: 1;
}
```

噪点 opacity 参考值：
- 0.03 — 几乎不可见，仅在大面积时有感
- 0.05 — 恰到好处，有质感但不粗糙
- 0.08 — 明显的磨砂感，适合暗底

## 参数调节指南

### 模糊值 (backdrop-filter: blur)

| 值 | 效果 | 适用场景 |
|----|------|---------|
| 8-16px | 轻微虚化，背后内容可辨 | 导航栏悬浮 |
| 24-40px | 中度模糊，背后有形无色 | 卡片、面板 |
| 48-64px | 深度雾化，仅保留色调 | 大面积覆盖、模态 |

### 透明度 (background rgba alpha)

| 值 | 效果 |
|----|------|
| 0.03-0.05 | 几乎全透明，仅靠模糊区分层 |
| 0.08-0.12 | 标准玻璃，最常用 |
| 0.15-0.25 | 半磨砂，内容不太可穿透 |

### 暗底 vs 亮底

**暗色背景 + 亮色玻璃**（推荐）：
```css
body { background: #0a0a0a; }
.glass { background: rgba(255, 255, 255, 0.08); }
```

**亮色背景 + 暗色玻璃**（慎用，容易脏）：
```css
body { background: #f0f0f0; }
.glass { background: rgba(0, 0, 0, 0.05); }
```

暗底 + 亮玻璃的层次感天然更强，因为光源隐喻更自然（玻璃反射光线）。

## 背景处理

玻璃效果依赖背景。背景越丰富，玻璃效果越好看。

### 背景方案

1. **暗色 + 渐变色块** — 最安全
```css
body {
  background: #0a0a0a;
  /* 添加色彩光斑 */
}
body::before {
  content: '';
  position: fixed;
  width: 600px; height: 600px;
  background: radial-gradient(circle, rgba(75, 63, 114, 0.3), transparent 70%);
  top: -200px; right: -100px;
}
```

2. **图片 + 暗化覆盖** — 最有氛围
```css
body {
  background: url('bg.jpg') center/cover;
}
body::after {
  content: '';
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.6);  /* 0.5-0.7 暗化 */
}
```

3. **暗边缘（暗角）** — 聚焦视觉中心
```css
body::after {
  background: radial-gradient(
    ellipse at center,
    transparent 40%,
    rgba(0, 0, 0, 0.35) 100%
  );
}
```

## 常见错误

- ❌ 白色背景上做玻璃 — 没有对比，效果不可见
- ❌ blur 值 < 8px — 看起来像 bug，不像设计
- ❌ 玻璃层太多（3层以上嵌套）— 模糊叠加变成灰糊糊
- ❌ 忘记 `-webkit-backdrop-filter` — Safari 需要前缀
- ❌ 玻璃面板内放复杂背景 — 玻璃层的内容应该简洁，复杂度留给背景层
