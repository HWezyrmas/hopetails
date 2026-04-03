# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Status

**HopeTails** is in the pre-implementation phase. The repository contains two specification documents and no implementation code yet:

- `hopetails_ai_spec.md` — Full mobile app specification
- `hopetails_landing_page_spec.md` — Landing page specification

## What We're Building

**HopeTails** is a platform connecting animal rescuers, international travelers ("Flight Parents"), and adopters to coordinate cat rescues across international borders.

**Tagline**: *Saving lives, one flight at a time.*

Two deliverables:
1. **Mobile App** — React Native (Expo) + Firebase
2. **Landing Page** — Single `index.html` with embedded CSS/JS, no build step

## Tech Stack

### Mobile App
- **Framework**: React Native with Expo
- **Backend**: Firebase (Firestore, Auth, Storage)
- **Auth**: Email/password + Google + Apple sign-in
- **Maps**: Google Maps API
- **Messaging**: Stream Chat API (3-way: Volunteer + Traveler + Adopter)

### Landing Page
- Plain HTML + CSS + Vanilla JS — single `index.html` file
- Fonts: `DM Serif Display` (headings) + `DM Sans` (body) from Google Fonts
- Icons: Inline SVGs or Lucide via CDN
- No external CSS frameworks — all styles written from scratch

## Core Architecture: 6-Stage State Machine

The central logic is a strict state machine on the `CatProfile` entity. **Stage 5 cannot begin until Stage 2 (Documents) AND Stage 3 (Funds) are both marked "Verified."**

| Stage | Name | Key Feature |
|-------|------|-------------|
| 1 | Create Profile | Photos/video + GPS → generates shareable "Adoption Card" |
| 2 | Adopter Match & Logistics | Confirms adopter; auto-generates country-specific document requirements |
| 3 | Fundraising Integration | Goal tracker UI; external links only (no internal ledger in V1) |
| 4 | Travel Companion Match | Travelers post flight itineraries; system matches + opens 3-way chat |
| 5 | Live Journey Milestones | Media uploads at 4 checkpoints: Prep → Handover → Transit/Arrival → The Meeting |
| 6 | Happy Tail Gallery | "Before & After" component: Stage 1 rescue photo vs. Stage 5 new life photo |

## Data Models

```typescript
interface CatProfile {
  id: string;
  status: 1 | 2 | 3 | 4 | 5 | 6; // The state machine enum
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

## User Roles

- **Volunteers (Rescuers)**: Create/manage cat profiles and logistics
- **Adopters**: Apply to adopt, track flight progress
- **Travelers (Flight Parents)**: Post flight itineraries, get matched with rescue cats
- **Route Experts**: Contribute corridor-specific document rules (e.g., UAE → UK)

## Mobile App Navigation

- Tab navigation: Dashboard, Map (global), Messages, Profile
- **My Journeys**: Card-based dashboard for active rescues showing 6-stage progress
- **Flight Board**: List of upcoming travelers looking for a rescue passenger
- **Document Vault**: Secure PDF upload/view (health certs, passports)
- **Dynamic Logistics Engine**: No hard-coded routes — origin/destination document requirements generated dynamically

## Landing Page Design System

```css
:root {
  --cream: #FDF8F2;
  --charcoal: #1A1A2E;
  --sage: #8CB8A8;
  --blush: #F2A7A7;
  --sky: #A8C8E8;
  --golden: #F5C842;       /* CTA button color */
  --golden-dark: #D4A800;
  --lavender: #C5B8E8;
  --light-gray: #F5F0EB;
  --mid-gray: #6B6B7A;
  --dark-section: #1A1A2E;
}
```

**Aesthetic**: "Airbnb for pets" — clean, premium, generous whitespace, `border-radius: 16px`, card-based layouts, subtle shadows (`box-shadow: 0 4px 24px rgba(0,0,0,0.08)`).

Landing page sections: Sticky Nav → Hero → Stats Bar → How It Works (6 stages) → Winter's Story (featured cat) → Three Roles → Happy Tails Gallery → Email Waitlist → Footer.

## Recommended First Steps (Mobile App)

Per the spec's developer hand-off instructions, build in this order:
1. Auth routing (email/password, Google, Apple)
2. Tab navigation structure
3. MapView integration
4. Firestore schema and rules
5. 6-stage state machine logic for `CatProfile`
6. "Before & After" Happy Gallery component (Stage 6)
