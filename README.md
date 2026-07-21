# Chorus 🏡
### Your chores, on us

Chorus is a lightweight task manager for the things that don't fit a normal to-do list: recurring chores that should just *appear* without being re-typed every day, and longer one-off tasks that move through stages over several days. It's built for phone and desktop, syncs through your own Google account, and keeps work and personal life cleanly separated.

**Live app:** https://genieinabottl3.github.io/chorus-app/

---

## For testers — start here

You don't need a Google Cloud project, a GitHub account, or any setup. You just need a Google account (the one you already use).

1. **Ask to be added.** Chorus isn't publicly published with Google yet, so only approved emails can sign in. Send the owner the Google email address you'll sign in with, and they'll add you to the access list.
2. **Open the app:** https://genieinabottl3.github.io/chorus-app/
3. **Click "Continue with Google"** and sign in.
4. You'll see a one-time **"Google hasn't verified this app"** warning — this is expected for a personal project, not a security problem. Click **Advanced → Go to Chorus (unsafe)** to continue.
5. That's it. You'll do the sign-in once per device/browser.

**Your data is your own.** When you sign in, Chorus creates a Google Sheet called *Chores App Data* in *your* Google Drive and stores everything there. Each tester has a completely separate task list — nothing is shared between accounts, and the owner cannot see your tasks. It's single-player per login (shared/team lists aren't built yet).

To add tasks from your phone, just open the same link in your phone browser and sign in.

---

## What's in the app

**Views (tabs):**

- **Today** — recurring chores due today, auto-generated from each chore's schedule. Tick them off; they reset on their next due day. Keeps a small streak counter for chores you keep going.
- **Upcoming** — everything due in the next 7 days, grouped by day.
- **Board** — a kanban board (To do / In progress / Done) for one-off or multi-day tasks, with drag-and-drop between columns.
- **Calendar** — a month view with a dot per task each day; click a day to see and tick off what's due.
- **Archive** — completed one-off tasks with their full history: created, started, time in progress, and completion date.

**Global search** — a search bar across the top finds any task by name, description, or tag, across *every* profile at once. Recurring chores show when they were last done; one-off tasks show status and dates. Handy when you can't remember when something was last done.

**Profiles** — switch between *Personal* and *Work* (add your own with the **+**). Today, Upcoming, Board, and Calendar scope to the active profile; the **All** chip gives a combined view across profiles. Search always spans everything.

**Tags** — label tasks (e.g. `chores`, `office`, `baby`) and filter any view by tag. New tags are created just by typing them on a task.

**Task detail** — every task supports an optional description, up to two levels of subtasks/dependencies (with an inline checklist and progress badge), and tracks created / last-updated / completed timestamps.

**Recurrence** — daily, weekly (pick days), monthly (pick date), or yearly (pick a date, repeats annually).

---

## How it works (the short technical version)

Chorus is a single static HTML file — no server, no backend, no database of its own. It's hosted on GitHub Pages and runs entirely in your browser.

On first sign-in it uses Google Sign-In and reads/writes a single Google Sheet in your own Drive using your own access token. No task data ever passes through the repo, GitHub, or any third-party server. Because each person signs in with their own Google account and gets their own sheet, everyone's data stays private and independent.

---

## Setting this up yourself (for forks / redeploys)

If you fork this repo or move it to a new URL, the embedded Google OAuth Client ID must match the new address:

1. **Google Cloud Console** → create/open a project → enable the **Google Sheets API** and **Google Drive API**.
2. **APIs & Services → OAuth consent screen** → User type *External* → fill in the basics → add tester emails under **Test users**.
3. **APIs & Services → Credentials → Create Credentials → OAuth client ID** → *Web application* → under **Authorized JavaScript origins** add your site's origin exactly (scheme + host only, e.g. `https://yourname.github.io` — no path, no trailing slash).
4. Copy the Client ID into `index.html`, replacing the `CLIENT_ID` constant near the top of the `<script>` block.
5. Push to GitHub, enable **Pages** in repo settings (deploy from branch, root folder), and open the resulting URL.

**Adding a tester later:** Google Cloud Console → your project → APIs & Services → OAuth consent screen → Test users → Add users → enter their Google email. No other setup needed on their end.

---

## Privacy

Your task data lives only in a Google Sheet in your own Drive, created and accessed with your own Google sign-in. Nothing is sent to or stored by this repo, GitHub, or any third-party server, and no other user (including the owner) can see your data.
