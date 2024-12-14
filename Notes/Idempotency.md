---
tags:
- automation
- web
---

# Idempotency

Webhook services must ensure idempotency to prevent duplicate event processing, especially during retries or errors. Key strategies include:

- Deduplication in message queues.
- Using event IDs as deduplication keys.

**Code Example for Idempotency Using In-Memory Store:**

```python
processed_events = set()

def process_event(event):
    event_id = event['id']
    if event_id in processed_events:
        return  # Duplicate event; skip processing
    # Process the event
    processed_events.add(event_id)
```

[[Workflow]]