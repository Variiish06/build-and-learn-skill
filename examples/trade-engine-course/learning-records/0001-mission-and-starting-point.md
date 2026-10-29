# Mission set: exactly-once trade execution engine in 12 days

The user is building an Agent-Driven Trade Execution Engine (Postgres queue, Python workers, Alpaca paper trading, exactly-once under worker crashes) as their main resume project, with a hard deadline of 2026-10-30. See [[MISSION.md]].

**Evidence**: Mission brief written by the user on 2026-10-19. The 9-topic order (Docker → Postgres → FastAPI → concurrency → SKIP LOCKED → leases → retries → idempotency → observability) is the user's own choice.

**Implications**:
- Prior knowledge level not yet demonstrated for any topic. Lesson 1 starts at Docker basics; probe with quick retrieval questions and skip ahead if the user already knows something.
- They are reading DDIA Ch. 7 now, so its vocabulary (lost update, read committed, explicit locking) can be used as an anchor.
- They write Python (studying DSA) but there's no evidence yet of SQL, Docker or FastAPI experience.
