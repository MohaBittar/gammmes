# PlayZone — Browser Game Portal + Admin Panel

A site like AddictingGames: users browse and play games instantly, and a password-protected
admin can upload a game's HTML code which immediately becomes visible to everyone.

## Stack
- Plain HTML/CSS/JS (no build step)
- Firebase Auth (admin login) + Firestore (game library), loaded from the Firebase CDN

## Run it
A web server is required (browsers block JS modules on `file://`):

```bash
npx serve .        # or:  python -m http.server 8000
```

Then open http://localhost:3000 (serve) — users go to `/`, admin goes to `/admin.html`.

## Firebase setup (one time)
1. Console → **Authentication → Get started → Email/Password** → enable.
2. Add user `admin12345678@gmail.com` / `1234567890` (already done if you created it).
3. **Firestore Database → Create database** (production mode).
4. **Rules** tab → paste the contents of [`firestore.rules`](firestore.rules) → Publish.

Rules ensure: everyone can read/play, only the admin email can create/delete games.

## Admin panel
1. Open `admin.html`, sign in with the admin email + password.
2. Fill in title, category, emoji, card colors, description.
3. Paste the **complete HTML file** of a game → **👁 Preview** (optional) → **Publish game**.
4. It appears on the home page instantly (Firestore live updates). **Delete** removes it.

Tip: any single-file HTML5 game works (e.g. exported from a game engine that bundles to one HTML file).

## Files
```
index.html        user portal
admin.html        admin panel (password login)
css/style.css     shared styles
js/firebase-config.js  Firebase app/auth/db
js/app.js         browse + play + Firestore streaming
js/admin.js       login, upload, delete
js/builtin-games.js     built-in demo games list
games/*.html      4 built-in demo games
firestore.rules   security rules
```

## Deploy
Any static host works (Firebase Hosting, Netlify, GitHub Pages). With Firebase CLI:
`firebase init hosting → public dir: . → then firebase deploy`.
