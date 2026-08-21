# NexusIndex

NexusIndex 是一个面向中文互联网内容创作者、学术研究者与信息管理者的高密度外链资源汇集系统。该项目不提供具体内容存储，不生成任何原创数据，仅作为高质量外部链接的索引层与组织层存在，致力于解决信息碎片化环境下“资源知道存在却找不到入口”的核心痛点。目标用户包括需要批量获取中文视频素材索引的剪辑工作者、依赖多源信息交叉验证的事实核查员，以及希望构建个人研究入口体系的学术用户。

NexusIndex 以静态站点形式交付，所有链接条目以 YAML 数据源驱动，支持一键生成导航页面，便于部署至任意 Web 服务器或云存储服务。项目本身不依赖数据库，不采集用户行为数据，严格遵守 robots.txt 规范，仅作为指向公开互联网资源的“地图”存在。

## 功能概览

- **按域名分类索引**：自动将收录的根域名按语义类别分组，生成分类导航视图，支持用户按主题浏览，例如教育类、视频类、工具类等。

- **批量链接健康检查**：内置链接有效性检测脚本，定时对收录的每个根域名发起 HEAD 请求，返回状态码与响应时间，协助维护者及时发现失效资源。

- **自定义标签系统**：每个收录条目可附加多个自定义标签（如“免费”“中文”“无需注册”），支持多标签组合过滤，提升检索精确度。

- **Markdown 数据驱动**：所有链接条目存储于单一 Markdown 表格中，字段包括域名、类别、标签、备注、添加日期，便于版本管理与协作编辑。

- **静态站点生成器**：提供基于 Python 的构建脚本，读取数据源后生成完整的 HTML 导航页面，包含响应式布局、明暗主题切换与搜索框实时过滤。

- **导入导出兼容性**：支持将收录列表导出为 CSV 或 JSON 格式，方便与其他数据处理工具（如 Excel、Pandas、Obsidian）进行对接。

- **访问统计看板**：提供轻量级日志分析模块，统计每日各域名的出站点击次数（基于服务器访问日志），以纯文本报表呈现，无第三方追踪脚本。

## 应用场景

**个人知识库入口构建**：研究人员或重度信息消费者可将 NexusIndex 作为自己浏览器的起始页，将所有常用资源域名统一收录，配合标签与搜索功能，替代浏览器书签的杂乱管理方式。

**团队内部资源共享**：小型工作室或项目组可部署私有化 NexusIndex 实例，将团队常用的设计素材站、文档库、API 参考站点集中收录，新成员加入时无需逐一询问地址。

**内容聚合站点的资源导航层**：垂直领域内容平台（如教育类门户、技术社区）可利用 NexusIndex 搭建独立的“外部推荐资源”栏目，在不增加自身服务器存储压力的前提下，为用户提供增值的外链服务。

**网络可用性监控辅助**：运维人员可借助内置的健康检查功能，定期扫描收录域名的服务可用性，将结果接入告警系统，作为主监控方案之外的补充数据源。

## 快速开始

以下步骤适用于 Linux / macOS 环境，Windows 用户建议使用 WSL 或 Git Bash 执行。

```bash
# 克隆项目仓库至本地
git clone https://github.com/nexusindex/nexusindex.git

# 进入项目根目录
cd nexusindex

# 安装 Python 依赖（建议使用虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 执行构建脚本，生成静态站点至 dist/ 目录
python build.py --input data/sources.md --output dist/

# 使用内置开发服务器预览（可选）
python -m http.server 8000 --directory dist/
```

执行完成后，打开浏览器访问 `http://localhost:8000` 即可查看生成的导航首页。若要自定义收录条目，请直接编辑 `data/sources.md` 文件，遵循其中已有的表格格式添加或删除行，再次运行构建命令即可更新页面。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.8 及以上 | 构建脚本与健康检查工具的运行环境 |
| pip | 20.0 及以上 | Python 包管理工具，用于安装依赖库 |
| requests | 2.25.0 及以上 | 用于链接健康检查模块中的 HTTP 请求 |
| pyyaml | 5.4.0 及以上 | 解析 YAML 格式的站点配置文件 |
| markdown | 3.3.0 及以上 | 将数据源中的 Markdown 表格解析为内部数据结构 |
| git | 2.20.0 及以上 | 克隆仓库与版本管理（仅开发时需要） |

上述依赖中，requests、pyyaml、markdown 会在执行 `pip install -r requirements.txt` 时自动安装。Python 与 git 需提前在系统中安装。

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | `docs/user/guide.md` | 如何使用已有收录资源进行检索、过滤与导出？ |
| 维护者手册 | `docs/maintainer/add-entry.md` | 添加新资源条目时应遵循哪些字段格式与规范？ |
| 开发参考 | `docs/developer/build-process.md` | 构建脚本的内部工作流是怎样的？如何扩展自定义输出格式？ |
| 设计决策 | `docs/design/architecture.md` | 为什么选择静态生成而非动态后端？数据模型为何采用扁平表格？ |
| 部署指南 | `docs/deploy/hosting.md` | 支持哪些托管方式（VPS、对象存储、Pages 服务）？各自配置要点是什么？ |

