---
type: agent-context
updated: 2026-08-19
---

# AGENT.md — Bruce × Claudian 协作上下文

> 新会话先读这个文件，快速上岗。系统细节与约定都在本文件。

## 👤 用户档案
- 称呼：Bruce（可以叫 bro）
- 交流语言：中文，口语化，别端着
- 环境：macOS · Obsidian vault 在 `~/Desktop/学习知识库/Bruce（MacObsidian）`
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

## 🤝 协作约定
1. **流程**：先提问澄清 → 需求/设计文档 → 执行计划 → 执行（Bruce 确认后再动手）
2. **README**：每个文件夹都要有，用简单口语中文
3. **文档**：系统文档集中在 `Claudian.md/`（AGENT.md + 模板），改动系统后同步更新本文件
4. **Git**：内容有更新就 commit + push 到 `https://github.com/bruceleeu-creator/My-Obsidian.git`——**细则见下方「📤 GitHub 备份细则」，必读必守**
5. **模板**：3 个（日志/周任务/周期），放 `Claudian.md/模板/`；周任务模板的 `cycle` 链接每周期要换

## 📤 GitHub 备份细则（所有协作者必守）

**仓库**：https://github.com/bruceleeu-creator/My-Obsidian.git（**公开**仓库）

### 上传 GitHub 完整步骤
1. **查看改动**：`git status`（确认改了哪些文件）
2. **暂存**：`git add -A`（⚠️ 永不手动加 `.claudian/`、`.DS_Store`、`workspace*.json`）
3. **提交**：`git commit -m "<type>: <中文描述>"`，type 用 `feat / fix / docs / refactor / chore`
4. **推送**：`git -c http.proxy= -c https.proxy= push origin main`
5. **确认成功**：`git status` 显示工作区干净 = 已同步；或 `git -c http.proxy= -c https.proxy= ls-remote origin` 查远程 main 的 hash

### 分支说明（当前状态）
- 仓库目前**只用 `main` 一个分支**，推送目标始终是 `origin main`
- 如果其他设备 / 协作者创建了新分支，需先合并到 main 再推送：
  1. `git branch -a` 查看全部分支
  2. `git merge <分支名>` 合并到当前分支
  3. 有冲突：解决后 `git add -A && git commit`
  4. 再按上面「完整步骤」推送
- 没有未推送提交时 `git status` 显示干净 / "up to date" = 已上传完毕

### ⚠️ 代理坑（必看，否则推送失败）
- 全局 git 配置了 `http.proxy = http://127.0.0.1:7890`（Clash 代理）
- **代理软件没开时**普通 `git push` 会报 `Failed to connect to 127.0.0.1 port 7890`
- 解法：推送命令临时加 `-c http.proxy= -c https.proxy=` 绕过（**不改全局配置**）；或先开代理再普通 push

### 提交规范
- conventional commits 前缀 + 中文描述，写清楚改了什么：
  - `feat: 新增知识卡片栏目（raw 素材箱 + wiki 知识库）`
  - `docs: 关系图谱打通（笔记 ↔ 知识卡片 ↔ Claudian.md 双向链接）`
  - `refactor: 移除原子卡片 + MOC 体系`
- 一个 commit 只干一件事，别把无关改动混在一起

### 🔒 隐私红线（公开仓库！）
- `.claudian/`（插件会话隐私）、`.DS_Store`、`.obsidian/workspace*.json` 已被 .gitignore 排除——**永远不要手动 `git add` 它们**
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

## 🧭 当前状态（2026-08-19 快照）
- **Cycle-3** active；本周 **W34**（8/17-8/23）
- P0 发票溯源 ✅；P1 利润表 🔄（8/19 流畅度 ✅，8/20 部署）；P2 合同拆分 🔄（8/19 提前修订 bug）
- 原子卡片 + MOC 体系已移除（2026-08-19），知识统一走 raw → wiki
- 关系图谱已打通（笔记 ↔ 知识卡片 ↔ Claudian.md 双向链接）

## 📌 待办 / 未决
- [x] 仪表盘：已确认不重建（`00-仪表盘.md` 已删，git 无历史）
- [ ] **wiki 第一波分类**：raw 攒够素材后，Claudian 分类整理
- [ ] 评分表行 1 有异常值 `7`（5 分制）——待 Bruce 确认清掉
- [ ] Dataview 渲染曾有问题（2026-08-18 诊断中，Bruce 重启后未回报结果）——若系统已正常显示可忽略
- [ ] git 提交身份是自动生成的 `BruceLeeu <bruceleeu@BruceLeeudeMac-mini-2.local>`——若需规范可配置 user.name/email

## 🗑️ 已知已删/不再使用
- `防弹笔记法.md` — 2026-08-19 删除（系统信息已并入本文件）
- `卡片/`（原子卡片 + MOC）— 2026-08-19 移除
- `原子卡片模板.md`、`MOC模板.md` — 已删
- `00-仪表盘.md`、`00-dataview诊断.md` — 已删（无 git 历史）
