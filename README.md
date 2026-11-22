# Ramesh Yara — Senior Software Engineer & Platform Architect

<p align="left">
  <img src="https://img.shields.io/badge/Platform%20Architect%20%7C%20Java%20%C2%B7%20Cloud--Native%20%C2%B7%20Distributed%20Systems%20%7C%2012%2B%20Years-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Location-Burbank,%20CA-orange?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Writing-Medium%20%7C%20Dev.to%20%7C%20DZone-green?style=for-the-badge" />
</p>

---

### 👋 About Me

I build **event-driven, cloud-native systems** that are observable from day one — not as an afterthought. My engineering focus sits at the intersection of distributed systems reliability, production-grade observability, and platform engineering.

- 🏗️ **Patterns I implement at depth:** Transactional Outbox, Idempotent Consumer with race-condition hardening, multi-window SLO burn-rate alerting, circuit breakers, and distributed tracing across async Kafka boundaries — verified by deliberate failure injection, not assumed.
- 🔭 **Observability-first:** I instrument systems so failure modes are caught before users see them. I've closed blind spots that generic monitoring misses (client-side consumer lag decaying to NaN; terminal-FAILED outbox events with no alert; Schema Registry cold-start races).
- ⚡ **Platform foundation:** Java 21 + Virtual Threads, Spring Boot 4, Kafka KRaft, AWS EKS, Terraform, ArgoCD GitOps (app-of-apps + sync waves), Chaos Engineering (Chaos Mesh), Spring AI + Ollama enrichment pipeline, full in-cluster observability (OpenTelemetry → Tempo, Prometheus, Loki).

---

### ⚡ Currently Building

