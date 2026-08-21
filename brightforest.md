# Resource Navigator

Resource Navigator 是一个面向开发人员和技术研究者的高质量外链资源聚合与导航系统。项目定位为技术信息的中转枢纽，通过对网络资源进行结构化整理、分类标注与可用性监测，帮助用户从碎片化的信息环境中快速定位具备实际参考价值的在线文档、工具站点与数据源。

该项目不生产原始内容，专注于资源链接的筛选、组织与状态追踪，适用于需要频繁查阅外部技术资料、维护项目依赖文档或构建个人知识库索引的工程场景。Resource Navigator 通过周期性检测与人工校对相结合的方式，降低资源失效带来的信息损耗，提升研发流程中信息获取环节的稳定性与效率。

## 功能概览

- **多层级资源分类体系**：按内容类型、语种、应用领域建立三级标签结构，支持快速筛选与定向检索。

- **链接存活状态监测**：内置轻量级 HTTP 状态检查模块，定期对收录资源进行可达性验证，并在界面中标记异常条目。

- **自定义收藏夹与标签系统**：允许用户为常用资源添加自定义标签和备注，构建个人化的资源子集。

- **全文元数据检索**：基于资源标题、描述、关键词与分类标签进行全文检索，检索响应时间控制在 300 毫秒以内。

- **批量导入与导出**：支持通过 JSON 和 CSV 格式批量导入外部链接列表，导出功能可用于生成项目依赖文档或团队共享清单。

- **访问统计与热度排序**：记录各资源的点击频次与最近访问时间，支持按热度、更新时间或字母序多种排序策略。

- **响应式 Web 管理界面**：提供适配桌面与移动设备的操作面板，所有核心功能均通过浏览器完成，无需安装额外客户端。

## 应用场景

- **技术文档聚合查阅**：开发人员在研究新框架或协议时，可通过 Resource Navigator 快速访问经过筛选的中文技术文档站点，避免在海量搜索结果中反复试错。

- **项目依赖资源归档**：技术负责人可将项目所引用的外部规范、SDK 下载页、API 参考手册等统一收录至导航系统，形成可追溯的外部依赖清单，便于团队交接与审计。

- **离线资源备份规划**：运维人员利用链接监测功能识别高风险失效资源，提前安排本地镜像或离线存档，保障生产环境文档的持续可用性。

- **学术研究文献线索整理**：研究人员借助分类标签与元数据检索，对领域内的开源数据集、预印本平台、工具库进行系统化梳理，提高文献调研效率。

## 快速开始

以下操作步骤适用于 Linux 和 macOS 环境，Windows 用户建议使用 WSL2 或 Git Bash。

```bash
# 克隆项目仓库
git clone https://github.com/resource-navigator/core.git
cd core

# 安装依赖（使用 npm）
npm install

# 初始化本地资源索引数据库
npm run init-db

# 以开发模式启动 Web 服务
npm run dev
```

启动成功后，访问控制台输出中显示的本地地址（默认 http://127.0.0.1:5173）即可进入导航面板。首次启动将自动执行示例资源数据的载入，用于验证系统功能完整性。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x 或 20.x LTS | 运行时环境，推荐使用 nvm 管理版本 |
| npm | 9.x 或 10.x | 包管理器，随 Node.js 一同安装 |
| SQLite | 3.39 及以上 | 嵌入式数据库，用于存储资源元数据与状态记录 |
| Git | 2.30 及以上 | 用于克隆仓库和版本管理 |
| 现代浏览器 | Chromium 110+ / Firefox 115+ | 用于访问 Web 管理界面，支持 ES2022 语法 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | /docs/user-guide/ | 如何添加资源、创建分类、执行检索与导出数据 |
| 管理员指南 | /docs/admin-guide/ | 如何配置检测周期、调整缓存策略、管理用户权限 |
| 开发文档 | /docs/developer-guide/ | 插件扩展机制、API 接口规范、数据库表结构说明 |
| 部署参考 | /docs/deployment/ | 生产环境容器化部署、反向代理配置与性能调优参数 |
| 设计说明 | /docs/design/ | 系统架构图、数据流模型、状态机设计及扩展性考量 |

## 资源列表

