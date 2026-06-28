# Version 2 Release Notes & Update History
### 2.3.0 - June 2026
BurgerPassport 2.3 🍔
─────────────────────

The passport update. A completely redesigned Passport view that looks
and feels like a real travel document, 10 new badges, and several
bug fixes.

─────────────────────
PASSPORT — REDESIGNED
─────────────────────

• New passport data page — deep navy background with gold typography,
  your profile photo in a passport-photo box, and official data fields
  (Holder, Rank, Member Since, Currency, Passport No.)
• Passport number is unique and permanent per account, derived from
  your user ID
• Holographic stamp on the right side of the data page — animated
  iridescent rings rotating in opposite directions with a 🍔 centre
  and circular "BGRPPT • BURGER PASSPORT •" text
• Stats row (Burgers / Countries / Avg Score) and gold progress bar
  embedded in the navy data page
• Machine-readable zone (MRZ) below the stats — decorative <<< lines
  matching real passport styling
• Stamps and Rewards are now separate tabs within the passport, accessed
  via a gold underline tab bar at the bottom of the navy section
• Country stamps now grouped by continent — Europe, North America,
  South America, Asia, Africa, Oceania, Antarctica — each rendered as
  a passport page with a navy spine/binding stripe, cream background,
  ruled horizontal lines, continent header in tracked uppercase, and
  page number in the corner
• Rewards tab matches the stamp page aesthetic — same cream background,
  ruled lines, navy spine, and ink-brown typography — consistent in both
  light and dark mode (all colours are hardcoded, not system adaptive)
• Profile photo in the passport data page is tappable to enlarge, with
  pinch-to-zoom and swipe-down to dismiss

─────────────────────
BADGES — 10 NEW ADDITIONS
─────────────────────

• Explorer: Home Turf 🏠 (5 burgers in most-visited country), Border
  Hopper 🛂 (2 countries in one weekend), Return Visit 🔁 (same
  restaurant twice)
• Critic: Consistent 📐 (10 burgers within 1 point of each other),
  Harsh Judge ⚖️ (never above 6.0 across 10+ burgers), Easy Pleased
  😊 (never below 7.0 across 10+ burgers)
• Social: Popular ❤️ (a burger liked by 5+ people), Influencer ⭐
  (3+ friends quest the same burger)
• Quirky: Double Decker 2️⃣ (2 burgers in one day), On a Roll 🎳
  (burgers in 3 consecutive weeks)
• Story Mode renamed from Volume; Plant Based renamed from Diet
• Casual tier icon updated from 🍔🍔 to 🔥; Getting Hungry badge
  updated to match

─────────────────────
OTHER IMPROVEMENTS
─────────────────────

