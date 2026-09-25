# ghostface-landing

Coming-soon landing page for **GHOSTFACE** — served at
[ghostface.co.nz](https://ghostface.co.nz).

A single self-contained `index.html`: no build step, no dependencies, no
framework. Fonts come from Google Fonts; the coin artwork is inlined as
base64, so the page has no other external requests.

## What's on the page

- A scratch-to-reveal foil overlay ("COMING SOON") drawn on a `<canvas>` —
  clears itself once ~45% is scratched away.
- Underneath: the app's radial menu, ported to the web — a spinning coin
  with tap-to-kick physics, hold-to-brake, an edge-band flash when the coin
  is edge-on, and motion blur that crossfades in at speed. Tapping the coin
  toggles six orbiting nav nodes.
- Geometry and interaction constants deliberately mirror the mobile app
  (`app/(tabs)/index.tsx` in the main repo) so the two stay visually in step.

## Deploying

**Vercel** — project `ghostface-landing`, team `ghostfacecommunications`.
The domain's A records (`216.150.16.1`, `216.150.1.1`) point at Vercel.

⚠️ **Merging to `main` does NOT deploy** (verified 24–25 Sep 2026: merged
pages stayed 404 for 5+ minutes while `server: Vercel` served a copy ~21 h
old). The Vercel project's Git connection most likely still points at the
repo that existed before it was recreated under the organisation — the same
failure Railway had. Until the Git connection is re-linked in the Vercel
dashboard, deploy by hand from a CLEAN export of `main` (never the working
folder — it holds untracked `index.html.bak-*` files that would go public):

```sh
D=$(mktemp -d) && git archive main | tar -x -C "$D" \
  && mkdir -p "$D/.vercel" && cp .vercel/project.json "$D/.vercel/" \
  && (cd "$D" && npx vercel deploy --prod --yes)
```

Then verify from outside, e.g. `curl -sI https://ghostface.co.nz/privacy`.

GitHub Pages is **not** configured on this repo (the API returns 404); an
older version of this README said it was. The `CNAME` file is left over
from that setup and is harmless.

## Local development

Open `index.html` in a browser. That's it.

For a local server (needed if you add anything that fetches):

```sh
python3 -m http.server 8000
```

## Notes

- `.env.local` and `.vercel/` are gitignored. The page itself needs no
  environment variables — it's fully static.
- This was split out of the `Secure-Ghost-Chat` monorepo (where it lived at
  `artifacts/site/`) so that app pushes can never trigger a deploy of the
  public site.
