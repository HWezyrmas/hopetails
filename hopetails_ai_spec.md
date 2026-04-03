# HopeTails: AI Application Specification

## 1. Project Overview
- **Name**: HopeTails
- **Tagline**: Saving lives, one flight at a time.
- **Concept**: A global, decentralized platform connecting animal rescuers, international travelers, and adopters to digitize the "Flight Parent" process.

## 2. Tech Stack & Architecture
- **Frontend**: React Native (Expo recommended for rapid development).
- **Backend & Database**: Firebase (Firestore for data, Firebase Auth, Firebase Storage for media/documents).
- **Authentication**: Email/Password and social logins (Google & Apple).
- **Mapping & Location**: Google Maps API for geolocation and map views.
- **In-App Messaging**: Stream Chat API for 3-way secure communication.
- **Core Architecture**: Dynamic Logistics Engine. No hard-coded routes. The app should allow users to select any origin/destination city or country, generating requirements dynamically.

## 3. User Roles & Onboarding
Users select their primary role during the onboarding flow. This selection is saved to their profile:
1. **Volunteers (Rescuers)**: Create cat profiles, manage logistics.
2. **Adopters**: Apply to adopt, track flight progress.
3. **Travelers (Flight Parents)**: Post flight itineraries, match with cats needing transit.
4. **Route Experts (Power Users)**: Contribute specific rules for complex corridors (e.g., UAE to UK).

## 4. The 6-Stage Workflow (The "Happy Path")
**Development Priority - Strict State Machine**: The app must build logic that prevents moving to Stage 5 until Stage 2 (Docs) and Stage 3 (Funds) are marked as "Verified."

- **🟢 Stage 1: Create Profile (The Identity)**
  - Input: 1-3 Photos + 1 Video.
  - Feature: "Storyteller UI"—turning raw data into a beautifully designed, shareable "Adoption Card".
  - Global Tagging: GPS-based (Google Maps API) or manual location entry.

- **🟢 Stage 2: Adopter Match & Logistics**
  - Action: Volunteer confirms an Adopter.
  - Feature: Requirement Generator based on origin/destination rules (baseline: Microchip, Rabies, Health Cert).

- **🟢 Stage 3: Fundraising Integration**
  - Feature: Goal Tracker UI (e.g., a real-time progress bar: "Flight & Vet costs: 65% funded").
  - Action: External link buttons to GoFundMe/PayPal (no internal ledger functionality for V1).

- **🟢 Stage 4: Travel Companion Match**
  - Action: Travelers post their "Flight Itinerary" (Date, Airline, Route).
  - Automation: System notifies Volunteers of route matches.
  - Communication: Open a 3-way secure chat (Volunteer + Traveler + Adopter) using Stream Chat.

- **🟢 Stage 5: Live Journey Milestones (The "Proof of Life" log)**
  - Requires media uploads at 4 specific global milestones:
    1. **Preparation**: Day before travel.
    2. **Handover**: Airport departure gate.
    3. **Transit/Arrival**: Landing at destination.
    4. **The Meeting**: Settling into the new home.

- **🟢 Stage 6: The "Happy Tail" Gallery**
  - Action: Once "Settled" is confirmed, profile moves to the global gallery.
  - Feature: "Before & After" Visual Component. Pulls the original rescue photo (Stage 1) side-by-side with the "New Life" photo (Stage 5) to create a wall of impact.

## 5. Navigation & User Experience (UX)
- **Vibe & Design System**: Think "Airbnb for pets." Clean, modern, ample whitespace, rounded corners, and premium card-based layouts. 
- **Color Palette**: Bright dreamy pastels.
- **Global Map View**: Discover cats needing flights/funds based on a world map.
- **The "Flight Board"**: A list of upcoming travelers looking for a rescue passenger.
- **My Journeys**: A card-based dashboard tracking the 6 stages for any active rescue.
- **Document Vault**: A secure place to upload and view PDFs (passports, health certificates).

## 6. Data Model Strategy
```typescript
interface CatProfile {
  id: string; // Document ID
  status: 1 | 2 | 3 | 4 | 5 | 6; // Enum enforcing the strict state machine
  origin: FirebaseFirestore.GeoPoint;
  destination: FirebaseFirestore.GeoPoint;
  media: string[]; // Firebase Storage URLs
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

## 7. AI Assistant Hand-off Command
> **Developer AI Instructions**: 
> "Act as a Senior React Native Developer. Use this specification to build the Hopetails mobile app using React Native (Expo) and Firebase. Focus first on setting up the Foundation (Auth routing, Tab Navigation, and MapView) and the Database Architecture. Prioritize the strict 6-Stage Workflow logic (State Machine) for the `CatProfile` entity, and ensure that when a cat reaches the final stage, its profile is automatically rendered in a 'Before & After' Happy Gallery component."
