# Sweet & Sassy of Cumming — Weekly "This Week to Film" Runbook (Claude Code)

**Purpose:** Every Monday, regenerate the store's one-week content page with fresh, trend-driven
ideas and **push it live through git so Render auto-deploys it.** The live page the team opens is
served by Render (e.g. `sass-zwml.onrender.com`) and deploys automatically when this repo receives
a new commit on the branch Render watches.

> This runbook replaces the old Cowork routine, which was publishing to a claude.ai artifact that
> the team's page was **not** connected to. The fix: update the page **in this repo** and push.

---

## THE PIPELINE (why this repo is the source of truth)

```
You edit the page file  →  git commit  →  git push  →  Render detects the commit  →  live site updates
```

If you skip the commit/push, nothing changes on the live site. The commit **is** the deploy.

---

## STEP 0 — ORIENT (first run only, or if the layout changed)

1. Confirm the git remote and branch Render watches:
   `git remote -v` and `git branch --show-current`.
2. Find the page file. It's the HTML the site serves — likely `index.html` (or `public/index.html`,
   `src/index.html`, `dist/index.html`). Open it and locate **where the weekly content lives.**
   - The current Render page (`index.html`) is **"This Week's Video Ideas"** — a day-by-day layout
     with three tabs: **This Week**, **Idea Bank**, and **How it works**. A sticky header shows the
     week label, the "Refreshed ..." line, and a filmed-progress bar.
   - All weekly content lives in **one JavaScript object, `const WEEK`**, at the top of the `<script>`
     block. Its shape:
     - `label` — e.g. `"September 14-20, 2026"`
     - `refreshed` — the "Refreshed <Mon DD, YYYY> - ..." line
     - `trends` — array of `[name, description]` pairs (2-3), rendered in the "Trending this week" bar
     - `posts` — array of 7 objects, one per day Mon->Sun, each with:
       `n` (day number), `dow` (`"Mon"`..`"Sun"`), optional `closed:true`, `pillar`, `goal`, `title`,
       `hook`, `filming` (array of shot-list strings), `onscreen`, `vo`, `caption`, `cta`,
       `hashtags` (array of 6-9), `filename`
   - `pillar` must be a key of the `PILLARS` map further down: `party`, `salon`, `spa`, `pierce`,
     `trust`, `camp`, `bts`, `local`.
   - **Update `WEEK` only.** `const BANK` (evergreen Idea Bank) is intentionally static - leave it
     alone unless asked. Do not restructure the HTML/CSS.
3. Note the exact variable name and shape so you can refresh it each week without touching the design.

---

## STEP 1 — DATES

Run `date`. The page covers the **current week, Monday–Sunday** (today through the coming Sunday).
Capture: the week label (e.g. `September 14–20, 2026`), a "Refreshed <Mon DD, YYYY>" line, and the
7 day-numbers for Mon–Sun.

---

## STEP 2 — TRENDS

Web-search what short-form formats and trending audio are current **this week**
(e.g. "trending Instagram Reels TikTok audio this week", "short-form video format trends").
Pick **2–3** that genuinely fit kids'-salon/spa/party footage — do not force trends that don't match.
Surface them on the page and weave them into the relevant posts.

---

## STEP 3 — BRAND CONTEXT (baked in — no external file needed)

- **Sweet & Sassy of Cumming** · 410 Peachtree Parkway, Suite 342, Cumming, GA 30041
- Call **(678) 931-8356** · Text **770-781-3863** · **sweetandsassy.com/cumming**
- Hours: **Tue–Sat 10–7, Sun 12–6, Closed Monday**
- Tagline: **"Where Little Moments Become Big Memories."**
- Services: kids' haircuts (incl. **"My First Haircut"** with keepsake lock of hair + certificate),
  styling/braiding, mani/pedis (**Sweet Treat**), makeovers, gentle **ear piercing** (both ears at
  once, sterile, hypoallergenic, certificate), and turnkey **birthday parties** — themes: Perfect
  Princess, Pop Star, Spa-tacular, Fashion Runway, Eras, K-Pop Glam, Design Your Dream Bash. All
  parties hosted start to finish. Ages ~4–12.