以下为 Resource Navigator 当前收录的外部信息资源，按内容主题分组陈列。所有链接均保留用户提供的原始格式，未做任何协议补全或域名规范化处理。

影视字幕与高清资源

<code>gaoqingshipinzhongwenzimu.com.cn</code>

<code>zhongwenzimuyirenzaixian.com.cn</code>

<code>zhongwenzimuzaixiankanpian.com.cn</code>

<code>gaoqingpianyuanzaixianbofang.com.cn</code>

成人内容与社交娱乐相关

<code>fujinderenyueai.com.cn</code>

<code>shenyeshangmen.com.cn</code>

<code>jiaoyouyiyeqing.com.cn</code>

## 项目结构

```
core/
├── src/                           # 源代码主目录
│   ├── api/                       # HTTP 接口层，处理路由与请求校验
│   ├── core/                      # 核心业务逻辑，包括资源索引与状态管理
│   ├── models/                    # 数据模型定义，对应 SQLite 表结构
│   ├── services/                  # 外部服务集成，含监测调度与邮件通知
│   └── utils/                     # 通用工具函数，含日志、加密与格式转换
├── web/                           # 前端资源目录
│   ├── components/                # Vue 3 可复用 UI 组件
│   ├── layouts/                   # 页面布局模板
│   └── static/                    # 静态资源，含 CSS 与 SVG 图标
├── docs/                          # 项目文档，按使用角色分子目录
├── tests/                         # 单元测试与集成测试脚本
│   ├── unit/                      # 针对核心模块的 Jest 测试用例
│   └── e2e/                       # 端到端测试剧本，基于 Playwright
├── scripts/                       # 构建与运维辅助脚本
├── config/                        # 环境配置文件，含默认参数与示例
├── data/                          # 本地 SQLite 数据库文件与初始种子数据
├── Dockerfile                     # 容器镜像构建文件
├── docker-compose.yml             # 本地开发与测试环境编排
├── package.json                   # npm 依赖清单与脚本入口
├── README.md                      # 项目总体说明（当前文档）
└── LICENSE                        # MIT 许可证全文
```

## 贡献指南

Resource Navigator 欢迎社区提交资源推荐、链接更新建议以及代码改进。请遵循以下流程进行贡献。

1. 查阅问题追踪器中的待办事项或标签为“help wanted”的议题，确认无重复工作后，在对应议题下留言声明认领。

2. 从主仓库派生个人副本，在派生仓库中创建以 `feature/` 或 `fix/` 为前缀的功能分支，并遵循项目已定义的代码风格与提交信息格式。

3. 完成变更后，确保新增或修改的代码通过全部单元测试，并在本地环境中验证核心功能未出现回归性错误。

4. 向主仓库的 `main` 分支发起合并请求，在请求描述中清晰说明变更目的、影响范围及测试覆盖情况。

5. 项目维护者将在三个工作日内进行代码审查，如有修改意见将在合并请求中逐行标注，贡献者需及时回应并补充调整。

## 常见问题

**问：系统提示“数据库连接失败”应如何处理？**

答：首先检查 `data/` 目录是否具有写入权限，SQLite 文件是否被其他进程占用。若为首次启动，请确认已执行 `npm run init-db` 完成数据库初始化。对于生产环境，建议检查 `config/production.json` 中的数据库路径配置是否正确指向持久化存储卷。

**问：链接检测模块产生大量误报，如何调整敏感度？**

答：检测模块默认使用 TCP 超时与 HTTP 状态码双重判定。可在管理后台的“监测设置”中调整超时阈值（单位毫秒）和重试次数。对于已知存在访问限制的目标站点，可将其加入白名单并手动设定检测策略为“仅人工确认”，避免自动化检查干扰。

**问：如何从旧版本迁移数据至新版本？**

答：项目提供版本迁移脚本，位于 `scripts/migrate.js`。执行前请备份原始数据库文件。迁移命令格式为 `npm run migrate -- --from v1 --to v2`，具体版本号请查阅对应版本的发布说明。若迁移失败，脚本会自动回滚并输出错误日志至 `logs/` 目录。

## 许可证

MIT License

Copyright (c) 2026 Resource Navigator Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-21 22:29:12
