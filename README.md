<div align="center" width="full">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=28&duration=2500&pause=800&color=00D9FF&center=true&vCenter=true&width=700&lines=Hey%2C+I'm+Vivek+%F0%9F%91%8B;Backend+%26+Distributed+Systems+Engineer;Java+%7C+Spring+Boot+%7C+Apache+Kafka" alt="Typing SVG" />
<h3 align="center">Specialized in backend systems engineering, distributed architectures, and performance-critical applications Proven track record architecting scalable microservices, Building Systems That Stay Correct Under Load, and optimizing production systems</h3>
<br/>

[![LinkedIn](https://img.shields.io/badge/LinkedIn-vivek--mane-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/vivek-mane)
[![Email](https://img.shields.io/badge/Email-vivekmane9860@gmail.com-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:vivekmane9860@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-vivek--9941-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/vivek-9941)

</div>

---

## 🧠 Who I Am

I'm a **Backend Systems Engineer** specializing in distributed architectures, event-driven systems, and performance-critical applications.

> I don't build CRUD apps. I build **systems that behave correctly under load, failure, and concurrency.**

My focus areas:
- **Distributed architectures** — microservices, service meshes, data consistency
- **Event-driven systems** — Kafka-based async pipelines, exactly-once semantics
- **Concurrency & orchestration** — DAG execution, parallel task scheduling
- **Production-grade reliability** — circuit breakers, retries, DLQ, self-healing

---

## 🔥 Featured Projects

> Ranked by engineering complexity and system depth

---

### 🥇 Low-Latency Trade Order Orchestration Engine
#### *DAG-Based Distributed Execution System with Concurrency Control*

> A distributed orchestration engine that models how **real-world trading systems safely execute orders** under strict latency and correctness constraints.
>
> ⚠️ This is not a trading UI — it is a **control plane ensuring safe execution under concurrency.**

**The Core Problem:**
A trade is not a single operation. Before execution, it must pass risk validation, margin checks, and compliance rules — all **in parallel**, **within strict latency bounds**, and with **consistency under failure**.

```
[ Order Received ]
       │
       ▼
┌─────────────────────────────────────────────┐
│           Pre-Trade (Sync, gRPC)            │
│  Risk Check ──┬── Margin Check ──┬── KYC   │
│               └──── Compliance ──┘          │
└──────────────────────┬──────────────────────┘
                       │ All pass?
                       ▼
┌─────────────────────────────────────────────┐
│       Orchestration Layer (DAG Engine)      │
│   CompletableFuture.allOf() + Retry/CB      │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│         In-Memory Matching Engine           │
│    Price-time priority + Partial fills      │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│      Post-Trade (Async, Kafka)              │
│  Ledger ─── Notifications ─── Analytics    │
└─────────────────────────────────────────────┘
```

| Engineering Concern | Implementation |
|---|---|
| **Parallel Validation** | gRPC + `CompletableFuture.allOf()` |
| **Failure Resilience** | Retries + Circuit Breakers + DLQ |
| **Exactly-Once** | Atomic DB + Kafka offset coordination |
| **State Machine** | Explicit order lifecycle transitions |
| **Async Decoupling** | Kafka-based post-trade pipeline |

**Stack:** `Java` `Spring Boot` `Apache Kafka` `gRPC` `Redis` `PostgreSQL`

---

### 🥈 Distributed CI/CD Workflow Execution Engine
#### *DAG-Based Orchestration Inspired by Apache Airflow & Netflix Conductor*

> Workflows are **not hardcoded pipelines** — they are defined as DAGs and executed dynamically across a distributed worker pool.

```
  [ Workflow Definition (DAG) ]
           │
     ┌─────▼─────┐
     │  Scheduler │  ← Topological dependency resolution
     └─────┬─────┘
           │
    ┌──────▼──────┐
    │  Kafka Bus  │  ← Decouples orchestration from execution
    └──────┬──────┘
           │
  ┌────────▼────────┐
  │  Worker Pool    │  ← Horizontally scalable via K8s HPA
  │ (Consumer Lag)  │
  └────────┬────────┘
           │ Task fails?
    ┌──────▼──────┐
    │  Retry →    │
    │  DLQ →      │  ← Self-healing fallback chain
    │  Alert      │
    └─────────────┘
```

| Engineering Depth | Detail |
|---|---|
| **DAG Scheduling** | Topological sort → dependency-aware execution |
| **Event-Driven Core** | Kafka decouples orchestration from execution |
| **Exactly-Once** | Atomic DB writes + Kafka offset commit |
| **Self-Healing** | Failed task detection → retry → DLQ fallback |
| **Horizontal Scaling** | Kubernetes HPA scales on consumer lag |

**Stack:** `Java` `Spring Boot` `Apache Kafka` `Kubernetes` `Docker` `PostgreSQL` `Prometheus` `Grafana`

---

### 🥉 Centralized KYC System
#### *Consent-Driven Distributed Identity Platform*

> A microservices-based KYC orchestration system that **eliminates redundant verification across institutions** while enforcing secure, consent-based data access.

**The Model:**
```
  Institution A ──┐
  Institution B ──┼──► [ KYC Service ] ──► [ Single Source of Truth ]
  Institution C ──┘          │
                              │  Consent Gate
                         ┌────▼─────┐
                         │  User    │  ← Explicit authorization required
                         └──────────┘
```

| Design Principle | Implementation |
|---|---|
| **Single Source of Truth** | One verified identity, reusable across orgs |
| **Consent as First-Class Primitive** | No access without explicit user authorization |
| **Event-Driven** | Async service communication via Apache Kafka |
| **Security-First** | JWT + RBAC + encrypted storage |
| **Lifecycle Automation** | KYC renewal, revocation, and updates via workflows |

> This system models **trust boundaries** and enforces **controlled data propagation** — it's a data governance system, not just a backend.

**Stack:** `Java` `Spring Boot` `Spring Security` `Apache Kafka` `MySQL` `Redis` `Docker`

---

### 🏅 Coding Analytics Dashboard
#### *Multi-Platform Data Aggregation & Insight Engine*

> A full-stack system that collects, normalizes, and analyzes competitive programming data across multiple platforms — with an **insight layer, not just charts**.

| Feature | Detail |
|---|---|
| **Multi-Source Ingestion** | REST + GraphQL pipelines across platforms |
| **Insight Layer** | Weakness detection, tag mastery, performance trends |
| **Caching Strategy** | 24-hour intelligent frontend cache to reduce API pressure |
| **Scheduled Pipelines** | Backend jobs continuously refresh analytics |
| **Auth** | OAuth 2.0 + JWT secure flow |

**Stack:** `Java` `Spring Boot` `React.js` `Tailwind CSS` `Recharts` `MySQL` `Redis`

---

## 🛠️ Tech Stack

<div align="center">

### Backend
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)
![Spring Security](https://img.shields.io/badge/Spring_Security-6DB33F?style=for-the-badge&logo=spring-security&logoColor=white)

### Messaging & Data
![Apache Kafka](https://img.shields.io/badge/Apache_Kafka-231F20?style=for-the-badge&logo=apache-kafka&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)

### Infrastructure & Observability
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=prometheus&logoColor=white)

### Frontend
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)

### APIs & Protocols
![GraphQL](https://img.shields.io/badge/GraphQL-E10098?style=for-the-badge&logo=graphql&logoColor=white)
![gRPC](https://img.shields.io/badge/gRPC-4285F4?style=for-the-badge&logo=google&logoColor=white)

</div>

---

## 🧩 Engineering Principles

```
  Design for failure, not success
  ─────────────────────────────────────────────────────────
  Decouple everything that can scale independently
  ─────────────────────────────────────────────────────────
  Prefer async over blocking when correctness allows
  ─────────────────────────────────────────────────────────
  Make state transitions explicit and traceable
  ─────────────────────────────────────────────────────────
  Measure everything — latency, retries, failures
```

---

## 📈 GitHub Activity

<div align="center">

<img src="https://streak-stats.demolab.com?user=vivek-9941&theme=tokyonight&hide_border=true" height="170"/>

<br/>

<img src="https://github-readme-activity-graph.vercel.app/graph?username=vivek-9941&theme=tokyo-night&hide_border=true" />

</div>

---

<div align="center">

<img src="https://komarev.com/ghpvc/?username=vivek-9941&label=Profile+Views&color=00D9FF&style=for-the-badge" alt="profile views" />

*Building execution engines that remain correct under concurrency, failure, and scale.*

</div>
