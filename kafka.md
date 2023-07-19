# Kafka Fundamentals

Speaker: Daniel Hinojosa

[Workshop Repository](https://github.com/dhinojosa/nfjs-kafka-half-day/)

- [Kafka Fundamentals](#kafka-fundamentals)
  - [Why Use Kafka?](#why-use-kafka)
  - [Messages](#messages)
  - [Producers](#producers)
  - [Consumers](#consumers)
  - [Brokers](#brokers)
  - [Hardware Requirements](#hardware-requirements)
  - [Guarantees](#guarantees)
  - [Other Resources](#other-resources)
    - [References](#references)

## Why Use Kafka?

- Having many different services or applications interacting via HTTP can be complicated and error prone
- Kafka can be used as a Pub/Sub mechanism to centralize the management of those interactions
- Producers publish messages and Consumers subscribe to them, but Producers can also be Consumers
- Handles millions of messages per second, high throughput, high volume
- Distributed and replicated commit-log
- Append-only, immutable messages
- Scalable and elastic
- Fault-tolerant

## Messages

- Similar to a row or record
- An array of bytes
- No special serialization
- May contain a key for better distribution to partitions
  - If provided, a partitioner will hash the key and map it to a single partition
  - Only time that something is guaranteed to be in order
- Stored in topics, similar tot database tables
- Retained for a week by default

## Producers

- Sends and prepares messages
- Batches messages when possible
  - Sent to the same topic and partition
  - Avoids overhead of sending multiple messages over the wire

## Consumers

- Consumer can be assigned to multiple partitions, but not vice versa
- Can choose how messages are read
  - From last read
  - From the beginning
  - From latest
  - From storage

## Brokers

- Holds the partitions
- Partitions of a topic are distributed across brokers, therefore a single topic is scaled
- Each partition elects a leader on a single broker
- All read and writes go to the leader partition for a topic, and the leader handles replication to other brokers

## Hardware Requirements

- Do not co-locate other applications due to memory page cache pollution, will degrade performance
- Performant drive is required (i.e. SSD)
- Storage capacity needs to be calculated b the expected messages per day and retention
- Slower networks can degrade the rate in which messages are produced

## Guarantees

- Messages sent by a producer to a particular topic partition will be appended in the order sent
- A consumer instance sees records in the order they are stored in the log
- For a topic with replication factor N, we will tolerate up to N-1 server failures without losing any records committed to the log

## Other Resources

### References

- [Confluent Hub: Discover Kafka connectors](https://www.confluent.io/hub/)
- [Kafka Visualization](https://softwaremill.com/kafka-visualisation/)
- [kcat Utility](https://docs.confluent.io/platform/current/clients/kafkacat-usage.html)
