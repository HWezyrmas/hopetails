# HopeTails — Landing Page Build Specification (v2)

## 🎯 Design Vision

**Aesthetic Direction**: Editorial-Cinematic. Think a premium documentary platform crossed with a travel editorial magazine. NOT a charity website. NOT a pet adoption portal. This should feel like the kind of brand that makes you stop scrolling.

**The one thing someone will remember**: A full-bleed dark hero with a single large cat photo and sparse, confident type — like an Apple product launch page, but warm and alive.

**References absorbed**:
- **Mailchimp Presents**: Bold editorial grid, mixed type sizes, cards that feel like magazine covers, confident use of black
- **Apple TV page**: Cinematic full-bleed sections, extreme whitespace, typography that breathes, high contrast dark/light alternation, left-aligned copy blocks

---

## 🛠️ Deliverable

Single `index.html` file. All CSS and JS embedded. No build step required.

---

## 🎨 Design System

### Fonts
Load from Google Fonts:
```html
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400;1,700&family=Instrument+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
```

- **Display / Headlines**: `Playfair Display` — elegant, editorial, warm. Use italic variant for emotional moments.
- **Body / UI**: `Instrument Sans` — refined, modern, highly legible. Light weight (300) for long copy.

### Color Palette
```css
:root {
  /* Core */
  --ink:        #0D0D0B;   /* near-black for dark sections */
  --paper:      #FAF7F2;   /* warm off-white, not clinical white */
  --pure:       #FFFFFF;

  /* Accents */
  --ember:      #E8622A;   /* warm orange-red — rescue urgency, warmth */
  --ember-soft: #F5936A;   /* lighter ember for hover states */
  --sand:       #C9B99A;   /* muted warm tan for secondary elements */
  --sage:       #7A9E87;   /* muted green — hope, nature */
  --sky-mist:   #B8D0DC;   /* pale blue — travel, sky, destination */

  /* Text */
  --text-primary:   #0D0D0B;
  --text-secondary: #5A5550;
  --text-on-dark:   #FAF7F2;
  --text-muted:     #9A9188;
}
```

### Core Rules
- **No border-radius on full-bleed sections** — sharp edges feel editorial
- **Cards**: `border-radius: 4px` — barely rounded, intentional
- **Buttons**: Flat rectangles with `border-radius: 0` OR sharp `2px` — no pill shapes
- **Spacing unit**: `8px` base. Use multiples: `16, 24, 40, 64, 96, 128px`
- **Max content width**: `1200px`, centered
- **Line-height for display type**: `1.05` — tight and cinematic
- **Line-height for body**: `1.7` — generous and readable
- **Letter-spacing on uppercase labels**: `0.12em`

---

## 📐 Section-by-Section Specification

---

### SECTION 1 — Navigation
**Style**: Fixed. Transparent over hero, becomes `--ink` background after 60px scroll.

**Left**: Wordmark — `HopeTails` in `Playfair Display` italic, `--paper` color, ~22px. Preceded by a small paw SVG icon.

**Right links** (Instrument Sans, 500 weight, uppercase, 0.1em letter-spacing, ~13px):
`How It Works` · `Winter's Story` · `Flight Board` · `Download`

**Download**: A sharp rectangular button, `--ember` background, white text, no border-radius. On hover: `--ember-soft`.

**Transition**: `backdrop-filter: blur(0)` → `blur(20px)` + ink background on scroll. Smooth 0.4s.

---

### SECTION 2 — Hero
**Full viewport height** (`100vh`). **Dark**. Cinematic.

**Background**: `--ink`. Layered with a very subtle warm grain texture (CSS noise via SVG filter or `background-image` with a base64 noise SVG). No stock photo gradients.

**Layout**: Asymmetric. Two zones:
- **Left zone** (~55% width): Text, anchored to vertical center-left
- **Right zone** (~45% width): Large cat silhouette / abstract shape — a CSS-drawn or SVG abstract form suggesting a curled cat, in `--ember` with low opacity (~15%), purely decorative atmosphere

**Headline** (Playfair Display, 900 weight, ~96px desktop / ~52px mobile, `--paper`, line-height 1.0):
```
Saving lives,
one flight
at a time.
```
The word *"flight"* renders in `Playfair Display italic` in `--ember`.

