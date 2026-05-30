---
title: "Floci on dev.to: the Short Version"
date: 2026-04-30
description: "A shorter, community-friendly intro to Floci that I published on dev.to, the fast, free, zero-auth AWS emulator. Cross-post with links to the original and the full deep dive."
tags: ["aws", "java", "quarkus", "devtools", "open-source", "docker"]
author: "Hector Ventura"
cover:
  image: "/images/floci2-final4.svg"
  imageDark: "/images/floci2-final4-dark.svg"
  alt: "Floci: a fast, free, no-strings AWS emulator"
showToc: false
TocOpen: false
draft: false
---

> **This is a cross-post.** I wrote a shorter, community-friendly intro to **Floci** for the dev.to audience. If you want the full architecture, benchmarks, and SDK compatibility numbers, read the in-depth write-up here on the site: [**Introducing Floci**](/posts/introducing-floci/).

The short pitch: **LocalStack Community Edition** started requiring auth tokens and moved features behind paid tiers in early 2026. **Floci** fills that gap, a free, open-source, MIT-licensed AWS emulator that starts in ~24ms, idles at ~13 MiB, runs on the same port `4566`, and never asks for an account, token, or quota.

It backs Lambda, RDS, ElastiCache, MSK, OpenSearch, ECS, and EKS with real Docker containers (not shallow mocks) and ships 1,850+ SDK compatibility tests across Java, JavaScript, boto3, AWS CLI, Go, and Rust.

```bash
docker run -p 4566:4566 floci/floci:latest
export AWS_ENDPOINT_URL="http://localhost:4566"
aws s3 mb s3://my-bucket
```

## Read it on dev.to

The full community write-up lives here:

**[Meet Floci: a fast, free, no-strings AWS emulator (no auth token, no quotas)](https://dev.to/hectorvent/meet-floci-a-fast-free-no-strings-aws-emulator-no-auth-token-no-quotas-2gdh)**

Prefer the deep dive with architecture diagrams and benchmark methodology? That's the [**Introducing Floci**](/posts/introducing-floci/) post.
