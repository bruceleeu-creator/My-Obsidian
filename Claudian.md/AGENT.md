---
type: agent-context
updated: 2026-08-19
---

# AGENT.md — Bruce × Claudian 协作上下文

> 新会话先读这个文件，快速上岗。系统细节与约定都在本文件。

## 👤 用户档案
- 称呼：Bruce（可以叫 bro）
- 交流语言：中文，口语化，别端着
- 环境：Windows · Obsidian vault 在 `C:\Users\Administrator\Desktop\BruceW(Obsidians)`
- 工作：前端开发（周任务里全是利润表、发票溯源、合同拆分这类活）

## 🏗️ 当前系统：防弹笔记法（2026-08 建成）
**核心**：日志收件箱 + ACT 三步分流
- **A** 任务 → [[任务/周任务/README|周任务]]（每周一篇 `2026-W34`）
- **C** 知识 → [[../知识卡片/raw/README|raw 素材箱]]（乱丢）→ 提炼成 [[../知识卡片/wiki/README|wiki 知识库]]（Claudian 分类整理）
- **T** 目标 → [[目标/十二周周期/README|十二周周期]]（`2026-Cycle-3`，W25-W36，2026-09-06 结束）

```
vault 根
├── Claudian.md/      系统文档 + 模板 + 本文件
├── 知识卡片/         raw（素材）/ wiki（知识）
├── 任务/
│   ├── 日志/         每日日志
│   └── 周任务/       周任务
└── 目标/十二周周期/    周期目标
```

> 本库另有保留文件：`执行2026/`（周计划执行表 md 归档，同步到 GitHub 备份）、`周计划执行表/`（原 HTML 周计划，已归档为 md）——与 ACT 结构共存，不冲突。

## 🤝 协作约定
1. **流程**：先提问澄清 → 需求/设计文档 → 执行计划 → 执行（Bruce 确认后再动手）
2. **README**：每个文件夹都要有，用简单口语中文
3. **文档**：系统文档集中在 `Claudian.md/`（AGENT.md + 模板），改动系统后同步更新本文件
4. **Git**：本库是**本地 git 仓库**（不推送远程），有内容更新就 commit——细则见下方「💻 Git 本地细则」
5. **模板**：3 个（日志/周任务/周期），放 `Claudian.md/模板/`；周任务模板的 `cycle` 链接每周期要换

## 💻 Git 本地细则（Windows 库专用）

**本库：本地 git 仓库，无远程。** 版本控制全靠本地 commit + obsidian-git 插件。

### 双库关系（Mac 库与 Windows 库）
| 库 | 位置 | git 模式 | 用途 |
|----|------|---------|------|
| Mac 库 | `~/Desktop/学习知识库/Bruce（MacObsidian）` | 推 GitHub 公开仓库 `bruceleeu-creator/My-Obsidian` | 云端备份 |
| **Windows 库（本库）** | `C:\Users\Administrator\Desktop\BruceW(Obsidians)` | **仅本地 commit** | 本地版本控制 |

两库结构一致（同一套防弹笔记法），内容分别维护。需要双机同步时手动对拷文件，**不共用远程仓库**（内容不同源，推同一仓库会冲突）。
> 例外：`执行2026/`（周计划执行表 md 归档）由 Windows 库维护，会手动同步到 Mac 库随其推送到 GitHub 做云端备份（2026-08-19 起）。

### 本地提交步骤
1. **查看改动**：`git status`（确认改了哪些文件）
2. **暂存**：`git add -A`（⚠️ 永不手动加 `.claudian/`、`workspace*.json`、`database.sqlite`——已在 .gitignore）
3. **提交**：`git commit -m "<type>: <中文描述>"`，type 用 `feat / fix / docs / refactor / chore`
4. **确认成功**：`git status` 显示工作区干净 = 已记录

### 提交规范
- conventional commits 前缀 + 中文描述，写清楚改了什么：
  - `feat: 新增知识卡片栏目（raw 素材箱 + wiki 知识库）`
  - `docs: 关系图谱打通（笔记 ↔ 知识卡片 ↔ Claudian.md 双向链接）`
  - `refactor: 移除原子卡片 + MOC 体系`
- 一个 commit 只干一件事，别把无关改动混在一起

### 🔒 隐私红线（本地仓库同样适用）
- `.claudian/`（插件会话隐私）、`.obsidian/workspace*.json`（窗口状态）、`database.sqlite`（Obsidian 本地数据库）已被 .gitignore 排除——**永远不要手动 `git add` 它们**
- 笔记内容禁止出现密码 / 密钥 / 身份证 / 手机号等敏感信息
- 拿不准的内容先问 Bruce 再提交

## 📐 数据结构速查
| 文件 | 命名 | 关键 frontmatter |
|------|------|-----------------|
| 日志 | `YYYY-MM-DD` | `week: "[[2026-W34]]"`、`type: log` |
| 周任务 | `YYYY-Www` | `cycle: "[[2026-Cycle-3]]"`、`type: weekly` |
| 周期 | `YYYY-Cycle-N` | `start/end/status: active` |
| raw 素材 | `YYYY-MM-DD 随便写` | `type: raw` |
| wiki 知识 | `主题名` | `type: wiki` + 分类标签 |

## 🧭 当前状态（2026-08-19 快照，与 Mac 库同步）
- **Cycle-3** active；本周 **W34**（8/17-8/23）
- P0 发票溯源 ✅；P1 利润表 🔄（8/19 流畅度 + UI 重构 ✅，8/20 部署）；P2 合同拆分 🔄（8/19 前端重构 + bug 修订 ✅）
- 原子卡片 + MOC 体系已移除（2026-08-19），知识统一走 raw → wiki
- 关系图谱已打通（笔记 ↔ 知识卡片 ↔ Claudian.md 双向链接，6 组 colorGroups 按类型上色）
- Windows 库已完成 ACT 结构改造（2026-08-19），数据与 Mac 库全量同步

## 📌 待办 / 未决
- [x] **wiki 第一波分类**：2026-08-19 完成（开发工作方式 + 开源效率工具集 2 张卡）
- [ ] 评分表行 1 有异常值 `7`（5 分制）——待 Bruce 确认清掉
- [x] Dataview 渲染曾有问题（Mac 库 2026-08-18 诊断中，Bruce 重启后未回报结果）——若系统已正常显示可忽略
- [x] git 提交身份是自动生成的 `BruceLeeu <...>`——若需规范可配置 user.name/email
- [x] Windows 库重启 Obsidian 后确认：日记生成到 `任务/日志/` 且带模板、模板命令面板可用、关系图谱按类型上色、Dataview 代码块正常渲染（2026-08-19 配置完毕待验证）

## 🗑️ 已知已删/不再使用
- `防弹笔记法.md` — 2026-08-19 删除（系统信息已并入本文件）
- `卡片/`（原子卡片 + MOC）— 2026-08-19 移除
- `原子卡片模板.md`、`MOC模板.md` — 已删
- `00-仪表盘.md`、`00-dataview诊断.md` — 已删（无 git 历史）