**Subheadline** (Instrument Sans 300, ~18px, `--sand`, line-height 1.6, max-width 420px, margin-top 28px):
```
HopeTails connects rescuers, travelers, and adopters
across the world — so no cat has to wait forever.
```

**CTA row** (margin-top 48px):
- Primary: Sharp rectangular button, `--ember` fill, `--paper` text, `Instrument Sans 500`, uppercase, letter-spacing 0.1em, padding `14px 32px` — `GET EARLY ACCESS`
- Secondary: No fill, `1px solid --sand`, `--sand` text, same sizing — `SEE HOW IT WORKS`
- Gap between: `16px`

**Below CTAs** (margin-top 32px):
A single line, `Instrument Sans 300`, `--text-muted`, ~13px:
`★★★★★  2,400+ rescuers across 38 countries`

**Animation (on page load)**:
- Headline lines: each line fades up from `translateY(30px)` opacity 0 → 1, staggered 0.15s delay per line
- Subheadline: same, delayed 0.45s
- CTA row: fades in at 0.7s
- The ember decorative shape: slow pulse animation, `opacity: 0.10 ↔ 0.18`, 6s loop

**Bottom of hero**: A single thin horizontal line `1px solid rgba(255,255,255,0.1)` and a small centered scroll indicator — a thin downward arrow that gently bobs.

---

### SECTION 3 — Stats Bar
**Background**: `--ember`
**Height**: ~160px on desktop
**Layout**: 4 stats, horizontally distributed, vertically centered

**Each stat**:
- Number: `Playfair Display 700`, ~56px, `--paper`
- Label: `Instrument Sans 500`, uppercase, ~11px, letter-spacing 0.14em, `rgba(255,255,255,0.75)`

| Number | Label |
|--------|-------|
| 2,400+ | Rescuers worldwide |
| 850+ | Cats rehomed |
| 38 | Countries reached |
| 100% | Volunteer powered |

Separated by thin `1px solid rgba(255,255,255,0.25)` vertical lines.

---

### SECTION 4 — The Problem / Manifesto
**Background**: `--paper`
**Padding**: `128px 0`

**Layout**: Single column, centered, max-width `680px`

**Eyebrow label** (Instrument Sans 500, uppercase, 0.14em spacing, `--ember`, ~12px):
`WHY HOPETAILS EXISTS`

**Headline** (Playfair Display 700 italic, ~52px, `--ink`, line-height 1.1, margin-top 16px):
*"There are thousands of cats waiting. The flights already exist. The problem is connection."*

**Body copy** (Instrument Sans 300, ~17px, `--text-secondary`, line-height 1.75, margin-top 32px):
```
Every day, rescuers around the world find animals that need a home — often in countries where adoption is near-impossible. And every day, hundreds of flights take off with empty cabin space.

HopeTails exists in that gap. We built the infrastructure to match a cat in Amman with a family in Toronto, through a traveler on that exact flight — handling every document, every milestone, every moment of the journey.

We call them Flight Parents. And they change everything.
```

---

### SECTION 5 — How It Works (The 6 Stages)
**Background**: `--ink`
**Padding**: `128px 0`

**Eyebrow** (Instrument Sans 500, uppercase, `--ember`, ~12px):
`THE PROCESS`

**Headline** (Playfair Display 700, ~52px, `--paper`):
`Six stages. One new life.`

**Layout**: On desktop — a 2-column grid staggered like a magazine layout. On mobile — single column stack.

**Each stage card**:
- Background: `rgba(255,255,255,0.04)` — barely visible dark card
- Border: `1px solid rgba(255,255,255,0.08)`
- Border-radius: `4px`
- Padding: `32px`
- Top-left: Stage number in large `Playfair Display 900`, `~80px`, `rgba(255,255,255,0.06)` — ghost number in background
- Over it: Small pill badge `STAGE 01` in `--ember`, `Instrument Sans 500`, uppercase, ~10px
- Title: `Playfair Display 700`, ~24px, `--paper`
- Description: `Instrument Sans 300`, ~15px, `--sand`, line-height 1.65

