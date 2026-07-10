# Project: Bachelor Trip Site (GitHub Pages)

## What this is
A static site for a 10-man bachelor trip, Sept 21–27, 2026. Two standalone pages, no shared code:

- **`index.html`** — Trip HQ, the groomsmen-facing homepage. Trip mode only: countdown, updates feed, and (once the destination is chosen) the itinerary. Currently shows the "awaiting the call" state.
- **`nm81634cuxhnpb/index.html`** — the candidate dossier (decide board) for the groom + best man ONLY. Passphrase-gated (`zzdeathscopezz`, client-side, cosmetic). Reached only by knowing the URL: `https://arathie.github.io/jaipal-bachelor-trip/nm81634cuxhnpb/`.

## Hard constraints (do not violate)
1. **Secrecy**: groomsmen must not see the candidate options or scores. All candidate data (`TRIPS`, statuses, costs, scores) lives ONLY in the dossier page. `index.html` must never contain candidate data, the passphrase, the slug, or any link/reference to the dossier — no UI elements, no comments, no source strings.
2. **The dossier is permanent — never delete it** (owner decision, July 2026). After the destination is chosen, the unchosen candidates stay in the dossier page at its slug URL, unlinked from the homepage. Obscurity (random slug + passphrase) is the accepted model; the owner knows the repo is public and accepts that someone could dig it up.
3. **No surprises leaked**: never add content about gifts, finale plans, or who pays what. The groom reads this site.
4. **No build step**: two self-contained HTML files deployable by file-upload. Vanilla JS only. No frameworks, no bundlers, no external JS dependencies. Google Fonts is the only external resource.
5. **Design system is fixed** (topo field-map): tokens at the top of each `<style>` block — bone/contour/ink/river/blaze/pine, Big Shoulders Display + Public Sans + IBM Plex Mono. Blaze orange is reserved for anchor-status and active markers only. Don't restyle; extend within the system. Keep the two pages visually consistent.
6. Keep `noindex` meta on both pages. Keep the site mobile-first (most of the crew reads on phones).

## Current state
- Homepage (`index.html`): awaiting-the-call hero, live countdown to `TRIP_START`, groomsmen-safe `UPDATES` feed. `CONFIG.CHOSEN_TRIP` is null.
- Dossier (`nm81634cuxhnpb/index.html`): complete decide board — hero, status tally, filter chips, sort, expandable candidate cards, compare table, passphrase gate (sessionStorage, cosmetic). 12 candidates in `TRIPS` (1 anchor, 5 contenders, 3 developing, 3 backups), current as of July 8, 2026. It also still carries the old single-file trip-mode code (`MODE`/`CHOSEN_TRIP_ID`); leave `MODE: "decide"` forever — the homepage is the trip tracker now.

## Decision-day runbook (when the destination is chosen)
1. Copy the winning trip's object out of the dossier's `TRIPS` array and paste it as `CONFIG.CHOSEN_TRIP` in `index.html`. Only the winner — no other candidate ever enters the homepage.
2. Expand its `build[]` into a real day-by-day with times and addresses as bookings land; add `UPDATES` entries.
3. Leave the dossier page exactly where it is (constraint 2). Optionally note the final call in an update there for posterity.

## Roadmap
1. Trip-mode additions when asked: flights table per person, packing list, payment-status board (names + paid y/n — get explicit OK before publishing anyone's payment status), FAQ, weather widget-free forecast link, map links per stop.
2. Nice-to-haves: print stylesheet for a one-page itinerary; add a countdown favicon.

## Conventions
- Homepage content edits happen in `CONFIG` / `UPDATES`; dossier content edits in its `TRIPS` / `UPDATES` arrays.
- Commit style: short imperative ("Add itinerary day cards").
- After any change, verify on mobile width (~380px) before pushing.
- This remote environment has no `gh` CLI — use the GitHub MCP tools for GitHub operations. GitHub Pages serves from the repo (Settings → Pages, deploy from a branch).
