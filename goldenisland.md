# LinkPilot

LinkPilot 是一款面向技术内容创作者、开源项目维护者与数字知识库管理者的轻量级外链资源聚合与导航系统。该项目并非传统意义上的爬虫或书签管理器，而是一个以可维护性、可读性与可审计性为核心的静态外链目录框架，专为需要频繁引用外部资源、构建学习路径或维护项目依赖文档的团队设计。

LinkPilot 解决的是多源外链在项目文档中散落、失效、难以追踪的问题。通过结构化的资源清单、版本化的依赖说明与场景化的分类导航，帮助开发者将零散的 URL 转化为有序的技术资产，从而提升文档的长期可用性与协作效率。本项目尤其适合作为技术博客的引用底座、开源项目的资源附录，或企业内部技术周报的素材池。

## 功能概览

- **静态外链目录生成**：基于 Markdown 与 YAML Front Matter 构建可版本控制的链接清单，支持批量导入与人工校验，避免数据库依赖。

- **多维度资源分类**：支持按技术领域、资源类型（文档/视频/工具）、维护状态（活跃/归档）进行三级标签过滤，便于快速定位。

- **可用性健康检查**：内置基于 GitHub Actions 的定时链接巡检脚本，可检测 HTTP 状态码变更与域名过期信息，输出巡检报告至 Issue 区。

- **自定义元数据扩展**：每条外链允许附加“推荐指数”、“最后验证日期”、“替代链接”等自定义字段，适配不同项目的审计需求。

- **Markdown 原生渲染**：所有资源列表与导航表格均以纯 Markdown 语法呈现，无需 JavaScript 即可在 Git 托管平台、IDE 或静态站点生成器中正常显示。

- **外链引用追溯**：支持在项目内其他文档中通过锚点 ID 引用特定资源，当资源列表变更时，系统可提示受影响文档，降低维护成本。

- **多格式导出**：支持将选定分类下的资源列表导出为 CSV、JSON 或 TOML 格式，便于集成到其他自动化工具或数据看板中。

## 应用场景

- **开源项目外部依赖索引**：当项目 README 或贡献指南中需要引用大量第三方库、API 文档、学习视频时，使用 LinkPilot 维护统一的外链附录，确保贡献者能获取最新有效地址。

- **技术课程或培训材料配套**：培训机构或教育作者可将每节课涉及的延伸阅读链接、实操视频地址整理为 LinkPilot 资源包，学员通过单一清单即可访问全部材料，无需在课件中四处翻找。

- **内部知识库的引用规范化**：企业技术团队在 Confluence、Notion 或 Git 仓库中维护设计文档时，利用 LinkPilot 将频繁引用的外部标准（RFC 文档）、供应商门户、社区讨论帖集中管理，降低文档维护人员逐一检查链接的负担。

- **个人技术博客的参考源仓库**：博主可将撰写文章时参考的视频教程、官方公告、数据来源统一存入 LinkPilot，每篇文章仅需引用资源 ID，既保证引用一致性，也方便读者获取原始材料。

## 快速开始

以下步骤将帮助您在本地环境中快速初始化 LinkPilot 实例，并生成第一份资源目录。

```bash
# 1. 克隆项目仓库至本地
git clone https://github.com/your-org/linkpilot.git
cd linkpilot

# 2. 安装依赖（项目基于 Python 3.10+，需要 pip 和 virtualenv）
python -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 3. 初始化示例资源库并生成静态导航页
python manage.py init --demo
python manage.py build --output ./public

# 4. 启动本地预览服务（默认端口 8000）
python -m http.server -d ./public
```

执行完毕后，访问 `http://localhost:8000` 即可查看生成的导航页面。若需自定义资源条目，请编辑 `data/resources.yaml` 文件后重新执行构建命令。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Python | 3.10 及以上 | 核心脚本运行环境，用于链接巡检与生成逻辑 |
| pip | 22.0+ | Python 包管理工具，用于安装依赖库 |
| Git | 2.30+ | 版本控制，用于克隆仓库及提交资源变更 |
| make | 3.81+ | 可选但推荐，用于自动化任务编排（如每日巡检） |
| curl | 7.68+ | 用于健康检查脚本中的 HTTP 请求探测 |
| yamllint | 1.26+ | 用于校验 resources.yaml 文件的语法正确性 |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|------|-----------|------------|
| 入门 | `docs/quick-start.md` | 如何快速创建第一份资源清单并进行本地预览？ |
| 配置 | `docs/configuration.md` | 如何自定义元数据字段、修改分类标签与巡检频率？ |
| 运维 | `docs/operations.md` | 如何解读巡检报告、处理失效链接、批量更新资源？ |
| 扩展 | `docs/extending.md` | 如何开发自定义导出插件或对接外部 API（如 Slack 通知）？ |

## 资源列表

### 视频资源类（中文外挂字幕相关）

<code>mianfeishipinzhongwenzimu.com.cn</code>

<code>zaixianmianfeiguankannidongde.com.cn</code>

<code>zaixianzhongwenzimuwangzhan.com.cn</code>

<code>zhongwenzimuzaixianyingyuan.com.cn</code>

