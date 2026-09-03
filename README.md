# Creaso Camps LLC — website

A single-page static site. No build step, no framework: `index.html` holds the markup, CSS, and JavaScript; `assets/` holds the logo, icons, and the share image.

```
index.html      the site (everything inline)
404.html        styled not-found page
CNAME           tells GitHub Pages the custom domain (creasocamps.com)
robots.txt      allows crawling, points at the sitemap
sitemap.xml
.nojekyll       stops GitHub from running Jekyll on the folder
assets/
  logo.png / logo.webp      the badge
  favicon.png               browser-tab icon
  apple-touch-icon.png      home-screen icon on iPhone
  og.jpg                    the image shown when the link is shared (1200×630)
```

## Put it on GitHub Pages

1. Create a new repository (for example `creasocamps-site`), then upload **the contents of this folder** to the root of the `main` branch (`index.html` must sit at the top level, not inside a subfolder).
2. In the repository go to **Settings → Pages**. Under *Build and deployment* pick **Deploy from a branch**, branch `main`, folder `/ (root)`. Save.
3. Still on the Pages screen, under *Custom domain* enter `creasocamps.com` and save. GitHub will look for the `CNAME` file, which is already here.
4. Once DNS is in place (next section) tick **Enforce HTTPS**. The certificate usually appears within an hour.

## Point the domain at GitHub instead of Google Sites

At the registrar where `creasocamps.com` is managed (the DNS records screen):

1. Delete the old records that send the domain to Google Sites (an `A` or `CNAME` record pointing at `ghs.googlehosted.com`, and the `www` CNAME if it points there).
2. Add four `A` records for the bare domain (`@`):

   ```
   185.199.108.153
   185.199.109.153
   185.199.110.153
   185.199.111.153
   ```

3. Add a `CNAME` record for `www` pointing at `kirkcreason-dev.github.io`.
4. In Google Sites, open the old site → Settings → Custom domains and remove `creasocamps.com`, so the two hosts stop competing for it.

DNS changes usually take 10–60 minutes to settle. If GitHub's *Custom domain* box shows a DNS check error, wait and press *Check again*.

## Editing the content

Everything is plain HTML in `index.html`, grouped by section with a comment header (`<!-- HERO -->`, `<!-- SERVICES -->`, …).

- **Contact details** (office address and hours) appear in the mobile menu, the Contact section, and the footer — search the file for `3401 Quebec` to find every spot. The phone number and the owner's email are deliberately not on the page.
- **Videos** live in the `<div class="vgrid">` block. Each tile is one line: `data-id` is the YouTube video id (the part after `v=` in the video's URL) and `data-title` is the caption. Add, remove, or reorder lines freely.
- **Donate link** is the Stripe payment link. It appears in the nav, the Foundation section, and the footer — search for `buy.stripe.com`.
- **Services** are the three panels under `<!-- SERVICES -->`; each `<li>` is one service.
- **Photos**: drop images into `assets/` and reference them with `<img src="assets/your-photo.jpg" alt="...">`. Keep them under ~400 KB each for fast loading.

The contact form opens the visitor's email app with a pre-filled message (no server needed). Foundation and volunteering messages are addressed to the Creaso Cares inbox; everything else goes to the office inbox, which is assembled in the script at click time rather than written out on the page.
