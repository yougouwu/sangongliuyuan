# 🏛️ 三宫六院 · SanGongLiuYuan (OpenClaw Multi-Agent System)

<p align="center">
  <img src="https://img.shields.io/badge/OpenClaw-Required-blue?style=for-the-badge" alt="OpenClaw">
  <img src="https://img.shields.io/badge/Agents-22_Specialized-8B5CF6?style=for-the-badge" alt="Agents">
  <img src="https://img.shields.io/badge/Dashboard-Real--time-F59E0B?style=for-the-badge" alt="Dashboard">
  <img src="https://img.shields.io/badge/License-MIT-22C55E?style=for-the-badge" alt="License">
</p>

<p align="center">
  <strong>“在三宫六院系统中，9 个 Agent 不再是冰冷的 API 调用接口，而是生活在你的“赛博皇城”中、拥有独立人格与动态情绪的 “模拟 Agent (Sim-Agents)”，重构了 AI 多智能体协作架构。”</strong><br>
  借古制御新技：比 CrewAI 多一层<b>制度性审核</b>，比 AutoGen 多一个<b>赛博实时看板</b>。<br>
  特别感谢：<a href="https://github.com/cft0808/edict">cft0808/edict (Original Inspiration)</a>
</p>

<p align="center">
  <a href="#🎬-demo">🎬 看 Demo</a> ·
  <a href="#🚀-30-秒快速体验">🚀 30秒体验</a> ·
  <a href="#🏛️-架构全景">🏛️ 架构</a> ·
  <a href="#📋-储秀宫看板">📋 看板功能</a> ·
  <a href="docs/task-dispatch-architecture.md">📚 架构文档</a> ·
  <a href="README_EN.md">English</a>
</p>

---

## 🎬 Demo

<p align="center">
  <video src="docs/Agent_video_Pippit_20260225121727.mp4" width="100%" autoplay muted loop playsinline controls>
    您的浏览器不支持视频播放，请查看下方预览。
  </video>
  <br>
  <sub>🎥 <b>从下旨到回奏：</b> Whatsapp/QQ/飞书下旨 → 太子分拣 → 三宫规划 → 门下审议 → 六院执行 → 奏折回报</sub>
</p>

<details>
<summary>📸 点击展开 GIF 预览（加载更快）</summary>
<p align="center">
  <img src="docs/demo.gif" alt="三宫六院 Demo" width="100%">
</p>
</details>

---

## 🤔 为什么需要“三宫六院”？

大多数 Multi-Agent 框架（如 CrewAI/AutoGen）的逻辑是：*“你们几个 Agent 自己聊，聊完给我结果。”* **结果：** 过程黑盒、不可复现、质量全靠 LLM 发挥。

**三宫六院 (SanGongLiuYuan)** 将中国古代帝国的**分权制衡**具象化为 22 个 Agent：

| 特性对比 | CrewAI / AutoGen | **三宫六院 (OpenClaw)** | 赛博解读 |
| :--- | :---: | :---: | :--- |
| **审核机制** | ⚠️ 弱/无 | **✅ 门下省专职审核** | **封驳权**：方案不行直接打回，严禁盲目执行 |
| **实时监控** | ❌ 终端日志 | **✅ 储秀宫看板** | **临朝听政**：UI 实时流转，谁在干活一目了然 |
| **任务干预** | ❌ 无法停止 | **✅ 实时叫停/恢复** | **圣旨下达**：随时撤回或叫停正在运行的任务 |
| **执行审计** | ⚠️ 碎片化 | **✅ 完整奏折归档** | **起居注**：5阶段时间线，完整溯源每一个逻辑 |
| **配置热更** | ❌ 需重启脚本 | **✅ 看板一键切模型** | **册封大典**：运行时动态为 Agent 更换底层 LLM |

> **核心杀手锏：门下省封驳。** 不受制约的权力必然出错。在交付给“六院”执行前，必须经过严苛的逻辑审计。

---

## 🏛️ 架构全景



