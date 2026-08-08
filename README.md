# threefoldinteractive.com

The public website for Threefold Interactive LLC, served by GitHub Pages at
<https://threefoldinteractive.com>.

Static HTML and CSS. No build step, no dependencies, no JavaScript — edit a
file, commit, and it's live.

## Layout

```
index.html        Home
games.html        Games (currently: first title in development)
support.html      Support, refunds, data deletion — the app stores link here
privacy.html      Privacy policy — the app stores link here too
terms.html        Terms of service / EULA
404.html          Not-found page (GitHub Pages serves this automatically)
robots.txt        Crawler rules
sitemap.xml       Search engine sitemap
favicon.png       Site icon, 180×180 (also the Apple touch icon)
CNAME             Custom domain binding for GitHub Pages
assets/
  styles.css        All styling, shared by every page
  og-image.png      Social share card (1200×630)
  logo-mark-web.png Header logo, 146×120 — the file the site actually loads
  logo-mark.png     Original full-resolution mark (source, not served)
  logo-full.png     Original full lockup with wordmark (source, not served)
```

## Editing

The header and footer are copied into each page by hand. If you change one,
change it in all six — there's no templating.

Colors, spacing, and type live in the `:root` block at the top of
`assets/styles.css`. Changing an accent color there updates every page.

### The site is dark only

There is no light theme. The logo is a cyan glow drawn for a black
background, so the palette commits to dark rather than carrying a washed-out
light variant. `:root` sets `color-scheme: dark` and there are no
`prefers-color-scheme` blocks.

If you ever add a light theme, note that `--accent` is bright cyan: white
text on it fails contrast, which is why buttons use `--on-accent` (near
black) for their label.

### Logo assets

`logo-mark.png` and `logo-full.png` are the originals as supplied, kept as
the source of truth. They're around 700 KB and 1 MB, far too heavy to serve
on every page, so the site loads the downscaled `logo-mark-web.png` (~16 KB)
instead. If you replace the logo, regenerate the served copies rather than
pointing the pages at the originals.

### Adding a released game

`games.html` has a commented-out card template near the top of the games
section. Copy it, fill in the title, description, and store links, and remove
the "in development" status card.

### Before shipping a game

`privacy.html` opens with a maintainer comment listing what has to be updated
before a first release — the collected-data section, the third-party SDK list,
and the children's-privacy section. The policy as written is accurate only
while no games are published. It also needs to match the Data Safety form on
Google Play and the App Privacy answers on the App Store.

## Local preview

```sh
python3 -m http.server 8000
```

Then open <http://localhost:8000>. Use a server rather than opening the files
directly — the pages use root-relative paths (`/assets/styles.css`), which
don't resolve over `file://`.

## Regenerating images

`assets/og-image.png`, `assets/logo-mark-web.png`, and `favicon.png` were all
rendered from HTML with headless Chromium and then cropped to size.

Two gotchas if you redo this with the same approach:

- Headless Chromium clamps its viewport to a 500px minimum width and loses
  about 87px of height to chrome, so `--window-size` is not the size you get.
  Render taller than you need and crop the padding off.
- Pass `--virtual-time-budget` so the screenshot waits for images to decode;
  without it you can capture a half-laid-out page.
