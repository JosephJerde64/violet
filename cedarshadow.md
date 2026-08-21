# NovaIndex

NovaIndex 是一个面向技术调研、内容聚合与知识工程场景的开源外链资源索引站。它不生产内容，也不抓取页面，而是以结构化、可维护、可扩展的方式，将散落在互联网各处的优质资源链接进行统一收录、分类标注与版本管理。NovaIndex 适用于个人开发者、技术团队、内容运营者以及研究机构，帮助其在信息过载的环境中建立可靠的参考信息源。

NovaIndex 本身不依赖数据库，不涉及后端服务，所有资源记录以 Markdown 形式维护于仓库中，支持静态站点生成、自动化校验与持续集成。通过明确的元数据规范与目录分层，NovaIndex 能够降低资源链接的失效风险，提升外链管理的可协作性，并可作为更复杂知识图谱或推荐系统的基础数据层。

## 功能概览

- **结构化资源登记**：每条资源按类别、域名、语言、可用状态等字段登记，支持批量导入与人工审核。

- **多级分类导航**：资源按主题、地域、语种、服务类型等维度组织，便于不同角色的使用者快速定位。

- **自动化链接检查**：集成 CI 脚本，定期检测已收录链接的可达性与状态码变化，自动标记异常条目。

- **版本化变更记录**：所有增删改操作通过 Git 提交记录追溯，支持回滚、审阅与责任划分。

- **静态站点生成适配**：资源数据可直接映射为 Hugo、VuePress 或 MkDocs 的源文件，无需二次转换。

- **资源元数据扩展**：支持自定义标签、摘要描述、更新频率、备案信息等扩展字段，满足国内合规要求。

- **社区贡献工作流**：基于 Pull Request 的协作模式，外部贡献者可按模板提交新资源，维护者进行复核。

## 应用场景

- **技术文档站的外链附录**：企业或开源项目在文档中需要引用大量外部参考链接时，可使用 NovaIndex 单独维护一个资源索引页面，避免文档正文被过长 URL 干扰，同时保证链接可集中更新。

- **行业信息周报素材库**：内容运营团队每周整理行业动态时，可将发现的优质文章、工具、数据平台先登记到 NovaIndex，再按标签筛选生成周报内容，确保素材不丢失且可追溯。

- **学术研究的参考源管理**：研究机构在开展政策分析或技术预研时，需要长期跟踪多个政府网站、学术数据库与行业白皮书来源。NovaIndex 可帮助记录这些源的入口与变更情况，减少重复查找时间。

- **合规审计的域名备案台账**：针对需要定期审查外部链接合规性的场景，NovaIndex 可记录每个域名的备案号、主办单位、接入商等信息，配合链接检查功能形成可审计的台账。

## 快速开始

以下命令适用于 Linux / macOS / Windows WSL 环境，帮助您在 5 分钟内完成 NovaIndex 的本地部署与预览。

```bash
# 克隆仓库
git clone https://github.com/novaindex/novaindex.git
cd novaindex

# 安装依赖（Python 3.9+ 环境）
pip install -r requirements.txt

# 执行本地资源校验与静态站点生成
python build.py --source ./resources --output ./dist

# 启动本地预览服务（默认端口 8000）
python -m http.server --directory ./dist 8000
```

执行完毕后，访问 `http://localhost:8000` 即可查看生成的资源索引页面。如需自定义分类或添加资源，请编辑 `./resources/catalog.yaml` 与 `./resources/links/` 目录下的 Markdown 文件，重新运行构建命令即可。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 构建脚本与链接检查工具的运行环境 |
| Git | 2.30 及以上 | 仓库克隆、版本管理与提交操作 |
| PyYAML | 6.0 及以上 | 解析分类目录与资源元数据配置文件 |
| requests | 2.28 及以上 | 用于链接可用性检查的 HTTP 请求库 |
| markdown | 3.4 及以上 | 将资源描述从 Markdown 转换为 HTML 片段 |
| pytest | 7.0 及以上 | 可选，用于运行单元测试与校验用例 |
| pre-commit | 2.20 及以上 | 可选，用于本地提交前的格式与链接检查钩子 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | `docs/user-guide/` | 如何浏览索引、筛选资源、查看详情及反馈问题 |
| 维护者手册 | `docs/maintainer-guide/` | 如何新增/修改/删除资源、如何合并贡献、如何触发 CI 检查 |
| 开发参考 | `docs/developer-guide/` | 构建脚本的模块划分、配置文件格式、扩展自定义检查规则 |
| 设计说明 | `docs/design/` | 索引结构设计原则、元数据字段含义、分类体系设计依据 |
| 部署示例 | `docs/deployment/` | 如何将生成结果部署到 Nginx、OSS 或 Pages 服务 |
| 常见问题 | `docs/faq/` | 收录标准、链接失效处理、备案合规等常见疑问解答 |
| 版本历史 | `CHANGELOG.md` | 各版本的功能变更、修复内容与兼容性说明 |

