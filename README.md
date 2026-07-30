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
404.html          Not-found page (GitHub Pages serves this automatically)
robots.txt        Crawler rules
sitemap.xml       Search engine sitemap
favicon.svg       Site icon
CNAME             Custom domain binding for GitHub Pages
assets/
  styles.css      All styling, shared by every page
  og-image.png    Social share card (1200×630)
```

## Editing

The header and footer are copied into each page by hand. If you change one,
change it in all five — there's no templating.

Colors, spacing, and type live in the `:root` block at the top of
`assets/styles.css`, with dark-mode overrides right below it. Changing an
accent color there updates every page.

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

## Regenerating the social card

`assets/og-image.png` was rendered from HTML with headless Chromium at
1200×630. To change it, rebuild the source HTML and re-screenshot at that size.
