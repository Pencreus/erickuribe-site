# erickuribe.com

Static personal site. Plain HTML and CSS — no framework, no build step, no
dependencies, nothing that can rot the way the old Blogger site did.

```
index.html      the whole site, one page
style.css       the CRT phosphor theme
assets/erick.svg  cartoon portrait, reused from the Pencreus boot splash
_headers        security + cache headers (Cloudflare Pages reads this)
robots.txt
sitemap.xml
```

## Editing it

Open `index.html` in any editor. Sections are commented. To add a build, copy
an existing `<article class="build">` block and change the text.

Colours live at the top of `style.css` as CSS variables. Change `--green` and
the whole site follows, including the portrait (it's alpha-masked, not a
coloured image).

## Previewing locally

```bash
python3 -m http.server 8092 --directory ~/Projects/erickuribe-site
```

Then open http://localhost:8092. Must be served over HTTP — opening
`index.html` directly as a `file://` URL will not load the CSS mask.

## Deploying to Cloudflare Pages (free)

**One-time setup:**

1. Push this folder to a GitHub repo.
2. Cloudflare dashboard → Workers & Pages → Create → Pages → Connect to Git.
3. Pick the repo. Framework preset: **None**. Build command: **leave empty**.
   Build output directory: **`/`**.
4. Deploy. You get a `*.pages.dev` URL immediately.
5. Custom domains → add `erickuribe.com` and `www.erickuribe.com`.

After that, every `git push` redeploys automatically.

**Do not touch the MX records.** Mail for this domain routes through Mailgun
(`mxa/mxb.mailgun.org`). Adding a Pages custom domain only rewrites the A /
CNAME records, so mail is unaffected — just don't clear the zone wholesale.

## Note on the current 525

Before this site existed, `erickuribe.com` returned Cloudflare **525 — SSL
handshake failed**, because the old Blogger origin no longer terminated TLS
for the domain. Pointing the domain at Pages replaces that origin entirely,
which resolves the error as a side effect.
