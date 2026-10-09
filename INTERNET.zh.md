# 🌐 AI Agent 联网速查表（中文版）

> 命令来源：[Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach)（2026-10-09 逐条核对 README）。
> 定位：它是个"能力层"——替你选好、装好、体检好各平台当前最稳的接入方式，接入方式换代了你不用操心。

---

## 0. 安装：一句话

把这句复制给你的 Agent（Claude Code / Cursor / OpenClaw / Windsurf，任何能跑命令行的 Agent）：

```
帮我安装 Agent Reach：https://raw.githubusercontent.com/Panniantong/agent-reach/main/docs/install.md
```

几分钟后它就能读推特、搜 Reddit、看 YouTube、刷小红书。已装过要更新，换这句：

```
帮我更新 Agent Reach：https://raw.githubusercontent.com/Panniantong/agent-reach/main/docs/update.md
```

先预览不改系统：`agent-reach install --dry-run`

---

## 1. 零配置即用（装完直接用，不用登录）

| 平台 | 命令 / 用法 | 说明 |
|---|---|---|
| 任意网页 | `curl https://r.jina.ai/目标URL` | Jina Reader，免费免 Key，抓回来是干净文本 |
| YouTube | `yt-dlp --write-subs --write-auto-subs --sub-langs "zh.*,en.*" --skip-download "视频URL"` | 提取字幕给 Agent 读，"这个视频讲了什么"就靠它 |
| GitHub 公开仓 | `gh repo view owner/repo` | 读仓库简介/README；搜代码用 `gh search` |
| B站 | `bili search "关键词"` | 无需登录可搜可读详情（yt-dlp 已被B站风控封，改走 bili-cli） |
| RSS/Atom | `python3 -c "import feedparser; d=feedparser.parse('RSS地址'); print([e.title for e in d.entries[:5]])"` | 订阅更新，Agent 定时拉 |
| V2EX | 零配置渠道 | 热门帖、节点帖、帖子详情+回复，直接让 Agent 用 |
| 雪球 | 零配置渠道 | 股票行情、搜股票、热门帖子、热股排行 |
| 全网搜索 | Exa 语义搜索（MCP 接入，免 Key） | 安装时自动配，"搜一下 LLM 框架对比"走这里 |

---

## 2. 登录后解锁（告诉 Agent 一句话，它引导你配）

| 平台 | 解锁方式 | 能干什么 |
|---|---|---|
| Twitter/X | 告诉 Agent「帮我配 Twitter」，Cookie-Editor 手工导出 Cookie | 读单条推文→搜推文、刷时间线、读长文 |
| Reddit | OpenCLI（桌面）或 `rdt-cli` | 匿名接口已被封，必须登录态：搜帖+读帖+评论 |
| 小红书 | OpenCLI（复用你已开的 Chrome 会话） | 搜索、阅读、评论；Agent 不替你登录 |
| Facebook | OpenCLI（桌面浏览器登录态） | 搜索、主页、Feed、群组列表 |
| Instagram | OpenCLI（桌面浏览器登录态） | 用户搜索、Profile、最近帖子、Explore |
| LinkedIn | Jina Reader 读公开页；配后走专用 MCP | Profile 详情、公司页、职位搜索 |
| GitHub 私有仓 | 告诉 Agent「帮我登录 GitHub」 | 读私有仓、提 Issue/PR、Fork |

---

## 3. 体检与维护

```bash
agent-reach doctor              # 每个渠道通不通、当前走哪个后端、坏了怎么修，一条命令全告诉你
agent-reach install --dry-run   # 安装前预览，不改系统
agent-reach uninstall           # 卸载：清 ~/.agent-reach/（token/cookie）、skill 文件、MCP 配置
agent-reach uninstall --keep-config  # 只删 skill，保留 token（重装用）
```

**核心心智模型：** 每个平台 = "首选 + 备选"的有序后端列表。某条路被平台封了，换列表顺序就行——`doctor` 永远告诉你现在走的是哪条。

---

## 4. Agent 实战场景（复制改改就能用）

| 场景 | 渠道组合 | 一句话做法 |
|---|---|---|
| 舆情监控 | Twitter/X + 小红书 | 每天定时搜产品名，Agent 汇总成 5 行简报 |
| 技术调研 | YouTube 字幕 + B站 + GitHub | 扒 3 个视频字幕+2 个仓库 README，让 Agent 写对比报告 |
| 竞品追踪 | GitHub releases + RSS | 订阅对手仓库 release，更新了推送通知你 |
| 行业动态 | LinkedIn 职位 + 雪球热帖 + V2EX | 每周扫一遍，Agent 提炼 3 条值得看的 |
| 客服知识库 | Jina Reader 抓文档页 | 把帮助文档全抓下来，喂给你的 RAG/客服 Agent |

---

## 5. 安全红线

- **Cookie 平台用小号**：Twitter、小红书等走 Cookie/登录态调用，有被平台检测封号的风险——务必用专用小号，别用主号（原仓安全建议）。
- **凭据只存本地**：Cookie/Token 存在 `~/.agent-reach/config.yaml`，权限 600，不上传不外传。
- **默认不改系统**：`agent-reach install` 默认只检查环境；只有你显式加 `--system` 才会装依赖、写配置。

---

*上游变化快，命令以原仓 README 为准，有疑问先跑 `agent-reach doctor`。*
