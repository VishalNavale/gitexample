# GitHub Copilot / AI Agent Instructions for this repository

Note: the repository is currently empty. The instructions below are tailored to help any AI coding agent quickly discover the project's structure and make productive changes once code is added. If this file already exists, merge carefully and preserve any project-specific guidance.

Overview — what to do first
- **Scan:** Run glob searches for `package.json`, `pyproject.toml`, `go.mod`, `pom.xml`, `Cargo.toml`, `README.md`, `Dockerfile`, `docker-compose.yml`, `Makefile`, `.github/workflows/**`, `services/**`, `src/**`, `cmd/**`, `internal/**`, `tests/**`.
- **Identify language & build:** Use file matches to determine primary language and build/test commands (see bottom for usual commands per ecosystem).
- **Find entrypoints:** Look for `main`, `index.js`, `app.py`, `cmd/`, `server/`, or `src/main` to locate the runtime entrypoint.

Big-picture architecture cues to extract
- **Service boundaries:** Prefer `services/<name>/`, `packages/` or `modules/` directories. Treat each top-level folder with its own `package.json`/`pyproject.toml`/`go.mod` as a separate service or package.
- **Config patterns:** Look for `.env`, `config/`, `configs/*.yaml`, `settings.py` or `config/*.json`. If present, configuration is environment-driven and use of environment variables is expected.
- **Data flows & integrations:** Search for imports referencing `clients/`, `lib/`, `pkg/`, `adapters/` or `integrations/`. Follow the chain from API/controller -> service -> repo/adapter.
- **Container & infra:** Presence of `Dockerfile`, `docker-compose.yml`, `k8s/`, or `helm/` indicates containerized deployment. Prioritize local `docker-compose` for multi-service runs.

Project-specific developer workflows to discover
- **Build / test / run commands:** Extract from `package.json` scripts, `Makefile` targets, `README.md`, or CI workflow files in `.github/workflows/`. Prefer using existing script names instead of inventing new ones.
- **CI patterns:** Inspect `.github/workflows/*.yml` for test/build steps; mirror those locally when reproducing CI failures.
- **Debugging:** If `launch.json` or `.vscode/` exists, prefer those debug configurations for recommended ports and env vars.

Conventions and patterns to follow
- **Naming:** Follow existing folder naming (kebab-case, snake_case, or camelCase) used in the repo — match style for new files.
- **Service structure:** Common pattern used in this repo (when present): `controllers/` or `api/` -> `services/` -> `repositories/` or `adapters/`. Keep that ordering in new code.
- **Dependency changes:** If adding or updating dependencies, update the appropriate top-level manifest (monorepos: update package in that package folder and root if present) and update `yarn.lock`/`package-lock.json` or equivalent.
- **Tests:** Prefer the repository's test runner; locate `pytest.ini`, `jest.config.js`, or `go.mod` test commands and run them with the same flags.

How to produce small PRs and commits
- Keep changes focused to 1-2 files when possible.
- Follow commit message style similar to existing commits (examine `git log` if available). If none, use: `feat: <short description>` or `fix: <short description>`.
- Add or update tests for behavior changes; place them next to the code module when repo uses that layout (e.g., `module_test.go`, `test_*.py`, `*.spec.ts`).

Examples of detective checks (concrete commands for agents)
- Find language and entrypoint:
  - `git ls-files | Select-String -Pattern "package.json|pyproject.toml|go.mod|pom.xml|Cargo.toml|Dockerfile"`
- Identify run/test scripts:
  - `Select-String -Path "**/package.json" -Pattern '"scripts"' -List`
- Inspect CI to replicate environment:
  - `ls .github/workflows || echo 'no workflows'`

Ecosystem quick-reference (common commands agents should try)
- Node: `npm ci` then `npm test` or `npm run build` (Windows PowerShell: `npm ci; npm test`).
- Python: create a venv, `pip install -r requirements.txt` then `pytest -q`.
- Go: `go test ./...`.
- Docker compose: `docker-compose up --build`.

Merging guidance
- If this repo already has an instruction file, preserve any human-written rationale and examples. Only add or adjust missing items that are discoverable from the tree.
- Add repository-specific commands and file paths you discover (replace generic commands above with exact scripts).

When something is missing
- Document what you tried (commands, files searched) and which files you expected to find (e.g., `package.json`, `README.md`).
- Propose a minimal runnable example if the repo lacks an obvious local-run path (small `docker-compose.yml` or `Makefile` stub).

Next steps for humans
- Add a short project README with run/test commands and primary language if you want agents to bootstrap faster.

If anything here is unclear or you'd like me to include repository-specific snippets once code exists, tell me which folders or languages to prioritize and I'll update this file.