# Prashant Seshadri — Portfolio Website (Build Tracker)

Modeled after Jenny Park's terminal-style portfolio (`portfolio-website-main-jenny`, reviewed under `Resume/GitHub Related/`). This file is the single source of truth for what's done and what's next — read it at the start of any session to know where we left off.

**Target repo:** `github.com/psaiquest/portfolio-website` (separate from the resume repo)
**Target live URL:** `https://psaiquest.github.io/portfolio-website`
**Google Drive mirror:** `My Drive > Claude > Portfolio - Related Claude` (folder ID `1FW_rqIps2KsZdfgboaniM3Bm6ps9eUTn`) — local sync path: `/Users/prash29/Library/CloudStorage/GoogleDrive-psaiquest@gmail.com/My Drive/Claude/Portfolio - Related Claude`

**⚠️ Standing rule (2026-07-12):** Whenever a code change is made to this project, mirror the same changed file(s) into the Drive folder above (plain `cp`, since it's locally synced — no Drive API/base64 needed) in addition to committing/pushing to GitHub. Keep both in sync every time, not just at milestones.

---

## Status table

**🎉 ALL STEPS COMPLETE. LIVE: https://psaiquest.github.io/portfolio-website/**

| # | Task | Done | Notes |
|---|---|:---:|---|
| 0.1 | Scaffold Next.js app (`create-next-app`, TypeScript + Tailwind + App Router) | ☑ | Hit two machine issues along the way: root-owned `~/.npm` cache (fixed via `sudo chown`), directory conflict from a partial first attempt (resolved by finishing `npm install` in place). Verified with `npm run dev` — HTTP 200. |
| 0.2 | Init local git repo | ☑ | Set global git identity (Prashant Seshadri / GitHub noreply email), `git init`, first commit `8e2ae80` (17 files, scaffold + tracker README) |
| 0.3 | Create GitHub repo `psaiquest/portfolio-website` | ☑ | Created **private**, via `gh repo create --source=. --remote=origin` |
| 0.4 | Push initial commit, connect local repo to GitHub remote | ☑ | `git push -u origin main` — verified live on GitHub, branch `main` tracked |
| 1.1 | Confirm content source: bio, skills, projects, contact | ☑ | Using locked resume content per `Resume/CLAUDE.md` |
| 1.2 | Add profile photo `public/me.png` | ☐ | Deferred — using "PS" initials placeholder avatar for now, swap in real photo later |
| 1.3 | Build static terminal page — hero, bio, skills, projects, contact (no animation yet) | ☑ | `app/page.tsx` + `app/globals.css` + `app/layout.tsx` rewritten. Type-checked clean, verified rendering via `npm run dev` (HTTP 200, expected text present) |
| 1.4 | Review static page on localhost, get sign-off | ☑ | Prashant reviewed at localhost:3000, approved |
| 2.1 | Add typing effect + collapsible "tool use" blocks + section reveal | ☑ | `page.tsx` rewritten as client component with state machine (adapted from Jenny's mechanics), reduced-motion + sessionStorage-once handling, "new session" replay button. Type-checked clean. |
| 2.2 | Verify animation plays once/session, respects reduced-motion | ☑ | Prashant confirmed in-browser |
| 3.1 | Write `data/qa.json` (~15-20 Q&A pairs about Prashant) | ☑ | 18 entries, first-person voice, consolidated from Prashant's feedback + ChatGPT draft, corrected a factual error (MBA is UC not Cincinnati), no employer name anywhere. Validated as clean JSON. |
| 3.2 | Build terminal chat box (regex match, no backend/LLM) | ☑ | Prashant tested in-browser: matched question streamed correct answer, unmatched question correctly triggered fallback |
| 4.1 | Add `.github/workflows/deploy.yml` (GitHub Actions → Pages) | ☑ | Mirrors Jenny's workflow. Repo made **public** (Prashant's call — plain professional info only, no SSN/address/phone anywhere) |
| 4.2 | Set `basePath`/`unoptimized` in `next.config.ts` | ☑ | `output: "export"`, `basePath: "/portfolio-website"`, verified via local build — `out/index.html` contains expected content |
| 4.3 | Enable Settings → Pages → Source → GitHub Actions | ☑ | Enabled via `gh api POST .../pages -f build_type=workflow` |
| 4.4 | Push to `main`, verify live deploy | ☑ | Pushed `8e72659`, Actions run succeeded in 47s, verified HTTP 200 + correct content live |
| 5.1 | Add live URL to resume, GitHub profile README, LinkedIn | ☑ | GitHub profile README updated (`GitHub Repo/README.md`); resume `build.js` + regenerated `.docx` + `.html` all updated — added clickable Portfolio + LinkedIn links, removed 2 broken/non-functional project GitHub links (tripflow-v2 private, Smart Portfolio missing href) along the way. LinkedIn itself needs Prashant to add the link manually (no API access) — Featured or About section. |

---

## Open blockers / inputs needed from Prashant
- [ ] Profile photo for `public/me.png`

---

## Related: GitHub repo cleanup (from psaiquest profile review, 2026-07-10)

**Initial pass missed private repos** — first review only saw the 5 public repos via unauthenticated web scrape. After `gh auth login`, found 9 total (5 public + 4 private). Corrected findings below.

### Deleted (2026-07-10)
| Repo | Was | Reason |
|---|---|---|
| `amazontest` | Public, 1 commit, throwaway HTML | Empty/stale |
| `amazonb2c` | Public, 1 commit, placeholder HTML | Empty/stale |
| `rag_simulator` | Public, completely empty | Empty/stale |
| `tripflow` | Public, 1 commit, thin duplicate | Superseded by private `tripflow-v2` (more complete, 3 commits, Lovable-built) |

### Remaining repos
| Repo | Visibility | What it is | Status |
|---|---|---|---|
| `rag_simulator_2` | Public | Real content, 5 commits | Keep as-is |
| `tripflow-v2` | Private | The real TripFlow project (resume-featured) | **Not visible to recruiters** — kept private per Prashant's call for now, revisit later |
| `action-portfolio` | Private | Confirmed via its own README: this IS the "Smart Portfolio" resume project, just under a mismatched repo name | **Not visible to recruiters** — kept private per Prashant's call for now, revisit later |
| `joy-upload-dash` | Private | Unrelated TanStack/Radix-UI dashboard — not one of the 3 locked-in resume projects | Needs a decision later (delete / keep private / rename) |
| `assignment5-airbnb-dashboard` | Private | Recent course/bootcamp assignment | Needs a decision later (delete / keep private / rename) |

- [ ] Revisit later: make `tripflow-v2` and/or `action-portfolio` public so resume/portfolio links actually resolve for recruiters
- [ ] Decide fate of `joy-upload-dash` and `assignment5-airbnb-dashboard` (not discussed yet)

---

## Session log
**2026-07-10** — Reviewed Jenny's actual source code (`page.tsx`, `layout.tsx`, `globals.css`, `deploy.yml`) to understand real mechanics (see chat for plain-language explanation). Installed `gh` CLI (verified checksum against official release), authenticated as `psaiquest`. Corrected initial repo review after discovering 4 private repos missed by the unauthenticated scrape. Deleted 4 stale/duplicate repos (amazontest, amazonb2c, rag_simulator, tripflow) with explicit per-repo confirmation. Scaffolded the Next.js app (TypeScript + Tailwind + App Router) — fixed a root-owned npm cache issue along the way. App not yet customized with Prashant's content.

**2026-07-11/12** — Built the full site: static content (Phase 1), typing/reveal animation (Phase 2), terminal chat box with `data/qa.json` (Phase 3) — all reviewed and tested by Prashant in-browser. Discussed public-vs-private tradeoffs for GitHub Pages (identity-theft concern addressed — only name/professional bio/career email exposed, no SSN/address/phone anywhere); Prashant chose to make the repo public. Added GitHub Actions deploy workflow, enabled Pages via `gh api`, pushed, and verified the **live site** at https://psaiquest.github.io/portfolio-website/. Fixed a word-tokenizer bug that dropped spaces after accent spans in the bio text ("solutionsfor", "100clients") and capitalized "Financial Services" — verified fix live via curl. Only 5.1 (link the URL from resume/GitHub profile/LinkedIn) remains.

---

## Local dev (standard Next.js — for reference)

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to view. Edit `app/page.tsx` — the page auto-updates. Uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to load the Geist font family.