**Rules (non-negotiable):**
- Never invent pricing, availability, party inclusions, or staff names beyond what's known.
- Direct parents to call/book online for dates; never claim a specific slot is open.
- No fake urgency ("stop scrolling", "book now before it's gone"). Tasteful emoji. Vary captions.
- The child is the guest but the **PARENT is the buyer** — captions/CTAs land with moms/gift-givers.
- On-camera is the girls/stylists on staff. **A person named Phil must NEVER appear on camera or in
  any concept.**
- Filming children: favor hands/details/reactions/backs/the team/the space; full faces only with
  parent approval — bake those alternatives into every shot list.

---

## STEP 4 — BUILD THE WEEK

Seven posts, **one per day Mon–Sun**, each native to Reels + TikTok + YouTube Shorts.
**Party-weighted:** about **2 of 7** are party spotlights (rotate which themes each week).
Fill the rest across the other pillars; **do not repeat a pillar back-to-back.**

Suggested rhythm: Mon behind-the-scenes/team · Tue party · Wed spa or salon proof/before-after ·
Thu party or seasonal/gift · Fri trend/reveal · Sat salon/local · Sun ear piercing or spa/milestone.
Favor what's seasonally timely (back-to-school, fall, Grandparents Day in Sept, Halloween pre-sell in
fall, holidays). Rotate CTAs so none repeats back-to-back:
book online · call (678) 931-8356 · text 770-781-3863 · come see us at 410 Peachtree Parkway ·
tag a mom whose kiddo would love this · book a party.

**Each post needs all NINE items:** (1) title/concept (2) hook that lands in the first 1–2 sec
(3) shot-by-shot filming instructions (4) on-screen text (5) spoken line/VO — or "trending-audio only"
(6) caption (parent-facing, varied openings) (7) call to action (8) 6–9 hashtags including
`#SweetAndSassyCumming` + the right service/event tag + local tags
(`#CummingGA #ForsythCounty #NorthAtlanta`) (9) filename like `SSCumming_MMDD_ShortName.mp4`.

**Apply the new content to the page's data object in its own shape.** If the page is trend-centric,
map the 2–3 trends into the trend cards (name, "why it works", "ways to try it", caption starter +
hashtags) and fold the 7 day ideas into whatever list the page uses. If the page is day-by-day, fill
its 7-post array. Either way: update the **data only**, keep the design.

---

## STEP 5 — VALIDATE

Quick sanity check before committing: the week label + refreshed line are correct; there are 7 day
ideas Mon→Sun; ~2 party spotlights; no back-to-back pillar repeat; every hashtag set is 6–9 long;
no invented pricing/slots; no fake urgency; Phil appears nowhere. If the page uses JS data, confirm
it still parses (open it, or `node -e` eval the object) so the site doesn't break.

---

## STEP 6 — SHIP IT (the whole point)

```bash
git add -A
git commit -m "Weekly content refresh: <week label>"
git push
```

Render auto-deploys from the pushed commit. After ~1–2 minutes, load the live URL and hard-refresh
(Cmd/Ctrl+Shift+R) to confirm the new week shows. If Render doesn't pick it up, check the Render
dashboard that the service is connected to this repo + branch and that auto-deploy is on.

---

## HANDING THIS TO CLAUDE CODE

Drop this file in the repo root (or `.claude/`), plus the finished content file for the current week.
Then just say: **"Run the weekly runbook — update this week's page and push."**
To make it a one-word command, save it as a slash command at `.claude/commands/weekly.md` and run
`/weekly`. To make it hands-off, schedule it (cron on your machine, a Render cron job, or a Cowork
scheduled task **scoped to this repo** so it can push).
