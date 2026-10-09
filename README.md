# Group Chat — setup (about 15 minutes)

Two free accounts: **Firebase** (stores messages and handles Google sign-in) and **GitHub** (hosts the page).

## Part 1 — Firebase

1. Go to **console.firebase.google.com** → **Create a project**. Any name. You can turn Google Analytics off.
2. Left menu → **Build → Authentication** → **Get started** → **Sign-in method** → **Google** → turn on **Enable** → pick your support email → **Save**.
3. Left menu → **Build → Firestore Database** → **Create database** → pick a US location → **Start in production mode** → **Create**.
4. In Firestore, open the **Rules** tab. Delete what's there, paste in everything from `firestore.rules`, then click **Publish**.
5. Create the invite code: in Firestore's **Data** tab, click **+ Start collection** → Collection ID **`invites`** → **Next**. For **Document ID**, type your invite code in **lowercase** (e.g. `sunny-pickle-4821`; longer is safer). Add one field (anything works, e.g. `active` = `yes`). Click **Save**.
6. Click the **gear icon → Project settings**. Under **Your apps**, click the web icon **`</>`**, give it any nickname, and click **Register app** (skip Hosting). Copy the `firebaseConfig = { ... }` values into `index.html` where it says **PASTE YOUR FIREBASE CONFIG HERE**.

## Part 2 — GitHub Pages

7. On **github.com**, create a new **public** repository named exactly **`bonjorno2.github.io`**.
8. In the repo, click **Add file → Upload files**, upload `index.html`, and click **Commit changes**.
9. Go to the repo's **Settings → Pages**. Under "Build and deployment", set Source to **Deploy from a branch**, Branch to **main**, folder **/ (root)**, and click **Save**. Wait 1–2 minutes.

## Part 3 — Connect them

10. Back in Firebase: **Authentication → Settings → Authorized domains → Add domain** → enter `bonjorno2.github.io`.
11. Open **https://bonjorno2.github.io**, sign in with Google, and send a test message.

## Share it

- Send everyone the link **and the invite code**. They sign in with any Google account and enter the code once.
- On a phone, open the link in Safari or Chrome → **Share → Add to Home Screen**, and it works like an app.
- **Change the code:** Firestore → Data → `invites` → delete the old code's document and add a new one. Existing members stay in.
- **Remove someone:** Firestore → Data → `members` → find their document (it shows their name and email) → delete it.

## Good to know

- The Firebase config being visible in a public repo is normal. The **rules** are what protect the messages; only members can read or post.
- The invite code is never in the page itself, so it can't be found by viewing the source. Anyone who signs in without it just sees the "enter invite code" screen.
- The free Firebase plan covers tens of thousands of messages a day, far more than a group chat needs.
- The 🔔 button gives notifications only while the page is open (e.g. in a background tab). It can't notify when the page is closed.
