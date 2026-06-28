# Version 1 Release Notes & Update History
### 1.4.0 - May 2026
Version 1.4.0

What's New

Quick save in Edit Burger
A Save button now appears in the top-right corner when editing a burger, so you can save your changes from any step without having to scroll through to the end.

Decline quester invites
You can now swipe left on a pending burger score in the Notifications tab to decline it, removing it from your list without having to score it.

Photo reordering
Photos can now be reordered in both the Log and Edit burger flows — hold and drag a thumbnail left or right to change the order. The first photo is always the hero image shown in lists and on the map.

Camera photos preserved when switching to library
Taking a photo with the camera and then adding more from your library no longer removes the camera shot. All photos are now correctly combined up to the 3-photo limit.

Score 10 shown in yellow
A perfect 10 on any scoring category or as a weighted average now displays in bright yellow, making it clearly distinct from the green used for high scores.

Bug Fixes

- Version number in Settings was hardcoded as 1.0 — now reads from the app bundle and updates automatically with each release

### 1.3.0 - May 2026
Bug Fixes
 
- United Kingdom appearing multiple times in Passport and Countries — "England", "UK", "Northern Ireland", "Scotland" and "Wales" now all group as a single United Kingdom stamp and country count
- Deleting a burger now also removes its photos from Firebase Storage — previously only the Firestore document was deleted, leaving orphaned files
- Like notifications in the Notifications tab are now tappable — tap any like notification to open the burger that was liked
- Explore keyboard did not dismiss when tapping the blank space at the top of the screen — fixed using a UIKit navigation bar gesture recogniser
- Private quested burgers were visible on a quester's public profile when viewed by a third party — now correctly hidden; only the burger owner and the quester themselves can see private quested burgers
- Country count on home screen, friend profiles and Stats was inflated when the same country was stored under different names — fixed with the same normalisation as Passport
- Like count and liked state not loading when opening a burger — fixed for both own and others' burgers
- Own burgers showed no like count — now shows a read-only heart with the like count
- Explore Most Liked sort was not ordering correctly — likeCount field was missing on older documents and not being updated on new likes; both now fixed
- Explore Highest/Lowest Score sort was not ordering correctly for quested burgers — averageGroupScore field was not being recalculated after quester scores were submitted; backfill applied to all existing burgers
- Explore profile pictures not loading on first render — fixed a race condition where owner profile image URLs arrived after cards were already drawn

### 1.2.0 - May 2026
What's New
 
Quester full edit
Questers can now edit all 7 steps of a burger — restaurant, photos, price, notes, and their own scores — not just the scoring step. Quester scores are saved separately so the owner's scores are never affected.
 
Group scoring in Explore
The score shown on Explore cards and map pins now reflects the average across the owner and all questers, not just the owner's score. A small "avg" label appears when multiple scores exist.
 
Full-screen photo viewer
Tap any burger photo to view it full screen. Pinch to zoom, double-tap to zoom to a point, swipe between photos, and swipe down to close.
 
Explore pagination
Explore now loads in pages of 20 rather than a fixed 50. Scroll to the bottom and the next page loads automatically. Sorting by Most Recent, Most Liked, Highest Score, or Lowest Score all work correctly against the full dataset — not just what's already loaded.
 
Scroll to top on tab tap
Tapping a tab you're already on now scrolls you back to the top of the list, just like the native iOS behaviour.
 
Image cache
Photos now load from a local disk cache after the first view, making the app significantly faster and usable offline. Cache size is shown in Settings and can be cleared manually.
 
Settings: Storage section
A new Storage section in Settings shows how much disk space the image cache is using and lets you clear it with a single tap.
 
Map pin improvements
Pins now animate with a pulse when tapped, appear faster, and are prefetched so the preview card image is usually already loaded when you tap.
 
Bug Fixes
 
- Quester scores were being saved to the owner's document instead of the quester's own subcollection — fixed
- Quester edit view was pre-filling the owner's scores instead of the quester's own previous scores — fixed
- Burger appearance score showing as 0.0 for questers — caused by Firestore storing whole-number doubles as integers, now handled correctly across all score fields
- Profile pictures on the home screen and settings were not loading from cache — now use the same cached image system as the rest of the app
- Full-screen photo carousel was broken across multiple iterations — rebuilt from scratch in UIKit with reliable layout, working pinch-to-zoom anchored to the touch point, page swiping, and swipe-down dismiss
- Panning a zoomed photo was switching pages instead of moving the image — fixed by disabling the pager scroll while zoomed
- Explore was showing only the owner's score, ignoring questers — fixed
- Explore profile pictures were not loading on first render — fixed a race condition where owner profile URLs arrived after cards were already drawn
- Like count and liked state not showing when opening a burger — fetchLikes was only called on entry change, not on initial open — fixed
- Own burgers showed no like information — now shows a read-only heart with like count
- Map pin tap had a visible delay and jitter — removed artificial delay, moved preview card state into the map view so the parent view no longer re-renders on pin tap
- Empty space at the top of My Burgers after scroll-to-top was added — removed phantom anchor rows, now scrolls to the first real item
- Firestore was fetching quester subcollections for all 50 Explore entries on every load, even those with no questers — now only fetches where needed
- Lowest score removed from Stats view

### 1.1.0 - May 2026
What's New:

- Multiple photos (up to 3) per burger with swipe carousel and tap to enlarge
- Full burger edit - all 7 steps pre-filled with existing data
- Notification preferences - choose which notifications you receive
- Likes in the Notifications tab with swipe to dismiss and clear all
- Like button on friends' burger profiles
- Friend burger notifications - get notified when a friend logs a public burger
- Like count badge on the notifications tab
- Explore filter by Most Recent, Most Liked, and Highest Score
- Explore vegan filter toggle
- Better restaurant search results
- Own burger like counts visible in Explore
- Swipe up from anywhere on home and friend profile panels
- Tap the map to collapse the panel
- Map pins now cluster and are colour-coded by score
- Photos save to camera roll when taken in-app
- Total spent stat in Stats view
- Passport progression bar moved to top
- 10 shows instead of 10.0 on scoring sliders

Bug Fixes:

- Map pinch-to-zoom fixed - no longer intercepted by burger pins
- Preview card now shows correct image when tapping between map pins
- Tap anywhere on map to dismiss pin preview card
- Tapping a pin preview card now opens the burger
- Keyboard dismiss no longer breaks double-tap text selection
- Duplicate friend requests now correctly show "Friend request sent"
- Non-friend quester profile pictures now load correctly
- Restaurant and city search dropdowns now dismiss when tapping away
- App performance significantly improved when viewing profiles with many pins
- Various stability improvements

### 1.0.0 — May 2026
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
