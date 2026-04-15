# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static website for NitroX Consulting (nitroxconsulting.com), a financial consulting firm. The site is served via nginx in a Docker container.

## Build & Run

```bash
# Build the Docker image
docker build -t nitroxconsulting .

# Run the container (serves on port 80)
docker run -d -p 8080:80 nitroxconsulting
```

The root `dockerfile` copies the entire `Nitroxconsulting.com/` directory into nginx's default HTML root (`/usr/share/nginx/html`). There is a duplicate dockerfile inside `Nitroxconsulting.com/` — use the one at the repo root.

## Architecture

This is a single-page application built with jQuery 1.7.1. All content lives in `Nitroxconsulting.com/index.html` as a set of `<li>` sections (`#pageHome`, `#pageAbout`, `#pageServices`, `#pageSolutions`, `#pageContacts`, `#pagePrivacy`, `#pageMore`) toggled via hash-based navigation (`#!/pageName`). There is no build step or bundler — all assets are served as-is by nginx.

**CSS layers:**
- `css/` — main site styles (`reset.css`, `layout.css`, `style.css`, `ie.css`)
- `Content/` — Bootstrap and scrolling-nav styles (from a legacy .NET project scaffold)

**JS layers:**
- `js/` — site functionality: `scripts.js` (main), `slider.js`, `sprites.js`, `forms.js`, `googleMap.js`, plus jQuery plugins
- `Scripts/` — Bootstrap/jQuery 3.3.1 (from the .NET scaffold, not actively used by `index.html`)

The `.csproj` file is a leftover from a Visual Studio web project and is not used for building.
