**MarkItDown — Developer Quickstart**

This repository contains the MarkItDown project. The actual Python package source lives under `packages/markitdown/packages/markitdown` in this workspace (the top-level `packages/markitdown` repo contains multiple packages).

**Overview**:
- **Purpose:** Convert a variety of document formats to Markdown via a CLI and programmatic API.
- **Where the code is:** `packages/markitdown/packages/markitdown`

**Environment setup**:
- **Create a virtual environment** (recommended):

  ```bash
  python -m venv .venv
  source .venv/bin/activate
  ```

- **Upgrade pip (optional but recommended):**

  ```bash
  ./.venv/bin/python -m pip install --upgrade pip
  ```

**Install the package (editable) with extras**:
- From the repository root, install the nested package in editable mode and include the `all` extras used for demos and testing:

  ```bash
  ./.venv/bin/pip install -e 'packages/markitdown/packages/markitdown[all]'
  ```

- If you prefer to install only base dependencies, omit the extras:

  ```bash
  ./.venv/bin/pip install -e 'packages/markitdown/packages/markitdown'
  ```

**Run the CLI (quick demo)**:
- Show help:

  ```bash
  ./.venv/bin/markitdown --help
  ```

- Convert a local file and write output to a file:

  ```bash
  ./.venv/bin/markitdown input.pdf -o output.md
  ```

- Read from stdin and write to stdout:

  ```bash
  cat input.pdf | ./.venv/bin/markitdown > output.md
  ```

- Example with a simple text demo (already run during development):

  ```bash
  printf 'Hello, MarkItDown demo\n' > demo-input.txt
  ./.venv/bin/markitdown demo-input.txt -o demo-output.md
  cat demo-output.md
  ```

**Programmatic usage**:
- Basic example in Python (run from anywhere inside the activated virtualenv):

  ```python
  from markitdown import MarkItDown

  md = MarkItDown()
  result = md.convert('path/to/file.pdf')
  print(result.markdown)
  ```

**Running tests**:
- From the repository root, run pytest against the package tests:

  ```bash
  ./.venv/bin/python -m pytest packages/markitdown/packages/markitdown/tests
  ```

**Development notes & tips**:
- The package uses `hatchling` via `pyproject.toml`; editable install uses PEP 660 and the nested project layout.
- The console entry point is `markitdown` (declared in `pyproject.toml`), so after editable install the CLI will be available in the venv as `./.venv/bin/markitdown`.
- Audio features require an external `ffmpeg`/`avconv` binary. If you see warnings like `Couldn't find ffmpeg or avconv`, install `ffmpeg` (Homebrew on macOS):

  ```bash
  brew install ffmpeg
  ```

- Document Intelligence (cloud) mode: use `-d --endpoint <ENDPOINT>` to call a Document Intelligence endpoint instead of local conversion. Ensure you have valid credentials and endpoint URL.

- Plugins: third-party plugins expose the `markitdown.plugin` entry point. Use `--list-plugins` to see installed plugins and `-p/--use-plugins` to enable them on conversion.

**Troubleshooting**:
- If `pip` is not found, make sure the virtualenv is activated or run `./.venv/bin/pip` directly.
- If editable install fails because the project path is different, locate the package's `pyproject.toml` and run `pip install -e '.[all]'` from that directory instead.

**Contributing**:
- Follow the existing repo conventions (pre-commit, tests in `tests/`, `pyproject.toml` for build metadata).
- Run `pre-commit` locally if configured (see `.pre-commit-config.yaml`).

**Where to look next**:
- Main source: `packages/markitdown/packages/markitdown/src/markitdown`
- Tests: `packages/markitdown/packages/markitdown/tests`
- Sample plugin: `packages/markitdown/packages/markitdown-sample-plugin`

If you want, I can now:
- Run the full test suite and collect failures, or
- Show a demo conversion of a specific file type (PDF, DOCX, PPTX, audio, etc.), or
- Add contribution guidelines / a CHANGELOG section to this README.
