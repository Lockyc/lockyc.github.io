# lockyc.github.io — agent orientation

The link-in-bio page served at **lockyc.com**. A fork of [LittleLink](https://littlelink.io)
**v2.5.0** (version marker: the comment at the top of `index.html`). Static HTML + CSS — no build,
no tests, no dependencies, no JavaScript. `README.md` carries the human tour and the layout table;
this file carries what will bite an agent.

## No version, no releases — by design

Prose and markup only. There is no version file, no tag, and no release cadence: nothing here is
consumed by anything, so there is nothing to pin. Don't add semver, a `justfile`, or a release
workflow. It is deliberately absent from the Mycelium graph too (it is listed in the homelab
overlay's `ignore`, so it does not scan as an orphan needing a `mycelium.toml`).

## Load-bearing: `main` is the live site — a commit is a deploy

**GitHub Pages serves the `main` branch root at `lockyc.com` directly. There is no workflow, no CI,
and no gate** — `.github/` does not exist, and that is not an omission to fix. Anything committed
and pushed to `main` is public at `lockyc.com` within about a minute.

This is the footgun, because the wrong move looks completely ordinary: the usual habits — commit
freely as you go, `git add -A`, land a work-in-progress and tidy it after — are all safe in a repo
whose trunk is not a deploy target, and all publish here. Two consequences:

- **Never commit speculatively.** There is no "I'll fix it in the next commit" — the broken state
  is live in between.
- **Keep scratch out of the tree.** `.gitignore` excludes `docs/superpowers/`, `.superpowers/`, and
  `.claude/worktrees/` precisely because a swept-up plan file would not merely be committed, it
  would be *published*.

To verify a change, open `index.html` locally (`open index.html`) or serve the dir over HTTP —
never by pushing.

## The fork boundary

`index.html` is ours; everything else is vendored LittleLink.

- **`index.html`** — the only file carrying anything personal: metadata, avatar, heading, bio, and
  the link buttons.
- **`css/`, `images/icons/`, `fonts/`** — upstream LittleLink assets, taken as-is. `css/brands.css`
  is the intended extension point (add a brand style); the icon set is the other (add a 24×24 SVG).
  Don't reformat or prune these — keeping them recognisably upstream is what makes a future
  LittleLink version bump a readable diff rather than a merge.

## Known gap — the template's metadata is still on the live site

`index.html:18-19` still carry LittleLink's own placeholder metadata: `description` is the bare URL
`https://littlelink.io`, and `author` is the template's author. Those two strings are what search
results and link/social previews render for lockyc.com. The rest of the page (`<title>`, avatar,
heading, bio) is correctly personalised — only these two were missed at fork time.

**Left deliberately, not overlooked: this needs the owner, not an agent.** The description is
editorial voice, and since `main` is the live site any edit publishes immediately — so it is the
owner's call to make and to word. Don't invent a description and ship it.
