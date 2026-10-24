# lockyc.github.io

The link-in-bio page served at **[lockyc.com](https://lockyc.com)** — a single static
`index.html` listing where to find me, with no build step, no dependencies, and no JavaScript.

A fork of **[LittleLink](https://littlelink.io) v2.5.0** (the version marker is the comment at the
top of `index.html`). LittleLink supplies the button/brand CSS and the icon set; everything
personal to this site lives in `index.html`, plus the avatar (`images/avatar.webp`) and `CNAME`.

## Deployment — pushing to `main` publishes the live site

**This repo has no CI and no gate. A push to `main` is a deploy**: GitHub Pages builds the branch
root and serves it at `lockyc.com` (custom domain via `CNAME`, HTTPS enforced). There is no staging
step and no way to preview a change from the repo — what lands on `main` is what the world sees,
within about a minute.

To preview locally, open `index.html` in a browser directly (`open index.html`), or serve the
directory over HTTP if you want paths to resolve exactly as they do in production:

```sh
python3 -m http.server 8000   # then visit http://localhost:8000
```

## Layout

| Path | What it is |
| --- | --- |
| `index.html` | The whole site — metadata, avatar, heading, bio, and one `<a class="button …">` per link. |
| `CNAME` | The custom domain (`lockyc.com`). Deleting it reverts the site to `lockyc.github.io`. |
| `css/brands.css` | LittleLink's per-brand button styles. Add your own brands here. |
| `css/skeleton-{auto,light,dark}.css` | The three themes. `index.html` links `skeleton-auto.css` — it follows the visitor's OS setting. |
| `css/normalize.css` | Cross-browser style reset. |
| `images/icons/` | The LittleLink icon set (24×24 SVG). |
| `fonts/` | Self-hosted Open Sans — no third-party font request at page load. |

## Editing

**Adding a link** — copy an existing `<a>` in `index.html`, then set three things: `href` (the
target), `button-<brand>` (the style, from `css/brands.css`), and the icon `src` (from
`images/icons/`). If the brand you want has no style yet, add one to `css/brands.css` and, if
needed, a 24×24 SVG to `images/icons/`.

**Changing the look** — swap the `skeleton-auto.css` link for `skeleton-light.css` or
`skeleton-dark.css` to pin a theme instead of following the visitor's OS.

Upstream carries the fuller guide: [sethcottle/littlelink](https://github.com/sethcottle/littlelink).
