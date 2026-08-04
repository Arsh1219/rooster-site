# Deploying wakerooster.com

The site is served from TWO places with identical content:

1. **wakerooster.com** — cPanel host `135.181.16.97` (behind Cloudflare;
   DNS A record → the server, proxied). This is the canonical home; every
   page's `<link rel="canonical">` points here.
2. **https://arsh1219.github.io/rooster-site/** — GitHub Pages, serving the
   SAME files. The live App Store listing and shipped app builds (1.0.0,
   1.0.1) still point at these URLs, so this copy must stay published and
   current until ASC metadata is swapped to the domain. There is
   deliberately NO `CNAME` file: with DNS pointed at the cPanel server, a
   CNAME here would put GitHub Pages in a failed-domain state and could
   break the github.io URLs the live listing depends on.

## Updating the site (both hosts, in this order)

```bash
# 1. GitHub (keeps the live-listing URLs current)
cd ~/Documents/coding_projects/rooster-site
git add -A && git commit -m "site: <what changed>" && git push

# 2. cPanel (the domain itself)
rsync -avz --delete \
  --exclude '.git*' --exclude 'CLAUDE.md' --exclude 'README.md' \
  --exclude 'DEPLOY.md' --exclude '.nojekyll' \
  ./ conversorsdeletr@135.181.16.97:<docroot for wakerooster.com>/
```

`.htaccess` (Apache) provides the custom 404 on cPanel; GitHub Pages
ignores it and uses `404.html` natively.

## SSL

Cloudflare terminates visitor HTTPS at the edge. On the origin, cPanel
AutoSSL issues the cert for the domain (Full/Strict mode safe). If the
padlock misbehaves right after setup, check Cloudflare SSL mode vs the
origin cert.

## Later (do NOT do these now)

- **App Store Connect metadata** (support/privacy URLs) is updated by
  `scripts/asc_publish.py metadata` in the app repo — run it only after the
  current review submission (1.0.1) is approved. Editing ASC metadata while
  a build is Waiting for Review silently drops it from the queue.
- After ASC points at wakerooster.com, the github.io copy becomes legacy
  but must keep working for already-shipped binaries.
