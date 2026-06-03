---
title: "Standing on Shoulders: The Stack That Makes Floci Start in 24ms"
date: 2026-05-21
description: "A dev.to write-up on the open-source stack behind Floci's ~24 ms startup: Netty, Vert.x, Quarkus, and GraalVM Mandrel, and how years of production hardening in those projects make it possible."
tags: ["aws", "java", "quarkus", "graalvm", "vertx", "open-source"]
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

Floci's ~24 ms startup is not one clever trick. It is four battle-tested open-source projects stacked on top of each other, each doing the job it does best:

- **Netty** for high-performance async I/O.
- **Vert.x** for the reactive, event-driven toolkit.
- **Quarkus** for the application framework and build-time optimization.
- **GraalVM Mandrel** to compile the whole thing to a native binary.

Together they take startup from the 2 to 6 seconds a typical JVM app needs down to ~24 ms, and idle memory from a few hundred MiB down to ~13 MiB. The honest takeaway is that this speed is borrowed: years of production hardening in those libraries are what let Floci spend its own effort on the part that matters, AWS protocol fidelity across 45 services and 1,925 SDK compatibility tests (Java, Python, Node.js, Go, and Rust).

## Read it on dev.to

The full write-up lives here:

**[Standing on shoulders: the stack that makes Floci start in ~24ms](https://dev.to/hectorvent/standing-on-shoulders-the-stack-that-makes-floci-start-in-24ms-45mk)**

Prefer the deep dive with architecture diagrams and benchmark methodology? That's the [**Introducing Floci**](/posts/introducing-floci/) post.
