# AIDB 交付验证记录

验证日期：2026-11-21。基线 `46737212860c53ca739c28ee02ac8db2a2fab7fc`；应用整理分支 `codex/aidb-handoff-20261121`；对外交付仓库为 `Shik-Utau/ai-ready-database-plans` 的同名分支。本记录对应本分支交付文件，原主目录和 `aidb-pr` 的未提交内容保留。

## Git 外文件核对

对照 `workspace.py`、`skill.py`、个人部署与配置文档、AIDB 独立安装目录说明，以及原验收记录核对了四层 skill 来源。默认用户目录的 `ai-ready-db` 与 `aidb-acceptance`、`aidb-parity14`、`aidb-normal-chat-replay/h2o-corrected-live` 三个验收环境中的安装副本进行了逐文件哈希比对；用于本交付的文件一致。清单保留原始哈希，并单独记录交付修订后的哈希。

确认 AIDB 源码仓库中的同名 skill 存在另一组未提交修改，且独立安装说明明确要求不以它覆盖 MatCreator 的安装版。本交付使用实际安装版。AIDB 运行包、配置模板与构建元数据取自完整提交 `008e881676c12fe2028200c944cc8bd99fabbdfb` 的已跟踪文件，未夹带外部仓库未提交的 skill、个人数据或环境。

另核对了仓库 Git LFS 属性：`database/domain_datasets.tar.gz` 是约 385 MB 的 LFS 对象，本次安装和自检均未下载、未使用它。交付归档仅保留原 LFS 指针，安装说明标明实际数据需从原应用仓库按需获取。

## 安装与数据路径

- 在独立、起初为空的 `.handoff/.venv` 中实际运行安装脚本，安装锁定依赖、本地 MatCreator 和随附 AIDB，并完成 `npm ci` 和 Vite 生产构建。
- `uv pip check --python .handoff/.venv/bin/python` 通过，269 个运行依赖包一致。
- 新环境自检确认 MatCreator 来自交付 `src/`、AIDB 来自 `delivery/vendor/`、skill 来自独立 `home/skills/ai-ready-db` 的真实目录。
- 自检在临时库上完成空库查询、Si 真实输出归档、重复归档、条件查询、按 ID 读回和三种导出；ASE 读回 EXTXYZ 为 8 个原子、`(8, 3)` 力数组、−43.38227814 eV/cell 总能量。未使用原用户的材料库。
- 四项安装保护回归在交付新环境通过：保留配置和数据库内容、备份修改过的 skill、拒绝静默重建缺失 sidecar、替换不能被发现的 skill 符号链接、哈希校验拒绝缺失文件（相关条件合并在四个测试中）。
- 实际从 `start_aidb_handoff.sh` 启动服务，ADK `/list-apps`（8100）、Web `/api/health`（8101）、前端首页（5174）均返回 HTTP 200，随后关闭本次启动的进程组。

## 功能与文档回归

前端 `npm test`：229 项通过；Vite 构建成功，保留原有 MUI directive 与大 chunk 提示。

后端 `tests/aidb`、ADK 兼容、skill 路径和远程作业 skill 检查：首次运行 174 项通过、3 个子测试通过，1 项 VASP Batch Job 文档检查失败。该失败在原 `aidb-pr` 版本也能复现：参考文档缺少 CONTCAR 与原始日志的显式保留说明。交付补入按任务需要请求这些原始文件的说明，保留候选必须满足显式交付要求的规则。

补齐上述参考文档后，在交付新环境重跑远程作业 skill、安装保护、ADK 兼容和 skill 路径检查：44 项通过。激活交付环境会设置高优先级 `MATCREATOR_CONFIG_PATH`，因此配置路径测试也明确清除外层配置路径，确保真正使用其临时配置；生产配置优先级未改变。AIDB 全套中通过的计算、归档、复用和导出检查无需因文档修订重复执行。

文档 `mkdocs build --strict` 通过，新增链接与验收锚点已核对。交付 skill 通过 skill-creator 格式验证。外部 AIDB 快照逐字节匹配固定提交；应用整理提交跟踪全部 234 个 manifest 文件；本仓库以源码归档、补丁和 runtime-manifest 固定这些内容（不包含生成的运行状态）。

## 证据范围

本次验证覆盖安装、实际 skill 发现、真实本地 AIDB 与 VASP 原始文件处理、服务启动及自动回归。未借用原用户密钥驱动新的正常模型对话，未提交付费 VASP 作业。接收方填写自己的模型配置后，按解压后 `MatCreator-aidb/docs/aidb-handoff.md` 中的正常对话验收步骤检查模型路由；新计算另外需要可用的计算后端和输入。历史正常对话、真实计算与回放的区别继续以解压后 `MatCreator-aidb/docs/aidb-implementation/ticket14.md` 中的原验收矩阵为准。

## 本仓库交付包验证

从应用提交 `2342173cd6bccfb3cb2334e0fad861da9c4a5ca6` 的 Git 树生成带目录前缀的源码归档，核对全部 234 个内部哈希。基线补丁通过 `git apply --cached --check`，可用于干净的 `4673721` 基线。

将本仓库源码包解压到另一目录，在没有应用 `.git`、旧虚拟环境和开发者运行目录的条件下重新执行安装：锁定依赖安装、前端依赖安装与构建完成。新路径自检再次确认使用包内 MatCreator、AIDB 和真实 skill 目录；空查询、归档、重复归档、查询读回和三种导出全部通过。交付目录的校验文件也已重新生成。
