# ZimuLink 资源导航系统

ZimuLink 是一个面向中文影视爱好者和字幕检索需求的开源导航聚合平台，专注于收集、整理和归类互联网上公开可访问的中文字幕在线观看与字幕资源站点。项目定位为技术型外链资源目录，不存储、不分发任何受版权保护的媒体文件，仅提供公开 URL 的索引与可用性监测服务。

项目主要服务于以下三类用户：需要快速定位中文字幕在线播放源的内容消费者、希望监测字幕站点可用性与响应时间的运维工程师、以及需要批量获取影视资源外链用于学术研究或数据分析的研究人员。ZimuLink 通过自动化检测机制对收录的域名进行可达性验证和响应时长记录，并在前端面板中以结构化方式呈现健康状态，帮助用户在众多候选站点中快速筛选出当前可用的播放或字幕下载入口。

## 功能概览

- **域名可用性拨测**：系统每 30 分钟对全部收录域名发起 HTTP/HTTPS 探活请求，记录状态码、响应时间与 TLS 握手耗时，并在界面中以颜色标记区分正常、降级与离线三种状态。

- **分类标签体系**：支持按资源类型（在线播放、字幕下载、影视资讯）、语言范围（中文字幕、双语字幕、原音无字）和更新频率（每日更新、每周更新、不定期更新）进行多维度筛选与排序。

- **站点详情快照**：每个收录条目包含域名注册时间、SSL 证书有效期、历史可用率趋势图以及最近七天的响应时间折线图，所有数据保留三十天滚动窗口。

- **自定义监控阈值**：用户可针对单个域名单独设置超时阈值（默认 5000 毫秒）和重试次数（默认 3 次），配置保存在浏览器本地存储中，无需后端数据库。

- **批量导入与导出**：支持 CSV 和 JSON 格式的链接批量导入，同时提供一键导出当前筛选结果的功能，方便运维人员备份或迁移监控配置。

- **RESTful API 接口**：提供 `/api/v1/domains`、`/api/v1/status`、`/api/v1/history` 三个标准接口，返回 JSON 格式数据，供第三方工具集成调用。

- **暗色主题与响应式布局**：界面适配桌面端与移动端，内置亮色和暗色两套配色方案，跟随系统偏好自动切换或由用户手动指定。

## 应用场景

- **影视爱好者日常选站**：当用户发现某个常用字幕站点无法打开时，可以通过 ZimuLink 面板快速查看同类别下其他替代站点的当前可用状态，避免逐个手动尝试的繁琐过程。

- **运维团队可用性巡检**：企业内网运维人员可将 ZimuLink 部署为内部工具，对多个外部字幕资源域名进行集中式健康监测，结合邮件告警功能在站点离线时第一时间收到通知。

- **数据分析师采集前筛源**：在进行影视数据爬取或舆情分析之前，分析师可以借助 ZimuLink 的历史可用率统计筛选出稳定性较高的域名列表，降低采集任务中的请求失败率。

## 快速开始

```bash
# 克隆项目仓库至本地
git clone https://github.com/zimulink/zimulink-navigator.git

# 进入项目根目录
cd zimulink-navigator

# 安装项目依赖（使用 npm）
npm install

# 启动开发服务器，默认监听 http://localhost:5173
npm run dev
```

生产环境构建与部署：

