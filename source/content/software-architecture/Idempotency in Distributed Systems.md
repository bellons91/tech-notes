---
title: "Idempotency in Distributed Systems"
tags:
  - distributed-systems
  - software-architecture
  - reliability
  - idempotency
  - retries
aliases:
  - Idempotent Operations
  - Idempotency Keys
---

Idempotency makes repeated attempts for one logical operation safe, even when a client cannot tell whether an earlier attempt completed. It is especially important for distributed writes and external side effects, where timeouts and retries can otherwise cause duplicate effects.

## Summary

- A timeout is an unknown outcome, not proof that an operation failed: the effect may have committed even if its acknowledgment was lost.
- An idempotency key binds multiple physical requests to one logical operation; clients must reuse the same key across retries.
- The reservation that grants one request the right to execute must be atomic, and the result must be stored durably so duplicates can replay it.
- Scope keys to the tenant or merchant and operation, and bind them to a hash of invariant payload fields.
- Retain deduplication records for the longest realistic retry or replay window, including delayed queue and operator replays.
- Natural idempotency works for deterministic conditional writes, but irreversible external effects need explicit deduplication and often reconciliation.
- Broker-level exactly-once guarantees do not automatically extend to external services.

## Handling Uncertain Outcomes

A request can reach a service, commit a write, and lose its response before it reaches the caller. The caller sees a timeout, but cannot infer whether the write happened. Retrying without a stable identity can therefore repeat a charge, order, or other side effect.

Treat the timeout as an uncertain state. The retry should identify the same logical operation, and the system should either return its recorded outcome or resolve the pending operation before another side effect is issued.

## Idempotency Keys and Reservations

An idempotency key identifies intent rather than a particular network attempt. A client creates it for a logical operation and reuses it across retries, reconnects, and other repeated submissions. The server should scope it to an appropriate boundary, such as a tenant or merchant and endpoint, and bind it to a hash of invariant payload fields. Reusing the same key with a different payload is a correctness error.

Checking whether a key exists and claiming the right to execute must be one atomic operation. Otherwise, concurrent retries can both pass the check and perform the side effect. A database uniqueness constraint can arbitrate the reservation: one insert wins, and a duplicate request reads the existing record.

The record needs at least two meaningful states:

- **Pending**: the reservation succeeded, but the operation has not reached a stable outcome.
- **Completed**: the outcome and response are durable and can be replayed to later requests with the same key.

For in-flight duplicates, the service can wait, poll, or return a retryable status rather than racing into another execution. Retention must cover the maximum realistic retry and replay window; if a record expires too early, a delayed retry can look like a new operation.

An atomic cache command such as Redis `SET NX PX` can reserve a key and set its expiry together. A cache may lose entries through eviction or failover, however, so the reservation alone is not proof that an operation completed. Keep the authoritative outcome in durable storage.

## Natural Idempotency and External Effects

Some operations are naturally idempotent when expressed as deterministic writes against a stable business identifier. For example, setting a preference by user ID and version can converge to the same state when repeated.

Irreversible effects such as charging a card, sending an email, or invoking an external command are different. They are safe to repeat only if the downstream system also honors a stable identity. Queue redelivery or a broker's exactly-once processing semantics do not make an external HTTP call idempotent; the guarantee stops at the broker boundary.

## End-to-End Recovery

For operations whose effects cross a system boundary, idempotency is a contract among the client, service, storage, and downstream provider. A robust pattern combines:

1. A client-supplied key reused for every retry of the same intent.
2. An atomic reservation with pending and completed states.
3. An append-only business ledger recording intent and committed effects.
4. A reconciliation process that checks uncertain external outcomes and finalizes pending records.

For example, if a service crashes after submitting a payment but before recording completion, a reconciliation worker can query the processor and record the actual outcome. Future retries can then replay that outcome rather than issuing the charge again. Tracking the age of pending records helps identify operations that remain unresolved.

Useful measurements include duplicate execution rate, reservation-write success, replay correctness, reconciliation time, and pending-record age. A single success metric can hide valid retries that were rejected or incorrect responses that were replayed.

## Related

- [[Event-Driven Architecture]] — message consumers may receive redelivered work.
- [[Event Sourcing]] — immutable histories and replay are related to recording and recovering business effects.

## Sources

- [How Idempotency Actually Works in Distributed Systems](https://medium.com/@systemdesignwithsage/how-idempotency-actually-works-in-distributed-systems-053241a4db59)
