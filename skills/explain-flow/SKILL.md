---
name: explain-flow
description: Explains how data moves through code as one arrow chain of real hops, from trigger to the field that changed. Use when asked how data gets from A to B, what happens after an upload, event, request, or schedule, or to trace a pipeline, queue, sync, or multi-service code path. Not for explaining a single function, an algorithm, or why a design was chosen.
---

# Explain flow

If it can be explained this way, it's worth having.

Write the path as one text chain. Arrows are `→`. Each hop is a real name from the code: bucket, producer, queue, consumer, table, API, object, field. Line breaks continue the same chain.

```text
reports bucket → ingest worker → job queue → consumer writes payments_table →
sync service PUT /api/accounts/{accountId}/billing (queued) →
CRM API PATCH /records/{externalId} →
total_paid (and remaining_balance / next_due_date)
```

## Write the chain

1. Start at the trigger: file, event, request, or schedule.
2. Follow the path in code to the sink. Keep a hop only if it moves the data or writes something.
3. Name what you found: service, queue, table, method + path, object, field. Do not invent hops.
4. Parentheses hold the payload, the fields written, or a one-word behavior such as `(queued)`.
5. End on the record or field that changed.

## Branches

A second path is a second chain, labeled in a few words. Do not fold two paths into one line.

```text
Valid row: consumer writes payments_table → …
Invalid row: consumer → dead-letter queue (raw row) → failed_imports table
```

## After the chain

Lead with the chain. Then add only the names, files, or conditions needed to trust it.

## Skip the diagram

Skip it when a single chain would hide a fork that changes the outcome. Name the fork, then give a chain only for the path that was asked about.
