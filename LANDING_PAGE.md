# HopeTails Landing Page — Technical Reference

Single file: `index.html` (2173 lines, ~April 2025). No build step. Deployed via Vercel, auto-deploys from `git push` to `main` on `https://github.com/HWezyrmas/hopetails.git`.

---

## Design System

### Fonts
- **Headings**: `Playfair Display` (italic heavy, loaded from Google Fonts)
- **Body / UI**: `Instrument Sans` (weight 300 for body, 500 for labels)

### CSS Variables (`:root`)
```css
--ink:            #0D0D0B   /* near-black, all headings & dark sections */
--paper:          #FAF7F2   /* warm off-white, page background */
--pure:           #FFFFFF
--ember:          #E8622A   /* primary accent — CTAs, eyebrows, stage 1 color */
--ember-soft:     #F5936A
--sand:           #C9B99A   /* secondary text on dark backgrounds */
--sage:           #7A9E87   /* stage 2 color */
--sky-mist:       #B8D0DC
--text-primary:   #0D0D0B
--text-secondary: #5A5550
--text-on-dark:   #FAF7F2
--text-muted:     #9A9188
```

### Global Classes
- `.eyebrow` — 11px uppercase label, `--ember` color, 0.14em letter-spacing
- `.display` — Playfair Display serif, line-height 1.05
- `.btn`, `.btn-ember`, `.btn-outline-sand`, `.btn-outline-ink` — pill-less buttons (no border-radius), uppercase, 12px
- `.reveal` / `.reveal.visible` — scroll fade-in (opacity 0→1, translateY 24px→0). Applied via `IntersectionObserver` at 12% threshold

### Decorative
- Film grain overlay: `body::before` with an SVG feTurbulence noise at `opacity: 0.035`, fixed position, `pointer-events: none`, z-index 9999
- Logo paw SVG bounces: `@keyframes paw-jump` — double-bounce every 3.2s

---

## Page Sections

### 1. `#nav` — Sticky Navigation
- Fixed, `z-index: 1000`, transparent by default
- On scroll > 60px: adds class `.scrolled` → `rgba(13,13,11,0.92)` background + `backdrop-filter: blur(20px)` + hairline border
- Desktop links: How It Works → `#process` | Winter's Story → `#winter` | Flight Board → `#gallery` | Download → `#cta` (ember button)
- Mobile: links hidden, `#hamburgerBtn` shown → opens `#mobileMenu` (full-screen overlay, Playfair 32px links)

### 2. `#hero` — Full-viewport hero
- Background: `--ink` (dark)
- Two-column grid (`1fr 1fr`): left = `.hero-content`, right = `.hero-photo`
- Headline: `.hero-headline` — Playfair Display 900, `clamp(52px, 7vw, 96px)`, three `.line` spans with staggered `animation-delay` (0.1s / 0.25s / 0.4s), fade+slide up on load
- Photo: `winter-recovery-1.jpg`... **wait, no** — Unsplash cat photo URL (`photo-1574158622682-e40e69881006`). The right column uses a real Unsplash image as `<img>` with `::after` gradient overlay blending it into the dark left side.
- `.hero-sub` — sand text, 18px, fades in at 0.55s delay
- `.hero-ctas` — "Get Early Access" (ember) + "See How It Works" (outline-sand), fade in at 0.7s
- `.hero-proof` — star + "2,400+ rescuers across 38 countries", fades in at 0.85s
- `.hero-bottom` — centered bobbing scroll arrow (`.scroll-arrow`)
- Mobile: hero becomes single column, photo goes full-bleed background (`position: absolute; inset: 0`), content overlaid `z-index: 2`

### 3. `#stats` — Stats bar
- Background: `--ember` (orange)
- 4-column grid: 2,400+ Rescuers / 850+ Cats / 38 Countries / 100% Volunteer-powered
- Numbers use `.stat-num` — Playfair 700, `clamp(40px, 4.5vw, 64px)`, white
- Count-up animation: `data-target` attribute + `IntersectionObserver` at 50% threshold, runs once
- Vertical dividers between items via `::before` pseudo-element
- Mobile: 2×2 grid, `.stat-context` hidden

### 4. `#manifesto` — Why we exist
- Background: `--paper`
- Narrow centered column (`max-width: 680px`)
- `.manifesto-headline` — Playfair italic 700, `clamp(28px, 4vw, 52px)`
- `.manifesto-body` — light 300, 17px, 1.8 line-height, left-aligned

### 5. `#process` — How It Works (6-stage carousel)
- Background: `--paper`
- Carousel: `.carousel-viewport` → `.carousel-track` → six `.pass` cards
- Each pass = `.pass-stub` (colored left strip) + `.pass-perf` (dashed divider) + `.pass-main` (white body)
- Pass stub has cutout circles top/bottom via `::before`/`::after`
- Stage accent colors: S1 `#E8622A` / S2 `#5A8A70` / S3 `#C4943A` / S4 `#4A7FA0` / S5 `#7B6BAE` / S6 `#2A7A4E`
- Active pass: `opacity: 1, scale(1)`; adjacent: `opacity: 0.65, scale(0.93)`; rest: `opacity: 0.4, scale(0.88)`
- Navigation: prev/next buttons (`#stagePrev` / `#stageNext`), 6 dot indicators, swipe support, keyboard arrows
- Stage 5 shows `.pass-lock` badge ("🔒 Requires stages 2 & 3")
- `.stages-note` — orange left-border callout about state machine enforcement

