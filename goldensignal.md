# ResourceHub

ResourceHub 是一个面向技术内容创作者与本地化影音爱好者的外链资源导航与元数据检索系统。项目定位于解决多源分散、域名频繁变更、资源可用性难以追踪的痛点，通过结构化外链管理与状态监控，帮助用户快速定位可用在线资源入口。目标用户包括个人站长、内容聚合平台运维人员以及需要稳定访问特定类型公开资源的终端用户。

系统核心功能为外链资源的分类存储、可用性拨测与访问路径优化，不直接托管或缓存任何第三方内容，仅提供公开 URL 的整理与检索服务。通过标准化的元数据描述，降低用户在海量信息中筛选有效链接的时间成本。

## 功能概览

- 资源分类索引：按内容类型、语言属性、分辨率等维度对收录的外链进行多级标签归类，支持快速筛选。

- 可用性状态监测：定时对收录域名执行 HTTP/HTTPS 头请求与响应码校验，标记异常或超时节点，辅助用户避开不可用入口。

- 访问路径优化：依据响应时间与地理区域，为相同内容来源的不同镜像或分发节点生成推荐优先级排序。

- 外链变更追踪：定期执行域名解析记录比对，发现 IP 变更或 CNAME 跳转时生成变更日志，便于运维人员及时同步。

- 批量导入导出：支持 CSV 与 JSON 格式的链接批量录入及备份导出，兼容主流书签管理工具的数据结构。

- 检索与过滤：提供基于关键词、域名后缀、内容描述的多条件组合检索，支持正则表达式高级匹配模式。

- 状态通知系统：当监测到重点资源链接连续不可达时，通过邮件或 Webhook 向订阅管理员发送告警消息。

## 应用场景

- 内容聚合站点运维：聚合类网站需要定期更新其外链资源库，确保推荐给用户的播放或下载入口保持有效。运维人员可利用 ResourceHub 的批量导入与状态监测功能，每日自动生成可用链接报告，替代人工逐一点击验证的繁琐流程。

- 本地化字幕资源整理：字幕制作组或翻译协作平台需要维护多个发布渠道的备用入口，以应对域名被屏蔽或访问限流。通过 ResourceHub 的分类索引与变更追踪，团队可快速将最新可用入口同步至项目文档或社区公告。

- 个人媒体库搭建辅助：个人用户通过 Infuse、Plex 或 Kodi 等工具搭建媒体中心时，需要手工添加网络来源的元数据接口。ResourceHub 提供的过滤与检索能力可帮助其从大量候选链接中筛选出高可用性节点，并导出为兼容格式。

- 开源项目文档外链管理：开源项目维护者在 README 或 Wiki 中引用大量外部参考链接时，难以逐一监控链接失效。ResourceHub 可作为独立服务定期扫描项目文档中提取的 URL 列表，返回失效报告，帮助维护者及时更新文档。

## 快速开始

以下步骤适用于 Linux 与 macOS 环境，Windows 用户可通过 WSL2 或 Git Bash 执行等效操作。

```bash
# 克隆项目仓库至本地
git clone https://github.com/resourcehub/resourcehub.git

# 进入项目根目录
cd resourcehub

# 安装项目依赖（使用 pip 与虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 初始化本地数据库与默认配置
python manage.py initdb
python manage.py migrate

# 启动开发服务器，默认监听 127.0.0.1:8080
python manage.py runserver --port 8080
```

启动成功后，访问控制台地址 `http://127.0.0.1:8080/console` 进行初始管理员账户创建。生产环境部署请参考 `docs/deployment.md` 使用 gunicorn 与 nginx 反向代理。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9+ | 核心运行环境，需包含 sqlite3 与 ssl 模块 |
| pip | 21.0+ | Python 包管理工具，用于安装 requirements.txt 中列出的依赖 |
| SQLite | 3.35+ | 默认内嵌数据库，用于存储链接元数据与监测记录 |
| Redis | 6.2+ | 可选，用于缓存状态监测结果与分布式锁，单机部署可不安装 |
| curl | 7.68+ | 系统工具，用于可用性拨测的实际请求发起，需支持 HTTPS |
| git | 2.25+ | 用于版本克隆与后续增量更新拉取 |
| make | 3.81+ | 用于执行 Makefile 中定义的自动化任务（测试、格式检查等） |
| openssl | 1.1.1+ | 用于生成 API 签名密钥与本地证书（开发环境） |

