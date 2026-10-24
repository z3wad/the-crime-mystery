# Firebase setup

## 1) Create the project (console)
1. https://console.firebase.google.com -> Add project
2. Build -> Realtime Database -> Create database (pick a region, start in locked mode)
3. Project settings -> Your apps -> Web (</>) -> register app
4. Copy the config values into `FIREBASE_CONFIG` in investigator_1_final.html
   (make sure `databaseURL` is included)

## 2) Apply the rules
Option A - console: Realtime Database -> Rules -> paste database.rules.json -> Publish

Option B - CLI:
    npm i -g firebase-tools
    firebase login
    firebase use --add        # choose your project
    firebase deploy --only database

## What the rules do
- Anyone can read the leaderboard.
- Only the `leaderboard` node is writable; everything else is locked.
- Each entry is validated (name <= 24 chars, correct 0-20, score 0-1000, no extra fields).
- Writes are open so the page can add entries and ZZZ admin can delete them / clear all.

## Note
ZZZ is checked only inside the page, so a determined user could delete entries
by calling Firebase directly. Fine for a club event. For real protection, add
Firebase Authentication for the admin and change `.write` accordingly.