### 6. `#winter` — Winter's Story (NYT Editorial layout)
- Background: `--paper`, `padding: 0`
- **Not** a `.container` wrapper — uses custom width constraints:
  - `.w-article` — `max-width: 660px`, centered, for text blocks
  - `.w-wide` — `max-width: 1000px`, centered, for photo blocks that "bleed" wider than text

**DOM order:**
1. `.w-header` (eyebrow + `.w-headline` + `.w-byline`) — centered, Playfair italic
2. `hr.w-rule` — hairline separator
3. `.w-wide.w-photo-hero` — full recovery photo (`winter-recovery-1.jpg`), `height: 500px, object-fit: cover`
4. `.w-article > .w-body` — first two paragraphs of story
5. `.w-wide > .w-photo-pair` — two rescue photos side-by-side (`winter-rescue-1.jpg` + `winter-rescue-2.jpg`), `height: 340px` each, with `.w-photo-label` overlaid badges ("Day 1" / "Week 2")
6. `.w-article > .w-pullquote` — "But Winter fought. And Winter won." (Playfair italic, double rule borders)
7. `.w-article > .w-body` — recovery paragraph
8. `.w-article > .w-card-widget` — inline adoption card (see below)
9. `.w-article > .w-footer-text` — closing quote + CTA button

**Adoption Card** (`.w-card-widget`):
- Outer: `display: flex`, `border: 1px solid rgba(0,0,0,0.10)`, no border-radius
- `.w-card-widget-accent` — 4px ember left stripe
- Inner `.adoption-card` — `background: #FAFAF8`, `padding: 24px 28px`
- Sub-elements: `.ac-stage-row`, `.ac-stage-pill`, `.ac-progress-bar`, `.ac-progress-fill`, `.ac-name`, `.ac-meta`, `.ac-route`, `.ac-checks`, `.ac-check`, `.ac-btn`
- Sub-element CSS (`.ac-stage-row`, `.ac-stage-pill`, `.ac-progress-bar`, etc.) was added in the "Style adoption card sub-elements inside Winter modal" commit.

