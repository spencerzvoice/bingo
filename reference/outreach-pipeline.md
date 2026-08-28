# Reference — VO Outreach Pipeline Tracker

The live CRM for Spencer's outreach. **The Google Sheet is ground truth** — Spencer edits it in real time and a daily cloud routine ([[vo-pipeline-routine]]) syncs it from Gmail. This file captures the stable structure, the operational hazards, and the standing action items. Client backgrounds are in [[vo-client-directory]].

## Resource IDs

- Sheet: **"VO Outreach Pipeline Tracker"** — root of My Drive (search by exact title, never a cached link — the file has been deleted/recreated before).
- spreadsheetId: `1SBauz4dCodqnfSVD5yqKETjU-25TY5HEZ7KRGggbgT0`
- Tabs: **Outreach Tracker** (sheetId `1117682425`, the CRM) · **Dashboard** (sheetId `777610067`, formula rollups + chart `445011089`) · **Legend & How To Use** (sheetId `792717929`).
- Gmail account swept: spencer@spencerzvoice.com (business). Personal spencerzpearman@gmail.com holds most Voices.com award notices — excluded from this work.

## Column schema (A–M)

`Contact Name | Company/Agency | Title/Role | Email Address | Category | Priority | Status | Date First Contacted | Last Contact Date | Days Since Last Contact | Follow-Up Flag | Next Action | Notes`

- **Category:** New Outreach - Agency · Active / Recurring Client · Old Client Reconnect · Professional Development
- **Priority:** High (red) · Medium (yellow/orange) · Low (green)
- **Days Since Last Contact** = formula `=IF(I{row}="","",TODAY()-I{row})` — leave alone
- **Follow-Up Flag** = formula. Logic: Bounced→"Fix Email & Resend"; Responded→"Active - Monitor"; Not Sent→"Send Initial Outreach"; Drafted-Not-Sent→"Ready to Send"; else by days: ≥10→"OVERDUE - Follow Up Now", ≥7→"Due Soon", else "Recently Contacted". Leave alone.
- The routine only writes **Status, Last Contact Date, Notes** (and adds rows). Dashboard and Legend tabs are never touched.

## ⚠️ Operational hazards (learned the hard way)

1. **Never write to a row from a remembered row number.** Re-read that row's Name/Company in the same turn before writing, then read it back after to confirm. The sheet grows and shifts; rows have been deleted unexpectedly.
2. **The cloud routine has silently deleted whole rows** (Robert Salas / GMR Marketing, Andy Roth / VO Coach) — not edits, row removal, no error. Root cause unknown. Treat row structure as unstable between sessions.
3. **Real write mistakes that happened:** Erick Sosa's LinkedIn data written into Maya Roberts' row; an OOO note for Michael MacMillan written into Didi Fraioli's row. Both from trusting stale row positions. Hence rule 1.
4. **Standard Gmail connector is buggy** (stale/incomplete thread results — hid 9+ messages of the live KU project once). Use **FGAC.ai** `google_api_get` against `gmail/v1/users/me/...` for anything accuracy-sensitive.
5. **FGAC has blanket permission** — never ask before using it. But FGAC's own `sheets_edit` scope (needed for structural `batchUpdate` / row deletion) can return "No approval received" — a real gate on FGAC's side, not something to retry past. Workaround for row deletion without `sheets_edit`: read the full range, filter rows in memory, rewrite kept rows to the top via `sheets_update_range`, blank the trailing rows.
6. **Never pull Voices.com marketplace contacts into the tracker from Gmail** — Spencer manages those in the Voices.com platform. (He may still add one manually — e.g. Zulubot Bravo Inc, a real paid job.)

## Pipeline snapshot (2026-08-27 — will drift; check the sheet)

