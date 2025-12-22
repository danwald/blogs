---
title: "Kafka considerations"
datePublished: Mon Dec 22 2025 16:52:32 GMT+0000 (Coordinated Universal Time)
cuid: cmjhe9eg9000102jp4jnz4es0
slug: kafka-considerations
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/HYcSWOYiWyE/upload/0a524d35173169a07f31497e84298e0b.jpeg
tags: queue, kafka

---

### Auto-commit - at most once delivery

When consumers are configured with auto-commit, the queue offset will commit on message delivery. If the process dies before processing, the message is effectively lost.

### Manual commit - at least once delivery

When manually committing messages which is done after processing occurs, if the process dies before committing, the message will be reprocessed by another consumer as the offset isn’t updated.

### Always close your connections

Kafka consumers are run in a long running processes or maybe as a cronjob. The process connects to the configured cluster, topic and group. On exit, you need to explicitly close the connection. If not the topic/group will enter a rebalancing state where no messages can be read by existing consumers causing a delay in processing or even message loss.

### Rebalancing

When a consumer enters/leaves a group, dies or partitions are reassigned.

### Use a consumer group

It will load balance non overlapping messages across consumers, automatically assigns partitions and manage offsets. However there is chance of reprocessing of messages during rebalancing.

### Exactly once delivery

Can be configured at the server level, but drastically reduces throughput.

### Be idempotent

Duplicate messages will be the norm. Use the strategies below to avoid reprocessing messages.

* Unique constraints on application tables
    
* Unique constraints on separate message table
    
* Use the outbox pattern when adding to the DB + producing a message
    
* Redis deduplication with NX
    
* Produce Application level messages with a unique ID
    

### Don’t manually assign partitions

This bypasses coordination across consumer group of a topic. The application has to manage conflicts.

### Static members to avoid rebalancing

You can specify a unique `group_instance_id` of each instance to avoid rebalancing and its effects. Can be managed via k8s.