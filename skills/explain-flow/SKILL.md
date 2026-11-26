---
name: explain-flow
description: Use when explaining complex data flows, pipelines, or multi-step code paths.
---

# Explain flow

If it can be explained this way, it's worth having.

Write the path as one text chain. Arrows are `→`. Each hop is a real name from the code: bucket, producer, queue, consumer, table, API, object, field. Line breaks continue the same chain.

```
reports bucket → ingest worker → job queue → consumer writes payments_table →
sync service PUT /api/accounts/{accountId}/billing (queued) →
CRM API PATCH /records/{externalId} →
total_paid (and remaining_balance / next_due_date)
```

## Write the chain

1. Start at the trigger (file, event, request, schedule).
2. Follow the path in code until the sink. Keep a hop only if it moves the data or writes something.
3. Name what you found: service, queue, table, method + path, object, field. Do not invent hops.
4. Parentheses are the payload, the fields written, or a one-word behavior such as `(queued)`.
5. End on the record or field that changed.

A second path is a second chain, with a few words naming the branch. Do not fold two paths into one line.

Lead with the chain, then add only the names, files, or conditions needed to trust it.

## Skip the diagram

Skip it when a single chain would hide a fork that changes the outcome. Name the fork, then give a chain only for the path that was asked about.
