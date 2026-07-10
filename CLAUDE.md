# Project: Bachelor Trip Site (GitHub Pages)

## What this is
A static site for a 10-man bachelor trip, Sept 21–27, 2026. Two standalone pages, no shared code:

- **`index.html`** — the groomsmen-facing homepage: countdown, updates feed, and (once the destination is chosen) the itinerary. Currently shows the "destination being decided" state.
- **`destination-choices/index.html`** — the destination-options page for the groom + best man ONLY. Passphrase-gated (`zzdeathscopezz`, client-side, cosmetic). Carousel UI: one option open in a big viewer (photos, day/night itinerary, trade-offs), all twelve in a strip pinned to the bottom. Reached only by knowing the URL: `https://arathie.github.io/jaipal-bachelor-trip/destination-choices/`.

## Hard constraints (do not violate)
1. **Secrecy**: groomsmen must not see the candidate options or scores. All candidate data (`TRIPS`, statuses, costs, scores) lives ONLY in the options page. `index.html` must never contain candidate data, the passphrase, the `destination-choices` path, or any link/reference to it — no UI elements, no comments, no source strings.
2. **The options page is permanent — never delete it** (owner decision, July 2026). After the destination is chosen, the unchosen options stay there at the same URL, unlinked from the homepage. The owner picked the slug himself, knows the repo is public, and accepts that someone could dig it up.
3. **No surprises leaked**: never add content about gifts, finale plans, or who pays what. The groom reads both pages. The budget cap is also private — never show it on either page.
4. **Tone is plain and unpretentious** (owner request, July 2026): no military/ops/spy metaphors ("HQ", "dossier", "classified", "ops", "riders", "the call"), no self-important framing of the groom/best man decision process. Plain enthusiasm about real activities is fine; theatrical copy is not.
5. **No build step**: two self-contained HTML files plus static images under `destination-choices/img/`. Vanilla JS only. No frameworks, no bundlers, no external JS. Google Fonts is the only external resource — photos are committed to the repo, never hotlinked.
6. **Design system is fixed** (topo field-map): tokens at the top of each `<style>` block — bone/contour/ink/river/blaze/pine, Big Shoulders Display + Public Sans + IBM Plex Mono. Blaze orange is reserved for anchor-status and active markers only. Don't restyle; extend within the system. Keep the two pages visually consistent.
7. Keep `noindex` meta on both pages. Keep the site mobile-first (~380px is the check width).
8. **Images must be freely licensed** (public repo): Wikimedia Commons / Unsplash / Pexels / public domain only, with attribution tracked in `destination-choices/img/CREDITS.md` and shown in the photo caption line.

## Current state
- Homepage (`index.html`): plain hero, live countdown to `TRIP_START`, groomsmen-safe `UPDATES` feed. `CONFIG.CHOSEN_TRIP` is null.
- Options page (`destination-choices/index.html`): reflects the July 2026 pivot to the villa formula (staffed villa + private chef + beach drinks + one private boat day; optional modules: jet skis, fishing, ATVs, snorkeling). Passphrase gate → hero with status tally + **Archive toggle** + compare-table toggle → viewer (selected option: photos with captions/credits, score gauges, why-it's-listed, day/night itinerary, requirements, flags, timing) → sticky bottom strip (tap to open, ◀ ▶ and arrow keys, URL hash deep-links; a hash pointing at an archived option auto-enables the archive).
- Data: 20 entries in `TRIPS` — the v4 board (9 CONTENDER villa options + 2 MONITOR) followed by the 9 ARCHIVED adventure-era options (`status:"ARCHIVED", archived:true`), which are hidden from strip/compare unless the Archive toggle is on. **The archived entries are permanent** (owner decision) — same rule as constraint 2. Scores are keyed per era: villa board `scores:{C,F,W}` (Comfort/Fun/Water), archived `scores:{A,F,S}` (Adventure/Fun/Skill); gauges/compare render labels from the keys. Other fields per trip: `id, name, region, status, cost:[lo,hi], flight, wow, second, gates[], flags[], fit, days:[{d, day, night}], photos:[{src, thumb, alt, caption, credit}]`.
- Planning source docs (the brief/shortlist) contain groom-secret logistics (rigged finale, superlatives, who-pays). **Never copy those onto the site** — constraint 3 applies when transcribing itineraries.

## Decision-day runbook (when the destination is chosen)
1. Copy the winning trip's object out of the options page's `TRIPS` array and paste it as `CONFIG.CHOSEN_TRIP` in `index.html`. Only the winner — no other option ever enters the homepage. Strip the `photos` array (or copy the image files out of `destination-choices/img/` into a homepage-safe location first — homepage must not reference the `destination-choices` path). Optionally add `nameHTML` with explicit `<br>` breaks for the hero heading; it falls back to `name` wrapping naturally.
2. Refine its `days[]` into the real schedule with times and addresses as bookings land; add `UPDATES` entries on the homepage.
3. Leave the options page exactly where it is (constraint 2).

## Roadmap
1. Trip-mode additions when asked: flights table per person, packing list, payment-status board (names + paid y/n — get explicit OK before publishing anyone's payment status), FAQ, weather forecast link, map links per stop.
2. Nice-to-haves: print stylesheet for a one-page itinerary; countdown favicon.

## Conventions
- Homepage content edits happen in `CONFIG` / `UPDATES`; options-page content edits in its `TRIPS` array.
- Commit style: short imperative ("Add itinerary day cards").
- After any change, verify on mobile width (~380px) before pushing.
- This remote environment has no `gh` CLI — use the GitHub MCP tools for GitHub operations. GitHub Pages serves from the repo (Settings → Pages, deploy from a branch).
