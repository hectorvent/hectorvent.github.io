---
title: "Meet Floci: a Fast, Free, No-Strings AWS Emulator"
date: 2026-04-30
description: "A summary of my dev.to post on Floci — a zero-auth, MIT-licensed AWS emulator that starts in 24ms and uses 13 MiB at idle."
tags: ["aws", "java", "quarkus", "devtools", "open-source", "docker"]
author: "Hector Ventura"
showToc: false
TocOpen: false
draft: false
---

If you've been following AWS local development tooling, you probably noticed that **LocalStack Community Edition** started requiring auth tokens and moved features behind paid tiers in early 2026. That left a real gap for developers who just want to run AWS services locally. No account, no quotas, no strings attached.

That's exactly why I built **Floci**.

## What is Floci?

Floci is a free, open-source local AWS emulator written in Java with [Quarkus](https://quarkus.io/) and compiled to a native binary via GraalVM. It runs on port `4566`, the same port as LocalStack, so switching requires changing just one environment variable.

The name comes from *cirrocumulus floccus*, a lightweight, popcorn-like cloud formation. The ethos: minimal footprint, fast startup, zero overhead.

## Why it's different

| Metric | Native Floci | LocalStack |
|---|---|---|
| Startup time | **~24 ms** | ~3,300 ms |
| Idle memory | **~13 MiB** | ~143 MiB |
| Image size | **~90 MB** | ~2 GB |
| Auth required | **Never** | Yes |
| Price | **Free forever** | Paid tiers |

Beyond the numbers, Floci runs **real Docker-backed services** for Lambda, RDS (PostgreSQL/MySQL), ElastiCache, MSK, OpenSearch, ECS, and EKS (not shallow mocks). It also ships with 1,850+ automated SDK compatibility tests covering Java v2, JavaScript v3, boto3, AWS CLI v2, Go v2, and Rust.

## Quick start

```bash
docker run -p 4566:4566 floci/floci:latest
export AWS_ENDPOINT_URL="http://localhost:4566"
aws s3 mb s3://my-bucket
```

Testcontainers and Spring Boot auto-configuration are available on Maven Central for seamless integration in your test suites.

## Supported services

Floci covers 40+ AWS services including S3, SQS, SNS, DynamoDB (with Streams), Lambda, API Gateway, Cognito, KMS, Secrets Manager, IAM, STS, Step Functions, CloudFormation, EventBridge, CloudWatch, and Kinesis.

---

For the full write-up including architecture details, benchmark methodology, and the roadmap read the original post on dev.to:

**[Meet Floci: a fast, free, no-strings AWS emulator (no auth token, no quotas)](https://dev.to/hectorvent/meet-floci-a-fast-free-no-strings-aws-emulator-no-auth-token-no-quotas-2gdh)**