| Stage | Icon | Title | Description |
|-------|------|-------|-------------|
| 01 | 🐱 | The Profile | Give the cat an identity. Photos, video, GPS tag, and a beautiful shareable adoption card. |
| 02 | 📋 | The Match | Confirm an adopter. Auto-generate document requirements based on origin and destination country. |
| 03 | 💛 | The Fund | Track vet and flight costs in real-time. Link out to GoFundMe or PayPal — fully transparent. |
| 04 | ✈️ | The Flight Parent | A traveler posts their itinerary. The system matches them to a rescue cat. A 3-way chat opens. |
| 05 | 📍 | The Journey | Four live milestones with required photo proof: Prep → Handover → Landing → Home. |
| 06 | 🌟 | The Happy Tail | Profile moves to the global gallery. Before & After. A wall of second chances. |

**Critical logic callout** — after Stage 04 card, a horizontal rule with small text:
`Instrument Sans 300`, `--text-muted`, ~13px, italic:
*"Flights cannot be arranged until documents and funding are fully verified. This is enforced by the app."*

---

### SECTION 6 — Winter's Story (Featured Cat Profile)
**Background**: `--paper`
**Padding**: `0` (edge to edge — no padding on the section container itself)

**Layout**: True 50/50 split. Left = photo zone. Right = story zone. Both full-height.

**Left zone**:
- Background: `--ink` (dark, like a cinema screen)
- Contains a large centered cat silhouette SVG (abstract, artistic — not cartoon) in `--ember` at ~30% opacity, layered
- At the top-left corner: A badge — `FEATURED RESCUE`, `Instrument Sans 500`, uppercase, `--ember` text, `1px solid --ember` border, `4px border-radius`, padding `6px 12px`
- At the bottom: A floating "Adoption Card" component (see below)

**Right zone**:
- Background: `--paper`
- Padding: `96px 80px`
- Vertical center alignment

**Eyebrow** (`--ember`, uppercase, `Instrument Sans 500`): `WINTER'S STORY`

**Headline** (Playfair Display 700 italic, ~44px, `--ink`, line-height 1.1):
*"He appeared on a windowsill in November. Wounded. Deaf. Purring."*

**Body copy** (Instrument Sans 300, ~16px, `--text-secondary`, line-height 1.8, margin-top 28px):

> On a cold November morning, he appeared — perched silently on a windowsill like he'd been waiting to be found. His name became **Winter**, and it suited him perfectly: quiet, striking, and carrying something heavy beneath the surface.
>
> Winter arrived with deep wounds across his back, almost certainly from a surprise attack by another stray — a cruel fate for a deaf cat who never heard it coming. Despite the pain, he purred. Despite the fear, he leaned in for cuddles. His wounds had turned severely infected by the time he was found, requiring weeks of treatment, careful medication, and delicate sutures.
>
> But Winter fought. And Winter won.
>
> Today, at around six months old, this silky, soulful boy has made a full recovery. He loves nothing more than curling into someone's lap — though he's equally happy charming other cats in the room before quietly slipping away to reclaim his throne on the sofa. Gentle. Loving. Entirely unaware of how extraordinary he is.

**Bold closing line** (Playfair Display 700 italic, ~22px, `--ember`, margin-top 24px):
*"Winter is ready for his flight home. Is that home yours?"*

**CTA button** (margin-top 32px): Sharp rectangle, `--ember`, white text, uppercase — `APPLY TO ADOPT WINTER`

---

#### Adoption Card Component (floats over left zone, bottom-left, overlapping the split)
**Position**: `absolute`, bottom `48px`, left `48px`, z-index elevated
**Size**: ~280px wide
**Background**: `--paper`
**Border-radius**: `4px`
**Shadow**: `0 20px 60px rgba(0,0,0,0.4)`
**Padding**: `24px`

