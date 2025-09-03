
# AI Textbook (Jupyter Book + uv)

This repo contains a Jupyter Book built and managed with the **uv** package manager.

- 📚 Authoring: Markdown (`.md`) or notebooks (`.ipynb`)
- 🧱 Builder: Jupyter Book (Sphinx)
- 📦 Env & deps: uv (`pyproject.toml`, `uv.lock`)
- 🌐 Hosting: GitHub Pages (`gh-pages` branch via `ghp-import`)

---

## Quick Start

### Prerequisites
- **uv** (Windows PowerShell):
  ```powershell
  iwr https://astral.sh/uv/install.ps1 -UseBasicParsing | iex

* Git + a GitHub repo

### Clone & set up

```powershell
git clone https://github.com/<USER>/<REPO>.git
cd <REPO>

# install dependencies from pyproject.toml / uv.lock
uv sync
```

(Optional) register a Jupyter kernel for this project:

```powershell
uv run python -m ipykernel install --user --name "textbook"
```

---

## Project Structure

```
book/
  _config.yml     # Jupyter Book config
  _toc.yml        # Table of contents
  intro.md        # Landing page
  references.bib  # (optional) bibliography
  ...             # your chapters/sections
pyproject.toml    # dependencies managed by uv
uv.lock           # lockfile (commit this)
```

---

## Writing Content

1. **Create a page** (Markdown or notebook) inside `book/`, e.g.:

   * `book/01-getting-started.md`
   * `book/02-basics.ipynb`

2. **Add it to the TOC** (`book/_toc.yml`):

   ```yaml
   format: jb-book
   root: intro
   chapters:
     - file: 01-getting-started
     - file: 02-basics
   ```

3. **(Optional) Citations**: Put references in `book/references.bib` and use standard MyST citation syntax.

---

## Notebook Execution Options

Control execution in `book/_config.yml`:

* **Turn off execution** (fastest local builds):

  ```yaml
  execute:
    execute_notebooks: "off"
  ```

* **Execute and allow errors** (useful while drafting):

  ```yaml
  execute:
    execute_notebooks: "auto"
    allow_errors: true
    timeout: 60
  ```

> Windows tip (optional): to silence an asyncio/zmq warning, add a `conf.py`:
>
> ```python
> # book/conf.py
> import asyncio, sys
> if sys.platform.startswith("win"):
>     asyncio.set_event_loop_policy(asyncio.WindowsSelectorEventLoopPolicy())
> ```

---

## Build Locally

```powershell
cd book
uvx jupyter-book build .
```

Open `_build/html/index.html` in your browser.

---

## Publish to GitHub Pages

> The first time, create the repo on GitHub and push `main` as usual.

Each time you want to publish:

```powershell
cd book
uvx jupyter-book build .
uvx ghp-import -n -p -f _build/html
```

* `-n` writes a `.nojekyll`
* `-p` pushes to the `gh-pages` branch
* `-f` forces update

If using a custom domain:

```powershell
uvx ghp-import -n -p -f -c yourdomain.com _build/html
```

Then set the domain under **GitHub → Settings → Pages** and enable **Enforce HTTPS** (once the cert is ready).

---

## Dependency Management (uv)

* **Add a package**:

  ```powershell
  uv add <package>
  ```
* **Remove a package**:

  ```powershell
  uv remove <package>
  ```
* **Run a tool without installing globally**:

  ```powershell
  uvx jupyter-book --version
  ```

The environment is defined by `pyproject.toml` and pinned by `uv.lock`. Commit both.

---

## Common Tasks

* **Create a new chapter**:

  ```powershell
  ni book\03-advanced.md
  # add to _toc.yml, then:
  cd book
  uvx jupyter-book build .
  ```

* **Serve locally (simple)**: open `_build/html/index.html` after build.
  (If you want live-reload, use your editor/preview tools or a local static server.)

* **Clean build artifacts**:

  ```powershell
  rmdir -Recurse -Force book\_build
  ```

---

## Troubleshooting

* **TOC changes not appearing**: rebuild the book, then republish (`ghp-import`).
* **Execution errors in demo pages**: set `allow_errors: true`, or remove the sample notebook from `_toc.yml`.
* **Repository not found when pushing**: create the GitHub repo first (empty), then `git push -u origin main`.

---
