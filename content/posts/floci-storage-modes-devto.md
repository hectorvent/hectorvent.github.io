---
title: "Floci Storage Modes: Pick the Right Trade-off Per Service"
date: 2026-05-03
description: "A dev.to write-up on Floci's four storage modes (memory, hybrid, persistent, and WAL), how to choose the right durability versus speed trade-off per service, and why none of it sits behind a paywall."
tags: ["aws", "java", "quarkus", "open-source", "devtools", "localstack"]
author: "Hector Ventura"
cover:
  image: "/images/floci2-final4.svg"
  imageDark: "/images/floci2-final4-dark.svg"
  alt: "Floci: a fast, free, no-strings AWS emulator"
showToc: false
TocOpen: false
draft: false
---

> **This is a cross-post.** I wrote this up for the dev.to audience. For the full architecture, benchmarks, and SDK compatibility numbers, read the in-depth write-up here on the site: [**Introducing Floci**](/posts/introducing-floci/).

Persistence is exactly the kind of feature emulators love to lock behind a Pro tier. In Floci it is free, and it is configurable. You get four storage modes and you can set them globally or per service, so each service gets the durability versus speed trade-off that actually fits your workload:

- **memory**: fully ephemeral, the fastest option, perfect for CI.
- **hybrid**: serves from memory and flushes to disk asynchronously (roughly every 5 seconds).
- **persistent**: synchronous writes for the strongest durability.
- **WAL**: an append-only write-ahead log with compaction.

All of this keeps Floci's ~24 ms cold start and ~13 MiB idle footprint intact, whether you are running throwaway tests, a long-lived local stack, or a high-throughput pipeline.

## Read it on dev.to

The full write-up lives here:

**[Floci storage modes: pick the right tradeoff per service (and never pay for it)](https://dev.to/hectorvent/floci-localstack-alternative-storage-modes-pick-the-right-tradeoff-per-service-and-never-pay-3nj5)**

Prefer the deep dive with architecture diagrams and benchmark methodology? That's the [**Introducing Floci**](/posts/introducing-floci/) post.
