---
title: "Infrastructure as Code (IaC) for Everyone - Java Dominicano"
date: 2024-10-01
description: "A summary of the talk presented at the Java Dominicano Monthly Talks (October 2024) on democratizing Infrastructure as Code, exploring how any developer can benefit from automation."
tags: ["iac", "opentofu", "pulumi", "ansible", "java-dominicano", "talk"]
author: "Hector Ventura"
cover:
  image: "/images/iac-hero-java.png"
  alt: "Infrastructure as Code Concept Image"
showToc: true
TocOpen: false
draft: false
---

*Talk presented at the [Java Dominicano Monthly Talks](https://linktr.ee/javadominicano) — October 2024*

---

## The Importance of Automation

In this edition of the Java Dominicano Monthly Talks, we revisited the concept of **IaC for everyone**. The premise is simple: infrastructure as code is not exclusive to Site Reliability Engineers (SREs) or DevOps experts; it is an essential skill for every modern software developer.

### Why should you use IaC?
- **Deployment Speed:** Go from taking hours to having an environment ready in seconds.
- **Living Documentation:** Your infrastructure is the code, not an outdated document.
- **Consistency:** Eliminate the "it works on my machine" problem at the infrastructure level as well.

---

## The Ecosystem Tools

During the session, we compared three different approaches to managing cloud resources (using DigitalOcean as an example):

### 1. The CLI Approach (`doctl`)
Ideal for quick scripts and ad-hoc tasks. It is the easiest entry point to interact with a provider's API.

### 2. The Declarative Approach (OpenTofu)
Using human-readable configuration files, we define the **desired state** of our infrastructure. OpenTofu takes care of calculating the difference and applying the necessary changes.

### 3. The Programmatic Approach (Pulumi)
For Java developers, Pulumi offers a familiar experience by allowing infrastructure to be defined using the Java SDK. This enables the use of loops, conditionals, and abstractions native to the language.

---

## Configuration and Demo

The final demo showed how to orchestrate the creation of a complete web infrastructure and its subsequent automatic configuration.

1. **Provisioning:** Creation of Droplets and a Load Balancer.
2. **Configuration:** Installing Nginx and databases using Ansible.

```bash
# Example of executing the complete workflow
opentofu apply -auto-approve
ansible-playbook -i inventory.ini setup-site.yml
```

---

## Conclusion

The main message for the Java Dominicano community was: **Start small**. You don't need to automate your entire company's infrastructure today. Start by automating the creation of a local database server or a testing environment, and you will soon see the benefits of having your infrastructure under version control.

---

### Resources
- [Demo code on GitHub](https://github.com/hectorvent/java-dominicano-monthly-talks)
- [Presentation (PDF)](/temp/IaC%20-%20Java%20Dominicano%20Monthly%20Talks.pdf)
- [Java Dominicano Community](https://linktr.ee/javadominicano)
