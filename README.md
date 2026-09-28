# offlyne-site
# Offlyne — marketing site

Single-page site for Offlyne. Static HTML, no build step, no dependencies.

**Real people, real places, IRL.**

---

## Publishing to GitHub Pages

1. Create a repository on GitHub (public, or private on a paid plan — Pages needs one of those).
2. Push these files to the repository root:

   ```bash
   git init
   git add .
   git commit -m "Offlyne site"
   git branch -M main
   git remote add origin https://github.com/<you>/<repo>.git
   git push -u origin main
   ```

3. In the repo: **Settings → Pages → Build and deployment**
   - Source: **Deploy from a branch**
   - Branch: **main**, folder: **/ (root)**
4. Wait a minute, then open the URL Pages shows you.

Every path in `index.html` is relative, so the site works both at a user site
root (`you.github.io`) and at a project subpath (`you.github.io/repo-name/`)
without changes.

### Custom domain

Add a file called `CNAME` at the repo root containing just your domain:

```
offlyne.com
```

Then point a `CNAME` DNS record at `<you>.github.io`, and tick
**Enforce HTTPS** in Settings → Pages.

---

## Files

```
index.html        The whole page — markup plus all CSS inline
assets/           Images and icons
.nojekyll         Stops GitHub running Jekyll over the files
```

There is no CSS file to link. Everything is in one `<style>` block in the
`<head>`, which is why the page renders the same served from GitHub, opened
off disk, or embedded in a preview pane.

### Images

The photos are resized and re-encoded for the sizes they actually display at
(roughly 2× for retina) — 1.7 MB down to 730 KB across the set. If you swap
one in, match the existing width so the page weight stays put:

| File                   | Width  | Used for            |
| ---------------------- | ------ | ------------------- |
| `group-of-friends.jpg` | 1800px | Hero background     |
| `sofia.jpg`            | 760px  | Profile screen      |
| everything else        | 420px  | Grid tiles, avatars |

### Icons

`favicon-coral-32.png`, `apple-touch-icon.png` and `offlyne-app-icon-192.png`
are generated from `offlyne-pin-coral.png` on a black field — placeholders so
nothing 404s. Replace them with the real app icon when you have it; keep the
filenames and no markup changes are needed.

---

## Editing

The page is hand-written HTML in source order: hero → the idea → how it works
→ the experience → the app → what it does → your call → waitlist → close.

Design tokens sit at the top of the `<style>` block as CSS custom properties
(`--coral`, `--paper`, `--black`), matching `design-tokens.css` in the Offlyne
design system.

App screens in "Less scrolling / More hello" are built from HTML and CSS
rather than screenshots, so they stay sharp at any density and can be edited
as markup.

---

## Waitlist form

The form in the **Get on the Waitlist Now** section is markup only — it posts
nowhere. GitHub Pages serves static files and cannot process a submission, so
it needs a third-party endpoint. Point the `<form>` at one, e.g.:

```html
<form class="getin-form" action="https://formspree.io/f/YOUR_ID" method="post">
```

Formspree, Buttondown, Mailchimp and Tally all work this way. Until then the
field accepts input and discards it.