```bash
# 构建静态文件
npm run build

# 预览构建结果
npm run preview

# 使用 pm2 部署（需提前安装 pm2）
pm2 start ecosystem.config.js
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x 或 20.x LTS | 运行时环境，需支持 ES2022 特性 |
| npm | 9.x 或 10.x | 包管理器，用于安装第三方库 |
| Git | 2.30 及以上 | 版本控制工具，用于克隆和拉取更新 |
| 现代浏览器 | Chrome 110+ / Firefox 110+ / Edge 110+ | 前端界面运行环境，需支持 CSS Grid 和 Fetch API |
| 网络连通性 | 可访问公网 | 用于对收录域名执行拨测请求，内网部署需配置出口代理 |

## 文档导航

| 层面 | 目录路径 | 回答的问题 |
|---|---|---|
| 用户手册 | `/docs/user-guide/` | 如何使用筛选面板、查看历史趋势、配置个人监控阈值 |
| 运维手册 | `/docs/ops-guide/` | 如何修改监控间隔、调整告警规则、迁移数据存储 |
| API 参考 | `/docs/api-reference/` | RESTful 接口的请求参数、返回字段释义及错误码说明 |
| 开发指引 | `/docs/development/` | 项目目录结构说明、新增数据源流程、本地调试方法 |
| 部署方案 | `/docs/deployment/` | 支持 Docker、Nginx 静态托管、Vercel 等多种部署方式 |

## 资源列表

本导航系统当前收录的域名索引如下，所有域名均来自公开互联网信息整理，项目本身不对任何站点的内容合法性、持续可用性及服务质量作出担保。请用户自行遵守相关法律法规并尊重版权方权益。

中文字幕在线播放资源类别

<code>zhongwenzimuyirenzaixian.org.cn</code>

<code>zhongwenzimuzaixiankanpian.org.cn</code>

<code>gaoqingpianyuanzaixianbofang.org.cn</code>

<code>zuixinzhongwenzimuzaixian.com.cn</code>

<code>zhongwenzaixianguankanshipin.com.cn</code>

<code>zhongwenzimuzhuanqu.com.cn</code>

<code>zhongwenzimuzaixianshipinguankan.com.cn</code>

## 项目结构

```
zimulink-navigator/
├── public/                         # 静态资源目录，存放 favicon 和 robots.txt
│   ├── favicon.ico                 # 网站图标文件
│   └── robots.txt                  # 搜索引擎爬虫规则
├── src/                            # 前端源代码主目录
│   ├── api/                        # API 请求封装层
│   │   ├── client.js               # 基于 fetch 的通用请求客户端，含重试与超时逻辑
│   │   └── endpoints.js            # 集中管理所有后端接口路径常量
│   ├── components/                 # Vue 组件库（按功能模块分类）
│   │   ├── dashboard/              # 仪表板页面相关组件，含状态概览和快速统计卡片
│   │   ├── monitor/                # 域名监控面板组件，含列表渲染和状态指示灯
│   │   ├── filters/                # 筛选器组件，含下拉菜单、复选框组和搜索输入框
│   │   ├── charts/                 # 图表组件，基于 ECharts 封装趋势折线图
│   │   └── common/                 # 通用复用组件，含按钮、提示框和模态框
│   ├── composables/                # Vue Composition API 可组合函数
│   │   ├── useDomainMonitor.js     # 封装域名状态轮询和更新逻辑
│   │   └── useLocalStorage.js      # 封装浏览器本地存储读写操作
│   ├── store/                      # Pinia 状态管理模块
│   │   ├── domains.js              # 域名列表数据存储，含增删改查操作
│   │   └── settings.js             # 用户配置存储，含主题和阈值设置
│   ├── styles/                     # 全局样式文件
│   │   ├── variables.css           # CSS 自定义属性，定义颜色与间距变量
│   │   └── dark-theme.css          # 暗色主题覆盖样式
│   ├── utils/                      # 工具函数目录
│   │   ├── validator.js            # URL 格式校验与域名标准化处理
│   │   └── formatter.js            # 时间格式化、字节单位转换等辅助函数
│   ├── App.vue                     # 根组件，负责布局和路由视图渲染
│   └── main.js                     # 应用入口文件，初始化 Vue 实例和插件
├── tests/                          # 单元测试与集成测试目录
│   ├── unit/                       # 基于 Vitest 的单元测试用例
│   └── e2e/                        # 基于 Playwright 的端到端测试脚本
├── docs/                           # 项目文档，包含用户手册和 API 参考
├── scripts/                        # 运维与构建辅助脚本
│   ├── health-check.js             # 本地拨测脚本，可用于 cron 定时任务
│   └── generate-sitemap.js         # 生成站点地图的脚本
├── index.html                      # HTML 入口模板文件
├── package.json                    # npm 项目配置文件，含依赖列表与脚本命令
├── vite.config.js                  # Vite 构建工具配置文件
├── eslint.config.js                # ESLint 代码检查配置文件
└── README.md                       # 项目说明文档（本文件）
```

## 贡献指南

欢迎社区开发者为本项目提交改进建议或代码贡献。请遵循以下流程以确保协作顺畅：

1. 在 GitHub 仓库的 Issues 区域搜索现有话题，确认无人正在处理同类问题后，新建一个 Issue 描述你的改进提案或缺陷报告，并标注合适的标签（enhancement、bug、documentation）。

2. 将项目复刻（Fork）至个人账号下，在本地切换到 `develop` 分支基础上新建功能分支，分支命名采用 `feature/简述` 或 `fix/简述` 格式，例如 `feature/add-timeout-slider`。

3. 完成代码编写后，请确保所有单元测试通过（执行 `npm run test`），并补充对应的测试用例覆盖新增逻辑。提交信息（Commit Message）需遵循约定式提交规范（Conventional Commits），例如 `feat: 增加自定义超时阈值滑块` 或 `fix: 修复暗色模式下状态颜色显示异常`。

4. 将本地分支推送至远程复刻仓库，然后向主仓库的 `develop` 分支发起 Pull Request。PR 描述中需关联对应的 Issue 编号，并简要说明修改内容与影响范围。项目维护者将在三个工作日内进行审查与合并。

## 常见问题

**问：ZimuLink 本身是否存储或缓存任何影视文件或字幕文件？**

答：ZimuLink 仅存储和展示域名 URL 字符串及其对应的可用性检测数据（状态码、响应时间、时间戳），不缓存、不代理、不转发任何媒体流或字幕文件内容。所有收录域名均以超链接形式呈现，用户点击后将在浏览器新标签页中直接访问原始站点，数据流不经过 ZimuLink 服务器。

**问：如何添加或删除监控列表中的域名？**

答：普通用户可以在界面的域名管理面板中点击「新增域名」按钮，输入完整的 URL 并选择分类标签后提交，该条目会保存在浏览器本地存储中仅对当前设备生效。若希望永久收录至公共列表，请通过 GitHub Issues 提交新增建议，项目维护者审核后将合并至主数据源。删除操作同理，本地删除不影响公共数据源。

**问：拨测结果是否会对目标站点造成较大的请求压力？**

答：每个拨测请求仅为一次标准的 HTTP HEAD 或 GET 请求（仅获取响应头，不下载正文），单次请求数据量不超过 2KB。全局监控间隔为 30 分钟，每个域名每轮仅探测一次，平均到每分钟的请求量极低，不会对目标站点的正常服务产生影响。

## 许可证

本项目采用 MIT 许可证进行开源。详细信息请参阅项目根目录下的 LICENSE 文件。

> 外链数量: 7 | 生成时间: 2026-08-21 22:29:49
