# Nova Index

Nova Index 是一个面向技术调研、数据挖掘与内容聚合场景的轻量级外链资源索引系统。项目定位为可自部署的导航与引用信息库，主要服务于需要频繁查阅特定垂直领域在线资料的研究人员、内容运营团队以及个人知识管理用户。系统通过结构化的分类索引和稳定的资源引用记录，帮助用户降低重复查找成本，并保持对高价值信息源的持续跟踪。

本项目的核心功能并非提供内容托管或代理服务，而是对分散在多个域名的公开资源进行语义化归类与可读性整理。项目本身不依赖动态数据库，所有索引数据以纯文本形式维护，便于版本控制与协作编辑。通过本项目提供的脚本工具，用户可以快速验证链接可用性、生成索引快照，并导出为 HTML 或 JSON 格式供其他系统调用。

## 功能概览

**静态索引生成** 基于配置文件自动生成分类导航页面，支持多级目录结构，输出为纯静态 HTML 文件，可直接部署于任何 Web 服务器或对象存储服务。

**链接状态巡检** 内置轻量级 HTTP 探测器，支持批量检测索引中所有外部链接的响应状态码，并生成可用性报告，便于定期维护。

**Markdown 编排支持** 所有索引条目均以 Markdown 格式撰写，支持标准语法扩展，可无缝集成到大多数文档平台或代码仓库中。

**多格式数据导出** 提供命令行工具，支持将索引数据导出为 JSON、CSV 或 YAML 格式，方便与其他数据处理流水线对接。

**自定义分类标签** 允许用户为每个资源链接添加多个自定义标签，并支持按标签组合过滤检索，满足精细化筛选需求。

**低依赖运行环境** 核心脚本仅依赖 Python 标准库，无需额外安装第三方包，可在任何带有 Python 解释器的系统上直接运行。

**变更历史追踪** 配合 Git 版本管理，每次索引更新均可记录变更内容，支持回溯任意历史版本，提升协作透明度。

## 应用场景

**垂直领域资料整理** 技术团队可将 Nova Index 用于维护内部常用的开发文档、API 参考站点或开源工具列表，统一团队知识入口，减少信息孤岛。通过定期巡检功能，可及时发现失效链接并更新替代资源。

**内容运营编辑台** 内容编辑人员在策划专题或撰写综述文章时，可使用本项目整理备选参考资料和素材来源。分类索引结构有助于快速定位同类站点，提高选题调研效率。

**个人知识管理补充** 个人用户可将频繁访问的特定领域站点（如技术博客、行业资讯、数据查询页）纳入索引，配合导出功能生成浏览器书签文件或自定义启动页，替代传统浏览器收藏夹的扁平管理方式。

**数据采集前期调研** 数据采集工程师在规划爬虫任务或数据源筛选时，可通过 Nova Index 预先收集并评估候选站点的稳定性和内容更新频率，为后续开发提供基础参考清单。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境。请确保系统已安装 Python 3.8 或更高版本。

```bash
# 克隆项目仓库
git clone https://github.com/novaindex/novaindex.git
cd novaindex

# 安装本地脚本（可选，使用 -e 模式便于开发调试）
pip install -e .

# 初始化默认索引配置
nova-cli init

# 构建静态站点（默认输出至 _build 目录）
nova-cli build

# 启动本地预览服务（默认监听 8000 端口）
nova-cli serve --port 8000
```

首次运行 `nova-cli init` 会在项目根目录生成 `index.yml` 示例配置文件和 `entries/` 目录，用户可按示例格式添加或修改资源条目。修改完成后执行 `build` 命令即可生成最新页面。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.8 及以上 | 解释器运行时，用于执行所有核心脚本 |
| pip | 20.0 及以上 | Python 包管理工具，用于安装项目脚本 |
| Git | 2.20 及以上 | 版本控制工具，用于克隆仓库和提交变更 |
| 操作系统 | Linux / macOS / Windows WSL | 支持 Unix 风格路径和命令行工具 |
| 网络连接 | 稳定公网访问 | 用于链接巡检功能发送 HTTP 请求 |
| 浏览器 | 任意现代浏览器 | 用于预览生成的静态 HTML 页面（可选） |
| 文本编辑器 | 支持 UTF-8 编码 | 用于编辑 YAML / Markdown 配置文件 |
| make | 3.8 及以上 | 用于执行 Makefile 中的自动化任务（可选） |
| curl | 7.0 及以上 | 用于测试脚本中的网络工具链（可选） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/user-guide/ | 如何安装、配置、构建和部署索引站点 |
| 配置参考 | docs/config-reference/ | YAML 配置文件中各字段的含义与取值示例 |
| 命令行工具 | docs/cli-commands/ | 所有支持的子命令、选项参数和退出码说明 |
| 开发指南 | docs/developer-guide/ | 项目代码结构、测试流程和提交规范 |

