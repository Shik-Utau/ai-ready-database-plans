# MatCreator AIDB 交付集合

日期：2026-11-21。以 MatCreator `46737212860c53ca739c28ee02ac8db2a2fab7fc` 为基础，包含后续本地修复、独立维护的 `ai-ready-db` skill、固定版本 AIDB 运行源码、依赖锁与安装说明。接收方可以直接从完整源码包安装，无需取得原作者的 MatCreator 开发分支。

## 安装

在 Linux 或 WSL2 的 Bash 中操作。先准备 Git、[uv](https://docs.astral.sh/uv/getting-started/installation/) 和 Node.js >= 24.14.1（含 npm），确认这些命令在 PATH 中。Python 3.12 由 uv 准备。安装需访问 Python/npm 包源，以及固定版本的 `mat_agent_bench`、`mat_know_base` Git 依赖；有权限限制时使用自己的 Git 凭据。

```bash
git clone --branch codex/aidb-handoff-20261121 https://github.com/Shik-Utau/ai-ready-database-plans.git
cd ai-ready-database-plans/deliveries/matcreator-aidb-20261121
sha256sum -c SHA256SUMS
tar -xzf MatCreator-aidb.tar.gz
cd MatCreator-aidb
python3 script/install_aidb_handoff.py
source .handoff/env.sh
python script/check_aidb_handoff.py
```

自检使用临时数据库，不调用模型、不提交 VASP。应看到 `PASS`，其中包括空库查询、Si 原始输出归档、重复归档去重、按 ID 读回、EXTXYZ/POSCAR/HTML 导出。

再设置自己的模型：

```bash
matcreator config set llm.model=openai/你的模型名称
matcreator config set llm.base_url=https://你的接口地址/v1
```

在解压目录 `.handoff/home/config.yaml` 的 `llm.api_key` 中填写自己的密钥，然后运行：

```bash
bash script/start_aidb_handoff.sh
```

浏览器打开 <http://127.0.0.1:5174/>。API、Web 后端分别使用 8100、8101。每次新开终端执行自检或配置前，先进入解压目录并 `source .handoff/env.sh`。启动脚本会自动加载默认运行目录；Ctrl+C 停止服务。

已有配置和数据库会保留；安装程序在替换修改过的 skill 前，先备份到 `.handoff/backups/`。保留原有 MatCreator 基线，在这里使用独立运行目录。

## 正常对话验收

确认新对话使用解压目录下 `.handoff/workspace` 的绝对路径。安装已将 `AI_READY_DB_CONFIG` 指向独立空库，若需显式绑定，向对话提供 `.handoff/aidb-config.json` 的实际绝对路径。

1. 「查询当前 AIDB 中化学式为 Si 的记录。」应为 0 条。
2. 「请把 aidb-demo/si-pbe-relax 中已经完成的 VASP 弛豫结果保存到 AIDB，告诉我读回的记录 ID。」
3. 「查询化学式为 Si、使用 PBE 且有逐原子力的记录。」应有 1 条，为 8 个 Si 原子，末帧总能量约 −43.38227814 eV/cell。
4. 点击详情与导出，或要求「将这条记录导出为 EXTXYZ、POSCAR 和完整详情 HTML」。
5. 再次要求保存同一目录，核对返回已有记录且 ID 不变。

以上不运行新的 VASP。新计算另外需要配置计算后端、项目、镜像、资源和有权使用的 POTCAR。自动自检、正常模型对话与真实付费计算是不同验证范围，见 [验证记录](VALIDATION.md)。

## 文件与版本

| 文件 | 用途 |
| --- | --- |
| `MatCreator-aidb.tar.gz` | 完整、已提交的应用源码树；含安装器、内置 skill、AIDB skill 和运行包、前端、样例、说明 |
| `matcreator-from-4673721.patch` | 相对指定基线的完整补丁，供审阅或应用到干净的同一基线；新安装直接用源码包即可 |
| `runtime-manifest.json` | 原安装 skill 的哈希、AIDB 来源及包内 234 个交付文件的哈希 |
| `manifest.json`、`SHA256SUMS` | 应用源码提交、固定依赖来源与当前交付件的 SHA-256 |
| `VALIDATION.md` | 已执行检查、证据范围及剩余的接收方验收 |

应用源码提交 `2342173cd6bccfb3cb2334e0fad861da9c4a5ca6`，AIDB 运行源码固定到 `008e881676c12fe2028200c944cc8bd99fabbdfb`。源码包不含应用 Git 历史、个人密钥、材料库、会话、虚拟环境、模型权重或 POTCAR。原仓库约 385 MB 的 LFS 数据对象仅保留指针，本次安装不需要下载它。

解压后进一步阅读：

- `MatCreator-aidb/docs/aidb-handoff.md`：安装、配置、skill 加载顺序和文件管理。
- `MatCreator-aidb/docs/aidb-vasp.md`：正式功能使用说明。
- `MatCreator-aidb/docs/aidb-vasp-examples.md`：可复制的对话样例。
- `MatCreator-aidb/docs/aidb-implementation/ticket14.md`：原真实计算与回放验收矩阵。

## skill 修改怎样进入下一次交付

运行时 skill 在解压目录 `.handoff/home/skills/ai-ready-db/`，不由本仓库跟踪。确认需要发布的修改后，同步回应用源码中的 `delivery/skills/ai-ready-db/`；内置 VASP skill 则位于 `src/matcreator/skills/vasp-pymatgen/`。然后运行 `python3 script/update_aidb_handoff_manifest.py`、重新验证、重新打包并更新本目录校验清单。

同名 skill 按内置 → official → 用户 → workspace 的顺序使用先发现者；workspace 并不覆盖内置 skill。安装的 AIDB skill 独立维护，不能用数据库仓库中的同名 skill 整包覆盖。实际部署使用真实目录，避免符号链接被加载器忽略。重新安装后重启正在运行的服务。

本交付目录是用户明确指定的分发位置。既有 OpenSpec 仍保留原讨论状态，不以本次交付改写旧提案的接受、归档或完成状态。
