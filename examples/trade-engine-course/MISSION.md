# Mission: Agent-Driven Trade Execution Engine

## Why
Build an Agent-Driven Trade Execution Engine as my main backend/system-design resume project: a signal generator puts orders into a Postgres queue, and a pool of Python workers claims and executes them against Alpaca's paper trading API with exactly-once guarantees, even when workers crash. It runs on my home server, and I will deliberately kill workers to prove no order runs twice.

## Success looks like
- A working engine on GitHub with a clear README, architecture diagram and demo video
- I can explain every design decision without notes
- I can answer interview questions such as: "What is a lost update?", "How does SKIP LOCKED work?", "What happens if a worker crashes after calling the broker but before updating the database?", "How do idempotency keys work?", "At-least-once vs exactly-once?"
- I can whiteboard the architecture in a system-design interview

## Learning path (in order)
1. Docker and Docker Compose: images, containers, ports, volumes
2. Postgres: tables, CRUD, transactions (BEGIN/COMMIT/ROLLBACK), constraints
3. FastAPI: endpoints, path/query params, Pydantic request bodies, psycopg 3 with raw SQL
4. Concurrency problems: race conditions, lost updates, atomic updates, `SELECT ... FOR UPDATE`
5. Job queues in Postgres: `FOR UPDATE SKIP LOCKED` with multiple workers
6. Lease-based crash recovery: what happens when a worker dies mid-job
7. Retries with exponential backoff and dead-letter tables
8. Idempotency keys: guaranteeing an order executes exactly once
9. Basic observability: structured logs and simple metrics

## Constraints
- Deadline: 12 days, 2026-10-19 to 2026-10-30, at 3-4 hours/day (DSA takes the rest)
  - Days 1-2 (Oct 19-20): Docker, Postgres, FastAPI basics, lost-update experiment
  - Days 3-8 (Oct 21-26): engine core (queue, SKIP LOCKED, leases, retries, idempotency, Alpaca)
  - Days 9-10 (Oct 27-28): deploy on home server, run failure tests
  - Days 11-12 (Oct 29-30): README, architecture diagram, demo video
- Server: old HP laptop, 8GB RAM, WiFi only, Ubuntu Server, accessed via SSH/Tailscale and VS Code Remote-SSH
- Stack: Python + FastAPI + Postgres + Docker Compose; raw SQL with psycopg 3, no ORM
- Reading *Designing Data-Intensive Applications* (Kleppmann) alongside, especially Chapter 7 (Transactions)

## Out of scope
- ORMs (SQLAlchemy etc.)
- Redis, unless genuinely needed later
- Kubernetes, cloud deployment, real-money trading
- Trading strategy design / quant theory: the signal generator only needs to emit orders
