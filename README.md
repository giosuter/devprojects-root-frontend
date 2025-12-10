# devprojects-root-frontend

Static landing page (welcome page) for **https://devprojects.ch**.

This project provides a clean, multilingual entry point to all my public projects
(TaskHub Cloud, OrderFlow Cloud, FXLite, Meteo, SMS, CMS, etc.).
It is implemented as a **framework-free** frontend: plain HTML, CSS, and a small
JavaScript i18n helper.

This repository intentionally lives outside the individual project repositories.
Its only responsibility is to provide a neutral, stable root entry point for
`devprojects.ch`.

---

## Features

- Static HTML – no build step, no Node / Angular required
- Multilingual (EN / DE) language switch
- Professional layout with centralized GitHub link
- Clean separation between welcome page assets and project folders
- Simple deployment to the Hostpoint webroot

---

## Technology Stack

- HTML5 (single static `index.html`)
- CSS (custom stylesheet, no framework)
- Vanilla JavaScript for:
  - language detection
  - loading translation JSON files
  - updating UI text via `data-i18n` attributes
- Favicon (`favicon.ico`) for browser tabs and bookmarks

No frameworks, no bundlers.

---

## Folder Structure

### Repository layout (local)

```text
devprojects-root-frontend/
├── index.html               # welcome page for devprojects.ch
├── favicon.ico              # site-wide favicon
├── _root/
│   ├── css/
│   │   └── style.css        # styling for the welcome page
│   └── i18n/
│       ├── en.json          # English translations
│       └── de.json          # German translations
└── README.md
```

### Deployment layout (server)

```text
/home/zitatusi/www/devprojects.ch/
├── index.html
├── favicon.ico
└── _root/
    ├── css/
    │   └── style.css
    └── i18n/
        ├── en.json
        └── de.json
```

All other folders at `/home/zitatusi/www/devprojects.ch/`
(e.g. `/taskhub-cloud`, `/orderflow-cloud`, `/fxlite`, `/sms`, `/cms`, …)
belong to **separate projects** and are not part of this repository.

---

## i18n (Language Switch) Concept

The welcome page uses a small JavaScript helper inside `index.html`.

- Translatable elements use attributes such as:
  - `data-i18n="project.taskhub.title"`
  - `data-i18n-html="project.taskhub.challenge"` (for HTML snippets)

The script performs the following steps:

1. Determines the active language:
   - from `localStorage` (`devprojects.lang`), or
   - from the browser language (auto-detect EN / DE)
2. Loads the translation file:
   - `/i18n/<lang>.json` (served from `/_root/i18n/*.json`)
3. Replaces `textContent` / `innerHTML` of all matching elements
4. Updates `<html lang="…">` and the document `<title>`

### Supported languages

- `en` – English  
- `de` – German

### Adding a new language (example: Italian)

1. Create `_root/i18n/it.json` (same structure as `en.json`)
2. Add `<option value="it">IT</option>` to the language `<select>` in `index.html`
3. The script will automatically load `/i18n/it.json` when selected

---

## Local Editing / Testing

No build step is required.

### Clone the repository (once)

```bash
cd /Users/giovannisuter/dev/projects/devprojects-root/front-end
git clone git@github.com:giosuter/devprojects-root-frontend.git
cd devprojects-root-frontend
```

### Edit files

```bash
vim index.html
vim _root/css/style.css
vim _root/i18n/en.json
vim _root/i18n/de.json
```

### Test locally

```bash
open index.html
```

---

## Non-goals

This repository intentionally does **not** include:

- Angular, React, or other frontend frameworks
- Build tools or bundlers
- Shared UI components for hosted projects
- Server-side logic

Each application under `devprojects.ch` remains fully independent
and lives in its own repository.

---

## License

This repository contains the personal landing page for **devprojects.ch**.

The structure and ideas may be used for inspiration.
Project content, text, and branding are not intended for direct reuse.
