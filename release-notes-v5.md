# Version 5 Release Notes & Update History

### 5.0.0 - September 2026
v5.0.0

---

## 🆕 New Features

**Comments**
- Comment on any public burger, with one level of threaded replies
- Like a comment, and see who liked it
- Push notifications when someone comments on your burger, replies to your
  comment, or likes your comment — each individually toggleable in Settings
- Client-side profanity filter censors flagged language before it's posted,
  with a server-side backstop that re-checks every comment regardless of
  how it was submitted

**Privacy & Safety**
- Report a comment (spam, harassment, inappropriate content, or other)
- Block a user — immediately hides their comments and cleanly ends any
  existing friendship or pending friend request between you
- Manage and undo blocks from Settings → Privacy & Safety → Blocked users
- Burger owners can now delete any comment on their own burgers, not just
  their own, for moderating reported content
- Direct "Contact support" link added to Settings

**Profile navigation**
- Tap a commenter's avatar or username to view their profile — straight to
  their full profile if you're already friends, or an add-friend prompt if not
- Tap the profile picture on an incoming friend request, or on a search /
  suggested-friend result, to preview their profile before accepting or adding

**Maps**
- Tap the location pin on a burger's map to open it directly in Apple Maps

**iPad**
- BurgerPassport is now a universal app, supporting iPhone and iPad

---

## 🎨 Redesigned Burger Detail View

- New hero layout: the group's average score now sits directly on the photo
- When more than one person has scored a burger, scores are shown as a
  compare-at-a-glance table instead of one card at a time
- Scores now animate in on open instead of appearing instantly
- Cleaner overall layout: relocated like/share/comment actions, streamlined
  meta info (location, date, price, sides), redesigned notes/location section
- Photo carousel indicator dots moved to bottom-center; the currency and
  visibility toggles are now visually distinct from the static info pills

---

## 🔧 Improvements

- Explore feed: comment and like counts relocated to a single summary row,
  matching familiar social-app conventions
- Explore feed cards are capped at a comfortable reading width and centered
  on iPad, instead of stretching full-width across a much larger screen
- Restaurant "review count" indicator restyled and reworded to "N burgers"
  with a clearer storefront icon, moved onto the photo itself
- Notification preferences: comments (and replies/likes on comments) are now
  an individually toggleable category, alongside existing notification types

---

## 🐛 Bug Fixes

- Fixed the city field showing a stale autocomplete dropdown after it had
  already been autofilled from a restaurant selection, or while editing an
  existing burger
- Fixed a duplicate-ID bug that could cause a burger to appear twice in a
  list (My Burgers, map pins, stats, passport stamps) if it was ever
  referenced in both the owned and quested entry sets
- Fixed comment counts silently drifting out of sync with the actual number
  of comments over time
- Fixed the comment box and keyboard occasionally dismissing at random while
  typing, discarding whatever had been typed
- Fixed comment like/unlike not visually updating immediately in some cases
- Fixed the currency-conversion pill's tap target
- Fixed the map screen's back button and info banner rendering with poor
  contrast against certain map colors

---

## ⚙️ Under the Hood

- `likeCount` and `commentCount` on burgers are now maintained exclusively
  by Cloud Functions (Admin SDK) instead of client-side writes, which were
  silently rejected by Firestore rules for anyone who wasn't the burger's
  owner or an existing quester on it — the root cause of the count-drift bug
  above
- Comment deletion (including cascaded reply deletion) now decrements counts
  via a Firestore transaction, avoiding a race condition possible when a
  parent comment and its reply are deleted within milliseconds of each other
- Firestore rules for comments substantially tightened: previously covered
  by the same permissive rule as quester scores and burger likes (meaning
  the app's own UI was the only thing preventing someone from editing or
  deleting another user's comment via a direct API call); now enforces
  author-only creation, field-level restrictions on edits, and
  author-or-owner-only deletion
- New `reports` collection: create-only from the client, unreadable by any
  client including the reporter, reviewed via the Firebase Console
- `firebase-functions` SDK upgraded to latest; resolved 11 of 21 flagged npm
  dependency vulnerabilities (including the one critical-severity one) via
  `npm audit fix`; two remaining moderate-severity issues require breaking
  major-version upgrades (`firebase-admin` v14, a test-only dependency) and
  are deliberately deferred to their own dedicated upgrade pass
- Fixed a guaranteed iPad crash: several share-sheet call sites presented
  `UIActivityViewController` without a popover anchor, which iPad requires
  and iPhone doesn't — this would have crashed the app immediately on iPad
  the first time anyone tapped Share
