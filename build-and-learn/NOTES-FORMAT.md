# NOTES.md format

`NOTES.md` is the teacher's working memory across sessions. Keep entries short and dated. Append to it; don't rewrite history.

```markdown
# Teaching Notes

## Learner
- Level: (e.g. "complete beginner in Docker/SQL; writes Python")
- Learns best: (from what has actually worked)
- Dislikes: (e.g. "long lesson pages")

## Environment
- Machine(s), OS, shell, where the project lives, what else runs there
- Things never to touch (other projects' containers, volumes, ports)

## Conventions
- Project folder, service names, ports, credentials location (.env, never the value)

## Progress
- Topic 1 ✅ ... / Topic 2 ⏳ Step 3 ...

## Struggles to revisit
- YYYY-MM-DD: <misconception> → correct idea. Status: open | re-asked YYYY-MM-DD ✓ resolved

## Session log
- YYYY-MM-DD: what was done, predictions right or wrong, slips
- YYYY-MM-DD (paused): RESUME AT: <exact next action, pending prediction, warm-up questions to ask>
```

Rules:
- The last session-log line always says exactly how to resume.
- Record predictions that were wrong. They show what the learner's mental model was.
- Never write secrets in NOTES.md.
