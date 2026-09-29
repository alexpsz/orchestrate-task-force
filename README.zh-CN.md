# Orchestrate Task Force

[English](README.md) | 简体中文

在 Codex Desktop、Claude Code 或 Google Antigravity 中，通过可见负责人任务、会话或子代理，共享侧栏分组或工作区隔离（宿主支持时），以及随工作变化的并发来协调独立工作。未请求独立任务时，核心也支持当前任务内有明确范围的内部助手。

这是一个纯指令技能，不需要额外服务、控制台或强制运行台账。它使用当前宿主实际提供的能力，默认保留用户的模型设置。

## 使用

需要可见负责人任务和分组时，提交：

> 使用 `$orchestrate-task-force` 协调本次请求。为独立工作包创建或复用左侧可见的独立负责人任务，并将它们与本协调任务放入同一个命名侧栏分组。根据当前容量和冲突调整并发，在授权范围内验证集成后的整体结果。

宿主支持时，默认提示词会提供这段请求。请检查实际提交的文字：仅提及技能名称不等于请求新建任务。只需只读审计时请明确说明；只需内部助手时，请明确要求保留在当前对话中处理。

在 Claude Code 中，在 `/orchestrate-task-force` 后提交同样的请求；其中负责人任务对应会话，侧栏分组对应自定义分组。Claude 也可能根据描述自动加载本技能，但这绝不授权新建会话或助手。在桌面应用中，新的可见会话可能以建议卡片的形式出现，点击后才会启动。

在 Google Antigravity 中，提交：

> 使用 `$orchestrate-task-force` 协调本次请求。为独立工作包派发可见子代理，使用合适的工作区隔离（branch 用于文件系统隔离，或 share 配合核验独立的检出目录/互不冲突的写入范围），在辅助面板中展示并附带会话链接，并在授权范围内验证集成后的整体结果。

继续同一编排时，可以这样请求：

> 继续使用现有负责人任务和侧栏分组。应用修订后的要求，保留不受影响的工作，并验证集成后的整体结果。

协调者会核验真实任务身份和分组成员。创建仍在排队不代表任务已经就绪。分组失败时保留已有任务；缺少所需可见任务能力时说明限制，不用隐藏助手替代。

## 保留的原则

- 每个冲突写入范围只有一个负责人；独立写者可以并行。
- 根据依赖、容量和资源压力动态调度，不固定任务数或写者数。
- 尽可能由原负责人处理修正，拒绝基于过期要求的结果。
- 交接或明显上下文中断前留下简短恢复摘要，继续时与实时状态核对。
- 工作者做定向检查，集成验收覆盖每一项当前要求。
- 明确报告未完成工作和仍占用的资源。

## 模型与宿主支持

默认不启用任何模型或推理强度预设。保留用户选择和宿主默认值，仅在有具体推理需要且权限允许时调整设置。[GPT-6 Astra 推理强度预设](references/astra-effort-preset.md) 为可选项。要启用它，请明确请求：“对新工作者使用 GPT-6 Astra 推理强度预设。”主任务的现有设置保持不变。

[Codex 适配说明](references/codex-profile.md) 使用实际可用的原生工具处理可见任务和分组。[Claude 适配说明](references/claude-profile.md) 覆盖 Claude Code：子代理作为有明确范围的内部助手并使用工作树隔离，桌面会话作为可见负责人，并使用自定义侧栏分组。[Antigravity 适配说明](references/antigravity-profile.md) 覆盖 Google Antigravity：子代理作为内部助手或可见负责人并使用工作区隔离（`Workspace: "branch"` 提供物理工作区隔离；`Workspace: "share"` 需核验独立的检出目录或使用互不冲突的文件范围），辅助面板追踪，以及可选的脑部产物。Astra 预设不适用于 Claude 或 Antigravity 宿主。其他宿主可以使用核心原则，但其可见任务与侧栏能力须现场确认。模型名称或推理强度标签不会赋予工具、权限或额外容量。

## 安装与阅读

将完整文件夹复制到宿主支持的技能位置。当前 Codex 文档列出的用户技能位置是 `~/.agents/skills/orchestrate-task-force`，仓库技能位置是 `.agents/skills/orchestrate-task-force`。已有被识别的安装应保留原位，避免重复安装。参见[官方安装说明](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills)。当前 Claude Code 文档列出的个人技能位置是 `~/.claude/skills/orchestrate-task-force`，项目技能位置是 `.claude/skills/orchestrate-task-force`，参见 [Claude Code 技能文档](https://code.claude.com/docs/en/skills)。

Google Antigravity 主要以独立技能方式安装：作为用户技能安装于 `~/.gemini/config/skills/orchestrate-task-force`（或 `~/.agents/skills/orchestrate-task-force`），或作为项目技能安装于 `.agents/skills/orchestrate-task-force`，参见[官方自定义说明](https://antigravity.google/docs/customizations)。若作为 Antigravity 插件包安装于 `~/.gemini/config/plugins/orchestrate-task-force/`，`plugin.json` 需位于插件根目录，而技能及其相对引用文件放在嵌套的 `skills/` 目录下：

```text
orchestrate-task-force/
├── plugin.json
└── skills/
    └── orchestrate-task-force/
        ├── SKILL.md
        ├── references/
        └── evals/
```

- [SKILL.md](SKILL.md)：英文规范核心。
- [Codex 适配说明](references/codex-profile.md)：仅在使用 Codex 可见任务操作时阅读。
- [Claude 适配说明](references/claude-profile.md)：在 Claude Code 宿主上派发助手或会话、分组、发消息或调整配置前阅读。
- [Antigravity 适配说明](references/antigravity-profile.md)：在 Google Antigravity 宿主上派发子代理、使用工作区隔离或报告辅助面板状态前阅读。
- [可选 Astra 预设](references/astra-effort-preset.md)：仅在明确选择后阅读。
- [决策指南](references/decision-guide.md)：决策不清楚时阅读。
- [审查场景](evals/behavior-cases.md)：维护示例，不是运行性能结果。

本中文 README 翻译英文使用指南。参考文件和译文不能覆盖核心或更高优先级指令。私人项目数据、凭据和运行时 ID 不写入可复用文件和公开示例。

## 许可证

MIT
