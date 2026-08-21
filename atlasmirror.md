# ZhongwenZimu Hub

ZhongwenZimu Hub is a comprehensive, community-driven navigation and resource aggregation platform tailored for Chinese-speaking audiences seeking access to multilingual subtitle resources, high-definition video sources, and online streaming indices. The project does not host, store, or distribute any copyrighted media content; instead, it functions as an organized, curated reference index that points to legally ambiguous third-party streaming and subtitle sources across the public internet.

The primary target users are developers, media archivists, linguistic researchers, and general end-users who require structured, machine-readable metadata and rapid navigation to subtitle-indexed video resources. By offering a unified query interface, standardized data schemas, and RESTful API endpoints, ZhongwenZimu Hub reduces the friction of locating and verifying subtitle-file origins and streaming availability across multiple disjointed domains. The project emphasizes transparency, reproducibility, and user-contributed curation, making it suitable for both automated scraping pipelines and manual browsing workflows.

## 功能概览

- **统一资源索引引擎** – 提供中心化的域名列表和健康状态检查，实时监测各第三方源站的可访问性与响应延迟。

- **多维度搜索过滤器** – 支持按影片类型、字幕语言、发布年份、视频清晰度标签进行组合筛选，返回匹配的资源入口列表。

- **元数据标准化提取** – 从各源站页面抓取并规范化影片标题、IMDb编号、发行日期、文件格式、字幕语种等关键字段，输出JSON或CSV格式。

- **状态监控与告警系统** – 定时任务周期性探测各资源域名的HTTP状态码、SSL证书有效期和页面关键元素存在性，异常时记录日志并通过Webhook通知维护者。

- **用户自定义收藏集** – 注册用户可创建私有或公开的资源列表，对常用域名或具体影片条目添加标签、备注和优先级标记。

- **批量导入与导出工具** – 支持通过CSV或YAML文件批量提交待索引的域名或影片查询条件，并支持将搜索结果导出为结构化数据包。

- **轻量级管理面板** – 提供基于角色的后台界面，供审核员处理用户提交的新域名、更新过期信息、合并重复条目并审计操作历史。

- **开放API v1** – 提供RESTful接口，允许第三方开发者以编程方式查询索引、获取详情、提交反馈，便于集成到媒体播放器或自动化脚本中。

## 应用场景

- **个人媒体库自动化整理** – 媒体爱好者可定期调用API获取最新字幕源站列表，将其导入本地自动化脚本，批量匹配已下载影片的字幕文件，减少手动搜索时间。

- **语言学习辅助平台** – 教育机构或语言学习应用可嵌入本索引，允许学习者按难度等级或语种筛选带双语字幕的视频资源，快速定位适合练习听力和阅读的素材入口。

- **内容审核与合规检查** – 法务或合规团队可利用本项目的监控模块，定期扫描所依赖的第三方域名是否出现内容变更、停运或被屏蔽，及时调整内部资源引用策略。

- **数据研究与趋势分析** – 学术研究者可导出历史监控数据，分析特定类型影片的字幕覆盖率和源站存活周期，撰写关于数字资源可用性的纵向研究报告。

- **开源社区协作维护** – 社区贡献者可通过提交PR或Issue来新增有效域名、更新失效地址、补充影片元数据，形成众包式资源库，降低单一维护者的负担。

## 快速开始

以下步骤适用于Linux / macOS / Windows WSL2环境，确保系统已安装Git、Node.js（v18+）和npm。

```bash
# 克隆项目仓库
git clone https://github.com/zhongwenzimu/zhongwenzimu-hub.git
cd zhongwenzimu-hub

# 安装依赖包（使用npm）
npm install

# 复制环境变量模板并填写必要配置
cp .env.example .env

# 初始化本地SQLite数据库并导入预置域名列表
npm run db:migrate
npm run db:seed

# 启动开发服务器（默认监听3000端口）
npm run dev
```

访问 `http://localhost:3000` 即可浏览本地索引界面。如需后台监控服务，另开终端执行：

