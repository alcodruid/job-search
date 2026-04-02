# Anti-Gravity Prompt — Resume EN (AI direction)

---

## ⚠️ DEPLOYMENT RULES — READ BEFORE GENERATING ANY DEPLOY CODE

This site runs on a home server (cyberdub-ai, Ubuntu 24.04). Follow these rules exactly.

**Architecture:** Internet → Caddy (80/443) → Docker containers (internal `n8n_net` network)

**Reverse proxy: CADDY ONLY.** Never nginx, never Apache, never any other proxy.

**New container — pick port from the free range:**
- Network: `n8n_net` (external, already exists)
- Occupied ports (do not use): 80, 443, 3000, 3001, 3020-3025, 3040, 3056, 3070-3096, 5432-5435, 5678, 6333, 6379-6385, 8050-8090, 8118-8119, 9090, 11434, 19999
- Use `expose:` not `ports:` in docker-compose.yml

**docker-compose.yml template:**
```yaml
services:
  resume-en:
    build: .
    container_name: resume-en
    restart: unless-stopped
    expose:
      - "PORT"
    networks:
      - n8n_net
networks:
  n8n_net:
    external: true
    name: n8n_net
```

**Full deploy rules:** `~/job-search/deploy-rules.md`

---

## TASK

Create a beautiful **single-page HTML resume** for Alexey Zhuykov.
Style: **AI Engineer, dark terminal aesthetic** — matches the cyberdub.su brand.