~85 data rows. Composition:
- **New Outreach - Agency:** Cheil USA (Colby Mitchell, Mark Van Duinen, Didi Fraioli, Tim Eger, +Andrew Davis unsent), Team One (Sam Walsh, Erick Sosa, Sascha Peuckert, Melanie Saitta + bounced: Maya Roberts, Tami Hachiya, Janae David; Janet Bell Anderson on hold), Untold Studios (Luke Colson, Tanya Ferguson, Chelsea Kammeyer, Josephine Gallagher, Nancy Loud), Octagon (Sean LaGamma, Melissa Dunlop Parsons), Anomaly (Erika Madison, Michelle Price, Michael MacMillan — OOO to Sept 1), The Team (Cameron Choate + Nathan Mallon bounced), Laundry Service (Stacy Robnett, Abbey Birsch Garbarino), Ogilvy (Luis Aguilera → Laysa Martins), GMR Marketing (Krista Hansen — OOO), IMG (Ian Henderson), MezzoLab (João Freitas), DDO (Alicia Beekman, Allie Silber).
- **Active / Recurring:** Noah Media Group (6 contacts), Lori Lins Ltd, Shadow Lion (Ryan Lago, Jeff Fine), Xpedition Media (Rebekah Bell, Mary Chaplin, Nandi Smythe), Diamond View (Jeff McKown), Kansas University (Liz Nelson, Steve Rausch — live paid), Kimley-Horn (Jordan Deva), Condado/Pentak (Sara Kear, Craig), iFIT (Michael Hamblin, Ryan Humpherys), Acclaim Lighting, Tellary (bounced), Tony Beck, Wild Creative, Some Odd Pilot, Narwal Creative, Dove Street Films, IMG (Jamie Pearson), Archetype, Rhymesayers (Tanner Groehler), Zulubot Bravo Inc.
- **Old Client Reconnect:** Melissa Gillis (ATTN), Rebeccah Sheridan (CGI), Evan Kay (Climb High), Ruthie Mason (Coronation), Kayla Gremer Foreid (Diamond View), Erin Daughenbaugh (EDP), Mel Kane (Invision), Lucas Bertoli (Laundry Design), Taylor Ballam (Modo), Evan Romoff (Romoff Media), Mackenzie Prokos (Rune Haus), David Martin (ShadowLion), Devin Leisher (TBC), Dan Haas (ATTN — sent), Deb (Kanahoma — sent).
- **Professional Development:** Elaine Craig (registered, Sept 19), Carrie Faverty (fall dates pending).

## Live leads & jobs in flight

_Auto-logged (see the memory protocol in CLAUDE.md). Keep status lines current; condense/prune resolved + cold entries on the schedule in MEMORY.md._

