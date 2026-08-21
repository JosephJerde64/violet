# ZHONGZI Resource Hub

ZHONGZI Resource Hub 是一个面向中文互联网内容创作者、数据研究员与信息聚合开发者的高性能外链资源聚合与导航系统。该项目定位于解决中文网络环境下高质量视频索引数据分散、URL 失效频繁、检索口径不一致等问题，通过结构化的资源分类与稳定的基础架构，为用户提供可维护、可扩展的参考信息源集合。项目本身不存储或分发任何受版权保护的内容，仅作为公开可访问 URL 的整理与分类工具，适用于个人学习、自动化数据采集测试及信息架构研究等合法用途。

## 功能概览

- **多级分类索引体系**：按内容主题、域名性质、更新活跃度对资源链接进行标签化分类，支持快速筛选与批量导出。
- **资源可用性健康检查**：内置周期性 HTTP 状态探测模块，对收录 URL 进行可访问性验证，并记录响应时间与状态码变化趋势。
- **自定义列表生成器**：用户可根据关键词、域名后缀或预设分类模板，动态生成专属外链清单，支持 JSON / CSV / Markdown 三种导出格式。
- **版本化快照记录**：每次资源列表更新时自动创建变更日志，记录新增、移除或状态变更的 URL，便于回溯与审计。
- **开放数据 API 端点**：提供 RESTful 风格的查询接口，支持按分类、关键字模糊匹配及随机采样方式获取资源条目，方便第三方工具集成。
- **本地化离线镜像支持**：允许用户将完整资源索引导出为单一 HTML 文件或 SQLite 数据库，适用于无网络环境下的查阅与开发测试。
- **响应式导航面板**：面向桌面与移动设备优化的浏览界面，在保持技术信息密度同时确保基础可用性。

## 应用场景

1. **内容聚合平台的数据采集预热**：在启动新的视频索引或推荐系统项目前，开发者可使用本项目的资源分类清单作为初始种子链接集，快速构建爬虫队列的测试环境，验证解析规则与反爬策略的有效性。

2. **网络信息可用性监测基线建设**：运维团队可将本项目导出的 URL 列表作为监测探针的目标池，定期检测各域名的响应状况，从而评估特定类别资源服务的稳定性趋势，并为告警阈值提供参考数据。

3. **学术研究与数据分析教学**：信息科学相关课程的教师可借助本项目清晰的资源分类结构，向学生展示中文互联网内容分布的基本特征，并基于真实 URL 数据进行网络拓扑、域名关联或内容演化等课题的课堂实验。

4. **个人知识管理工具的外链补充**：使用 Obsidian、Notion 或 Logseq 等工具构建个人知识库的用户，可将本项目提供的分类列表作为外部参考节点，丰富其信息网络中的原始素材索引层。

5. **开源项目文档中的参考资源附录**：其他开源项目维护者可在其 README 或文档中引用本项目的分类成果，作为推荐的外部数据源列表，减少自身维护同类链接集合的工作量。

## 快速开始

以下指令适用于 Linux / macOS 及 Windows WSL 环境，Python 3.9 及以上版本要求。

```bash
# 克隆项目仓库
git clone https://github.com/zhongzi-resource-hub/core.git
cd core

# 创建并激活虚拟环境（推荐）
python3 -m venv venv
source venv/bin/activate      # Linux/macOS
# venv\Scripts\activate       # Windows

# 安装核心依赖
pip install -r requirements.txt

# 执行初始化资源索引构建
python scripts/build_index.py --input data/raw_urls.txt --output dist/index.json

# 启动本地开发服务器（默认端口 8080）
python app.py --port 8080
```

访问 `http://127.0.0.1:8080` 即可浏览本地资源导航界面。如需生成静态镜像文件，请使用 `python scripts/export_static.py`。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 - 3.12 | 核心运行环境，类型注解与异步特性依赖 |
| requests | 2.31.0+ | 用于 HTTP 健康检查与 API 代理请求 |
| beautifulsoup4 | 4.12.0+ | 可选安装，用于解析部分返回 HTML 的域名信息 |
| flask | 2.3.0+ | 提供 Web 导航界面与 REST API 服务 |
| pytest | 7.4.0+ | 仅开发测试需要，生产环境可不安装 |
| black | 23.0.0+ | 代码格式化工具，贡献代码时需保持一致风格 |

所有依赖均可在 PyPI 获取，建议使用虚拟环境隔离。生产部署时可移除 `dev-requirements.txt` 中的测试与格式化相关包。

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | `/docs/user-guide/` | 如何浏览分类、创建自定义列表、导出数据以及配置健康检查参数？ |
| API 参考 | `/docs/api/` | REST 接口的端点定义、请求参数格式、返回结构及错误码含义？ |
| 运维指南 | `/docs/ops/` | 如何部署生产环境服务、配置反向代理、调整探测频率及处理日志？ |
| 贡献者文档 | `/docs/contributing/` | 代码风格规范、提交信息格式、PR 流程以及新增分类的审核标准？ |

