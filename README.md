# Personal Academic Website

A minimal, dark-themed academic personal website. Pure HTML/CSS/JS — no frameworks, no build tools.

## Structure

```
site/
├── index.html          ← Main page (hero + canvas + all sections)
├── publications.html   ← Full publication list
├── projects.html       ← Projects & lab work
├── cv.html             ← Curriculum vitae
├── blog.html           ← Notes & blog index
├── style.css           ← Shared styles (colors, nav, footer, layout)
├── main.js             ← Shared scroll-reveal animation
└── README.md           ← This file
```

## Quick Start (Local)

No build step needed. Just open the files:

```bash
# Option 1: just open in browser
open index.html

# Option 2: local dev server (better for testing links between pages)
# If you have Python installed:
python3 -m http.server 8000
# Then go to http://localhost:8000

# Or with Node:
npx serve .
```

## How to Customize

### Colors
All colors are CSS variables in `style.css` (and duplicated in `index.html` for the standalone hero page). Change them in one place:

```css
:root {
  --bg: #1c1b22;        /* Main background */
  --surface: #24232b;   /* Card backgrounds */
  --text: #e0ddd6;      /* Primary text */
  --soft: #b5b0a6;      /* Secondary text */
  --dim: #837e74;        /* Muted text */
  --accent: #8bb8cc;     /* Primary accent (blue) */
  --accent2: #cc9b8b;    /* Secondary accent (warm) */
  --border: #35343d;     /* Borders */
}
```

> **Important**: `index.html` has its own `<style>` block with the same variables.
> If you change colors in `style.css`, update them in `index.html` too.
> (Or refactor index.html to use the shared stylesheet — see TODO below.)

### Fonts
Currently using Google Fonts (loaded via CDN in each HTML file):
- **Fraunces** — display/headings (serif)
- **JetBrains Mono** — labels, dates, tags (mono)
- **Outfit** — body text (sans-serif)

To change fonts: update the `<link>` tag in each HTML file and the `--serif`, `--mono`, `--sans` variables.

### Canvas Background
The interactive wave animation lives in `index.html` inside a `<script>` tag at the bottom. Key things to tweak:
- **Colors**: search for the RGB values in the `frame()` function (~line with `d[idx]`)
- **Speed**: `t += 0.008` controls animation speed
- **Number of sources**: the `srcs` array
- **Mouse follow strength**: `srcs[2].x += (mx - srcs[2].x) * 0.008` — higher = faster follow

### Adding a Blog Post
1. Create a new file like `posts/my-post.html`
2. Copy the structure from any subpage (nav + page-header + section + footer)
3. Add a link to it in `blog.html`

### Adding a Publication
Edit `publications.html` — copy a `.pub-item` block and fill in your data.

## Deploy to GitHub Pages

### First time setup

```bash
# 1. Create a GitHub repo
# Go to github.com → New Repository
# Name it: yourusername.github.io (for user site)
# Or any name (for project site)

# 2. Initialize git in this folder
cd site
git init
git add .
git commit -m "Initial commit"

# 3. Push to GitHub
git remote add origin https://github.com/yourusername/yourusername.github.io.git
git branch -M main
git push -u origin main

# 4. Enable Pages
# Go to repo Settings → Pages → Source: Deploy from branch → main → / (root)
# Wait ~1 min → your site is live at https://yourusername.github.io
```

### Updating the site

```bash
# After making changes:
git add .
git commit -m "Update publications"
git push
# Changes go live in ~1 min
```

### Custom domain (optional)

1. Buy a domain (~$10/year) from Namecheap, Cloudflare, or Porkbun
2. In your repo: Settings → Pages → Custom domain → enter your domain
3. At your domain registrar, add DNS records:
   - **A records** pointing to GitHub's IPs:
     ```
     185.199.108.153
     185.199.109.153
     185.199.110.153
     185.199.111.153
     ```
   - **CNAME**: `www` → `yourusername.github.io`
4. Check "Enforce HTTPS" in GitHub Pages settings
5. Wait ~30 min for DNS propagation

## TODO (things to improve later)

- [ ] Refactor `index.html` to use shared `style.css` (currently has inline styles)
- [ ] Add actual content (bio, publications, project descriptions)
- [ ] Add your photo
- [ ] Make the pub filter buttons actually work (add JS)
- [ ] Add individual blog post template
- [ ] Add a `favicon.ico`
- [ ] Consider adding a sitemap.xml for SEO
- [ ] Add Open Graph meta tags for nice link previews