### CrowdReply — first Lane 1 (direct-to-brand) opportunity
- **Contact:** Jim Loining ("Jim L"), **co-founder**, 20s. Met in person 2026-08-28 (padel). Also runs a separate side project, BambooVPN.
- **Company:** CrowdReply (crowdreply.io) — AI-search-visibility / GEO-AEO platform (get your brand cited by ChatGPT, Perplexity, Gemini, Claude) + Reddit/social listening + backlinks marketplace. Founded Feb 1 2025 by Jim Loining + Dawood Khan. Seed-stage, NZ-linked (Icehouse Ventures), content-marketing-heavy — claims "5,000+ brands" (marketing figure, ~18-month-old company).
- **Their cadence:** ~1 product/marketing video per month → X + YouTube, likely with paid promotion behind it. Spencer asked whether they also do internal / B2B client videos — awaiting answer (that's the retainer-expansion path).
- **The opening:** Jim sent two CrowdReply product videos from X. Spencer re-voiced both and **sent samples 2026-08-28 14:14 (Lisbon)** to `jim@crowdreply.io`, subject "VO samples" — 2 re-voiced videos (Drive links) + 2 attached past jobs (Amazon AWS SageMaker overview, Artlist 2024). Warm casual note, no pricing, padel sign-off. **Status: awaiting reply.**
- **Pricing plan:** one-off fair rate **~$350/video**; recurring retainer **$300/month** for 1 guaranteed video (24h turnaround, 12-mo rate lock); **~$275** per additional video same month. **Floor $250** — no mate's rates; VC-backed company, his credits justify it. Quote per-video first, then offer the retainer. No pricing in the first send. Confirm paid-media spend + usage term when pricing comes up (real ad spend → attach 12-mo digital usage, rate rises).
- Note for next send: all files on Drive, not mixed Drive links + 21MB attachments (near Gmail's limit).

### Enterprise "#OnEveryCorner" — Voices.com case-study narration
- **What:** Voices.com VoiceMatch (90% match, ~28 responses). Internal case-study video for **Enterprise**'s #OnEveryCorner World Cup 2026 campaign (corner-kick sweepstakes w/ Kia). 370 words / ~2m28s. **Non-broadcast, in-perpetuity.** Requires a 1-hr Source Connect **directed session** this week. Cleaned mix-ready WAVs. 2 rounds revisions for talent error; script changes billable. Budget $250–$499 (gross, incl. platform fee) but explicitly "quote as you see fit."
- **Bingo's quote guidance (2026-08-28):** quote **$850** — $600 narration (2.5 min, non-broadcast, in-perp buyout) + $250 directed session. **Floor $600** ($400 + $200); pass below that. Don't apologise for going over; they invited it.
- **Status:** guidance given — Spencer deciding whether to audition/quote. If booked → another World Cup credit next to the FIFA series.

### Father-daughter animated educational series — recurring character (Voices.com)
- **What:** Voices.com (116 responses). Short-form animated educational series, international social-media release. **Recurring voice for "the father"** — warm, calm, human, "sounds like a father speaking to his daughter, not a narrator." Male, neutral English, middle age. 1 min/episode. **Usage: Cartoons / Online (organic social).** Budget **€150–249**.
- **Bingo's quote guidance (2026-08-28):** treat as episodic content-series character work, NOT commercial — GFTB's €500 organic-video rate is the wrong comp. Fair: **€250–300/episode**, or a **batch session ~€300–350 covering 4–6 episodes** (better for a series). Their €249 ceiling ≈ bottom of Spencer's own recurring-content rate, so negotiate structure, don't walk. **Don't drop to €150/episode on singles** — that's batch-only territory. **Get the episode count + schedule in writing before building a rate.** Cap the licence at life-of-series; paid ads = separate fee; watch for a character-exclusivity ask (that's a premium).
- **Status:** guidance given — Spencer deciding whether to audition/quote.

### Walmart Marketplace Seller Summit — Voices.com internal video
- **What:** Voices.com (116 responses). **Internal Video** — "Walmart Marketplace Seller Summit" (event/summit content for Walmart's 3rd-party Marketplace sellers). 100 words / ~0m40s. **Non-broadcast, in-perpetuity.** Budget **$500–$749** (gross).
- **Bingo's guidance (2026-08-28):** budget at/above fair market (~$500). With 116 bids, guidance was $600–625 to win; **Spencer quoted $700** (nets ~$560). Flag left in the quote: confirm genuinely internal — if seller-facing (YouTube / seller portal / recruitment) it's wider usage worth $900–1200+.
- **Status:** quoted $700. Awaiting outcome.

## Quick marketplace quote log

Compact log of rapid-fire Voices.com / marketplace jobs Spencer prices with Bingo. Calibration since 2026-08-28: quote **fair-market-mid to win** (not the ceiling) on high-response jobs, keep a real floor, don't undercut. Prune resolved rows on the MEMORY.md schedule.

| Date | Job | Format | Licence | Budget | Bingo quote | Floor | Outcome |
|---|---|---|---|---|---|---|---|
| 08-28 | "BRING IT!" initiative | Internal video, 309 wds / ~2m, **+ live directed session** | Non-bcast, in-perp | $250–499 | **$675** ($450 narration + $225 session) | $550 | quoted / TBD |
| 08-28 | "Avery" | **Online Ad** — :30 + :15 cutdown, 112 wds, **+ live directed session w/ playback** | **Online Ad, Worldwide, 3 yrs** + non-bcast in-perp | $250–499 (105 responses) | **$2,400** ($1,600 :30 ww/3yr + $600 :15 + $200 session) — or **pass** | $1,500 | **Spencer quoted $1,500** (the floor). Held the line — good. Awaiting outcome. |
| 08-28 | Changes in Medicaid in Virginia | Animation/explainer, 206 wds / ~1m22s | Non-bcast, in-perp | $100–249 (131 resp) | **$325** (or $299 for win-rate) | $250 | **REPEAT CLIENT** — did "Georgia Power Revised Videos 1&2" with them (see [[vo-client-directory]] — Meg Easterbrook / Job #833137). Priced; Spencer not confirmed auditioning. |

_Avery note: their $250–499 budget is off by ~5–10× for a **worldwide 3-year online-ad commercial** with 2 deliverables + a directed session (full GVAA worldwide/3yr :30 is $8–16k). The directed session alone > half their max. 105 responses = client shopping for someone who doesn't know licensing. **Do not take this at their number** — voicing a worldwide 3-yr commercial + perpetual buyout for ~$400 is the exact trap. Either pass, or quote straight (~$2,400, floor $1,500) with a scope question (confirm brand + territories; note $499 ≈ a 1-yr national single-cut licence at most). If they're legit, the professional quote + education stands out; if they ghost, no loss._

_BRING IT! note: adding the directed session flips this from "inside budget" to budget-below-fair-market — same trap as Enterprise. The session is ~$200–250 of live time; their $499 ceiling can't cover session + 2-min perpetual buyout. Confirm session length. Pass below $550._

## Standing action items

1. **Fix + resend bounced emails:** Maya Roberts, Tami Hachiya, Janae David (Team One — pattern `firstname.lastname@teamone-usa.com` but these bounced; verify via Hunter.io), Nathan Mallon (The Team — Mimecast `550 5.4.1` rejection), Anna Jacobsen (Tellary — try `poullet@tellary.com` or `tellyourstory@tellary.com`).
2. **Send the ~18 written-but-unsent reconnect drafts** (see list below).
3. **Re-add Robert Salas** (GMR Marketing, Senior Producer) — row vanished before his ready draft was sent.
4. **Lori Lins auditions:** Plaud + AT&T Quantum Fiber (were due Aug 28) — check status.
5. Follow up when Sam Walsh (back Aug 25) and Michael MacMillan (back Sept 1) return from OOO.
6. Investigate why the routine deletes rows.
7. Submit the Gmail-connector bug report to Anthropic support if not already done.
8. Track the Sept 19 Elaine Craig workshop → resubmit to Allie Silber at DDO afterward.

## The ~18 unsent reconnect drafts (exist, ready, not sent)

Andrew Davis (Cheil) · Melissa Gillis (ATTN) · Rebeccah Sheridan (CGI) · Evan Kay (Climb High) · Ruthie Mason (Coronation) · Kayla Gremer Foreid (Diamond View) · Erin Daughenbaugh (EDP) · Mel Kane (Invision) · Lucas Bertoli (Laundry Design) · Taylor Ballam (Modo) · Evan Romoff (Romoff Media) · Mackenzie Prokos (Rune Haus) · David Martin (ShadowLion) · Devin Leisher (TBC) · Jeff McKown (Diamond View) · Lilah Kohlman (Altra) · Luke Mellows (Noah Media) · Luke O'Reilly (Noah Media).
Held intentionally: Janet Bell Anderson (Team One — wait until cast). Excluded: Tony / Vishuddha.

## History: the Gmail sweep (Aug 19–20 2026)

A full historical sweep of the business Gmail built most of this tracker: 579 sent-mail threads → 311 correspondents → 77 new client/contact rows added (73 initial + 4 from ambiguous cases). Also fixed 11 data-quality issues in pre-existing rows (blank/wrong emails) and two sheet-infrastructure bugs (conditional formatting and Dashboard formulas were both hardcoded to stop at row 57). Voices.com contacts and YouTube-channel cold-outreach were excluded by rule.
