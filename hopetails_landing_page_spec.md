# HopeTails — Landing Page Build Specification

## 🎯 Project Brief

Build a **stunning, conversion-focused landing page** for **HopeTails** — a mobile app that connects animal rescuers, international travelers, and adopters to save cats through a coordinated "Flight Parent" logistics process.

**Tagline**: *Saving lives, one flight at a time.*

---

## 🖥️ Tech Stack

- **Framework**: Plain HTML + CSS + Vanilla JS (single `index.html` file, no build step)
- **Fonts**: Load from Google Fonts — use `DM Serif Display` for headings and `DM Sans` for body text (similar warmth and authority to the Mailchimp reference)
- **Icons**: Use inline SVGs or Lucide icons via CDN
- **No external CSS frameworks** — write all styles from scratch

---

## 🎨 Design System

### Color Palette
Inspired by the Mailchimp reference's use of strong contrast sections with warm accents, adapted to a dreamy, pastel-forward animal welfare brand:

```css
:root {
  --cream: #FDF8F2;          /* page background, soft warm white */
  --charcoal: #1A1A2E;       /* primary text, hero headings */
  --sage: #8CB8A8;           /* accent green — nature, hope */
  --blush: #F2A7A7;          /* warm coral/pink accent */
  --sky: #A8C8E8;            /* soft blue — travel, sky */
  --golden: #F5C842;         /* CTA button color — warm yellow like Mailchimp */
  --golden-dark: #D4A800;    /* CTA button hover */
  --lavender: #C5B8E8;       /* section accent */
  --off-white: #FFFFFF;
  --light-gray: #F5F0EB;     /* alternating section background */
  --mid-gray: #6B6B7A;       /* secondary text */
  --dark-section: #1A1A2E;   /* dark CTA/footer sections */
}
```

### Typography
```css
/* Headings */
font-family: 'DM Serif Display', serif;

/* Body / UI */
font-family: 'DM Sans', sans-serif;
```

