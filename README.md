# Lekka App — voice-entry test build

## Included
- Responsive, installable web app (PWA) layout.
- Borrowers, loans, loan repayments, separate daily depositor accounts, reports and local backup/export.
- Brand profile with each business's own name, tagline and logo.
- Floating Lekka Assistant (bottom-right on every screen), with a chat-style interface, Kannada microphone input (`kn-IN`), typed fallback, simple local command parsing, spoken confirmation where a Kannada system voice is available, and explicit confirmation before saving a loan repayment.
- Account numbers assigned to borrowers; existing borrowers receive a sequential account number when loaded.
- Neutral Lekka logo, Firebase Hosting config, starter Firestore rules, and a Firebase config template.

## Try the Kannada voice feature
1. Unzip this folder on your computer.
2. Open `index.html` in a browser to try the text-command path. Microphone recognition usually needs HTTPS or localhost and a supported browser.
3. For phone testing, deploy to Firebase Hosting or another HTTPS static host, then open it in Chrome on Android.
4. Tap the floating **✦** button in the bottom-right corner, tap the microphone, and say something like:
   - `ಅಕೌಂಟ್ ನಂಬರ್ ಎರಡು, ಕಲೆಕ್ಷನ್ ಒಂದು ಸಾವಿರ`
   - `Account number 2, collection 1000`
5. Check the borrower name and amount shown in the preview. Tap **Confirm and record payment** only if correct.
6. If microphone recognition is unavailable, type the same command into the assistant message box and press send.

## Important prototype limits
- **Not connected to Firebase yet.** Records remain in browser localStorage on the current device. They do not sync between devices. Export backups frequently and do not use this as the sole record for real financial transactions.
- Voice recognition is browser/device dependent. The Web Speech API is not supported everywhere, and some browsers send audio to an online recognition service. Kannada recognition accuracy must be tested on your actual Android phone.
- The current voice assistant supports loan repayment commands and a simple today-collection query. It currently expects clear account and amount phrases such as `1000` or `ಒಂದು ಸಾವಿರ`. It refuses ambiguous cases, missing accounts, accounts with multiple active loans, and amounts above the pending balance.
- The speech parser is a small rule-based prototype, not a full AI model. No AI API key or paid AI service is used.
- Kannada text-to-speech depends on a Kannada voice installed/provided by the device. If unavailable, the app may not speak Kannada aloud.
- `firestore.rules` is a starter rule template for a future per-user data layout. Since this build does not use Firebase Auth or Firestore yet, these rules do not currently protect localStorage. Do not deploy an app containing real customer data until authentication, tenant separation, cloud sync, backups, and security rules are fully implemented and tested.
- The example 365-day depositor maturity bonus is a user-specified business rule, not legal advice. Confirm applicable Indian lending/deposit rules before accepting real deposits or lending.

## Firebase Hosting deployment (static frontend only)
1. Create a Firebase project at https://console.firebase.google.com/.
2. Install Node.js and Firebase CLI on your computer.
3. In this folder, run `firebase login`.
4. Run `firebase init hosting`, select your project, choose the current folder as the public directory, and do not overwrite the existing `index.html` or `firebase.json`.
5. Run `firebase deploy --only hosting`.

This publishes the current frontend only. It does **not** activate cloud storage or multi-user accounts. Firebase configuration template is provided as `firebase-config.example.js`; never place service-account keys in the frontend.

## File list
- `index.html` — app UI and local business logic
- `logo.svg` — neutral Lekka app mark
- `manifest.json` — installable PWA metadata
- `sw.js` — basic service-worker cache
- `firebase.json` — Firebase Hosting/Firestore rules config
- `firestore.rules` — locked-down starter rules for future user-scoped data
- `firebase-config.example.js` — configuration template only
- `firebase-config.js` — blank placeholder; no project is connected
- `README.md` — setup and limitations
- `check.js` — existing app helper/check script


## Clean zero-value prototype (refined)
This version starts with zero balances and no sample customers, loans, repayments, or deposits. It uses a new local-storage namespace (`lekka_local_v2_clean`) so old prototype data does not appear in this version. It is still a local prototype; Supabase is not connected.