### 1️⃣ 核心国策 (Core Features) 
* 👑 **父皇 (huanghou):** 尔乃朕之眼目，守卫逻辑之重臣。门下省存在的唯一意义，就是替朕封驳一切庸才的废话。。
* ⚖️ **太子 (taizi):** 消息分拣。闲聊自动回复，唯有“旨意”才会创建任务。
* 👸 **皇后 (huanghou) :** 协理小太子，管理好东宫，重点是皇帝翻牌子、后宫妃嫔的养成、和皇帝的起居等。
* 🎛️ 翻牌子大屏 (Real-time Dashboard):** 沉浸式监控 9 位 Agent 的实时工作流转。谁在偷懒，谁在疯狂输出 Token，大屏上一目了然。支持拖拽式“翻牌子”直接唤醒指定 Agent。
* 💄 后宫养成 (Model Configuration):** 为不同的“宫院”赐配不同的灵魂。你可以精调每个 Agent 的 System Prompt（人设）和 Temperature（性格火候）。
* 📖 赛博起居注 (Full Audit Trails):** 敬事房特供功能。详细记录每一次 API 调用、上下文流转链路、以及 Token 消耗。一切“宫斗”（Agent 间的交叉验证与逻辑冲突）与“伴驾”（执行结果）皆有迹可循。

### 2️⃣ 三宫 - 中枢调度层 (Supervision)
* 👑 **东宫 (Router Agent):** 皇后。负责意图识别与任务分发。
* 🧠 **西宫 (Memory Agent):** 伴驾。负责长短期记忆管理与上下文注入。
* 🛡️ **中宫 (Security Agent):** 禁军。负责输出审核、防 Prompt 注入与合规拦截。

### 3️⃣ 六院 - 专职执行层 (Workers)
* ✍️ **翰林院 (Writer Agent):** 文案生成与文档编写。
* 🌐 **天机院 (Search Agent):** 联网检索与 RAG 知识库问答。
* 📊 **神算院 (Data Analyst):** 数据处理与可视化图表生成。
* 💻 **天工院 (Coder Agent):** 代码编写、架构设计。
* 🧐 **御史院 (Reviewer Agent):** 代码审查、逻辑纠错与“弹劾”。
* 🛠️ **神机院 (Tool-Use Agent):** 外部 API 调用与自动化操作。

---

## 📋 东宫看板 (10 大功能面板)

基于 React 18 + Python stdlib 构建的零依赖强大看板。

* **📋 旨意 Kanban:** 任务状态墙，心跳徽章（🟢活跃/🔴告警），支持实时操控。
* **📜 奏折阁 (Memorials):** 已完成任务自动归档，生成 Markdown 格式的正式奏折。
* **⚙️ 模型配置:** 运行时为 22 个 Agent 分别赐配模型（GPT-4/Claude/MiniMax等）。
* **🛠️ 技能配置:** 从官方 **Skills Hub** 一键增补远程技能，赋予 Agent 爬虫、代码审计等新能力。
* **📰 天下要闻:** 每日自动采集科技资讯，通过飞书推送，让“皇帝”尽知天下事。

---

## 🚀 30 秒快速体验

### A. Docker 一键体验 (Demo 模式)
```bash
docker run -p 7891:7891 cft0808/sangongliuyuan-demo
```
打开 http://localhost:7891 即可体验储秀宫看板。

<details>
<summary><b>⚠️ 遇到 <code>exec format error</code>？（点击展开）</b></summary>

如果你在 **x86/amd64** 机器（如 Ubuntu、WSL2）上看到：
```
exec /usr/local/bin/python3: exec format error
```

这是因为镜像架构不匹配。请使用 `--platform` 参数：
```bash
docker run --platform linux/amd64 -p 7891:7891 cft0808/sangongliuyuan-demo
```

或使用 docker-compose（已内置 `platform: linux/amd64`）：
```bash
docker compose up
```

</details>

### 完整安装

