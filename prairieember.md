# ResourceHub

ResourceHub 是一个轻量级技术资源导航与外链聚合平台，面向开发者、技术研究人员与开源项目维护者，帮助用户快速发现、分类管理与批量引用优质外部技术资源。项目本身不存储任何第三方内容，仅提供结构化的链接索引与元数据描述，解决个人书签分散、团队共享不便、文档引用难以追踪等问题。

ResourceHub 定位于中大型技术团队的知识库辅助工具，可作为内部文档站的外链管理中心，也可部署为公开的技术资源导航站。项目采用纯静态架构，支持 Markdown 驱动的资源清单更新，兼容主流 CI/CD 工作流，便于与现有技术栈集成。

## 功能概览

- **资源分类管理** 支持按技术领域、应用场景、资源类型等多维度标签对链接进行分组，内置前端、后端、运维、AI 等十余种预设分类。

- **批量外链导入** 提供脚本工具，支持从 CSV、JSON 及浏览器书签 HTML 文件批量导入链接，自动去重并校验 URL 可用性。

- **元数据增强** 每条资源可记录标题、描述、维护状态、更新日期、语言、许可证等信息，支持自定义扩展字段。

- **全文检索与过滤** 基于资源标题、描述、标签和域名进行快速搜索，支持按分类、语言、状态等多条件组合过滤。

- **链接健康检查** 内置定时任务模块，可配置周期对已收录链接进行 HTTP 状态探测，异常链接自动标记并生成报告。

- **团队协作支持** 提供资源认领、评论建议、变更历史记录功能，便于多人维护资源清单，所有变更可追溯。

- **嵌入与引用生成** 为每条资源自动生成 Markdown 引用格式、HTML 卡片代码和纯文本列表，方便在技术文档、博客或 Wiki 中直接引用。

- **开放 API 接口** 提供 RESTful 风格的查询与导出接口，支持 JSON 格式输出，便于与其他内部系统集成。

## 应用场景

- **技术文档站外链管理** 团队内部技术文档中引用大量外部工具库和参考资料，使用 ResourceHub 集中维护所有外链，文档中仅嵌入资源 ID 或自动生成的引用标记，避免链接散落和失效。

- **开源项目 README 资源汇总** 开源项目维护者将项目依赖的文档、教程、社区论坛、镜像源等链接统一收录至 ResourceHub，并在 README 中通过单条短链接展示完整资源列表，提升文档可维护性。

- **技术团队知识库建设** 企业技术部门积累了大量外部学习资料、官方文档镜像、沙箱环境和调试工具，通过 ResourceHub 分类归档并定期健康检查，减少新人上手时的信息检索成本。

- **个人开发者书签同步与备份** 开发者可将浏览器收藏夹导出后导入 ResourceHub，获得跨设备访问能力，同时利用标签和检索功能快速定位历史收藏的技术链接。

- **DevOps 资产登记** 运维团队将常用的 Helm 仓库地址、Docker 镜像源、监控面板链接、日志查询入口等统一登记，配合健康检查监控服务可达性。

## 快速开始

以下命令演示了从源码克隆到本地开发环境启动的完整流程。

```bash
# 克隆项目仓库
git clone https://github.com/resourcehub/resourcehub.git

# 进入项目目录
cd resourcehub

# 安装项目依赖（使用 npm）
npm install

# 复制默认配置文件并修改本地端口等参数
cp .env.example .env

# 启动开发服务器，默认监听 3000 端口
npm run dev
```

生产环境部署建议执行完整构建流程：

```bash
npm run build
npm run start
```

## 安装要求

项目运行依赖以下环境与工具，请确保部署前满足所有必需条件。

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Node.js | >= 18.0.0 | 项目运行时环境，推荐使用 LTS 版本 |
| npm | >= 9.0.0 | 包管理器，用于安装依赖和执行脚本 |
| SQLite | 3.40.0+ | 默认内置数据库，用于存储资源元数据与索引 |
| Git | >= 2.30.0 | 版本控制工具，用于克隆仓库及 CI/CD 集成 |
| 操作系统 | Linux / macOS / Windows (WSL2 推荐) | 跨平台支持，生产环境建议使用 Linux |
| 内存 | >= 512 MB（开发）/ >= 1 GB（生产） | 最低内存要求，实际根据资源数量线性增长 |
| 磁盘空间 | >= 200 MB | 用于存储数据库文件和静态资源缓存 |
| 浏览器 | 现代浏览器（Chrome / Firefox / Edge 最新两版） | 管理界面访问要求 |

## 文档导航

项目文档按使用者角色划分层次，下表指导快速定位所需文档。

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户指南 | /docs/user/quick-start.md | 如何快速录入第一条资源？如何检索和导出链接？ |
| 管理员手册 | /docs/admin/configuration.md | 环境变量有哪些？如何修改分类体系？如何配置健康检查周期？ |
| 开发文档 | /docs/developer/api-reference.md | API 接口规范是什么？如何扩展自定义字段？如何编写插件？ |
| 运维手册 | /docs/ops/deployment.md | 支持哪些部署方式（Docker / 裸机 / 云平台）？如何备份数据库？ |
| 贡献规范 | /docs/contributing/coding-standards.md | 代码风格要求、提交信息格式、PR 评审流程是什么？ |
| 设计文档 | /docs/design/data-model.md | 数据库表结构如何设计？资源与分类的关联关系是什么？ |

## 资源列表

本项目资源导航模块按类别收录以下外部链接。所有链接均保持用户提供的原始格式，不做任何协议补全或域名改写。

技术资讯与社区

- <code>zhongwenzimuzaixianbofangshipin.com.cn</code>

在线工具与演示

- <code>zaixianzhongwenzimushipin.com.cn</code>