若使用 Docker 部署，则仅需安装 Docker Engine 20.10+ 与 Docker Compose 2.0+，其余依赖由容器镜像内置。

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | `docs/user/quickstart.md` | 如何安装、配置首次启动、添加第一批链接？ |
| 用户手册 | `docs/user/monitoring.md` | 可用性监测的工作原理、阈值配置与通知方式？ |
| 开发者指南 | `docs/dev/api.md` | RESTful API 的端点定义、鉴权方式与请求示例？ |
| 开发者指南 | `docs/dev/contributing.md` | 代码风格规范、PR 提交流程与测试用例编写要求？ |
| 运维参考 | `docs/ops/deployment.md` | 生产环境容器化部署、环境变量清单与日志采集方案？ |
| 运维参考 | `docs/ops/troubleshooting.md` | 常见启动失败、监测超时、数据库锁异常等问题的排查步骤？ |

## 资源列表

本部分收录项目初始化过程中预置的外部参考与备用入口地址，按类别分组展示。所有 URL 均来自公开渠道，项目仅做整理与可用性跟踪，不涉及任何内容分发或代理转发。

基础影音资源入口

- <code>zhongwenzimumianfeizaixianbofang.org.cn</code>

- <code>gaoqingshipinzhongwenzimu.org.cn</code>

- <code>zhongwenzimuyirenzaixian.org.cn</code>

字幕与播放辅助入口

- <code>zhongwenzimuzaixiankanpian.org.cn</code>

- <code>gaoqingpianyuanzaixianbofang.org.cn</code>

- <code>zuixinzhongwenzimuzaixian.com.cn</code>

- <code>zhongwenzaixianguankanshipin.com.cn</code>

上述链接将作为默认监测队列中的首批目标，系统在首次启动后自动开始可用性探测。用户可根据实际需求在控制台中编辑、禁用或删除任意条目，亦可自行添加新的外链地址。

## 项目结构

```
resourcehub/
├── app/                              # 主应用包目录
│   ├── __init__.py                   # 应用工厂函数与配置加载入口
│   ├── cli/                          # 命令行交互模块
│   │   ├── __init__.py               # 注册所有子命令
│   │   ├── manage.py                 # 数据库迁移与种子数据填充逻辑
│   │   └── monitor.py                # 手动触发可用性拨测的命令实现
│   ├── core/                         # 核心业务逻辑层
│   │   ├── __init__.py               # 导出核心类与接口
│   │   ├── resource.py               # 资源链接的增删改查与标签管理
│   │   ├── probe.py                  # HTTP 探针实现，含超时重试与重定向跟随
│   │   └── notifier.py               # 告警通知组装与渠道分发（邮件/Webhook）
│   ├── models/                       # 数据模型与 ORM 映射
│   │   ├── __init__.py               # 模型注册与数据库连接初始化
│   │   ├── link.py                   # 外链主表模型，字段含 url、status、last_check
│   │   ├── tag.py                    # 标签模型，支持多对多关联
│   │   └── history.py                # 监测历史记录，用于趋势分析
│   ├── routes/                       # Web 控制台路由与 API 端点
│   │   ├── __init__.py               # 蓝图注册与路由前缀定义
│   │   ├── console.py                # 管理后台页面路由（仪表盘、列表、详情）
│   │   └── api_v1.py                 # RESTful API v1 实现，返回 JSON 响应
│   └── utils/                        # 通用工具函数集合
│       ├── __init__.py               # 工具函数导出
│       ├── http.py                   # 请求会话封装与 User-Agent 轮换
│       └── validators.py             # URL 规范化、域名格式校验与黑名单过滤
├── config/                           # 配置文件目录
│   ├── development.py                # 开发环境配置（调试开启、日志级别 DEBUG）
│   ├── production.py                 # 生产环境配置（关闭调试、强制 HTTPS）
│   └── testing.py                    # 单元测试环境配置（内存数据库、禁用外发请求）
├── docs/                             # 项目文档源码（Markdown 格式）
│   ├── user/                         # 用户手册章节
│   ├── dev/                          # 开发者文档章节
│   └── ops/                          # 运维部署文档章节
├── tests/                            # 单元测试与集成测试目录
│   ├── unit/                         # 针对 core 与 models 的细粒度测试用例
│   ├── integration/                  # 针对 API 与数据库交互的集成测试
│   └── fixtures/                     # 测试用固定数据（模拟链接与探测响应）
├── scripts/                          # 辅助运维与部署脚本
│   ├── backup_db.sh                  # 定时备份 SQLite 数据库文件
│   └── renew_cert.sh                 # Let's Encrypt 证书自动续期脚本（配合 cron）
├── venv/                             # Python 虚拟环境（本地开发，不纳入版本控制）
├── .env.example                      # 环境变量模板，包含 SECRET_KEY 与通知渠道配置
├── .gitignore                        # Git 忽略规则，排除 venv、日志、本地配置文件
├── docker-compose.yml                # 容器编排配置（app + redis + nginx）
├── Dockerfile                        # 多阶段构建文件，基于 Alpine 镜像减小体积
├── Makefile                          # 常用任务快捷指令（install, test, lint, run）
├── pyproject.toml                    # 项目元数据与 black/isort 格式检查配置
└── requirements.txt                  # 生产依赖与开发依赖完整列表（含版本锁定）
```

