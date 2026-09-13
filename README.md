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
- [Platform Support](#platform-support)
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
- All scores visible side by side in burger detail view — a compact comparison table when more than one person has scored, so every category is scannable across everyone at a glance
- Scores animate in on open rather than appearing instantly

### 🌍 Explore
- Public burger feed from all users
- Filter to friends only
- Search by restaurant, city or country
- Like burgers with a heart button — owner gets push notification
- Comment on burgers directly from the feed
- Tap profile icons to view friend profiles or send friend requests
- Map view showing all public entries globally
- On iPad, the feed is capped at a comfortable reading width and centered rather than stretched edge-to-edge across the full screen

### 💬 Comments
- Comment on any public burger, with one level of threaded replies
- Like a comment, and see who liked it (with the same friend/add-friend navigation as everywhere else)
- Tap a commenter's avatar or username to view their profile — straight to their full profile if you're already friends, or an add-friend prompt if not
- Client-side profanity filter censors flagged words before posting; a server-side Cloud Function re-checks every comment as an authoritative backstop, so it can't be bypassed by a modified client
- Push notifications for: someone commenting on your burger, someone replying to your comment, someone liking your comment — each individually toggleable in Settings
- Comment counts are tracked server-side (Cloud Functions), not client-side, so they can't drift out of sync regardless of who's commenting

### 🛡️ Privacy & Safety
- **Report** any comment (spam, harassment, inappropriate content, or other) — reports are reviewed directly by the developer via the Firebase Console and aren't visible to any user, including the reporter
- **Block** a user — hides their comments from you immediately, and cleanly ends any existing friendship or pending friend request in either direction
- **Manage blocks** from Settings → Privacy & Safety → Blocked users, with a one-tap unblock
- Burger owners can delete any comment on their own burgers (not just their own comments), for moderating reported content
- Direct **Contact support** link from Settings

### 👥 Friends / Questers
- Search users by username
- Send and accept friend requests
- View friends' public burger profiles with map and gallery
- Private burger count shown on friend profiles (count only, content hidden)
- Swipe to remove friends

### 🔔 Notifications
- Friend request received / accepted
- Invited to score a burger
- Quester submitted their score
- Someone liked your burger
- A friend logged a new public burger
- Someone commented on your burger, replied to your comment, or liked your comment
- In-app notification centre showing all of the above, plus pending scores and friend requests, with a badge count on the tab

### 🛂 Passport
- Visual passport-style record of all countries visited for burgers

### 📊 Stats
- Total burger count, countries visited, questers
- Breakdown by category scores
- Tier system based on burger count

### ⚙️ Settings
- Edit profile (username, bio, profile picture, home currency)
- Notification preferences, individually toggleable per notification type
- Privacy & Safety: blocked users, contact support
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
- Node.js (for deploying Cloud Functions)

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/burgerpassport.git
   cd burgerpassport
   ```

2. Install dependencies via Swift Package Manager in Xcode (File → Add Package Dependencies):
   - `firebase-ios-sdk`

3. Add your `GoogleService-Info.plist` to the project root (not included in repo).

4. Deploy Firestore security rules:
   ```bash
   firebase deploy --only firestore:rules
   ```
   (or paste `firestore.rules` directly into the Firebase Console → Firestore → Rules)

5. Deploy Cloud Functions:
   ```bash
   cd functions
   npm install
   firebase deploy --only functions
   ```

6. Build and run on a device or simulator.

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

### Commenting on a Burger
1. Tap the comment icon on any public burger (Explore or burger detail view)
2. Type a comment and post — or tap **Reply** under an existing comment
3. Tap the heart to like a comment, or the like count to see who liked it
4. Tap "•••" on a comment to **Report** it or **Block** the person who posted it

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
│   └── Models.swift                 # BurgerEntry, QuesterScore, Comment,
│                                     # CommentNotification, Friend, etc.
├── Managers/
│   ├── FirestoreManager.swift       # Firestore reads/writes, real-time listeners,
│   │                                 # comment CRUD, deduplicated combined-entries helper
│   ├── AuthManager.swift            # Firebase Auth (email + Apple Sign In)
│   ├── UserProfileManager.swift     # Profile, friends, friend requests, blocked users
│   ├── StorageManager.swift         # Firebase Storage photo uploads
│   ├── NetworkMonitor.swift         # NWPathMonitor for offline detection
│   ├── CacheManager.swift           # UserDefaults persistence for offline cache
│   └── ProfanityFilter.swift        # Client-side comment censoring
├── Views/
│   ├── Home/                        # Map, bottom panel, profile header, friends
│   ├── Entry/                       # Burger logging flow
│   ├── Detail/                      # Burger detail, edit, scores, comments entry point
│   ├── Explore/                     # Public feed with likes, comments, map view
│   ├── Comments/
│   │   └── CommentsSheet.swift      # Comment list, replies, likers, report/block UI
│   ├── Friends/                     # Friend profile, blocked users list
│   ├── Activity/                    # Notifications, friend requests, pending scores
│   ├── Questing/                    # Score submission flow with confirmation
│   ├── Auth/                        # Sign in, sign up, Apple Sign In
│   └── Shared/                      # Reusable form components, offline banner, etc.
└── functions/
    └── index.js                     # Firebase Cloud Functions (10 triggers)
```

---

## Firebase Setup

### Firestore Collections

```
burgers/{burgerId}
  ├── questerScores/{questerUid}
  ├── likes/{userId}
  └── comments/{commentId}
        └── likes/{userId}

users/{userId}
  ├── pendingScores/{burgerId}
  ├── friends/{friendId}
  ├── friendRequests/{requestId}
  ├── sentRequests/{requestId}
  ├── blockedUsers/{blockedUid}
  ├── likeNotifications/{notifId}
  └── commentNotifications/{notifId}

usernames/{username}          # Username uniqueness reservation

reports/{reportId}            # Comment reports — create-only from clients,
                               # readable only via the Firebase Console
```

### Firestore Security Rules
The current `firestore.rules` enforces:
- Authenticated users can read/write their own user document
- Authenticated users can read public burgers and their own burgers
- Burger likes and quester scores: any authenticated user may read/write
- Comments: only the author can create a comment as themselves (with a
  500-character server-side cap); clients may only ever touch the
  `likeCount` field afterward; only the comment's author *or* the burger's
  owner can delete it
- Comment likes: anyone can read, but only your own like doc is writable by you
- `commentNotifications` / `likeNotifications`: the *other* person writes into
  your subcollection when they comment/like, so these allow any signed-in
  write, restricted to owner-only read/delete
- `reports`: create-only, by the reporter, for themselves — never readable,
  updatable, or deletable from the client

See the full `firestore.rules` for exact conditions.

### Storage Rules
- Authenticated users can upload to `burgers/{burgerId}/` and `users/{userId}/`

---

## Push Notifications

Ten Cloud Function triggers in `functions/index.js`:

| Trigger | Path | Notifies |
|---|---|---|
| `onFriendRequestSent` | `users/{userId}/friendRequests/{id}` | Recipient |
| `onFriendRequestAccepted` | `users/{userId}/friends/{friendId}` | Original requester |
| `onPendingScoreCreated` | `users/{questerUid}/pendingScores/{id}` | Quester |
| `onQuesterScoreSubmitted` | `burgers/{id}/questerScores/{uid}` | Burger owner |
| `onBurgerLiked` | `burgers/{id}/likes/{uid}` | Burger owner |
| `onBurgerUnliked` | `burgers/{id}/likes/{uid}` (delete) | — (decrements likeCount only) |
| `onPublicBurgerCreated` | `burgers/{id}` | Owner's friends, for new public burgers |
| `onCommentCreated` | `burgers/{id}/comments/{commentId}` | — (profanity re-check + increments commentCount) |
| `onCommentDeleted` | `burgers/{id}/comments/{commentId}` (delete) | — (decrements commentCount, transaction-safe) |
| `onCommentNotificationCreated` | `users/{userId}/commentNotifications/{id}` | Recipient (comment/reply/like on comment) |

FCM tokens are saved to `users/{userId}.fcmToken` on each app launch. Each notification type respects a per-user preference toggle in `users/{userId}.notificationPreferences`.

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

## Platform Support

BurgerPassport is a universal app, supporting both iPhone and iPad. On iPad:
- Share sheets (burger detail, Explore, friend profile, invite-a-friend) are
  anchored correctly for iPad's popover-based presentation — a raw
  `UIActivityViewController` presentation without this anchor crashes
  outright on iPad, so this is a functional requirement, not just polish
- The Explore feed is capped at a comfortable reading width and centered,
  rather than stretching full-width across a much larger screen

---

## Known Limitations

- **Coordinates:** Entries logged without selecting a restaurant from search results use city/country geocoding, falling back to country centroid if city geocoding fails
- **Exchange rates:** Currency conversion uses hardcoded approximate rates — not live
- **Offline cache:** Writes are blocked offline; new entries require a connection
- **Friend profiles:** Only public burgers are visible — private entries show a count only
- **Comment moderation:** Reports are reviewed manually via the Firebase Console, not through an in-app moderation dashboard
- **Comment threading:** Replies are one level deep only (no nested reply chains), by design

---

## Version History

see release-notes-v{release}

---

## License

Private — all rights reserved.
