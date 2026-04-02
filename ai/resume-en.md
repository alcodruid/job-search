# Resume

## Alexey Zhuykov

**Saint Petersburg, Russia** · Remote · +7 (921) 946-85-35 · alexey.zhuykov@gmail.com  
**GitHub:** github.com/alcodruid · **Website:** cyberdub.su · **LinkedIn:** linkedin.com/in/alexeyzhuykov

---

## Target Role

Senior AI Engineer · LLM Infrastructure Engineer · MLOps Engineer · Head of AI

---

## Summary

AI practitioner with production LLM infrastructure running 24/7. I build, deploy, and operate AI systems — not just prototype them. My home GPU server (NVIDIA Tesla P40) runs multiple open-source LLMs (Qwen 32B, Devstral 24B, Llava), Qdrant vector database, and n8n automation pipelines. Shipped 6+ AI-powered products. Specialization: **private LLM deployment for enterprise** — models run on client hardware, data never leaves the perimeter.

19 years as CEO of a telecom operator means I understand enterprise requirements deeply: reliability, SLAs, compliance, team ownership, and sustainable architecture.

---

## Technical Skills

**LLM & Inference:**
Ollama, vLLM, Hugging Face (transformers, PEFT, LoRA), qwen2.5:32b, devstral:24b, qwen3-coder:30b, llava, Prompt Engineering, RAG pipelines, Agentic systems, Tool use / Function calling

**Vector Databases:**
Qdrant (production, multi-collection), bge-m3 (1024-dim), nomic-embed-text (768-dim), mxbai-embed-large, semantic search, hybrid search

**Automation & Orchestration:**
n8n (complex multi-step workflows, webhook integrations, Telegram/HTTP nodes), Python (FastAPI, asyncio, httpx, SQLAlchemy), Telegram Bot API (PTB 20+)

**Infrastructure:**
Docker, Docker Compose, Caddy (reverse proxy, TLS), Linux (Ubuntu Server 24.04), Bash scripting, PostgreSQL, Redis, GitHub Actions

**Monitoring:**
Netdata, Prometheus, Grafana, Uptime Kuma

**GPU Hardware:**
NVIDIA Tesla P40 24GB, CUDA, GPU memory management for multi-model serving

---

## Projects

### Replyo — AI-Powered CRM
Business CRM with RAG core: trains on company knowledge base, classifies inquiries, generates contextual responses, integrates with Telegram.  
**Stack:** qwen2.5:32b (main), qwen2.5:7b (fast classifier), nomic-embed-text, Qdrant, n8n, Python/TypeScript, Docker  
**Highlights:** Multi-tenant knowledge base, conversation memory, automated response suggestions

### TelecomExpert.ru — Materials Marketplace for Telecom Operators
**Status:** In development · telecomexpert.ru

A marketplace of regulatory documents, contract templates, and operational materials for small Russian telecom operators. Search powered by a RAG pipeline with LLM-generated answers.

**Platform capabilities:**
- Library of regulatory docs, contract templates, and technical conditions
- SORM/TSPU compliance guides, RKN/FAS/Rossvyaz interaction manuals
- AI-powered search: ask a question — get an answer with source citation
- Open marketplace: operators can join and contribute to the knowledge base

**Stack:** bge-m3 (1024-dim), Qdrant, qwen2.5:32b, FastAPI, Python, Docker

**Invitation:** Running a telecom operator? Join us → telecomexpert.ru

### Job Matcher — AI Job Search Assistant
Telegram bot with LLM core: resume analysis, job matching, resume adaptation for specific positions, interview preparation coaching.  
**Stack:** qwen2.5:32b, Python, PTB 22.7, PostgreSQL  
**Highlights:** Multi-step conversation flow, structured output parsing, HH.ru integration

### FinPulse — AI Financial News Digest
Automated aggregation from Telegram channels → LLM analysis → structured digest delivered twice daily.  
**Stack:** n8n, qwen2.5:32b, Telegram Bot API, Python  
**Highlights:** Multi-source aggregation, topic extraction, editorial formatting

### SNT-Pilot — AI-Assisted HOA Management
Mobile app + backend for homeowners associations: property tracking, automated complaint system, multi-channel notifications.  
**Stack:** React Native, FastAPI, PostgreSQL, qwen2.5:32b for AI assistant  
**Highlights:** Offline-capable mobile app, AI-generated complaint letters

### AI-CFO — Financial Analysis AI Platform
AI tools marketplace for CFOs: financial report analysis, forecasting, presentation generation.  
**Stack:** qwen2.5:32b, Qdrant RAG, n8n, React, FastAPI

---

## Experience

### CEO & AI/DevOps Practitioner
**JSC TELSI** · Saint Petersburg · *2007–2026 (19 years)*

While running a telecom operator, independently built and operated all server infrastructure. Led DevOps modernization and deployed first AI tooling into operations.

- Migrated all services to Docker/Docker Compose (zero-downtime)
- Built monitoring stack: Prometheus + Grafana + Uptime Kuma
- Deployed private Ollama LLM server for internal automation tasks
- Automated operational workflows via n8n + Python

---

## Open Source & Infrastructure

- **GPU Server (cyberdub-ai):** Ubuntu 24.04, Docker, Ollama + Tesla P40, Qdrant, n8n, Caddy, Prometheus/Grafana
- **Active Ollama models:** qwen2.5:32b, devstral:24b, qwen3-coder:30b, llava, bge-m3, nomic-embed-text
- **Infrastructure as code:** All services in Docker Compose, secrets in `/srv/secrets/`, reverse proxy via Caddy

---

## Education

Saint Petersburg State University of Aerospace Instrumentation (SPbGUAP) · Degree, 2000  
Institute for Problems in Mechanical Engineering RAS (IPMash RAS) · Postgraduate studies, 2003

---

## Languages

Russian — Native · English — Professional working proficiency (technical documentation, communication)