### 7. `#roles` — App Showcase (Apple-style)
- Background: `#f5f5f7` (Apple's gray)
- Layout: `.roles-header` (centered text) + `.phones-row` (5 iPhone frames, full-bleed below the header)

**iPhone PNG Technique:**
- Device frame: `iphone-mockup.png` (566×802px PNG; phone body occupies left 57%, diagonal drop shadow extends right 43%)
- Each `.showcase-phone` contains `.iphone-frame` with:
  - `.iphone-mockup-img` — the PNG at `z-index: 2`, full width, pointer-events none
  - `.iphone-screen` — absolutely positioned at `top: 2.5%, left: 3.4%, width: 51%, bottom: 20.3%`, `z-index: 1`, `border-radius: 10%`
- Screen area measured pixel-precisely from PNG (x=19–308, y=20–639 of 566×802)
- `.iphone-frame` width: `440px`
- Shadow collapse: `margin-right: -160px` on each `.showcase-phone` (not last-child) to overlap the baked-in PNG shadow with the next phone's body

**5-phone arc animation:**
- Phones order (left → right): app1, app3, app2 (center/hero), app3, app1
- Z-index: outer=1, second=3, center=2, (not explicitly set for 4th/5th, inherits)
- Start state: outer 2 at `translateY(44px)`, center at 0
- When `.phones-row` has `.phones-leveled` class: outer 2 → `translateY(0)` — all three at same baseline
- `IntersectionObserver` at 25% threshold: adds `phones-leveled` after 300ms delay when in view, removes it when out of view
- Mobile (≤768px): `iphone-frame` width `80vw`, `margin-right: -28vw`, phone labels hidden

**⚠️ Note:** Current implementation has 3 phones not 5 in the nth-child selectors (`.showcase-phone:first-child`, `.showcase-phone:nth-child(2)`, `.showcase-phone:last-child`). The 4th and 5th phones inherit first/last-child styles differently than the session summary implies. Inspect visually to confirm arc looks correct.

### 8. `#gallery` — Happy Tails Gallery (Polaroid Wall)
- Background: `--ink` (dark)
- 3×2 grid of `.polaroid` cards: `.polaroid-photo` (square, `aspect-ratio: 1/1`) + `.polaroid-caption`
- Each polaroid: white background, `padding: 12px 12px 56px`, box-shadow
- Scatter: `nth-child` rotate + translateY (between -3.2deg and +2.8deg)
- Hover: `rotate(0) translateY(-16px) scale(1.05)`, z-index 10, enhanced shadow
- Photo layout: `.p-after` (full size, vibrant new-life photo) + `.p-before` (33% corner thumbnail, `grayscale(80%)`, rotated -5deg, white border)
- Cat roster: Winter (`winter-recovery-2.jpg` / `winter-rescue-2.jpg`), Luna (Unsplash), Mochi (Unsplash), Saffron (Unsplash), Nala (Unsplash), Olive (Unsplash)
- Routes: Amman→Forever Home / Istanbul→Amsterdam / Beirut→London / Cairo→Berlin / Dubai→Melbourne / Athens→New York
- Footer link: "View all Happy Tails →"

### 9. `#cta` — Email Waitlist
- Background: `--ink`
- Ghost `"` decorative behind content (`position: absolute`, 480px, `opacity: 0.03`)
- `.cta-headline` — Playfair 900, `clamp(44px, 6vw, 72px)`, "Every rescue needs a *Flight Parent.*"
- Form: underline-style email input + ember "Notify Me" button
- On submit: button text → "You're on the list ✓", input placeholder → "See you at launch.", both disabled

### 10. `#footer`
- Background: `--ink`
- 4 rows: tagline (ghost text), logo+socials, 3 nav columns + brand text paragraph, copyright
- Tagline: "Saving lives, one flight at a time." at `opacity: 0.10` — ghost effect
- Socials: Instagram, TikTok, X/Twitter (inline SVGs)
- Grid: `1fr 1fr 1fr 2fr` (App / Community / Info / Brand text)

---

## JavaScript

All JS is inline at bottom of `<body>`, no external dependencies.

| Block | What it does |
|-------|-------------|
| Nav scroll | `window.scroll` listener → toggles `.scrolled` class at 60px |
| Mobile menu | `#hamburgerBtn` / `#mobileClose` toggle `.open` on `#mobileMenu` |
| Scroll reveals | `IntersectionObserver` at 12% → adds `.visible` to `.reveal` elements (one-way) |
| Phone arc | `IntersectionObserver` at 25% on `.phones-row` → toggles `.phones-leveled` (reversible, 300ms delay) |
| Stats count-up | `IntersectionObserver` at 50% → animates `data-target` numbers over ~1s (one-way) |
| Stage carousel | Full carousel: goTo(idx), prev/next buttons, dot indicators, swipe, keyboard arrows, resize recalc |
| Form submit | Prevents default, shows confirmation state, disables input |

---

## Local Image Files

| File | Used in | Description |
|------|---------|-------------|
| `iphone-mockup.png` | `#roles` × 5 | iPhone 14 Pro PNG frame (566×802px). Body left 57%, drop shadow extends right 43%. Screen opening: x=19–308, y=20–639. |
| `app1.jpeg` | `#roles` phones 1 & 5 | Flights screen |
| `app2.jpeg` | `#roles` phone 3 (center) | Discover screen |
| `app3.jpeg` | `#roles` phones 2 & 4 | Journeys screen |
| `winter-rescue-1.jpg` | `#winter` photo pair left | Winter day 1 (rescue, wounds) |
| `winter-rescue-2.jpg` | `#winter` photo pair right, `#gallery` Winter polaroid "before" | Winter week 2 |
| `winter-recovery-1.jpg` | `#winter` hero photo | Winter recovered (full-bleed) |
| `winter-recovery-2.jpg` | `#gallery` Winter polaroid "after" | Winter happy and healthy |

Hero cat photo is an **Unsplash URL**, not a local file.

---

## Responsive Breakpoints

| Breakpoint | Key changes |
|---|---|
| `≤1024px` | Container padding 28px; footer grid 2-col |
| `≤768px` | Nav hamburger; hero goes single-col (photo becomes full-bleed BG); stats 2×2; carousel card shrinks to `min(440px, 80vw)`; Winter photos shorter; phones `80vw`; gallery 2-col; CTA form stacks |
| `≤480px` | Hero padding tighter; footer 1-col |

---

## Known Issues / Pending Work

1. **Winter's Story section** — Flagged for polish pass. Current NYT editorial layout is functional but user wanted to revisit it. Hero photo (`winter-recovery-1.jpg`) shows at `height: 500px` which may be too large on some screens.

3. **App showcase arc** — 5-phone arc nth-child selectors only explicitly handle `first-child`, `nth-child(2)`, and `last-child`. Phones 3, 4, 5 behavior should be verified visually. Screen positioning (`top: 2.5%, left: 3.4%, width: 51%, bottom: 20.3%`) was derived from pixel analysis — may need fine-tuning.

---

## Common Edit Pitfalls

- **Edit tool "file modified since read"**: If Edit fails, use Python: `python3 -c "f=open('index.html');c=f.read();f.close();c=c.replace(OLD,NEW);f=open('index.html','w');f.write(c);f.close()"`. Always verify the replacement string with `repr()` first.
- **Smart quotes and em-dashes** (`"`, `"`, `—`) in `old_string` break Edit tool matching. Use Python for any edit touching those characters.
- **Unsplash URLs** are used in the hero and gallery. Do not commit API keys or tokens — the URLs are public and unauthenticated.
- **Git deployment**: `git add <files> && git commit -m "..." && git push` → Vercel picks up automatically. Always `git add` new image files before pushing — untracked images won't deploy.
