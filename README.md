# v0ui_skill

> 一个类似 v0 的前端约束 Skill，用于生成现代、干净、可落地的 React / Next.js / Tailwind / shadcn UI。

## 简介

`v0ui_skill` 提供 `v0-frontend-constraints` Skill。

它的目标不是复制 v0，而是复用 v0 背后的有效约束方式：让 AI 编码助手在更窄、更稳定的前端设计空间里工作，优先使用现有设计系统、组件原语、Tailwind token、响应式布局、完整交互状态和浏览器验证。

这个 Skill 适合用在：

- 从零生成前端页面或 Web 应用
- 重构或美化已有页面
- 构建 SaaS、后台、CRM、管理端、设置页、表单、表格、仪表盘
- 需要 React、Next.js、Tailwind、shadcn/ui 风格约束的场景
- 希望 AI 输出减少“随机现代感”和“AI 味 UI”的场景

## 安装

在支持 Skills 的编码助手中安装：

```bash
npx skills add skyyewen/v0ui_skill
```

安装后即可通过 `@v0ui`、`$v0ui` 或直接点名 `v0-frontend-constraints` 来触发。

## 使用方式

```text
@v0ui 帮我做一个订阅数据看板
```

```text
$v0ui 用 shadcn/ui 和 Tailwind 重做这个设置页
```

```text
Use v0-frontend-constraints to build this frontend.
```

## 主要约束

- 如果项目已有技术栈，优先遵守现有技术栈和目录结构
- 如果没有现成栈，默认偏向 React / Next.js / TypeScript / Tailwind CSS
- 优先使用 shadcn/ui、Radix、lucide-react 或项目内已有组件
- 吸收 v0 prompt 中适合真实项目的输出契约：完整代码、先规划结构、可访问性、媒体、依赖和运行限制
- 用 token 控制颜色、间距、圆角、边框、阴影和字体层级
- SaaS、后台、CRM、内部工具默认走紧凑、克制、可扫描的产品界面
- 表单、表格、弹窗、导航、设置项必须包含合理状态和交互反馈
- 避免随机渐变、装饰圆球、嵌套卡片、单一色系堆叠和文字溢出
- 完成前需要检查桌面端和移动端渲染效果

## 与 v0 prompt 的关系

这个 Skill 会参考 v0 prompt 里有价值的通用约束，例如完整可运行代码、shadcn/ui 优先、Tailwind token、lucide-react、语义化 HTML、ARIA、`sr-only`、图片 alt、响应式设计和实现前规划。

它不会照搬 v0 平台专用规则，例如 MDX code block 元数据、强制单文件、强制默认导出 `Component`、`/placeholder.svg`、Vercel Blob-only 图片规则、无条件禁止 fetch 或无条件禁止 dynamic import。

## 目录结构

```text
v0ui_skill/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    └── v0-frontend-rules.md
```

## 文件说明

- `SKILL.md`：Skill 主入口，负责触发条件和执行流程
- `references/v0-frontend-rules.md`：详细前端约束规则，是实际执行时的规则来源
- `agents/openai.yaml`：OpenAI Agent 界面展示元数据

## 适合的调用方式

当你希望 AI 做出的前端更接近 v0 的稳定现代感时，可以直接说：

```text
用 @v0ui 做这个页面
```

或者：

```text
用 v0-frontend-constraints 约束这个前端实现
```

## License

MIT
