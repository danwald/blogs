---
title: "5 Event-Driven Architecture Pitfalls to Avoid"
datePublished: Thu Dec 04 2025 03:43:49 GMT+0000 (Coordinated Universal Time)
cuid: cmiqw5rov000a02jx50py7fay
slug: 5-event-driven-architecture-pitfalls-to-avoid
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/wc3jFFQxo8k/upload/a50df64ccb0a486f9d8b3578bd281ae9.jpeg
tags: system-architecture, event-driven-architecture, pitfalls

---

I needed to understand the gotchas in event-driven architecture before migrating more services. Wix's engineering team [documented](https://medium.com/wix-engineering/event-driven-architecture-5-pitfalls-to-avoid-b3ebf885bdb1) 5 painful lessons learned from moving over 2300 microservices from request-reply to event-driven patterns.

## The Pitfalls

### **1\. Non-atomic database writes and event publishing**

Writing to a database and firing an event isn't atomic. If either the DB or message broker fails, you get data inconsistency.

Solutions:

* Resilient producer that retries until the event reaches Kafka
    
* CDC (Change Data Capture) with Debezium - captures DB changes via binlog and produces them as events automatically
    

### **2\. Using Event Sourcing everywhere**

Event sourcing stores events instead of entity state. You reconstruct current state by replaying events. Sounds cool but adds serious complexity:

* Need snapshots to avoid performance degradation
    
* Harder to create generic libraries (unlike CRUD ORMs)
    
* Only eventual consistency
    

Better approach: CRUD + CDC. Simple reads from the database, with CDC publishing changes for downstream materialized views. Get the benefits without the complexity.

### **3\. No context propagation**

Debugging distributed event flows is hard. Unlike HTTP chains, events scatter across topics and services.

```python
# Add request context to event headers
event_headers = {
    'requestId': request_id,
    'userId': user_id
}
```

Automatically propagate these IDs through your event chain. Makes filtering logs and events trivial during incident investigation.

### **4\. Large event payloads**

Events over 5MB kill broker performance. Three remedies:

* **Compression** - Kafka and Pulsar support lz4, snappy. Broker-level compression beats application-level
    
* **Chunking** - Split payloads into chunks with metadata for reassembly
    
* **Object store reference** - Store payload in S3, pass URL in event
    

### **5\. Duplicate event processing**

Most brokers guarantee at-least-once delivery. Events can be processed multiple times.

```python
# Use optimistic locking with revisionId
def process_event(event):
    revision_id = event['revisionId']
    # Read current version
    entity = db.get(event['entityId'])
    if entity.revision_id != revision_id:
        return  # Already processed
    
    # Update with new revision
    entity.update(revision_id=revision_id + 1)
```

For Kafka, use topic-partition-offset as unique transaction ID.

## The Migration Strategy

Migrate gradually. Mix HTTP/RPC with event-driven patterns as needed. CDC is the sweet spot - ensures consistency without full event-sourcing complexity.

Context propagation (pitfall #3) is critical for operations. Fix that early.

Compression and transaction IDs are good defaults even if you don't hit pitfalls #4 and #5 yet.

Happy hackin'!

## **References:**

* [Wix Engineering: Event Driven Architecture pitfalls](https://medium.com/wix-engineering/event-driven-architecture-5-pitfalls-to-avoid-b3ebf885bdb1)
    
* [Debezium: CDC Kafka connector](https://debezium.io/documentation/reference/stable/architecture.html)
    
* [DDD Aggregates via CDC-CQRS Pipeline using Kafka & Debezium](https://debezium.io/blog/2023/02/04/ddd-aggregates-via-cdc-cqrs-pipeline-using-kafka-and-debezium/)
    
* [Greyhound: Wix messaging platform](https://github.com/wix/greyhound#greyhound)
    
* [Kafka: Exactly once semantics](https://www.confluent.io/blog/exactly-once-semantics-are-possible-heres-how-apache-kafka-does-it/)