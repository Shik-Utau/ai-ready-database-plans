# 四类主动操作：MatCreator 体验原型

[下载单文件 HTML](https://raw.githubusercontent.com/Shik-Utau/ai-ready-database-plans/codex/share-explicit-operations-prototype/docs/prototypes/explicit-operations/index.html) · [查看源码](index.html) · [发布来源与指纹](provenance.json)

点击下载链接后，保存为 `aidb-prototype.html`，用浏览器打开。也可在 GitHub 的 index.html 文件页选择 Download raw file。GitHub 文件页显示源码，不直接运行页面；无需 Node、Python、AIDB、服务器、登录或网络连接。

## 从这里开始

顶部选“1 四类连起来体验”，按聊天底部橙色按钮依次保存、查询、选中、查看、导出、修改和删除。一键发送完整请求，执行步骤自动出现在聊天中。宽窗口显示 MatCreator 三栏；窄窗口采用上下布局。

另外四组场景：备注会不会被重新导入覆盖、导出缺了什么、删除后旧选择失效、零命中与数据库故障。可以自由点击各类别的按钮，也可以在结果卡中选记录，查看完整字段，下载页面生成的样例 JSONL 或体验记录。刷新会重置本页内存。

## 反馈什么

对应 OpenSpec 变更 [plan-aidb-three-flows](../../../openspec/changes/plan-aidb-three-flows/proposal.md)，具体参照[主动操作规格](../../../openspec/changes/plan-aidb-three-flows/specs/aidb-explicit-operations/spec.md)和[设计阻塞项](../../../openspec/changes/plan-aidb-three-flows/design.md) B1、B3、B5。

反馈请写明场景、按钮顺序、看到的结果、希望的行为，必要时附页面导出的体验记录。重点讨论：重新导入是否应保留备注，导出缺单位如何反馈，删除范围包含什么，以及由谁提供可核对的完成证据。原型发布或 PR 合并不代表上述问题已决定。

## 真实与模拟

数据来自既有 Si 样本及一次隔离实验的 16 个事件。已观察：JSONL 出口缺少部分应力／维里语义标签、重导入覆盖备注、旧 ID 导出实际 0 条。页面的聊天、调度、数据库及自由操作均为内存模拟；点按钮不会调用真实 AIDB、执行计算或修改用户数据库。实际调用详情是固定记录，不是当前点击的新运行。

本次只发布自包含审阅附件和必要演示值，没有上传用户数据库、原始 VASP 文件、凭据或生产实现。个人绝对路径已替换为占位标识，展示命令不能直接复制执行。没有在本次发布时重跑数据库实验；宿主集成、任意导入格式、并发恢复、完整字段和业务职责仍不能据此认定通过。
