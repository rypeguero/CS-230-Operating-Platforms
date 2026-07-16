# 🎮 Game Design Document: **Draw It or Lose It**
### CS 230 Project Software Design — Version 3.0

<p align="left">
  <img src="https://img.shields.io/badge/Course-CS--230-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Project-Software%20Design-success?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Version-3.0-orange?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Last%20Updated-12%2F13%2F2024-lightgrey?style=for-the-badge" />
</p>

---

## 📚 Table of Contents
- [Document Revision History](#-document-revision-history)
- [Executive Summary](#-executive-summary)
- [Requirements](#-requirements)
- [Design Constraints](#-design-constraints)
- [System Architecture View](#-system-architecture-view)
- [Domain Model](#-domain-model)
- [Continued Evaluation](#-continued-evaluation)
  - [Server Side](#server-side)
  - [Client Side](#client-side)
  - [Development Tools](#development-tools)
- [Final Recommendations for “Draw It or Lose It”](#-final-recommendations-for-draw-it-or-lose-it)
  - [Operating Platform](#operating-platform)
  - [Operating Systems Architectures](#operating-systems-architectures)
  - [Storage Management](#storage-management)
  - [Memory Management](#memory-management)
  - [Distributed Systems and Network](#distributed-systems-and-network)
  - [Security](#security)

---

## 📝 Document Revision History

| Version | Date       | Author            | Comments                                           |
|---------|------------|-------------------|----------------------------------------------------|
| 3.0     | 12/13/2024 | Ryan A Peguero    | Third and Final Software Design “Draw It or Lose It” |

---

## 🚀 Executive Summary

This software design document presents the proposed solution for developing **“Draw It or Lose It,”** a web-based game application for our client, **The Gaming Room**. Inspired by the classic TV game show *Win, Lose, or Draw*, this game enables teams to compete by guessing drawings.

The solution includes displaying images from a stock drawing library as clues and supporting multiple teams through four rounds of gameplay. By transitioning to a web-based platform, the game becomes accessible across many devices and operating systems, delivering a more engaging and user-friendly experience.

---

## ✅ Requirements

- The game should be accessible via a **web-based platform**, ensuring compatibility across devices and operating systems.
- Each game must support **one or more teams**, with multiple players assigned to each team.
- **Game and team names must be unique**, with validation for name availability during setup.
- The application should enforce **a single active game instance in memory** using unique IDs for games, teams, and players.
- Game rounds should include **fixed time limits** (e.g., one minute per round), with drawings gradually revealed and fully visible by the 30-second mark.
- If a team cannot solve the puzzle in time, other teams should each receive **one guess within a 15-second window**.

---

## ⚙️ Design Constraints

### 1) Web-Based Distributed Platform
The application must run on a distributed web platform, introducing challenges in networking, browser compatibility, and security.

### 2) Unique Naming Requirement
Game, team, and player names must be unique to prevent collisions and improve usability during setup and gameplay.

### 3) Single Instance Restriction
The design must ensure only one active game service instance exists in memory at a time.

---

## 🏗️ System Architecture View

> **Note:** There is nothing required in this section for this specific project.  
> However, in other projects, this section may require a full description of:
> - system/subsystem architecture,
> - physical tiers/components,
> - communication and storage topology.

---

## 🧩 Domain Model

The domain model for **Draw It or Lose It** includes the following structure:

- **Entity** is the foundational superclass containing shared attributes:
  - `id`
  - `name`
- **Game**, **Team**, and **Player** extend `Entity`.
  - A **Game** contains multiple **Teams**.
  - A **Team** contains multiple **Players**.

### Relationships
- **GameService** composes/manages `Game` objects and their lifecycle.
- **Game** composes `Team`.
- **Team** composes `Player`.

### Application Flow
- **ProgramDriver** contains the `main` method (application entry point).
- A singleton instance of **GameService** is created in `ProgramDriver`.
- `ProgramDriver` adds games, teams, and players through `GameService`.
- `ProgramDriver` depends on **SingletonTester**.

### OOP Principles Demonstrated
- **Inheritance**: `Game`, `Team`, and `Player` inherit from `Entity`.
- **Encapsulation**: data and behaviors are maintained in class boundaries.
- **Abstraction**: common behavior is centralized in the superclass.
- Use of `super` constructors minimizes duplication and keeps entities consistent.

---

## 📊 Continued Evaluation

Using platform analysis across **Linux, Mac, Windows, and Mobile**, the following characteristics, strengths, and limitations were identified.

### Server Side

| Platform | Evaluation |
|----------|------------|
| **Mac** | **Characteristics:** Unix-based, stable, secure. **Advantages:** Robust ecosystem, developer friendly. **Weaknesses:** Higher hardware costs, limited scalability compared to Linux and Windows. |
| **Linux** | **Characteristics:** Open-source, highly customizable. **Advantages:** Highly scalable, stable, secure, and provides broad access to software/tools. **Weaknesses:** GUI limitations and occasional hardware compatibility issues. |
| **Windows** | **Characteristics:** Extensive software compatibility with strong developer support. **Advantages:** Broad hardware support and comprehensive documentation. **Weaknesses:** More prone to known security vulnerabilities. |
| **Mobile Devices** | **Characteristics:** Portable, touch/gesture-based. **Advantages:** Built-in hardware features like camera, GPS, push notifications. **Weaknesses:** Smaller screens and varying hardware capabilities. |

### Client Side

| Platform | Evaluation |
|----------|------------|
| **Mac** | User-friendly interface with a low learning curve, but building/maintaining multiple clients can increase development time and cost. |
| **Linux** | Free to use/distribute; additional hardware/tooling costs may still apply. Has a steeper learning curve and may require broader platform expertise. |
| **Windows** | Strong tooling and broad compatibility, though licensing costs may exceed open-source alternatives. |
| **Mobile Devices** | Requires adaptive UI design and handling connectivity constraints; can leverage camera, GPS, and notifications for richer experiences. |

### Development Tools

| Platform | Languages & Tools | Impact |
|----------|-------------------|--------|
| **Mac** | Node.js, JavaScript, VS Code, Xcode | Developer-friendly ecosystem and popular environments. |
| **Linux** | Node.js, JavaScript, VS Code, Atom, Sublime Text, strong CLI and package managers | Comprehensive environment with excellent command-line tooling. |
| **Windows** | C#, .NET Framework, Visual Studio, JetBrains IDEs | Strong support for Windows-oriented web application development. |
| **Mobile Devices** | Kotlin, Swift, Objective-C, Java, JavaScript, Android Studio, Xcode | Requires cross-platform expertise and multiple toolchains. |

---

## 🧠 Final Recommendations for “Draw It or Lose It”

## Operating Platform

A cloud-based platform such as **Amazon Web Services (AWS)** or **Google Cloud Platform (GCP)** is recommended for scalability, flexibility, and multi-OS support.

### Why AWS/GCP?
- Supports Linux distributions and Windows Server.
- Pay-as-you-go pricing reduces upfront costs.
- Reserved/savings plans can reduce predictable workload costs.
- Provides robust security controls (encryption, IAM, network firewalls).
- Integrates with common IDEs and CI/CD pipelines to accelerate delivery.

---

## Operating Systems Architectures

A **Linux-based architecture** is recommended.

### Benefits
- Open-source licensing lowers cost.
- High reliability/stability for strong uptime.
- LTS distributions ensure long-term updates/support.
- Large community support for troubleshooting and innovation.
- Strong concurrency and CPU efficiency for multiplayer scale.

### Architectural Fit
A **microservices approach** is recommended:
- Services (auth, game logic, leaderboard, etc.) are independently deployable.
- Teams can iterate in parallel with lower deployment risk.
- Individual services scale independently based on traffic.
- Fault isolation and maintenance are simpler than monolithic designs.

---

## Storage Management

A hybrid storage strategy is recommended:

### Relational Databases (MySQL/PostgreSQL)
Best for structured data:
- User accounts
- Scores
- Transactions
- Game state with strict integrity needs

Benefits:
- ACID compliance
- Complex querying and joins
- Strong consistency guarantees

### NoSQL / Document Stores (e.g., MongoDB)
Best for unstructured/semi-structured data:
- Chat logs
- Event streams
- Dynamic content models

Benefits:
- Flexible schema evolution
- Rapid iteration
- Efficient handling of variable data structures

### Object Storage (AWS S3 / Google Cloud Storage)
Best for large binary assets:
- Images
- Videos
- Audio
- User-generated game content

Benefits:
- Durable cloud storage
- Tiered lifecycle cost optimization

---

## Memory Management

Efficient memory design is critical for game performance and reliability.

### Recommended Practices
- Use **virtual memory** to extend effective RAM via disk paging.
- Isolate processes by virtual address space for better stability/security.
- Support multitasking for concurrent game operations.
- Use paging/swapping strategies to optimize runtime usage.

### Managed Runtime Advantages
With languages like Java/C#:
- Built-in garbage collection reduces memory leaks.
- Generational and concurrent collection minimize pause times.
- Better long-term performance stability under sustained load.

### Caching Benefits
- Reduces database load for repeated requests.
- Improves response times through in-memory access.
- Enhances gameplay smoothness and perceived responsiveness.

---

## Distributed Systems and Network

A containerized, orchestrated deployment model is recommended.

### Core Components
- **Docker** for packaging services consistently.
- **Kubernetes** for orchestration, scaling, and operations.
- **REST/gRPC** for inter-service communication.
- **Load balancing** for traffic distribution and high availability.
- **Failover mechanisms** for resilience during outages.
- **Service discovery** for dynamic microservice dependency management.

This model supports high scalability, operational consistency, and reliable network behavior.

---

## Security

A layered security approach is recommended to protect users and platform integrity.

### Key Controls
- **Encryption in transit and at rest** (TLS/SSL + platform encryption).
- **OAuth 2.0** for secure authentication.
- **RBAC** for role-based authorization and least privilege.
- **Regular audits and vulnerability scans** to identify and fix threats early.
- Cloud-native defenses:
  - IAM policies
  - Network firewalls
  - Intrusion detection and monitoring

By combining these controls, The Gaming Room can scale confidently while maintaining strong protection of user data and system trust.

---

## 🎯 Closing Note

This design supports The Gaming Room’s goals for:
- cross-platform accessibility,
- scalable architecture,
- maintainable services,
- reliable performance,
- and robust security.

The result is a practical, future-ready foundation for **Draw It or Lose It**.

---
```
