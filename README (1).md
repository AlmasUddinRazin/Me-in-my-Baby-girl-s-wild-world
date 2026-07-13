# Me in my Baby girl's wild world

A private, sign-up-then-approval couple's space: chat, direct media uploads,
and voice/video calling with noise-cancelled audio. Static site — hosted free
on GitHub Pages, backed by your Firebase project.

## 1. Turn on the Firebase pieces you need

In the [Firebase Console](https://console.firebase.google.com) → your project
(`u-n-me-n-our-wild-world`):

1. **Authentication** → Sign-in method → enable **Email/Password**.
2. **Firestore Database** → Create database (any region close to Bangladesh,
   e.g. `asia-south1`) → start in **production mode**.
3. **Storage** → Get started → same region → production mode.

## 2. Paste in the security rules

- Firestore → Rules tab → paste the contents of `firestore.rules` from this
  folder → Publish.
- Storage → Rules tab → paste the contents of `storage.rules` from this
  folder → Publish.

These rules make sure:
- Only signed-in people can even try to sign up.
- Only people whose account is marked `approved` can read/send chat messages
  or use calling.
- Only **you** (`almas.razin.official@gmail.com`) can approve or reject
  someone.
- Each person can only upload media into their own folder.

## 3. How the approval flow works

- When someone signs up, a `users` document is created with `status: pending`
  — except for your email, which is auto-approved (you're the gatekeeper).
- You'll see a 🗝️ key icon in the top bar once you're signed in — tap it to
  see anyone waiting, and Approve or Reject them.
- Once approved, the person's pending screen automatically switches over to
  the chat — no refresh needed.
- **Practically**: sign up with your own account first (auto-approved), then
  send your girlfriend the link so she can request access, then approve her
  from the key icon.

## 4. Put it on GitHub Pages

1. Create a new **private** GitHub repo (keep it private — the Firebase
   config being public is fine, security lives in the rules, but there's no
   reason to advertise the project).
2. Upload `index.html` to the repo root.
3. Repo → Settings → Pages → Deploy from branch → `main` → `/ (root)` → Save.
4. GitHub gives you a URL like `https://yourusername.github.io/repo-name/` —
   that's your private world's address.

## 5. Notes on the calling feature

- Calls use WebRTC (peer-to-peer, so audio/video never touches a server other
  than the connection setup). Noise suppression, echo cancellation, and auto
  gain are all turned on automatically when a call starts.
- This uses only free public STUN servers (no TURN relay). On most home wifi
  and mobile data this connects fine for two people. If a call gets stuck on
  "Connecting..." on a very restrictive network (some corporate/campus wifi),
  that's the one limitation of the free version — switching one side to
  mobile data usually fixes it.
- Only one call can happen at a time (which is exactly what a two-person app
  needs).

## 6. Costs

Everything here runs on Firebase's free **Spark plan**: generous daily quotas
for Auth, Firestore reads/writes, and Storage — more than enough for two
people chatting and calling. You will not be charged unless you manually
upgrade the plan.
