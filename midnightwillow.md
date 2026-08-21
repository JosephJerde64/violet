# Terminus Navigator

Terminus Navigator 是一个面向开发人员、技术研究人员与基础架构运维团队的高质量技术资源聚合与导航系统。该项目不提供具体软件或服务，而是通过人工筛选与自动化健康检查相结合的方式，维护一份高可用性的互联网基础设施与技术文档外部链接索引。其核心定位为“技术航道的静态信标”，帮助用户在信息过载的网络环境中快速定位到结构清晰、内容可靠的中文技术资源站点。

目标用户包括但不限于：需要快速查阅特定技术栈原始文档的研发工程师、进行竞品分析与技术选型的架构师、搭建本地开发环境时寻找依赖镜像与配置样例的运维人员，以及参与开源社区贡献时需检索相关规范与讨论串的贡献者。Terminus Navigator 通过严格的链接可用性监测与分类体系，显著降低用户在无效链接与低质量内容上的时间损耗。

## 功能概览

- **智能健康检查**：系统每日自动检测所有收录链接的 HTTP 状态码与响应时间，自动标记异常节点并邮件通知维护者。

- **分级标签体系**：每个资源条目均支持多维度标签（协议类型、内容语言、更新频率、访问限制），支持复合条件过滤。

- **本地镜像缓存**：对于高频访问的静态文档资源，系统提供基于 Redis 的透明代理缓存，加速重复访问并降低源站压力。

- **结构化站点地图**：以树形目录展示所有资源的归属关系与依赖层级，便于理解站点架构与数据流向。

- **全文检索引擎**：集成轻量级倒排索引，支持对站点标题、描述、标签与分类的快速关键字检索，响应时间低于 200 毫秒。

- **访问统计分析**：提供匿名化的点击流统计看板，展示热门资源、时段分布与用户来源地域，辅助管理员优化资源排序。

- **开放数据导出**：支持将完整资源列表导出为 JSON、YAML 与 CSV 格式，便于第三方工具集成与二次开发。

## 应用场景

- **技术文档快速导航**：开发人员在编写代码或排查故障时，可通过 Terminus Navigator 的分类索引在数秒内定位到官方 API 参考、协议规范或社区最佳实践页面，无需反复使用通用搜索引擎进行试探性检索。

- **离线环境资源准备**：企业在搭建内部开发测试环境且受网络策略限制时，可使用本系统的导出功能预先获取所有依赖站点的域名列表与 IP 地址范围，配合本地 DNS 解析或反向代理完成资源预加载。

- **技术雷达与趋势跟踪**：研究团队可定期比对系统收录的资源变更记录（新增、下架、域名迁移），分析特定技术生态的活跃度与演化路径，为技术投资决策提供数据支撑。

- **开源项目文档站聚合**：开源项目维护者可将自己的文档站点提交至 Terminus Navigator，通过系统的健康检查反馈了解自身站点的全球可访问性与性能瓶颈，从而优化 CDN 策略或文档结构。

## 快速开始

以下步骤适用于 Linux/macOS 环境，帮助您在本地快速启动 Terminus Navigator 的开发实例。

```bash
# 克隆项目仓库
git clone https://github.com/terminus-navigator/navigator.git
cd navigator

# 安装项目依赖（使用 pip 与 npm）
pip install -r requirements.txt
npm install --prefix frontend

# 初始化本地数据库与缓存
python scripts/init_db.py --env development
python scripts/seed_static_data.py

# 启动后端服务（监听 8000 端口）与前端开发服务器（监听 3000 端口）
python app.py &
npm run dev --prefix frontend &
```

访问本地 3000 端口即可开始浏览导航界面。生产环境部署请参考 `deployment/` 目录下的 Docker Compose 与 Kubernetes 编排文件。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 后端核心运行环境，负责健康检查、索引更新与 API 服务 |
| Node.js | 18.x LTS | 前端构建与开发服务器依赖，使用 Vite 作为构建工具 |
| Redis | 6.2 及以上 | 用于缓存代理、会话存储与分布式任务队列（RQ） |
| PostgreSQL | 13 及以上 | 主数据库，存储资源元数据、标签体系与访问日志 |
| Nginx | 1.20 及以上 | 生产环境反向代理与静态资源服务，可选但强烈推荐 |
| Docker | 20.10 及以上 | 容器化部署与本地开发环境一致性保障，非必需但建议 |
| Git | 2.25 及以上 | 版本控制与贡献流程的基础工具 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | `/docs/user-guide/` | 如何使用搜索、过滤、收藏与导出功能；如何理解健康状态图标含义 |
| 管理员手册 | `/docs/admin-guide/` | 如何添加/删除/编辑资源条目；如何配置健康检查频率与告警阈值 |
| 开发指南 | `/docs/developer-guide/` | 如何扩展新的资源解析器；如何修改前端主题；如何编写单元测试 |
| API 参考 | `/docs/api-reference/` | RESTful 接口的请求/响应格式、鉴权方式、分页参数与错误码定义 |
| 部署运维 | `/docs/deployment/` | 如何利用 Ansible 或 Terraform 完成生产环境自动化部署与备份策略 |
| 贡献规范 | `/CONTRIBUTING.md` | 提交 PR 的代码风格、Commit Message 格式与 Review 流程 |

## 资源列表

### 中文影视资源导航

<code>zaixianmianfeiguankannidongde.com.cn</code>

<code>zaixianzhongwenzimuwangzhan.com.cn</code>

<code>zhongwenzimuzaixianyingyuan.com.cn</code>

