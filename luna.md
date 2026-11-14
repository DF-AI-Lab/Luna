# Luna (morning briefing agent)

## Where we are
- Current step: Build & Test (Darren said "build all of it"; Step 1 grill skipped for now, parked)
- Last session (8 Nov 2026): built V1 end to end: live page, run instructions, helper memory, 7:40am schedule. Merged to `main`.
- Next action: Darren checks the first real 7:40am run (Mon 9 Nov), then recap and tweak

## Principles / constraints
- Easy to read: cards, not a wall of text (Darren has ADHD)
- Reply to ONE card, not an awkward chat
- Runs on Darren's Claude plan usage, not the API. Keep helpers small.
- Never delete or make big changes without asking
- Learning matters: replies are saved to train Orbit

## 1. Idea
- Who: Darren only
- Problem: the current 8am briefing comes as an email/chat message that's hard to read and awkward to reply to
- Destination: a card page each morning. One card per item. Buttons + reply box on each. Luna acts on replies.
- Success looks like: Darren glances, taps or replies on a card, and things get added or sorted without a long chat
- Assumptions: an Artifact page can save replies (shared database) and Luna can read them next run
- Missing info: does Darren want a phone ping when the page is ready? Keep the email as well, or stop it?
- In scope: TaskNotes, Google Calendar, Gmail. Merge, skip known stuff, add new things, card page, save replies.
- Out of scope (for now): Todoist (dropped), tidy-up agent, cleaning up the earlier Orbit agents attempt

- Extra from brain dump 2: the schedule itself knows nothing, it just points Opus at the `.md`. Each helper could keep its own memory of what it last reported. Reply per card ("yep, do that") so everything gets done in one go.

## Card page design (agreed in mock)
- Mock: `mock/cards-mock.html`. Pickers: `mock/picker.html`, `mock/headers.html`
- Deep-space sky, moving stars, odd shooting star
- Sky changes by itself with the time of day (night / morning / afternoon / evening)
- Header: glass banner (option 4). LUNA in thin, wide-spaced caps (Josefin Sans 200). Realistic moon on the right showing the real phase
- Cards: glass, grouped Do today / Coming up / FYI. Each card has a "Luna will…" line so Done = yes, go ahead
- Done / Tomorrow / Drop + reply box on each card. Done = card bursts into stardust, with Undo
- Must fit a Z Fold 8 cover screen (narrow)

## 2. Steps (rough, not grilled)
1. Scheduled task wakes Opus in this repo at 8am (Europe/London)
2. Opus reads `BRIEFING.md`
3. Opus sends 3 small helpers out, each with its own rules file in `helpers/`
4. Helpers report back what they found
5. Opus merges: already in `known-facts.md` → skip; new → tells a helper to add it (TaskNotes task / Calendar event)
6. Opus builds the card page: 🔴 Do today / 🟡 Coming up / 🟢 FYI
7. Darren taps / replies on cards
8. Next run (or when asked): Opus reads replies, acts, updates `known-facts.md`, writes each reply to `log/`

## 3. Choose & Prove (not started)
- Open: helpers as subagents vs Opus doing all of it (usage cost vs tidiness)
- Open: card page = Artifact with the shared database (`db`) for replies

## 4. Fine Detail (not started)

