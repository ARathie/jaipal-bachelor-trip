# Bachelor Trip Site — Sept 21–27, 2026

Static site, two standalone pages, no build step:

- **`index.html`** — Trip HQ. The homepage the crew sees: countdown, updates, and — once the destination is locked — the full itinerary. Shows "awaiting the call" until then.
- **`nm81634cuxhnpb/index.html`** — the candidate dossier: every trip option with status, cost, A/F/S scores, gates, flags, and build outline. For the groom + best man only. Not linked from anywhere; passphrase-gated on top of the unlisted URL.

## Deploy (GitHub Pages)
Settings → Pages → Source: "Deploy from a branch" → pick the branch, folder `/ (root)` → Save.
Site: `https://arathie.github.io/jaipal-bachelor-trip/` (live in ~1 minute). The dossier deploys with it at its own path.

## Privacy model — read this before sharing links
- The dossier gate is **client-side and cosmetic** — it deters casual visitors, it does not secure anything. The repo and both pages are public. Obscurity (random path) + passphrase is the model, by explicit choice.
- Don't put anything on this site you couldn't survive the crew finding.
- `noindex` meta is set on both pages, so search engines are told to ignore them.
- Share the homepage link freely with the crew; the dossier URL goes to the decision team only.

## Editing content
- Homepage: `CONFIG` block and `UPDATES` array in `index.html`.
- Dossier: `TRIPS` and `UPDATES` arrays in `nm81634cuxhnpb/index.html`.
- Decision day: see the runbook in `CLAUDE.md` — the winner gets pasted into the homepage; the dossier stays put.

Edit, commit, Pages redeploys automatically.
