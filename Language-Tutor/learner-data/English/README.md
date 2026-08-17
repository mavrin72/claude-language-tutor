# English — Learner Data

This folder is the persistent state for one learner's English practice, read and written by the `langtutor-*` skills.

| File | Created by | Status |
|---|---|---|
| `profile.json` | langtutor-assessor (first real assessment) | not created yet |
| `plan.json` | langtutor-assessor | not created yet |
| `sessions.json` | langtutor-session (appends each session) | initialized empty `[]` |
| `vocab.json` | langtutor-vocab / langtutor-session | initialized empty `[]` |
| `progress.json` | langtutor-tracker | not created yet |
| `materials/` | langtutor-immersion | empty |
| `dictionaries/` | langtutor-vocab | empty |

**First step**: run an assessment ("Оціни мій рівень англійської") to create `profile.json` and `plan.json`. Everything else builds on that.

Do not hand-edit these files unless you know what you're doing — the skills expect the exact schemas documented in each skill's `SKILL.md` / `references/*.md`.
