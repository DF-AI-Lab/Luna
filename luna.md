# Luna (morning briefing agent)

## Where we are
- Current step: 1. Idea (brain dump done, not grilled yet)
- Last session (8 Nov 2026): repo made, idea moved here from app-assistant, starter rule files written
- Next action: grill Step 1, then build a first test card page with real data

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
- In scope: Todoist, Google Calendar, Gmail. Merge, skip known stuff, add new things, card page, save replies.
- Out of scope (for now): TaskNotes, tidy-up agent, cleaning up the earlier Orbit agents attempt

## 2. Steps (rough, not grilled)
1. Scheduled task wakes Opus in this repo at 8am (Europe/London)
2. Opus reads `BRIEFING.md`
3. Opus sends 3 small helpers out, each with its own rules file in `helpers/`
4. Helpers report back what they found
5. Opus merges: already in `known-facts.md` → skip; new → tells a helper to add it (Todoist task / Calendar event)
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
| 2 | Start with Todoist, Calendar, Gmail | What the current briefing already uses | 8 Nov 2026 |
| 3 | Card replies saved to `log/` as message → app | Free real training data for Orbit | 8 Nov 2026 |

## Link to Orbit (app-assistant repo)
- Luna = the shop. Orbit = the school. `log/` = the receipts.
- Orbit's tiny router learns which app a message belongs to. Darren's real card replies are perfect examples.
- Format: see `log/README.md`. Orbit side: `luna-link.md` in DF-AI-Lab/app-assistant.

## Parked (this version, not now)

## Research

## Prototypes / tests

## Risks
- Usage: 3 helpers + Opus every day could eat plan usage. Measure on the first runs.

## Later / V2
- TaskNotes helper + tidy-up agent (dates, duplicates, old tasks)
- Save Darren's requests so Luna learns how he likes things
- Clean up the earlier Orbit agents attempt

## PRD

## Tickets

## Build / test progress

## Change log
- 8 Nov 2026: Project file created; idea moved here from app-assistant
