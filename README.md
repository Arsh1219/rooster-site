# rooster-site

> ⚠️ **This repo is PUBLIC and holds static pages only** — never add app code,
> keys, or build artifacts. The app source lives in the private repo
> `rooster-alarm`. Scope is enforced by `.githooks/pre-commit`
> (`git config core.hooksPath .githooks` after cloning).

Static GitHub Pages site for the Rooster iOS alarm app, served at
**https://wakerooster.com** (see `CNAME`; setup steps in `DEPLOY.md`).

- `/` — marketing landing page
- `/privacy/` — privacy policy (App Store Connect "Privacy Policy URL" + in-app links)
- `/terms/` — terms of use (in-app links)
- `/support/` — support page (App Store Connect "Support URL")

No build step, no JavaScript, no analytics. Fonts are self-hosted
(SIL OFL, see `fonts/OFL-LICENSES.txt`).
