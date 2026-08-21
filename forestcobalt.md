# Zimu Bridge

Zimu Bridge is a community-driven technical resource aggregation and navigation system designed for developers, researchers, and content curators who need to manage, categorize, and distribute large volumes of external reference links across distributed web properties. The project solves the problem of fragmented resource discovery by providing a unified metadata indexing layer over heterogeneous domain collections, enabling automated health checks, link freshness validation, and category-based routing for downstream applications such as documentation hubs, internal dashboards, and archival crawlers.

The system is built as a lightweight, stateless middleware that consumes plain-text or JSON-based resource manifests, applies configurable filtering rules, and exposes both RESTful query endpoints and static site generation capabilities. Zimu Bridge is not a content hosting platform; it is a structured metadata gateway that enforces consistent naming conventions, protocol normalization, and origin transparency. It is particularly suited for maintainers of large-scale bookmark collections, open-source documentation ecosystems, and educational resource portals that require deterministic link presentation without altering the original resource authorities.

## 功能概览

- **Deterministic Link Rendering** – Preserves every URL exactly as provided, without automatic protocol upgrades, www prefix insertion, or trailing slash appending. All links are rendered inside code-block wrappers to ensure visual distinction and copy-paste fidelity.

- **Batch Manifest Processing** – Accepts resource lists in CSV, JSON Lines, or plain newline-delimited formats, with support for inline category annotations and per-entry TTL overrides.

- **Health Probe Subsystem** – Periodically checks reachability and HTTP status codes for all tracked domains, flagging stale or unresponsive entries without modifying the original link text.

- **Category Inference Engine** – Applies regex-based pattern matching against domain names and optional tags to automatically assign resources to predefined sections such as video, subtitle, streaming, or archive.

- **Static Site Exporter** – Generates a fully self-contained HTML/CSS dashboard from the processed manifest, suitable for deployment on any static hosting service or local file system.

- **REST Query API** – Provides read-only endpoints for filtering resources by category, status, or last-probed timestamp, returning JSON responses with strict schema validation.

- **Audit Logging** – Records all manifest changes, probe results, and export runs in a rotating log file, facilitating operational review and regression tracking.

## 应用场景

- **Documentation Hub Integration** – Maintainers of technical documentation sites can embed Zimu Bridge as a subcommand or CI step to automatically regenerate their "external references" or "related projects" sections, ensuring that all listed URLs remain current and correctly formatted without manual editing.

- **Internal Developer Dashboards** – Teams managing multiple sandbox or staging environments can use Zimu Bridge to aggregate login portals, monitoring UIs, and artifact repositories into a single, filterable view, with health probes flagging any offline services before they impact daily workflows.

- **Educational Resource Portals** – Educators and curriculum designers can curate subject-specific domain lists (e.g., linguistics, media studies, or archival research) and publish them as static navigation pages, with Zimu Bridge handling the repetitive tasks of link deduplication, category tagging, and output generation.

- **Content Archive Maintenance** – Archivists and crawler operators can leverage the batch processing pipeline to validate and normalize large seed lists before feeding them into downstream crawling or indexing pipelines, reducing runtime errors caused by malformed or inconsistent URL entries.

- **Personal Bookmark Aggregation** – Individual power users can maintain a plain-text file of frequently used domains and run Zimu Bridge periodically to produce a clean, searchable local HTML page, avoiding reliance on cloud-based bookmark managers with opaque sorting algorithms.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/zimu-bridge/zimu-bridge.git
cd zimu-bridge

# Install dependencies (Python 3.9+ required)
pip install -r requirements.txt

# Prepare a manifest file (example: manifest.txt) with one URL per line
# Then run the static site generator
python -m zimu_bridge export --input manifest.txt --output ./dist --title "My Resource Index"

