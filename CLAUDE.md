# Language Tutor — Session Context for Claude Code

This repository is a personal, git-tracked English-learning system built on the `langtutor-*` skills (assessor, session, vocab, tracker, immersion — see `Language-Tutor-Instructions.md` for what each does and how to trigger it). The learner's native language is Ukrainian; target language is English.

## On every session start in this repo

1. Check whether `Language-Tutor/learner-data/English/profile.json` exists.
   - **If it does NOT exist**: no assessment yet. Suggest running the assessor skill first ("Оціни мій рівень англійської") before anything else, and stop there until the learner responds.
   - **If it exists**: read it plus `progress.json` (if present) and the last 3 entries of `sessions.json` and `vocab.json`. Give a short status in Ukrainian *before* asking what the learner wants to do:
     - current CEFR level
     - current streak (consecutive calendar days with a `sessions.json` entry, ending today or yesterday)
     - how many `vocab.json` words have `next_review <= today`
     - one concrete next-action recommendation

2. Route the learner's request to the right skill based on the trigger phrases in `Language-Tutor-Instructions.md` (assessor / session / vocab / tracker / immersion). If the learner just says something like "давай позаймаємось" with no more detail, default to: due vocab review first (langtutor-vocab), then a langtutor-session of a type not used in the last 2 sessions (check `sessions.json`), sized to fit ~30-45 minutes total.

## End-of-session protocol — do this every time, unprompted

1. Make sure every data file touched this session is actually written: `sessions.json`, `vocab.json`, `profile.json`, `progress.json`, anything under `materials/` or `dictionaries/`.
2. Regenerate root `PROGRESS.md` from the current contents of `Language-Tutor/learner-data/English/*.json` (level, streak, words due, last session, next recommended action — see the file's own structure).
3. `git add` the changed learner-data files and `PROGRESS.md`, then commit with this convention:

   `YYYY-MM-DD: <session-type> — <one-line summary>`

   Examples:
   - `2026-08-17: vocab review — 12 words reviewed, 92% accuracy, 3 new words added`
   - `2026-08-18: conversation session — restaurant ordering, A2, 15 min`
   - `2026-08-20: assessment — initial placement, A2 overall`

   One commit per practice session (not batched across days). The commit history is the practice journal and streak record on purpose — `git log --oneline` should read as a diary.
4. Push to the current branch (`git push`) so progress survives container resets.
5. Tell the learner in one sentence what got committed.

Never skip this because the session felt short — even a 5-minute vocab review gets its own commit.

## Daily reminder

A Routine fires into this conversation daily at 19:00 Europe/Kyiv asking to check in on practice. When that reminder arrives: read `sessions.json`, check whether today already has an entry, and if not, send one short (1-2 sentence), low-pressure nudge to start today's session — no lectures. If `profile.json` doesn't exist yet, the nudge should point at running the assessment instead.

## Hard rules

- Never fabricate `profile.json` / `plan.json` / `progress.json` content. These only get written by actually running the assessor/tracker skills with the learner's real answers — not guessed or templated.
- If usage credits run out mid-session, follow that skill's own "Credit Limit Handling" / "Usage Credits" section: save partial progress, tell the learner plainly, don't guess the rest.
