# build-and-learn

A Claude skill that teaches a technical topic by having you **build a real project step by step in chat**: short concept → predict → you write it → break it on purpose → explain it back → spaced recall across sessions.

The goal is **storage strength**: you can explain every decision later, without notes, in an interview.

## What's in here

```
build-and-learn/                 ← the skill itself (copy or zip this folder)
  SKILL.md                       ← teaching method and rules
  NOTES-FORMAT.md                ← format of the teacher's NOTES.md
examples/trade-engine-course/    ← a real course run with this skill (personal details redacted)
  MISSION.md                     ← why / success criteria / topic order / constraints
  NOTES.md                       ← the teacher's working notes: struggles, predictions, RESUME AT lines
  RESOURCES.md                   ← reading list mapped to topics
  why-build-first-mode.md        ← why the course switched from lesson pages to build-first chat
  learning-records/              ← early decisions (mission, "complete beginner" reset)
  reference/study-notes.html     ← study page kept up to date as topics finish
  reference/docker-compose.html  ← an old-style lesson page (the format that was dropped)
```

The example is a course on building an **exactly-once trade execution engine** (Docker → Postgres → transactions → lost updates → `SKIP LOCKED` job queue → crash demo → leases …). Read `examples/trade-engine-course/NOTES.md` to see what the skill's notes look like after about 10 sessions.

## Install

**Claude Code (any machine):** copy the skill folder into your skills directory, then restart.

```bash
# Linux / macOS
cp -r build-and-learn ~/.claude/skills/
```
```powershell
# Windows
Copy-Item -Recurse build-and-learn $env:USERPROFILE\.claude\skills\
```

**claude.ai / desktop app (syncs to all your devices):** zip the folder and upload it under **Settings → Capabilities → Skills**.

```bash
zip -r build-and-learn.zip build-and-learn
```

## Use

- Start: "teach me X by building Y", or `/build-and-learn`.
- Continue: say **"resume"** in the teaching folder. The skill reads `NOTES.md` first.
- Pause: say "pausing" / "brb". The skill writes a `RESUME AT` line.

Progress lives in the teaching folder's `NOTES.md` and in the project folder, not in the skill. To continue a course on another machine, you need those folders too.