## Decisions
| # | Decision | Why | Date |
|---|----------|-----|------|
| 1 | Own repo, named `luna` | Separate from Orbit, linked only by the log | 8 Nov 2026 |
| 2 | Start with TaskNotes, Calendar, Gmail (Todoist dropped) | TaskNotes is Darren's own app and already connected; no throwaway Todoist helper | 8 Nov 2026 |
| 3 | Card replies saved to `log/` as message → app | Free real training data for Orbit | 8 Nov 2026 |
| 4 | Mock the card page before grilling | See it first, then test with real data | 8 Nov 2026 |
| 5 | Card page look: see "Card page design" | Picked by Darren from mocks | 8 Nov 2026 |
| 6 | Opus runs it; Haiku for TaskNotes + Calendar helpers, Sonnet for Gmail and for doing actions | Save usage where data is neat, judgement where it is messy | 8 Nov 2026 |
| 7 | Runs as a Claude Code scheduled task on the Pro plan, no API | Darren wants it on his own usage | 8 Nov 2026 |
| 8 | Each run logs rough token use to `log/usage.md` | Check it fits Pro after a week of testing | 8 Nov 2026 |
| 9 | All .md files live in the GitHub repo; each helper gets a `-memory.md` of its last report | Phone-only, nothing on the PC; helpers say "nothing new" instead of repeating | 8 Nov 2026 |
| 10 | Page is opened from a phone home-screen shortcut to one fixed artifact link | Same link every day | 8 Nov 2026 |
| 11 | Live page `app/luna.html` reads cards from its own database (`briefing/today`) and saves replies to `replies/<date>`; only Darren can write | Same link daily, no Claude usage when Darren taps | 8 Nov 2026 |
| 12 | Schedule: daily 7:40am Europe/London, fresh cloud session, push ping when done | Page ready before 8am | 8 Nov 2026 |
| 13 | Done and typed/spoken replies happen straight away from the page (Sonnet-tier helper using Darren's connectors, on his Pro usage). Tomorrow/Drop wait for the morning run. Emails are drafts only, nothing deleted (the page has no delete or send tools) | Darren wants it done when he taps it, with a message saying what was done | 8 Nov 2026 |
| 14 | Voice button on each card (browser speech-to-text). Falls back to the phone keyboard mic if blocked | Faster replies | 8 Nov 2026 |
| 15 | Buttons: OK (seen) · Done · Remind (tomorrow / 3 days / next week / date) · Drop (deletes nothing). All fold with Undo | Clearer than Tomorrow/Drop | 8 Nov 2026 |
| 17 | Names: **Luna Agent** (violet, online) and **Luna Assistant** (light blue). Header v1.01, icons in `brand/` | Easy to tell apart at a glance | 9 Nov 2026 |
| 16 | Luna + Orbit stay two apps, one look: Smart Luna (online, claude.ai, Pro usage, schedule) + Thick Luna (Orbit reskinned as Luna, offline, free tiny model, learns from Luna's logs). Claude API only as a backup in Thick Luna, with a monthly spend cap | Pro usage only works in claude.ai; offline needs its own app; API costs money so keep it on a leash | 8 Nov 2026 |

## Link to Orbit (app-assistant repo)
- Luna = the shop. Orbit = the school. `log/` = the receipts.
- Orbit's tiny router learns which app a message belongs to. Darren's real card replies are perfect examples.
- Format: see `log/README.md`. Orbit side: `luna-link.md` in DF-AI-Lab/app-assistant.

## Parked (this version, not now)

## Research

## Prototypes / tests
- Card page mock with example data: done, look agreed (`mock/cards-mock.html`)
- Done 8 Nov: first real-data page (mock/cards-real-test.html), 12 cards from TaskNotes, Calendar, Gmail, read only

## Risks
- Usage: 3 helpers + Opus every day could eat plan usage. Measure on the first runs.

## Later / V2
- Full transcript report (training data for Orbit). For every chat message and card reply, save one line:
  - **Said**: Darren's exact words (typos kept)
  - **Did**: what Luna actually did (tools used, what changed, where)
  - **Result**: the outcome / Luna's reply
  - **Right?**: yes / no, plus Darren's correction if wrong
  - Builds on `log/*.jsonl` (cards) and the page's `chat/<date>` docs. Needs one shared format + a "was it right?" tap

## PRD

## Tickets

## Build / test progress
- 8 Nov: V1 built. Live page https://claude.ai/artifact/K9WPKsdLQLMoMyb6iCPm5C seeded with today's real cards (test run). Reply saving tested in a browser with a fake store; access rule checked (only Darren writes).
- Scheduled task "Luna morning briefing" created (7:40am daily, push on). It was created with NO connectors: Darren must add TaskNotes, Google Calendar and Gmail to it in claude.ai before it can read anything.
- First real scheduled run: Mon 9 Nov, 7:40am. Check: did it run, did the page update, did the ping arrive, token use in `log/usage.md`.

## Change log
- 14 Nov 2026: Luna page v25. Chat pictures are redrawn as a clean, smaller JPEG before sending; picture errors now say what went wrong and are saved in the chat log. Old cards show an amber "these cards are old · Run now" bar. Found why the board was stale: the 7:40 task fires into an old chat that waits for Darren's "go" and never runs
- 14 Nov 2026: Cleared Later / V2 (Thick Luna, Orbit tidy-up, learn requests, Orbit clean-up, thinking animation). Only the full transcript report stays
- 8 Nov 2026: Project file created; idea moved here from app-assistant
- 8 Nov 2026: Brain dump 2 added; card page mocked and design agreed
- 8 Nov 2026: Locked model split, Pro-plan schedule, token log, repo layout with helper memory files (mock/structure.html)
- 8 Nov 2026: Dropped Todoist; TaskNotes is the to-do app from now (helpers/tasknotes.md). Orbit tidy-up idea added to Later/V2
- 8 Nov 2026: First real-data test page built (read only)
- 8 Nov 2026: V1 built and merged to main: live page, BRIEFING.md run, helper memory, usage log, 7:40am schedule
- 8 Nov 2026: Buttons renamed to Done / Tomorrow / Drop. Done now also marks calendar events ✅ (never deleted). Moon redrawn
- 8 Nov 2026: Instant actions from the page + 'What Luna did' box + voice button
- 2026-11-08: Buttons now OK · Done · Remind (Tomorrow / 3 days / Next week / date) · Drop. All fold with Undo. Drop deletes nothing.
- 2026-11-08: Decided Luna + Orbit = Smart Luna (online) + Thick Luna (offline, Orbit reskinned), API backup only with a cap. Parked till after first runs
- 2026-11-09: Settings ⋮ menu + Run now (quick run from the page: read-only look-ups, skips facts/, keeps pins, writes briefing/today with quickRun:true). The 7:40 full run still overwrites it each morning.
- 2026-11-11: Luna page v17: chat dock (type, + photo/camera/file, talk mode tap-to-talk/tap-to-send, segment progress). Chat logs to db chat/<date>.
- 2026-11-11: Luna page v21: dock replaced by progress chip (bottom-left) + Ask Luna button (bottom-right). Opens straight on the talk orb; typing switches to chat. No Type/Talk tabs.
