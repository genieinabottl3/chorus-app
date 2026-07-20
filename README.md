# Chorus 🏡
### Your chores, on us

Chorus is a lightweight task manager for the stuff that doesn't fit neatly into a normal to-do list: recurring chores that need to just *show up* without being re-typed every day, and longer one-off tasks that move through stages over several days.

**Live app:** https://genieinabottl3.github.io/chorus-app/

## Features

- **Today** — a checklist of recurring chores (daily, weekly, monthly, or yearly) that appears automatically based on the schedule you set. Nothing to re-enter each day.
- **Board** — a Kanban board (To do / In progress / Done) for one-off or multi-day tasks, with drag-and-drop between columns.
- **Calendar** — a month view showing everything due on a given day, recurring occurrences and one-off due dates alike, with a day panel to check things off inline.
- **Tags** — filter any view by tag (e.g. `chores`, `office`, `baby`). New tags are created just by typing them on a task.
- **Subtasks** — up to two levels deep (a task can have subtasks, and each subtask can have one level of its own dependency), with an inline checklist and progress badge.
- **Timestamps** — every task tracks when it was created, last updated, and (for one-off tasks) completed, so you can see how long things actually take.
- **Descriptions** — optional free-text notes on any task.

## How it works

Chorus is a single static HTML file — no server, no build step, no backend. It's designed to be hosted on GitHub Pages (or similar) and opened from any browser, desktop or mobile.

Data is **not stored on any server Claude or Anthropic controls**. On first use, you sign in with your own Google account, and Chorus creates a Google Sheet called `Chores App Data` in *your own* Google Drive. All your tasks live in that one sheet as a single data blob. Every change is written straight to that sheet from your browser using your own Google sign-in — nothing passes through a third party.

Because each person signs in with their own Google account, **each user gets their own independent sheet** — this is a single-player app per login, not a shared/team task list (that's a possible future addition, not what's built today).

## Using it on a new device

Just open the URL and sign in with Google. That's it — no install, no account to create beyond your existing Google account. You'll need to click "Continue with Google" once per browser/device; there's no persistent login across devices beyond your data itself, which lives in your Drive.

## Letting someone else try it

Because this app isn't published/verified with Google, only email addresses added as **Test users** on the OAuth consent screen can sign in. To let someone else use it:

1. Go to the [Google Cloud Console](https://console.cloud.google.com/) → your project → **APIs & Services → OAuth consent screen**.
2. Under **Test users**, click **Add users** and enter their Google account email.
3. They can now open the app URL and sign in — they'll see a one-time "Google hasn't verified this app" warning (expected for a personal project; click **Advanced → Go to Chorus (unsafe)** to continue).

Each tester gets their own private sheet and task list — nothing is shared between accounts.

## Setting this up yourself (for forks/redeploys)

If you fork this repo or move it to a new URL, the embedded Google OAuth Client ID needs to match the new address:

1. **Google Cloud Console** → create/open a project → enable the **Google Sheets API** and **Google Drive API**.
2. **APIs & Services → OAuth consent screen** → User type *External* → fill in the basics → add your own email (and any testers) under **Test users**.
3. **APIs & Services → Credentials → Create Credentials → OAuth client ID** → type *Web application* → under **Authorized JavaScript origins**, add your site's origin exactly (scheme + host only, e.g. `https://yourname.github.io` — no path, no trailing slash).
4. Copy the generated Client ID and paste it into `index.html`, replacing the `CLIENT_ID` constant near the top of the `<script>` block.
5. Push to GitHub, enable **Pages** in the repo settings (deploy from branch, root folder), and open the resulting URL.

## Privacy

Your task data lives only in a Google Sheet in your own Drive, created and accessed with your own Google sign-in. No task data is sent to or stored by this repo, GitHub, or any third-party server.
