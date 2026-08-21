# Resource Navigator

Resource Navigator 是一个面向技术研究者和内容分析人员的结构化外链资源管理与导航系统。该项目并非一个传统的网站爬虫或链接收藏工具，而是一个基于语义分类与状态监测的资源聚合框架。其主要目标用户为需要长期追踪特定领域信息源、进行内容趋势分析或构建私有知识库索引的研发人员与数据分析师。

该项目的核心价值在于解决信息源分散、链接失效难以追踪以及资源类型混杂难以筛选的痛点。通过提供统一的资源录入规范、自动化的可用性检查脚本以及清晰的项目文档结构，Resource Navigator 能够帮助用户将零散的 URL 转化为可维护、可共享、可版本控制的结构化数据集，从而提升信息调研与资源管理的效率。

## 功能概览

- **结构化资源录入** 提供标准化的 Markdown 资源清单模板，支持按类别、语种、媒体类型对 URL 进行一级分类，便于团队协作与后续自动化处理。

- **自动化链接状态检测** 集成基于 Python 的轻量级脚本，可定时或手动对资源列表中的域名进行 HTTP 状态码检查，自动标记疑似失效或重定向的链接。

- **语义标签生成辅助** 根据资源域名的关键词特征（如 zimu、shipin、gaoqing 等），自动生成建议性分类标签，减少人工归类的工作量。

- **多维度资源视图** 支持按“最近检查时间”、“响应状态”、“域名类别”等维度对资源列表进行筛选与排序，方便快速定位重点关注对象。

- **变更追踪与审计** 借助 Git 版本控制对资源列表的每一次增删改进行记录，支持回溯任意历史版本的资源集合，满足审计与回溯需求。

- **扩展性钩子接口** 预留自定义脚本接入点，用户可在外围添加通知、报告生成或数据持久化等高级逻辑，而不必修改核心框架代码。

## 应用场景

- **学术研究与内容分析** 研究人员可通过 Resource Navigator 持续追踪特定主题（如影视翻译、字幕组动态）的在线资源，收集一段时间内的域名存活数据，用于网络内容生态或版权传播路径的研究。

- **技术文档与知识库构建** 技术团队在撰写行业分析报告或维护内部知识库时，可利用该项目的结构化列表收录大量参考链接，并通过自动化检测确保文档中引用的外部资源长期有效。

- **个人兴趣资源整理** 对于需要管理大量流媒体相关网站的个人用户，Resource Navigator 提供了一种轻量级、非侵入式的管理方案，将分散的网址集中存储于单一 Markdown 文件中，并辅以分类与备注。

- **开源项目外部依赖索引** 开源软件或框架的维护者可使用该项目记录其依赖的第三方文档、镜像源或插件仓库地址，通过统一格式与定期检查降低因外部链接变动导致的维护成本。

## 快速开始

以下步骤适用于 Linux 与 macOS 环境，Windows 用户建议通过 WSL 或 Git Bash 执行。

```bash
# 1. 克隆项目仓库
git clone https://github.com/example/resource-navigator.git
cd resource-navigator

# 2. 安装 Python 依赖（建议使用虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 3. 运行资源状态检测示例
python scripts/check_links.py --input resources/index.md --output reports/status.json
```

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.8 及以上 | 用于运行链接检测脚本与辅助工具 |
| Git | 2.25 及以上 | 用于版本控制及项目克隆操作 |
| requests | 2.28.0 及以上 | 发送 HTTP 请求进行链接状态探测 |
| markdown | 3.4.0 及以上 | 解析资源列表 Markdown 文件以提取 URL |
| pytest | 7.0.0 及以上 | 用于运行单元测试（开发环境可选） |
| pre-commit | 2.20.0 及以上 | 用于配置 Git 提交前检查钩子（推荐） |

## 文档导航

| 层面 | 目录/文档 | 回答的问题 |
|------|----------|------------|
| 入门 | `docs/quick-start.md` | 如何快速配置第一个资源集合并运行状态检查？ |
| 使用 | `docs/usage-guide.md` | 如何自定义分类标签、调整检查频率及解读状态报告？ |
| 开发 | `docs/development.md` | 如何扩展新的检测协议（如 TCP 检测）、提交补丁或增加新脚本？ |
| 运维 | `docs/operations.md` | 如何将检测结果集成到监控系统或定时任务（cron）中？ |
| 参考 | `docs/reference.md` | 资源列表 YAML 前置字段、脚本参数及错误码的完整说明 |

## 资源列表

### 中文影视资源类