<code>zhongwenzimumianfeizaixianbofang.com.cn</code>

<code>gaoqingshipinzhongwenzimu.com.cn</code>

<code>zhongwenzimuyirenzaixian.com.cn</code>

## 项目结构

```
linkpilot/
├── .github/                         # GitHub Actions 工作流配置
│   └── workflows/
│       └── health-check.yml         # 定时执行链接巡检（每周一 09:00 UTC）
├── data/
│   ├── resources.yaml               # 主资源清单（核心数据文件）
│   ├── tags.yaml                    # 标签体系与别名定义
│   └── archived/                    # 归档的旧版本资源快照
│       └── 2026-q1.yaml
├── docs/                            # 完整文档目录
│   ├── quick-start.md
│   ├── configuration.md
│   ├── operations.md
│   └── extending.md
├── src/
│   ├── core/                        # 核心解析与索引引擎
│   │   ├── parser.py                # 解析 YAML 并校验必填字段
│   │   └── indexer.py               # 构建内存索引及标签关联
│   ├── checkers/                    # 链接健康检查模块
│   │   ├── http_checker.py          # 基于 curl 的并发状态探测
│   │   └── report_generator.py      # 生成 Markdown 格式巡检报告
│   ├── exporters/                   # 多格式导出器
│   │   ├── csv_exporter.py
│   │   ├── json_exporter.py
│   │   └── toml_exporter.py
│   └── cli/                         # 命令行入口
│       ├── main.py                  # 总入口，分发子命令
│       └── commands.py              # init / build / check / export 实现
├── tests/                           # 单元测试与集成测试
│   ├── test_parser.py
│   ├── test_checker.py
│   └── fixtures/                    # 测试用的示例资源文件
├── public/                          # 构建输出的静态站点目录（默认）
│   ├── index.html                   # 自动生成的导航首页
│   └── reports/                     # 历史巡检报告存档
├── scripts/                         # 辅助运维脚本
│   ├── migrate-v1-to-v2.py          # 数据迁移工具
│   └── sync-to-cdn.sh               # 将 public 目录同步至对象存储
├── Makefile                         # 常用任务快捷命令（如 make check）
├── requirements.txt                 # Python 依赖列表（requests, pyyaml, click）
└── README.md                        # 本文件
```

## 贡献指南

我们欢迎并感谢任何形式的贡献，包括但不限于新增资源条目、改进巡检脚本、完善文档或报告缺陷。请遵循以下流程以确保协作顺畅：

1. **查阅现有议题与项目看板**：在提交拉取请求之前，请访问 GitHub Issues 与 Projects 页面，确认您打算处理的工作尚未被他人认领。若为新需求，请先创建一个议题以讨论可行性。

2. **派生仓库并创建功能分支**：将本仓库派生至您的个人账户，然后基于 `main` 分支创建一个描述性的新分支，例如 `feature/add-video-resources` 或 `fix/http-checker-timeout`。

3. **编写或修改内容并执行自检**：若您更新了 `data/resources.yaml`，请运行 `make lint` 校验 YAML 语法；若修改了 Python 源码，请执行 `pytest tests/` 确保所有单元测试通过，并尽量为新增函数添加测试用例。

4. **提交变更并签署开发者原产地证书**：提交信息请采用约定式提交格式（如 `feat: add new resource group for video subtitles`）。同时，您需要确保提交已签署 DCO（Developer Certificate of Origin），即 `git commit -s`。

5. **发起拉取请求并参与复审**：推送分支后，在 GitHub 上发起 Pull Request 至 `main` 分支。项目维护者将在 3 个工作日内进行复审，并可能要求您调整格式或补充说明。合并后，您的贡献将出现在下一版本的贡献者列表中。

## 常见问题

**问：LinkPilot 是否必须依赖 Python 环境运行？能否用于纯静态项目？**

答：LinkPilot 的核心价值在于其自动化校验与导出能力，这些功能依赖 Python 脚本。如果您仅需要静态 Markdown 表格，可以手动复制 `data/resources.yaml` 中的内容自行渲染，但将失去健康检查与格式校验等特性。我们建议至少使用 Python 3.10 运行巡检脚本，以保持资源列表的长期可用性。

**问：资源列表中的链接发生变更或失效时，系统如何通知我？**

答：我们推荐配置 GitHub Actions 定时任务（参见 `.github/workflows/health-check.yml`）。每次巡检后，系统会自动创建一个新的 Issue 或更新现有 Issue，详细列出状态码异常的链接，并附带 HTTP 状态码与响应时间。您可以根据报告手动更新 YAML 文件中的 `url` 字段或 `status` 标记。若您不使用 GitHub，也可以本地执行 `python manage.py check --report` 生成 Markdown 报告文件。

**问：我可以在一个 LinkPilot 实例中维护多个独立的资源集合（例如不同部门或不同项目）吗？**

答：可以。您可以在 `data/resources.yaml` 中通过顶层字段 `collections` 来划分不同命名空间，每个集合拥有独立的标签体系和元数据默认值。在构建输出时，可通过 `--collection` 参数指定仅生成特定集合的导航页。具体用法请参考 `docs/configuration.md` 中的“多集合管理”章节。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-21 22:29:56
