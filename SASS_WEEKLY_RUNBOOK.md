# Sweet & Sassy of Cumming — Weekly Trend Refresh (Claude Code)

**The idea:** every Monday, find what's **actually gaining traction** in short-form video right now,
and put 4–5 of those trends on the team's page as light prompts they can riff on.

**Not** shot-by-shot scripts, VO lines, or filenames. The team knows how to film. What they need is
*"here's what's working this week, here are a few ways to use it with what's in the chair today."*

---

## THE PIPELINE

```
Edit index.html  →  git commit  →  git push (main)  →  Render redeploys  →  live site updates
```

The live page is served by Render from the **`main`** branch of this repo. **The commit is the deploy.**
Skip the push and nothing changes for the team.

---

## STEP 1 — DATES

Run `date`. The page covers the **current week, Monday–Sunday**. You need the week label
(e.g. `September 14–20, 2026`) and a `Refreshed <Mon DD, YYYY>` line.

---

## STEP 2 — FIND WHAT'S GAINING TRACTION

Web-search what's trending in short-form **this week** — e.g. "trending Instagram Reels audio this
week", "TikTok trending sounds this week", "short-form video format trends".

Pick **4–5** that genuinely work with kids'-salon/spa/party footage. Prefer trends that:
- need **no faces** (hands, details, backs, the room, the team) — the face rule is non-negotiable
- work with whatever is *already happening that day* — a mani, a braid, a party setup, a restock
- are easy to shoot on a phone in one take

**Do not force a trend that doesn't fit.** A trend the team can't actually film is worse than
one fewer card. It's fine to round out the list with one or two "Always works" evergreens.

---

## STEP 3 — BRAND CONTEXT (baked in)

- **Sweet & Sassy of Cumming** · 410 Peachtree Parkway, Suite 342, Cumming, GA 30041
- Call **(678) 931-8356** · Text **770-781-3863** · **sweetandsassy.com/cumming**
- Hours: **Tue–Sat 10–7, Sun 12–6, Closed Monday**
- Services: kids' haircuts (incl. **"My First Haircut"** with keepsake lock + certificate),
  styling/braiding, mani/pedis (**Sweet Treat**), makeovers, gentle **ear piercing** (both ears at
  once, sterile, hypoallergenic, certificate), and turnkey **birthday parties** — themes: Perfect
  Princess, Pop Star, Spa-tacular, Fashion Runway, Eras, K-Pop Glam, Design Your Dream Bash.
  Ages ~4–12.

**Rules (non-negotiable):**
- Never invent pricing, availability, party inclusions, or staff names.
- Never claim a specific slot is open — point people to call or book online.
- No fake urgency ("stop scrolling", "book now before it's gone"). Tasteful emoji.
- The child is the guest but the **PARENT is the buyer** — captions land with moms and gift-givers.
- On-camera is the girls/stylists on staff. **A person named Phil must NEVER appear on camera or in
  any concept.**
- **Filming children:** favor hands / details / reactions / backs / the team / the space. Full faces
  only with parent approval. Favor trends that work without faces at all.

---

## STEP 4 — UPDATE THE PAGE

All content lives in **one object, `const WEEK`**, at the top of the `<script>` block in `index.html`:

- `label` — e.g. `"September 14–20, 2026"`
- `refreshed` — e.g. `"Refreshed Sep 14, 2026"`
- `ideas` — array of 4–5 cards, each:
  - `kind` — `"Trending sound"`, `"Trending format"`, or `"Always works"`
  - `name` — the trend, as the team would recognize it
  - `why` — one or two sentences on *why it's working right now*
  - `tryit` — 3 short bullets: concrete ways to use it with real salon/spa/party footage
  - `caption` — a caption *starter*, one line, for them to make their own
  - `hashtags` — 6 tags: `#SweetAndSassyCumming` + service/local
    (`#CummingGA #ForsythCounty #NorthAtlanta`)

**Update `WEEK` only. Do not restructure the HTML/CSS.** Keep it light — if a card is starting to
read like a script, cut it back.

---

## STEP 5 — VALIDATE

Week label and refreshed line correct · 4–5 cards · every `tryit` is filmable with what's on hand ·
6 hashtags each · no invented pricing or slots · no fake urgency · Phil nowhere · face-safe.
Confirm the JS still parses (open the page, or eval the object) so the site doesn't break.

---

## STEP 6 — SHIP IT (the whole point)

```bash
git add -A
git commit -m "Weekly trend refresh: <week label>"
git push origin main
```

Render auto-deploys from `main`. After ~1–2 min, hard-refresh the live URL to confirm.

> **History:** this used to publish to a claude.ai artifact that the Render page was never connected
> to, so the live site silently went stale. The live page is **this repo, `main` branch**. If a run
> can't push, the run failed — say so; don't publish somewhere else and call it done.
