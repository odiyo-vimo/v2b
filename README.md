# V2B Trade Journal

Web pages for the V2B NinjaTrader strategy, published with GitHub Pages
(Settings → Pages → Source: **GitHub Actions**).

- `/v2b/` – list of traders (`index.html`, reads `users.json`)
- `/v2b/<name>/` – one trader's journal: trades by date and the bar-by-bar decision log

## How it is filled

Each trader's V2B strategy uploads, using its own fine-grained token:

| Path | When |
|---|---|
| `<name>/data/index.json`, `<name>/data/YYYY-MM-DD.json` | after each closed trade |
| `<name>/logs/YYYY-MM-DD.txt` | after each 5-minute bar while live |
| `<name>/index.html` | copied from `template/index.html` when it changes |
| `users.json` | when a trader uploads for the first time |

`.github/workflows/pages.yml` republishes the site only when a page changes.
Data uploads (`<name>/data`, `<name>/logs`, `users.json`) don't republish it;
the pages read those files straight from the repo through GitHub's API.