- <code>rihanzaixianshipinguankan.org.cn</code>
- <code>zuixinzhongwenzimuzaixian.org.cn</code>
- <code>zhongwenzaixianguankanshipin.org.cn</code>
- <code>zhongwenzimuzhuanqu.org.cn</code>
- <code>zhongwenzimuzaixianshipinguankan.org.cn</code>
- <code>zhongwenzimugaoqingzaixianguankan.org.cn</code>
- <code>zhongwenzimuzaixianbofangshipin.org.cn</code>

## 项目结构

```
resource-navigator/
├── resources/                         # 核心资源目录
│   ├── index.md                       # 主资源清单（包含所有分类 URL）
│   ├── categories/                    # 按领域拆分的子清单
│   │   ├── media.md                   # 媒体类资源专项列表
│   │   └── archive.md                 # 历史归档资源（备用）
│   └── templates/                     # 新增清单的 Markdown 模板
│       └── resource-template.md
├── scripts/                           # 可执行脚本目录
│   ├── check_links.py                 # 主链接检测脚本
│   ├── report_generator.py            # 生成 HTML/JSON 格式报告
│   └── utils/                         # 公共工具函数
│       ├── parser.py                  # 解析 Markdown 提取 URL
│       └── notifier.py                # 邮件/Webhook 通知接口
├── tests/                             # 单元测试与集成测试
│   ├── test_parser.py
│   ├── test_checker.py
│   └── fixtures/                      # 测试用的固定样例数据
│       └── sample_links.md
├── docs/                              # 完整文档
│   ├── quick-start.md
│   ├── usage-guide.md
│   ├── development.md
│   ├── operations.md
│   └── reference.md
├── reports/                           # 运行时生成的检测报告（Git忽略）
│   ├── latest.json
│   └── history/                       # 历史报告归档目录
├── config/                            # 配置文件目录
│   ├── settings.yaml                  # 主配置（超时、重试、通知规则）
│   └── categories.yaml                # 分类映射与关键词规则
├── .github/                           # GitHub 社区文件
│   ├── ISSUE_TEMPLATE/
│   └── PULL_REQUEST_TEMPLATE.md
├── requirements.txt                   # 生产环境 Python 依赖
├── requirements-dev.txt               # 开发环境额外依赖
├── .pre-commit-config.yaml            # 提交前检查配置
├── LICENSE                            # MIT 许可证
└── README.md                          # 本文件
```

## 贡献指南

我们欢迎并鼓励社区贡献，无论是报告问题、改进文档还是提交新功能。请遵循以下步骤：

1. **查阅现有议题** 访问项目的 Issues 页面，确认您要解决的问题或建议的功能尚未被他人认领或讨论。若无相关议题，请先创建一个新的 Issue 描述您的意图。

2. **派生仓库并创建分支** 将本项目派生至您的个人账户，然后基于 `main` 分支创建一个命名清晰的功能分支，例如 `feature/add-tcp-check` 或 `fix/parser-encoding`。

3. **编写测试并提交代码** 所有新增脚本或对核心逻辑的修改必须包含对应的单元测试（位于 `tests/` 目录）。提交前请运行 `pytest` 确保全部测试通过，并执行 `pre-commit` 检查代码风格。

4. **更新相关文档** 如果您的更改影响了用户可见的功能（如新增配置项或修改命令行参数），请同步更新 `docs/` 下的对应文档以及 `README.md` 中的功能概览。

5. **发起拉取请求** 从您的分支向本仓库的 `main` 分支发起 Pull Request。请清晰描述您的更改内容、测试结果以及相关 Issue 编号。PR 合并前需要至少一名维护者的审阅。

## 常见问题

**Q: 检测脚本提示“连接超时”但浏览器可以正常访问该域名，是什么原因？**

A: 这通常是由于脚本默认的 User-Agent 或请求头被目标服务器拒绝所致。您可以在 `config/settings.yaml` 中调整 `request_headers` 字段，模拟常见浏览器的标识。此外，某些站点可能对 Python 发起的请求存在限流策略，建议适当增加 `retry_interval` 参数值。

**Q: 资源列表中的域名分类规则是固定的吗？如何自定义？**

A: 分类规则不是硬编码的。项目提供了 `config/categories.yaml` 文件，您可以通过修改其中的关键词正则表达式来重新定义分类逻辑。例如，若您需要增加“纪录片”类别，只需在该文件中添加新的关键词映射，无需改动任何 Python 代码。

**Q: 能否将检测结果自动发送到钉钉或飞书？**

A: 可以。项目在 `scripts/utils/notifier.py` 中预留了 Webhook 接口。您只需在 `settings.yaml` 中配置相应的 `webhook_url` 和 `notify_condition`，并根据您使用的平台格式修改 `format_webhook_payload` 函数的返回值即可。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-21 22:29:55
