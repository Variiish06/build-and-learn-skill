# Trade Execution Engine Resources

> Status: compiled 2026-10-19. Entries marked ✓ were fetched and checked on 2026-10-19; check the others before citing them in a lesson.

## Knowledge

### Core book
- [Book: _Designing Data-Intensive Applications_ by Martin Kleppmann (O'Reilly)](https://dataintensive.net/)
  The user is reading it alongside. Use for: Ch. 7 Transactions (dirty reads/writes, lost updates, write skew, isolation levels, `FOR UPDATE`), Ch. 8 (process pauses, leases, fencing tokens), Ch. 11 (exactly-once, idempotence).

### Docker & Compose (topic 1)
- ✓ [Docker Docs: Docker concepts, "The basics" and "Running containers"](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-container/)
  Official intro to images, containers, publishing ports and persisting data. Use for: lesson 1 fundamentals.
- [Docker Docs: Compose](https://docs.docker.com/compose/)
  Official Compose reference. Use for: `compose.yaml`, services, networks, named volumes, healthchecks, `depends_on`.
- ✓ [Docker Docs: Compose startup order](https://docs.docker.com/compose/how-tos/startup-order/)
  Healthcheck + `depends_on: condition: service_healthy`, with a postgres:18 example. Use for: API/workers waiting on the db.
- ✓ [Docker Docs: Packet filtering and firewalls](https://docs.docker.com/engine/network/packet-filtering-firewalls/)
  States Docker and ufw are incompatible (published ports bypass ufw). Use for: why ports bind to 127.0.0.1.
- ✓ [Docker Hub: Official `postgres` image](https://hub.docker.com/_/postgres)
  Env vars (`POSTGRES_PASSWORD`, etc.), data directory (pg18+ mounts at `/var/lib/postgresql`, ≤17 at `/var/lib/postgresql/data`), init scripts. Use for: running Postgres in Compose.

### Postgres (topics 2, 4, 5)
- [PostgreSQL Docs: Tutorial](https://www.postgresql.org/docs/current/tutorial.html)
  Official SQL basics: tables, CRUD, transactions. Use for: topic 2.
- [PostgreSQL Docs: Transaction Isolation](https://www.postgresql.org/docs/current/transaction-iso.html)
  Authoritative description of Read Committed vs Repeatable Read vs Serializable. Use for: lost-update experiment and the DDIA Ch. 7 link.
- [PostgreSQL Docs: Explicit Locking](https://www.postgresql.org/docs/current/explicit-locking.html)
  Row-level locks. Use for: `SELECT ... FOR UPDATE`.
- [PostgreSQL Docs: SELECT, "The Locking Clause"](https://www.postgresql.org/docs/current/sql-select.html#SQL-FOR-UPDATE-SHARE)
  Official semantics of `FOR UPDATE`, `NOWAIT`, `SKIP LOCKED`. Use for: topic 5 job queue.
- [PostgreSQL Docs: Constraints](https://www.postgresql.org/docs/current/ddl-constraints.html)
  `UNIQUE`, `CHECK`, `NOT NULL`, foreign keys. Use for: topic 2 and idempotency keys (unique constraint).

### Python / FastAPI / psycopg (topic 3)
- [FastAPI Docs: Tutorial - User Guide](https://fastapi.tiangolo.com/tutorial/)
  Official tutorial. Use for: path/query params, request bodies with Pydantic.
- [psycopg 3 Docs](https://www.psycopg.org/psycopg3/docs/)
  Official docs. Use for: connections, transactions (`conn.transaction()`), parameter passing (never f-string SQL), connection pools (`psycopg_pool`).

### Reliability patterns (topics 6-8)
- [Article: "Exponential Backoff And Jitter" (AWS Architecture Blog, Marc Brooker)](https://aws.amazon.com/blogs/architecture/exponential-backoff-and-jitter/)
  Classic analysis of backoff strategies. Use for: topic 7 retries.
- [Article: "Designing robust and predictable APIs with idempotency" (Stripe blog, Brandur Leach)](https://stripe.com/blog/idempotency)
  How a payments company uses idempotency keys. Use for: topic 8.
- [Article: "Implementing Stripe-like Idempotency Keys in Postgres" (Brandur Leach)](https://brandur.org/idempotency-keys)
  Deep, Postgres-specific design with recovery points. Use for: topic 8 and the crash-between-broker-and-DB question.

### Broker
- [Alpaca Docs: Paper Trading](https://docs.alpaca.markets/docs/paper-trading)
  Paper environment and API keys. Use for: executing orders.
- [Alpaca Docs: Orders (`client_order_id`)](https://docs.alpaca.markets/docs/orders-at-alpaca)
  Client-supplied order IDs, which act as the broker-side idempotency key. Use for: topic 8 exactly-once at the broker boundary.

### Observability (topic 9)
- [Python Docs: `logging` HOWTO](https://docs.python.org/3/howto/logging.html)
  Official logging basics. Use for: structured (JSON) logs.

## Wisdom (Communities)
- [r/PostgreSQL](https://www.reddit.com/r/PostgreSQL/)
  Use for: queue/locking design critique.
- [PostgreSQL mailing lists (pgsql-general)](https://www.postgresql.org/list/)
  High-expertise, slower. Use for: precise semantics questions.
- [FastAPI GitHub Discussions](https://github.com/fastapi/fastapi/discussions)
  Use for: FastAPI/psycopg integration questions.
- [r/ExperiencedDevs](https://www.reddit.com/r/ExperiencedDevs/) and [r/cscareerquestions](https://www.reddit.com/r/cscareerquestions/)
  Use for: feedback on the README and how to present the project in interviews.

## Gaps
- A good, trustworthy write-up on **lease-based job recovery in Postgres** (visibility timeout pattern). DDIA Ch. 8 covers leases conceptually; find a concrete implementation reference.
- A concise, trustworthy guide to **structured logging + simple metrics in FastAPI** without heavy infra (no Prometheus/Grafana stack on an 8GB laptop unless it's cheap).
