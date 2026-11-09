# MatCreator 主动操作：精简体验原型

[下载单文件 HTML](https://raw.githubusercontent.com/Shik-Utau/ai-ready-database-plans/codex/share-explicit-operations-prototype/docs/prototypes/explicit-operations/index.html) · [查看源码](index.html) · [来源与指纹](provenance.json)

保存为 `aidb-prototype.html`，用浏览器打开。GitHub 文件页只显示源码，也可点击 Download raw file。无需安装、登录或服务器，打开后可离线体验。

## 从这里开始

默认选择“使用已有记录”，点击橙色按钮依次查询 Si、选择备注、导出结构。在 Files 点击 `.vasp` 文件下载。顶部另有“保存已有计算结果”，从空库体验独立保存，再查询。

主界面只突出当前记录、备注和文件。执行过程与状态可展开，删除在记录详情内。已移除字段导出、JSONL 导出、故障开关及异常专项场景；异常研究证据仍保留在上一版 Git 历史中。

## 2026-11-09 反馈与边界

2026-11-09：用户接受师兄反馈中的 1、2、5：减少信息量、减少防御性功能展示、移除字段导出和 JSONL 导出。本版将默认体验收敛为查询 → 备注 → 导出结构；技术过程与状态折叠，故障开关和异常专项场景移出当前体验。删除保留在详情内。

POSCAR 是本版为结构导出选择的候选格式，尚不是用户确认的最终格式。主动查询 query 与保存 insert 分开；自动采集的触发覆盖仍由对应工单决定。本页不模拟自动导入。默认一条预置记录，另提供空库下主动保存的流程。

本版重复保存仅提示已存在，不执行覆盖，这是聚焦主流程的原型简化，不是已修复现有重导入覆盖备注问题。旧实验和旧版本仍作为历史证据保留，不因隐藏异常演示宣告问题解决。

数据来自已有 Si 导入快照。聊天、备注、删除和文件生成均在本页内存中；点击不会调用真实数据库，刷新会重置。POSCAR 只含晶格与原子坐标，不含备注、能量或力。未在这轮重新运行数据库实验。

已核对浏览器中的查询、备注、POSCAR 预览与下载，以及空库查询不导入、主动保存后再查询。该验证不代表宿主集成或业务验收通过。

对应 OpenSpec [主动操作规格](../../../openspec/changes/plan-aidb-three-flows/specs/aidb-explicit-operations/spec.md)和[设计](../../../openspec/changes/plan-aidb-three-flows/design.md)。请反馈主流程是否清楚、备注与结构交付是否满足用途；B1/B3/B5 其余事项仍待讨论。
