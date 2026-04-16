# Environment Setup Guide (macOS)

This document lists the tools and libraries needed to build and run the Gmail Email Extractor project locally.

## 1) System Tools to Install

Install these first:

- `git`
- `python@3.11` (or `3.12`)
- `node` (`v20+`)
- `npm` (bundled with Node)
- `sqlite`
- `docker` + Docker Compose (recommended)
- `gh` (GitHub CLI, recommended)

### Install with Homebrew

```bash
brew update
brew install git python@3.11 node sqlite gh
brew install --cask docker
```

### Verify installation

```bash
git --version
python3 --version
node --version
npm --version
sqlite3 --version
gh --version
docker --version
docker compose version
```

---

## 2) Python Environment (Backend)

From the project root:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -U pip
```

Install backend/runtime libraries:

```bash
pip install fastapi "uvicorn[standard]" sqlalchemy alembic pydantic-settings python-dotenv httpx google-api-python-client google-auth google-auth-oauthlib cryptography python-multipart
```

Install testing/linting libraries:

```bash
pip install pytest pytest-asyncio ruff black pre-commit
```

---

## 3) Frontend Environment (React + TypeScript)

Create app scaffold:

```bash
npm create vite@latest frontend -- --template react-ts
cd frontend
```

Install runtime libraries:

```bash
npm install react-router-dom axios
```

Install development/testing libraries:

```bash
npm install -D eslint prettier vitest @testing-library/react @testing-library/jest-dom @vitejs/plugin-react
```

---

## 4) Google Cloud / Gmail API Prerequisites

Before OAuth flow can work, configure:

1. Create Google Cloud project
2. Enable Gmail API
3. Configure OAuth consent screen
4. Create OAuth Client ID (Web application)
5. Add redirect URI (example):
   - `http://localhost:8000/api/gmail/callback`

Store client ID/secret in your backend environment variables.

---

## 5) Recommended Versions

- Python: `3.11.x` (preferred)
- Node.js: `20.x` or newer
- npm: latest stable bundled with Node

---

## 6) Quick Start Checklist

- [ ] Homebrew tools installed
- [ ] Python virtual environment created
- [ ] Python dependencies installed
- [ ] Frontend scaffold created
- [ ] Frontend dependencies installed
- [ ] Google OAuth credentials created
- [ ] Redirect URI configured correctly

---

## 7) Notes

- Keep `.venv/` out of git (add to `.gitignore`).
- Do not commit OAuth client secrets or `.env` files.
- Run Docker Desktop at least once after installation so `docker compose` is available.
