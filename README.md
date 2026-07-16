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
| Samsung| `samsung-phones-9`  | 1455    | 1457             | ⏳ Partial   |
| Sony   | `sony-phones-7`     | 163     | 163              | ✅ Complete  |
| Nokia  | `nokia-phones-1`    | 596     | 596              | ✅ Complete  |
| Xiaomi | `xiaomi-phones-80`  | 528     | 527              | ✅ Complete  |
| Vivo   | `vivo-phones-98`    | 602     | 600              | ✅ Complete  |
| OnePlus| `oneplus-phones-95` | 113     | 112              | ✅ Complete  |

\* Apple: 146 of 148 — 2 models unaccounted for (not yet scraped).

Samsung is paused mid-scrape because GSMArena returned HTTP 429
(rate limit). Re-running the scraper resumes incrementally (existing
`details.json` files are skipped). Currently 18 Samsung models failed with
`error.json` (git-ignored, not committed) and will be retried on resume.

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
