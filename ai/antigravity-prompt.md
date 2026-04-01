# Anti-Gravity Prompts — cyberdub.su

---

## ⚠️ DEPLOYMENT RULES — READ BEFORE GENERATING ANY DEPLOY CODE

This site runs on a home server (cyberdub-ai, Ubuntu 24.04). Follow these rules exactly.

**Architecture:** Internet → Caddy (80/443) → Docker containers (internal `n8n_net` network)

**Reverse proxy: CADDY ONLY.** Never nginx, never Apache, never any other proxy.

**Existing setup — DO NOT change container name or port:**
- Container: `cyberdub-website`, internal port `3056`
- Network: `n8n_net` (external, already exists)
- Compose: `~/stack/cyberdub-website/docker-compose.yml`
- Caddy already routes `cyberdub.su → cyberdub-website:3056` in `~/stack/n8n/Caddyfile`

**docker-compose.yml must look like:**
```yaml
services:
  cyberdub-website:
    build: .
    container_name: cyberdub-website
    restart: unless-stopped
    expose:
      - "3056"       # use expose:, NOT ports:
    networks:
      - n8n_net
networks:
  n8n_net:
    external: true
    name: n8n_net
```

**Occupied ports (do not use):** 80, 443, 3000, 3001, 3020-3025, 3040, 3056, 3070-3096, 5432-5435, 5678, 6333, 6379-6385, 8050-8090, 8118-8119, 9090, 11434, 19999

**Deploy commands:**
```bash
cd ~/stack/cyberdub-website && docker compose build && docker compose up -d
docker exec caddy caddy reload --config /etc/caddy/Caddyfile  # if Caddyfile changed
```

**Full deploy rules:** `~/job-search/deploy-rules.md`

---

## DESIGN SYSTEM (apply to all pages)

MOOD: "Private GPU server meets hacker's portfolio meets senior engineering blog"
Feeling: Not startup-flashy, not academic. Like someone who actually ships things.
The terminal is not decoration — it's the aesthetic because this person lives in terminals.

COLOR PALETTE:
- Background primary: #0d1117 (GitHub dark — near-black, slight blue tint)
- Background secondary: #161b22 (slightly lighter dark, for cards)
- Background tertiary: #1c2128 (for code blocks, hover states)
- Accent primary: #00d4ff (electric cyan — active, live, processing)
- Accent secondary: #00ff88 (neon green — success, confirmation, "it works")
- Accent warning: #ffb347 (amber — for stats, highlights, "important")
- Text primary: #e6edf3 (near-white, slight blue cast — like terminal text)
- Text secondary: #7d8590 (muted grey — like code comments)
- Text dim: #484f58 (very muted — placeholders, borders)
- Border: #30363d (dark grey, GitHub-style)
- Code text: #a5d6ff (light blue — like syntax highlighting)

TYPOGRAPHY:
- Headlines H1/H2: "Space Grotesk" weight 700-800 (technical but not cold)
  fallback: "DM Sans", system-ui, sans-serif  
- Body: "Space Grotesk" weight 400-500, size 16px
- Code / Technical: "JetBrains Mono" weight 400-500
  This font appears everywhere: in tags, in stack listings, in stat numbers
  fallback: "Fira Code", "Cascadia Code", monospace
- Very large display numbers: "Space Grotesk" weight 800, color #00d4ff

LAYOUT PRINCIPLES:
- Dense but breathable — more information density than the telecom site
- Code-block aesthetic for stack listings (dark bg, monospace, syntax colors)
- Tag chips everywhere: [Python] [Docker] [Ollama] — small monospace pills
  Background: #1c2128, border: 1px solid #30363d, text: #a5d6ff, font: JetBrains Mono
  Border-radius: 4px, padding: 3px 8px, font-size: 12px
- Horizontal scroll sections for tech stacks on mobile
- "Live" indicators: pulsing green dot (•) for "currently running" items

SPECIAL VISUAL ELEMENTS:
- Terminal window component: dark box with traffic-light dots (red/yellow/green circles)
  Title bar: #1c2128, dots at 8px, content area: #0d1117
  Use for code snippets, architecture descriptions, stack listings
