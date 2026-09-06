# leaguetonight.com

Static waitlist site for League Tonight, hosted on GitHub Pages. No build step: edit the HTML and push to `main`.

## Files

- `index.html` — the landing page (hero with the sample episode, rundown, sample lines, cast, pricing, FAQ, waitlist form)
- `privacy.html`, `terms.html` — policy pages (also the URLs to give OAuth developer consoles later)
- `style.css`, `favicon.svg`, `assets/` (sample episode at 720p, poster, cast crops, social image)
- `CNAME` — the custom domain

## One-time setup

1. **Formspree.** Create a free form at formspree.io, copy its id, and replace `YOUR_FORM_ID` in `index.html`. Until then the form falls back to opening an email to hello@leaguetonight.com, so nothing is broken in the meantime.
2. **Email.** Set up forwarding for `hello@leaguetonight.com` (Namecheap: Domain List → Manage → Redirect Email) to the inbox you read. The policy pages and the footer point there.
3. **DNS at Namecheap** (Advanced DNS):
   - `A` records for host `@` → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - `CNAME` record for host `www` → `zooksey.github.io`
   - remove the parking-page records Namecheap adds by default
4. **GitHub Pages.** Repository → Settings → Pages: source `main` / root, custom domain `leaguetonight.com`, then tick *Enforce HTTPS* once the certificate is issued (up to an hour after DNS resolves).

## Replacing the sample episode

`assets/sample-episode.mp4` is a 720p, 9 MB copy of a real episode. Make the next one with:

```
ffmpeg -i final.mp4 -vf scale=720:1280 -c:v libx264 -preset slow -crf 27 -pix_fmt yuv420p -movflags +faststart -c:a aac -b:a 96k assets/sample-episode.mp4
ffmpeg -ss <seconds> -i final.mp4 -frames:v 1 -vf scale=720:-1 -q:v 3 assets/poster.jpg
```