**Contents**:
```
┌─────────────────────────────┐
│  STAGE 4 OF 6    [progress] │  ← ember badge + thin progress bar
│                             │
│  Winter                     │  ← Playfair Display 700, 22px, ink
│  ~6 months · Male · Deaf    │  ← Instrument Sans 300, 13px, muted
│                             │
│  📍 Amman, Jordan           │  ← origin
│  ✈️  → Anywhere, World      │  ← destination
│                             │
│  ✓ Vaccinated               │  ← sage color checkmarks
│  ✓ Health Cert Ready        │
│  ✓ Fully Funded             │
│                             │
│  [ APPLY TO ADOPT ]         │  ← ember button, full width
└─────────────────────────────┘
```
Progress bar: thin `4px` bar, `--sage` fill at 60%, `rgba(0,0,0,0.08)` track.

---

### SECTION 7 — The Three Roles
**Background**: `--paper`
**Padding**: `128px 0`

**Headline** (Playfair Display 700, ~52px, `--ink`, centered):
`Everyone has a part to play.`

**Layout**: 3 cards in a row on desktop. Each card is full-height with a top colored stripe.

**Card structure**:
- Top stripe: `8px` tall, solid color (`--ember` / `--sage` / `--sky-mist` respectively)
- Background: `--pure` (white)
- Border: `1px solid rgba(0,0,0,0.08)`
- Border-radius: `4px`
- Padding: `40px 32px`
- Hover: `transform: translateY(-4px)`, transition `0.3s`

| Stripe Color | Role | Description |
|---|---|---|
| `--ember` | **Rescuers & Volunteers** | You found them — now find them a home. Create profiles, coordinate documents, manage every stage of the journey. |
| `--sage` | **Adopters** | Your forever family is waiting somewhere in the world. Apply, follow the journey live, and welcome them through your door. |
| `--sky-mist` | **Flight Parents** | Your next trip could save a life. Post your itinerary, get matched with a rescue cat, and become someone's hero at 35,000 feet. |

Below each description: A small arrow link in the card's stripe color — `Learn more →`

---

### SECTION 8 — Happy Tails Gallery
**Background**: `--ink`
**Padding**: `128px 0`

**Eyebrow** (`--ember`, uppercase, `Instrument Sans 500`): `THE GALLERY`

**Headline** (Playfair Display 700, ~52px, `--paper`):
`The wall of second chances.`

**Subheadline** (Instrument Sans 300, ~18px, `--sand`, max-width 560px):
`Every face here has a story. Every story started with someone who chose to act.`

**Layout**: Masonry-style grid. 4 columns on desktop, 2 on mobile. Mixed heights — some cards taller than others. This is the Mailchimp Presents energy: editorial grid, not uniform tiles.

**Each Before/After Card**:
- A split panel — left half darker (grayscale tint via CSS `filter: grayscale(80%) brightness(0.7)`), right half full color
- A thin vertical `1px` `--ember` line dividing left and right
- Small paw icon centered on the dividing line
- Cat name in `Playfair Display italic` at bottom-left, `--paper`
- Route below name: `Amman 🇯🇴 → Toronto 🇨🇦`, `Instrument Sans 300`, `--sand`, ~12px
- Hover: right panel expands to ~65% width smoothly (`transition: 0.5s`)

**Note to developer**: Use placeholder colored rectangles for photos (CSS background colors with subtle gradients). Leave `data-src` attributes for real images. Heights should vary: some `280px`, some `340px`, some `200px` — avoid uniform grid.

**Below grid**: Centered `Instrument Sans 500` link in `--ember` — `View all Happy Tails →`

---

### SECTION 9 — Download / App CTA
**Background**: `--paper`
**Padding**: `160px 0`

**Layout**: Centered, single column, max-width `700px`

**Eyebrow** (`--ember`, uppercase): `COMING SOON`

**Headline** (Playfair Display 900, ~72px, `--ink`, line-height 1.0, centered):
```
Every rescue
needs a
Flight Parent.
```
*"Flight Parent"* renders in italic + `--ember`.

**Subheadline** (Instrument Sans 300, ~18px, `--text-secondary`, centered, line-height 1.65, margin-top 24px):
`Join our early access list. Be the first to know when HopeTails launches.`

