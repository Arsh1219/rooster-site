# rooster-site — STRICT SCOPE RULES

**This repo is PUBLIC.** It is the GitHub Pages site for the Rooster iOS app
(privacy policy + support pages) and nothing else.

## Hard rules — never violate

1. **Static pages only.** Allowed content: HTML, CSS, images, `.nojekyll`,
   `CNAME`, `robots.txt`, markdown docs, and `.githooks/`. Nothing else.
2. **Never add app code here.** No Swift files, no Xcode projects, no
   `project.yml`, no IPAs/archives, no scripts from the app repo. The app's
   full source lives in the separate PRIVATE repo `Arsh1219/rooster-alarm`
   (local: `../rooster_alarm`). If a task involves app code, do it there.
3. **No secrets, keys, or credentials** of any kind — everything committed
   here is public on the internet immediately.
4. Do not delete or rename `/privacy/` or `/support/` paths — they are wired
   into the shipped app (PaywallView/SettingsView) and App Store Connect.
   Breaking these URLs breaks App Review compliance (guideline 3.1.2).

## Enforcement

`.githooks/pre-commit` rejects any staged file outside the allowlist.
It is enabled via `git config core.hooksPath .githooks` — after a fresh
clone, re-run that command once. Never bypass with `--no-verify`.
