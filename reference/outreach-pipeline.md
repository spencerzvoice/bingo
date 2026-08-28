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

## Live leads (not yet in the sheet)

### CrowdReply — first Lane 1 (direct-to-brand) opportunity
- **Contact:** Jim Loining ("Jim L"), **co-founder**, 20s. Met in person 2026-08-28 (padel). Also runs a separate side project, BambooVPN.
- **Company:** CrowdReply (crowdreply.io) — AI-search-visibility / GEO-AEO platform (get your brand cited by ChatGPT, Perplexity, Gemini, Claude) + Reddit/social listening + backlinks marketplace. Founded Feb 1 2025 by Jim Loining + Dawood Khan. Seed-stage, NZ-linked (Icehouse Ventures), content-marketing-heavy — claims "5,000+ brands" (marketing figure, ~18-month-old company).
- **The opening:** Jim sent Spencer two of their product videos from X. Spencer re-voiced both and **sent samples 2026-08-28 14:14 (Lisbon)** to `jim@crowdreply.io`, subject "VO samples" — 2 re-voiced CrowdReply videos (Google Drive links) + 2 attached past jobs (Amazon AWS SageMaker overview, Artlist 2024). Warm casual note, no pricing, padel sign-off. **Awaiting reply.** Goal: land the recurring monthly video, then expand.
- Note for next send: put all files on Drive rather than mixing Drive links + 21MB of attachments (close to Gmail's limit).
- **Their cadence:** ~1 product/marketing video per month, posted to X + YouTube, likely with paid promotion behind it. Spencer has asked whether they also do internal / B2B client videos — awaiting answer (that's the retainer-expansion path).
- **Pricing plan (2026-08-28):** one-off fair rate **~$350/video**; recurring retainer **$300/month** for 1 guaranteed video (24h turnaround, rate locked 12 months); **~$275** per additional video in the same month. **Floor $250** — do not go "mate's rates" below that; it's a VC-backed company and Spencer's credits justify it. Quote per-video first, then offer the retainer as the better deal. No pricing in the first send — samples only. Confirm paid-media spend + usage term when pricing comes up (real ad spend → attach a 12-month digital usage term, rate goes up).

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