**Email form** (margin-top 48px):
- `display: flex` row
- Input: `Instrument Sans 300`, `--ink`, `border-bottom: 2px solid --ink` only (no box border — underline style), background transparent, `~300px` wide, `14px` font, padding `12px 0`
- Button: Sharp rectangle, `--ember`, `--paper` text, `Instrument Sans 500`, uppercase, letter-spacing 0.1em, `padding: 14px 32px` — `NOTIFY ME`
- Gap: `16px`
- Below form: `Instrument Sans 300`, `--text-muted`, ~12px — *"No spam. No noise. Just the moment we go live."*

---

### SECTION 10 — Footer
**Background**: `--ink`
**Padding**: `80px 0 40px`

**Top row**: Logo (left) + Social icons (right): Instagram, TikTok, X/Twitter — simple SVG icons, `--sand` color, hover `--paper`

**Middle row** (margin-top 48px): 3 link columns + 1 text column

| Column | Links |
|---|---|
| App | How It Works · Download · Flight Board · Global Map |
| Community | Rescuers · Adopters · Flight Parents · Route Experts |
| Info | About · Privacy · Terms · Contact |
| Text | `Instrument Sans 300`, `--sand`, ~14px: *"HopeTails is a volunteer-powered platform. We believe every cat deserves a second chance, no matter where in the world they were born."* |

**Bottom bar** (margin-top 64px, `1px solid rgba(255,255,255,0.08)` top border, padding-top 24px):
- Left: `© 2025 HopeTails` — `Instrument Sans 300`, `--text-muted`, ~13px
- Right: `Built with love. 🐾` — same style

---

## ✨ Animation Master List

| Element | Animation | Timing |
|---|---|---|
| Hero headline (each line) | `translateY(30px) opacity:0` → base state | Stagger 0.15s per line, ease-out |
| Hero decorative shape | Slow opacity pulse 0.10 ↔ 0.18 | 6s infinite |
| Scroll down arrow | `translateY 0 ↔ 8px` | 2s infinite ease-in-out |
| Stats bar numbers | Count up from 0 on enter viewport | `IntersectionObserver` trigger |
| Stage cards | `translateY(20px) opacity:0` → base | Stagger 0.1s, trigger on scroll |
| Role cards | `translateY(-4px)` on hover | `transition: 0.3s` |
| Before/After card divider | Right panel widens on hover | `transition: 0.5s` |
| Nav background | Transparent → `--ink` + blur | `transition: 0.4s` on scroll |
| Section headlines | Fade up on scroll enter | `IntersectionObserver` |

All scroll animations use `IntersectionObserver` with `threshold: 0.15`.

---

## 📱 Responsive Breakpoints

| Breakpoint | Key Changes |
|---|---|
| `> 1200px` | Full layout as specified |
| `768px – 1200px` | Stage grid → 2 col. Winter section stacks vertically. Role cards → 2+1 layout. |
| `< 768px` | Everything single column. Hero text ~42px. Nav → hamburger. Form → stacked. |

---

## 🧩 Implementation Notes

1. **Grain texture**: Add to `body::before` — a semi-transparent SVG noise overlay, `opacity: 0.03`, `pointer-events: none`, `position: fixed`, `z-index: 9999`. This gives the whole page a slight film grain feel without being heavy.

2. **Winter's section**: The left/right split should use CSS Grid with `grid-template-columns: 1fr 1fr`. The left side should be `position: relative` to contain the absolutely-positioned Adoption Card.

3. **Adoption Card overlap**: On desktop, the card should slightly overlap the right text zone using `transform: translateX(40px)` — it crosses the boundary between the two zones, which is a classic editorial trick.

4. **Before/After photos**: Use `position: relative` on the card, two absolutely-positioned child divs with `clip-path` or `width` transitions. The before side: `filter: grayscale(80%) brightness(0.6)`. The after side: full color.

5. **No CSS frameworks**. No Tailwind. Pure CSS with custom properties. This is intentional — it keeps the file self-contained and the design purposeful.

6. **The ember italic trick**: In Playfair Display, italic weight feels noticeably different and more emotional. Use it intentionally on key emotional words or phrases — never for entire paragraphs.

---

*End of specification. Deliver as a single `index.html` file with all CSS in a `<style>` block and all JS in a `<script>` block at the end of `<body>`.*
