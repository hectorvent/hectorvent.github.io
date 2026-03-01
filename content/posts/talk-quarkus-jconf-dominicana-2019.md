---
title: "Quarkus: Supersonic Subatomic Java"
date: 2019-07-01
description: "A talk given at JConf Dominicana 2019 introducing Quarkus — the Kubernetes-native Java stack built on GraalVM and OpenJDK, unifying imperative and reactive programming with blazing-fast startup times and minimal memory footprint."
tags: ["java", "quarkus", "graalvm", "kubernetes", "microservices", "talk"]
author: "Hector Ventura"
cover:
  image: "https://design.jboss.org/quarkus/logo/final/PNG/quarkus_logo_horizontal_rgb_600px_default.png"
  alt: "Quarkus - Supersonic Subatomic Java"
showToc: true
TocOpen: false
draft: false
---

*Talk given at [JConf Dominicana](https://jconfdominicana.org/) — July 2019*

---

## What Is Quarkus?

**Quarkus** is a Kubernetes-native Java stack designed for GraalVM and OpenJDK HotSpot, crafted from the best Java libraries and standards.

| | |
|---|---|
| **Created by** | Red Hat |
| **License** | Apache License v2.0 |
| **Version at time of talk** | 1.0.0.CR2 |

The tagline says it all: **Supersonic Subatomic Java** — startup times measured in milliseconds, memory footprints measured in megabytes.

---

## GraalVM — The Engine Behind Native Compilation

**GraalVM** is a universal virtual machine capable of running JavaScript, Python, Ruby, R, Java, all JVM-based languages, and LLVM-based languages like C and C++.

It eliminates the isolation between programming languages and enables interoperability in a shared runtime.

| | |
|---|---|
| **Created by** | Oracle |
| **Licenses** | CE (GPLv2), Enterprise Edition |
| **Version at talk** | CE 19.3.0 (Java 11 support) |

GraalVM sits at the center of a polyglot ecosystem:

```
Kotlin  Java  JS  Ruby  R  Python  C  C++  Rust
           ↓    ↓   ↓   ↓   ↓     ↓   ↓
  ┌─────────────────────────────────────────┐
  │  Automatic transformation of            │
  │  interpreters to compiler               │
  │                                         │
  │              GraalVM                    │
  │                                         │
  │  Embeddable in native or managed apps   │
  └─────────────────────────────────────────┘
       ↑           ↑           ↑          ↑
   OpenJDK      Node.js    Oracle DB   standalone
```

### AOT vs JIT — Choosing Your Trade-offs

GraalVM introduces **Ahead-of-Time (AOT)** compilation as an alternative to the traditional **Just-in-Time (JIT)** model:

| Dimension | AOT (Native) | JIT (JVM) |
|---|---|---|
| **Startup Speed** | Excellent | Slow |
| **Peak Throughput** | Good | Excellent |
| **Low Memory Footprint** | Excellent | Average |
| **Reduced Max Latency** | Good | Excellent |
| **Small Packaging** | Excellent | Average |

AOT wins on startup speed, memory, and packaging — ideal for containers and serverless. JIT wins on raw throughput — ideal for long-running batch or high-load services.

---

## Built on Standards

Quarkus doesn't reinvent the wheel. It is built on top of the Java ecosystem's most proven libraries and specifications:

- **CDI** — Contexts and Dependency Injection
- **JAX-RS** — REST web services
- **JPA / JTA** — Persistence and transactions
- **MicroProfile** — Cloud-native Java APIs
- **Apache Camel** — Integration patterns
- **Hibernate** — ORM
- **Eclipse Vert.x** — Reactive toolkit
- **Netty** — Async networking

### MicroProfile 3.0

MicroProfile 3.0 (current at the time) provided a rich set of cloud-native APIs that Quarkus fully supports:

| Spec | Version | Status |
|---|---|---|
| Open Tracing | 1.3 | Unchanged |
| Open API | 1.1 | Unchanged |
| Rest Client | 1.3 | **New** |
| Config | 1.3 | Unchanged |
| Fault Tolerance | 2.0 | Unchanged |
| Metrics | 2.0 | **Updated** |
| JWT Propagation | 1.1 | Unchanged |
| Health Check | 2.0 | **Updated** |
| CDI | 2.0 | Unchanged |
| JSON-P | 1.1 | Unchanged |
| JAX-RS | 2.1 | Unchanged |
| JSON-B | 1.0 | Unchanged |

---

## Developer Joy

Quarkus was designed with developer experience at its core:

- **Unified configuration** — one `application.properties` file for everything
- **Live reload in the blink of an eye** — save the file, see the change instantly, no restart needed
- **Simplified code for 80% of use cases**, flexible for the remaining 20%
- **Effortless native executable generation** — one Maven flag to produce a native binary

> *"Wait. So you just save it, and your code is running? And it's Java?!"*
> *"I know, right? Supersonic Java, FTW!"*

---

## Unifying Imperative and Reactive Programming

One of Quarkus's biggest innovations is that it lets you write both **imperative** and **reactive** code within the same application, choosing the best style for each use case.

**Imperative style** (familiar, blocking):
```java
@Inject
SayService say;

@GET
@Produces(MediaType.TEXT_PLAIN)
public String hello() {
    return say.hello();
}
```

**Reactive style** (non-blocking, streaming):
```java
@Inject
@Channel("kafka")
Publisher<String> reactiveSay;

@GET
@Produces(MediaType.SERVER_SENT_EVENTS)
public Publisher<String> stream() {
    return reactiveSay;
}
```

### How Does Quarkus Achieve This?

The secret is **Eclipse Vert.x / Netty** as the unified I/O core. All incoming traffic — HTTP requests, messages, events — flows through the same non-blocking layer:

```
  Undertow         RESTEasy        Reactive     Reactive
  (Servlet)        (JAX-RS)        Messaging     Routes
      ↑               ↑               ↑             ↑
      └───────────────┴───────────────┴─────────────┘
                           │
                  Eclipse Vert.x / Netty
                  (Messages, HTTP, Events)
                           │
                           └──────────────→ Reactive Data Access
```

The thread model separates concerns cleanly:

- **Worker threads** handle blocking code (Undertow/Servlet, JAX-RS)
- **Event loops** handle non-blocking I/O (Vert.x/Netty)

Both live in the same process, sharing the same I/O layer, which is what makes the unification possible.

---

## Container-First Performance

The numbers speak for themselves.

### REST Application

| Stack | Memory | Startup Time |
|---|---|---|
| Quarkus + Native (GraalVM) | **12 MB** | **0.016 s** |
| Quarkus + JVM (OpenJDK) | 73 MB | 0.943 s |
| Traditional Cloud-Native Stack | 136 MB | 4.3 s |

### REST + CRUD Application

| Stack | Memory | Startup Time |
|---|---|---|
| Quarkus + Native (GraalVM) | **28 MB** | **0.042 s** |
| Quarkus + JVM (OpenJDK) | 145 MB | 2.033 s |
| Traditional Cloud-Native Stack | 209 MB | 9.5 s |

Quarkus Native starts **226× faster** and uses **94% less memory** than a traditional stack in the REST+CRUD scenario. This makes a dramatic difference when scaling thousands of containers.

---

## Getting Started

### Prerequisites

**Tools:**
- JDK (OpenJDK 8+)
- Maven 3.6+
- GraalVM 19.2+ (for native builds)

**Environment variables:**
```bash
export JAVA_HOME=/path/to/jdk
export MAVEN_HOME=/path/to/maven
export GRAALVM_HOME=/path/to/graalvm
```

### Bootstrap a New Project

```bash
mvn io.quarkus:quarkus-maven-plugin:create \
  -DprojectGroupId=org.acme \
  -DprojectArtifactId=getting-started \
  -DclassName="org.acme.GreetingResource" \
  -Dpath="/hello"
```

### Run in Dev Mode (Live Reload)

```bash
mvn quarkus:dev
```

### Build a Native Executable

```bash
mvn package -Pnative
./target/getting-started-runner
```

---

## Demo Focus Areas

The live demo covered:

- **Easy configuration** — single unified properties file
- **The Twelve-Factor App** — codebase, dependencies, config, port binding, etc.
- **Microservices patterns**:
  - Fault Tolerance & Resilience (`@Fallback`, `@Retry`, `@CircuitBreaker`)
  - Metrics (`/metrics` endpoint via MicroProfile Metrics)
  - Health Checks (`/health/live`, `/health/ready`)
- **Containerizing the demo** — packaging the native binary in a minimal Docker image

---

## Resources

- [Quarkus official site](https://quarkus.io/)
- [Quarkus guides](https://quarkus.io/guides/)
- [GraalVM](https://www.graalvm.org/)
- [MicroProfile](https://microprofile.io/)
- [JConf Dominicana](https://jconfdominicana.org/)
