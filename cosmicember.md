# Nova Horizon

Nova Horizon 是一个面向技术内容聚合与外部资源索引的开源工具集，定位于帮助开发者、研究者和内容策展人高效管理、校验和展示外部 URL 资源。项目本身不托管任何第三方内容，而是提供一套标准化的资源描述、健康检查与展示框架，适用于构建技术导航站、论文参考文献库、工具清单或社区推荐列表。目标用户包括开源项目维护者、技术博主、社区运营人员以及需要长期维护大量外链的中小型团队。

项目核心解决外链管理中的三大痛点：链接失效不可感知、资源分类混乱、展示方式缺乏技术规范。通过提供统一的数据结构、自动化检查脚本和可定制的展示模板，Nova Horizon 使用户能够以最低维护成本保持资源列表的准确性与可读性。

---

## 功能概览

- **资源描述语言** 提供基于 YAML 和 JSON 的资源描述规范，支持标题、描述、标签、状态、优先级等元数据字段，便于机器读取与人工编辑。

- **自动化链接健康检查** 内置基于 HTTP 状态码和响应时间的检测脚本，支持定时任务或手动触发，输出可用性报告，标记失效或重定向链接。

- **多格式展示模板** 提供 Markdown、HTML 和纯文本三种展示模板，可将结构化资源列表渲染为 README 文档、静态网页或日志文件，适配不同发布渠道。

- **标签与分类体系** 支持自定义标签和分类层级，允许同一资源归属多个分类，便于多维度筛选与检索，适应复杂知识库组织需求。

- **变更日志与审计追溯** 自动记录资源条目的新增、删除、修改及状态变更，生成带时间戳的审计日志，方便团队协作与问题回溯。

- **外部元数据增强** 支持通过公共 API（如 Open Graph 解析、域名 WHOIS 查询）自动补全资源的标题、描述和图标信息，减少手动录入工作量。

- **命令行与 API 双接口** 提供完整的 CLI 工具用于日常操作，同时暴露 RESTful API 供其他系统集成，满足自动化流水线需求。

---

## 应用场景

- **技术社区资源导航站维护** 社区运营人员可使用 Nova Horizon 管理精选工具、教程、文档等外部链接，每周自动运行健康检查，确保导航站不出现死链，提升用户体验。

- **学术论文参考文献管理** 研究人员在撰写综述或技术报告时，可将参考文献 URL 导入系统，统一校验可访问性，并生成格式规范的引用列表，避免提交前逐一手动检查。

- **企业内部工具目录构建** 中小型团队可使用本工具建立内部常用开发工具、监控面板、文档库的索引，通过标签按团队或项目筛选，并设置优先级标注核心服务。

- **开源项目外部依赖清单维护** 开源项目维护者可将项目依赖的第三方库文档、镜像源、构建工具链接纳入管理，在版本发布前自动检查所有外部资源可用性，降低下游用户的使用障碍。

---

## 快速开始

以下命令演示了从代码仓库克隆、安装依赖到运行基础资源检查的完整流程：

```bash
# 克隆项目仓库
git clone https://github.com/novahorizon/novahorizon.git
cd novahorizon

# 安装 Python 依赖（建议使用虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 初始化示例资源数据库
python scripts/init_db.py --sample-data

# 执行链接健康检查
python scripts/check_links.py --config config/default.yaml --output report.md

# 启动本地预览服务器（可选）
python app.py --port 8080
```

---

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.9 或更高 | 核心运行环境，用于 CLI 工具、API 服务和检查脚本 |
| pip | 22.0 或更高 | Python 包管理器，用于安装项目依赖 |
| SQLite | 3.35 或更高 | 默认嵌入式数据库，存储资源元数据和审计日志 |
| curl | 7.68 或更高 | 用于链接健康检查中的备选网络探测（可选） |
| git | 2.25 或更高 | 用于版本管理和贡献流程中的代码同步 |
| jq | 1.6 或更高 | 用于命令行下 JSON 数据处理和格式化输出（可选） |
| pytest | 7.0 或更高 | 仅开发测试阶段需要，用于运行单元测试和集成测试 |

---

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户入门 | `docs/getting-started/` | 如何安装、配置首次运行、添加第一个资源条目并生成展示页面 |
| 配置参考 | `docs/config-reference/` | 所有配置文件（YAML）的字段含义、默认值及示例，涵盖检查策略、输出格式和通知设置 |
| API 手册 | `docs/api/` | RESTful API 的端点列表、请求/响应结构、鉴权方式及错误码说明 |
| 数据规范 | `docs/schema/` | 资源描述模型的完整 JSON Schema，包括元数据字段、标签结构和扩展机制 |
| 运维指南 | `docs/operations/` | 如何部署至生产环境、设置定时健康检查、配置日志轮转和备份策略 |
| 贡献者指引 | `CONTRIBUTING.md` | 代码风格、提交规范、测试流程和 PR 审核标准 |

---

## 资源列表

### 分类：示例资源集合（仅供功能演示）

以下 URL 均为项目默认示例数据中的占位资源，用于展示链接管理、分类标注和健康检查流程。用户可完全替换为自身所需的真实链接。

