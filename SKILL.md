---
name: ppvi
description: "PinPin Visual Identity — 一套经过实战验证的设计美学方法论。核心：克制优雅、灰阶为基、严格字体层级、玻璃拟态纵深、信息密度呼吸。Use when: 用户需要设计审美指导、建立视觉系统、定义 UI 风格、或面对'好看但说不清为什么好看'的设计决策。NOT for: 纯技术实现问题（用 frontend-design）、品牌 logo 设计、印刷设计。"
---

# PinPin Visual Identity 方法论

> 设计的本质不是加法，是选择。每一个像素都是一次审美决策。

## 与 frontend-design 的关系

- `frontend-design` = **怎么写**（技术执行：代码、动画、Tailwind）
- `ppvi` = **怎么想**（审美决策：为什么选这个颜色、这个间距、这个字重）
- 两者互补：ppvi 做审美判断，frontend-design 做技术落地

## 五条核心原则

### 1. 克制优雅 — Less, but deliberate

好设计不是"加到好看"，是"减到刚好"。

- 每个视觉元素必须有存在理由，问不出理由就删掉
- 装饰 ≠ 美。一个精心选择的渐变 > 十个随意的阴影
- **反面清单**: 渐变彩虹色、随机阴影叠加、无理由的圆角变化、为动画而动画

详见 [references/visual-principles.md](references/visual-principles.md)

### 2. 灰阶为基 — Color is punctuation, not prose

灰阶是画布，颜色是标点。大面积用灰阶建立层次，色彩只用在需要注意力的地方。

- 背景色域: #fafafa → #f5f5f5 → #e0e0e0（微妙的灰度梯度）
- 彩色占比 ≤ 15%，作为点缀而非主体
- 一个主色 + 一个强调色足矣，不需要"调色盘"

详见 [references/color-philosophy.md](references/color-philosophy.md)

### 3. 严格层级 — Every size has a reason

字体不是"大中小"，是有严格定义的 5 级系统。跨级使用，级内一致。

| 级别 | 用途 | 参考尺寸 | 字重 |
|------|------|----------|------|
| Display | 封面大标题 | 96-120px | 700 |
| Headline | 区块标题/数据大字 | 48-72px | 700 |
| Subtitle | 副标题/卡片标题 | 28-32px | 600 |
| Body | 正文/列表 | 18-22px | 400 |
| Caption | 辅助信息/页码 | 13-15px | 400 |

- 单视图字号数量上限: 5 个(用满 5 级即可,不再叠加)
- 跨级比例 ≥ 1.4x,同级保持一致
- 字号用 `clamp()` fluid 定义,防压缩时字过小(下限:中文 Body ≥16px,Caption ≥13px)
- 强调用三权重(400 读 / 510-550 强调 / 590-700 宣告),不用字号变化
- 层级 5 个 vectors(Scale/Weight/Spacing/Tracking/Alignment)至少 2 个同向才算 dominant

详见 [references/typography-system.md](references/typography-system.md)

### 4. 玻璃拟态 — Depth through light

玻璃效果不是"加个模糊"，是用光、透明度、层叠创造空间纵深感。

- 三层结构: 背景层（暗/纹理）→ 玻璃层（半透明 + 模糊）→ 内容层（清晰文字）
- 模糊值: 32-64px（轻度毛玻璃到深度雾化）
- 噪点叠加: SVG noise filter，opacity 0.03-0.08，增加质感
- 暗底 + 亮玻璃 > 亮底 + 暗玻璃（前者层次更分明）

详见 [references/glassmorphism-recipe.md](references/glassmorphism-recipe.md)

### 5. 密度呼吸 — Every pixel of whitespace is intentional

不是"留白越多越好"，是信息密度和呼吸感的精确平衡。

- 内容区域紧凑但不拥挤，留白区域宽敞但不空洞
- 相关元素紧密，无关元素远离（格式塔亲近性）
- 卡片内 padding 紧凑（12-16px），卡片间 gap 宽松（24-32px）
- 滚动条、分隔线、边框 — 越少越好，用间距代替线条

详见 [references/spatial-density.md](references/spatial-density.md)

## 扩展能力

5 条核心原则之外,以下两类执行规则补足实战短板:

### 响应自适 — Layout breathes with container

容器宽度变化时,字号、列数、间距应优雅过渡而非硬切。

- 字号用 `clamp()` 定义,设绝对下限(中文 Body ≥16px / Caption ≥13px)
- 组件用**容器查询**(`@container`)而非媒体查询,按自己容器自适应
- 中文换行三件套: `word-break: keep-all` + `overflow-wrap: anywhere` + `text-wrap: balance`
- Grid 用 `repeat(auto-fit, minmax(280px, 1fr))` 自动减列,卡片设 `min-width: 0`

详见 [references/responsive-layout.md](references/responsive-layout.md)

### 图示穿插 — Diagram, don't paragraph

逻辑/数据用图表表达,不堆段落和 bullet。

- 11 类图表 catalog: Time-Series / Gap / Before-After / Donut / Investment / Timeline / Comparison / 2×2 / Benchmarking / Waterfall / Cover
- 图表标题 MUST 假设驱动 (e.g. "时序一致性成为关键差异",不是"AI 视频模型对比")
- 单图表信息密度上限: 折线 ≤12 数据点 / 饼 ≤6 块 / 表格 ≤7×5 / 流程图 ≤7 步
- 颜色规则: 单系列用主色 + 灰阶,强调单点时全图灰阶仅强调点用主色

详见 [references/chart-catalog.md](references/chart-catalog.md)

## 审美决策框架

面对设计选择时，按此优先级判断：

1. **有存在理由吗？** — 没有就删掉（克制优雅）
2. **层级清晰吗？** — 用户能在 0.5 秒内找到最重要的信息（严格层级）
3. **色彩克制吗？** — 彩色只出现在需要注意力的地方（灰阶为基）
4. **有纵深感吗？** — 界面不是平的，有前后关系（玻璃拟态）
5. **呼吸感对吗？** — 紧的地方够紧，松的地方够松（密度呼吸）

## 反模式（绝对避免）

### 视觉
- ❌ 渐变彩虹背景 — 没有审美判断的堆砌
- ❌ 所有元素等大等重 — 没有层级就没有设计
- ❌ 随机圆角（8px/12px/16px 混用）— 圆角值应统一或有明确规则
- ❌ 为炫技的动画 — 动画是为了传达信息层级和状态变化
- ❌ 纯白大面积背景 — 用 #fafafa 或带微妙纹理,纯白太刺眼
- ❌ 用边框分隔一切 — 间距和背景色差异是更优雅的分隔方式
- ❌ 通用 AI 审美 — Inter + 紫色渐变 + 白底 = 零辨识度

### 排版与自适应
- ❌ 单视图 6+ 种字号 — 层级崩溃
- ❌ 字号用 `vw` 没 clamp — 小屏字小到不可读
- ❌ 中文用英文换行规则 — 出现"句首逗号"等版式问题
- ❌ Grid 不设 `min-width: 0` — minmax 失效,长内容撑爆卡片
- ❌ 用断点(@media)硬切字号 — 应用 clamp 渐变

### 信息表达
- ❌ 长段落不用图表辅助 — 逻辑/数据用图示,不堆 bullet
- ❌ 图表标题描述性而非假设驱动 — 标题应是结论,不是话题
- ❌ Excel 默认样式直接搬 — 网格、刻度、图例都要重设
- ❌ 装饰性 emoji bullet 作图标 — 用文字或同源 SVG icon
