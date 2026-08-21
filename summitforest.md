# Rihan Resource Hub

Rihan Resource Hub 是一个面向中文用户的技术资源导航与外部链接汇总平台，专注于收集、整理和展示互联网上具有实际使用价值的工具型网站与内容型站点。项目定位为轻量级的技术资源索引系统，主要服务于开发者、内容研究者、语言学习者和跨境互联网从业人员，帮助其快速定位并访问特定功能类站点，避免在分散的书签或搜索引擎中反复试错。

本项目本身不存储、不分发任何第三方内容，仅作为公开可访问的链接聚合层，以结构化方式呈现外部资源入口。所有收录站点均经过基础可用性校验，并按功能维度进行分类管理，便于用户按场景批量访问。

## 功能概览

- 资源分类导航：按站点功能与内容类型进行一级分类，支持按语言、媒体格式、服务地区快速筛选。
- 外部链接跳转：每个收录条目提供直达外部站点的纯文本链接，不附加跟踪参数或中间跳转页。
- 可用性状态标注：对每个收录的 URL 定期进行基础 HTTP 可达性检测，并在列表中标注当前状态。
- 分类视图切换：支持按“全部资源”、“语言类”、“媒体类”、“工具类”等预设视图切换展示。
- 搜索过滤：提供基于域名关键词和站点描述文本的实时搜索过滤能力，支持大小写不敏感匹配。
- 批量导出：允许用户将当前筛选结果导出为纯文本 URL 列表，便于批量导入其他工具。
- 提交与反馈入口：提供公开的站点提交通道，允许用户推荐新资源，经审核后可纳入索引。

## 应用场景

- 语言学习材料检索：用户需要查找提供中文或特定语言字幕的在线视频资源时，可通过本导航快速定位相关站点，无需在多个搜索引擎间反复切换查询词。
- 跨境内容比对研究：从事海外内容分析或市场调研的人员，可通过本平台同时访问多个区域性的媒体资源站，进行内容对比和趋势观察。
- 开发测试用外部依赖源：开发人员在构建需要外部媒体链接的测试环境时，可使用本导航提供的稳定 URL 列表作为数据源或测试样本。
- 日常书签替代方案：普通用户可将本导航作为浏览器首页或书签替代，按需访问整理好的常用站点，减少手动维护书签分类的成本。

## 快速开始

以下步骤适用于在本地环境部署 Rihan Resource Hub 的静态站点版本，用于个人或团队内部使用。

```bash
# 克隆项目仓库
git clone https://github.com/rihan-resource/rihan-hub.git

# 进入项目目录
cd rihan-hub

# 安装依赖（基于 Node.js 18+ 与 npm）
npm install

# 启动本地开发服务器
npm run dev
```

访问控制台输出的本地地址（通常为 `http://localhost:3000`）即可预览导航页面。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Node.js | 18.x 或更高 | 运行时环境，用于构建与本地服务 |
| npm | 9.x 或更高 | 包管理器，用于安装项目依赖 |
| Git | 2.30 或更高 | 版本控制工具，用于克隆仓库 |
| 现代浏览器 | Chrome 110+ / Firefox 110+ / Edge 110+ | 前端界面运行环境，需支持 ES2022 |
| 网络连接 | 稳定公网访问 | 用于首次启动时同步资源索引更新 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户指南 | `/docs/user-guide.md` | 如何使用分类导航、搜索过滤和导出功能 |
| 维护手册 | `/docs/maintainer-guide.md` | 如何新增、编辑或移除资源条目，如何更新可用性状态 |
| 部署说明 | `/docs/deployment.md` | 如何将项目部署到生产环境（Vercel / Netlify / 自建服务器） |
| 数据格式规范 | `/docs/data-schema.md` | 资源索引文件（JSON）的字段定义与扩展规则 |

## 资源列表

本导航当前收录的外部资源站点均为公开可访问的独立域名，按功能类别划分如下。

### 中文视频与字幕类资源

- <code>rihanzaixianw.org.cn</code>
- <code>rihanzaixianshipinguankan.org.cn</code>
- <code>zuixinzhongwenzimuzaixian.org.cn</code>
- <code>zhongwenzaixianguankanshipin.org.cn</code>
- <code>zhongwenzimuzhuanqu.org.cn</code>
- <code>zhongwenzimuzaixianshipinguankan.org.cn</code>
- <code>zhongwenzimugaoqingzaixianguankan.org.cn</code>

## 项目结构

```
rihan-hub/
├── public/                         # 静态资源目录
│   └── favicon.ico                 # 站点图标
├── src/                            # 源代码主目录
│   ├── assets/                     # 样式与图片资源
│   │   ├── styles/                 # CSS 模块与全局样式
│   │   └── images/                 # 界面用图
│   ├── components/                 # UI 组件库
│   │   ├── NavBar/                 # 顶部导航栏组件
│   │   ├── ResourceList/           # 资源列表渲染组件
│   │   ├── FilterPanel/            # 搜索与分类过滤面板
│   │   └── StatusBadge/            # 可用性状态标签组件
│   ├── data/                       # 数据层
│   │   ├── resources.json          # 主资源索引文件（所有 URL 及元数据）
│   │   └── categories.json         # 分类定义与显示配置
│   ├── hooks/                      # 自定义 React Hooks
│   │   ├── useFilter.js            # 搜索与筛选逻辑
│   │   └── useStatusCheck.js       # 可用性检测钩子
│   ├── pages/                      # 页面路由
│   │   ├── index.jsx               # 首页列表视图
│   │   └── about.jsx               # 项目介绍页
│   └── utils/                      # 工具函数
│       ├── validator.js            # URL 格式校验与规范化
│       └── exporter.js             # 导出功能实现
├── tests/                          # 单元测试与集成测试脚本
├── docs/                           # 项目文档
├── .gitignore                      # Git 忽略文件配置
├── package.json                    # npm 依赖与脚本声明
├── README.md                       # 项目说明文档（本文件）
└── LICENSE                         # MIT 许可证文本
```

## 贡献指南

我们欢迎社区贡献者参与资源索引的扩充与维护。请遵循以下步骤提交变更。

1. 复刻本项目仓库至个人账户，并克隆到本地开发环境。
2. 在 `src/data/resources.json` 中按既有格式追加或修改资源条目，确保每个条目包含 `id`、`url`、`category`、`description` 和 `status` 字段。
3. 在本地执行 `npm run test` 运行所有校验测试，确保新增数据不破坏现有结构或类型约束。
4. 提交变更时请使用语义化提交信息，例如 `feat: add new resource entry` 或 `fix: update status for existing domain`。
5. 创建 Pull Request 至主仓库的 `main` 分支，并在描述中说明变更原因与验证方式。

## 常见问题

**问：收录的某个站点无法访问，应该怎么办？**

答：本站对收录 URL 的可用性检测基于 HTTP 状态码与响应时间，若您发现某个站点持续不可用，请通过 GitHub Issues 提交反馈，或直接在资源条目中标注异常状态。维护团队会定期复查并决定是否保留该条目。

**问：如何申请将自己的站点加入导航？**

答：请在项目仓库的 `Issues` 页面选择“资源提交”模板，填写站点 URL、分类、简短描述以及联系邮箱。审核通过后，会在下一个索引更新周期中纳入列表。提交前请确认该站点符合公开访问、内容合法且与本站定位相关的要求。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-21 22:29:12
