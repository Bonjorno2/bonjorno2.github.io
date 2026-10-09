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

## Share it (QR keys)

The admin (`awarlock2002a@gmail.com`, set in `firestore.rules` and `ADMIN_EMAIL` in `index.html`) signs in and is let in automatically. Then:

- Click **Admin** (top right of the chat) → type a label like "For Sam" → **Create**. You get a QR code plus a link.
- Share the QR (show it, or **Download QR** and send the image) or **Copy link**. Whoever scans it signs in with Google and is in — no typing.
- **Keys are single-use.** The first person to join with a key uses it up; after that it does nothing. Make one key per person.
- **Keys** lists every key: "Not used yet" (with **Revoke**) or "Used by <name>".
- **Members** lists everyone with their email. **Remove** takes away access right away; they can only come back with a new key.
- Names are locked to each person's Google account name when they join, and every message must carry that name, so members can't post as someone else.
- On a phone: open the link in Safari or Chrome → **Share → Add to Home Screen**, and it works like an app.
- Typed codes still work: the "Almost there" screen accepts a key typed by hand.

## Emojis, photos & GIFs

- 😊 opens an emoji picker (your recent ones are at the top). Messages that are only 1–3 emoji show big.
- 📷 sends a photo. It's shrunk on your device to about 1600px so it fits in the free database — sharp on a phone, but not the full-resolution original. On a computer you can also paste a screenshot straight into the message box. Tap a photo to view it full screen.
- **GIF** opens GIF search (GIPHY) and an **Upload GIF** button for GIF files up to ~700 KB.
- **GIF search needs a GIPHY key:** sign up at developers.giphy.com → Create an API key (choose "API", not SDK) → paste it into `GIPHY_API_KEY` in `index.html` and upload the file again.
- Photos are saved on each device after the first view, so scrolling back doesn't re-download them. The free plan holds roughly 3,000–5,000 photos in total.

## Good to know

- The Firebase config being visible in a public repo is normal. The **rules** are what protect the messages; only members can read or post.
- Keys are never in the page itself, so they can't be found by viewing the source. The key in a QR link sits after `#`, which browsers don't send to GitHub. Anyone who signs in without a key just sees the "enter invite code" screen.
- Treat an unused QR like a house key: whoever uses it first gets in. If one goes astray before its person uses it, **Revoke** it and make a new one. If someone you don't know shows up in **Members**, remove them.
- The free Firebase plan covers tens of thousands of messages a day, far more than a group chat needs.
- The 🔔 button gives notifications only while the page is open (e.g. in a background tab). It can't notify when the page is closed.