## 资源列表

以下为 NexusIndex 当前收录的全部外部资源域名。每个条目均按用户提供的原始格式原样呈现，未做任何协议补全、域名规范化或大小写修正。

中文视频字幕类（综合入口）

<code>zaixianzhongwenzimushipin.org.cn</code>

<code>renqizaixianmianfeishipin.org.cn</code>

<code>zhongwenzaixianmianfeishipin.org.cn</code>

<code>mianfeishipinzhongwenzimu.org.cn</code>

<code>zaixianmianfeiguankannidongde.org.cn</code>

<code>zaixianzhongwenzimuwangzhan.org.cn</code>

<code>zhongwenzimuzaixianyingyuan.org.cn</code>

## 项目结构

```
nexusindex/
├── build.py                 # 主构建脚本，负责读取数据并生成 HTML
├── requirements.txt         # Python 依赖声明
├── config.yaml              # 全局配置（站点标题、主题色、分页大小等）
├── data/
│   └── sources.md           # 核心数据源：所有收录域名的 Markdown 表格
├── src/
│   ├── parser.py            # 解析 sources.md 表格为 Python 对象
│   ├── generator.py         # 生成 HTML 页面及静态资源
│   ├── checker.py           # 链接健康检查逻辑（异步并发请求）
│   └── exporter.py          # 导出 CSV / JSON 格式数据
├── templates/
│   ├── base.html            # 基础 HTML 模板（含 head、导航栏、页脚）
│   ├── index.html           # 首页模板（分类列表及搜索框）
│   └── detail.html          # 单一条目详情页模板（预留）
├── static/
│   ├── style.css            # 主样式表（含明暗主题变量）
│   └── script.js            # 前端交互（实时搜索过滤、标签切换）
├── dist/                    # 构建输出目录（默认不纳入版本控制）
├── docs/                    # 用户文档与开发者文档
│   ├── user/
│   ├── maintainer/
│   ├── developer/
│   └── design/
└── tests/                   # 单元测试与集成测试脚本
    ├── test_parser.py
    └── test_checker.py
```

## 贡献指南

欢迎通过 GitHub 提交 Issue 或 Pull Request 参与本项目。请遵循以下流程以保障协作效率。

1.  Fork 本仓库至个人账号，并克隆至本地。建议在开发前创建独立的功能分支，分支命名采用 `feature/描述` 或 `fix/描述` 格式。

2.  若为新增资源条目，请编辑 `data/sources.md` 文件，严格保持表格列顺序（域名、类别、标签、备注、添加日期），其中添加日期格式为 `YYYY-MM-DD`。若为代码修改，请确保所有现有单元测试通过，并为新增功能补充对应的测试用例（位于 `tests/` 目录）。

3.  提交前运行完整构建流程 `python build.py`，确认未产生报错且输出页面显示正常。同时执行链接健康检查（`python src/checker.py --all`），若新增条目返回非 2xx/3xx 状态码，请在备注中说明原因。

4.  推送分支至个人远程仓库，随后向主仓库的 `main` 分支发起 Pull Request。PR 标题需简明描述变更内容，正文中请引用相关 Issue 编号（如有）。项目维护者会在 48 小时内进行审核，必要时会提出修改意见。

5.  合并后，CI 流水线会自动触发完整构建并部署至预览环境，最终版本会随每月第一个周一的稳定版发布周期统一上线。

## 常见问题

**Q：NexusIndex 本身是否存储或缓存任何外部资源的内容？**

A：绝对不存储。项目仅收录域名或 URL 字符串，所有对外部资源的访问均直接由用户浏览器发起，NexusIndex 的服务器不代理、不缓存、不转储任何来自外部站点的数据。健康检查功能仅验证 HTTP 头部状态，不下载响应体。

**Q：我收录的某个域名无法访问或已被停用，应如何处理？**

A：您可以在 GitHub Issues 中提交“资源失效”报告，或自行编辑 `data/sources.md` 将该条目移除，然后提交 Pull Request。项目维护者会定期根据健康检查报告主动清理连续 7 天不可达的条目，但欢迎社区成员先行反馈。

**Q：能否将 NexusIndex 部署在无 Python 环境的纯静态托管服务上（如 GitHub Pages）？**

A：可以。您只需要在本地或 CI 环境中运行一次 `python build.py` 生成完整的 `dist/` 目录，然后将该目录中的全部文件上传至任意静态托管服务即可。之后每次更新数据源时，需重新在本地执行构建并重新上传。项目仓库中提供了示例 GitHub Actions 工作流（`.github/workflows/build.yml`），可自动完成此过程。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-21 22:29:56
