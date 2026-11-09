# AI-ready Database Plans

独立的 AI-ready Database 计划书与规格讨论仓库，使用 OpenSpec 组织提案。维护规划文档及明确授权的可交互审阅附件，不包含 MatCreator / AIDB 生产实现或用户数据库。

## 体验主动操作原型

[查看说明与下载入口](docs/prototypes/explicit-operations/README.md)：MatCreator 风格的精简主动操作，主流程为查询、备注、导出结构，另有独立保存入口。点击按钮代替自然语言输入。下载 HTML 后用浏览器打开即可，无需安装或登录。页面是内存模拟，含演示所需的 Si 数值；不连接真实数据库。GitHub 文件页显示源码，不会直接运行 HTML。

## 从这里阅读

当前提案：**三条 AIDB 业务线的统一规划**。状态：讨论稿；文档齐备不代表业务已批准或代码已实现。

1. [提案：目的、范围与审阅问题](openspec/changes/plan-aidb-three-flows/proposal.md)
2. 行为要求：[主动操作](openspec/changes/plan-aidb-three-flows/specs/aidb-explicit-operations/spec.md) · [计算前查询](openspec/changes/plan-aidb-three-flows/specs/aidb-precompute-lookup/spec.md) · [计算后采集](openspec/changes/plan-aidb-three-flows/specs/aidb-result-collection/spec.md)
3. [设计方向与阻塞决策](openspec/changes/plan-aidb-three-flows/design.md)
4. [后续任务与验收准备](openspec/changes/plan-aidb-three-flows/tasks.md)
5. [来源与证据限制](docs/source-notes.md)

首版从已有讨论提炼；只明确已有方向，未定问题保持可见，未迁移原任务的认领与状态。

## 如何一起修改

- 在本仓库开分支，用 PR 修改计划书；评论请指出具体段落、建议行为和例子。
- 提案文件中“讨论稿 / 已接受 / 已替代”是团队审阅状态；Git 合并本身不表示所有业务方向已接受。
- 飞书适合快速讨论，采纳的结论通过 PR 整理进本仓库；记录来源版本和确认范围。
- 实现发生在另行确定的代码仓库，通过链接关联。本仓库不自动触发实现或发布。
- 具体约定见 [审阅与交接流程](docs/review-workflow.md)。

## 本地查看与校验

GitHub 可以直接阅读，无需安装工具。编辑者可安装 OpenSpec（首版使用 1.16.1），在本仓库根目录执行：

```bash
openspec list
openspec status --change plan-aidb-three-flows
openspec validate plan-aidb-three-flows --strict
```

status 的文档完成状态仅表示所需文件已存在；validate 仅检查规格格式，不代表方向、实现或测试已通过。

本仓库以 `--tools none` 初始化，没有绑定某个 AI 工具的生成技能。后续需要时可在克隆目录选择自己的工具；不要让 apply 将本计划仓库当作实现目标。

## 目录

- `openspec/changes/`：仍在讨论或推进的提案。
- `openspec/specs/`：当前保留为空；不把草案同步成已接受主规格。
- `docs/`：审阅流程与来源摘要。
