---
title: "Introduction to Eclipse Vert.x: Reactive Programming on the JVM"
date: 2018-09-01
description: "A talk given at ITLA Santiago introducing reactive systems concepts and Eclipse Vert.x — an event-driven, non-blocking toolkit for building reactive applications on the JVM."
tags: ["java", "vertx", "reactive", "jvm", "talk"]
author: "Hector Ventura"
cover:
  image: "https://vertx.io/images/vertx_logo.svg"
  alt: "Eclipse Vert.x logo"
showToc: true
TocOpen: false
draft: false
---

*Talk given at [ITLA Santiago](https://itla.edu.do/) — September 2018*

---

## What Are Reactive Systems?

Modern applications demand a new architecture. Reactive systems are designed to be:

- **More flexible** and adaptable to change
- **Loosely coupled** — components interact without tight dependencies
- **Scalable** — from a single node to thousands
- **Fault tolerant** — they handle failures gracefully instead of crashing
- **Highly responsive** — they respond in a timely manner, always

### The Reactive Manifesto

The [Reactive Manifesto](https://www.reactivemanifesto.org/) defines four core traits that every reactive system must have:

```
                    ┌─────────────┐
                    │  Responsive │  ← Value
                    └──────┬──────┘
           ┌───────────────┼───────────────┐
    ┌───────┴──────┐        │       ┌───────┴──────┐
    │   Elastic    │◄───────┼──────►│   Resilient  │  ← From
    └───────┬──────┘        │       └───────┬──────┘
           └───────────────┼───────────────┘
                    ┌──────┴──────┐
                    │Message Driven│  ← Means
                    └─────────────┘
```

**1. Responsive** — The system responds in a timely manner whenever possible. Fast and consistent response times, establishing reliable upper bounds so they deliver a consistent quality of service.

**2. Resilient** — The ability of a system to withstand and recover from failures and disturbances. Failures are contained within each component, isolating them from each other.

**3. Elastic** — The system reacts to changes in the input rate by increasing or decreasing the resources allocated to serve those inputs. No contention points or central bottlenecks.

**4. Message Driven** — Communication via messages/events, including errors, with transparency in the location of components — highly decoupled.

---

## Why Reactive Systems?

The demands on applications have fundamentally changed over the past decade:

| | 10 Years Ago | Present & Future-Proof |
|---|---|---|
| **Hosting** | 10s of servers | 1000s of nodes or containers |
| **Response time** | Seconds | Milliseconds, <200ms |
| **Maintenance window** | Hours of downtime | Zero downtime, hot updates |
| **Data volume** | GBs | TBs → PBs |

Applications built the old way simply cannot meet these new requirements. Reactive systems exist to close that gap.

---

## Eclipse Vert.x

> **Eclipse Vert.x** is a toolkit for building reactive applications on the JVM.

Vert.x is an open source project under the **Eclipse Foundation**, started in 2012 by Tim Fox. It is built on top of **Netty** — a high-performance asynchronous networking library.

### Scalable by Design

Vert.x is **event-driven** and **non-blocking**. This means your applications can handle massive concurrency using a small number of kernel threads. Vert.x lets you scale with minimal hardware.

### Polyglot

You can use Vert.x with multiple languages — all running on the same JVM:

- **Java**
- **JavaScript**
- **Groovy**
- **Ruby**
- **Ceylon**
- **Scala**
- **Kotlin**

The same HTTP server in three languages:

**Java**
```java
import io.vertx.core.AbstractVerticle;

public class Server extends AbstractVerticle {
    public void start() {
        vertx.createHttpServer().requestHandler(req -> {
            req.response()
               .putHeader("content-type", "text/plain")
               .end("Hello from Vert.x!");
        }).listen(8080);
    }
}
```

**JavaScript**
```javascript
vertx.createHttpServer()
    .requestHandler(function(req) {
        req.response()
            .putHeader("content-type", "text/plain")
            .end("Hello from Vert.x!");
    }).listen(8080);
```

**Ruby**
```ruby
$vertx.create_http_server.request_handler { |req|
    req.response
        .put_header("content-type", "text/plain")
        .end("Hello from Vert.x!")
}.listen(8080)
```

---

## Key Concepts in Vert.x

### Verticle

The **Verticle** is the fundamental unit of deployment in Vert.x — similar to an Actor in actor-model frameworks. You write your application logic inside Verticles.

```java
import io.vertx.core.AbstractVerticle;

public class Server extends AbstractVerticle {
    public void start(Future<Void> startFuture) {
        // Your code here
    }
}
```

### Event Bus

The **Event Bus** is the nervous system of Vert.x. It allows different parts of your application — even running on different nodes — to communicate via messages. It supports three patterns:

- **Point to Point** — send a message to a single consumer
- **Publish / Subscribe** — broadcast to all registered consumers
- **Request / Response** — send and await a reply

### Event Loop

Vert.x follows the **multi-reactor pattern**: instead of a single event loop (like Node.js), Vert.x runs multiple event loops — one per CPU core — allowing true parallel processing without shared mutable state.

```
Single Reactor         Multi-Reactor (Vert.x)
     ↺                  ↺  ↺
                        ↺  ↺
```

Each Verticle is always executed on the same event loop thread, making concurrency safe without synchronization.

### The Golden Rule

> **Never block the Event Loop.**

Calling `Thread.sleep()`, doing blocking I/O, or running CPU-intensive work on the event loop thread will degrade performance for all other requests. For blocking operations, Vert.x provides a **worker thread pool**.

### Future

`Future<T>` is Vert.x's mechanism for handling asynchronous results. Operations that would normally block return a `Future` immediately, and you attach handlers that execute when the result is available.

---

## Demo Lab

The code used in this talk is available on GitHub:

- [github.com/hectorvent/vertx-lab](https://github.com/hectorvent/vertx-lab)

---

## Resources

- [Eclipse Vert.x official site](https://vertx.io/)
- [The Reactive Manifesto](https://www.reactivemanifesto.org/)
- [Vert.x documentation](https://vertx.io/docs/)
