# Hospital Digitalisation Handbook — source

This folder is the source of the handbook. The content is Markdown under `docs/`; `mkdocs.yml` is
the navigation and theme. The site is built with [MkDocs Material](https://squidfunk.github.io/mkdocs-material/),
the same toolchain as AUCOOP's [Community Network Handbook](https://aucoop.github.io/Community-Network-Handbook/).

## Run it locally (Windows)

Open **PowerShell** and run these one at a time.

**1. Check Python is installed**

```powershell
python --version
```

You want 3.9 or newer. If you get *"Python was not found"*, install it from
<https://www.python.org/downloads/windows/> and **tick "Add python.exe to PATH"** during setup, then
close and reopen PowerShell.

**2. Go to this folder**

```powershell
cd "C:\Users\polgi\OneDrive\Escritorio\POL\Master\TFM\10_Handbook"
```

**3. Install MkDocs Material** (once)

```powershell
python -m pip install -r requirements.txt
```

**4. Start the local server**

```powershell
python -m mkdocs serve
```

You will see a line like `Serving on http://127.0.0.1:8000/`.

**5. Open it in Chrome**

Go to <http://127.0.0.1:8000>. Leave the PowerShell window open — that is the server. Every time
you save a `.md` file the page reloads on its own.

**6. Stop it**

Back in PowerShell, press `Ctrl + C`.

## If something goes wrong

| Symptom | Fix |
|---|---|
| `mkdocs : The term 'mkdocs' is not recognized` | Use `python -m mkdocs serve` instead of `mkdocs serve` — same thing, avoids PATH problems |
| `python : The term 'python' is not recognized` | Python is not on PATH. Reinstall with the PATH box ticked, or try `py -m mkdocs serve` |
| Port already in use | `python -m mkdocs serve -a 127.0.0.1:8001` and open port 8001 instead |
| Page shows but no styling | Normal on first load while fonts download; refresh once |
| `ERROR - Config value 'theme'` | `pip install` did not finish — run step 3 again and read the last line |

## Build a static copy

To produce plain HTML you can open without a server, or hand to someone on a USB stick:

```powershell
python -m mkdocs build
```

This creates a `site/` folder. Open `site\index.html` in Chrome. (`site/` is a build output — do not
edit it; edit `docs/` and rebuild.)

## Share it

Three ways, from quickest to most permanent.

**1. Send a folder (today, no accounts needed)**

```powershell
python -m mkdocs build
```

Zip the `site\` folder and send it. The recipient unzips it and opens `index.html` — it works
offline, in any browser, with search. Good for showing directors before anything is public.

**2. Publish on GitHub Pages (the proper way — what the Community Network Handbook does)**

The repository is already initialised here. Once a repository exists under the `aucoop`
organisation:

```powershell
git remote add origin https://github.com/aucoop/Hospital-Digitalisation-Handbook.git
git push -u origin main
```

Then, on GitHub: **Settings → Pages → Source: GitHub Actions**. The workflow in
`.github/workflows/deploy.yml` builds and publishes the site on every push to `main`. Within a
couple of minutes it is live at
`https://aucoop.github.io/Hospital-Digitalisation-Handbook/`, and every page carries an "edit
this page" link back to the source.

Check `repo_url` in `mkdocs.yml` matches the real repository name before the first push.

**3. Add a downloadable PDF** (later)

The sibling handbook attaches a PDF to each GitHub release so there is a copy for the field. Worth
copying once the content settles; not needed for v0.2.

## Same toolchain as the network handbook?

Almost. That project uses [Zensical](https://zensical.org/) — the successor to Material for MkDocs
by the same authors — and reads the same `mkdocs.yml`. This one uses Material for MkDocs directly
because it is more widely documented and easier to get help with. To match theirs exactly, change
`requirements.txt` to `zensical` and use `zensical serve` instead of `python -m mkdocs serve`.
Nothing in `docs/` changes.

## Licence

Not yet chosen. The Community Network Handbook is AGPL-3.0; for documentation, CC BY-SA 4.0 is the
more usual choice. Decide before the repository goes public and add a `LICENSE` file.

## Editing

- Content: `docs/**/*.md`. Plain Markdown, with a few extensions (admonition boxes, tabs, tables).
- Navigation: the `nav:` block at the bottom of `mkdocs.yml`. A new page must be added there to
  appear in the menu.
- Version: bump it in `docs/1-Introduction/1.3-How-To-Use-It.md` and in `docs/index.md` together.

See `docs/contributing/index.md` for house style.
