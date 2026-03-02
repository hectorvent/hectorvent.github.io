---
title: "Ansible: IT Automation Without an Agent"
date: 2020-11-01
description: "A talk given at BarCamp Dominican Republic 2020 introducing Ansible — the agentless, open source IT automation tool that lets you configure systems, deploy software, and orchestrate complex workflows using simple YAML playbooks."
tags: ["ansible", "devops", "automation", "linux", "infrastructure", "talk"]
author: "Hector Ventura"
cover:
  image: "/images/ansible-logo.png"
  alt: "Ansible logo"
showToc: true
TocOpen: false
draft: false
---

*Talk given at [BarCamp Dominican Republic](https://barcamp.org.do/) — November 2020*

---

## What Is Ansible?

**Ansible®** is an open source, command-line IT automation tool written in Python. It can:

- **Configure systems** — install packages, manage services, edit config files
- **Deploy software** — push application releases across fleets of servers
- **Orchestrate advanced workflows** — rolling upgrades, multi-tier deployments, system updates

What makes Ansible stand out is that it is **agentless** — it communicates with target nodes over standard protocols:
- **OpenSSH** for Linux/Unix targets
- **WinRM** for Windows targets

No daemon to install, no port to open, no certificate authority to manage. If you can SSH into a server, Ansible can automate it.

---

## How It Works

The core model is simple: a **Controller Node** reads an **Inventory** (a list of target hosts) and a **Playbook** (a set of tasks to run), then connects to each target via SSH and executes the tasks.

```
  Host Inventory          Playbook
  ──────────────          ──────────────
  10.58.121.51            zookeeper.yml
  10.58.121.52                │
  10.58.121.53                │
        │                     │
        └──────────┬──────────┘
                   ▼
        ┌─────────────────────┐
        │  Ansible Automation │
        │       Engine        │
        └──────────┬──────────┘
                   │  SSH
          ┌────────┼────────┐
          ▼        ▼        ▼
         Dev       QA      UAT / Prod
```

The same playbook runs against Dev, QA, UAT, and Production — with environment-specific variables swapped in via the inventory. One source of truth, consistent results everywhere.

---

## Key Concepts

### Target Node
Any machine Ansible manages — a VM, a bare-metal server, a cloud instance, a network device. The only requirement is SSH access and Python installed.

### Inventory
A file (INI or YAML) that lists the hosts and groups Ansible will target.

```ini
# inventory.ini
[webservers]
web-server-01 ansible_host=192.168.1.242
web-server-02 ansible_host=192.168.1.243
web-server-03 ansible_host=192.168.1.249

[loadbalancer]
haproxy ansible_host=192.168.1.239

[all:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=~/.ssh/id_rsa
```

### Playbook
A YAML file that defines what to do on which hosts. Each play targets a group and runs a list of tasks.

```yaml
# site.yml
- name: Configure web servers
  hosts: webservers
  become: true
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present

    - name: Copy site config
      template:
        src: nginx.conf.j2
        dest: /etc/nginx/nginx.conf
      notify: Restart nginx

  handlers:
    - name: Restart nginx
      service:
        name: nginx
        state: restarted
```

### Task
A single unit of work — install a package, copy a file, run a command, start a service. Tasks use **modules** (Ansible's built-in library of actions).

### Handler
A task that only runs when notified by another task. Used for actions that should happen only when something actually changes — like restarting a service after its config file is updated.

### Role
A structured way to organize related tasks, templates, variables, and files into a reusable unit. Roles follow a standard directory layout:

```
roles/
  nginx/
    tasks/main.yml
    templates/nginx.conf.j2
    handlers/main.yml
    defaults/main.yml
    vars/main.yml
```

### Ansible Galaxy
The public hub for sharing and downloading pre-built roles and collections. Think of it as npm or Maven Central, but for Ansible automation.

```bash
ansible-galaxy install geerlingguy.nginx
```

### Ansible Collection
A distribution format introduced to package roles, modules, plugins, and playbooks together. Collections replaced loose roles as the standard unit of distribution.

```bash
ansible-galaxy collection install community.general
```

---

## Demo Setup

The demo showed a real-world scenario: **automating the provisioning of an HA Proxy load balancer with three web servers** — all configured from scratch using a single Ansible run.

```
  Clients
     │
     ▼
  HA Proxy  (192.168.1.239)
  ┌─────────────────────────┐
  │                         │
  ▼         ▼               ▼
web-01    web-02           web-03
192.168.1.242  .243        .249

          ▲ managed by ▲
    Controller Node (Ansible)
         192.168.1.141
```

With one `ansible-playbook` command, Ansible:
1. Installed and configured nginx on all three web servers
2. Deployed the application to each node
3. Installed and configured HAProxy on the load balancer
4. Verified health checks

```bash
ansible-playbook -i inventory.ini site.yml
```

Demo code: [github.com/JavaDominicano/ansible-barcamp-2020](https://github.com/JavaDominicano/ansible-barcamp-2020)

---

## Similar Tools

Ansible is not the only configuration management tool out there. Here's how it compares:

| Tool | Agent Required | Language | Learning Curve |
|---|---|---|---|
| **Ansible** | No (agentless) | YAML | Low |
| **Chef** | Yes | Ruby (DSL) | High |
| **Puppet** | Yes | Puppet DSL | High |
| **SaltStack** | Optional | YAML / Python | Medium |

Ansible's agentless model and plain YAML syntax make it the easiest to start with, especially in teams that don't have a dedicated DevOps engineer.

---

## Resources

- [Ansible official site](https://www.ansible.com/)
- [Ansible documentation](https://docs.ansible.com/)
- [Getting started with Ansible](https://steampunk.si/blog/getting-started-with-ansible/)
- [Introduction to configuration management tools](https://steampunk.si/blog/introduction-to-configuration-management-tools/)
- [Adventures in Ansible — lessons from real-world deployments](https://www.redhat.com/en/blog/adventures-ansible-lessons-learned-real-world-deployments)
- [Demo source code](https://github.com/JavaDominicano/ansible-barcamp-2020)