```bash
npm run monitor:start
```

该命令会每30分钟探测一次所有已收录域名的可用性，并将结果写入 `logs/monitor.log`。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | v18.0.0 或更高 | 运行时环境，使用原生fetch和crypto模块 |
| npm | v9.0.0 或更高 | 包管理器，用于安装依赖和运行脚本 |
| SQLite3 | v3.40.0 或更高 | 嵌入式数据库，存储域名元数据、用户收藏和监控历史 |
| Git | v2.30.0 或更高 | 版本控制，用于克隆仓库和提交贡献 |
| 网络出口 | 可访问公网IPv4/IPv6 | 用于探测第三方域名状态，需允许出站HTTP/HTTPS流量 |
| 内存 | 最低512MB，推荐1GB | 运行监控进程和API服务的内存占用 |
| 存储 | 最低200MB可用空间 | 存放数据库文件、日志和缓存数据 |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|------|----------|----------|
| 用户手册 | `docs/user-guide/` | 如何注册账户、搜索资源、管理收藏集、导出列表？ |
| 开发者指南 | `docs/developer/` | API认证方式、请求限流策略、数据模型字段含义、如何编写自定义爬虫？ |
| 运维手册 | `docs/operations/` | 如何部署至生产环境、配置systemd服务、备份数据库、迁移至PostgreSQL？ |
| 贡献规范 | `CONTRIBUTING.md` | 提交新域名的格式要求、PR标题规范、测试覆盖率门槛、签署CLA的流程？ |
| 变更日志 | `CHANGELOG.md` | 每个版本的发布日期、新增功能、破坏性变更和已修复的缺陷？ |
| 安全策略 | `SECURITY.md` | 如何报告漏洞、漏洞响应时间窗口、已加固的输入校验和输出编码措施？ |

## 资源列表

以下为项目当前索引的第三方域名列表，按类别分组。这些域名由社区提交并经初步审核，项目本身不对其内容、可用性或法律合规性负责。用户访问这些域名时应自行评估风险并遵守当地法律法规。

### 综合字幕索引类

- <code>zhongwenzimuzaixianyingyuan.org.cn</code>
- <code>zhongwenzimumianfeizaixianbofang.org.cn</code>
- <code>gaoqingshipinzhongwenzimu.org.cn</code>
- <code>zhongwenzimuyirenzaixian.org.cn</code>
- <code>zhongwenzimuzaixiankanpian.org.cn</code>
- <code>gaoqingpianyuanzaixianbofang.org.cn</code>
- <code>zuixinzhongwenzimuzaixian.com.cn</code>

## 项目结构

```
zhongwenzimu-hub/
├── src/                           # 核心源代码目录
│   ├── api/                       # RESTful API 路由与控制器
│   │   ├── v1/                    # API v1 版本实现
│   │   │   ├── domains.js         # 域名增删改查与状态查询
│   │   │   ├── search.js          # 多条件搜索聚合逻辑
│   │   │   └── user.js            # 用户注册、登录、收藏管理
│   │   └── middleware/            # 身份验证、限流、日志中间件
│   ├── crawler/                   # 爬虫与解析模块
│   │   ├── fetcher.js             # 并发HTTP请求与重试策略
│   │   ├── parser.js              # 基于cheerio的HTML元数据提取
│   │   └── scheduler.js           # 定时任务编排与队列管理
│   ├── db/                        # 数据库层
│   │   ├── migrations/            # SQLite schema 版本迁移脚本
│   │   ├── models/                # 数据模型定义（Domain, User, Favorite）
│   │   └── seeders/               # 初始预置域名和测试数据
│   ├── monitor/                   # 健康监控子模块
│   │   ├── probe.js               # 单域名探测逻辑（状态码、响应时间、SSL）
│   │   ├── alert.js               # 告警触发器与Webhook发送
│   │   └── reporter.js            # 生成日/周可用性统计报告
│   └── utils/                     # 通用工具函数
│       ├── validator.js           # 域名格式、URL安全校验
│       ├── cache.js               # 内存缓存与LRU过期策略
│       └── logger.js              # 分级日志（error/warn/info/debug）
├── config/                        # 环境配置文件（development, production, test）
├── docs/                          # 完整文档体系（用户手册、开发指南、运维手册）
├── tests/                         # 单元测试与集成测试（Jest + Supertest）
│   ├── unit/                      # 独立函数与工具测试
│   └── integration/               # API端到端测试与爬虫模拟
├── scripts/                       # 运维辅助脚本
│   ├── backup-db.sh               # 数据库定时备份脚本
│   ├── deploy.sh                  # 生产环境部署自动化脚本
│   └── health-check.sh            # 系统前置检查（端口、依赖、权限）
├── public/                        # 静态资源（前端CSS、JS、图标）
├── logs/                          # 运行时日志输出目录（自动轮转）
├── .env.example                   # 环境变量配置模板
├── package.json                   # npm 项目配置与依赖清单
├── package-lock.json              # 精确依赖版本锁定
├── README.md                      # 项目主文档（即本文档）
├── CONTRIBUTING.md                # 详细贡献指南与行为准则
├── CHANGELOG.md                   # 版本历史与发布说明
├── SECURITY.md                    # 安全漏洞报告流程
└── LICENSE                        # MIT 许可证全文
```

