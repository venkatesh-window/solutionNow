<!-- Repository-specific Copilot / AI agent instructions. Keep this short and concrete. -->
# Copilot instructions — repository snapshot and actionable rules

Repository snapshot (auto-discovered):

- Root contains a single file: `website` (path: `website`). That file is currently empty.
- No `README.md`, `package.json`, or other source directories were found during inspection.

What this means for an AI agent

- Do not assume a particular framework. The repo is effectively empty except for `website`.
- Before making scaffolded or heavy changes (adding a full app, toolchain, or CI), ask the repo owner which direction they want (static site, Node app, Python app, etc.).

Actionable rules (follow these strictly)

1. Exploration first — always search for these files before making changes: `README.md`, `package.json`, `pyproject.toml`, `package-lock.json`, `yarn.lock`, `src/`, `public/`, `.gitignore`, `.github/`.
   - Example: if `package.json` exists, prefer `npm ci` over `npm install` when preparing the environment.

2. Non-destructive edits — never overwrite `website` or delete files without explicit confirmation from the user.

3. If asked to scaffold a project, propose options and wait for approval. When scaffolding for Node/JS web projects, include a minimal set of files and a single `npm` script; do not enable CI or push workflow changes unless requested.

4. Use Windows PowerShell-friendly commands when suggesting terminal steps (this workspace uses PowerShell). Example quick checks:

```
Get-ChildItem -Force -Recurse -File | Select-Object FullName
if (Test-Path package.json) { npm ci }
```

5. When you add files, include a short `README.md` change describing purpose and a test command. Keep commits logically small and include a descriptive commit message.

6. Reference patterns by file when applicable. Examples of checks to run if those files appear:
   - `package.json` -> inspect `scripts` for `dev`, `start`, `build` (use them).
   - `README.md` -> honor project's stated instructions.
   - `src/` or `app/` -> treat as primary source directory.

Templates and examples (only add after approval)

- Minimal web scaffold suggestion (ask first): create `package.json`, `src/index.html`, `src/styles.css`, and `README.md` with one `start` script using a tiny local server (serve with `npx http-server` or equivalent).

When in doubt

- Ask a clarifying question. The repo is too small to safely infer a target stack. Examples of clarifying prompts:
  - "Do you want a static website, a Node/Express app, or a Next/React site?"
  - "May I create a minimal scaffold and where should it live (root or `website/` directory)?"

Files to check first (ordered): `README.md`, `package.json`, `pyproject.toml`, `requirements.txt`, `src/`, `app/`, `public/`, `.github/workflows/`.

If you modify the repo

- Add one-line instructions in the root `README.md` describing how to run the project locally on Windows PowerShell.
- Add at least one minimal smoke test or `npm script`/`python -m` entry so the owner can validate quickly.

Contact for unclear cases: ask the repository owner before making large structural changes.

— End of file
