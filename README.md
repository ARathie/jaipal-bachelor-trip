# Bachelor Trip Site — Sept 21–27, 2026

Static site, two standalone pages, no build step:

- **`index.html`** — the homepage the group sees: countdown, updates, and — once the destination is booked — the full plan.
- **`destination-choices/index.html`** — the destination-options page for the decision: the current shortlist with photos, day/night outlines, costs, scores, and trade-offs, in a carousel layout, plus the earlier archived list behind an Archive toggle. Passphrase-gated on top of an unlisted URL; not linked from anywhere.

## Deploy (GitHub Pages)
Settings → Pages → Source: "Deploy from a branch" → branch `claude/bachelor-trip-website-5nm5m3` (the default branch), folder `/ (root)` → Save. Not yet enabled as of July 10, 2026.
Site: `https://arathie.github.io/jaipal-bachelor-trip/` (live in ~1 minute). The options page deploys with it at its own path.

## Privacy model — read this before sharing links
- The options-page gate is **client-side and cosmetic** — it deters casual visitors, it does not secure anything. The repo and both pages are public. Unlisted path + passphrase is the model, by explicit choice.
- Don't put anything on this site you couldn't survive the group finding.
- `noindex` meta is set on both pages.
- Share the homepage link freely with the group; the options URL stays with the decision team.

## Editing content
- Homepage: `CONFIG` block and `UPDATES` array in `index.html`.
- Options: the `TRIPS` array in `destination-choices/index.html`. Photos live in `destination-choices/img/` (freely licensed only; attributions in `img/CREDITS.md`).
- Decision day: see the runbook in `CLAUDE.md` — the winner gets pasted into the homepage; the options page stays put.

Edit, commit, Pages redeploys automatically.