## 贡献指南

1. 查阅贡献规范与行为准则 – 在提交任何代码或数据之前，请完整阅读 `CONTRIBUTING.md` 和 `CODE_OF_CONDUCT.md`，确保理解PR分类（新增域名、修复bug、文档改进、新功能）对应的不同流程。

2. 创建分支并本地开发 – 从 `main` 分支创建以 `feature/` 或 `fix/` 为前缀的新分支，进行代码修改或数据更新。对于新增域名，需在 `db/seeders/` 中按模板格式添加条目并附带来源说明。

3. 编写或更新测试用例 – 所有对解析逻辑、API响应结构、监控探测器的改动，必须补充对应的单元测试或集成测试，确保测试覆盖率不低于80%。运行 `npm test` 验证全部用例通过。

4. 提交前进行代码格式化与静态检查 – 执行 `npm run lint` 和 `npm run format` 统一代码风格，并运行 `npm run build` 确认无构建错误。提交信息需遵循常规提交规范，包含类型（feat/fix/docs/chore）和简短描述。

5. 发起Pull Request并等待审核 – 推送分支至远程仓库，在GitHub上创建PR。填写PR模板中的检查清单，关联相关Issue（如有）。至少一名项目维护者将进行代码审查，可能要求修改或补充信息。合并后您的贡献将出现在下一个版本的变更日志中。

## 常见问题

**问：这个项目是否提供实际的视频文件或字幕文件下载？**  
答：不提供。本项目仅维护第三方域名的索引和元数据查询接口，不存储、缓存、分发任何视频、音频或字幕文件。所有实际内容均由外部站点提供，用户需自行承担访问责任。我们建议用户尊重版权，仅在合法授权范围内使用相关资源。

**问：如果某个列出的域名无法访问或显示异常内容，应该怎么办？**  
答：请通过GitHub Issues提交报告，标题注明“[Domain Down]”并附上域名及您所在地区的网络环境描述。监控系统也会自动记录异常，但用户反馈往往更及时。维护者会核实后将其标记为“失效”或从主列表中移除。同时，我们也欢迎您提交替代域名或更新的URL。

**问：我可以部署这个项目作为私有实例，只索引我自己关注的域名吗？**  
答：完全允许。MIT许可证授予您自由修改、部署和分发的权利。您可以通过修改 `db/seeders/` 中的初始数据或使用管理面板手动添加/删除域名，来定制您的私有索引。我们推荐您保留监控和导出功能，以便持续跟踪您的自定义资源列表。

## 许可证

MIT License。完整文本请参阅项目根目录下的 `LICENSE` 文件。

> 外链数量: 7 | 生成时间: 2026-08-21 22:29:12
