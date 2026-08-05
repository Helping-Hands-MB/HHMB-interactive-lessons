# AGENTS.md

Static lesson site for Helping Hands MB (4th/5th grade STEAM), embedding PhET simulations. No framework; plain HTML/CSS/JS + a Node build script.

## Commands

- `npm run build` — runs `build.js`: compiles `_lessons/*.md` into `/<lesson-id>/index.html` + `steps.js`, regenerates `shared/keyterms.js` from `shared/keyterms.json`, and rebuilds the lessons-grid in root `index.html`.
- `npm run dev` — build, then serve the repo root with `live-server`.
- No tests, linter, or typecheck exist. Verification = successful `npm run build` + manual check in browser.

## Critical: generated files are committed

Build output is tracked in git (repo history shows `chore: rebuild ...` commits). After editing any lesson markdown or `keyterms.json`, you MUST run `npm run build` and commit the regenerated files (`*/index.html`, `*/steps.js`, `shared/keyterms.js`, root `index.html`). `shared/keyterms.js` is generated — edit only `shared/keyterms.json`.

## Lesson authoring

- One markdown file per lesson in `_lessons/`, filename = output directory id.
- YAML front matter: `title`, `badge`, `description`, `icon`, `simulator` (PhET URL; defaults to circuit-construction-kit-dc). `icon` must be a key in `ICON_SVGs` inside `build.js` (`electricity`, `magnetism`, `planning`, `generic`) or it silently falls back to `generic`.
- Each step is an `##` H2 section; the first line of the section becomes the step title, the rest is the body (markdown).
- Plain YouTube URLs/links in markdown are auto-embedded as iframes by the marked renderer in `build.js`.

## Runtime architecture (client-side, loaded per lesson)

Load order in `_templates/lesson-template.html`: DOMPurify (CDN) → `shared/keyterms.js` (defines global `KEYTERMS`) → lesson `steps.js` (defines global `lessonSteps`) → `shared/lesson-engine.js`. `lesson-engine.js` renders steps, sanitizes with DOMPurify, and underlines keyterms that exist in `KEYTERMS` for hover translations (languages: en/es/pt/fr/de). If you add a term to lesson text, add it to `shared/keyterms.json` or the keyterm tooltip won't work.

## Gotchas

- `build.js` regenerates the root `index.html` lessons grid by regex-replacing everything inside `<section class="lessons-grid">...</section>` — don't restructure that section, or the build breaks with a warning.
- `drawer/` is a standalone city-planning grid-painter app (own page, own JS/CSS), independent of the lesson build pipeline.
- CI deploys on push to `main` (GitHub Actions → gh-pages; CNAME is `lessons.helpinghandsmb.org`). Build locally before pushing; the workflow runs `npm install` (npm is canonical despite `pnpm-lock.yaml` also being present).
