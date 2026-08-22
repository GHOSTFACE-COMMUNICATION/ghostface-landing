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

**GitHub Pages**, served from `main` at the repo root. Pushing to `main`
rebuilds the site — there is no build step, Pages just serves `index.html`.

The `CNAME` file pins the custom domain to `ghostface.co.nz`. Don't delete
it: Pages rewrites its domain config from that file on every build.

> **Historical note.** A Vercel project (`ghostface-landing`, team
> `ghostfacecommunications`) also served this domain and was the live host
> until the switch to Pages. If the site ever reverts to an old design
> unexpectedly, check which of the two DNS is pointing at before debugging
> the HTML — three near-identical versions of this page existed at one
> point, and the wrong host serving a stale copy looks exactly like a
> caching bug.

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