学习资料与视频

- <code>renqizaixianmianfeishipin.com.cn</code>

中文资源聚合

- <code>zhongwenzaixianmianfeishipin.com.cn</code>

免费影音素材

- <code>mianfeishipinzhongwenzimu.com.cn</code>

综合内容平台

- <code>zaixianmianfeiguankannidongde.com.cn</code>

中文站点导航

- <code>zaixianzhongwenzimuwangzhan.com.cn</code>

## 项目结构

项目采用模块化分层设计，核心代码与配置分离，便于维护和扩展。以下为项目主要目录及文件说明。

```
resourcehub/
├── src/                           # 源代码主目录
│   ├── core/                      # 核心业务逻辑
│   │   ├── resource.js            # 资源增删改查及校验逻辑
│   │   ├── category.js           # 分类树管理与层级计算
│   │   └── health-check.js       # 链接健康检查调度器
│   ├── api/                       # RESTful API 路由处理
│   │   ├── v1/                   # API 版本 v1 路由定义
│   │   │   ├── resources.js      # 资源相关接口
│   │   │   └── stats.js          # 统计与状态接口
│   │   └── middleware/           # 请求解析、日志、鉴权中间件
│   ├── ui/                        # 管理界面前端源码
│   │   ├── pages/                # 页面组件（首页、资源列表、详情等）
│   │   ├── components/           # 复用 UI 组件（表格、筛选栏、卡片）
│   │   └── static/               # 样式表、图标、前端脚本
│   ├── scripts/                   # 辅助脚本（导入、导出、迁移）
│   │   ├── import-csv.js         # 从 CSV 批量导入资源
│   │   ├── export-markdown.js    # 生成 Markdown 引用列表
│   │   └── health-report.js      # 生成健康检查报告
│   └── config/                    # 配置加载与合并模块
│       ├── default.js            # 默认配置（端口、超时、分类预设）
│       └── custom.js             # 用户自定义配置覆盖
├── data/                          # 数据存储目录
│   ├── db/                       # SQLite 数据库文件存放位置
│   └── cache/                    # 健康检查结果缓存与临时文件
├── docs/                          # 项目文档（详见文档导航章节）
│   ├── user/
│   ├── admin/
│   ├── developer/
│   └── ops/
├── tests/                         # 单元测试与集成测试
│   ├── unit/                     # 核心模块单元测试
│   └── integration/              # API 接口与数据库交互测试
├── .env.example                   # 环境变量示例文件
├── package.json                   # npm 依赖声明与脚本定义
├── docker-compose.yml            # 容器化编排示例（含数据库与缓存）
├── Dockerfile                    # 生产环境镜像构建文件
├── README.md                     # 项目入口文档（本文件）
└── LICENSE                       # MIT 许可证文本
```

## 贡献指南

我们欢迎社区贡献，无论是报告问题、完善文档还是提交代码。请遵循以下步骤参与项目。

1. 查阅贡献规范与行为准则 在提交 Issue 或 Pull Request 前，请仔细阅读 /docs/contributing/coding-standards.md 中的代码风格要求、测试覆盖标准和行为准则。

2. 选择或提交 Issue 在 GitHub Issues 中查找标记为 `good-first-issue` 或 `help-wanted` 的任务，或提交新的 Bug 报告与功能建议，描述清晰、附上重现步骤或示例场景。

3. 创建分支并本地开发 从 `main` 分支创建以 `feature/` 或 `fix/` 为前缀的新分支，本地完成代码修改，确保所有单元测试通过（`npm run test`），并补充相应测试用例。

4. 提交符合规范的 Commit 提交信息采用 `<type>(<scope>): <subject>` 格式，类型包括 `feat`、`fix`、`docs`、`refactor`、`test` 等，正文说明变更动机和影响。

5. 发起 Pull Request 推送分支至远程仓库，创建 Pull Request 并关联相关 Issue，等待维护者审阅。审阅通过后由维护者合并，合并后分支将被删除。

## 常见问题

**问：项目是否支持 MySQL 或 PostgreSQL 替代内置的 SQLite？**

答：当前版本默认使用 SQLite 以降低部署门槛，无需额外数据库服务。如需使用 MySQL 或 PostgreSQL，可在配置文件中修改 `db.dialect` 参数，并在 `data/config/custom.js` 中提供连接信息。项目已内置对这两种数据库的适配层，但需要手动安装对应的 npm 驱动包（如 `mysql2` 或 `pg`）。切换后请运行 `npm run migrate` 执行表结构迁移。

**问：健康检查会影响已收录链接的访问速度或触发反爬机制吗？**

答：健康检查模块默认采用 `HEAD` 请求方法，仅获取响应头信息，不下载响应体，对目标服务器的负载极小。检查间隔默认设置为 24 小时，且支持配置随机延迟（0-5 秒）以避免集中请求。用户可在配置文件中调整 `check.userAgent` 字段，设定合法的 User-Agent 字符串，降低被识别为爬虫的风险。

**问：如何在团队内部共享资源列表而不暴露公网访问？**

答：ResourceHub 支持两种内网部署模式：第一种为只读模式，通过环境变量 `READONLY_MODE=true` 启动，管理界面自动隐藏写入操作入口，仅提供检索和导出功能；第二种为镜像模式，可配置将资源数据导出为静态 JSON 文件，适用于纯静态托管环境（如内部 S3 或 Nginx 目录）。所有部署方式均不强制要求开放公网端口，建议在生产环境搭配反向代理（如 Nginx）并启用基础认证。

## 许可证

MIT License。详细信息请查阅项目根目录下的 LICENSE 文件。

> 外链数量: 7 | 生成时间: 2026-08-21 22:29:12