<code>zhongwenzimumianfeizaixianbofang.com.cn</code>

<code>gaoqingshipinzhongwenzimu.com.cn</code>

<code>zhongwenzimuyirenzaixian.com.cn</code>

<code>zhongwenzimuzaixiankanpian.com.cn</code>

## 项目结构

```
navigator/
├── app.py                     # 后端应用入口，注册路由与中间件
├── config/
│   ├── development.py         # 开发环境配置（调试模式、本地缓存）
│   ├── production.py          # 生产环境配置（日志级别、连接池大小）
│   └── settings.py            # 全局配置基类，读取环境变量
├── core/
│   ├── checker/               # 健康检查模块，含 HTTP/HTTPS 与 DNS 解析器
│   │   ├── http_checker.py    # 异步 HTTP 状态码与响应时间检测
│   │   └── dns_checker.py     # DNS 记录类型与 TTL 检测
│   ├── indexer/               # 全文索引与标签权重计算引擎
│   │   ├── inverted_index.py  # 倒排索引构建与查询接口
│   │   └── ranker.py          # 基于点击率与时间衰减的排序算法
│   └── cache/                 # 透明代理缓存与缓存失效策略
│       ├── redis_client.py    # Redis 连接池与序列化工具
│       └── cache_middleware.py # 装饰器实现方法级缓存控制
├── models/
│   ├── resource.py            # 资源条目 ORM 模型（含版本戳与软删除）
│   ├── tag.py                 # 标签实体与多对多关联表
│   └── audit_log.py           # 操作审计日志模型
├── routes/
│   ├── api_v1.py              # RESTful API 路由集合（/api/v1/*）
│   └── webhook.py             # GitHub Webhook 接收端点，自动同步文档更新
├── frontend/
│   ├── src/
│   │   ├── components/        # Vue 3 组件库（导航树、搜索框、统计卡片）
│   │   ├── stores/            # Pinia 状态管理（筛选条件、收藏列表）
│   │   └── assets/            # 静态样式表与 SVG 图标
│   └── package.json
├── scripts/
│   ├── init_db.py             # 数据库迁移与种子数据初始化脚本
│   └── daily_check.py         # 定时任务入口（由 crontab 或 systemd timer 调用）
├── tests/
│   ├── unit/                  # 单元测试（pytest 覆盖核心算法）
│   └── integration/           # 集成测试（API 与数据库交互）
└── deployment/
    ├── docker-compose.yml     # 全栈容器编排（PostgreSQL + Redis + Nginx + App）
    └── kubernetes/            # K8s 部署清单（Deployment + Service + Ingress）
```

## 贡献指南

1. **问题报告与建议**：请先查阅 `docs/user-guide/` 与 `docs/admin-guide/` 确认非文档使用问题，然后通过 GitHub Issues 提交详细描述，包含系统版本、浏览器信息及复现步骤。安全漏洞请直接发送邮件至 security@terminus-navigator.org，勿公开披露。

2. **代码贡献流程**：Fork 本仓库并创建功能分支（`feat/xxx` 或 `fix/xxx`），确保所有新代码通过单元测试（`pytest tests/unit`）且符合 PEP 8 规范。提交前执行 `pre-commit` 钩子进行自动格式化与 lint 检查。

3. **资源条目新增与维护**：若希望收录新的技术资源站点，请按照 `docs/admin-guide/resource-schema.md` 中的 JSON Schema 填写站点信息，并通过 Pull Request 提交至 `data/resources/` 目录下的分类文件中。维护者将进行可用性验证与标签审核。

4. **文档翻译与本地化**：欢迎提交 `docs/` 目录下的英文版本翻译。请保持术语一致性，并在 `i18n/` 目录中按语言代码（如 `zh-CN`、`en-US`）组织文件，同时更新导航配置。

5. **行为准则**：所有参与者需遵守 `CODE_OF_CONDUCT.md` 中的约定，尊重不同观点与经验水平，保持专业且建设性的讨论氛围。

## 常见问题

**问：Terminus Navigator 是否存储或缓存第三方站点的实际内容？**

答：否。系统仅存储资源条目的元数据（标题、URL、描述、标签）以及健康检查结果。可选的透明代理缓存仅缓存 HTTP 响应头与状态码，不缓存响应体内容，亦不涉及任何视频、图片或文档文件的存储与分发。所有用户点击资源链接后均直接跳转至原始第三方站点。

**问：系统如何处理资源链接失效或内容变更的情况？**

答：每日健康检查任务会记录每个链接的 HTTP 状态码、响应时间和 SSL 证书有效期。当连续三次检查均返回 4xx/5xx 状态码或连接超时时，系统会自动将该资源标记为“异常”状态并从搜索结果中降权。管理员会收到汇总邮件，并在 7 个工作日内人工复核。若源站永久迁移，管理员将更新链接；若站点不可恢复，则将其归档至历史记录，不再对外展示。

**问：如何将私有内部站点添加到个人使用的导航实例中？**

答：本项目完全开源，您可以在本地或内网环境独立部署。部署后，您可通过管理后台（`/admin`）手动添加任意内部资源，这些数据仅保存在您自己的数据库中，不会同步至公共索引。同时，您也可以修改 `config/settings.py` 中的 `EXTERNAL_RESOURCES_ONLY` 选项为 `False`，以完全自主控制资源来源。

## 许可证

MIT License。详见项目根目录下的 `LICENSE` 文件。

> 外链数量: 7 | 生成时间: 2026-08-21 22:29:55