## 资源列表

### 综合类资源入口

<code>guochanzhenshizipai.com.cn</code>

<code>wuyezaixianjuchang.com.cn</code>

### 日语在线内容相关

<code>rihanzaixianw.org.cn</code>

<code>rihanzaixianshipinguankan.org.cn</code>

### 中文字幕与影视资源

<code>zuixinzhongwenzimuzaixian.org.cn</code>

<code>zhongwenzaixianguankanshipin.org.cn</code>

<code>zhongwenzimuzhuanqu.org.cn</code>

## 项目结构

```
novaindex/
├── build.py                 # 主构建脚本，负责读取资源、生成静态页面
├── requirements.txt         # Python 依赖列表
├── .pre-commit-config.yaml  # 预提交钩子配置，用于格式与链接检查
├── .github/
│   └── workflows/
│       └── ci.yml           # GitHub Actions 持续集成流水线，每日检查链接可用性
├── resources/
│   ├── catalog.yaml         # 分类体系定义，含一级分类、二级标签及显示顺序
│   ├── links/               # 所有资源条目按子目录存放，每个条目一个 .md 文件
│   │   ├── domestic/        # 国内可访问资源，含备案信息字段
│   │   ├── overseas/        # 海外资源，含网络环境备注字段
│   │   └── special/         # 特殊类型资源，如文件站、聚合页等
│   └── meta/
│       └── domain_aliases.yaml  # 域名别名映射，用于识别同一主体下的不同域名
├── docs/                    # 完整文档目录，覆盖用户、维护者、开发者三类角色
│   ├── user-guide/
│   ├── maintainer-guide/
│   ├── developer-guide/
│   ├── design/
│   ├── deployment/
│   └── faq/
├── tests/                   # 单元测试与集成测试脚本
│   ├── test_builder.py      # 测试构建流程各环节
│   ├── test_checker.py      # 测试链接检查逻辑
│   └── fixtures/            # 测试用的样例资源文件
├── templates/               # 静态页面生成所使用的 Jinja2 模板
│   ├── index.html.j2        # 首页分类导航模板
│   ├── category.html.j2     # 分类详情页模板
│   └── detail.html.j2       # 单个资源详情页模板
└── dist/                    # 构建输出目录（不纳入版本控制）
    ├── index.html
    ├── categories/
    └── assets/
```

## 贡献指南

1. **阅读贡献者行为准则**：所有贡献者需遵守项目内的 `CODE_OF_CONDUCT.md`，确保沟通礼貌、讨论聚焦于技术内容。

2. **选择贡献类型并查找对应模板**：新资源推荐请使用 `.github/ISSUE_TEMPLATE/resource_request.md` 提交申请；链接失效报告请使用 `broken_link_report.md`；代码或文档改进请直接提交 Pull Request。

3. **本地环境自检**：在提交前，请确保本地已安装所有开发依赖，并执行 `pytest tests/` 通过全部测试用例，同时运行 `pre-commit run --all-files` 通过所有钩子检查。

4. **提交 Pull Request 并关联 Issue**：分支命名请遵循 `feature/` 或 `fix/` 前缀，PR 描述中需明确说明改动目的、涉及资源条目及测试结果。PR 需要至少一位维护者审阅通过后合入主分支。

5. **定期参与资源清理**：维护者团队每季度会发布一期“资源健康度报告”，欢迎贡献者协助复核高失效风险条目，并在讨论区提交清理建议。

## 常见问题

**Q：收录资源是否有审核标准？是否接受任何类型的外链？**

A：NovaIndex 主要收录具有稳定内容输出能力、主题明确且无恶意代码的站点。不接受纯广告页、镜像站、盗版内容或频繁变更域名的资源。所有新资源需经维护者人工复核，复核周期通常为 3 个工作日。若资源属于影视或字幕类，需同时备注其内容合规说明。

**Q：如果收录的链接失效了，我应该如何报告？**

A：您可以在仓库的 Issues 中选择“链接失效报告”模板，填写资源名称、当前返回状态码及访问时间。我们建议同时提供互联网档案馆的快照链接作为参考。维护者收到报告后会进行二次确认，若确认失效则会在下一个版本中标记为“已下线”或移除条目。

**Q：我可以将 NovaIndex 用于商业项目吗？是否需要支付费用？**

A：可以。NovaIndex 采用 MIT 许可证发布，您可以在商业项目中免费使用、修改和再分发，无需支付任何费用，也无需公开您的修改代码。但我们希望您保留原始版权声明，并欢迎将改进反馈给上游社区。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-21 22:29:12
