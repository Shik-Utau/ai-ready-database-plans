# MatCreator 主动操作审阅原型

[下载单文件 HTML](https://raw.githubusercontent.com/Shik-Utau/ai-ready-database-plans/codex/share-explicit-operations-prototype/docs/prototypes/explicit-operations/index.html) · [查看源码](index.html) · [来源与指纹](provenance.json)

下载后用浏览器打开。页面以按钮代替文字输入，默认从空库开始，也可以选择已有记录。查询、保存、结构交付和记录维护均可自由体验。右栏可展开异常示例。

## 这轮请确认

1. **入库条件和回执**。先看「查看保存条件」。保存需要可读取的稳定 VASP XML、末态结构和双收敛；回执展示实际保存条数、记录 ID 和读回字段。试「缺力标签（模拟）」，看能否清楚区分结果已入库与 E+F 帧数为 0。
2. **查询摘要和详情**。先保存 Si 结果，再点「查金刚石相 Si · 300 K MD」。严格查询为 0 条，主动放宽为纯 Si 后可看到弛豫末帧候选。请确认摘要能否看出覆盖及缺口，以及展开后能否核对结构、采样、标签方法与单位、磁性及来源。

页面使用一条既有 Si 弛豫末帧的隔离库快照和明确标注的缺力模拟。查询条件、覆盖统计和写入在浏览器内演示，刷新重置。POSCAR 为候选结构交付格式；同源重复保存暂按保留备注演示。

Edge 已核对缺文件或未收敛、缺力仍可保存、严格查询和显式放宽、详情、下载及窄屏。相关规则仍待审阅。详见[主动操作规格](../../../openspec/changes/plan-aidb-three-flows/specs/aidb-explicit-operations/spec.md)和[设计](../../../openspec/changes/plan-aidb-three-flows/design.md)。
