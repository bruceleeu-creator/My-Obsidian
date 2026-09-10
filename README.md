# BruceW(Obsidians) · Bruce 的知识库

Bruce 的 Obsidian 库，按**防弹笔记法**组织：日志是入口，收件箱随手扔，ACT 三步分流（任务 / 知识 / 目标）。Mac 库与 Windows 库共用这套结构，双远程备份。

## 目录结构

```
vault 根
├── Claudian.md/      系统文档（AGENT.md 协作上下文）+ 模板
├── 知识卡片/         raw（素材箱，乱丢）/ wiki（知识库，提炼后）
├── 任务/
│   ├── 日志/         每日日志（系统入口）
│   └── 周任务/       每周任务清单
├── 目标/十二周周期/   12 周周期目标（当前 2026-Cycle-3）
├── 执行2026/         周计划执行表 md 归档（AGENT.md 格式）
├── 创作区/           开发灵感 / 研究
└── Agent手册/        定时任务 / 工作流研发 / 错误整理
```

系统约定（协作流程、数据结构、Git 细则）**以 [Claudian.md/AGENT.md](Claudian.md/AGENT.md) 为准**，新会话先读它。

## 📤 上传方式（GitHub + Gitea 双远程，两个都要推）

本库配了**两个远程，提交后两个都要推**，缺一个都不算备份完成：

| 远程名 | 地址 | 用途 |
|--------|------|------|
| `origin` | https://github.com/bruceleeu-creator/My-Obsidian.git | GitHub 主备份（公开仓库） |
| `gitea` | https://3cc7xt.site:8443/team/Bruce-Obsidian.git | 自建 Gitea 备份（腾讯云轻量服务器，nginx 反代 HTTPS；2026-09-01 起弃用旧地址 `http://49.232.160.7:3000`） |

> 查看远程：`git remote -v`。注意 Gitea 是自建服务器，**不是** gitee.com。

### 日常完整流程（每次提交做全 6 步）

```bash
# 1. 查看改动
git status

# 2. 暂存（.claudian/、workspace*.json、database.sqlite 已在 .gitignore，永不手动加）
git add -A

# 3. 提交（conventional commits + 中文描述）
git commit -m "feat: 本次改了什么"

# 4. 推送 GitHub
#    Windows：优先走默认代理；Clash 没开（报 via 127.0.0.1）就去代理直连重试
git push origin main
git -c http.proxy= -c https.proxy= push origin main   # Clash 未开时用这行
#    Mac：需绕 Clash 代理，用这个写法
git -c http.proxy= -c https.proxy= push origin main

# 5. 推送 Gitea（2026-09-01 起走域名 HTTPS）
git push gitea main

# 6. 确认两边都到位
git ls-remote gitea main
git ls-remote origin main          # Windows 直接查
git -c http.proxy= -c https.proxy= ls-remote origin main   # Mac 去代理查
```

### ⚠️ Windows 推 GitHub 的坑（2026-09-10 更新）

这台 Windows 机器的网络现状：
- 首选 `git push origin main` 走默认代理（Clash `127.0.0.1:7892`）
- **Clash 没开**时 push 报 `Failed to connect ... via 127.0.0.1`——改用去代理直连：`git -c http.proxy= -c https.proxy= push origin main`（9/10 实测直连**间歇可用**，失败多试几次或先把 Clash 开起来）
- 库内与全局配置里的死代理已于 9/10 清理；若日后直连又不通，`git config --global http.proxy http://127.0.0.1:7892` 加回来即可

### 换机 / 双机同步

```bash
git pull origin main    # 拉最新（Mac 端可能需同样去代理写法）
# ...改完按上面 6 步推双远程
```

- pull 到冲突（两边改了同一文件）：解决后 `git add -A && git commit`，再分别 `git push origin main` + `git push gitea main`
- Gitea 推送失败：确认用的是新域名地址（旧 IP:3000 已于 2026-09-01 废弃）；服务器 ping 通但端口不通 = Gitea 服务或 nginx 反代挂了，SSH 上去查
- GitHub 推送失败：报 `via 127.0.0.1` = Clash 没开，改去代理直连；直连超时则开 Clash 再试

### 提交规范

- conventional commits 前缀 + 中文描述：`feat / fix / docs / refactor / chore`
- 例：`feat: W35 收口归档 + W36 开学过渡周计划`
- 一个 commit 只干一件事

### 🔒 隐私红线（GitHub 是公开仓库！）

- `.claudian/`、`.DS_Store`、`.obsidian/workspace*.json`、`database.sqlite` 已被 .gitignore 排除，**永不手动 `git add`**
- 笔记内容禁止出现密码 / 密钥 / 身份证 / 手机号等敏感信息
- 拿不准的内容先问 Bruce 再提交

## 数据结构速查

| 文件 | 命名 | 关键 frontmatter |
|------|------|-----------------|
| 日志 | `YYYY-MM-DD` | `week: "[[2026-W36]]"`、`type: log` |
| 周任务 | `YYYY-Www` | `cycle: "[[2026-Cycle-3]]"`、`type: weekly` |
| 周期 | `YYYY-Cycle-N` | `start/end/status: active` |
| raw 素材 | `YYYY-MM-DD 随便写` | `type: raw` |
| wiki 知识 | `主题名` | `type: wiki` + 分类标签 |
