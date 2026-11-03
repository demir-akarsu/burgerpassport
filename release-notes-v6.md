Version 6 Release Notes & Update History

### 6.0.1 - November 2026 (security update)
v6.0.1

---

## 🔒 Security

- Updated the Firebase SDK (Firestore) to the latest patched release in
  response to Google's security notice about compromised eMudhra
  intermediate certificate authorities. The affected SDK versions compile
  their TLS root certificate bundle into the app itself, so the fix can
  only reach users through an app update — updating to this version is
  strongly recommended

---

## ⚙️ Under the Hood

- Firebase iOS SDK upgraded from 12.12.1 to 13.1.1 (Firebase's recommended
  fix; the 12.19.3 backport was the alternative). Related Swift Package
  dependencies were updated alongside it

---

### 6.0.0 - November 2026
v6.0.0

---

## 🆕 New Features

**Featured Restaurants**
- A new horizontally-scrolling "Promoted Restaurants" reel sits at the top
  of the Explore feed, spotlighting hand-picked restaurants — manually
  curated, not a paid/automated placement
- Each card can carry an "Our Pick" or "Sponsored" badge
- Tapping a card filters Explore straight to every burger logged at that
  restaurant, across all of its branches worldwide, or scoped to a single
  branch
- A restaurant can be featured worldwide or tied to one specific city
- Featured restaurants can be scheduled with a start/end date, so a
  promotion automatically goes live and expires without manual cleanup
- The reel smoothly shrinks as you scroll down the feed and expands back
  when you scroll to the top, staying out of the way without disappearing
  entirely
- Managed entirely from a new admin-only screen in Settings (visible only
  to the app's admin account) — restaurants are picked by searching burgers
  that have already been logged, rather than typed in by hand, so the
  listing always matches real, existing data

**App Store rating prompt**
- After reaching a logging milestone (3rd, 10th, 25th, 50th, or 100th
  burger), you may be prompted to rate BurgerPassport — shown at most once
  per install, the first time any milestone is reached

---

## 🐛 Bug Fixes

- Fixed Explore search and filters (including tapping a featured
  restaurant) sometimes showing only one or two results with a loading
  spinner that never resolved, until manually pulled to refresh — search
  now always runs against the full, up-to-date set of public burgers
- Fixed a stray loading spinner appearing at the bottom of a filtered
  Explore feed and silently re-fetching an unrelated page of the main feed
  in the background
- Fixed the reply box on a comment ("Replying to @username") occasionally
  closing on its own a couple of seconds after tapping Reply
- Fixed the keyboard sometimes not dismissing when tapping outside a text
  field on My Burgers, including the blank space around the screen title

---

## 🔧 Improvements

- Scrolling Explore while a search or filter is active is noticeably
  smoother — the new featured-restaurants reel no longer recalculates the
  entire feed on every frame of scrolling

---

## ⚙️ Under the Hood

- Promoted-restaurant photos use a dedicated Firebase Storage path and
  rule set, scoped to the admin account, separate from burger photos
- New Firestore composite index supporting the live/active, ordered
  promoted-restaurants query
- Firestore rules updated to restrict writes to the `promotedRestaurants`
  collection to the admin account only
- The featured-restaurants reel's horizontal scrolling is backed directly
  by a native `UIScrollView` (rather than SwiftUI's own horizontal
  `ScrollView`), locking its drag to strictly left/right and eliminating a
  diagonal rubber-banding issue that SwiftUI's own scroll-bounce controls
  couldn't fully suppress
- Removed temporary debug logging left in from diagnosing the comment
  reply-box bug
6.0.0 - November 2026

v6.0.0

🆕 New Features

Featured Restaurants

A new horizontally-scrolling "Promoted Restaurants" reel sits at the top of the Explore feed, spotlighting hand-picked restaurants — manually curated, not a paid/automated placement
Each card can carry an "Our Pick" or "Sponsored" badge
Tapping a card filters Explore straight to every burger logged at that restaurant, across all of its branches worldwide, or scoped to a single branch
A restaurant can be featured worldwide or tied to one specific city
Featured restaurants can be scheduled with a start/end date, so a promotion automatically goes live and expires without manual cleanup
The reel smoothly shrinks as you scroll down the feed and expands back when you scroll to the top, staying out of the way without disappearing entirely
Managed entirely from a new admin-only screen in Settings (visible only to the app's admin account) — restaurants are picked by searching burgers that have already been logged, rather than typed in by hand, so the listing always matches real, existing data

App Store rating prompt

After reaching a logging milestone (3rd, 10th, 25th, 50th, or 100th burger), you may be prompted to rate BurgerPassport — shown at most once per install, the first time any milestone is reached
🐛 Bug Fixes
Fixed Explore search and filters (including tapping a featured restaurant) sometimes showing only one or two results with a loading spinner that never resolved, until manually pulled to refresh — search now always runs against the full, up-to-date set of public burgers
Fixed a stray loading spinner appearing at the bottom of a filtered Explore feed and silently re-fetching an unrelated page of the main feed in the background
Fixed the reply box on a comment ("Replying to @username") occasionally closing on its own a couple of seconds after tapping Reply
Fixed the keyboard sometimes not dismissing when tapping outside a text field on My Burgers, including the blank space around the screen title
🔧 Improvements
Scrolling Explore while a search or filter is active is noticeably smoother — the new featured-restaurants reel no longer recalculates the entire feed on every frame of scrolling
⚙️ Under the Hood
Promoted-restaurant photos use a dedicated Firebase Storage path and rule set, scoped to the admin account, separate from burger photos
New Firestore composite index supporting the live/active, ordered promoted-restaurants query
Firestore rules updated to restrict writes to the promotedRestaurants collection to the admin account only
The featured-restaurants reel's horizontal scrolling is backed directly by a native UIScrollView (rather than SwiftUI's own horizontal ScrollView), locking its drag to strictly left/right and eliminating a diagonal rubber-banding issue that SwiftUI's own scroll-bounce controls couldn't fully suppress
Removed temporary debug logging left in from diagnosing the comment reply-box bug
