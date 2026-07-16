# Version 4 Release Notes & Update History

### 4.1.0 - July 2026
v4.1.0

Bug fixes
- Champion badge progression now correctly counts quested burgers — previously only owned burgers were counted, meaning questers couldn't progress past Pebble Badge
- Weekly burger count in the Notifications tab now includes quested burgers
- Average score in Notifications tab now includes quested burgers
- Badge backfill updated to wait for questedEntries to load before running, eliminating race condition where quested burgers weren't available in time
- Removed champion badge check from quested snapshot listener — was firing on every app launch and could cause repeat badge toasts in some conditions
- Added retry logic to earnedIds Firestore fetch in both checkAndAwardBadges and checkAndAwardChampionBadges to handle cold cache on reinstall
- Backfill key bumped v4 → v5 to trigger re-run for existing users

### 4.0.0 - July 2026
v4.0.0

Burger Champion (Story tab)
- New progression system: 8 Passport Stamps → Burger Council (4 badges) → Champion badge
- Linear gating — each badge only unlocks once the previous one is earned
- Burger Council locked until all 8 stamps are complete
- Champion badge requires all 12 + a perfect 10 score
- Badges shown as a grid in a new Story tab on the Passport screen (alongside existing Stamps and Rewards tabs)
- Tapping any badge shows name, description, requirement, and earned status
- Locked badges show ??? until unlocked
- Season 1 branding — designed to expand with future seasons
- Backfill runs on first app open after update — existing users will have eligible badges awarded automatically

Drafts
- Save as Draft button in NewEntryView header (greyed out until restaurant, city and country populated)
- Drafts stored locally on device via DraftManager (UserDefaults)
- All selected photos saved with the draft and restored on reopen
- Drafts shown above Recent Burgers on Home tab with photo thumbnail, title, subtitle and saved timestamp
- Tap to reopen and continue editing — all fields, scores and photos restored
- Trash button with confirmation alert to delete a draft
- Draft auto-deleted on successful burger submission

Explore
- Quested burgers show a 👥 Quested amber pill on the top-right of the hero image
- Detection uses storedAverageGroupScore vs myWeightedScore diff — works even when questerScores subcollection isn't loaded in the paginated feed
- storedAverageGroupScore now read from Firestore in parseSingleEntry and stored on BurgerEntry

Image quality
- Upload max dimension raised 1080 → 1440px
- Upload compression raised 0.5 → 0.85 (fallback 0.3 → 0.72)
- Cache storage quality raised 0.75 → 0.92 (resized: 0.88)
- Hero images in Explore now load at native screen scale (UIScreen.main.bounds.width × scale) instead of fixed 400pt
- Image decode moved off main thread via ImageCache.getAsync()
- Explore hero images prefetched at display width for first 10 entries on feed load

Performance
- Explore scroll jitter reduced: background image decode, 0.3s debounce on loadLikeState Firestore reads
- ExploreCard hero images use loadCachedResized instead of full-res

Recent Burgers
- Home tab now merges firestoreManager.entries + firestoreManager.questedEntries sorted by date

Photo step (NewEntryView)
- All photos now use consistent square cells via GeometryReader + aspectRatio(1)
- Drag to reorder replaced with native onDrag/onDrop (PhotoDropDelegate) — gives standard iOS hold-lift-drag feel
- Add button is same size as photo cells

Rewards tab
- Career category renamed from Story Mode
- champion BadgeCategory excluded from Rewards tab ForEach (was showing empty Burger Champion 0/0 section)
- Badge summary count excludes champion badges

Misc
- BadgeBackfill key bumped v3 → v4 to trigger champion badge check for existing users on first open
