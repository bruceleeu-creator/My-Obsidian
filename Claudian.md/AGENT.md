---
type: agent-context
updated: 2026-08-30
---

# AGENT.md — Bruce × Claudian 协作上下文

> 新会话先读这个文件，快速上岗。系统细节与约定都在本文件。

## 👤 用户档案
- 称呼：Bruce（可以叫 bro）
- 交流语言：中文，口语化，别端着
- 工作：前端开发（周任务里全是利润表、发票溯源、合同拆分这类活）
- 双库环境（共用同一套防弹笔记法 + 同一套远程仓库：GitHub + Gitea 双远程，2026-08-19 起统一）：
  - **Mac 库**：`~/Desktop/学习知识库/Bruce（MacObsidian）`
  - **Windows 库**：`C:\Users\Administrator\Desktop\BruceW(Obsidians)`
- 本文件两个库共用：Claudian 在哪个库运行，就在哪个库执行，内容以本文件约定为准

## 🏗️ 当前系统：防弹笔记法（2026-08 建成）
**核心**：日志收件箱 + ACT 三步分流
- **A** 任务 → [[任务/周任务/README|周任务]]（每周一篇 `2026-W36`）
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

> 另有保留文件：`执行2026/`（周计划执行表 md 归档，随仓库备份）、`周计划执行表/`（原 HTML 周计划，已归档为 md）——与 ACT 结构共存，不冲突。

## 🤝 协作约定
1. **流程**：先提问澄清 → 需求/设计文档 → 执行计划 → 执行（Bruce 确认后再动手）
2. **README**：每个文件夹都要有，用简单口语中文
3. **文档**：系统文档集中在 `Claudian.md/`（AGENT.md + 模板），改动系统后同步更新本文件
4. **Git**：内容有更新就 commit + push **双远程都要推**——GitHub（`origin`）+ Gitea（`gitea`）——**细则见下方「📤 双远程备份细则」，必读必守**
5. **模板**：3 个（日志/周任务/周期），放 `Claudian.md/模板/`；周任务模板的 `cycle` 链接每周期要换

## 📤 双远程备份细则（GitHub + Gitea，所有协作者必守）

本库配了**两个远程，提交后两个都要推**（2026-08-30 起按此执行）：

| 远程名 | 地址 | 用途 |
|--------|------|------|
| `origin` | https://github.com/bruceleeu-creator/My-Obsidian.git | GitHub 主备份（**公开**仓库） |
| `gitea` | http://49.232.160.7:3000/team/Bruce-Obsidian.git | 自建 Gitea 备份（腾讯云轻量服务器） |

> 查看远程：`git remote -v`。注意 Gitea 是**自建服务器**，不是 gitee.com。

### 完整步骤（每次提交都要做全）
1. **查看改动**：`git status`（确认改了哪些文件）
2. **暂存**：`git add -A`（⚠️ 永不手动加 `.claudian/`、`workspace*.json`、`database.sqlite`——已在 .gitignore）
3. **提交**：`git commit -m "<type>: <中文描述>"`，type 用 `feat / fix / docs / refactor / chore`
4. **推送 GitHub**：
   - **Windows**：`git push origin main` ——直接走默认代理即可；**不要加 `-c http.proxy= -c https.proxy=` 去代理**，这台机器直连 GitHub 443 不通，去代理的命令必失败（2026-08-30 实测）
   - **Mac**：`git -c http.proxy= -c https.proxy= push origin main`（Mac 需绕 Clash 代理）
5. **推送 Gitea**：`git push gitea main` ——直连服务器 IP 的 http 地址，正常情况直接推
6. **确认成功**：`git status` 显示工作区干净 = 本地已提交；再看两边远程都到位：
   - `git -c http.proxy= -c https.proxy= ls-remote origin main`（Mac 去代理查；Windows 直接 `git ls-remote origin main`）
   - `git ls-remote gitea main`

### 分支说明
- 两个远程都只用 `main` 一个分支
- 换机 / 双机同步：先 `git pull origin main` 拉最新（Mac 端可能需要同样去代理写法），改完按上面步骤推双远程
- pull 到冲突（两边改了同一文件）：解决冲突后 `git add -A && git commit`，再分别 push 两个远程
- Gitea 推送失败先查网络 / 服务器状态（49.232.160.7 是腾讯云轻量服务器）；GitHub 推送失败先确认没去掉代理

