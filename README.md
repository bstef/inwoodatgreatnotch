# Inwood at Great Notch — Community Website

Static HTML website for **Inwood at Great Notch**, a townhouse and apartment co-op community located at 181 Long Hill Road, Little Falls, NJ 07424.

---

## File Structure

```
/
├── inwood-at-great-notch.html   # Main single-page site
├── gallery.html                 # Full photo gallery page
└── README.md                    # This file
```

No build tools, bundlers, or dependencies. Both pages are self-contained HTML files — drop them into any static hosting environment and they work immediately.

---

## Pages

### `inwood-at-great-notch.html` — Main Site

Single-page layout with smooth-scroll navigation. Sections in order:

| Section | ID | Description |
|---|---|---|
| Hero | `#hero` | Full-screen intro with CTA buttons |
| About | `#about` | Community overview and feature list |
| Amenities | `#amenities` | 6-card grid (pool, tennis, basketball, grounds, management, playground) |
| Gallery Preview | `#gallery-preview` | 6-photo teaser linking to full gallery |
| Location | `#location` | Commute cards + Google Maps embed |
| Residents | `#residents` | Shareholder resources and CP Management portal links |
| Contact | `#contact` | Address, neighborhood context, property management info |

### `gallery.html` — Photo Gallery

Full gallery with all 20 community photos sourced from the original site.

**Features:**
- Category filter bar (All, Entrance, Grounds, Pool, Courts, Living, Playground)
- Masonry 3-column grid (responsive: 2-col tablet, 1-col mobile)
- Lightbox viewer with prev/next navigation, thumbnail strip, and photo counter
- Keyboard navigation: `←` `→` to browse, `Esc` to close
- Touch/swipe support on mobile

---

## External Dependencies

All loaded via CDN — no npm, no build step.

| Resource | Purpose | CDN |
|---|---|---|
| Playfair Display | Display/headline typeface | Google Fonts |
| Inter | Body and UI typeface | Google Fonts |
| Google Maps Embed | Location iframe in main site | Google |

Photos are hotlinked directly from `http://www.inwoodatgreatnotch.com/img-gallery/`. If the original server is decommissioned, download the images and update the `src` paths accordingly.

---

## Key External Links

| Link | URL |
|---|---|
| Resident Portal | https://portal.cp-management.com/public |
| CP Management | https://www.cp-management.com/ |
| Current Notices | http://www.inwoodatgreatnotch.com/shareHolders/notices.shtml |
| Meeting Minutes | http://www.inwoodatgreatnotch.com/shareHolders/minutes.shtml |
| Inside Inwood | http://www.inwoodatgreatnotch.com/shareHolders/inside.shtml |
| Shareholder Forms | http://www.inwoodatgreatnotch.com/shareHolders/forms.shtml |
| Board Members | http://www.inwoodatgreatnotch.com/boardMembers/boardMembers.shtml |
| Contact Form | http://www.inwoodatgreatnotch.com/cgi-bin/contact.cgi?page=inquires |

---

## Design System

All colors are defined as CSS custom properties on `:root` in both files.

| Token | Hex | Usage |
|---|---|---|
| `--forest` | `#1E3A2F` | Primary dark green — nav, hero, section backgrounds |
| `--forest-mid` | `#2D5445` | Hover states |
| `--forest-light` | `#3B6B57` | Accents and dot markers |
| `--gold` | `#C8A96E` | Primary accent — eyebrows, icons, CTAs |
| `--gold-light` | `#E2C99A` | Lighter accent — secondary text on dark backgrounds |
| `--cream` | `#F5F2EE` | Page background |
| `--sage` | `#E8EDE9` | Section backgrounds, hover fills |
| `--sage-mid` | `#D0DAD2` | Borders, dividers |
| `--slate` | `#4A5568` | Body text |
| `--slate-light` | `#718096` | Secondary/muted text |

**Typefaces:**
- Headlines: `Playfair Display` (400 regular, 400 italic, 600 semibold)
- Body/UI: `Inter` (300 light, 400 regular, 500 medium, 600 semibold)

---

## Deployment

### Cloudflare Pages (recommended)

1. Push both HTML files (and this README) to a GitHub repository.
2. In the Cloudflare dashboard, go to **Workers & Pages → Create → Pages → Connect to Git**.
3. Select the repo. Build settings:
   - **Framework preset:** None
   - **Build command:** *(leave blank)*
   - **Build output directory:** `/` (or the subfolder containing the files)
4. Deploy. Cloudflare Pages will serve the files at a `*.pages.dev` domain, or you can attach a custom domain (e.g. `inwoodatgreatnotch.com`).

### Any other static host

Upload both `.html` files to the same directory. No server-side logic required.

---

## Google Maps Embed

The Location section uses a no-API-key `<iframe>` embed pointing to **181 Long Hill Rd, Little Falls, NJ 07424**. This works for low-traffic community sites without a billing account.

If you need a more precisely pinned map:
1. Go to [maps.google.com](https://maps.google.com) and search for the address.
2. Click **Share → Embed a map**.
3. Copy the `src` URL from the generated `<iframe>` code.
4. Replace the `src` value in the `<iframe>` inside the `#location` section of `inwood-at-great-notch.html`.

---

## Updating Content

### Adding a new gallery photo

1. Add the image file to your hosting (or reference an external URL).
2. In `gallery.html`, copy any existing `.gallery-item` block and update:
   - `data-category` — one of: `entrance`, `grounds`, `pool`, `courts`, `living`, `playground`
   - `data-label` — caption shown in the lightbox
   - `data-index` — increment by 1 from the last item
   - `img src` and `img alt`
3. Also add the photo to the filter category count if adding a new category.

### Changing the Resident Portal URL

Search both files for `portal.cp-management.com/public` and update all instances.

### Adding a new residents section link

In `inwood-at-great-notch.html`, find the `.portal-links` div and add a new `<a>` with class `portal-link portal-link-secondary`. Include the lock icon SVG if the resource is shareholder-only.

---

## Browser Support

Tested layout targets: Chrome, Firefox, Safari, Edge (current versions). Uses CSS `clamp()`, `grid`, `columns`, `backdrop-filter`, and `position: sticky` — all well-supported in modern browsers. No IE11 support.

---

*Last updated June 2026*
