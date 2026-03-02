---
title: "Workshop: Building Modern and Scalable Web Applications with Java"
date: 2023-11-01
description: "A hands-on workshop presented at PUCMM in collaboration with Java Dominicano, focusing on building full-stack Java applications using Vaadin Flow, Spring Boot, and modern deployment practices with Docker and Ansible."
tags: ["java", "vaadin", "spring-boot", "docker", "ansible", "workshop", "pucmm"]
author: "Hector Ventura"
cover:
  image: "/images/vaadin-logo.svg"
  alt: "Vaadin Logo"
showToc: true
TocOpen: false
draft: false
---

*Workshop presented at [PUCMM](https://www.pucmm.edu.do/) — November 2023. Co-presented with Freddy Peña.*

---

## Overview

In this workshop, we explored how the Java ecosystem has evolved to allow developers to build modern, highly interactive, and scalable web applications without the traditional complexity of managing separate frontend and backend stacks.

The focus was on **Vaadin Flow**, a framework that enables building web UIs 100% in Java, running on the server side while automatically handling the synchronization with the browser.

---

## The Stack

We built a complete application from scratch using:
- **Java 17+** (OpenJDK)
- **Spring Boot 3** for the core application logic.
- **Vaadin Flow** for the reactive web interface.
- **Jakarta Persistence (JPA)** & MariaDB for data storage.
- **Spring Security** for authentication and access control.
- **Docker & Traefik** for local development and containerization.
- **OpenTofu & Ansible** for automated deployment.

---

## Key Modules

### 1. UI Development with Vaadin
We moved away from manual HTML/JS and used Vaadin's component-based model. We explored:
- Creating layouts with `VerticalLayout` and `HorizontalLayout`.
- Data binding with the `Binder` API to connect Java Beans to forms.
- Handling events and navigation using the `@Route` system.

### 2. Backend & Persistence
Integrated Spring Data JPA to manage our database entities. We emphasized:
- Service layer abstraction.
- Automatic database migrations with **Flyway**.
- Secure data access patterns.

### 3. Security
Configuring Spring Security to protect views and data. Vaadin makes this seamless by providing annotations like `@AnonymousAllowed` or `@RolesAllowed` directly on the UI components.

### 4. Scalable Deployment
The final part of the workshop focused on taking the app to production:
- **Dockerization:** Creating efficient multi-stage Docker builds.
- **Reverse Proxy:** Using **Traefik** for automatic SSL and load balancing.
- **Automation:** Using **Ansible** to provision and update the application servers.

---

## Conclusion

Building web applications in Java doesn't mean building "old" applications. With tools like Vaadin and Spring Boot, Java developers can achieve a development speed comparable to modern JS frameworks while maintaining the type safety and robustness of the JVM.

---

### Resources
- [Demo Project on GitHub](https://github.com/hectorvent/workshop-modern-java-web-apps)
- [Full Presentation (PDF)](/temp/WorkShop%20-%20Construyendo%20Aplicaciones%20Web%20Modernas%20y%20Escalables%20con%20Java.pdf)
- [Vaadin Documentation](https://vaadin.com/docs)
