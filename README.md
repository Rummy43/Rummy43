# Ramesh Yara — Senior Java Full-Stack Engineer

<p align="left">
  <img src="https://img.shields.io/badge/Senior%20Software%20Engineer%20%26%20Architect%20%7C%20Java%20%C2%B7%20Full--Stack%20%C2%B7%20Distributed%20Systems%20%7C%2012%2B%20Years-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Location-Burbank,%20CA-orange?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Writing-Medium%20%7C%20Dev.to%20%7C%20InfoQ-green?style=for-the-badge" />
</p>

---

### 👋 About Me

I build **event-driven, cloud-native systems** that are observable from day one — not as an afterthought. My engineering focus sits at the intersection of distributed systems reliability, production-grade observability, and platform engineering.

- 🏗️ **Patterns I implement at depth:** Transactional Outbox, Idempotent Consumer with race-condition hardening, multi-window SLO burn-rate alerting, circuit breakers, and distributed tracing across async Kafka boundaries — verified by deliberate failure injection, not assumed.
- 🔭 **Observability-first:** I instrument systems so failure modes are caught before users see them. I've closed blind spots that generic monitoring misses (client-side consumer lag decaying to NaN; terminal-FAILED outbox events with no alert; Schema Registry cold-start races).
- ⚡ **Platform foundation:** Java 21 + Virtual Threads, Spring Boot 4, Kafka KRaft, Kubernetes (Kustomize + kind), full in-cluster observability (OpenTelemetry → Tempo, Prometheus, Loki). Angular 20 + Signals on the frontend when the project calls for it.

---

### ⚡ Currently Building