## 资源列表

本部分按照类别整理项目收录的全部原始资源链接。所有 URL 严格遵循用户提供的原始格式输出，未做任何协议补全、域名改写或路径调整。

**按域名特征归类（基于原始字符串）**

- 核心视频索引类

  <code>zhongwenzimuzaixianshipinguankan.com.cn</code>
  <code>zhongwenzimugaoqingzaixianguankan.com.cn</code>
  <code>zhongwenzimuzaixianbofangshipin.com.cn</code>
  <code>zaixianzhongwenzimushipin.com.cn</code>

- 热门免费资源类

  <code>renqizaixianmianfeishipin.com.cn</code>
  <code>zhongwenzaixianmianfeishipin.com.cn</code>
  <code>mianfeishipinzhongwenzimu.com.cn</code>

所有链接均以纯域名形式收录，不包含路径参数或协议前缀。项目默认对所有域名执行 `http://` 与 `https://` 双协议探测，并记录最优可达结果。

## 项目结构

```
.
├── app.py                      # Flask 应用入口，注册路由与初始化扩展
├── requirements.txt            # 生产环境核心依赖列表
├── dev-requirements.txt        # 开发测试专用依赖
├── config/
│   ├── settings.py             # 应用配置类（环境变量、默认参数）
│   └── categories.yaml         # 分类标签体系定义，包含层级关系
├── data/
│   ├── raw_urls.txt            # 原始收录 URL 清单（每行一条）
│   └── health_cache.db         # SQLite 存储的探测结果缓存
├── scripts/
│   ├── build_index.py          # 从 raw_urls 构建索引 JSON
│   ├── checker.py              # 异步 HTTP 状态探测调度器
│   └── export_static.py        # 生成离线静态 HTML 镜像
├── src/
│   ├── api/                    # REST 端点实现（分类查询、随机采样）
│   ├── models/                 # 数据类定义（Resource, Category, ProbeResult）
│   └── utils/                  # 通用辅助函数（日志、格式化、验证）
├── tests/
│   ├── test_api.py             # API 接口单元测试与集成测试
│   └── test_checker.py         # 健康检查模块模拟测试
├── docs/                       # 完整文档源码（Markdown + MkDocs）
└── static/                     # 前端静态资源（CSS, JavaScript 导航逻辑）
```

## 贡献指南

1. **问题报告与功能请求**：请使用 GitHub Issues 模板提交，明确说明当前行为、期望行为以及复现步骤。对于新增分类建议，需附带至少 5 个同类 URL 示例。

2. **代码贡献流程**：Fork 主仓库，基于 `develop` 分支创建以 `feature/` 或 `fix/` 为前缀的新分支。代码提交前请运行 `black .` 格式化，并通过 `pytest tests/` 全量测试。

3. **资源列表更新规范**：如需增删或修改 `data/raw_urls.txt` 中的条目，请同步更新 `data/health_cache.db` 对应的初始状态记录，并在 PR 描述中说明变更理由与验证方式。

4. **文档补充要求**：任何新增功能或配置项必须在 `/docs/` 下对应的用户手册或运维指南中添加章节，确保文档与代码同步。文档使用 Markdown 撰写，遵循中文技术文档风格指南。

5. **审查与合并**：所有 PR 需至少一名项目维护者审核，并通过持续集成检查（包括 Python 版本兼容性与链接格式校验）。合并后自动触发索引重建与静态站点部署。

## 常见问题

**Q：收录的 URL 出现无法访问或域名过期，项目会如何处理？**

A：项目内置的周期健康检查进程会每日自动探测所有收录域名。连续三次探测失败（间隔 24 小时）的条目将被标记为“不稳定”，并在导航界面以灰色标识。连续七天不可达的条目将自动移至归档列表，不再出现在默认分类视图中。用户可通过 API 的 `include_archived=true` 参数查询历史记录。

**Q：我可以将本项目的资源列表用于商业产品或自动化脚本中吗？**

A：可以。本项目采用 MIT 许可证，资源列表本身仅包含公开注册的域名字符串，不涉及任何受保护数据。您可以将列表集成至商业系统，但请注意独立验证各域名当前的使用条款，本项目不对任何外部域名的内容合法性或可访问性承担连带责任。

**Q：如何确保我通过 API 获取的分类信息与最新索引保持同步？**

A：所有 API 响应均实时查询内存缓存中的索引结构，该缓存会在每次 `build_index.py` 执行后自动更新。您可以通过响应头中的 `X-Index-Version` 字段校验当前版本，该字段值对应索引文件的 MD5 哈希。项目也支持通过 Webhook 方式在索引更新时主动通知注册的接收端点。

## 许可证

MIT License

Copyright (c) 2026 ZHONGZI Resource Hub Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-21 22:29:54
