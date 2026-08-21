# ZimuIndex 开源技术资源与影视元数据导航平台

ZimuIndex 是一个面向开发者和技术爱好者的轻量级影视元数据与字幕资源导航聚合系统。项目定位为技术演示与数据源验证工具，旨在为自建媒体服务器（如 Jellyfin、Emby、Plex）的维护者、自动化刮削脚本开发者以及字幕资源研究者提供一套稳定、可扩展的外链管理方案。项目本身不存储任何媒体文件或字幕数据，仅以结构化方式整理公开可用信息资源，并对外提供标准化的接入示例。

目标用户包括：媒体服务器运维人员、开源刮削工具贡献者、字幕格式转换脚本开发者以及需要批量测试网络资源可用性的自动化测试工程师。项目通过集中管理高频访问资源，显著降低开发者维护分散书签的人力成本，同时提供简洁的 RESTful 风格状态检测接口，方便集成至各类监控系统。

## 功能概览

- **资源导航仪表板**：提供分类清晰的影视字幕与片源外链聚合页面，支持按资源类型、数据来源、更新频率进行快速筛选与排序。

- **可用性健康检查**：内置定时任务对已收录的每一个外链资源执行 HTTP HEAD 请求，记录响应状态码与延迟时间，并在仪表板高亮显示异常节点。

- **元数据映射模板**：预置 JSON Schema 定义标准影视元数据结构，涵盖片名、季数、集数、字幕语言、格式信息等字段，便于二次开发与数据交换。

- **外链变更日志**：自动记录每次导航链接的新增、删除或 URL 变更操作，支持版本回滚与变更审计，方便团队协作维护。

- **批量导入导出**：支持通过 CSV 或 YAML 文件批量导入外链列表，也可将当前完整导航数据导出为结构化文件，便于离线备份或迁移。

- **容器化部署支持**：提供 Dockerfile 与 docker-compose 示例，配合环境变量可快速在本地或云服务器拉起完整服务，无需额外配置数据库。

- **开放 API 端点**：提供 `/api/v1/links`、`/api/v1/status` 等只读接口，返回 JSON 格式的链接列表及其实时可用状态，方便第三方脚本调用。

## 应用场景

- **自建媒体服务器补充字幕源**：当 Jellyfin 或 Emby 内置字幕插件无法找到匹配字幕时，运维人员可通过 ZimuIndex 快速定位到高可用性字幕外链，手动下载并上传至媒体库对应目录。

- **自动化刮削脚本的备用数据源**：开源刮削工具（如 TinyMediaManager 或自研 Python 脚本）可将 ZimuIndex 的 API 作为备选数据源，当主数据源（如 TMDB）出现限流或不可用时，自动切换至本平台提供的资源映射进行元数据补全。

- **网络质量与资源可用性监控**：测试工程师可配置定时任务调用 ZimuIndex 的健康检查接口，将结果推送至 Prometheus 或 Grafana，实现对多个影视资源站点的存活与响应趋势监控，及时发现服务降级。

- **新人开发者学习项目**：前端或全栈开发者可将 ZimuIndex 作为练习项目，通过阅读本仓库的结构化导航代码理解资源聚合类应用的设计模式，并参与外链维护贡献以熟悉开源协作流程。

## 快速开始

以下命令适用于 Linux / macOS 及 Windows WSL 环境。请确保已安装 Git 和 Node.js 18+。

```bash
# 克隆仓库到本地
git clone https://github.com/zimu-index/zimuindex.git
cd zimuindex

# 安装项目依赖（使用 npm）
npm install

# 以开发模式启动服务（默认监听 3000 端口）
npm run dev
```

启动成功后，在浏览器中访问 `http://localhost:3000` 即可看到导航仪表板。如需构建生产版本并启动，请执行：

