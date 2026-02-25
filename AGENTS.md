# AGENTS.md

## Cursor Cloud specific instructions

### Overview

This is Microsoft's **AI Agents for Beginners** educational course — a collection of 23 Jupyter notebooks across 11 lessons teaching AI Agent development patterns using Semantic Kernel, AutoGen, and Azure AI Agent Service.

### Services

| Service | How to start | Notes |
|---|---|---|
| Jupyter Notebook Server | `source .venv/bin/activate && jupyter notebook --no-browser --port=8888 --ip=0.0.0.0 --ServerApp.token='' --ServerApp.password=''` | Primary dev interface; serves all 23 lesson notebooks |
| Chainlit App (Lesson 11) | `cd 11-mcp/code_samples/github-mcp && chainlit run app.py -w` | Optional MCP demo; requires `GITHUB_TOKEN` |

### Development setup

- Python virtual environment is at `.venv` (Python 3.12). Always activate with `source .venv/bin/activate` before running commands.
- Configuration is in `.env` (copied from `.env.example`). Notebooks require either `GITHUB_TOKEN` (for GitHub Models samples) or Azure credentials (for Azure AI samples) to execute LLM calls.
- ChromaDB runs embedded in-process — no separate service needed for RAG notebooks (Lesson 5).
- Node.js is required for the MCP server in Lesson 11 (`npx @modelcontextprotocol/server-github`).

### Linting & testing

- No Python linters are configured in-repo (no pyproject.toml, ruff, flake8). The CI pipeline only runs **markdownlint** on `.md` and `.ipynb` files via `DavidAnson/markdownlint-cli2-action`.
- To syntax-check all notebook code cells: `python -c "import nbformat, ast, os; ..."` (see setup verification in README's course-setup).
- Import verification: `python -c "import semantic_kernel; import autogen_core; import chromadb; import chainlit; import openai"`.

### Gotchas

- The `notebook` and `jupyter` pip packages are **not** in `requirements.txt` but are needed to run `jupyter notebook`. The update script installs them.
- A benign `RequestsDependencyWarning` about urllib3/chardet versions appears on import — this can be ignored.
- ChromaDB telemetry warnings (`Failed to send telemetry event`) are harmless and expected in sandboxed environments.
