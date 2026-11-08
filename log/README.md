# Log: card replies (training data for Orbit)

One file per day: `YYYY-MM-DD.jsonl`. One line per reply:

```json
{"date": "2026-11-08", "message": "add dentist, I'll confirm a time later", "app": "calendar", "action": "add_event"}
{"date": "2026-11-08", "message": "remind me tomorrow to chase email", "app": "todo", "action": "add_task"}
```

- `message` = Darren's own words, exactly as typed (typos too, they help training)
- `app` = where it really went: `calendar`, `todo`, `wmm`, `fridge`, or `none`
- `action` = what Luna did
- Button taps (Done / Later / Skip) are logged too, with `message` set to the button name
