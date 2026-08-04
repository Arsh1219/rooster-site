# rooster-site — STRICT SCOPE RULES

**This repo is PUBLIC.** It is the source for the Rooster website, served
from TWO hosts with identical content (see `DEPLOY.md`): the canonical
**https://wakerooster.com** (cPanel at 135.181.16.97 behind Cloudflare,
uploaded via rsync) and **https://arsh1219.github.io/rooster-site/**
(GitHub Pages — still what the live App Store listing and shipped builds
link to; must stay published and current).

## Hard rules — never violate

1. **Static pages only.** Allowed content: HTML, CSS, images, self-hosted
   fonts (`.woff2` + license `.txt`), `.nojekyll`, `CNAME`, `robots.txt`,
   `sitemap.xml`, markdown docs, and `.githooks/`. Nothing else.
2. **Never add app code here.** No Swift files, no Xcode projects, no
   `project.yml`, no IPAs/archives, no scripts from the app repo. The app's
   full source lives in the separate PRIVATE repo `Arsh1219/rooster-alarm`
   (local: `../rooster_alarm`). If a task involves app code, do it there.
3. **No secrets, keys, or credentials** of any kind — everything committed
   here is public on the internet immediately.
4. Do not delete or rename the `/privacy/`, `/terms/` or `/support/` paths —
   they are wired into the shipped app (PaywallView/SettingsView) and App
   Store Connect. Breaking these URLs breaks App Review compliance
   (3.1.2; `/support/` is the required ASC Support URL — user confirmed
   keeping it on Jul 16, 2026 after considering deletion).
5. **Never add a `CNAME` file.** DNS for wakerooster.com points at the
   cPanel server, not GitHub — a CNAME here would put Pages in a
   failed-domain state and could break the github.io URLs the live App
   Store listing still uses. Every site change must be BOTH pushed here
   and rsynced to cPanel (`DEPLOY.md`).
6. Content style (user preference): no "short version"/TL;DR summary boxes
   on legal pages; the site is a fixed dark theme (matches the app's
   "pre-dawn" identity) and the header brand uses the real app logo SVG
   (`assets/logo-on-dark.svg`), not an emoji. Marketing copy: sentence case,
   no exclamation marks, and no hyphens or dashes in rendered text.
7. Legal pages (`/privacy/`, `/terms/`) changed only with explicit user
   approval — they are load-bearing for App Review and ad platforms.

## Enforcement

`.githooks/pre-commit` rejects any staged file outside the allowlist.
It is enabled via `git config core.hooksPath .githooks` — after a fresh
clone, re-run that command once. Never bypass with `--no-verify`.

## Deploy

Push to `main` → GitHub Pages deploys automatically. DNS + custom-domain
setup steps live in `DEPLOY.md`.
