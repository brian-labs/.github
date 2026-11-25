# Brian Labs

An independent engineering workspace by [Brian Muigai](https://github.com/BrianGMuigai) for backend systems and the developer tooling around them. The work here centres on data integrity under concurrency, explicit failure handling and relational designs that are easy to maintain and change.

## Engineering standards

The practices each project here is built to:

- **Data-first modelling:** normalised relational schemas, composite indexes tuned from execution plans, and forward-only Flyway migrations on PostgreSQL and SQL Server
- **Concurrency and transaction boundaries:** deliberate isolation levels, with row-level locking (`SELECT ... FOR UPDATE` on PostgreSQL, `UPDLOCK` on SQL Server) on check-then-write paths
- **Predictable API contracts:** Spring Boot REST services with validation at the boundary, cursor-based pagination, idempotent operations where retries are likely, and one centralised error mapping
- **Asynchronous work and caching:** event-driven workflows on Kafka, with Redis where read latency matters and the relational database as the source of truth
- **Automated verification and delivery:** JUnit and Mockito tests, multi-stage Docker builds, and GitHub Actions CI on every pull request

### Reference architecture

```text
Client / Ingestion ──► API boundary (validation and auth)
                             │
             ┌───────────────┴───────────────┐
             ▼                               ▼
     Kafka event stream              Spring Boot domain layer
     (async workers)                 (explicit transaction boundaries)
                                             │
                             ┌───────────────┴───────────────┐
                             ▼                               ▼
                     Redis hot cache                 PostgreSQL (ACID)
                                                     (Flyway migrations, row locks)
```

## Core stack

![Java](https://img.shields.io/badge/Java-ED8B00?style=flat&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat&logo=springboot&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=flat&logo=postgresql&logoColor=white)
![SQL Server](https://img.shields.io/badge/SQL_Server-CC2927?style=flat&logo=microsoftsqlserver&logoColor=white)
![Flyway](https://img.shields.io/badge/Flyway-CC0200?style=flat&logo=flyway&logoColor=white)
![Kafka](https://img.shields.io/badge/Kafka-231F20?style=flat&logo=apachekafka&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DD0031?style=flat&logo=redis&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-0db7ed?style=flat&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2671E5?style=flat&logo=githubactions&logoColor=white)
![Python](https://img.shields.io/badge/Python-3670A0?style=flat&logo=python&logoColor=ffdd54)

## Active systems

### [Hospital Management System](https://github.com/brian-labs/Hospital-System)

**Status:** in development · **Stack:** Java, Spring Boot, PostgreSQL, Flyway

A hospital backend on a 52-table relational PostgreSQL schema covering clinical workflows, pharmacy, laboratory operations, billing and HR. The design separates the rules the database enforces from the rules the service layer enforces, uses row-level locking for concurrency-sensitive operations, and ships schema changes as forward-only Flyway migrations. Individual project.

## Contact

For backend engineering roles, architecture discussions or collaboration:

- **Maintainer:** [Brian Muigai (@BrianGMuigai)](https://github.com/BrianGMuigai)
- **LinkedIn:** [linkedin.com/in/brian-muigai](https://www.linkedin.com/in/brian-muigai/)
- **Portfolio:** [brianmuigai.vercel.app](https://brianmuigai.vercel.app/)
- **Email:** [brianmuigai40@gmail.com](mailto:brianmuigai40@gmail.com)
