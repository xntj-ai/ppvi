# PPVI — PinPin Visual Identity

> Claude Code skill: 一套经过实战验证的设计美学方法论。让 AI 做出**有审美**的网页 — 不是"加到好看"，而是"减到刚好"。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code skill](https://img.shields.io/badge/Claude%20Code-skill-blueviolet.svg)](https://claude.com/claude-code)

---

## 是什么

Claude Code 自带的设计能力已经很强，但出来的页面有"通用 AI 美学"的味道：Inter 字体 + 紫色渐变 + 白底 + 大圆角。零辨识度。

**PPVI** 是张拼拼·XNTJ 在自己日常分享中沉淀出来的视觉系统，封装成一个 Claude Code skill。装上之后，所有 AI 生成的网页都按这套方法论生产，既保留 Claude Code 的技术力，又有自己的审美骨架。

> 设计的本质不是加法，是选择。每一个像素都是一次审美决策。

---

## 五条核心原则

| # | 原则 | 一句话 |
|---|------|--------|
| 1 | 克制优雅 | 每个视觉元素必须有存在理由,问不出理由就删掉 |
| 2 | 灰阶为基 | 灰阶是画布,颜色是标点 — 彩色 ≤ 15% |
| 3 | 严格层级 | 5 级字号系统,跨级 ≥ 1.4× 比例,级内一致 |
| 4 | 玻璃拟态 | 用光/透明度/层叠创造空间纵深感 |
| 5 | 密度呼吸 | 信息密度和呼吸感的精确平衡 |

外加两条执行规则（响应自适应 + 图示穿插），完整方法论见 [`SKILL.md`](SKILL.md)。

---

## 跟 frontend-design 的关系

- **`frontend-design`** = 怎么写 — 技术执行（代码、动画、Tailwind）
- **`ppvi`** = 怎么想 — 审美决策（为什么选这个颜色、这个间距、这个字重）

两者互补。Claude Code 同时装上，让技术力和审美力联手。

---

## 安装

把整个 `ppvi/` 文件夹放到 `~/.claude/skills/` 下：

```bash
git clone https://github.com/xntj-ai/ppvi.git ~/.claude/skills/ppvi
```

Claude Code 启动时会自动加载，触发场景见 `SKILL.md` frontmatter 的 `description` 字段。

---

## 何时触发

需要建立视觉系统、定义 UI 风格、面对"好看但说不清为什么好看"的设计决策时,Claude Code 会自动启用这套方法论。

**不适合**:
- 纯技术实现问题 → 用 [`frontend-design`](https://github.com/anthropics/skills)
- 品牌 logo 设计 → 需要专门的 brand identity 流程
- 印刷设计 → PPVI 面向屏幕显示,不覆盖 CMYK

---

## 沉淀来源

张拼拼·XNTJ 日常用 Claude Code 做分享网页（约 20+ 期视频每期一个网页 + 5 个 demo 站），从 2025 年 11 月到 2026 年 5 月迭代出这套方法论。**EP0022 视频** 完整讲了这套 skill 的逻辑：

→ [xntj.tv/ep/live-ep0022](https://xntj.tv/ep/live-ep0022/)

---

## 文件结构

```
ppvi/
├── SKILL.md                 # 五条核心原则 + 反模式总纲
├── references/              # 详细执行手册
│   ├── visual-principles.md      # 克制优雅
│   ├── color-philosophy.md       # 灰阶为基
│   ├── typography-system.md      # 严格层级
│   ├── glassmorphism-recipe.md   # 玻璃拟态配方
│   ├── spatial-density.md        # 密度呼吸
│   ├── responsive-layout.md      # 响应自适
│   └── chart-catalog.md          # 图示穿插
└── demo/
    └── index.html           # PPVI 视觉系统实战示例
```

---

## License

MIT — 用、改、商用都可以,credit 张拼拼·XNTJ 即可。
