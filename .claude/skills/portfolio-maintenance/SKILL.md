---
name: portfolio-maintenance
description: Resume or extend Prashant Seshadri's terminal-style portfolio website (modeled on Jenny Park's build) — checking the status tracker, working one step at a time, and keeping GitHub + Google Drive in sync
user-invocable: true
---

# Portfolio Maintenance

This skill governs how to work on `portfolio-website` — a terminal-styled Next.js portfolio for Prashant Seshadri, modeled after Jenny Park's build (`Resume/GitHub Related/portfolio-website-main-jenny`).

## Always start here

1. Read `README.md` at the repo root — it is the single source of truth for what's done and what's next. It contains a status table (☑/☐ checkboxes) and a "CURRENT STEP" pointer.
2. Show the current status table to Prashant before doing anything else.
3. Work on whichever step is marked ☐, in order — do not skip ahead to later steps even if related work seems convenient. Confirm before starting non-trivial changes.
4. Update the table's checkbox and add a session log entry in `README.md` as each step completes.

## Keep GitHub and Google Drive in sync

Every code or content change must be mirrored to **both**:
- **GitHub:** `git add` / `commit` / `push` to `github.com/psaiquest/portfolio-website`
- **Google Drive:** copy the same changed file(s) into the locally-synced mirror at
  `/Users/prash29/Library/CloudStorage/GoogleDrive-psaiquest@gmail.com/My Drive/Claude/Portfolio - Related Claude`
  (Drive folder ID `1FW_rqIps2KsZdfgboaniM3Bm6ps9eUTn`, path `My Drive > Claude > Portfolio - Related Claude`)

Use a plain `cp` for the Drive sync — it's a real synced folder on disk, not a Drive-API upload. **Never** hand-encode a binary file as base64 for the Drive API (`create_file`/`base64Content`) — a large base64 string was previously mistyped mid-transfer and silently corrupted a `.docx` (wrong ZIP end-of-file bytes, wrong file size), and there is no Drive delete tool to clean up such mistakes afterward. If a Drive-API upload is ever unavoidable, verify with `download_file_content` + byte/hash comparison before considering it done.

## How the site works (for extending it)

Single client component (`app/page.tsx`) with three layers, all originally adapted from Jenny's mechanics:
1. **Static content** — hero (name/role/bio/social links), skills, projects, contact — all hardcoded data arrays at the top of the file, no CMS/backend.
2. **Reveal animation** — a state machine steps through 5 sections in sequence; each types out its prompt line, runs a fake "N tool uses" block (cosmetic only — no real file reads), then streams its content. Plays once per browser tab via `sessionStorage`, skipped entirely under `prefers-reduced-motion`. "New session" button in the chrome bar replays it.
3. **Terminal chat** — `data/qa.json` holds regex `patterns` → `answer` pairs; a `$ ask>` input matches typed questions against them and streams back the match (or a fallback). No LLM call, no backend — pure client-side regex.

Deploy: `next.config.ts` sets `output: "export"` + `basePath: "/portfolio-website"`; `.github/workflows/deploy.yml` builds and publishes `out/` to GitHub Pages via GitHub Actions on every push to `main`.

## Known open items (check README.md for current state)

- Profile photo is a placeholder ("PS" initials) — swap in when Prashant provides one
- `tripflow-v2` and `action-portfolio` GitHub repos are the *real* TripFlow/Smart Portfolio projects but kept **private** by Prashant's choice — the portfolio site cannot deep-link to them until/unless he makes them public
- `joy-upload-dash` and `assignment5-airbnb-dashboard` repos — no decision made on these yet
- LinkedIn Featured/About section link is a manual step for Prashant (no API access)