The page must:
- Look like a professional document with premium design
- Support **print to PDF** via browser (Ctrl+P or on-page button)
- Be standalone (single HTML file or Vite/React — Nano Banana's choice)
- Include a **"Download PDF"** button that calls `window.print()`

---

## DESIGN SYSTEM

MOOD: "Private GPU server meets hacker's portfolio meets senior engineering blog"
Feeling: Not a startup landing page. Not academic. Someone who actually ships.

**COLOR PALETTE:**
```
Background primary:   #0d1117  (GitHub dark — near-black)
Background secondary: #161b22  (slightly lighter, for cards)
Background tertiary:  #1c2128  (code blocks, hover states)
Accent primary:       #00d4ff  (electric cyan — active/live state)
Accent secondary:     #00ff88  (neon green — success, "it works")
Accent warning:       #ffb347  (amber — stats, highlights)
Text primary:         #e6edf3  (near-white)
Text secondary:       #7d8590  (muted grey — like code comments)
Text dim:             #484f58  (very muted — placeholders, borders)
Border:               #30363d  (dark grey, GitHub-style)
Code text:            #a5d6ff  (light blue — syntax highlighting)
```

**TYPOGRAPHY:**
```
Headlines H1/H2: "Space Grotesk" 700-800
Body text:       "Space Grotesk" 400-500, 15px
Code/Technical:  "JetBrains Mono" 400-500
                 (tech names, tags, stat numbers)
```

Google Fonts: Space Grotesk 400,500,700,800 + JetBrains Mono 400,500

**TAG CHIPS for technologies:**
```css
background: #1c2128;
border: 1px solid #30363d;
color: #a5d6ff;
font-family: 'JetBrains Mono';
border-radius: 4px;
padding: 3px 8px;
font-size: 12px;
```

**LAYOUT:**
- Max content width: 860px, centered
- Two layout modes: web (dark bg, shadows, glow) and print (white bg, black text)
- Print: @media print → white background, black text, no shadows/animations

---

## PRINT STYLES

```css
@media print {
  body { background: white; color: #1a1a1a; }
  .no-print { display: none !important; }
  .section { page-break-inside: avoid; }
  a { color: #1a1a1a; text-decoration: none; }
}
@page {
  margin: 15mm 20mm;
  size: A4;
}
```

---

## PAGE STRUCTURE

### HEADER

Terminal prompt line at top:
```
> cv.cyberdub.su                                          [EN] [RU]
```
- Logo: `> cv.cyberdub.su` in JetBrains Mono, #00d4ff
- Language switcher (decorative): [EN] active amber, [RU] #7d8590
- Sticky on web only, hidden in print

---

### SECTION 1: HERO — Personal Info

**Name:** `Alexey Zhuykov`
- Size: 42px, Space Grotesk 800, #e6edf3
- Decorative line above: `$ whoami` in JetBrains Mono, #7d8590, 14px

**Title line below name:**
```
Senior AI Engineer · LLM Infrastructure Engineer · Head of AI
```
- Space Grotesk 500, 18px, #00d4ff

**Contacts — horizontal row:**
```
📍 Saint Petersburg, Russia (Remote)
📧 alexey.zhuykov@gmail.com
📱 +7 (921) 946-85-35
🔗 cyberdub.su
🐙 github.com/cyberdub-ai
💼 linkedin.com/in/alexeyzhuykov
```
- JetBrains Mono 400, 13px, #7d8590
- Links: #00d4ff, hover: underline

**"Download PDF" button** on the right side of header:
- `[⬇ Download PDF]` — amber (#ffb347), JetBrains Mono, border 1px solid #ffb347
- onclick: `window.print()`
- Class `.no-print` — hidden on print

---

### SECTION 2: Summary

Terminal component (dark box with traffic-light dots):
```
╭─ about.md ──────────────────────────────────────────────────╮
│                                                              │
│  AI practitioner with production LLM infrastructure         │
│  running 24/7. I build, deploy, and operate AI systems —    │
│  not just prototype them. My home GPU server (NVIDIA        │
│  Tesla P40) runs multiple open-source LLMs (Qwen 32B,       │
│  Devstral 24B, Llava), Qdrant vector database, and n8n      │
│  automation pipelines. Shipped 6+ AI-powered products.      │
│                                                              │
│  Specialization: private LLM deployment for enterprise —    │
│  models run on client hardware, data never leaves the       │
│  perimeter.                                                  │
│                                                              │
│  19 years as CEO of a telecom operator means I understand   │
│  enterprise requirements deeply: reliability, SLAs,         │
│  compliance, team ownership, and sustainable architecture.  │
╰──────────────────────────────────────────────────────────────╯
```

Implementation: div with border 1px solid #30363d, background #161b22, border-radius 8px.
Header bar: `about.md` in JetBrains Mono + traffic-light dots (⬤ red #ff5f57, ⬤ yellow #ffbd2e, ⬤ green #28ca41).

---

### SECTION 3: Technical Skills

**Section header:** `$ cat stack.json` in JetBrains Mono, #7d8590

4 cards in 2×2 grid (mobile: 1 column):

**Card 1: LLM & Inference**
```
LLM & Inference
─────────────────────────────────
Ollama    vLLM    Hugging Face
qwen2.5:32b    devstral:24b
qwen3-coder:30b    llava (vision)
Fine-tuning · LoRA · PEFT
Prompt Engineering
RAG pipelines · Agentic systems
Function calling / Tool use
```

**Card 2: Vector Databases**
```
Vector Databases
─────────────────────────────────
Qdrant (production, multi-tenant)
bge-m3 (1024-dim embeddings)
nomic-embed-text (768-dim)
mxbai-embed-large
Semantic search · Hybrid search
```

**Card 3: Automation**
```
Automation & Orchestration
─────────────────────────────────
n8n    Python    FastAPI
asyncio · httpx · SQLAlchemy
Telegram Bot API (PTB 22+)
Docker    Docker Compose
Caddy    PostgreSQL    Redis
```

**Card 4: Infrastructure**
```
Infrastructure & Hardware
─────────────────────────────────
Linux (Ubuntu Server 24.04)
NVIDIA Tesla P40 · 24GB VRAM
CUDA · GPU memory management
Prometheus · Grafana
Netdata · Uptime Kuma
GitHub Actions · Bash
```

Each card: border #30363d, background #161b22, title #00d4ff JetBrains Mono.
Technologies rendered as tag chips (see Design System).

---

### SECTION 4: Projects

**Section header:** `$ ls ~/projects/` in JetBrains Mono, #7d8590

6 project cards. Each card:
- Top line: status badge `[PROD]` in green / `[WIP]` in amber
- Project name: Space Grotesk 700, #e6edf3
- One-line description: #7d8590, 14px
- Stack: tag chips
- Hover: border #00d4ff, background #1c2128

**Project 1:**
```
[PROD] Replyo — AI-Powered CRM
Business CRM with RAG core: trains on company knowledge base, classifies
inquiries, generates contextual responses, Telegram integration.
Stack: [qwen2.5:32b] [qwen2.5:7b] [nomic-embed-text] [Qdrant] [n8n] [Python] [Docker]
Highlights: Multi-tenant knowledge base · Conversation memory · Auto-response suggestions
```

**Project 2:**
```
[PROD] TelecomExpert.ru — Telecom Materials Marketplace
Marketplace of regulatory docs, contract templates, and SORM/TSPU guides for small Russian
ISPs. RAG-powered search: ask a question — get an answer with source citation.
Open to operators: telecomexpert.ru
Stack: [bge-m3 1024-dim] [Qdrant] [qwen2.5:32b] [FastAPI] [Python] [Docker]
```

**Project 3:**
```
[PROD] Job Matcher — AI Job Search Assistant
Telegram bot: resume analysis, job matching, resume tailoring, interview prep coaching.
Stack: [qwen2.5:32b] [Python] [PTB 22.7] [PostgreSQL]
Highlights: Multi-step conversation flow · Structured output parsing · HH.ru integration
```

**Project 4:**
```
[PROD] FinPulse — AI Financial News Digest
Auto-aggregation from Telegram channels → LLM analysis → structured digest 2×/day.
Stack: [n8n] [qwen2.5:32b] [Telegram Bot API] [Python]
Highlights: Multi-source aggregation · Topic extraction · Editorial formatting
```

**Project 5:**
```
[WIP] SNT-Pilot — AI-Assisted HOA Management
Mobile app + backend: property tracking, complaint system, multi-channel notifications.
Stack: [React Native] [FastAPI] [PostgreSQL] [qwen2.5:32b]
Highlights: Offline-capable mobile app · AI-generated complaint letters
```

**Project 6:**
```
[WIP] AI-CFO — Financial Analysis AI Platform
AI tools marketplace for CFOs: financial report analysis, forecasting, presentation gen.
Stack: [qwen2.5:32b] [Qdrant RAG] [n8n] [React] [FastAPI]
```

---

### SECTION 5: Experience

**Section header:** `$ cat experience.log` in JetBrains Mono, #7d8590

**Position 1:**
```
CEO & AI/DevOps Practitioner
JSC TELSI · Saint Petersburg, Russia · March 2007 — April 2026 (19 years)
```

Regional telecommunications operator providing internet, telephony, and video surveillance.
While running the company, independently built and operated all server infrastructure.

Bullet points (use `▸` icon in #00d4ff):
- Migrated all services to Docker/Docker Compose (zero-downtime deployments)
- Built monitoring stack: Prometheus + Grafana + Uptime Kuma
- Deployed private Ollama LLM server for internal automation tasks
- Automated operational workflows via n8n + Python scripting
- Full P&L ownership for 18-person team over 19 consecutive years

---

### SECTION 6: Production Infrastructure

Terminal component:
```
$ docker ps --format "{{.Names}}\t{{.Status}}"

cyberdub-ai server (running 24/7):
├── ollama          [UP] qwen2.5:32b · devstral:24b · qwen3-coder:30b · llava
├── qdrant          [UP] collections: telecom-docs · job-listings · kb-replyo
├── n8n             [UP] workflows: 47 active
├── prometheus      [UP] scraping: 12 targets
├── grafana         [UP] dashboards: 8
└── caddy           [UP] TLS: cyberdub.su · cv.cyberdub.su

GPU:  NVIDIA Tesla P40 · 24GB VRAM · CUDA 12.x
Host: Ubuntu Server 24.04 LTS
```

---

### SECTION 7: Education

Two cards side by side:

```
SPbGUAP                                   IPMash RAS
Saint Petersburg State University         Institute for Problems in Mechanical
of Aerospace Instrumentation              Engineering, Russian Academy of Sciences
Degree, 2000                              Postgraduate studies, 2003
```

---

### SECTION 8: Languages

```
Russian     ████████████  Native
English     ████████░░░░  Professional working proficiency
                          (technical documentation, written communication)
```

Bars: #00d4ff fill, #30363d background.

---

### FOOTER

```
> Last updated: April 2026
> alexey.zhuykov@gmail.com · cyberdub.su · github.com/cyberdub-ai
```

JetBrains Mono, #484f58, 12px.

---

## TECHNICAL REQUIREMENTS

- Single `index.html` with inline CSS or Vite+React — Nano Banana's choice
- Google Fonts via `<link>` (no @import)
- No external dependencies except Google Fonts
- Print button: `onclick="window.print()"`
- `<title>Alexey Zhuykov — AI Engineer</title>`
- `<meta name="description" content="Resume of AI Engineer Alexey Zhuykov">`
- Responsive: works on mobile (320px+) and desktop

---

**Output to:** `resume-en/index.html` with Dockerfile for nginx deployment.
