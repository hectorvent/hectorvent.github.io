---
title: "Why Floci Is Built in Java (and Why That's the Right Call in 2026)"
date: 2026-05-16
description: "A dev.to write-up on why Floci is built with Java 25, Quarkus, and GraalVM. A choice driven by hard constraints (cold start, memory, single binary) rather than preference."
tags: ["aws", "java", "quarkus", "graalvm", "open-source", "devtools"]
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

"Java" is not the answer people expect for a tool that has to feel instant. But the choice was made on constraints, not taste. Floci needs to cold start in milliseconds, idle in single-digit MiB, and ship as one small binary that drops cleanly into a CI pipeline. Java 25, compiled with Quarkus and GraalVM, hits all three: a ~24 ms cold start, ~13 MiB idle memory, and a single ~90 MB binary. Modern features like virtual threads let it juggle many AWS services concurrently without ceremony.

The comparison with Python-based LocalStack makes the point plainly: roughly 10x smaller image, far less RAM, and a startup measured in milliseconds instead of tens of seconds. In 2026, "native Java" is not a compromise; it is the efficient default.

## Read it on dev.to

The full write-up lives here:

**[Why Floci is built in Java (and why that's the right call in 2026)](https://dev.to/hectorvent/why-floci-is-built-in-java-and-why-thats-the-right-call-in-2026-50ag)**

Prefer the deep dive with architecture diagrams and benchmark methodology? That's the [**Introducing Floci**](/posts/introducing-floci/) post.