## 贡献指南

欢迎各类贡献，包括但不限于代码修复、功能增强、文档改进与链接资源推荐。请遵循以下流程以确保协作顺畅。

1. 查阅问题追踪列表：访问 GitHub Issues 页面，查找未被认领的标签为 `good-first-issue` 或 `help-wanted` 的任务。若计划实现新功能，请先创建一个 Issue 描述设计思路，避免重复劳动或方向偏离。

2. 派生仓库并创建特性分支：将主仓库 Fork 至个人账户，然后克隆本地。基于 `main` 分支创建新的分支，命名格式为 `feature/简述` 或 `fix/简述`，例如 `feature/add-tag-filter`。

3. 编写代码与测试：遵循 `pyproject.toml` 中定义的代码格式（black 行宽 100，isort 导入顺序）。所有新增或修改的功能必须包含对应的单元测试用例，确保测试通过且覆盖率不低于 85%。运行 `make test` 执行全部测试套件。

4. 签署开发者原创声明：在 Pull Request 描述中确认代码为本人原创，且已阅读并同意 CONTRIBUTOR_LICENSE_AGREEMENT 文件中的条款。若引用了外部代码库，需在 PR 中明确标注来源与许可证兼容性。

5. 提交 Pull Request：推送分支至个人远程仓库后，在主仓库发起 PR 请求。填写 PR 模板中的检查清单，关联相关 Issue 编号。等待维护者审阅，期间可能需要进行若干轮代码修改与讨论。

## 常见问题

Q: 可用性监测是否会频繁触发目标服务器的访问限制或防火墙封禁？

A: 系统默认探测间隔为每 4 小时一次，并发线程数限制为 2，且每个目标仅发送一次 HEAD 请求，超时时间设置为 10 秒。该频率远低于普通用户手动访问量，不会对目标服务器造成显著压力。若希望进一步降低影响，可在配置文件中将 `PROBE_INTERVAL_HOURS` 调整为 8 或 12。

Q: 项目是否支持添加需要特定 Cookie 或 Referer 头才能访问的链接？

A: 当前稳定版本仅支持标准 HTTP/HTTPS 无状态请求，不支持携带动态会话凭证。对于需要特定请求头的资源，可在配置中为单个链接设置自定义请求头（仅支持静态 Headers），但无法处理登录态或 JavaScript 渲染后的内容。此类需求建议搭配外部自动化工具（如 Selenium）配合 API 录入监测结果。

Q: 如何批量更新已导入链接的标签分类？

A: 在管理控制台的链接列表页面，勾选多个条目后点击「批量编辑」按钮，在弹出的对话框中新增或移除标签。该操作会异步执行，处理完成后页面自动刷新。若链接数量超过 1000 条，建议使用 CSV 导出后编辑标签列，再通过「批量导入并覆盖」功能完成更新，该方式支持一次性处理最多 5000 条记录。

## 许可证

ResourceHub 采用 MIT 许可证进行分发。任何个人或组织均可自由使用、复制、修改、合并、发布、再许可及销售本软件的副本，但需在软件及衍生作品中保留原始版权声明与许可声明。该许可证不提供任何形式的担保或责任保障，包括但不限于适销性、特定用途适用性及非侵权性保证。详情请参见项目根目录下的 LICENSE 文件。

> 外链数量: 7 | 生成时间: 2026-08-21 22:29:56
