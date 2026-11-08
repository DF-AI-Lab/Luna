# Luna (morning briefing agent)

## Where we are
- Current step: 1. Idea (brain dump done, card page look mocked and agreed, not grilled yet)
- Last session (8 Nov 2026): second brain dump; card page mocked and styled (branch `card-page-mock`, `mock/`)
- Next action: first real-data test page (read only), then grill Step 1

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

- Extra from brain dump 2: the schedule itself knows nothing, it just points Opus at the `.md`. Each helper could keep its own memory of what it last reported. Reply per card ("yep, do that") so everything gets done in one go.

## Card page design (agreed in mock)
- Mock: `mock/cards-mock.html`. Pickers: `mock/picker.html`, `mock/headers.html`
- Deep-space sky, moving stars, odd shooting star
- Sky changes by itself with the time of day (night / morning / afternoon / evening)
- Header: glass banner (option 4). LUNA in thin, wide-spaced caps (Josefin Sans 200). Realistic moon on the right showing the real phase
- Cards: glass, grouped Do today / Coming up / FYI. Each card has a "Luna will…" line so Done = yes, go ahead
- Done / Later / Skip + reply box on each card. Done = card bursts into stardust, with Undo
- Must fit a Z Fold 8 cover screen (narrow)

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
| 4 | Mock the card page before grilling | See it first, then test with real data | 8 Nov 2026 |
| 5 | Card page look: see "Card page design" | Picked by Darren from mocks | 8 Nov 2026 |

## Link to Orbit (app-assistant repo)
- Luna = the shop. Orbit = the school. `log/` = the receipts.
- Orbit's tiny router learns which app a message belongs to. Darren's real card replies are perfect examples.
- Format: see `log/README.md`. Orbit side: `luna-link.md` in DF-AI-Lab/app-assistant.

## Parked (this version, not now)

## Research

## Prototypes / tests
- Card page mock with example data: done, look agreed (`mock/cards-mock.html`)
- Next: same page with today's real Todoist, Calendar, Gmail (read only, no changes)

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
- 8 Nov 2026: Brain dump 2 added; card page mocked and design agreed
