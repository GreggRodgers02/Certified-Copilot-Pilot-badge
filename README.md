# Certified Copilot Pilot Badge

Hosts the "Certified Copilot Pilot" badge image on GitHub Pages, giving it a stable
public HTTPS URL that can be used as an external image source in a Copilot agent.

## The image

`certified-copilot-pilot-badge.png` — 750 × 750 PNG, 8-bit RGBA. A circular badge
**frame**: a navy ring lettered CERTIFIED COPILOT PILOT, gold aviator wings and the
Copilot mark at the bottom, and a **fully transparent center** so it can be layered
over a profile photo or avatar.

## URLs

Once Pages is enabled (see below):

| Purpose | URL |
| --- | --- |
| Direct image | `https://greggrodgers02.github.io/Certified-Copilot-Pilot-badge/certified-copilot-pilot-badge.png` |
| Badge tool (share this) | `https://greggrodgers02.github.io/Certified-Copilot-Pilot-badge/` |

Share the **tool URL** with teammates — they upload a photo and download the
finished badge, with nothing to install and nothing uploaded anywhere. Use the
**image URL** when an agent needs to display or return the badge, and the same tool
URL when adding a public website knowledge source, since crawlers index HTML pages
rather than bare image files.

## Enabling GitHub Pages

One-time, in the GitHub web UI — it cannot be turned on from a commit:

1. **Settings → Pages**
2. **Source:** Deploy from a branch
3. **Branch:** `main`, folder `/ (root)` → **Save**

The site publishes within a couple of minutes. The repository must be public for
Pages on the GitHub Free plan.

## Files

| File | Purpose |
| --- | --- |
| `certified-copilot-pilot-badge.png` | The badge image |
| `index.html` | The badge tool: upload a photo, position it, download it. Also documents the badge and its URLs |
| `overlay.html` | Redirect to the home page, where the tool now lives |
| `.nojekyll` | Serves files as-is, skipping Jekyll processing |
| `robots.txt` | Allows crawling; points at the sitemap |
| `sitemap.xml` | Helps search engines discover the page and image |

## Notes

- The direct image URL is served as `image/png` over HTTPS from GitHub's CDN, with
  no auth and no hotlink restrictions.
- Renaming or moving the PNG breaks every reference to it — keep the path stable.
- `raw.githubusercontent.com` also serves the file, but it is meant for source
  access rather than hotlinking and is rate limited; prefer the Pages URL.
