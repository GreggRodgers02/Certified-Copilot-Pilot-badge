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
| Landing page | `https://greggrodgers02.github.io/Certified-Copilot-Pilot-badge/` |
| Overlay tool | `https://greggrodgers02.github.io/Certified-Copilot-Pilot-badge/overlay.html` |

Use the **image URL** when the agent needs to display or return the badge. Use the
**landing page URL** when adding a public website knowledge source, since crawlers
index HTML pages rather than bare image files.

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
| `index.html` | Landing page: renders the badge, describes it, lists the URLs |
| `overlay.html` | Browser tool to frame a photo with the badge; runs client-side |
| `.nojekyll` | Serves files as-is, skipping Jekyll processing |
| `robots.txt` | Allows crawling; points at the sitemap |
| `sitemap.xml` | Helps search engines discover the page and image |

## Notes

- The direct image URL is served as `image/png` over HTTPS from GitHub's CDN, with
  no auth and no hotlink restrictions.
- Renaming or moving the PNG breaks every reference to it — keep the path stable.
- `raw.githubusercontent.com` also serves the file, but it is meant for source
  access rather than hotlinking and is rate limited; prefer the Pages URL.