**[`ai-microservices-platform`](https://github.com/Rummy43/ai-microservices-platform)** — A production-grade, cloud-native, event-driven microservices platform deployed on **AWS EKS** with GitOps delivery via ArgoCD, Chaos Engineering validation via Chaos Mesh, and a complete in-cluster observability stack. Phase 11 (ArgoCD + Chaos Engineering on EKS) complete; Phase 12 is next.

---

### 🏗️ Featured Project — ai-microservices-platform

> **The measure of a monitoring stack is whether it catches failures you didn't plan for.** This project verifies every alert with deliberate injection — and the exit gate found a real unplanned failure on its first run.

A portfolio platform built to production standards: three microservices (user-service, notification-service, api-gateway), Kafka event backbone, Keycloak IAM, Spring AI + Ollama enrichment pipeline, and a full observability stack deployed on **AWS EKS** via GitOps (ArgoCD) with Chaos Engineering validation.

**Distributed systems patterns implemented:**
- **Transactional Outbox** (`PENDING → PROCESSING → PUBLISHED`) — outbox row and entity committed in the same transaction; scheduled publisher fans out to Kafka; survives gateway circuit breaker timeouts
- **Idempotent Consumer** — application-layer check + database unique constraint as final race-condition arbiter; `DataIntegrityViolationException` suppresses duplicate side effects
- **Circuit Breaker** (Resilience4j) — at the gateway layer; tested under cold JVM + WSL2 contention; outbox guarantees no event loss even when CB opens
- **GitOps Delivery** (ArgoCD app-of-apps, sync waves) — multi-source Helm with `$values` refs; ServerSideApply=true for 262KB CRD annotation limit; automated self-healing verified in EKS
- **Chaos Engineering** (Chaos Mesh) — network delay, pod kill, CPU stress injected against live EKS workloads; alert SLOs verified under fault conditions
- **SLO burn-rate alerting** (multi-window: 5m / 30m / 1h / 6h) — 10 platform alert rules + 5 recording rules; broker-side consumer lag via `kafka-exporter` closed the client-side `records_lag_max → NaN` blind spot
- **Keycloak realm-as-code** (`--import-realm` from ConfigMap) — verified by live realm-loss injection in-cluster; risk fired, closed permanently

**Observability stack (AWS EKS):**
`OpenTelemetry Java agent 2.28.1` → `Grafana Tempo 2.9.0` (distributed traces across HTTP + async Kafka)
`Promtail 3.5.1` → `Loki 3.6.11` (structured JSON logs with `traceId` injection, bidirectional Tempo↔Loki correlation)
`Prometheus` (kube-prometheus-stack) → `Alertmanager` → runbook links per alert
`kafka-exporter v1.7.0` — broker-side consumer lag metric (`kafka_consumergroup_lag`) that survives consumer process death

**Exit gate result:** failure injection in EKS → `OutboxPublishTerminalFailure` fired (`severity: page`, `slo: outbox_integrity`) → Alertmanager delivered → condition cleared → auto-resolved in 30 seconds. The alert caught a real unplanned failure on its first in-cluster run.

**Stack:** `Java 21` · `Spring Boot 4` · `Virtual Threads` · `Kafka KRaft` · `AWS EKS` · `Terraform` · `ArgoCD` · `Helm` · `Chaos Mesh` · `Spring AI` · `Ollama` · `Kubernetes` · `Kustomize` · `OpenTelemetry` · `Grafana Tempo` · `Loki` · `Prometheus` · `Alertmanager` · `Keycloak` · `Resilience4j` · `Avro` · `Schema Registry` · `MySQL` · `PostgreSQL` · `Liquibase` · `Flyway`

---

### 🧰 Tech Arsenal

#### Distributed Systems & Backend
![Java](https://img.shields.io/badge/Java%2021-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot%204-%236DB33F.svg?style=for-the-badge&logo=spring&logoColor=white)
![Spring AI](https://img.shields.io/badge/Spring%20AI-6DB33F?style=for-the-badge&logo=spring&logoColor=white)
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

#### Cloud, Infrastructure & GitOps
![AWS](https://img.shields.io/badge/AWS%20EKS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-%235835CC.svg?style=for-the-badge&logo=terraform&logoColor=white)
![ArgoCD](https://img.shields.io/badge/ArgoCD-EF7B4D?style=for-the-badge&logo=argo&logoColor=white)
![Helm](https://img.shields.io/badge/Helm-0F1689?style=for-the-badge&logo=helm&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-%23326ce5.svg?style=for-the-badge&logo=kubernetes&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Azure](https://img.shields.io/badge/Azure-%230072C6.svg?style=for-the-badge&logo=microsoft-azure&logoColor=white)
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
| 🏅 **Tech Debt Slayer Award — Warner Bros. Discovery** | Recognized for eliminating critical architectural debt that reduced system fragility across a core distributed platform (Dec 2025). |
| 📈 **Scale** | Designed and maintained systems processing **500K+ events/day**, serving **10K+ daily active users** across distributed microservices. |
| ⚡ **Latency** | Consistently achieved **30–40% p99 latency reductions** through Virtual Thread adoption, connection pool tuning, and async pipeline optimization. |
| 💰 **Cost** | Saved **~$20K/year** in cloud infrastructure spend via autoscaling policy redesign and right-sizing. |

---

### ✍️ Writing — Distributed Systems & Observability

I write about real failure modes — not idealized architectures. Most articles start from a production blind spot I found by actually running the system under failure conditions.

| | |
|---|---|
| 📄 [**I Deleted kubectl apply From My Workflow. Here's What Replaced It.**](https://medium.com/@yara.ramesh/i-deleted-kubectl-apply-from-my-workflow-heres-what-replaced-it-b5e3090e84ec) · *Medium + Dev.to* | ArgoCD app-of-apps, sync waves, multi-source Helm, and the 262KB CRD annotation limit that breaks naive GitOps. |
| 📄 [**Your Service Map Is Lying: Verifying OTel Auto-Instrumentation**](https://medium.com/@yara.ramesh/your-service-map-is-lying-cfc84fb38990) · *Medium* | Why auto-instrumentation is a claim, not a guarantee — and how to verify it against live spans. |
| 📄 [**Who Did This? Identity Propagation Across Async Boundaries**](https://medium.com/@yara.ramesh/who-did-this-identity-across-async-boundaries-823c712b073f) · *Medium* | How actor context survives Kafka hops, retries, and dead letter routing without leaking through thread locals. |
| 📄 **The Outbox Pattern Is Not Enough** · *Published — Medium* | The 4 ev/s config-line ceiling, 720-row burst suppression, and why your SLOs need to know the difference. |
| 📄 **Three Ways Your Alerts Go Blind** · *Submitted — DZone* | The decay / vanish / unqueried-terminal blind-spot taxonomy with live injection evidence. |

10+ articles published across **Medium**, **Dev.to**, and **DZone** (2,000+ views) — covering event-driven architecture, distributed tracing, Kubernetes observability, GitOps patterns, and chaos engineering.

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
<a href="https://sessionize.com/ramesh-yara/" target="_blank">
  <img src="https://img.shields.io/badge/Sessionize-1AB394?style=for-the-badge&logo=sessionize&logoColor=white" alt="Sessionize">
</a>
</p>