### Key Design Principles
- **Airbnb for pets** aesthetic: clean, premium, generous whitespace, rounded corners (`border-radius: 16px`), card-based layouts
- Alternate between `--cream`, `--light-gray`, and `--dark-section` backgrounds across sections (like Mailchimp's distinct content blocks)
- Large, bold headlines with comfortable line-height (~1.15)
- Subtle drop shadows on cards (`box-shadow: 0 4px 24px rgba(0,0,0,0.08)`)
- CTA buttons: `background: var(--golden)`, bold weight, rounded pill shape (`border-radius: 50px`), slightly large padding (`16px 36px`)
- All images/avatars use `border-radius: 16px` or `50%` for circles

---

## 📐 Page Structure & Section-by-Section Spec

### 1. 🔝 Sticky Navigation Bar
- Left: HopeTails logo (paw icon + wordmark in `DM Serif Display`)
- Right: Links — `How It Works`, `Success Stories`, `Join a Flight`, `Download App`
- `Download App` = pill button in `--golden`
- Sticky on scroll with subtle `backdrop-filter: blur(10px)` and a thin `border-bottom`
- Mobile: hamburger menu

---

### 2. 🦁 Hero Section
**Background**: Warm cream (`--cream`) with a subtle repeating dot pattern or soft grain texture overlay

**Layout**: Two columns — Left: text + CTAs | Right: floating mobile app mockup (use a placeholder div styled as a phone frame if no image available, or a full-bleed illustration of a cat traveling)

**Headline** (DM Serif Display, ~72px desktop / ~42px mobile):
> Every rescue cat deserves a hero.
> Find yours in the sky.

**Subheadline** (DM Sans, ~20px, `--mid-gray`):
> HopeTails connects rescuers, adopters, and international travelers to give abandoned cats a second chance — anywhere in the world.

**CTAs**:
- Primary button: `Download on iOS` → golden pill button
- Secondary button: `Get on Android` → outlined pill button
- Below CTAs: small social proof line — `★★★★★  Trusted by 2,400+ rescuers in 38 countries`

**Right column**: A large rounded card (`border-radius: 24px`) showing the "app mockup" — can be a cat image with a floating UI overlay showing Stage progress (e.g., a pill badge saying "Stage 4: Flight Matched ✈️")

**Animation**: On page load, the headline words fade+slide up with staggered `animation-delay`. The phone mockup gently floats with a CSS `@keyframes float` (subtle up-down oscillation).

---

### 3. 📊 Social Proof Bar
**Background**: `--charcoal` (dark, like Mailchimp's black stats bar)

**Layout**: Horizontal row of 3–4 stats, centered, separated by thin vertical lines

**Stats**:
| Stat | Label |
|------|-------|
| 2,400+ | Rescuers Worldwide |
| 850+ | Cats Rehomed |
| 38 | Countries Reached |
| 100% | Volunteer-Powered |

**Style**: Numbers in `DM Serif Display`, large (~48px), `--golden`. Labels in `DM Sans`, small, `--sky`.

---

### 4. 🐾 How It Works — The 6 Stages
**Background**: `--light-gray`

**Headline**: `How a rescue becomes a reunion.`

**Subheadline**: `Six carefully orchestrated steps, powered by a global community.`

**Layout**: A horizontal step flow on desktop, vertical accordion/stack on mobile.

**Render each stage as a card**:
- Icon (emoji or SVG)
- Stage number badge (small pill, `--sage` background)
- Title
- One-line description

| # | Icon | Title | Description |
|---|------|-------|-------------|
| 1 | 🐱 | Create a Profile | Build a beautiful adoption card with photos, video, and GPS location |
| 2 | 📋 | Match an Adopter | Confirm an adopter and auto-generate country-specific document requirements |
| 3 | 💛 | Fund the Journey | Track fundraising goals in real-time — linked to GoFundMe or PayPal |
| 4 | ✈️ | Find a Flight Parent | Travelers post their itinerary; get matched with a rescue cat passenger |
| 5 | 📍 | Live Journey Updates | Media uploads at 4 global milestones: Prep → Handover → Landing → Home |
| 6 | 🌟 | Happy Tails Gallery | The rescue goes live in the global Before & After wall of impact |

**Progression Line**: A dotted horizontal line connecting stage cards on desktop (like a timeline)

**Key callout**: Add a small `⚠️ Note` below Stage 4: *"Flights can only be booked once documents (Stage 2) and funds (Stage 3) are fully verified."*

---

### 5. 🐈 Featured Cat Profile — Winter's Story
**Background**: `--cream`

**Headline**: `Meet Winter. He waited on a windowsill for his miracle.`

**Layout**: Two-column card — Left: cat image (placeholder: a rounded white card with a paw silhouette, or an actual cat photo slot), Right: story + adoption card UI

**The Story** (render as flowing body copy, `DM Sans`, ~17px, `--charcoal`, generous line-height):

> On a cold November morning, he appeared — perched silently on a windowsill like he'd been waiting to be found. His name became **Winter**, and it suited him perfectly: quiet, striking, and carrying something heavy beneath the surface.

> Winter arrived with deep wounds across his back, almost certainly from a surprise attack by another stray — a cruel fate for a deaf cat who never heard it coming. Despite the pain, he purred. Despite the fear, he leaned in for cuddles. His wounds had turned severely infected by the time he was discovered, requiring weeks of treatment, medication, and careful sutures.

> But Winter fought. And Winter won.

> Today, at around six months old, this silky, soulful boy has made a **full recovery**. He loves nothing more than curling into someone's lap, though he's equally happy charming other cats in the room before quietly slipping away to reclaim his throne on the sofa. He is gentle, deeply loving, and entirely unaware of how extraordinary he is.

> **Winter is ready for his flight home. Is that home yours?**

**Right Side — "Adoption Card" UI Component**:
Render a stylized card that mimics the in-app "Adoption Card" feature:

```
┌──────────────────────────────┐
│  🐾 WINTER                   │
│  Age: ~6 months · ♂ Male     │
│  Origin: Amman, Jordan 🇯🇴    │
│  Status: ✈️ Stage 4 — Flight  │
│          Parent Needed        │
│                               │
│  [Progress Bar: Stage 4/6]    │
│                               │
│  🩺 Vaccinated  📋 Docs Ready │
│  💛 Fully Funded               │
│                               │
│  [ 💛 Apply to Adopt ]        │
│  [ ✈️  Offer a Flight ]       │
└──────────────────────────────┘
```

Style this card with:
- White background, `border-radius: 20px`
- Soft shadow
- Progress bar filled to 60% in `--sage`
- Status badge: `--sky` background
- Two pill buttons at the bottom: golden "Apply to Adopt", outlined "Offer a Flight"

---

### 6. 👥 Three Roles — Who Is This For?
**Background**: `--dark-section` (`--charcoal`)

**Headline**: `Everyone has a role to play.` (white text)

**Layout**: 3 equal cards side by side (stack on mobile)

**Cards**:

| Role | Icon | Title | Description |
|------|------|-------|-------------|
| 🛟 | 🐾 | Rescuers & Volunteers | You found them, now find them a home. Create profiles, manage logistics, coordinate the rescue from start to finish. |
| 🏠 | ❤️ | Adopters | Your forever family is waiting across the world. Apply, track the journey, and welcome them home. |
| ✈️ | ✈️ | Travelers (Flight Parents) | Your next trip could save a life. Post your itinerary, get matched, become a hero at 35,000 feet. |

**Card style**: Semi-transparent dark cards with a `--sage` or `--blush` top accent stripe, white text

---

### 7. 🖼️ Happy Tails Gallery — Before & After
**Background**: `--light-gray`

**Headline**: `The wall of second chances.`

**Subheadline**: `Every face here has a story. Every story started with someone who cared enough to act.`

**Layout**: A grid of 4–6 "Before & After" cards (use placeholder content)

**Each card**:
- Split left/right: Left = grayscale rescue photo, Right = vibrant "new life" photo
- A thin dividing line with a small ✈️ or paw icon in the center
- Cat name + origin → destination route below (`Amman 🇯🇴 → Toronto 🇨🇦`)
- Soft card border, hover: slight scale-up (`transform: scale(1.02)`)

**Below grid**: A CTA — `[ 🌟 See All Happy Tails ]` outlined button

---

### 8. 📬 Email Signup / Waitlist Section
**Background**: `--golden` (full-width warm yellow block — mirrors Mailchimp's bold CTA sections)

**Headline** (`--charcoal`, DM Serif Display):
> Be the first to know when HopeTails launches.

**Subheadline**:
> Join our early access list. Get notified the moment the app goes live.

**Form**:
- Email input field (rounded, white background)
- Submit button: `--charcoal` background, white text — `"Join the Waitlist"`
- Below: tiny text — *"No spam. Just cats that need you."*

---

### 9. 🔗 Footer
**Background**: `--charcoal`

**4-column layout**:
- Col 1: Logo + tagline + social icons (Instagram, TikTok, Twitter/X)
- Col 2: App — `How It Works`, `Download`, `Flight Board`, `Global Map`
- Col 3: Community — `Rescuers`, `Adopters`, `Travelers`, `Route Experts`
- Col 4: Info — `About`, `Privacy Policy`, `Terms`, `Contact`

**Bottom bar**: `© 2025 HopeTails. Built with love for animals everywhere. 🐾`

---

## 📱 Responsive Behavior

| Breakpoint | Behavior |
|---|---|
| Desktop (>1024px) | Full multi-column layouts as specified |
| Tablet (768–1024px) | 2-column grids, scaled typography |
| Mobile (<768px) | Single column, hamburger nav, stacked sections, CTA buttons full-width |

---

## ✨ Animations & Interactions

| Element | Animation |
|---|---|
| Hero headline | Words fade+slide up on load with staggered `animation-delay` (0.1s per word) |
| Phone mockup | Gentle float loop (`translateY -8px` ↕ `translateY 0`) every 4s |
| Stage cards | Fade in from bottom as user scrolls into view (`IntersectionObserver`) |
| Before/After cards | Scale up on hover (`transform: scale(1.02), transition: 0.3s`) |
| Nav bar | `backdrop-filter: blur(10px)` + `box-shadow` appears after scrolling 80px |
| CTA buttons | Scale `1.03` on hover, press `0.97` on active |

---

## 🧩 Component Checklist

- [ ] Sticky navbar with mobile hamburger
- [ ] Hero (2-col, headline, CTAs, phone mockup card)
- [ ] Stats bar (dark background, 4 figures)
- [ ] How It Works (6 stage cards with connecting line)
- [ ] Featured Cat Profile — Winter's story + Adoption Card UI
- [ ] 3 Roles section (dark background, 3 cards)
- [ ] Happy Tails Before/After gallery grid
- [ ] Email waitlist CTA section (golden background)
- [ ] Footer (4-column)
- [ ] Scroll animations via IntersectionObserver
- [ ] Full mobile responsiveness

---

## 📝 Copy Notes

- **Tone**: Warm, hopeful, emotionally resonant — not clinical. Like a great charity campaign that also happens to be a tech product.
- **Action verbs**: "rescue", "reunite", "fly", "match", "save"
- **Always refer to cats as individuals**, not "animals" or "pets" — they have names, stories, and personalities
- **The word "Flight Parent"** should appear naturally in the copy — it's the core concept that makes HopeTails unique

---

*End of specification. Build the full page as a single `index.html` file with embedded CSS and JS.*
