---
title: "Floci — AWS Local Emulator"
date: 2026-02-28
description: "A fast, free, and open-source local AWS service emulator built with Quarkus and GraalVM. Starts in 19ms, uses 42 MiB at idle, and passes 100% of AWS SDK compatibility tests."
tags: ["aws", "java", "quarkus", "graalvm", "docker", "open-source"]
showToc: false
draft: false
---

**Floci** is a local AWS service emulator — a drop-in replacement for LocalStack's community
edition that requires no auth token, has no usage limits, and is MIT-licensed.

The name comes from *cirrocumulus floccus*, a small, fluffy cloud formation. That's the design
goal: minimal, lightweight, and always free.

**GitHub:** [github.com/hectorvent/floci](https://github.com/hectorvent/floci)

---

## Key Numbers

| Metric | Native | JVM |
|---|---|---|
| Startup time | 19 ms | 771 ms |
| Idle memory | 42 MiB | 96 MiB |
| AWS SDK test pass rate | 100% (166/166) | 100% (166/166) |
| Docker image size | ~47 MB | ~400 MB |

---

## Supported AWS Services

SSM · SQS · S3 · DynamoDB · Lambda · SNS · API Gateway · IAM · STS · ElastiCache · RDS

Lambda functions run inside **real Docker containers** (Node.js, Python, Java, Go, Ruby) with a
warm pool for sub-millisecond reuse. ElastiCache and RDS spin up actual Redis and database
containers on demand.

---

## Stack

- **Java 25** + **Quarkus 3.x** — reactive, lightweight runtime
- **GraalVM Mandrel** — compiles to a native binary with no JVM required
- **Vert.x** — embedded HTTP server for the Lambda Runtime API
- **docker-java** — container lifecycle management
- **MIT License**

---

## Quick Start

```bash
docker run --rm -p 4566:4566 hectorvent/floci:native
```

Then point any AWS SDK or CLI at `http://localhost:4566` with any dummy credentials.

---

> Read the full deep-dive on the [blog]({{< relref "/posts/introducing-floci" >}}).