## 资源列表

### 特定主题索引分类

<code>jimonvren.net.cn</code>

<code>chuguiriji.com.cn</code>

<code>gaoqingwumaziyuan.com.cn</code>

<code>ribennvyoutuijian.com.cn</code>

<code>guochanzhenshizipai.com.cn</code>

### 在线影音与娱乐相关分类

<code>wuyezaixianjuchang.com.cn</code>

### 综合信息聚合分类

<code>rihanzaixianw.org.cn</code>

## 项目结构

```
novaindex/
├── .gitignore                # Git 忽略规则，排除临时文件和构建产物
├── Makefile                  # 常用任务快捷命令，如 clean / test / deploy
├── README.md                 # 项目说明文档（本文件）
├── LICENSE                   # MIT 许可证全文
├── setup.py                  # Python 安装脚本，定义入口点与元信息
├── requirements.txt          # 开发环境额外依赖（用于测试和文档生成）
├── index.yml                 # 主索引配置文件，用户自定义分类层级
├── entries/                  # 资源条目存储目录（按分类子目录组织）
│   ├── category-a/           # 示例分类 A 的条目文件
│   │   ├── entry1.md
│   │   └── entry2.md
│   ├── category-b/           # 示例分类 B 的条目文件
│   │   └── sub-category/     # 支持多级子分类
│   │       └── entry3.md
│   └── _templates/           # 新条目的 Markdown 模板文件
├── src/                      # 核心 Python 源代码
│   ├── __init__.py
│   ├── cli.py                # 命令行接口主入口
│   ├── builder.py            # 静态页面构建逻辑
│   ├── checker.py            # 链接可用性巡检模块
│   ├── exporter.py           # JSON / CSV / YAML 导出器
│   └── utils.py              # 通用工具函数（路径处理、HTTP 请求）
├── tests/                    # 单元测试与集成测试脚本
│   ├── test_builder.py
│   ├── test_checker.py
│   └── fixtures/             # 测试用的固定配置样例
├── docs/                     # 完整文档源文件（Markdown 格式）
│   ├── user-guide/
│   ├── config-reference/
│   ├── cli-commands/
│   └── developer-guide/
└── _build/                   # 构建输出目录（默认生成，不入库）
    ├── index.html
    ├── categories/
    └── assets/
```

## 贡献指南

**提交问题报告** 请使用 GitHub Issues 提交 bug 报告或功能请求。提交前请先搜索已有 issue 以避免重复，并附上可复现的步骤、环境信息和相关日志。

**改进文档内容** 文档位于 `docs/` 目录下，接受拼写修正、示例补充和章节重组织。修改后请确保本地 `make docs` 构建无警告，并提交单独的 Pull Request。

**新增索引分类模板** 若希望扩展默认分类体系，可在 `entries/` 下新增子目录并提供对应的 `_category.yml` 描述文件。新增分类需包含名称、描述和至少一个示例条目。

**代码变更流程** 所有代码变更应基于 `main` 分支创建特性分支，完成后提交 Pull Request。提交前请运行 `make test` 确保所有测试通过，并遵守 PEP 8 代码风格。核心模块的新增功能需附带相应单元测试。

## 常见问题

**链接巡检报告显示大量超时，如何调整检测参数？**

默认超时时间为 5 秒，并发数为 10。若网络环境较差，可在执行 `nova-cli check` 时通过 `--timeout` 和 `--workers` 参数分别调整。例如 `nova-cli check --timeout 10 --workers 5` 可降低并发并延长等待时间。部分站点可能启用反爬机制，可尝试增加 `--user-agent` 参数自定义请求头。

**如何迁移已有书签或收藏夹到 Nova Index？**

项目提供 `import` 子命令（需启用实验性功能），支持从 Chrome / Firefox 导出的 HTML 书签文件或通用 CSV 格式转换。具体用法请参考 `docs/user-guide/import-export.md`。转换后系统会自动尝试匹配现有分类，用户可手动调整 `index.yml` 中的映射关系。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-21 22:29:55