#### 前置条件
- [OpenClaw](https://openclaw.ai) 已安装
- Python 3.9+
- macOS / Linux

#### 安装

```bash
git clone https://github.com/yougouwu/sangongliuyuan.git
cd sangongliuyuan
chmod +x install.sh && ./install.sh
```

安装脚本自动完成：
- ✅ 创建全量 Agent Workspace（含太子/皇后/吏部/早朝，兼容历史 main）
- ✅ 写入各宫各院 SOUL.md（角色人格 + 工作流规则 + 数据清洗规范）
- ✅ 注册 Agent 及权限矩阵到 `openclaw.json`
- ✅ 构建 React 前端（需 Node.js 18+，如未安装则跳过）
- ✅ 初始化数据目录 + 首次数据同步
- ✅ 重启 Gateway 使配置生效

#### 启动

```bash
# 终端 1：数据刷新循环
bash scripts/run_loop.sh

# 终端 2：看板服务器
python3 dashboard/server.py

# 打开浏览器
open http://127.0.0.1:7891
```

> 💡 **看板即开即用**：`server.py` 内嵌 `dashboard/dashboard.html`，Docker 镜像包含预构建的 React 前端

> 💡 详细教程请看 [Getting Started 指南](docs/getting-started.md)

---

## 🏛️ 架构

```
                           ┌───────────────────────────────────┐
                           │          👑 皇帝/皇太后（你）       │
                           │     Feishu · Telegram · Signal     │
                           └─────────────────┬─────────────────┘
                                             │ 下旨
                           ┌─────────────────▼─────────────────┐
                           │          👑 太子 (taizi)           │
                           │    分拣：闲聊直接回 / 旨意建任务      │
                           └─────────────────┬─────────────────┘
                                             │ 传旨
                           ┌─────────────────▼─────────────────┐
                           │          👸 皇后 (huanghou)         │
                           │    协理：翻牌子、后宫妃嫔、皇帝起居    │
                           └─────────────────┬─────────────────┘
                                             │ 传旨
                           ┌─────────────────▼─────────────────┐
                           │     🏛️ 三宫 (qianqinggong)         │
                           │  接旨 → 规划 → 拆解子任务            │
                           └─────────────────┬─────────────────┘
                                             │ 提交审核
                           ┌─────────────────▼─────────────────┐
                           │          🔍 六院 (menxia)         │
                           │       审议方案 → 准奏 / 封驳 🚫      │
                           └─────────────────┬─────────────────┘
                                             │ 准奏 ✅
                           ┌─────────────────▼─────────────────┐
                           │          📮 众议院 (shangshu)       │
                           │     派发任务 → 协调六院 → 汇总回奏    │
                           └───┬──────┬──────┬──────┬──────┬───┘
                               │      │      │      │      │
                         ┌─────▼┐ ┌───▼───┐ ┌▼─────┐ ┌───▼─┐ ┌▼─────┐
                         │💰 翰林│ │📝 天机│ │⚔️ 神算│ │⚖️ 御史│ │🔧 神机│
                         │ 数据  │ │ 文档  │ │ 工程  │ │ 合规  │ │ 基建  │
                         └──────┘ └──────┘ └──────┘ └─────┘ └──────┘
                                                               ┌──────┐
                                                               │📋 天工│
                                                               │ 人事  │
                                                               └──────┘
```

### 各省部职责

| 👑 **太子** | `taizi` | 消息分拣、需求整理 | 闲聊识别、旨意提炼、标题概括 |
| 👸 **皇后** | `huanghou` | 协理小太子，管理好东宫，重点是皇帝翻牌子、后宫妃嫔的养成、和皇帝的起居等 |
| 🏛️ **东宫** | `The Router Agent` | 系统的“皇后”。负责统筹全局，接收你的 Prompt，理解意图，并将其精准分发给六院的其他小主（Agents） |
| 🏛️ **西宫** | `The Context & Memory Agent` | 负责“伴驾”与记忆。管理长短期 Memory，记住你的偏好、历史对话和上下文，确保所有回复合乎你的心意 |
| 🏛️ **中宫** | `The Security & Audit Agent` | 负责后宫安保。也就是你的 Full Audit Trails，监控所有 Agent 的 API 调用、成本消耗和输出安全性，防止“后宫干政”（幻觉或越权操作） |
| 🔍 **翰林院** | `The Writer Agent` | 专职内容生成、文案润色与文档编写 |
| 📮 **天机院** | `The Search & RAG Agent` | 专职联网搜索与知识库检索，为你打探外界情报 |
| 💰 **神算院** | `The Data Analyst Agent` | 专职处理 Excel/CSV、生成图表与数据可视化 |
| 📝 **天工院** | `The Coder Agent` | 专职写代码、Debug 与技术架构设计 |
| ⚔️ **御史院** | `The Reviewer Agent` | 专职 Code Review 与内容逻辑交叉验证，负责“挑错” |
| ⚖️ **神机院** | `The Tool-Use Agent` | 专职调用外部 API（发邮件、查天气、控制智能家居等自动化操作） |
| 🌅 **早朝官** | `zaochao` | 每日早朝、新闻聚合 | 定时播报、数据汇总 |

### 等级体系

```
皇后 → 皇贵妃 → 贵妃 → 妃 → 嫔 → 贵人 → 常在 → 答应
```

### 六院分布

| 东六宫（左侧） | 西六宫（右侧） |
|---------------|---------------|
| 景仁宫 (jinggong) | 永寿宫 (yongshou) |
| 承乾宫 (chengqian) | 翊坤宫 (yikun) |
| 钟粹宫 (zhongcui) | 储秀宫 (chuxiu) |
| 延禧宫 (yanxi) | 启祥宫 (qixiang) |
| 永和宫 (yonghe) | 长春宫 (changchun) |
| 景阳宫 (jingyang) | 咸福宫 (xianfu) |

### 权限矩阵

> 不是想发就能发 —— 真正的分权制衡

| From ↓ \ To → | 太子 | 皇后 | 乾清 | 交泰 | 坤宁 | 门下 | 尚书 | 户 | 礼 | 兵 | 刑 | 工 | 吏 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **太子** | — | ✅ | ✅ | | | | | | | | | | |
| **皇后** | ✅ | — | ✅ | ✅ | ✅ | | | | | | | | |
| **东宫** | ✅ | ✅ | — | | | ✅ | ✅ | | | | | | |
| **西殿** | ✅ | ✅ | | — | | ✅ | ✅ | | | | | | |
| **中宫** | ✅ | ✅ | | | — | ✅ | ✅ | | | | | | |
| **三省** | | | ✅ | ✅ | ✅ | — | ✅ | | | | | | |
| **六院** | ✅ | ✅ | | | | ✅ | — | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| **众议院** | | | | | | | ✅ | | | | | | |

### 任务状态流转

```
皇帝 → 太子分拣 → 皇后协理 → 三宫规划 → 门下审议 → 已派发 → 执行中 → 待审查 → ✅ 已完成
                      ↑          │                              │
                      └──── 封驳 ─┘                    阻塞 Blocked
```

---

## 📁 项目结构

```
sangongliuyuan/
├── agents/                     # 22 个 Agent 的人格模板
│   ├── taizi/SOUL.md           # 太子 · 消息分拣（含旨意标题规范）
│   ├── huanghou/SOUL.md        # 皇后 · 协理分拣、重大决策复核
│   ├── qianqinggong/SOUL.md   # 乾清宫 · 规划中枢
│   ├── jiaotaidian/SOUL.md    # 交泰殿 · 皇后权力中枢
│   ├── kunninggong/SOUL.md    # 坤宁宫 · 祭祀典礼
│   ├── menxia/SOUL.md          # 门下省 · 审议把关
│   ├── shangshu/SOUL.md        # 尚书省 · 调度大脑
│   ├── hubu/SOUL.md            # 户部 · 数据资源
│   ├── libu/SOUL.md            # 礼部 · 文档规范
│   ├── bingbu/SOUL.md          # 兵部 · 工程实现
│   ├── xingbu/SOUL.md          # 刑部 · 合规审计
│   ├── gongbu/SOUL.md          # 工部 · 基础设施
│   ├── libu_hr/                # 吏部 · 人事管理
│   ├── zaochao/SOUL.md         # 早朝官 · 情报枢纽
│   ├── jinggong/               # 景仁宫
│   ├── chengqian/              # 承乾宫
│   ├── zhongcui/               # 钟粹宫
│   ├── yanxi/                  # 延禧宫
│   ├── yonghe/                 # 永和宫
│   ├── jingyang/                # 景阳宫
│   ├── yongshou/               # 永寿宫
│   ├── yikun/                  # 翊坤宫
│   ├── chuxiu/                 # 储秀宫
│   ├── qixiang/                # 启祥宫
│   ├── changchun/              # 长春宫
│   └── xianfu/                 # 咸福宫
├── dashboard/
│   ├── dashboard.html          #看板（单文件 · 零依赖 储秀宫 · ~2500 行）
│   ├── dist/                   # React 前端构建产物（Docker 镜像内包含，本地可选）
│   └── server.py               # API 服务器（Python 标准库 · 零依赖 · ~1200 行）
├── scripts/
│   ├── run_loop.sh             # 数据刷新循环（每 15 秒）
│   ├── kanban_update.py        # 看板 CLI（含旨意数据清洗 + 标题校验）
│   ├── skill_manager.py        # Skill 管理工具（远程/本地 Skills 添加、更新、移除）
│   ├── sync_from_openclaw_runtime.py
│   ├── sync_agent_config.py
│   ├── sync_officials_stats.py
│   ├── fetch_morning_news.py
│   ├── refresh_live_data.py
│   ├── apply_model_changes.py
│   └── file_lock.py            # 文件锁（防多 Agent 并发写入）
├── tests/
│   └── test_e2e_kanban.py      # 端到端测试（17 个断言）
├── data/                       # 运行时数据（gitignored）
├── docs/
│   ├── task-dispatch-architecture.md  # 📚 详细架构文档：任务分发、流转、调度的完整设计（业务+技术）
│   ├── getting-started.md             # 快速上手指南
│   ├── wechat-article.md              # 微信文章
│   └── screenshots/                   # 功能截图（11 张）
├── install.sh                  # 一键安装脚本
├── CONTRIBUTING.md             # 贡献指南
└── LICENSE                     # MIT License
```

---

## 🎯 使用方法

### 向 AI 下旨

通过 Feishu / Telegram / Signal 给太子发消息：

```
给我设计一个用户注册系统，要求：
1. RESTful API（FastAPI）
2. PostgreSQL 数据库
3. JWT 鉴权
4. 完整测试用例
5. 部署文档
```

**然后坐好，看戏：**

1. 👑 太子接旨，皇后协理分拣
2. 🏛️ 乾清宫接旨，规划子任务分配方案
3. 🔍 门下省审议，通过 / 封驳打回重规划
4. 📮 尚书省准奏，派发给六院
5. ⚔️ 各院并行执行，进度实时可见
6. 📮 尚书省汇总结果，回奏给皇帝

全程可在**储秀宫看板**实时监控，随时可以**叫停、取消、恢复**。

### 使用圣旨模板

> 看板 → 📜 旨库 → 选模板 → 填参数 → 下旨

9 个预设模板：周报生成 · 代码审查 · API 设计 · 竞品分析 · 数据报告 · 博客文章 · 部署方案 · 邮件文案 · 站会摘要

### 自定义 Agent

编辑 `agents/<id>/SOUL.md` 即可修改 Agent 的人格、职责和输出规范。

### 增补 Skills（从网上连接）

**三种方式添加 Skills：**

#### 1️⃣ 看板 UI（最简单）

```
看板 → 🔧 技能配置 → ➕ 添加远程 Skill
→ 输入 Agent + Skill 名称 + GitHub URL
→ 确认 → ✅ 完成
```

#### 2️⃣ CLI 命令（最灵活）

```bash
# 从 GitHub 添加 code_review skill 到乾清宫
python3 scripts/skill_manager.py add-remote \
  --agent qianqinggong \
  --name code_review \
  --source https://raw.githubusercontent.com/openclaw-ai/skills-hub/main/code_review/SKILL.md \
  --description "代码审查技能"

# 一键导入官方 skills 库到指定 agents
python3 scripts/skill_manager.py import-official-hub \
  --agents qianqinggong,jiaotaidian,kunninggong,menxia,shangshu,bingbu,xingbu

# 列出所有已添加的远程 skills
python3 scripts/skill_manager.py list-remote

# 更新某个 skill 到最新版本
python3 scripts/skill_manager.py update-remote \
  --agent qianqinggong \
  --name code_review
```

#### 3️⃣ API 请求（自动化集成）

```bash
# 添加远程 skill
curl -X POST http://localhost:7891/api/add-remote-skill \
  -H "Content-Type: application/json" \
  -d '{
    "agentId": "qianqinggong",
    "skillName": "code_review",
    "sourceUrl": "https://raw.githubusercontent.com/...",
    "description": "代码审查"
  }'

# 查看所有远程 skills
curl http://localhost:7891/api/remote-skills-list
```

**官方 Skills Hub：** https://github.com/openclaw-ai/skills-hub

支持的 Skills：
- `code_review` — 代码审查（Python/JS/Go）
- `api_design` — API 设计审查
- `security_audit` — 安全审计
- `data_analysis` — 数据分析
- `doc_generation` — 文档生成
- `test_framework` — 测试框架设计

详见 [🎓 远程 Skills 资源管理指南](docs/remote-skills-guide.md)

---

## 🔧 技术亮点

| 特点 | 说明 |
|------|------|
| **React 18 前端** | TypeScript + Vite + Zustand 状态管理，13 个功能组件 |
| **纯 stdlib 后端** | `server.py` 基于 `http.server`，零依赖，同时提供 API + 静态文件服务 |
| **Agent 思考可视** | 实时展示 Agent 的 thinking 过程、工具调用、返回结果 |
| **一键安装** | `install.sh` 自动完成全部配置 |
| **15 秒同步** | 数据自动刷新，看板倒计时显示 |
| **每日仪式** | 首次打开播放上朝开场动画 |
| **远程 Skills 生态** | 从 GitHub/URL 一键导入能力，支持版本管理 + CLI + API + UI |

---

## 📚 深入了解

### 核心文档

- **[📖 任务分发流转完整架构](docs/task-dispatch-architecture.md)** — **必读文档**
  - 详细讲解三宫六院如何处理复杂任务的业务设计和技术实现
  - 涵盖：9大任务状态机 / 权限矩阵 / 4阶段调度（重试→升级→回滚）/ Session JSONL数据融合
  - 包含完整的使用案例、API端点说明、CLI工具文档
  - 对标 CrewAI/AutoGen：为什么制度化>自由协作
  - 故障场景与恢复机制
  - **读这个文档会理解为什么三宫六院这么强大**（9500+ 字，30 分钟完整理解）

- **[🎓 远程 Skills 资源管理指南](docs/remote-skills-guide.md)** — Skills 生态
  - 从网上连接和增补 skills，支持 GitHub/Gitee/任意 HTTPS URL
  - 官方 Skills Hub 预设能力库
  - CLI 工具 + 看板 UI + Restful API
  - Skills 文件规范与安全防护
  - 支持版本管理和一键更新

- **[⚡ Remote Skills 快速入门](docs/remote-skills-quickstart.md)** — 5 分钟上手
  - 快速体验、CLI 命令、看板操作示例
  - 创建自己的 Skills 库
  - API 完整参考 + 常见问题

- **[🚀 快速上手指南](docs/getting-started.md)** — 新手入门
- **[🤝 贡献指南](CONTRIBUTING.md)** — 想参与贡献？从这里开始

---
## 🔧 常见问题排查

<details>
<summary><b>❌ 任务总超时 / 下属完成了但无法传回太子</b></summary>

**症状**：六院或尚书省已完成任务，但太子收不到回报，最终超时。

**排查步骤**：

1. **检查 Agent 注册状态**：
```bash
curl -s http://127.0.0.1:7891/api/agents-status | python3 -m json.tool
```
确认 `taizi` agent 的 `statusLabel` 是 `alive`。

2. **检查 Gateway 日志**：
```bash
ls /tmp/openclaw/ | tail -5          # 找到最新日志
grep -i "error\|fail\|unknown" /tmp/openclaw/openclaw-*.log | tail -20
```

3. **常见原因**：
   - Agent ID 不匹配（已在 v1.2 修复：`main` → `taizi`）
   - LLM provider 超时（增加了自动重试）
   - 僵尸 Agent 进程（运行 `ps aux | grep openclaw` 检查）

4. **强制重试**：
```bash
# 手动触发巡检扫描（自动重试卡住的任务）
curl -X POST http://127.0.0.1:7891/api/scheduler-scan \
  -H 'Content-Type: application/json' -d '{"thresholdSec":60}'
```

</details>

<details>
<summary><b>❌ Docker: exec format error</b></summary>

**症状**：`exec /usr/local/bin/python3: exec format error`

**原因**：镜像架构（arm64）与主机架构（amd64）不匹配。

**解决**：
```bash
# 方法 1：指定平台
docker run --platform linux/amd64 -p 7891:7891 cft0808/sangongliuyuan-demo

# 方法 2：使用 docker-compose（已内置 platform）
docker compose up
```

</details>

<details>
<summary><b>❌ Skill 下载失败</b></summary>

**症状**：`python3 scripts/skill_manager.py import-official-hub` 报错。

**排查**：
```bash
# 测试网络连通性
curl -I https://raw.githubusercontent.com/openclaw-ai/skills-hub/main/code_review/SKILL.md

# 如果超时，使用代理
export https_proxy=http://your-proxy:port
python3 scripts/skill_manager.py import-official-hub --agents qianqinggong
```

**常见原因**：
- 中国大陆访问 GitHub raw 资源需要代理
- 网络超时（已增加到 30 秒 + 自动重试 3 次）
- 官方 Skills Hub 仓库维护中

</details>

---
## 🗺️ Roadmap

> 完整路线图及参与方式：[ROADMAP.md](ROADMAP.md)

### Phase 1 — 核心架构 ✅
- [x] 二十二部制 Agent 架构（太子 + 皇后 + 三宫 + 门下 + 尚书 + 十二院 + 吏部 + 早朝官）+ 权限矩阵
- [x] 储秀宫实时看板（10 个功能面板 + 实时活动面板）
- [x] 任务叫停 / 取消 / 恢复
- [x] 奏折系统（自动归档 + 五阶段时间线）
- [x] 圣旨模板库（9 个预设 + 参数表单）
- [x] 上朝仪式感动画
- [x] 天下要闻 + 飞书推送 + 订阅管理
- [x] 模型热切换 + 技能管理 + 技能添加
- [x] 官员总览 + Token 消耗统计
- [x] 小任务 / 会话监控
- [x] 太子消息分拣（闲聊自动回复 / 旨意建任务）
- [x] 皇后协理分拣（重大决策复核）
- [x] 旨意数据清洗（路径/元数据/前缀自动剥离）
- [x] 重复任务防护 + 已完成任务保护
- [x] 端到端测试覆盖（17 个断言）
- [x] React 18 前端重构（TypeScript + Vite + Zustand · 13 组件）
- [x] Agent 思考过程可视化（实时 thinking / 工具调用 / 返回结果）
- [x] 前后端一体化部署（server.py 同时提供 API + 静态文件服务）

### Phase 2 — 制度深化 🚧
- [ ] 御批模式（人工审批 + 一键准奏/封驳）
- [ ] 功过簿（Agent 绩效评分体系）
- [ ] 急递铺（Agent 间实时消息流可视化）
- [ ] 国史馆（知识库检索 + 引用溯源）

### Phase 3 — 生态扩展
- [ ] Docker Compose + Demo 镜像
- [ ] Notion / Linear 适配器
- [ ] 年度大考（Agent 年度绩效报告）
- [ ] 移动端适配 + PWA
- [ ] ClawHub 上架

---

## 🤝 参与贡献

欢迎任何形式的贡献！详见 [CONTRIBUTING.md](CONTRIBUTING.md)

特别欢迎的方向：
- 🎨 **UI 增强**：深色/浅色主题、响应式、动画优化
- 🤖 **新 Agent**：适合特定场景的专职 Agent 角色
- 📦 **Skills 生态**：各宫各院专用技能包
- 🔗 **集成扩展**：Notion · Jira · Linear · GitHub Issues
- 🌐 **国际化**：日文 · 韩文 · 西班牙文
- 📱 **移动端**：响应式适配、PWA

---

## 📂 案例

`examples/` 目录收录了真实的端到端使用案例：

| 案例 | 旨意 | 涉及部门 |
|------|------|----------|
| [竞品分析](examples/competitive-analysis.md) | "分析 CrewAI vs AutoGen vs LangGraph" | 乾清→门下→户部+兵部+礼部 |
| [代码审查](examples/code-review.md) | "审查这段 FastAPI 代码的安全性" | 乾清→门下→兵部+刑部 |
| [周报生成](examples/weekly-report.md) | "生成本周工程团队周报" | 乾清→门下→户部+礼部 |

每个案例包含：完整旨意 → 乾清宫规划 → 门下省审核意见 → 各院执行结果 → 最终奏折。

---

## ⭐ Star History

如果这个项目让你会心一笑，请给个 Star 🏛️

[![Star History Chart](https://api.star-history.com/svg?repos=yougouwu/sangongliuyuan&type=Date)](https://star-history.com/#yougouwu/sangongliuyuan&Date)

---

## 📮 联 系

> 古有邸报传天下政令，今有 GitHub 聊 AI 架构。

<p align="center">
  <strong>🏛️ 以古制御新技，以智慧驾驭 AI</strong><br>
  <sub>Governing AI with the wisdom of ancient empires</sub><br><br>
</p>

---

## 📄 License

[MIT](LICENSE) · 由 [OpenClaw](https://openclaw.ai) 社区构建
