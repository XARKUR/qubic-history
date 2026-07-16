# Events

`events` stores manually curated Qubic ecosystem events that are not directly discoverable from on-chain data or deterministic protocol rules.

These events are intended to provide context for epoch-aligned charts. They must not be presented as direct causes of price movement.

## Files

- `events.json`: the real source file consumed by backend import jobs.
- `events.example.json`: a non-production example showing the full shape.
- `schema.json`: JSON Schema for basic validation.

## Event Rules

1. Every non-draft event must include at least one public source.
2. Prefer official or primary sources. If the original source is volatile, add an archived URL.
3. `date` is the event date in UTC calendar date format.
4. `epoch` is optional. Backend import should compute it from `date` and validate it when provided.
5. `importance` controls chart visibility. `major` and `normal` can be shown on the price chart; `minor` may be detail-only.
6. Do not write causal language such as "price rose because of this event".
7. Keep titles factual and short. Put context in `summary`.

## Categories

Current categories:

- `ecosystem`
- `release`
- `exchange`
- `incident`
- `network`
- `mining`
- `qearn`
- `governance`
- `community`
- `other`

## Recommended Backend Flow

```text
events/events.json
-> validate schema
-> compute/validate epoch
-> upsert custom_events by id
-> /events/price aggregates as type = custom
```
