# Version 3 Release Notes & Update History

### 3.3.0 - June 2026
v3.2.0

Launch experience
- New LaunchScreenView gates the main UI behind a readiness check: auth state, profile, and friends list must all resolve (or hit a timeout) before the app appears
- Fixes friend count flashing 0 before populating with the real value
- 4-second hard timeout ensures the app never hangs indefinitely on poor connectivity
- Removed unnecessary Messaging.deleteToken() call on every foreground — was forcing an unneeded FCM token refresh on each app resume

Misc
- App Privacy updated to declare Coarse Location collection

### 3.2.0 - June 2026
Explore tab
- New two-row filter bar: search + list/map toggle on row 1, Friends / Vegan / Near me / Sort pills on row 2
- Near me filter — uses device location to show burgers in the user's city
- Friends filter now fetches all friend burgers directly from Firestore rather than filtering the paginated page, so all friends show correctly
- Skeleton loading cards while the feed is fetching
- Haptic feedback on like
- Location permission alert with deep link to Settings if denied

Bug fixes
- Friends filter was missing burgers from friends whose entries weren't in the first page of results
- le_chonkre (formerly rtsmre) username corrected in Firestore usernames collection

### 3.1.0 - June 2026
New
- Perfect 10 celebration: full-screen gold confetti animation with triple haptic when any burger scores 9.99+, fires on new entry, edit, and quester submit flows
- Perfectionist badge visibility changed from hidden to visible — users can now see and chase it in the Rewards grid
- Longest Streak sheet: tapping the streak card in Advanced Stats opens a full burger list for that streak period, with flag, restaurant, burger name, city, date and score
- Streak card now shows the date range of the longest streak inline

Fixed
- Passport stamp toasts firing on every burger edit — root cause was checkAndAwardBadges being called with an empty previousCountries set on edit dismiss, making every existing country appear new
- Longest streak week count was inflated due to weekOfYear calculation losing year context — weeks from different years (e.g. week 36 of 2022 and 2023) were collapsing into the same bucket
- Streak burger list and week count are now computed in a single unified pass, eliminating the mismatch between the displayed count and the listed burgers

### 3.0.0 - June 2026
What's new in v3.0.0
This is the biggest update to BurgerPassport yet.
BurgerPassport Pro

Unlock the full experience with a one-time purchase — no subscription, no hidden fees.
Custom Scoring

Rename any scoring category, add up to 4 of your own, and set custom weights so what matters most to you counts more.
Advanced Stats

A brand new Advanced tab with monthly score trends, restaurant leaderboard, category radar chart, score velocity, biggest score swing, spending insights, streak tracker and more.
Improved Scoring Step

Score, Weights and Categories are now separate tabs — much cleaner to use.
People You May Know

The Add Friend screen now suggests people based on your friends network, with mutual friend counts shown.
Export Your Data

Export all your burger entries as a CSV — open in Numbers, Excel or any spreadsheet app. Free for everyone.
Better Notifications

The notifications screen now shows your weekly activity and friend count when there's nothing new.
First-Time Experience

New empty states on Home and My Burgers guide new users through logging their first burger.
Bug fixes and performance improvements
