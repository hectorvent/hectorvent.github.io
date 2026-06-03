---
title: "The Floci Philosophy: Stay Tiny, Feel Like Real AWS"
date: 2026-05-09
description: "A dev.to write-up on the design philosophy behind Floci: how it stays tiny while still behaving like real AWS, instead of forcing you to choose between fast-but-fake and heavy-but-faithful emulation."
tags: ["aws", "java", "quarkus", "open-source", "devtools", "architecture"]
author: "Hector Ventura"
cover:
  image: "/images/floci2-final4.svg"
  imageDark: "/images/floci2-final4-dark.svg"
  alt: "Floci: a fast, free, no-strings AWS emulator"
showToc: false
TocOpen: false
draft: false
---

> **This is a cross-post.** I wrote up the design philosophy behind **Floci** for the dev.to audience. For the full architecture, benchmarks, and SDK compatibility numbers, read the in-depth write-up here on the site: [**Introducing Floci**](/posts/introducing-floci/).

Most AWS emulators make you pick a side: fast-but-fake (shallow mocks that pass your unit tests but never catch real integration bugs) or heavy-but-faithful (a giant container that boots in seconds and eats hundreds of MiB). Floci refuses that tradeoff.

The trick is a three-pattern architecture. Stateless services run in-process for instant responses. Analytics-style services lean on tiny embedded engines like DuckDB. The genuinely complex services (think PostgreSQL via RDS) spin up real Docker containers on demand. The guiding rule is simple: never reimplement an engine that already exists; wrap the real AWS API around the real thing. That is how Floci keeps a ~24 ms startup, ~13 MiB idle footprint, and a ~90 MB image while still feeling like real AWS. A service like Postgres taking ~3 seconds to start is an acceptable price for true fidelity.

## Read it on dev.to

The full write-up lives here:

**[The Floci philosophy: stay tiny, feel like real AWS](https://dev.to/hectorvent/the-floci-philosophy-stay-tiny-feel-like-real-aws-1h3d)**

Prefer the deep dive with architecture diagrams and benchmark methodology? That's the [**Introducing Floci**](/posts/introducing-floci/) post.