### 提交规范
- conventional commits 前缀 + 中文描述，写清楚改了什么：
  - `feat: 新增知识卡片栏目（raw 素材箱 + wiki 知识库）`
  - `docs: 关系图谱打通（笔记 ↔ 知识卡片 ↔ Claudian.md 双向链接）`
  - `refactor: 移除原子卡片 + MOC 体系`
- 一个 commit 只干一件事，别把无关改动混在一起

### 🔒 隐私红线（公开仓库！）
- `.claudian/`（插件会话隐私）、`.DS_Store`、`.obsidian/workspace*.json`、`database.sqlite`（Obsidian 本地数据库）已被 .gitignore 排除——**永远不要手动 `git add` 它们**
- 笔记内容禁止出现密码 / 密钥 / 身份证 / 手机号等敏感信息
- 拿不准的内容先问 Bruce 再提交

## 📐 数据结构速查
| 文件 | 命名 | 关键 frontmatter |
|------|------|-----------------|
| 日志 | `YYYY-MM-DD` | `week: "[[2026-W36]]"`、`type: log` |
| 周任务 | `YYYY-Www` | `cycle: "[[2026-Cycle-3]]"`、`type: weekly` || 周期 | `YYYY-Cycle-N` | `start/end/status: active` |
| raw 素材 | `YYYY-MM-DD 随便写` | `type: raw` |
| wiki 知识 | `主题名` | `type: wiki` + 分类标签 |

## 🧭 当前状态（2026-08-30 快照）
- **Cycle-3** active，仅剩收官一周：本周 **W36**（8/31-9/6，开学过渡周），9/7 起 Cycle-4；9/6 周日做周期收官复盘
- 上周 W35 已归档（8/30）：三系统部署上线 ✅、合同拆分/利润宝云端优化 ✅、账号隔离+后台管理 ✅、安全盘点+整改计划成文（执行待确认）；硅行业 🚫 暂缓待老板过稿；影子机器人换模型 ⏳ 顺延 W36
- 本周 W36 主题：开学过渡 + 行业面板内容更新（新工作任务）+ 发票溯源续更（服务器 OCR + 密钥存储）——见 [[任务/周任务/2026-W36|2026-W36]] 与 [[执行2026/2026-W36 周计划执行表|W36 执行表]]；开发任务全部**弹性模式**（有空就干，没空顺延）
- 单词卡立项（W36 新项目，8/31-9/6 弹性调研）：基于 Anki 开源，见 [[创作区/开发灵感/单词卡开发灵感]]
- 双远程备份启用（2026-08-30）：GitHub（`origin`）+ Gitea（`gitea`）**两边都要推**，Windows 推 GitHub 必须走默认代理（去代理必失败）——细则见上方「📤 双远程备份细则」
- 关系图谱已打通（笔记 ↔ 知识卡片 ↔ Claudian.md 双向链接，6 组 colorGroups 按类型上色）
- 双库共用仓库（2026-08-19 起）：Mac + Windows 均推同一仓库 main

## 📌 待办 / 未决
- [x] 仪表盘：已确认不重建（`00-仪表盘.md` 已删，git 无历史）
- [x] **wiki 第一波分类**：2026-08-19 完成（开发工作方式 + 开源效率工具集 2 张卡）
- [x] Dataview 渲染：Windows 库重启后确认正常（8/19）
- [x] Windows 库重启验证：日记生成到 `任务/日志/` 且带模板、模板命令面板、关系图谱上色、Dataview 均正常（8/19）
- [ ] 评分表行 1 有异常值 `7`（5 分制）——待 Bruce 确认清掉
- [ ] 双库共用 main 后，Mac 库 pull 验证（主题 / 插件列表变化，Obsidian Nord vs AnuPpuccin）——2026-08-19 待 Mac 端确认
- [ ] 🔒 **安全整改（已计划，暂不执行，执行前需 Bruce 确认）**：① Obsidian 内相关 API key 存储方式全部删除（涉及 7 个项目）；② GitHub 端相应整改（git 历史泄漏密钥清理 / .gitignore 复查）——清单见 [[任务/周任务/2026-W35|W35 整改清单]]

## 🗑️ 已知已删/不再使用
- `防弹笔记法.md` — 2026-08-19 删除（系统信息已并入本文件）
- `卡片/`（原子卡片 + MOC）— 2026-08-19 移除
- `原子卡片模板.md`、`MOC模板.md` — 已删
- `00-仪表盘.md`、`00-dataview诊断.md` — 已删（无 git 历史）
- `周计划执行表/weekly-execution-plan.html.md`（空占位）— 2026-08-19 删除
