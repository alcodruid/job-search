# Anti-Gravity Prompt — Resume EN (Telecom direction)

---

## ⚠️ DEPLOYMENT RULES — READ BEFORE GENERATING ANY DEPLOY CODE

This site runs on a home server (cyberdub-ai, Ubuntu 24.04). Follow these rules exactly.

**Architecture:** Internet → Caddy (80/443) → Docker containers (internal `n8n_net` network)
**Reverse proxy: CADDY ONLY.** Never nginx, never Apache, never any other proxy.
**Network:** n8n_net (external, already exists). Use `expose:` not `ports:`.
**Occupied ports (do not use):** 80, 443, 3000, 3001, 3020-3025, 3040, 3056, 3070-3096, 5432-5435, 5678, 6333, 6379-6385, 8050-8090, 8118-8119, 9090, 11434, 19999
**Full deploy rules:** `~/job-search/deploy-rules.md`

---

## TASK

Create a beautiful **single-page HTML resume** for Alexey Zhuykov.
Style: **Telecom Executive, Bloomberg Terminal gold** — matches alexeyzhuykov.ru brand.

The page must:
- Look like a premium executive-level professional document
- Support **print to PDF** via browser (Ctrl+P or on-page button)
- Be standalone (single HTML file or Vite/React)
- Include a **"Download PDF"** button that calls `window.print()`

---

## DESIGN SYSTEM

MOOD: Bloomberg Terminal meets executive biography. Authoritative, earned depth.
Like a serious person's CV told through architecture, not a marketing brochure.

**COLOR PALETTE:**
```
Background primary:   #0a1628
Background secondary: #0f1f3d
Background tertiary:  #1e3050
Accent primary:       #c9a84c  (warm aged brass/gold)
Accent secondary:     #e8d5a3  (light gold)
Text primary:         #f0ece4
Text secondary:       #8a9ab5
Text dim:             #4a5568
Border:               #1e3050
```

**TYPOGRAPHY:**
Fraunces 800-900 (headlines) + Space Grotesk 400-500 (body)
Google Fonts: `Fraunces:wght@800;900` + `Space+Grotesk:wght@400;500;600;700`

**DECORATIVE ELEMENTS:**
- Gold accent lines: 1px solid #c9a84c (section dividers)
- Subtle diagonal line pattern on bg: SVG, 2px lines, 15% opacity #1e3050
- Faint radial gradient: rgba(201,168,76,0.06) at 20% 50%

**PRINT STYLES:**
```css
@media print {
  body { background: white; color: #1a1a1a; }
  .no-print { display: none !important; }
  .section { page-break-inside: avoid; }
  a { color: #1a1a1a; text-decoration: none; }
  .gold-line { border-color: #1a1a1a; }
}
@page { margin: 15mm 20mm; size: A4; }
```

---

## PAGE STRUCTURE

### HEADER (hidden on print)
Logo: "AZH" in Fraunces 700, #c9a84c, letter-spacing 0.3em
Right: "alexeyzhuykov.ru" Space Grotesk 400, #8a9ab5

---

### SECTION 1: HERO

**Name:** `Alexey Zhuykov`
- Fraunces 900, 48px, #f0ece4
- Above name: gold line 40px + label "RESUME · APRIL 2026" Space Grotesk 400, 11px, letter-spacing 0.25em, #8a9ab5

**Title line:**
"Head of Operations · Technical Director · IT Director"
Space Grotesk 500, 18px, #c9a84c

**Contacts:**
```
📍 Saint Petersburg, Russia (Remote)  📧 alexey.zhuykov@gmail.com  📱 +7 (921) 946-85-35
🔗 alexeyzhuykov.ru  💼 linkedin.com/in/alexeyzhuykov
```
Space Grotesk 400, 13px, #8a9ab5. Links: #c9a84c.

**"Download PDF" button** (class .no-print):
- `[⬇ Download PDF]` — gold bg, text #0a1628, Space Grotesk 600
- onclick: `window.print()`

---

### SECTION 2: KEY STATS

3 stat blocks horizontally (same as alexeyzhuykov.ru home page):
```
19 Years            1 ISP               18 People
In Telecom          Built from scratch  Team managed
```
Numbers: Space Grotesk 700, 56px, #c9a84c.
Labels: Space Grotesk 400, 12px, letter-spacing 0.15em, UPPERCASE, #8a9ab5.

---

### SECTION 3: TARGET ROLE & SUMMARY

**Target roles:** Head of Operations / Technical Director / IT Director
**Industries:** Telecom, ISP, Infrastructure-driven companies

