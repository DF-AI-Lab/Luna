# Luna brand

Two apps, one family. Colour tells them apart.

| | Luna Agent (online) | Luna Assistant |
|---|---|---|
| Colour | Violet `#a99bff` | Light blue `#8fd3ff` |
| Header moon | 3/4 full, shadow on the right | Crescent lit on the left |
| Header glow | Faint purple | Faint blue |
| Icon | `luna-agent-icon.png` | `luna-assistant-icon.png` |

- Header: `LUNA` wordmark + small coloured tag (AGENT / ASSISTANT) + version pill.
- Version format: `v1.01` (bump the last part for small changes, the first for big ones).
- Date line: date · current time · cards. No moon-phase label.
- Same moon surface on both (same seed, spread-out seas), only the shadow differs.
- Icons: "Ring behind" orbit style, LUNA on top, AGENT / ASSIST underneath, 512×512, still images.
- `headers-and-icons-mock.html` holds the approved Assistant header (copy its `header.asst` block and CSS when building the Assistant app).
- Settings: faint ⋮ in the header's top-right corner (option 1). Same on the Assistant header.
