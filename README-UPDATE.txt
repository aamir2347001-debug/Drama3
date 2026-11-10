Hm Book - Updated Build v19

Files included:
- index.html
- manifest.webmanifest
- sw.js
- icon-192.png
- icon-512.png
- icon-maskable-512.png

Deployment:
1. Take a Full Backup from Hm Book Settings before updating.
2. Extract this ZIP.
3. Replace the existing GitHub Pages app files with these files in the same folder.
4. Commit/push the update.
5. Open the installed Hm Book app online once so the v19 service worker can install.
6. If the old screen remains, close the app completely and reopen it.

Existing customer data uses the same local storage key and is not intentionally reset by this update.

Changes in v19:
- PIN can be removed from Settings; removing it also disables PIN unlock.
- Fingerprint/device biometric login can be removed from Hm Book Settings. This removes the app's saved credential reference; Android/browser-managed authenticator entries are managed by the device.
- Switching to another app no longer triggers the lock. A new app launch/session asks for PIN/biometric when security is enabled. Refreshing the current app session does not trigger the lock.
- Pull-to-refresh overscroll is disabled, and the service worker serves the app shell from cache first.
- The web app manifest keeps standalone display mode. For an app-like full-screen experience, launch Hm Book from its installed home-screen icon, not from a normal browser tab.

Limitations:
- A website/PWA cannot reliably receive a guaranteed "Quit app" event on every Android device. This build uses a fresh app-session marker: it avoids locking on app switching and page refresh, and locks on a fresh standalone launch. Android may preserve a prior app session on some device/browser versions, so verify the quit/reopen behaviour on the target phone.
- The browser's own refresh command still reloads the document by design; this update prevents accidental pull-to-refresh and avoids treating a reload as a new security session.
- Biometric setup requires HTTPS and a compatible device authenticator. Depending on device support, Android may request fingerprint, face, or screen-lock PIN.
- Business records remain in local browser storage. The optional lock is an access barrier, not encryption of stored records.
