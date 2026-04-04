# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Status

**HopeTails** — platform connecting animal rescuers, international travelers ("Flight Parents"), and adopters to coordinate cat rescues across borders.

**Tagline**: *Saving lives, one flight at a time.*

- **Landing page** (`index.html`) — **implemented and deployed**. See `LANDING_PAGE.md` for the full technical reference.
- **Mobile App** (React Native + Firebase) — **not yet started**. Spec in `hopetails_ai_spec.md`.

## Deliverables

1. **Landing Page** — Single `index.html`, no build step, deployed via Vercel
2. **Mobile App** — React Native (Expo) + Firebase (auth, Firestore, Storage), Google Maps, Stream Chat

## Landing Page

**Full reference**: `LANDING_PAGE.md` — covers every section, all CSS classes, JavaScript blocks, image files, breakpoints, and known issues. Read it before editing `index.html`.

**Design references**: `.firecrawl/` — saved Apple product page HTML files used as design inspiration (Apple Card, Apple Pay, iPhone showcase, etc.). Reference these when matching layout patterns.

**Specs**: `hopetails_landing_page_spec.md` / `hopetails_landing_spec_v2.md` — original landing page briefs. `hopetails_ai_spec.md` — full mobile app spec.

### Deploy
```bash
git add <changed files>
git commit -m "..."
git push   # Vercel auto-deploys from main
```
Always `git add` new image files explicitly — untracked images won't deploy.

### Design tokens (actual, from `index.html`)
```css
--ink:            #0D0D0B   /* near-black, headings, dark sections */
--paper:          #FAF7F2   /* warm off-white, page background */
--ember:          #E8622A   /* primary accent — CTAs, eyebrows */
--ember-soft:     #F5936A
--sand:           #C9B99A
--sage:           #7A9E87
--sky-mist:       #B8D0DC
--text-secondary: #5A5550
--text-muted:     #9A9188
```

Fonts: `Playfair Display` (headings, serif, italic-heavy) + `Instrument Sans` (body, weight 300/500).

### Known issues (from `LANDING_PAGE.md`)
1. **Winter's Story section** — flagged for polish pass.
2. **App showcase arc** — nth-child selectors only explicitly handle `first-child`, `nth-child(2)`, and `last-child`; verify phones 3–5 visually.

### Edit pitfalls
- **Smart quotes and em-dashes** (`"`, `"`, `—`) break the Edit tool's string matching. Use Python for edits touching those characters:
  ```bash
  python3 -c "f=open('index.html');c=f.read();f.close();c=c.replace(OLD,NEW);f=open('index.html','w');f.write(c);f.close()"
  ```
- **"File modified since read"** Edit errors: same Python workaround above.

---

## Mobile App (not yet built)

### Tech Stack
- React Native with Expo
- Firebase (Firestore, Auth, Storage)
- Auth: Email/password + Google + Apple
- Google Maps API
- Stream Chat API (3-way: Volunteer + Traveler + Adopter)

### Core: 6-Stage State Machine on `CatProfile`

Stage 5 cannot begin until Stage 2 (Documents) AND Stage 3 (Funds) are both "Verified."

| Stage | Name |
|-------|------|
| 1 | Create Profile — photos/video + GPS → shareable Adoption Card |
| 2 | Adopter Match & Logistics — auto-generates country-specific document requirements |
| 3 | Fundraising Integration — goal tracker UI; external links only (no internal ledger V1) |
| 4 | Travel Companion Match — travelers post itineraries; system matches + opens 3-way chat |
| 5 | Live Journey Milestones — media at 4 checkpoints: Prep → Handover → Transit/Arrival → The Meeting |
| 6 | Happy Tail Gallery — Stage 1 rescue photo vs. Stage 5 new-life photo |

### Data Models
```typescript
interface CatProfile {
  id: string;
  status: 1 | 2 | 3 | 4 | 5 | 6;
  origin: FirebaseFirestore.GeoPoint;
  destination: FirebaseFirestore.GeoPoint;
  media: string[];     // Firebase Storage URLs
  documents: string[]; // Firebase Storage URLs (PDFs)
}

interface FlightItinerary {
  id: string;
  travelerID: string;
  date: FirebaseFirestore.Timestamp;
  airline: string;
  route: string;
}

interface UserProfile {
  id: string; // Matches Firebase Auth UID
  role: 'Volunteer' | 'Adopter' | 'Traveler' | 'RouteExpert';
  authProvider: 'email' | 'google' | 'apple';
}
```

### Build order (per spec)
1. Auth routing (email/password, Google, Apple)
2. Tab navigation (Dashboard, Map, Messages, Profile)
3. MapView integration
4. Firestore schema and rules
5. 6-stage state machine logic
6. "Before & After" Happy Gallery component (Stage 6)