```bash
npm run build
npm start
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | >= 18.0.0 | 运行时环境，需支持 ES2020 特性 |
| npm | >= 9.0.0 | 包管理工具，用于安装及脚本执行 |
| Git | >= 2.30.0 | 版本控制，用于克隆仓库及提交贡献 |
| 操作系统 | Linux / macOS / Windows (WSL2) | 推荐使用 Debian 11 或 Ubuntu 22.04 进行生产部署 |
| 网络访问 | 出站 80/443 端口开放 | 健康检查需向外链站点发送 HTTP 请求，需确保可访问公网 |
| 内存 | >= 512 MB | 运行开发服务器及构建过程的最低内存要求 |
| 磁盘空间 | >= 200 MB | 包含 node_modules 及构建产物在内的完整占用 |
| 浏览器 | Chrome 90+ / Firefox 88+ | 仪表板 UI 所需现代浏览器特性 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|-----|------|-----------|
| 用户指南 | `/docs/user-guide/` | 如何使用仪表板、如何筛选链接、如何查看健康状态 |
| 开发者文档 | `/docs/developer/` | API 接口规范、数据模型定义、如何新增外链类别 |
| 部署手册 | `/docs/deployment/` | 如何配置反向代理、使用 Docker 部署、设置 HTTPS 证书 |
| 维护指南 | `/docs/maintenance/` | 如何清理失效链接、如何更新依赖、如何执行版本发布 |

## 资源列表

以下为 ZimuIndex 当前版本收录的全部外链资源。所有链接均按照原始格式原样列出，未做任何改写。列表按资源功能分类组织，便于快速查阅。

### 中文字幕在线观看类

- <code>zhongwenzimuzaixianyingyuan.com.cn</code>
- <code>zhongwenzimumianfeizaixianbofang.com.cn</code>
- <code>gaoqingshipinzhongwenzimu.com.cn</code>
- <code>zhongwenzimuyirenzaixian.com.cn</code>
- <code>zhongwenzimuzaixiankanpian.com.cn</code>

### 高清片源在线播放类

- <code>gaoqingpianyuanzaixianbofang.com.cn</code>

### 其他影视相关资源

- <code>fujinderenyueai.com.cn</code>

## 项目结构

```
zimuindex/
├── src/                                 # 核心源代码目录
│   ├── api/                             # RESTful API 路由及控制器
│   │   ├── v1/                          # API 版本 v1 实现
│   │   │   ├── links.js                 # 链接列表与筛选接口
│   │   │   └── status.js                # 健康检查状态接口
│   │   └── index.js                     # 路由注册入口
│   ├── services/                        # 业务逻辑层
│   │   ├── healthChecker.js             # 定时执行外链 HEAD 请求
│   │   ├── linkManager.js               # 链接增删改与变更日志
│   │   └── schemaValidator.js           # 元数据 JSON Schema 校验
│   ├── data/                            # 数据存储与种子文件
│   │   ├── seedLinks.yaml               # 初始外链列表（YAML 格式）
│   │   ├── changelog.json               # 变更日志持久化文件
│   │   └── backup/                      # 每日自动备份目录
│   ├── frontend/                        # 前端仪表板源码
│   │   ├── components/                  # Vue/React 组件（按项目选型）
│   │   ├── pages/                       # 页面级视图
│   │   └── assets/                      # CSS、图片等静态资源
│   ├── config/                          # 配置文件目录
│   │   ├── default.json                 # 默认端口、超时、重试次数
│   │   └── custom.example.json          # 用户自定义配置示例
│   └── utils/                           # 通用工具函数
│       ├── logger.js                    # 日志格式化与输出
│       └── request.js                   # 封装 axios 超时与重试逻辑
├── tests/                               # 单元测试与集成测试
│   ├── unit/                            # 服务层单元测试
│   └── integration/                     # API 端点集成测试
├── docs/                                # 完整文档（用户/开发/部署/维护）
│   ├── user-guide/                      # 用户操作手册
│   ├── developer/                       # API 与数据模型文档
│   ├── deployment/                      # 生产环境部署指南
│   └── maintenance/                     # 日常维护与故障排查
├── scripts/                             # 辅助运维脚本
│   ├── backup.sh                        # 手动备份数据脚本
│   └── health-report.sh                 # 输出健康检查报告文本
├── Dockerfile                           # 多阶段构建 Docker 镜像文件
├── docker-compose.yml                   # 本地编排服务示例
├── package.json                         # npm 依赖与脚本定义
├── .eslintrc.js                         # 代码风格检查配置
├── .gitignore                           # Git 忽略文件清单
└── README.md                            # 项目入口文档（本文件）
```

## 贡献指南

我们欢迎开发者以多种方式参与本项目。请遵循以下步骤提交贡献：

1. **查阅现有议题**：访问 GitHub Issues 页面，查找带有 `help wanted` 或 `good first issue` 标签的未分配任务。如计划新增功能，请先新建议题描述设计思路，避免重复劳动。

2. **分叉并克隆仓库**：将本项目 fork 至个人账户，随后克隆到本地开发环境。建议在独立分支上开发，分支命名遵循 `feature/功能简述` 或 `fix/问题简述` 格式。

3. **本地自测**：在提交前，请运行 `npm run test` 确保所有单元测试和集成测试通过。新增功能需附带对应的测试用例。同时执行 `npm run lint` 修复代码风格问题。

4. **提交变更并推送**：编写清晰的提交信息，采用 `<类型>: <简短描述>` 格式（例如 `feat: 添加按语言筛选字幕链接`）。提交后推送到个人分叉仓库。

5. **发起拉取请求**：在 GitHub 上向本仓库的 `main` 分支发起 Pull Request。PR 描述中需关联相关议题编号，并列出变更摘要与测试结果。等待项目维护者审核，期间可能需要进行一轮或多轮修改。

## 常见问题

**问：项目是否提供在线演示站点？如何快速体验完整功能？**

答：目前项目未部署公共演示站点，原因在于收录的外链资源可能因第三方站点策略变更而频繁失效，维护公开演示环境存在较高人力成本。但您可以通过执行 `npm run dev` 在本地启动完整的仪表板和 API 服务，所有功能均可在本地环境中正常运行。同时，`/data/seedLinks.yaml` 中已预置了完整的示例数据，启动后即可看到分类导航与健康检查结果。

**问：健康检查将外链标记为失效后，系统是否会主动重试？多久更新一次状态？**

答：健康检查模块采用指数退避重试策略，首次失败后间隔 5 秒重试，第二次失败间隔 10 秒，第三次失败间隔 30 秒，三次均失败则标记为不可用。定时任务默认每 30 分钟执行一次全量检查。如果某个链接连续三次检查（即 90 分钟内）均不可用，系统会将其状态更新为“长期离线”，并在仪表板中将其移动至列表底部。

**问：如果项目收录的某个外链网站涉及版权争议，我该如何处理？**

答：ZimuIndex 本身不存储、不代理、不缓存任何媒体内容，仅以中立方式提供公开可访问的 URL 导航。如果您认为某个链接指向的内容侵犯了您的合法权益，请通过 GitHub Issues 提交移除请求。我们在收到包含详细侵权说明的正式通知后，会在 2 个工作日内审核并移除相关链接。同时，项目维护者保留定期审查链接列表的权利，对于长期不可用或明显失效的链接也会予以清理。

## 许可证

MIT License

Copyright (c) 2026 ZimuIndex Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-21 22:29:12
