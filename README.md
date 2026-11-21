# borealdream-media

Static media host for the BorealDream Social Calendar app, deployed on
Cloudflare Workers (static assets, same pattern as borealdream-home).

Everything lives at the repo root, which is the site root:

- `video-*.mp4` — 720×1280 preview encodes (H.264 CRF 28, faststart) of
  the 12 social videos V1–V12. File names match the master files in
  `~/workspace/user/files/social-videos/` so the calendar app maps
  master → preview by name. Masters are NOT in this repo.
- `video-*.jpg` — poster frame (1s) per video, same base name.
- `pin-01.jpg` … `pin-07.jpg` — Pinterest pin images.
- `_headers` — long-lived immutable caching for media + CORS `*`.
  Cloudflare static assets answer HTTP range requests, so the app's
  video player starts fast and can seek.
- `wrangler.jsonc` — Worker name `borealdream-media`, assets = repo root.

Live URL after deploy: https://borealdream-media.inexproject.workers.dev/