- Grid overlay: very subtle dot grid pattern on backgrounds (2% opacity, #30363d)
- Gradient blobs: extremely subtle, 4% opacity cyan/green blobs in background corners
- Animated typing cursor (|) on key text elements — blinking CSS animation

ANIMATIONS:
- Entrance: elements fade in + slide up, 100ms stagger
- Cards: hover → lift 4px + border-color transition to #00d4ff + background lighten
- Buttons: hover → slight glow (box-shadow 0 0 12px rgba(0, 212, 255, 0.3))
- Tags: hover → border-color #00d4ff, text #00d4ff

---

## PAGE 1: HOME

Create the HOME page for cyberdub.su, AI engineering portfolio website for Alexey Zhuykov.
Apply the design system above completely.

### Page Structure

**Navigation:**
- Left: Logo — "cyberdub.su" in JetBrains Mono 600, #00d4ff, no decoration
  Preceded by: "> " in #7d8590 (like a terminal prompt)
  So it looks like: > cyberdub.su
- Right: "Stack | Projects | Resume | Contact" — Space Grotesk 400, #7d8590
  Hover: #e6edf3 with 0.15s ease
- Background: rgba(13, 17, 23, 0.95) with backdrop-filter blur
- Bottom: 1px solid #30363d
- Sticky on scroll

**SECTION 1: Hero**

Full-viewport-height hero section.

UPPER LEFT: Status indicator
  Pulsing green dot (•, animation: pulse 2s infinite) + "Available for remote roles"
  Font: JetBrains Mono 400, 13px, color #00ff88
  Letter-spacing: 0.1em

MAIN HEADLINE (left-aligned, not centered):
  Line 1: "I Deploy AI" — Space Grotesk 800, 88px desktop / 52px mobile, #e6edf3
  Line 2: "That Works" — Space Grotesk 800, 88px / 52px, #e6edf3
  Line 3: "in Production." — Space Grotesk 800, 88px / 52px, color #00d4ff
  
  After "Production." add a blinking cursor: | (CSS animation, color #00d4ff)

DESCRIPTOR (below headline, max-width 560px):
  "Not prototypes. Not notebooks. Running 24/7 on my GPU server: 
  Ollama, Qdrant, n8n pipelines, and 6 AI products shipping to real users."
  Font: Space Grotesk 400, 18px, #7d8590, line-height 1.7

CTA ROW (two buttons + a text link):
  Button 1 (Primary): "See My Stack →"
    Background: #00d4ff, text: #0d1117, font: Space Grotesk 600, 14px
    Padding: 14px 28px, border-radius: 6px
    Hover: background #33ddff, box-shadow 0 0 20px rgba(0, 212, 255, 0.3)
    
  Button 2 (Secondary): "View Projects"
    Border: 1px solid #30363d, text: #e6edf3, background: transparent
    Hover: border-color #00d4ff, text #00d4ff
    
  Text link: "Download Resume ↓" — JetBrains Mono 400, 13px, #7d8590, hover #e6edf3

RIGHT SIDE (desktop only — 40% width):
  Terminal window component showing a live-looking command output:
  
  [Terminal window with traffic light dots]
  Title bar text: "alexey@cyberdub-ai:~$"
  
  Content (JetBrains Mono 400, 13px, with syntax colors):
  
  $ ollama list
  NAME                    ID           SIZE    MODIFIED
  qwen2.5:32b            a3...        19 GB   running
  devstral:24b           c7...        14 GB   2 days ago
  qwen3-coder:30b        f2...        18 GB   1 week ago
  llava:latest           9c...        4.7 GB  1 week ago
  bge-m3:latest          b1...        1.2 GB  running
  
  $ docker ps --format "{{.Names}}"
  n8n
  qdrant  
  caddy
  ollama
  monitoring
  
  [cursor blinking]
  
  Color scheme: commands in #e6edf3, output labels in #7d8590, 
  values in #a5d6ff, "running" in #00ff88

**SECTION 2: Stack Overview Strip**

Full-width dark strip (#161b22), padding 40px 0
Label: "THE STACK" — JetBrains Mono 400, 11px, letter-spacing 0.3em, #7d8590

Horizontal scrollable row of tech chips (larger than regular tags):
Each chip: background #1c2128, border 1px solid #30363d, border-radius 8px
Font: JetBrains Mono 500, 14px, padding 10px 16px
Hover: border-color #00d4ff, text #00d4ff

Chips in order:
[Ollama] [qwen2.5:32b] [Qdrant] [n8n] [Python] [FastAPI] [Docker] [Tesla P40] 
[bge-m3] [RAG] [vLLM] [Telegram Bot API] [PostgreSQL] [Caddy] [Ubuntu 24.04]

**SECTION 3: Three-column Value Props**

Three cards, equal width, with top border accent (3px solid #00d4ff on card 1, 
#00ff88 on card 2, #ffb347 on card 3):

Card 1 — Private LLM Deployment:
  Icon area: terminal icon, cyan
  Title: "Private LLM for Enterprise" — Space Grotesk 700, 20px, #e6edf3
  Body: "Models run on your hardware. Data never leaves your perimeter. 
  Already running qwen2.5:32b and devstral:24b in production with 
  multi-model serving and GPU memory management."

Card 2 — RAG Systems:
  Icon: database/search icon, green
  Title: "Production RAG Pipelines"
  Body: "Not hello-world RAG. Full pipelines: document ingestion, 
  chunking, bge-m3 embeddings, Qdrant collections, retrieval tuning, 
  generation quality evaluation. Deployed for two different domains."

Card 3 — Automation:
  Icon: workflow/lightning icon, amber
  Title: "AI Automation Pipelines"
  Body: "n8n + Python + LLMs for complex multi-step workflows. 
  Telegram bots with AI cores, scheduled digest generation, 
  webhook-driven processing. 6 products shipped."

**SECTION 4: Projects Teaser**
Simple two-row grid of 3 project cards each (6 total).
Each card: dark background #161b22, border #30363d, hover border #00d4ff
Card content: Project name (Space Grotesk 700), one-line description, 3 tech tags
Link: "View all projects →" below grid, Space Grotesk 500, #00d4ff

Projects to show:
1. Replyo — AI CRM with RAG core — [Ollama] [Qdrant] [n8n]
2. TelecomExpert — Technical documentation RAG — [bge-m3] [Qdrant] [FastAPI]
3. Job Matcher — AI job search assistant — [LLM] [Python] [Telegram]
4. FinPulse — Automated news digest — [n8n] [Qwen] [Telegram]
5. SNT-Pilot — HOA management platform — [React Native] [FastAPI] [AI]
6. AI-CFO — Financial analysis AI — [RAG] [Qdrant] [React]

**SECTION 5: About Strip (minimal)**

Dark divider section:
Left: Large text quote style
  '"I don't work on AI. I run AI." — Alexey Zhuykov, Saint Petersburg'
  Font: Space Grotesk 400 italic, 24px, #7d8590
  
Right: Brief bio (2 sentences)
  "19 years as CEO of a telecom operator. In parallel: built private GPU infrastructure, 
  shipped 6 AI products, currently specializing in private LLM deployment for enterprise."
  + Link: "Full background →"


---

## PAGE 2: STACK

Create the STACK page for cyberdub.su. Same design system.

### Content

**Page Header:**
  Label: "THE STACK" — terminal style with > prefix
  H1: "What's Running Right Now"
  Subhead: "Everything here is in production. Not a resume list — a running system."

**Infrastructure Architecture Section:**

Section title: "cyberdub-ai — Home GPU Server"

Architecture description (styled as a large terminal window):

[Terminal window component]

HARDWARE:
  CPU: Intel Core i9 / AMD Ryzen (production server)
  GPU: NVIDIA Tesla P40 · 24GB GDDR5 (adding)
  RAM: 64GB ECC
  Storage: NVMe SSD + HDD array
  OS: Ubuntu 24.04 LTS

NETWORK:
  Proxy: Caddy (HTTPS, auto TLS, BasicAuth)
  VPN: WireGuard (172.16.82.0/24)
  Tunnel: SSH SOCKS5 → VPS LA (for API access)
  
RUNNING SERVICES (docker ps):
  ollama         → :11434  (LLM inference)
  qdrant         → :6333   (vector database)
  n8n            → :5678   (automation workflows)
  caddy          → :80/:443 (reverse proxy)
  prometheus     → :9090   (metrics)
  grafana        → :3000   (dashboards)
  netdata        → :19999  (system monitoring)
  uptime-kuma    → :3001   (uptime tracking)

**LLM Models Section:**

Section title: "Active LLM Models"
Subtitle: "Loaded in Ollama, available via API at localhost:11434"

Table-style layout (not actual HTML table — styled divs with mono font):

Header row: MODEL NAME | SIZE | USE CASE | STATUS
Divider line

Row 1: qwen2.5:32b | 19 GB | Primary LLM — reasoning, generation, RAG | [● RUNNING]
Row 2: devstral:24b | 14 GB | Code generation, review | [● ACTIVE]
Row 3: qwen3-coder:30b | 18 GB | Advanced coding tasks | [● LOADED]  
Row 4: llava:latest | 4.7 GB | Vision — image analysis | [○ STANDBY]
Row 5: qwen2.5:7b | 4.7 GB | Fast inference, classification | [● RUNNING]
Row 6: bge-m3:latest | 1.2 GB | Embeddings 1024-dim (TelecomExpert) | [● RUNNING]
Row 7: nomic-embed-text | 274 MB | Embeddings 768-dim (Replyo) | [● RUNNING]

[● RUNNING] in #00ff88, [○ STANDBY] in #7d8590, [● ACTIVE] in #00d4ff

**Qdrant Vector Collections:**

Section title: "Vector Database — Qdrant"
Subtitle: "Production collections powering RAG systems"

Two collection cards:

Collection 1: telecom_knowledge
  Dimensions: 1024
  Embedding model: bge-m3
  Distance: Cosine
  Used by: TelecomExpert RAG system
  Status: [● ACTIVE]

Collection 2: replyo_*
  Dimensions: 768
  Embedding model: nomic-embed-text
  Distance: Cosine
  Used by: Replyo CRM (multi-tenant)
  Status: [● ACTIVE]

**Full Technology Stack Table:**

Four columns of skill cards:

Column 1 — LLM & AI:
  [Ollama] [vLLM] [Hugging Face] [RAG Pipelines] [Fine-tuning/LoRA]
  [Prompt Engineering] [Agentic Systems] [Tool Use / Function Calling]

Column 2 — Data & Storage:
  [Qdrant] [PostgreSQL] [Redis] [bge-m3] [nomic-embed-text]
  [Vector Search] [Hybrid Search] [Semantic Similarity]

Column 3 — Automation & APIs:
  [n8n] [Python] [FastAPI] [asyncio] [Telegram Bot API (PTB 22)]
  [httpx] [SQLAlchemy] [REST / Webhook]

Column 4 — Infrastructure:
  [Docker / Docker Compose] [Caddy] [Linux Ubuntu 24.04]
  [Prometheus] [Grafana] [Netdata] [Uptime Kuma]
  [GitHub Actions] [WireGuard VPN] [SSH]

**Philosophy Section (bottom of Stack page):**

Dark card with left border #00d4ff:
Title: "Why Private LLM?"
Body: "Every enterprise client I've talked to has the same concern: their data.
Sending prompts to OpenAI API means your documents, your customer data, your internal 
knowledge leaves your network. Private LLM deployment solves this completely.
qwen2.5:32b on your own hardware, isolated network, zero data leakage.
That's what I build. That's what cyberdub-ai runs on."

---

## PAGE 3: PROJECTS

Create the PROJECTS page for cyberdub.su. Same design system.

### Content

**Page Header:**
  Label: "PROJECTS"
  H1: "Shipped. Running. Real."
  Subhead: "6 AI products built and deployed on private infrastructure."

**Project Cards (one full-width card per project, stacked vertically):**

Each card: 
  - Dark background #161b22
  - Left colored accent border (4px): cyan for first, green, amber, cyan, green, amber
  - Two-column layout: 60% description / 40% tech details
  - Hover: border-left brightens, subtle background lightens

---

PROJECT 1: Replyo — AI CRM

Left column:
  Status badge: [● PRODUCTION] — #00ff88 text, #1c2128 bg
  Title: "Replyo" — Space Grotesk 700, 36px, #e6edf3
  Subtitle: "AI-Powered CRM for Business"
  
  Description: "Business CRM with RAG at its core. The system learns from a company's 
  knowledge base and generates contextually accurate responses to customer inquiries. 
  Multi-tenant architecture: each client has isolated Qdrant collections and independent 
  model fine-tuning capability.
  
  Built for real customer service operations: Telegram integration as the primary 
  channel, conversation memory, automated response suggestions, escalation logic, 
  and a classifier that routes messages by intent."
  
  Key features list (with green check ✓):
    ✓ Learns from company knowledge base
    ✓ Qdrant-backed semantic search
    ✓ Telegram Bot integration
    ✓ Conversation memory
    ✓ Intent classification (qwen2.5:7b)
    ✓ Multi-tenant isolated data

Right column (terminal-style):
  TECH STACK:
  
  LLM:      qwen2.5:32b (main)
            qwen2.5:7b (classifier)
  
  Vectors:  Qdrant
            nomic-embed-text (768-dim)
  
  Backend:  Python / FastAPI
            PostgreSQL
            Redis (sessions)
  
  Frontend: TypeScript
  
  Infra:    Docker Compose
            n8n (workflows)
            Telegram Bot API

---

PROJECT 2: TelecomExpert — Documentation RAG

Left:
  Status: [● PRODUCTION]
  Title: "TelecomExpert"
  Subtitle: "Enterprise Documentation RAG System"
  
  Description: "RAG system for navigating complex technical documentation in the 
  telecommunications domain. Handles heterogeneous document types (PDFs, Word, web), 
  applies domain-specific chunking strategies, and uses bge-m3 — a multilingual model 
  with 1024-dimensional embeddings — for high-quality semantic retrieval.
  
  The key engineering decision: separate Qdrant collection with bge-m3 embeddings 
  (not the default nomic-embed-text), which significantly improved retrieval quality 
  for technical telecom content vs general-purpose embedding models."
  
  Key features:
    ✓ Domain-specific embedding model selection
    ✓ bge-m3 1024-dim embeddings
    ✓ Separate Qdrant collection per tenant
    ✓ PDF + Word + web ingestion
    ✓ Retrieval quality evaluation pipeline
    ✓ FastAPI REST interface

Right:
  LLM:      qwen2.5:32b
  Vectors:  Qdrant (telecom_knowledge)
            bge-m3 (1024-dim, Cosine)
  Backend:  Python / FastAPI
  Infra:    Docker, n8n

---

PROJECT 3: Job Matcher — AI Career Assistant

Left:
  Status: [● PRODUCTION]
  Title: "Job Matcher"
  Subtitle: "AI-Powered Job Search Assistant"
  
  Description: "Telegram bot with LLM core for intelligent job search. 
  Analyzes uploaded resumes, matches against job descriptions, identifies gaps, 
  suggests improvements, and generates adapted versions for specific positions.
  
  Includes mock interview preparation: the bot asks role-specific questions and 
  evaluates answers using STAR methodology. Built on PTB 22.7 with proper 
  callback_query handling and conversation state management via FSM."
  
  Key features:
    ✓ Resume analysis and scoring
    ✓ Job description matching
    ✓ Resume adaptation for specific roles
    ✓ Mock interview mode (STAR methodology)
    ✓ Multi-step conversation FSM
    ✓ HH.ru integration

Right:
  LLM:      qwen2.5:32b
  Backend:  Python
            PTB 22.7
            PostgreSQL
  Infra:    Docker

---

PROJECT 4: FinPulse — AI Financial Digest

Left:
  Status: [● PRODUCTION]
  Title: "FinPulse"
  Subtitle: "Automated AI Financial News Digest"
  
  Description: "Aggregates messages from curated financial Telegram channels and chats, 
  processes them through qwen2.5:32b for topic extraction and summarization, 
  and delivers a structured digest twice daily.
  
  The challenge: getting the LLM to reliably return structured JSON for 50+ input messages 
  without hallucination or empty responses. Solved through output format enforcement 
  and multi-pass validation in the n8n pipeline."
  
  Key features:
    ✓ Multi-channel Telegram aggregation
    ✓ LLM topic extraction and clustering
    ✓ Structured digest formatting
    ✓ 2× daily automated delivery
    ✓ n8n orchestration

Right:
  LLM:      qwen2.5:32b
  Automation: n8n
  Channels: Telegram Bot API
  Infra:    Docker, Python

---

PROJECT 5: SNT-Pilot — HOA Management Platform

Left:
  Status: [● IN DEVELOPMENT]
  Title: "SNT-Pilot"
  Subtitle: "AI-Assisted HOA Management"
  
  Description: "Mobile-first platform for managing homeowners associations (садоводческие 
  товарищества / СНТ) in Russia. Handles property registry, utility accounting, 
  meeting minutes, and a multi-channel complaint/claim system with automated 
  document generation.
  
  AI component: generates formal complaint letters in legal Russian based on 
  user-described issues. 152-FZ compliance for personal data handling."
  
  Key features:
    ✓ Property and owner registry
    ✓ Utility billing calculator
    ✓ AI-generated legal documents
    ✓ Multi-channel notifications
    ✓ 152-FZ compliant
    ✓ React Native mobile app

Right:
  Mobile:   React Native
  Backend:  FastAPI / Python
            PostgreSQL
  AI:       qwen2.5:32b
  Infra:    Docker

---

PROJECT 6: AI-CFO — Financial AI Platform

Left:
  Status: [● IN DEVELOPMENT]
  Title: "AI-CFO"
  Subtitle: "AI Tools Marketplace for Financial Directors"
  
  Description: "Platform of AI-powered tools for CFOs and financial analysts: 
  financial statement analysis, scenario forecasting, board presentation generation, 
  and cash flow optimization recommendations.
  
  RAG-backed knowledge base of accounting standards and financial regulations. 
  Generates structured Excel-compatible reports."
  
  Key features:
    ✓ Financial statement analysis
    ✓ Regulatory RAG knowledge base
    ✓ Scenario forecasting
    ✓ Presentation generation
    ✓ Excel export

Right:
  LLM:      qwen2.5:32b
  Vectors:  Qdrant RAG
  Frontend: React
  Backend:  FastAPI
  Automation: n8n

---

## PAGE 4: RESUME / DOWNLOADS

Create the RESUME page for cyberdub.su. Same dark design system.

### Content

**Page Header (terminal style):**
  Label: "> resume"
  H1: "Download CV"
  Subhead: "Senior AI Engineer · LLM Infrastructure · Remote"

**Download Cards (same layout as telecom site but dark theme):**

Card 1 — Russian:
  [RU] Резюме — Русский
  Для российских AI-компаний и команд
  • Полный технический стэк · 4 страницы
  • Портфолио проектов с описаниями
  Button: "Скачать (RU)" — cyan button
  
Card 2 — English:
  [EN] Resume — English  
  For international remote positions
  • Full technical stack · 4 pages  
  • Project portfolio with descriptions
  Button: "Download (EN)" — cyan button

**Skills Visualization Section:**

Section title: "Core Competencies" in terminal style

Four-row skill bars (not percentage bars — level indicators):

Row: "LLM Deployment & Inference" ████████████ Expert
Row: "RAG Architecture" ████████████ Expert  
Row: "n8n Automation" ████████████ Expert
Row: "Python / FastAPI" ██████████░░ Advanced
Row: "MLOps / Docker" ██████████░░ Advanced
Row: "Fine-tuning / LoRA" ████████░░░░ Intermediate
Row: "Kubernetes / k8s" ██████░░░░░░ Learning

Style: bars in #00d4ff, empty sections in #30363d, label in #e6edf3, level in #7d8590

**Open for section:**
  Title: "What I'm Looking For"
  
  Cards (3, horizontal):
  
  Card 1: Senior AI Engineer
    Remote · Full-time
    "Building and scaling AI systems in production"
    Target: 500k–900k ₽/mo or $80k–150k/yr remote

  Card 2: Head of AI
    Remote · Full-time  
    "Building AI teams and strategy, with hands-on technical involvement"
    
  Card 3: AI Consulting
    Project-based
    "Private LLM deployment, RAG systems, automation pipelines"

---

## PAGE 5: CONTACT

Create the CONTACT page for cyberdub.su. Same dark design system.

### Content

**Page Header:**
  Label: "> contact"
  H1: "Get in Touch"
  Subhead: "Remote-first. Available worldwide. Response within 24h."

**Two-column layout:**

Left (55%): Contact form with terminal-style inputs
  Dark inputs: background #161b22, border #30363d, focus border #00d4ff
  Font: Space Grotesk 400 for labels, JetBrains Mono 400 for input text
  
  Fields:
  name: [text input — placeholder: "your_name"]
  email: [email — placeholder: "contact@company.com"]  
  type: radio group with monospace style:
    ○ job_offer
    ○ consulting_project  
    ○ collaboration
    ○ other
  message: [textarea — placeholder: "Describe what you're building..."]
  
  Submit: "send_message()" — cyan button, full width
  Below: "// Response time: usually < 24 hours"

Right (45%): Contacts
  
  Section styled as terminal output:
  
  [Terminal window]
  $ cat ~/.contact_info
  
  email:     info@sntpilot.ru
  telegram:  @alexeyzhuykov
  github:    github.com/alcodruid
  linkedin:  linkedin.com/in/alexeyzhuykov
  location:  Saint Petersburg, Russia (UTC+3)
  remote:    worldwide
  
  $ cat ~/.availability
  
  status:      OPEN TO OPPORTUNITIES
  format:      remote-first
  types:       full-time, part-time, consulting
  timezone:    UTC+3 (flexible overlap)
  
  [blinking cursor]