**Professional Summary:**
"Telecom executive with 19 years of uninterrupted CEO experience running a full-cycle ISP in Saint Petersburg, Russia. Built and operated network infrastructure from the ground up — fiber, IP routing, GPON, billing, regulatory compliance (SORM/TSPU/FSB), inter-operator agreements, and P&L — with a team of 18. Currently expanding into AI-augmented operations with production deployments of LLM-based automation tools."

Space Grotesk 400, 16px, #f0ece4, line-height 1.75.

---

### SECTION 4: CORE COMPETENCIES

4 columns:

**Operations Management:**
- Full-cycle ISP management (network → customers → P&L)
- Team leadership up to 18 people: hiring, training, management
- Budgeting, financial planning, P&L
- JSC corporate governance

**Network Infrastructure:**
- Fiber optics, IP/MPLS, GPON, Ethernet switching
- Eltex, Mikrotik RouterOS, Cisco IOS (basics)
- BGP/AS (RIPE allocation), NetBox, NEXUS, AutoCAD, Visio

**Regulatory Compliance:**
- Telecom licensing: Roskomnadzor, FAS, Rossvyaz
- SORM/TSPU: design, FSB handover, operation
- GRCHTS / AS Revizor, RKN blocklist compliance
- Numbering resources, inter-operator agreements

**Billing & Automation:**
- BGBilling (administration, tariffs, contract templates)
- Docker, Linux, CI/CD
- AI tooling in operations
- n8n automation, Python scripting

---

### SECTION 5: EXPERIENCE

Vertical timeline (2px gold line #c9a84c on left).

**Position 1:**
```
March 2007 — April 2026  ·  19 years
Chief Executive Officer
JSC TELSI · Saint Petersburg, Russia
```
"Regional telecommunications operator providing internet access, telephony, and video surveillance services to residential and business customers in Saint Petersburg."

Bullets (gold ▸):
- Built and scaled fiber-optic GPON/Ethernet infrastructure from inception to full operations
- Obtained AS allocation from RIPE; deployed BGP dynamic routing on operator interconnects
- Implemented and administered BGBilling: tariff management, subscriber contracts, CRM integration
- Deployed SORM and TSPU systems per FSB/Roskomnadzor requirements; zero violations across 19 years of inspections
- Negotiated and maintained 10+ inter-operator interconnection agreements; developed technical conditions
- Passed all scheduled and unscheduled RKN and FSB inspections with zero violations over 19 years
- Migrated all infrastructure services to Docker/Docker Compose (zero-downtime)
- Built monitoring stack: Prometheus + Grafana + Uptime Kuma
- Managed 18-person team across technical, customer service, and administrative departments

**Position 2:**
```
November 2021 — March 2026  ·  Concurrent
Chief Executive Officer
LLC Technopark Treugolnik · Saint Petersburg
```
- Commercial real estate management (business technopark)
- Tenant relations coordination, regulatory interactions

**Early Career (2003–2007):**
- LLC Format / Aspect-Plus — Director, retail chain
- LLC Fides — Manager, domain registrar (.com/.net, US partner relationships)
- Media Markt — Head of Sales, first Russia store from fit-out to launch

---

### SECTION 6: OWN PROJECTS

One card with gold border-left 4px:

```
TelecomExpert.ru — Telecom Materials Marketplace
─────────────────────────────────────────────────
A marketplace of regulatory documents, contract templates, technical conditions,
SORM/TSPU compliance guides, and operational materials for small Russian telecom
operators. Search powered by RAG pipeline (Qdrant + Ollama). Open to operators.

[Join us → telecomexpert.ru]
```

---

### SECTION 7: EDUCATION

Two cards side by side:
```
SPbGUAP                                   IPMash RAS
Saint Petersburg State University         Institute for Problems in Mechanical
of Aerospace Instrumentation              Engineering, Russian Academy of Sciences
Degree, 2000                              Postgraduate studies, 2003
```

---

### SECTION 8: LANGUAGES

```
Russian     ████████████  Native
English     ████████░░░░  Professional working proficiency
```

---

### FOOTER

"© 2026 Alexey Zhuykov · alexeyzhuykov.ru · alexey.zhuykov@gmail.com"
Space Grotesk 400, 12px, #8a9ab5.

---

## TECHNICAL REQUIREMENTS

- `<title>Alexey Zhuykov — Telecom Executive Resume</title>`
- `<meta name="description" content="Resume of Telecom Executive Alexey Zhuykov, 19 years ISP">`
- Print button: `onclick="window.print()"`
- Responsive: 320px+
- Dockerfile + nginx for server deployment
