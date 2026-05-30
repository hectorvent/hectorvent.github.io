---
title: "Floci: Local Cloud Emulators for AWS, Azure & GCP"
date: 2026-02-28
description: "Floci is a suite of fast, free, MIT-licensed local cloud emulators for AWS, Azure, and GCP. Built with Quarkus and GraalVM, each starts in ~24ms and idles around 13 MiB, with no accounts, auth tokens, or usage limits."
tags: ["aws", "azure", "gcp", "java", "quarkus", "graalvm", "docker", "open-source"]
showToc: false
draft: false
---

**Floci** is a suite of local cloud emulators that let you run **AWS, Azure, and GCP** services on
your own machine, with no accounts, auth tokens, or usage limits. Every emulator is built with
Quarkus, compiled to a native binary with GraalVM Mandrel, starts in ~24 ms, and idles around
13 MiB. Everything is MIT-licensed and free forever.

The name comes from *cirrocumulus floccus*, a small, fluffy cloud formation. That's the design
goal: minimal, lightweight, and always free.

**Website:** [floci.io](https://floci.io) &nbsp;·&nbsp; **GitHub:** [github.com/floci-io](https://github.com/floci-io)

---

## The Floci family

- **[Floci](https://github.com/floci-io/floci)** (AWS): a drop-in replacement for LocalStack,
  emulating 47 services on port `4566`.
- **[Floci-Az](https://github.com/floci-io/floci-az)** (Azure): 8 services on port `4577`, including
  Blob, Queue, and Table Storage, Functions, Key Vault, Event Hubs, and Service Bus.
- **[Floci-GCP](https://github.com/floci-io/floci-gcp)** (GCP): 7 services on port `4588`, including
  Cloud Storage, Pub/Sub, Firestore, Datastore, Secret Manager, IAM, and Managed Kafka.

---

## Native Floci (AWS) vs LocalStack

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
real Docker containers on demand. All 47 services are free, with no auth tokens required.

---

## Stack

- **Java 25** + **Quarkus 3.x**: reactive, lightweight runtime
- **GraalVM Mandrel**: compiles to a native binary with no JVM required
- **Vert.x**: embedded HTTP server for the Lambda Runtime API
- **docker-java**: container lifecycle management
- **MIT License**

---

## Quick Start

```bash
# AWS  (port 4566)
docker run --rm -p 4566:4566 floci/floci:latest

# Azure  (port 4577)
docker run --rm -p 4577:4577 floci/floci-az:latest

# GCP  (port 4588)
docker run --rm -p 4588:4588 floci/floci-gcp:latest
```

Then point any AWS, Azure, or GCP SDK or CLI at the matching local endpoint with any dummy
credentials.

---

> Read the full deep-dive on the [blog]({{< relref "/posts/introducing-floci" >}}).