**[`ai-microservices-platform`](https://github.com/Rummy43/ai-microservices-platform)** — A production-grade, cloud-native, event-driven microservices platform running fully in Kubernetes with a complete in-cluster observability stack. Phase 8 (K8s observability) just closed; Phase 9 adds Spring AI and traced LLM calls next.

---

### 🏗️ Featured Project — ai-microservices-platform

> **The measure of a monitoring stack is whether it catches failures you didn't plan for.** This project verifies every alert with deliberate injection — and the exit gate found a real unplanned failure on its first run.

A portfolio platform built to production standards: three microservices (user-service, notification-service, api-gateway), Kafka event backbone, Keycloak IAM, and a full observability stack all running in a local Kubernetes cluster.

**Distributed systems patterns implemented:**
- **Transactional Outbox** (`PENDING → PROCESSING → PUBLISHED`) — outbox row and entity committed in the same transaction; scheduled publisher fans out to Kafka; survives gateway circuit breaker timeouts
- **Idempotent Consumer** — application-layer check + database unique constraint as final race-condition arbiter; `DataIntegrityViolationException` suppresses duplicate side effects
- **Circuit Breaker** (Resilience4j) — at the gateway layer; tested under cold JVM + WSL2 contention; outbox guarantees no event loss even when CB opens
- **SLO burn-rate alerting** (multi-window: 5m / 30m / 1h / 6h) — 10 platform alert rules + 5 recording rules; broker-side consumer lag via `kafka-exporter` closed the client-side `records_lag_max → NaN` blind spot
- **Keycloak realm-as-code** (`--import-realm` from ConfigMap) — verified by live realm-loss injection in-cluster; risk fired, closed permanently

**Observability stack (all in-cluster):**
`OpenTelemetry Java agent 2.28.1` → `Grafana Tempo 2.9.0` (distributed traces across HTTP + async Kafka)
`Promtail 3.5.1` → `Loki 3.6.11` (structured JSON logs with `traceId` injection, bidirectional Tempo↔Loki correlation)
`Prometheus` (kube-prometheus-stack) → `Alertmanager` → runbook links per alert
`kafka-exporter v1.7.0` — broker-side consumer lag metric (`kafka_consumergroup_lag`) that survives consumer process death

**Exit gate result:** failure injection in Kubernetes → `OutboxPublishTerminalFailure` fired (`severity: page`, `slo: outbox_integrity`) → Alertmanager delivered → condition cleared → auto-resolved in 30 seconds. The alert caught a real unplanned failure on its first in-cluster run.

**Stack:** `Java 21` · `Spring Boot 4` · `Virtual Threads` · `Kafka KRaft` · `Kubernetes` · `Kustomize` · `OpenTelemetry` · `Grafana Tempo` · `Loki` · `Prometheus` · `Alertmanager` · `Keycloak` · `Resilience4j` · `Avro` · `Schema Registry` · `MySQL` · `PostgreSQL` · `Liquibase` · `Flyway`

---

### 🧰 Tech Arsenal

#### Distributed Systems & Backend
![Java](https://img.shields.io/badge/Java%2021-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot%204-%236DB33F.svg?style=for-the-badge&logo=spring&logoColor=white)
![Kafka](https://img.shields.io/badge/Apache%20Kafka-%2320232a.svg?style=for-the-badge&logo=apache-kafka&logoColor=white)
![Avro](https://img.shields.io/badge/Avro%20%7C%20Schema%20Registry-E6522C?style=for-the-badge&logoColor=white)
![Resilience4j](https://img.shields.io/badge/Resilience4j-6DB33F?style=for-the-badge&logoColor=white)
![GraphQL](https://img.shields.io/badge/GraphQL-E10098?style=for-the-badge&logo=graphql&logoColor=white)
![JUnit5](https://img.shields.io/badge/JUnit5-25A162?style=for-the-badge&logo=junit5&logoColor=white)

#### Observability & Platform Engineering
![OpenTelemetry](https://img.shields.io/badge/OpenTelemetry-425CC7?style=for-the-badge&logo=opentelemetry&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-%23F46800.svg?style=for-the-badge&logo=grafana&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=Prometheus&logoColor=white)
![Grafana Tempo](https://img.shields.io/badge/Grafana%20Tempo-F46800?style=for-the-badge&logo=grafana&logoColor=white)
![Loki](https://img.shields.io/badge/Grafana%20Loki-F46800?style=for-the-badge&logo=grafana&logoColor=white)
![Micrometer](https://img.shields.io/badge/Micrometer-1BA3C6?style=for-the-badge&logoColor=white)

#### Cloud & Infrastructure
![Kubernetes](https://img.shields.io/badge/Kubernetes-%23326ce5.svg?style=for-the-badge&logo=kubernetes&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Azure](https://img.shields.io/badge/Azure-%230072C6.svg?style=for-the-badge&logo=microsoft-azure&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-%235835CC.svg?style=for-the-badge&logo=terraform&logoColor=white)
![Keycloak](https://img.shields.io/badge/Keycloak-4D4D4D?style=for-the-badge&logo=keycloak&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-%23D24939.svg?style=for-the-badge&logo=jenkins&logoColor=white)

#### Databases
![MySQL](https://img.shields.io/badge/MySQL-%2300f.svg?style=for-the-badge&logo=mysql&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-%23336791.svg?style=for-the-badge&logo=postgresql&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-%234ea94b.svg?style=for-the-badge&logo=mongodb&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-%23DD0031.svg?style=for-the-badge&logo=redis&logoColor=white)

#### Frontend
![Angular](https://img.shields.io/badge/Angular%2020-%23DD0031.svg?style=for-the-badge&logo=angular&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-%23007ACC.svg?style=for-the-badge&logo=typescript&logoColor=white)
![React](https://img.shields.io/badge/React-%2320232a.svg?style=for-the-badge&logo=react&logoColor=61DAFB)
![TailwindCSS](https://img.shields.io/badge/TailwindCSS-%2338B2AC.svg?style=for-the-badge&logo=tailwind-css&logoColor=white)

---

### 🏆 Recognition & Impact

| | |
|---|---|
| 🥇 **Championship Award — Wells Fargo** | Delivered a high-stakes enterprise migration under tight regulatory deadlines; zero production incidents post-launch. |
| 🚀 **Hi-Flyer Award — HighRadius** | Led cross-functional innovation sprint that shipped a net-new product feature in under 6 weeks. |
| 📈 **Scale** | Designed and maintained systems processing **500K+ events/day**, serving **10K+ daily active users** across distributed microservices. |
| ⚡ **Latency** | Consistently achieved **30–40% p99 latency reductions** through Virtual Thread adoption, connection pool tuning, and async pipeline optimization. |
| 💰 **Cost** | Saved **~$20K/year** in cloud infrastructure spend via autoscaling policy redesign and right-sizing. |

---

### ✍️ Writing — Distributed Systems & Observability

I write about real failure modes — not idealized architectures. Most articles start from a production blind spot I found by actually running the system under failure conditions.

| | |
|---|---|
| 📄 [**Your Service Map Is Lying: Verifying OTel Auto-Instrumentation**](https://medium.com/@yara.ramesh/your-service-map-is-lying-cfc84fb38990) | Why auto-instrumentation is a claim, not a guarantee — and how to verify it against live spans. |
| 📄 [**Who Did This? Identity Propagation Across Async Boundaries**](https://medium.com/@yara.ramesh/who-did-this-identity-across-async-boundaries-823c712b073f) | How actor context survives Kafka hops, retries, and dead letter routing without leaking through thread locals. |
| 📄 **The Outbox Pattern Is Not Enough** *(upcoming — ITNEXT)* | The 4 ev/s config-line ceiling, 720-row burst suppression, and why your SLOs need to know the difference. |
| 📄 **Three Ways Your Alerts Go Blind** *(submitted — InfoQ Java queue)* | The decay / vanish / unqueried-terminal blind-spot taxonomy with live injection evidence. |

More on [Medium](https://medium.com/@yara.ramesh) · [Dev.to](https://dev.to/ramesh-yara)

---

### 📊 GitHub Activity

<p align="left">
<img height="180em" src="https://github-readme-stats.vercel.app/api?username=Rummy43&show_icons=true&theme=tokyonight&include_all_commits=true" alt="GitHub Stats"/>
<img height="180em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=Rummy43&layout=compact&theme=tokyonight" alt="Top Languages"/>
</p>

---

### 📫 Let's Connect

<p align="left">
<a href="https://www.linkedin.com/in/ramesh-yara/" target="_blank">
  <img src="https://img.shields.io/badge/LinkedIn-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn">
</a>
<a href="https://medium.com/@yara.ramesh" target="_blank">
  <img src="https://img.shields.io/badge/Medium-12100E?style=for-the-badge&logo=medium&logoColor=white" alt="Medium">
</a>
<a href="https://dev.to/ramesh-yara" target="_blank">
  <img src="https://img.shields.io/badge/Dev.to-0A0A0A?style=for-the-badge&logo=devdotto&logoColor=white" alt="Dev.to">
</a>
</p>
