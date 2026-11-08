# Log: card replies (training data for Orbit)

One file per day: `YYYY-MM-DD.jsonl`. One line per reply:

```json
{"date": "2026-11-08", "message": "add dentist, I'll confirm a time later", "app": "calendar", "action": "add_event"}
{"date": "2026-11-08", "message": "remind me tomorrow to chase email", "app": "tasknotes", "action": "add_task"}
```

- `message` = Darren's own words, exactly as typed (typos too, they help training)
- `app` = where it really went: `calendar`, `tasknotes`, `gmail`, `wmm`, `fridge`, or `none`
- `action` = what Luna did
- Button taps (Done / Tomorrow / Drop) are logged too, with `message` set to the button name

Each line can also carry `"card"` (the card id) and `"title"` so Orbit can see what the reply was about.

`usage.md` holds rough token use per run.
