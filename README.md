# Lumen for iPhone

A daily stained-glass puzzle, packaged as an iPhone app with Capacitor 8.

## What's inside

- `www/index.html`: the whole game, working offline (fonts included in `www/fonts`)
- `ios/App`: the Xcode project, already set up with:
  - app name **Lumen**, iPhone only, portrait only
  - app icon and splash screen
  - Apple's privacy manifest (`PrivacyInfo.xcprivacy`)
  - the "no encryption" flag, so you skip the export compliance question on each upload
- `store-screenshots/`: five screenshots at 1320 × 2868, the 6.9-inch size App Store Connect asks for

Native features, which only work inside the app:

- vibration feedback when panes clear, stronger for bigger groups, plus a success buzz on a full restoration
- the iPhone share sheet, sharing the result card image and text together
- an optional daily reminder notification at a time the player picks (Settings → Reminders)
- progress, streaks, hints and the gallery saved in the app's own storage, which iOS keeps safe

The same `index.html` still runs in any browser. Native features simply switch off there.

## Build it on your Mac

You need a Mac with **Xcode** (from the Mac App Store) and **Node.js** (from nodejs.org).

```bash
cd lumen-ios
npm install
npx cap sync ios
npx cap open ios
```

Then in Xcode:

1. **Add the privacy manifest to the project (one time).** Drag `ios/App/App/PrivacyInfo.xcprivacy` into the **App** folder in Xcode's left sidebar, and tick "Copy items if needed" and the **App** target.
2. **Set your bundle ID.** Click **App** (blue icon) → **App** target → **General**, and change `com.example.lumen` to your own reverse domain, for example `com.yourname.lumen`. Change `appId` in `capacitor.config.json` to match.
3. **Sign the app.** Go to **Signing & Capabilities**, tick "Automatically manage signing" and pick your team.
4. **Run it on your phone.** Plug in your iPhone, select it at the top of the window, and press ▶.

Whenever you change `www/index.html`, run `npx cap sync ios` again.

## Website and browser version

https://correll.github.io/lumen-ios/ is published from this repo by GitHub Actions ([.github/workflows/pages.yml](.github/workflows/pages.yml)) on every push to `main`:

- `/` , `/support/` and `/privacy/` come from `site/`
- `/play/` is `www/`, the same game file the iPhone app ships

## Publish to the App Store

1. Join the Apple Developer Program at developer.apple.com ($99 per year).
2. In App Store Connect, create a new app with the same bundle ID.
3. In Xcode, choose **Product → Archive**, then **Distribute App → App Store Connect**.
4. Fill in the listing:
   - Upload the images in `store-screenshots/`.
   - Support URL: https://correll.github.io/lumen-ios/support/
   - Privacy Policy URL: https://correll.github.io/lumen-ios/privacy/
   - Marketing URL (optional): https://correll.github.io/lumen-ios/
   - App Privacy: choose "Data Not Collected." Lumen keeps everything on the phone.
   - Age rating: 4+.
   - Category: Games → Puzzle.
5. Test with TestFlight first, then submit for review.

## Before you submit

- Pick a final name and make sure it's free on the App Store and not a trademark.
- Lumen is inspired by a common tile-clearing puzzle style. Keep its look, name and text clearly your own, distinct from Farbfusion on faz.net.
- Fonts: IM Fell English and Atkinson Hyperlegible are under the SIL Open Font License, and their licenses are in `www/fonts`.
