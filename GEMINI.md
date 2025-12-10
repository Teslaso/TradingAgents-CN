# TradingAgents-CN 上下文说明

## 项目概览

**TradingAgents-CN** 是一个专为中文用户量身定制的多智能体和大模型股票分析学习平台。它利用 AI 智能体进行股票研究和策略实验。本项目是原 TradingAgents 框架的“中文增强版”，具有对 A 股的完整支持、本地化模型集成（DeepSeek 等）以及现代化的 Web 架构。

**版本:** v1.0.0-preview
**架构:** 单一代码库 (后端 + 前端)

### 技术栈

*   **后端:** Python 3.10+, FastAPI, Uvicorn
*   **前端:** Vue 3, Vite, Element Plus, TypeScript
*   **数据库:** MongoDB (数据存储), Redis (缓存与队列)
*   **AI/LLM:** OpenAI, LangChain, Google Gemini, DeepSeek, DashScope
*   **数据源:** AKShare, Tushare, BaoStock, YFinance
*   **基础设施:** Docker, Docker Compose

## 目录结构

*   `app/`: FastAPI 后端源代码。
    *   `main.py`: 应用程序入口点。
    *   `routers/`: API 路由定义。
    *   `services/`: 业务逻辑。
    *   `models/`: 数据库模型。
    *   `core/`: 核心配置和工具。
*   `frontend/`: Vue 3 前端应用程序。
    *   `src/`: 源代码。
    *   `vite.config.ts`: Vite 配置文件。
*   `config/`: 配置文件（日志等）。
*   `data/`: 数据存储（报告、分析结果）。
*   `docker/`: Docker 配置文件。
*   `examples/`: 演示用法的 Python 脚本。
*   `tests/`: 测试套件。
*   `docker-compose.yml`: Docker 编排文件。
*   `main.py`: 根入口脚本（包装 `app.main`）。

## 开发环境设置

### 前置要求

*   **Python:** >= 3.10
*   **Node.js:** >= 18.0.0 (用于前端)
*   **服务:** MongoDB, Redis (本地运行或通过 Docker)

### 后端开发

1.  **环境:**
    ```bash
    python -m venv venv
    # Windows
    .\venv\Scripts\activate
    # Linux/Mac
    source venv/bin/activate
    ```

2.  **依赖:**
    ```bash
    pip install -r requirements.txt
    ```

3.  **配置:**
    *   确保根目录或 `app/` 目录下存在 `.env` 文件。如果有 `.env.example`，请复制一份。
    *   配置 `MONGODB_HOST`, `REDIS_HOST` 和 LLM API 密钥。

4.  **运行:**
    ```bash
    # 通过 Python 包装器运行
    python main.py
    # 或直接通过 Uvicorn 运行
    uvicorn app.main:app --reload
    ```

### 前端开发

1.  **进入目录:**
    ```bash
    cd frontend
    ```

2.  **依赖:**
    ```bash
    npm install
    # 或
    yarn install
    ```

3.  **运行:**
    ```bash
    npm run dev
    ```

### Docker 部署

要运行整个技术栈（后端 + 前端 + 数据库）：

```bash
docker-compose up -d --build
```

## 常用命令

*   **后端运行:** `python main.py`
*   **前端运行:** `npm run dev` (在 `frontend/` 目录中)
*   **前端构建:** `npm run build` (在 `frontend/` 目录中)
*   **Docker 启动:** `docker-compose up -d`
*   **Docker 日志:** `docker-compose logs -f`

## 开发规范

*   **代码风格:** Python 遵循 PEP 8。前端使用 ESLint/Prettier。
*   **提交:** 使用清晰、语义化的提交信息 (例如 `feat: ...`, `fix: ...`)。
*   **语言:** 文档和注释主要使用中文 (CN)，但代码变量/函数名使用英文。
*   **API:** 使用 FastAPI 路由设计的 RESTful API。
*   **异步:** 大量使用 `asyncio` 进行 I/O 密集型操作（数据库、API 调用）。