• Tapping a profile photo (your own or a friend's) now opens it
  fullscreen with pinch-to-zoom and swipe-down to dismiss
• Continent grouping correctly places Lanzarote in Europe and gives
  Antarctica its own section (🧊)
• Tier icon next to usernames now correctly includes quested burgers
  in the count — fixes incorrect tier display for heavy questers
• Passport average score now uses each user's own quested score rather
  than the burger owner's score

─────────────────────
BUG FIXES
─────────────────────

• Fixed: passport average score used owner's score for quested burgers
  instead of the viewer's own score
• Fixed: tier icon on own profile excluded quested burgers from the
  count, showing a lower tier than earned
• Fixed: Stamps/Rewards tab bar only registered taps on the text label,
  not the surrounding area

### 2.2.0 - June 2026
BurgerPassport 2.2 🍔
─────────────────────

The rewards update. A completely new badges system, an overhauled
Passport tier ladder, and a handful of bug fixes.

─────────────────────
REWARDS & BADGES
─────────────────────

• 22 badges across 6 categories — Volume, Explorer, Critic, Diet,
  Social, and Quirky
• Volume badges: First Bite, Getting Hungry, Bronze Palate, Silver
  Tongue, Gold Standard, Diamond Jaw, Legend (1, 5, 10, 25, 50, 100,
  250 burgers)
• Explorer badges: Passport Starter, World Traveller, Globetrotter,
  Around the World (3, 5, 10, 20 countries), Continental (3 continents),
  Local Legend (10+ burgers in one city)
• Critic badges (hidden until unlocked): Tough Crowd (5 burgers under
  5.0), Connoisseur (10 burgers at 9.0+), Perfectionist (a perfect 10)
• Diet badges: Going Green (first vegan burger), Plant Pioneer (10 vegan
  burgers)
• Social badges (hidden): Squad Goals (quested 5 friends' burgers)
• Quirky badges (hidden): Night Owl (burger logged after midnight),
  Whirlwind (3 countries in one calendar month)
• Hidden badges show as ??? in the grid until unlocked — tap any badge
  to see its name, description, and locked/unlocked status
• Animated toast notification springs in from the top whenever a badge
  is unlocked — shown after every burger save or edit
• Badges stored in Firestore so they persist across devices and app
  reinstalls
• Existing users receive all earned badges automatically on first launch
  after updating — with toasts for each one

─────────────────────
PASSPORT — TIER OVERHAUL
─────────────────────

• 7-tier ladder replaces the previous 4-tier system:
  🍔 Beginner (1–4) → 🍔🍔 Casual (5–9) → 🥉 Bronze (10–24) →
  🥈 Silver (25–49) → 🥇 Gold (50–99) → 💎 Diamond (100–249) →
  👑 Legend (250+)
• Passport view now has two tabs — Stamps and Rewards — keeping the tier
  banner, progress bar, and stats always visible at the top
• New country stamps also trigger a toast notification on first visit

─────────────────────
BUG FIXES
─────────────────────

• Fixed: friends count on a friend's profile showed too high — was
  counting stale/pending documents in the friends subcollection instead
  of using the accurate stored friendCount field

### 2.1.0 - June 2026
BurgerPassport 2.1 🍔
─────────────────────

A polish-focused release: smoother loading, a more characterful Passport,
a cleaner map, deeper Countries exploration, and a completely refreshed
Stats screen.

─────────────────────
LOADING & VISUAL POLISH
─────────────────────

• Shimmer loading animation replaces flat grey placeholders while images
  load — used across Explore hero images, the map detail card, the Visits
  sheet, profile galleries, friend burger lists, and burger detail views
• Fixed: burgers with photos that hadn't finished loading yet briefly
  showed a "No photo" empty state instead of a loading indicator
• Explore score badges are now colour-filled pills (matching the score
  colour) instead of plain text, for more visual weight at a glance

─────────────────────
PASSPORT
─────────────────────

• Country stamps redesigned with a hand-stamped, ink-bleed look — dashed
  distressed rings, a soft ink-bleed texture, and per-country ink colours
  (red, blue, green, sepia) instead of plain grey circles

─────────────────────
COUNTRIES — OVERHAULED
─────────────────────

• Fixed: viewing a friend's profile could undercount their countries
  visited if they had private burgers — totals now correctly include
  every country, public or private
• Friends' Countries list now shows an "Also visited (private) 🔒" section
  for countries only represented by private burgers
• Countries are now tappable — both on your own profile and a friend's —
  showing a list of every burger logged in that country, sorted by score
• Tap any burger in that list to open its full detail view

─────────────────────
STATS — REDESIGNED
─────────────────────

• New hero header showing your animated overall average score with a
  colour-matched gradient and a tagline based on your average
  ("Burger connoisseur 👑", "Tough crowd! 😅", etc.)
• Overview stat cards (Avg score, Burgers, Countries, Total spent) now
  animate in with a count-up effect and subtle colour-tinted backgrounds
• All sections now animate into place with a staggered fade/slide on open
• Score distribution chart bars now grow in with a springy animation
• Score over time chart line and fill now draw in left-to-right
• Fixed: questers' Avg score, Top burgers podium, score distribution, and
  score-over-time chart all used the burger owner's score instead of the
  quester's own score — now corrected throughout

─────────────────────
BUG FIXES
─────────────────────

• Fixed: liking a burger or its data finishing loading could cause the
  burger detail view to instantly close when opened from a friend's
  profile, countries list, or other nested screens
• Fixed: friend's burger detail view was missing the Like/Share row and
  the "who liked this" list present on your own burgers
• Fixed: Explore's "Reviews" button always showed a count even for a
  single visit, and has been renamed to "Visits" for clarity

### 2.0.0 - June 2026
BurgerPassport 2.0 🍔
─────────────────────

This is the biggest update to BurgerPassport yet. The Explore feed has been completely redesigned, the like system has been rebuilt from the ground up, and profiles are now far more connected and interactive.

─────────────────────
EXPLORE FEED — REDESIGNED
─────────────────────

• Completely new card layout inspired by social media feeds — profile picture and username at the top, notes, then the hero image, then engagement
• Cards are now visually separated with rounded corners, a subtle border, and shadow so each entry feels like its own post
• Passport tier badge (🥉🥈🥇💎) shown next to every username so you can see how experienced each reviewer is at a glance
• Quester badge shown when a burger was scored by a group
• Restaurant and city shown in the header alongside the flag
• Notes are shown above the image and truncate to 3 lines — tap "...more" to expand in place
• Profile picture and username are now tappable — tap to view that user's profile, send a friend request, or view your own profile
• You can now like your own burgers

─────────────────────
LIKES — REBUILT
─────────────────────

• Like counts are now always accurate — pulled directly from the likes subcollection rather than a stored field, which could get out of sync
• Existing corrupted like counts heal automatically the first time a burger is viewed
• New social-media style layout: a ❤️ count row above the action buttons — tap it to see who liked
• Like, Share, and Reviews buttons now have a full-width tap area so they're much easier to hit
• You can like your own burgers from both Explore and the burger detail view
• Likers sheet now shows profile pictures, with your friends listed first
• Tap any friend in the likers list to view their profile
• Tap a non-friend in the likers list to send them a friend request

─────────────────────
SHARE
─────────────────────

• Share button added to every card in Explore and to every burger detail view
• Shares the burger name, restaurant, location, score, and notes via the iOS share sheet
• Includes the hero photo where available
• Works correctly from all screens including when a burger is open as a full-screen sheet

─────────────────────
RESTAURANT REVIEWS
─────────────────────

• When multiple entries exist for the same restaurant in the current feed, a Reviews button appears in the action bar with a count badge
• Tap Reviews to see all entries for that restaurant sorted by score — each row shows the burger name, reviewer, date, and score
• Tap any entry in the list to open the full burger detail

─────────────────────
PROFILES
─────────────────────

• Viewing your own profile from Explore now shows accurate burger, country, and friend counts — including private burgers in your totals
• Countries stat is now tappable — see a full list of every country with a burger count and the country name in its own language
• Friends stat is now tappable — see who that user is friends with, add anyone you don't already know
• Burger count, country count, and friend count all update instantly without needing to refresh

─────────────────────
FLAGS & COUNTRY NAMES
─────────────────────

• Flag emoji now works for every country in the world — previously only ~40 countries were supported and others showed a white flag
• Country names now shown in their own language in the Countries list (Deutschland, Česko, 日本, Ελλάδα, etc.) with the English name as a subtitle

─────────────────────
PERFORMANCE
─────────────────────

• Two-level image cache (memory + disk) introduced — images load instantly on repeat visits and survive app restarts
• Disk cache prunes entries older than 7 days automatically to keep storage usage low
• Explore now pre-warms images for the first visible cards before the feed appears, so profile pictures and hero images load without a blank flash on first open

─────────────────────
BUG FIXES
─────────────────────

• Fixed: tapping Like, Share, or Reviews in Explore sometimes opened the burger instead of performing the action
• Fixed: tapping "...more" on notes opened the burger instead of expanding the text
• Fixed: blank space above the hero image was tappable and opened the burger
• Fixed: likers sheet could dismiss itself unexpectedly when tapping a non-friend
• Fixed: profile picture avatars in the likers sheet could expand to full size when no image was available
• Fixed: like counts showing higher than the actual number of likers (data healed on view)
• Fixed: share button did nothing when tapped from the burger detail view
• Fixed: Czechia and many other countries showed a white flag instead of the correct emoji
• Fixed: app crash caused by a duplicate dictionary key in the country names list

