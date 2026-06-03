---
title: "Real-Time Data Streaming with Postgres & Debezium"
date: 2026-04-15
description: "An interactive presentation about Change Data Capture (CDC) using Debezium to stream real-time updates from PostgreSQL."
tags: ["postgresql", "debezium", "cdc", "kafka", "data-streaming", "talk"]
author: "Hector Ventura"
deck: "/presentation/2026-debezium/"
event: "Postgres MetroPlex Dallas"
showToc: false
draft: false
---

This presentation explores the power of **Change Data Capture (CDC)** to transform your database into a real-time event source. We dive into the architecture of Debezium, how it leverages PostgreSQL's logical decoding, and how to build resilient data pipelines.

## What is CDC?

**Change Data Capture (CDC)** is a set of software design patterns used to determine and track the data that has changed so that action can be taken using the changed data.

Instead of traditional polling (which is slow and adds load to the database), CDC allows us to stream every `INSERT`, `UPDATE`, and `DELETE` as it happens, with sub-second latency.

## Why Debezium?

[Debezium](https://debezium.io/) is an open-source distributed platform for change data capture. It points at your databases, and your applications can start responding to all of the row-level changes other applications make to your databases.

Debezium is built on top of **Apache Kafka** and provides connectors for several databases, with PostgreSQL being one of the most robust.

### Key Advantages
- **Low Latency:** Changes are captured almost instantly.
- **No Schema Changes:** You don't need to add `updated_at` columns or triggers to your tables.
- **Reliability:** Captures every change, even those that happen while your application is down.

## How it Works with Postgres

PostgreSQL uses a mechanism called **Logical Decoding** to extract changes from the Write-Ahead Log (WAL). Debezium hooks into this log using a logical decoding plugin (like `pgoutput`), converts the binary log into a structured format (JSON or Avro), and pushes it to Kafka.

### Data Flow Diagram

```mermaid
flowchart LR
    subgraph DB ["PostgreSQL Server"]
        WAL[(Write-Ahead Log)]
        Plugin[Logical Decoding Plugin]
        WAL --> Plugin
    end

    subgraph Streaming ["Streaming Layer"]
        Debezium[Debezium Connector]
        Kafka{{Apache Kafka}}
        Debezium --> Kafka
    end

    Plugin -- Change Events --> Debezium

    subgraph Consumers ["Downstream Systems"]
        App[Search Index / ES]
        Cache[Redis / Cache]
        Analytics[Data Warehouse]
    end

    Kafka --> App
    Kafka --> Cache
    Kafka --> Analytics

    style Kafka fill:#fff9c4,stroke:#fbc02d,stroke-width:2px
    style DB fill:#e1f5fe,stroke:#01579b
```

## What the Talk Covers

1. **Configuring PostgreSQL** for logical replication.
2. **Setting up Debezium** using Docker and Kafka Connect.
3. **Handling Schema Evolutions** without breaking downstream consumers.
4. **Real-world Use Cases:** cache invalidation, building search indexes, and microservices synchronization.

### Resources
- [Postgres MetroPlex Dallas Meetup](https://www.meetup.com/dallas-fort-worth-postgres/)
- [Debezium Official Documentation](https://debezium.io/documentation/)
- [PostgreSQL Logical Replication](https://www.postgresql.org/docs/current/logical-replication.html)
