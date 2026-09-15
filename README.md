# Sweet & Sassy of Cumming — "This Week's Trends" page

A calm, self-contained weekly page: what's **gaining traction** in short-form video right now, and a
few ways to use it with whatever's happening in the shop that day. Not scripts — prompts. One file,
no build step.

## Open it
Double-click `index.html` — it runs in any browser.

## It refreshes itself
A scheduled task runs **every Monday morning**: it looks up what's gaining traction that week, picks
the 4–5 trends that actually work with kids'-salon/spa/party footage, and pushes the updated page
here. Render redeploys it. You just open it and film. Nothing to maintain.

## Host it free on Render (one-time, ~2 minutes)
1. Put this folder in a GitHub repo.
2. In Render: **New → Static Site** → connect the repo.
3. **Build Command:** leave blank · **Publish Directory:** `.` (a dot)
4. Deploy → you get a public link.

`render.yaml` is included so Render auto-configures it. Point the Render service at this repo's
**`main`** branch with auto-deploy on — that's what makes the weekly refresh reach the live link.

## How the team uses it
- **4–5 trend cards** — what's working right now and *why*, in plain language.
- **"A few ways to try it"** — concrete ideas that work with a mani, a braid, a party setup, a restock.
- **Caption starter + hashtags** — one tap to copy, then make it yours.
- **Mark filmed** — so the team can see what's been used this week.

## Weekly refresh
`SASS_WEEKLY_RUNBOOK.md` is the procedure. A Monday routine runs it, commits, and pushes to `main` —
Render redeploys automatically. **The commit is the deploy**; if a run can't push, the live page
silently goes stale, so a failed push is a failed run.