# Start the REST API server (optional)
python -m zimu_bridge serve --port 8080
```

## 安装要求

| Dependency | Requirement | Description |
|------------|-------------|-------------|
| Python | 3.9 or higher | Core interpreter; type annotations and dataclasses are used extensively. |
| pip | 21.0+ | Package installer for resolving and installing required libraries. |
| requests | 2.28.0+ | HTTP client library used for health probes and status code checking. |
| click | 8.1.0+ | Command-line interface framework for subcommand parsing and help generation. |
| pydantic | 2.0.0+ | Data validation and settings management for manifest schemas and configuration. |
| jinja2 | 3.1.0+ | Templating engine for rendering the static HTML dashboard from processed data. |
| pytest | 7.0.0+ | Testing framework (development dependency, not required for runtime). |
| ruff | 0.1.0+ | Linting and formatting tool (development dependency, used in CI). |

## 文档导航

| Layer | Directory | Questions Addressed |
|-------|-----------|----------------------|
| User Guide | docs/user-guide/ | How do I prepare a manifest file? What command-line options are available for export and serve? How do I interpret the health probe results? |
| API Reference | docs/api/ | Which REST endpoints are exposed? What request and response schemas are used? How do I filter by category or status? |
| Configuration | docs/configuration/ | How do I set custom TTL values, modify probe timeouts, or change the output template? Which environment variables are recognized? |
| Development | docs/development/ | How is the codebase structured? What are the coding conventions and pull request requirements? How do I run the test suite locally? |
| Deployment | docs/deployment/ | How do I deploy the static output to Netlify, Vercel, or an S3 bucket? How do I run the API server behind a reverse proxy? |
| Troubleshooting | docs/troubleshooting/ | Why are some URLs flagged as unhealthy? How do I handle rate-limiting when probing many domains? What does the audit log contain? |

## 资源列表

The following resources represent the initial seed set for this project. All URLs are preserved exactly as provided, without modification, and are rendered within code tags for unambiguous reference.

### Video and Subtitle Resource Domains

<code>zaixianzhongwenzimuwangzhan.org.cn</code>

<code>zhongwenzimuzaixianyingyuan.org.cn</code>

<code>zhongwenzimumianfeizaixianbofang.org.cn</code>

<code>gaoqingshipinzhongwenzimu.org.cn</code>

<code>zhongwenzimuyirenzaixian.org.cn</code>

<code>zhongwenzimuzaixiankanpian.org.cn</code>

<code>gaoqingpianyuanzaixianbofang.org.cn</code>

## 项目结构

```
zimu-bridge/
├── src/
│   └── zimu_bridge/                # Main package root
│       ├── __init__.py             # Package metadata and version
│       ├── cli.py                  # Click command definitions (export, serve, probe)
│       ├── manifest.py             # Manifest loader, parser, and validator
│       ├── probe.py                # Health check worker with timeout and retry logic
│       ├── exporter.py             # Static site generator using Jinja2 templates
│       ├── api.py                  # Flask/FastAPI-like REST endpoint definitions
│       ├── models/                 # Pydantic data models for resources and config
│       │   ├── resource.py
│       │   ├── config.py
│       │   └── status.py
│       ├── utils/                  # Helper functions (URL normalization, logging, file I/O)
│       │   ├── url_utils.py
│       │   ├── log_utils.py
│       │   └── fs_utils.py
│       └── templates/              # Jinja2 HTML templates for dashboard rendering
│           ├── base.html
│           ├── index.html
│           └── partials/
├── tests/                          # Unit and integration tests (pytest)
│   ├── test_manifest.py
│   ├── test_probe.py
│   ├── test_exporter.py
│   └── fixtures/                   # Sample manifest files for test cases
├── docs/                           # User and developer documentation (Markdown)
│   ├── user-guide/
│   ├── api/
│   ├── configuration/
│   ├── development/
│   ├── deployment/
│   └── troubleshooting/
├── scripts/                        # Utility scripts for local development and CI
│   ├── format.sh                   # Ruff formatting wrapper
│   ├── lint.sh                     # Ruff linting wrapper
│   └── test.sh                     # Pytest invocation with coverage
├── requirements.txt                # Runtime dependencies
├── requirements-dev.txt            # Development and testing dependencies
├── pyproject.toml                  # Project metadata, build config, and tool settings
├── README.md                       # This document
├── LICENSE                         # MIT license text
└── .gitignore                      # Ignored files and directories
```

## 贡献指南

We welcome contributions that improve link processing reliability, extend output formats, or enhance the probe subsystem. Please follow these steps:

1. Review the development documentation in `docs/development/` to understand the codebase structure, coding conventions, and testing requirements. Ensure your local environment matches the specified Python and dependency versions.

2. Open an issue describing the problem you intend to solve or the feature you wish to add. Clearly state the motivation, expected behavior, and any potential impact on existing functionality. Wait for maintainer feedback before proceeding with significant changes.

3. Fork the repository and create a new branch with a descriptive name (e.g., `feature/add-jsonl-manifest-support` or `fix/probe-timeout-handling`). Commit your changes with clear, concise commit messages that reference the issue number when applicable.

4. Write or update unit tests to cover your changes. Ensure all existing tests pass and that code coverage does not decrease. Run the linting and formatting scripts (`scripts/format.sh` and `scripts/lint.sh`) to maintain code style consistency.

5. Submit a pull request against the main branch, including a detailed description of your changes, test results, and any manual verification steps performed. Pull requests must pass all CI checks before they are considered for review.

## 常见问题

**Q: How does Zimu Bridge handle URLs that are unreachable or return 5xx status codes?**

A: The probe subsystem performs up to three retries with exponential backoff (1s, 2s, 4s) for each URL. If all attempts fail or return a server-error status, the entry is marked as `unhealthy` in the internal status store. The static exporter includes an optional filter to exclude unhealthy entries, and the REST API provides a query parameter to filter by health status. Audit logs record each probe attempt with timestamps and response details for manual inspection.

**Q: Can I use Zimu Bridge with a manifest that contains mixed protocols (http and https) or non-standard ports?**

A: Yes. The manifest parser does not alter any part of the URL string. The probe subsystem respects the protocol and port as specified in the original entry. For health checks, the system uses the `requests` library with default timeouts and no automatic redirect following beyond the standard library behavior. Users are advised to ensure that their manifest entries are syntactically valid; malformed URLs are logged as errors and skipped during processing.

**Q: Is there a way to schedule periodic manifest regeneration and site export without manual intervention?**

A: The Zimu Bridge CLI does not include a built-in scheduler, but it is designed to be invoked by external automation tools such as cron (Unix) or Task Scheduler (Windows). A typical setup involves a cron job that runs `python -m zimu_bridge export --input manifest.txt --output ./dist` every hour, combined with a separate job for probing. For containerized deployments, you can wrap the export command in a lightweight Docker image and use orchestration features like Kubernetes CronJob or AWS EventBridge.

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-21 22:29:12
