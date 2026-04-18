# Habit Performance Tracker

This package contains a mobile-friendly single-page app with:
- Daily logging for diet, exercise, prayer, study, and sleep
- Editable targets in-app
- Weekly and monthly review
- Optional Firebase Authentication + Firestore sync for cross-device access
- Offline support via service worker when hosted over HTTPS

## Files
- `index.html` — main app
- `manifest.json` — PWA manifest
- `service-worker.js` — offline cache

## Fastest way to run locally
Open `index.html` in a browser.

## Best way to use across devices
Host the files online, then open the same URL on each device.

### Recommended: Firebase Hosting + Firestore + Authentication
1. Create a Firebase project and register a Web app to get your Firebase config object. The official setup docs explain how to create a project, register a web app, and initialize the SDK. citeturn848435search0turn848435search3
2. Enable **Authentication** with Email/Password in the Firebase console. Firebase’s web auth guide covers email/password sign-in for websites. citeturn848435search5
3. Create a **Cloud Firestore** database for sync storage. Firebase’s Firestore quickstart covers creating the database and connecting a web app. citeturn848435search2
4. Deploy the app files to **Firebase Hosting**, which is designed for static and single-page web apps. citeturn848435search1turn848435search3
5. In the app’s **Sync** tab, paste the Firebase web config JSON, then sign up or sign in with the same email/password on each device.
6. Use **Push local data to cloud** on the device with your current data, then **Pull cloud data to this device** on the other device.

### Firestore security rules
Use authenticated, user-owned access. Example rules:

```text
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/app/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

## Notes
- If you use the app only as a local file, sync and installability will be limited.
- For Android home-screen install and service worker offline behavior, host the app over HTTPS.
- The app also supports JSON export/import as a backup path.
