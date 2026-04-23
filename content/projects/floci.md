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

**GitHub:** [github.com/floci-io/floci](https://github.com/floci-io/floci)

---

## Native Floci vs LocalStack

| Metric | Native Floci | LocalStack | Advantage |
|---|---|---|---|
| **Startup Time** | **~24 ms** | ~3,300 ms | **138× faster** |
| **Idle Memory** | **~13 MiB** | ~143 MiB | **91% less** |
| **Lambda Latency** | **2 ms avg** | 10 ms avg | **5× faster** |
| **Lambda Throughput** | **289 req/s** | 120 req/s | **2.4× faster** |
| **Docker Image Size** | **~90 MB** | ~1.0 GB | **11× smaller** |
| **Price** | **Free Forever** | Auth Token Req. | **$0 / No Auth** |
---

## Supported AWS Services

SSM · SQS · SNS · S3 · DynamoDB · DynamoDB Streams · Lambda · API Gateway REST · API Gateway v2 · IAM · STS · Cognito · KMS · Kinesis · Secrets Manager · CloudFormation · Step Functions · ElastiCache · RDS · MSK · EventBridge · EventBridge Scheduler · CloudWatch Logs · CloudWatch Metrics · ECS · EC2 · ACM · ECR · SES · SES v2 · OpenSearch · Athena · Glue · Data Firehose · AppConfig · AppConfigData · Bedrock Runtime · EKS

Lambda functions run inside **real Docker containers** (Node.js, Python, Java, Go, Ruby) with a
warm pool for sub-millisecond reuse. ElastiCache, RDS, MSK, ECS, EKS, ECR, and OpenSearch spin up
real Docker containers on demand. All 35 services are free, with no auth tokens required.

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
docker run --rm -p 4566:4566 floci/floci:latest
```

Then point any AWS SDK or CLI at `http://localhost:4566` with any dummy credentials.

---

> Read the full deep-dive on the [blog]({{< relref "/posts/introducing-floci" >}}).
