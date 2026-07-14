# GSMArena Scraped Data

Structured phone specifications scraped from GSMArena via the
[`gsmarena-dxomark-mobile-specs-api`](https://github.com/Sanjeevu-Tarun/gsmarena-dxomark-mobile-specs-api)
and saved as JSON.

## Structure

```
data/<brand-slug>/<model>/details.json
```

Each `details.json` is the full API response for that model (specs, color
images, camera samples, etc.). `error.json` files (failed scrapes) are
git-ignored and not committed.

## Status

| Brand  | Slug                | Scraped | Total (GSMArena) | Status      |
|--------|---------------------|--------:|-----------------:|:------------|
| Apple  | `apple-phones-48`   | 146     | 148              | ✅ Complete* |
| Google | `google-phones-107` | 40      | 40               | ✅ Complete  |
| Samsung| `samsung-phones-9`  | 582     | 1457             | ⏳ Partial   |
| Sony   | `sony-phones-7`     | 50      | 163              | ⏳ Partial   |

\* Apple: 146 of 148 — 2 models failed (see `error.json`, not committed).

Samsung and Sony are paused mid-scrape because GSMArena returned HTTP 429
(rate limit). Re-running the scraper resumes incrementally (existing
`details.json` files are skipped).

## Regenerate / resume

From the API repo root:

```bash
pnpm dev                      # start API on :4000
node scraper/scrape-brand.js --delay 3000   # slower rate avoids 429
```

Then commit new `details.json` here:

```bash
cd data
git add -A
git commit -m "data: update <brand> scraped specs"
```