- <code>jiaoyouyiyeqing.com.cn</code>
- <code>moliaoyue.com.cn</code>
- <code>tongchengyue.com.cn</code>
- <code>yueaiwang.com.cn</code>
- <code>jimonvren.net.cn</code>
- <code>chuguiriji.com.cn</code>
- <code>gaoqingwumaziyuan.com.cn</code>

---

## 项目结构

```
novahorizon/
├── app.py                         # Flask 应用入口，提供 Web 界面和 RESTful API
├── config/
│   ├── default.yaml               # 主配置文件：检查间隔、超时阈值、输出格式
│   ├── logging.yaml               # 日志级别、文件轮转策略
│   └── schema/                    # JSON Schema 定义目录
│       └── resource_v1.json       # 资源条目的完整校验规则
├── scripts/
│   ├── init_db.py                 # 初始化 SQLite 数据库表结构
│   ├── check_links.py             # 核心链接健康检查脚本，支持多线程并发
│   ├── import_from_csv.py         # 从 CSV 批量导入资源条目
│   └── export_to_markdown.py      # 将资源列表渲染为 Markdown 表格
├── src/
│   ├── core/                      # 核心逻辑模块
│   │   ├── resource.py            # 资源数据模型类（校验、序列化）
│   │   ├── checker.py             # HTTP 探测引擎（状态码、响应时间、重定向跟踪）
│   │   └── registry.py            # 资源注册表管理（增删改查、标签索引）
│   ├── api/                       # API 路由及请求处理
│   │   ├── routes.py              # 蓝图定义：/api/v1/ 下的所有端点
│   │   └── validators.py          # 请求参数校验与错误响应封装
│   ├── output/                    # 输出渲染器
│   │   ├── markdown_renderer.py   # 生成 GitHub 风格 Markdown 表格
│   │   ├── html_renderer.py       # 生成带过滤和排序功能的静态 HTML 页面
│   │   └── json_renderer.py       # 输出纯 JSON 数据，用于程序化消费
│   └── utils/                     # 通用工具函数
│       ├── network.py             # 网络请求封装（超时、重试、User-Agent 伪装）
│       ├── logger.py              # 统一日志格式和上下文绑定
│       └── datetime_utils.py      # 时间戳解析、时区转换
├── tests/                         # 单元测试和集成测试
│   ├── unit/
│   │   ├── test_resource.py
│   │   └── test_checker.py
│   └── integration/
│       └── test_api.py
├── docs/                          # 完整文档（见上文文档导航）
├── requirements.txt               # Python 运行时依赖列表
├── README.md                      # 本文档
└── LICENSE                        # MIT 许可证
```

---

## 贡献指南

1. 阅读 `CONTRIBUTING.md` 文档，了解代码风格约定（PEP 8）、提交信息格式（Conventional Commits）和测试覆盖率要求（不低于 85%）。

2. 从 GitHub 仓库 Fork 项目到个人账户，克隆并创建功能分支，分支命名遵循 `feature/` 或 `fix/` 前缀，例如 `feature/add-timeout-config`。

3. 在本地完成开发和自测，运行 `pytest tests/` 确保所有现有测试通过，若新增功能或修复缺陷，请同步补充对应测试用例。

4. 提交前执行 `./scripts/lint.sh` 进行代码风格检查和静态分析，修复所有警告和错误后，推送分支并提交 Pull Request。

5. PR 描述中须说明修改动机、实现方案及影响范围，至少一位项目维护者审阅通过后方可合并。合并后自动触发 CI 流水线（GitHub Actions）进行完整回归测试。

---

## 常见问题

**Q: 链接健康检查是否会因为频繁请求而被目标服务器封禁？**  
A: 项目默认开启请求间隔延迟（`delay` 参数，默认 1 秒），并支持设置 `User-Agent` 伪装和随机延迟抖动。建议针对大型资源列表（超过 1000 条）分批执行，或配置 `--max-concurrent` 限制并发数。此外，检查脚本遵循 `robots.txt` 的隐式约定，不主动绕过访问限制。

**Q: 如何迁移或备份现有的资源数据和审计日志？**  
A: 所有数据默认存储在 SQLite 数据库文件 `data/novahorizon.db` 中，直接复制该文件即可完成完整迁移。若需导出为纯文本格式，可使用 `scripts/export_to_markdown.py` 生成 Markdown 表格，或使用 `scripts/export_to_csv.py` 导出 CSV 用于 Excel 处理。日志文件位于 `logs/` 目录，按天轮转，可根据需求通过 `config/logging.yaml` 调整保留策略。

**Q: 项目是否支持 MySQL 或 PostgreSQL 替代 SQLite？**  
A: 当前版本仅内置 SQLite 支持以保证开箱即用。但从数据模型层设计上，所有数据库操作均通过 SQLAlchemy ORM 抽象，用户可自行修改 `config/default.yaml` 中的 `database_url` 配置项，切换至 MySQL 或 PostgreSQL，需额外安装对应的数据库驱动（如 `pymysql` 或 `psycopg2`）。官方文档的运维指南章节提供了详细的切换步骤和常见问题排查。

---

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-21 22:29:12
