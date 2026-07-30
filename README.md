<img width="1892" height="910" alt="image" src="https://github.com/user-attachments/assets/a2409020-52da-4eea-b25d-bc1a06933e3d" /># YanzDimension — Photography Portfolio

A single-page, dependency-free photography portfolio built with vanilla HTML, CSS and JavaScript. No build step, no framework, no bundler — clone it, open it, deploy it.

**Live Demo:** [https://your-username.github.io/yanzdimension](https://your-username.github.io/yanzdimension) <!-- replace with your GitHub Pages / Netlify / Vercel URL -->

---

## Preview

| Home | Gallery |
|---|---|
| ![Home preview](<img width="1892" height="910" alt="image" src="https://github.com/user-attachments/assets/c98d2afe-7774-402f-a3d3-0ebb7f5635bf" />
 | ![Gallery preview](<img width="1867" height="896" alt="image" src="https://github.com/user-attachments/assets/f9edfa51-7993-4779-9738-46fa69d31ca3" />
) |

| About | Contact |
|---|---|
| ![About preview](<img width="1880" height="902" alt="image" src="https://github.com/user-attachments/assets/5d7a9741-10a8-46b0-a2be-b6384324de36" />
) | ![Contact preview](<img width="1817" height="882" alt="image" src="https://github.com/user-attachments/assets/c37d9bee-171d-43c2-ac36-00ef2a3b8fe7" />
) |

> Screenshots not showing? Add your own images to `docs/screenshots/` using the filenames above (see [Adding Screenshots](#adding-screenshots)).

---

## Overview

YanzDimension is a static, client-rendered portfolio site for a photography brand. Every "page" (Home, About, Galleries, Contact) lives inside a single `index.html` file and is toggled via JavaScript — there is no server-side routing and no page reload, so navigation stays instant while still supporting deep, distinct sections.

The project was built to demonstrate that a polished, animation-heavy portfolio doesn't require a framework: routing, transitions, a lightbox, and interactive hover physics are all implemented in plain, readable JavaScript.

---

## Features

- **SPA-style routing without a framework** — sections are toggled via `data-page` attributes and a lightweight `goToPage()` router; no page reloads, no hash-based history complexity.
- **Custom page-transition system** — a full-screen overlay slides in from the left, swaps the active section, then slides out to the right on every navigation, with a rotating dual-triangle loader for a premium loading feel.
- **Randomized masonry photo grid** — each gallery block is generated at runtime from a shuffled pool of row profiles (column count × row height), so the composition looks intentional but never identical between rows or reloads.
- **Interactive photo hover physics** — cursor position drives a combined `translateX` (parallax pan), `rotate` (subtle tilt), and `scale` (soft zoom) transform on each image, eased with a `cubic-bezier` transition for a fluid, non-linear feel.
- **Custom lightbox** — clicking any photo opens a full-screen viewer with a scale + fade-in entrance animation, keyboard navigation (`←` `→` `Esc`), prev/next controls, and a live counter.
- **Scroll-triggered skill bars** — progress bars on the About page animate via `IntersectionObserver`, firing once the section enters the viewport rather than on page load.
- **Fully responsive** — a single breakpoint (`900px`) collapses the multi-column grids, forms, and navigation into a mobile-friendly layout.
- **Zero dependencies** — no npm install, no bundler, no framework. Two Google Fonts (`Fraunces`, `Manrope`) are the only external assets besides placeholder imagery.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Markup | HTML5 |
| Styling | CSS3 (custom properties, CSS Grid, Flexbox, `clip-path`-free SVG icons) |
| Behavior | Vanilla JavaScript (ES6+, no framework/library) |
| Fonts | [Fraunces](https://fonts.google.com/specimen/Fraunces) (display serif), [Manrope](https://fonts.google.com/specimen/Manrope) (body sans) via Google Fonts CDN |
| Placeholder images | [Picsum Photos](https://picsum.photos) (seeded, swappable — see [Customization](#customization)) |

---

## Project Structure

```
yanzdimension/
├── index.html          # Entire site: markup, CSS, and JS in one file
├── images/              # (create this) local photo assets, once you swap out placeholders
│   ├── about.jpg
│   ├── together.jpg
│   ├── contact.jpg
│   └── gallery/
├── docs/
│   └── screenshots/     # README preview images
└── README.md
```

> The site currently ships as a single `index.html`. The `images/` folder above is a suggested structure for when you replace the placeholder images with your own — see below.

---

## Getting Started

No build tools required.

```bash
git clone https://github.com/your-username/yanzdimension.git
cd yanzdimension
```

Then either:

- **Open directly** — double-click `index.html`, or
- **Serve locally** (recommended, avoids any local file-path quirks):

```bash
# Python 3
python3 -m http.server 8000

# or with Node
npx serve .
```

Visit `http://localhost:8000` in your browser.

---

## Deployment (GitHub Pages)

1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Under **Source**, select the `main` branch and `/ (root)` folder.
4. Save — GitHub will publish the site at `https://your-username.github.io/yanzdimension/`.
5. Update the **Live Demo** link at the top of this README with that URL.

The site works identically on Netlify, Vercel, or any static host — no environment variables or build command needed.

---

## Customization

### Replacing placeholder images

All gallery images are generated at runtime from [Picsum Photos](https://picsum.photos) via a seeded URL, defined in `index.html`:

```js
function imgUrl(seed, w = 700, h = 900) {
  return `https://picsum.photos/seed/${seed}/${w}/${h}`;
}
```

To use your own photos instead:

1. Add your image files to an `images/` folder in the repo.
2. Replace the three fixed placeholder `<img src="...picsum.photos/seed/...">` tags (About photo, "Better Together" photo, Contact photo) with local paths, e.g. `src="images/about.jpg"`.
3. For the dynamically generated gallery grids (Home and Galleries pages), replace the `seeds` array and the body of `imgUrl()` in the `<script>` section with your own file list, e.g.:

```js
const seeds = ['gallery/photo-01.jpg', 'gallery/photo-02.jpg', /* ... */];
function imgUrl(path) { return path; }
```

> Once local files replace the external Picsum URLs, the site no longer depends on any third-party image service at runtime.

### Adding screenshots

Add PNG/JPG captures of each page to `docs/screenshots/` with these filenames so the preview table above renders correctly:

```
docs/screenshots/home.png
docs/screenshots/gallery.png
docs/screenshots/about.png
docs/screenshots/contact.png
```

### Colors, typography & content

- **Color palette** — all colors are defined as CSS custom properties at the top of the `<style>` block (`--bg-page`, `--bg-dark`, `--accent`, etc.). Change these once to re-theme the entire site.
- **Copy** — bio, stats, and gallery labels are plain text inside `index.html`; edit directly.
- **Navigation** — menu items live inside `<nav class="main-nav">`; each link needs a `data-page` attribute matching a `<section class="page" id="page-*">`.

---

## Browser Support

Tested on current versions of Chrome, Firefox, Safari, and Edge. Relies on `IntersectionObserver`, CSS Grid, and CSS custom properties — no polyfills included for legacy browsers (IE11 is not supported).

---

## License

Released under the [MIT License](./LICENSE). Feel free to fork and adapt for your own portfolio.

---

## Author

**YanzDimension**
Photography & Visual Storytelling
[Instagram](#) · [Behance](#) · [Contact](#)
