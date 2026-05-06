# 🍔 BurgerPassport

**Track every patty, everywhere.**

BurgerPassport is an iOS app for logging, rating and sharing burger experiences around the world. Built with SwiftUI and Firebase, it lets you build a personal burger journal, score each burger across multiple categories, quest with friends, and explore what others are eating globally.

---

## Table of Contents

- [Features](#features)
- [Getting Started](#getting-started)
- [How to Use](#how-to-use)
- [Architecture](#architecture)
- [Firebase Setup](#firebase-setup)
- [Push Notifications](#push-notifications)
- [Tech Stack](#tech-stack)
- [Known Limitations](#known-limitations)

---

## Features

### 🗺️ Home
- Full-screen world map showing all your logged burgers as pins
- Bottom panel with your profile, stats and recent burgers
- Tap any map pin to preview the burger entry
- Overlapping pins in the same city are spread in a circle so all are tappable

### 📝 Logging a Burger
- 7-step card flow: restaurant → burger name → photo → price → questers → notes → scoring
- Restaurant search powered by MapKit — finds real restaurants with address suggestions
- City/country validation via CLGeocoder — blocks nonsense entries
- Coordinates saved from restaurant search or geocoded from city/country
- Weighted scoring system across 6 categories:
  - Overall appearance (5%)
  - Bun (20%)
  - Meat / patty (20%)
  - Toppings (20%)
  - Sauces (20%)
  - Holdability (15%)
- Categories can be excluded — weights redistribute automatically
- Live weighted average updates as you drag sliders
- Public/private toggle — public entries appear in the Explore feed

### 🎯 Questing
- Invite friends to score the same burger independently
- Questers can't see the owner's scores until they submit their own
- Confirmation screen after submitting with the final score
- All scores visible side by side in burger detail view

### 🌍 Explore
- Public burger feed from all users
- Filter to friends only
- Search by restaurant, city or country
- Like burgers with a heart button — owner gets push notification
- Tap profile icons to view friend profiles or send friend requests
- Map view showing all public entries globally

### 👥 Friends / Questers
- Search users by username
- Send and accept friend requests
- View friends' public burger profiles with map and gallery
- Private burger count shown on friend profiles (count only, content hidden)
- Swipe to remove friends

### 🔔 Notifications
- Friend request received
- Friend request accepted
- Invited to score a burger
- Quester submitted their score
- Someone liked your burger
- In-app notification centre showing pending scores and friend requests

### 🛂 Passport
- Visual passport-style record of all countries visited for burgers

### 📊 Stats
- Total burger count, countries visited, questers
- Breakdown by category scores
- Tier system based on burger count

### ⚙️ Settings
- Edit profile (username, bio, profile picture, home currency)
- Appearance mode (light / dark / system)
- Delete account

### 📶 Offline Support
- Cached data loads instantly when offline (burgers, explore feed, quested entries)
- Offline banner shown at top of screen
- Write actions (logging, editing, liking) blocked when offline
- Auto-refreshes all data when connection restored

---

## Getting Started

### Prerequisites

- Xcode 15+
- iOS 17+ deployment target
- Firebase project with Firestore, Auth, Storage and Cloud Messaging enabled
- CocoaPods or Swift Package Manager for Firebase dependencies

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/burgerpassport.git
   cd burgerpassport
   ```

2. Install dependencies via Swift Package Manager in Xcode (File → Add Package Dependencies):
   - `firebase-ios-sdk`

3. Add your `GoogleService-Info.plist` to the project root (not included in repo).

4. Deploy Cloud Functions:
   ```bash
   cd functions
   npm install
   firebase deploy --only functions
   ```

5. Build and run on a device or simulator.

---

## How to Use

### Signing Up
1. Open the app and tap **Get started**
2. Choose **Sign up with Apple** or **Get started with email**
3. Pick a username (3–20 characters, letters/numbers/underscores)
4. Add a profile photo (or skip)

### Logging a Burger
1. Tap **Log a burger** on the home screen
2. Search for the restaurant by name — select from suggestions to pin the exact location
3. Enter the burger name
4. Add a photo (required)
5. Optionally enter the price, invite questers, and add notes
6. Score across up to 6 categories using the sliders
7. Tap **Submit** — a confirmation screen shows your final score

### Inviting Questers
1. On step 5 of the logging flow, tap **Add a quester**
2. Select from your friends list
3. Your quester will receive a push notification
4. They score independently in the **Notifications** tab
5. Both scores appear side by side in the burger detail view

### Adding Friends
1. Tap **Friends** on the home screen stats row
2. Tap the **+** icon in the top right
3. Search by username and tap **Add**
4. Your friend receives a notification and can accept from their Notifications tab

### Making Entries Public
- Toggle **Make this entry public** on step 5 of the logging flow
- Or tap the **Private / Public** pill on any burger detail view to toggle
- Public entries appear in the Explore feed for all users

---

## Architecture

```
BurgerPassport/
├── App/
│   └── burgermirApp.swift          # App entry point, Firebase init, FCM setup
├── Models/
│   ├── Models.swift                # BurgerEntry, QuesterScore, Friend, etc.
│   └── ScoringCategory             # In NewEntryView.swift
├── Managers/
│   ├── FirestoreManager.swift      # All Firestore reads/writes, real-time listeners
│   ├── AuthManager.swift           # Firebase Auth (email + Apple Sign In)
│   ├── UserProfileManager.swift    # Profile, friends, friend requests
│   ├── StorageManager.swift        # Firebase Storage photo uploads
│   ├── NetworkMonitor.swift        # NWPathMonitor for offline detection
│   └── CacheManager.swift          # UserDefaults persistence for offline cache
├── Views/
│   ├── Home/
│   │   └── HomeView.swift          # Map, bottom panel, profile header, friends
│   ├── Entry/
│   │   └── NewEntryView.swift      # 7-step burger logging flow
│   ├── Detail/
│   │   ├── BurgerDetailView.swift  # Full burger view with scores, map, likes
│   │   ├── EditBurgerView.swift    # Edit scores/notes with sliders
│   │   └── ReadOnlyBurgerDetailView.swift
│   ├── Explore/
│   │   └── ExploreView.swift       # Public feed with likes, map view
│   ├── Friends/
│   │   └── FriendProfileView.swift # Friend's burger map and list
│   ├── Activity/
│   │   └── ActivityView.swift      # Notifications, friend requests, pending scores
│   ├── Questing/
│   │   └── QuesterScoringView.swift # Score submission flow with confirmation
│   ├── Auth/
│   │   └── AuthView.swift          # Sign in, sign up, Apple Sign In
│   └── Shared/
│       ├── SharedFormComponents.swift
│       ├── OfflineBanner.swift
│       ├── MapPinOffsetHelper.swift
│       └── KeyboardDismissModifier.swift
└── functions/
    └── index.js                    # Firebase Cloud Functions (5 notification triggers)
```

---

## Firebase Setup

### Firestore Collections

```
burgers/{burgerId}
  ├── questerScores/{questerUid}
  └── likes/{userId}

users/{userId}
  ├── pendingScores/{burgerId}
  ├── friends/{friendId}
  └── friendRequests/{requestId}

usernames/{username}          # Username uniqueness reservation
```

### Firestore Security Rules
Ensure your `firestore.rules` allows:
- Authenticated users to read/write their own user document
- Authenticated users to read public burgers (`isPublic == true`)
- Authenticated users to read/write their own burger documents
- Authenticated users to read/write subcollections they own

### Storage Rules
- Authenticated users can upload to `burgers/{burgerId}/` and `users/{userId}/`

---

## Push Notifications

Five Cloud Function triggers in `functions/index.js`:

| Trigger | Path | Notifies |
|---|---|---|
| `onFriendRequestSent` | `users/{userId}/friendRequests/{id}` | Recipient |
| `onFriendRequestAccepted` | `users/{userId}/friends/{friendId}` | Original requester |
| `onPendingScoreCreated` | `users/{questerUid}/pendingScores/{id}` | Quester |
| `onQuesterScoreSubmitted` | `burgers/{id}/questerScores/{uid}` | Burger owner |
| `onBurgerLiked` | `burgers/{id}/likes/{uid}` | Burger owner |

FCM tokens are saved to `users/{userId}.fcmToken` on each app launch.

Deploy with:
```bash
firebase deploy --only functions
```

---

## Tech Stack

| Layer | Technology |
|---|---|
| UI | SwiftUI |
| Authentication | Firebase Auth (email + Apple Sign In) |
| Database | Firebase Firestore |
| Storage | Firebase Storage |
| Push Notifications | Firebase Cloud Messaging |
| Backend | Firebase Cloud Functions (Node.js) |
| Maps | MapKit / MKLocalSearch |
| Geocoding | CLGeocoder |
| Networking | NWPathMonitor |
| Purchases | StoreKit (RevenueCat) |
| Image Caching | Custom `ImageCache` (NSCache) |
| Offline Cache | UserDefaults (JSON encoded) |

---

## Known Limitations

- **Coordinates:** Entries logged without selecting a restaurant from search results use city/country geocoding, falling back to country centroid if city geocoding fails
- **Exchange rates:** Currency conversion uses hardcoded approximate rates — not live
- **Explore feed:** Loads the 50 most recent public entries — no pagination yet
- **Offline cache:** Writes are blocked offline; new entries require a connection
- **Friend profiles:** Only public burgers are visible — private entries show a count only

---

## Version History

### 1.0 (Build 3) — May 2026
Initial TestFlight release.

- Full burger logging flow with weighted scoring
- Questing system with push notifications
- Explore feed with likes
- Friends system with friend requests
- Offline support with cached data
- City validation via geocoder
- Apple Sign In + email authentication
- Public/private burger toggle
- Passport view

---

## License

Private — all rights reserved.
