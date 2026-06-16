# ppvi · PinPin Visual Identity

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE)
[![Claude Code Skill](https://img.shields.io/badge/Claude%20Code-Skill-d97757.svg)](https://claude.com/claude-code)

**A design-taste methodology that makes AI-built web pages look intentional — not "added until pretty," but "subtracted until right."**

**一套让 AI 做出有审美的网页的设计方法论 —— 不是"加到好看",而是"减到刚好"。**

ppvi (PinPin Visual Identity) is a [Claude Code](https://claude.com/claude-code) / Agent skill. It is not code — it is a way of thinking. Install it and every page Claude builds is produced under one taste framework: five core principles, a dark/light dual system, and full-screen / half-screen / mobile adaptation. It keeps Claude Code's engineering power and adds a visual backbone of its own, so the output stops reading as generic AI aesthetic and starts reading as a deliberate visual identity.

ppvi(PinPin Visual Identity)是一个 [Claude Code](https://claude.com/claude-code) / Agent 技能。它不是代码,是一套"怎么想"的方法。装上之后,Claude 做出来的每一个页面都按同一套审美框架生产:五条核心原则、深浅双系统、全屏/半屏/手机自适应。它保留 Claude Code 的工程能力,再加一层属于自己的视觉骨架 —— 让输出不再是"通用 AI 美学",而是一套有意为之的视觉身份。

> Design is not addition, it's selection. Every pixel is an aesthetic decision.
>
> 设计的本质不是加法,是选择。每一个像素都是一次审美决策。

## Why ppvi · 为什么用 ppvi

Claude Code's built-in design ability is already strong, but left to itself the output carries the "generic AI aesthetic" tell: Inter font + purple gradient + pure-white background + big uniform rounded corners. Zero recognizability. The reason isn't a lack of skill — it's the absence of taste *constraints*. Anything is possible, so nothing is decided.

Claude Code 自带的设计能力已经很强,但放任不管,出来的页面有"通用 AI 美学"的味道:Inter 字体 + 紫色渐变 + 纯白底 + 一律大圆角,零辨识度。问题不在能力不够,而在缺少审美的*约束* —— 什么都能做,于是什么都没决定。

ppvi supplies the missing layer: a small set of hard rules, distilled over six months of real work, that turn "looks nice but I can't say why" into a checklist you can actually apply. It tells the model *why* this color, this spacing, this weight — so taste becomes reproducible instead of accidental.

ppvi 补上缺的那一层:一组在半年实战里沉淀出来的硬规则,把"好看但说不清为什么好看"变成一份能真正执行的清单。它告诉模型*为什么*选这个颜色、这个间距、这个字重 —— 让审美变得可复现,而不是碰运气。

## The five principles · 五条核心原则

| # | Principle · 原则 | In one line · 一句话 |
|---|---|---|
| 1 | **Restraint · 克制优雅** | Every visual element must justify itself; if it can't, delete it. 每个视觉元素必须有存在理由,问不出理由就删掉。 |
| 2 | **Grayscale base · 灰阶为基** | Grayscale is the canvas, color is the punctuation — color ≤ 15%. 灰阶是画布,颜色是标点 —— 彩色 ≤ 15%。 |
| 3 | **Strict hierarchy · 严格层级** | A 5-level type scale, ≥ 1.4× between levels, consistent within. 5 级字号系统,跨级 ≥ 1.4×,级内一致。 |
| 4 | **Glassmorphism · 玻璃拟态** | Use light, transparency and stacking to create real depth. 用光、透明度、层叠创造空间纵深感。 |
| 5 | **Density & breath · 密度呼吸** | The precise balance of information density and whitespace. 信息密度与呼吸感的精确平衡。 |

Two execution rules round out the field gaps — **responsive adaptation** (fluid `clamp()` type, container queries, Chinese line-breaking) and **diagram-don't-paragraph** (an 11-type chart catalog with hypothesis-driven titles). The full methodology, anti-patterns included, lives in [`SKILL.md`](./SKILL.md) and [`references/`](./references).

另有两条执行规则补足实战短板 —— **响应自适**(fluid `clamp()` 字号、容器查询、中文换行)与**图示穿插**(11 类图表 catalog,标题假设驱动)。完整方法论(含反模式)见 [`SKILL.md`](./SKILL.md) 与 [`references/`](./references)。

## When to use · 适用场景

Reach for ppvi whenever a design decision needs taste, not just code — building a visual system, defining a UI style, or facing a "looks good but I can't articulate why" call. It is the *judgement* layer; pair it with `frontend-design` for the *execution* layer.

当一个设计决策需要的是审美判断而不只是代码时,就用 ppvi —— 建立视觉系统、定义 UI 风格,或面对"好看但说不清为什么好看"的取舍。它是*判断*层;落地的*执行*层交给 `frontend-design`。

- **Good fit** — sharing pages, reports, dashboards, landing pages, posters; any artifact where the visual *is* the deliverable. **适合** —— 分享页、报告、仪表盘、落地页、海报;任何"视觉本身就是交付物"的产物。
- **Not for** — pure technical implementation (use [`frontend-design`](https://github.com/anthropics/skills)), brand logo design (needs a dedicated brand-identity process), or print / CMYK (ppvi targets screens). **不适合** —— 纯技术实现(用 [`frontend-design`](https://github.com/anthropics/skills))、品牌 logo 设计(需专门的 brand identity 流程)、印刷 / CMYK(ppvi 面向屏幕)。

## Install · 安装

Clone this repository into your Claude Code skills directory:

把本仓库克隆到你的 Claude Code 技能目录:

```bash
git clone https://github.com/xntj-ai/ppvi.git ~/.claude/skills/ppvi
```

That's the whole setup. Claude Code auto-loads the skill on start and triggers it on the scenarios in `SKILL.md`'s `description`. Nothing else to configure.

只需这一步。Claude Code 启动时自动加载,按 `SKILL.md` 的 `description` 场景触发,不必再配任何东西。

## Usage · 用法

**With Claude** — describe a visual task and ask for ppvi taste, e.g. *"use ppvi to design this report page,"* or *"apply ppvi and tell me why this layout works."* Claude runs the five-principle decision framework — does each element justify itself, is the hierarchy readable in 0.5s, is color restrained, is there depth, is the breathing right — and produces (or critiques) the design accordingly.

**对 Claude 说** —— 描述一个视觉任务并要求用 ppvi 的审美,比如"用 ppvi 帮我设计这个报告页",或"用 ppvi 审一下这个布局,告诉我为什么成立"。Claude 会跑那套五原则决策框架 —— 每个元素有理由吗、层级 0.5 秒内可读吗、色彩克制吗、有纵深吗、呼吸感对吗 —— 据此产出或挑刺。

ppvi is a *methodology*, so it has no template to run and no JSON to fill: its output is judgement applied to your design, expressed in whatever Claude is building (HTML/CSS, a React component, a report page). The `demo/` and `references/` are the worked examples and the executable handbook.

ppvi 是一套*方法论*,没有模板可跑、没有 JSON 要填:它的产物是把审美判断应用到你的设计上,体现在 Claude 正在做的东西里(HTML/CSS、React 组件、报告页)。`demo/` 与 `references/` 是实战范例与可执行手册。

## ppvi vs frontend-design · 与 frontend-design 的关系

The two are complementary, not competing. Install both and let engineering power and design taste work as one pair of hands.

两者互补,不是二选一。同时装上,让工程力与审美力当成一双手来用。

| | **ppvi** | **frontend-design** |
|---|---|---|
| Question · 管什么 | **How to think · 怎么想** | **How to write · 怎么写** |
| Layer · 层 | Aesthetic decisions · 审美决策 | Technical execution · 技术执行 |
| Answers · 回答 | Why *this* color / spacing / weight · 为什么选这个颜色 / 间距 / 字重 | How to code / animate / Tailwind it · 怎么写代码 / 动画 / Tailwind |
| Output · 产物 | A taste framework + checklist · 审美框架 + 清单 | Production-grade code · 可上线的代码 |

ppvi decides *what is right*; frontend-design makes it *real*. Run the design through ppvi's framework first, then hand the decisions to frontend-design to build.

ppvi 决定*什么是对的*,frontend-design 把它*变成真的*。先用 ppvi 的框架过一遍设计,再把决策交给 frontend-design 落地。

## Examples · 示例

[`demo/index.html`](./demo/index.html) — a single self-contained page that *is* the methodology rendered: the dark base, the `#d97757` single accent, glass panels, the strict five-level scale, and a side-by-side dark/light comparison. Open it in a browser to see every principle applied at once.

[`demo/index.html`](./demo/index.html) —— 一个自包含页面,本身就是这套方法论的实体:暗色基底、`#d97757` 单一强调色、玻璃面板、严格五级字号,以及深/浅双系统的并排对照。浏览器打开即可一次看全所有原则的落地。

The reference handbook in [`references/`](./references) carries the executable detail behind each principle — the exact grayscale ramp, the `clamp()` type tokens, the glass recipe, the chart catalog.

[`references/`](./references) 里的参考手册装着每条原则背后的可执行细节 —— 精确的灰阶梯度、`clamp()` 字号 token、玻璃配方、图表 catalog。

## FAQ · 常见问题

**Is ppvi code or a methodology?** A methodology. There's no library to import and no build step — it's a set of taste rules Claude reads and applies. The `demo/` is an illustration, not a runtime.

**ppvi 是代码还是方法论?** 方法论。没有库要导入、没有构建步骤 —— 它是一组 Claude 读了就照着做的审美规则。`demo/` 是示意,不是运行时。

**Does it replace frontend-design?** No — they sit on different layers. ppvi is *how to think* (taste), frontend-design is *how to write* (technique). Install both; ppvi judges, frontend-design builds.

**它会取代 frontend-design 吗?** 不会 —— 两者在不同层。ppvi 是*怎么想*(审美),frontend-design 是*怎么写*(技术)。同时装,ppvi 做判断,frontend-design 做落地。

**Dark or light?** Both. The skill defines a dark/light dual system; the demo defaults to dark (it shows depth most clearly) but ships a light scope for the comparison. Most of the xntj.tv sharing pages run light-mode ppvi.

**深色还是浅色?** 都有。技能定义了深/浅双系统;demo 默认暗色(纵深感最分明),但内置浅色作用域做对照。xntj.tv 的大部分分享页跑的是浅色 ppvi。

**Why does my AI page look "generic"?** Usually the tell stack: Inter as the only font, a purple gradient, a pure-white background, and random rounded-corner values. ppvi's anti-pattern list targets exactly these — see `SKILL.md`.

**为什么我的 AI 页面看着"通用"?** 通常是这套 tell:Inter 当唯一字体、紫色渐变、纯白底、随机圆角值。ppvi 的反模式清单针对的正是这些 —— 见 `SKILL.md`。

## Related · 相关

- [creator-analytics](https://github.com/xntj-ai/creator-analytics) — a self-media analytics → light-mode PPVI report-page skill; ppvi is its visual backbone. 自媒体数据分析 → 浅色 PPVI 报告页技能,ppvi 是它的视觉骨架。
- [flowmaker](https://github.com/xntj-ai/flowmaker) — single-HTML, drag-to-edit web flowcharts; its light glass look is built on ppvi. 单 HTML、可拖拽编辑的网页流程图,浅色玻璃风沿用 ppvi。
- [frontend-design](https://github.com/anthropics/skills) — Claude Code's official front-end skill; the *how to write* counterpart to ppvi's *how to think*. Claude Code 官方前端技能;ppvi 管"怎么想",它管"怎么写"。
- [xntj.tv](https://xntj.tv) — more Claude Code workflows and skills from 张拼拼 · XNTJ. 更多来自张拼拼·XNTJ 的 Claude Code 工作流与技能。

## License · 许可证

[MIT](./LICENSE) © [张拼拼 · XNTJ](https://xntj.tv)
