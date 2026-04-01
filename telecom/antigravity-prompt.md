# Anti-Gravity Prompts — alexeyzhuykov.ru

## PAGE 1: HOME (index page)

Create a single-page website section for the HOME page of a personal branding website 
for Alexey Zhuykov, a Telecom Executive. This is the first page visitors see.

### Design System

MOOD: Bloomberg Terminal meets executive biography. Authoritative, earned depth. 
Like a serious person's life story told through architecture, not marketing brochure.

COLOR PALETTE:
- Main background: #0a1628 (deep navy, near-black)
- Card/section background: #0f1f3d
- Primary accent: #c9a84c (warm aged brass/gold)
- Secondary accent: #e8d5a3 (light gold for highlights)  
- Primary text: #f0ece4 (warm off-white)
- Secondary text: #8a9ab5 (muted blue-grey)
- Borders: #1e3050

FONTS (load from Google Fonts):
- Headlines: Fraunces, weight 800-900 (serif, editorial)
- Body: Space Grotesk, weight 400-500 (geometric sans)
- Numbers/Stats: Space Grotesk, weight 700, oversized

ANIMATIONS:
- Page load: elements stagger in with translateY(30px) → 0, opacity 0 → 1
- Each element delays by 150ms from the previous
- Easing: cubic-bezier(0.22, 1, 0.36, 1)
- Gold accent lines: draw-in animation from left (scaleX 0→1)

BACKGROUND TREATMENT:
Apply a subtle radial gradient: 
radial-gradient(ellipse at 20% 50%, rgba(201, 168, 76, 0.06) 0%, transparent 60%)
Add a very faint diagonal line pattern (SVG, 2px lines, 15% opacity #1e3050)

### Page Structure

**SECTION 1: Navigation Bar**
- Left: Text logo "AZH" in Fraunces 700, color #c9a84c, letter-spacing 0.3em
- Right: Navigation links (Space Grotesk 400, #8a9ab5): About | Expertise | Resume | Contact
- Navigation links hover: color transition to #c9a84c with 0.2s ease
- Bottom border: 1px solid #1e3050
- Background: #0a1628 with backdrop-filter blur(10px), sticky on scroll
- Mobile: hamburger menu, same colors

**SECTION 2: Hero — Full viewport height**

Layout: Two-column on desktop (60% text / 40% photo), single column on mobile

LEFT COLUMN — Text content:
- Overline text (top label): 
  "TELECOM EXECUTIVE · SAINT PETERSBURG · REMOTE-READY"
  Font: Space Grotesk 400, size 11px, letter-spacing 0.25em, color #8a9ab5
  Add a 1px gold line (#c9a84c) of 40px width to the left of this text

- Main headline (H1), split into two lines:
  Line 1: "19 Years" — Fraunces 900, 96px desktop / 56px mobile, color #f0ece4
  Line 2: "in Telecom." — Fraunces 900, 96px desktop / 56px mobile, color #c9a84c
  
- Subheadline (H2):
  "Every Role. End to End." 
  Fraunces 400 italic, 32px desktop / 24px mobile, color #8a9ab5

- Descriptor paragraph:
  "Built, operated, and led a telecom company for nearly two decades — 
  from routing tables to regulatory filings, from fiber deployments to P&L. 
  Now bringing that depth, plus modern AI tooling, to operations leadership."
  Font: Space Grotesk 400, 17px, color #f0ece4, line-height 1.75, max-width 520px

- CTA Button Row (two buttons, horizontal, gap 16px):
  Button 1 (Primary): "Download Resume" 
    Background: #c9a84c, text: #0a1628, font: Space Grotesk 600, 14px, letter-spacing 0.1em
    Padding: 14px 28px, border-radius: 2px (nearly square, not pill)
    Hover: background #e8d5a3, transform scale(1.02)
  Button 2 (Secondary): "View LinkedIn ↗"
    Border: 1px solid #c9a84c, text: #c9a84c, background: transparent
    Same sizing as Button 1
    Hover: background rgba(201, 168, 76, 0.1)

RIGHT COLUMN — Photo area:
  - Container: 300×300px circle on desktop
  - Background placeholder: radial gradient #1e3050 → #0f1f3d
  - Gold ring: 2px solid #c9a84c, 8px offset (ring separated from photo)
  - Center text when no photo: Initials "АЖ" in Fraunces 700, 64px, #c9a84c
  - Subtle outer glow: box-shadow 0 0 60px rgba(201, 168, 76, 0.15)

**SECTION 3: Three Key Stats Bar**

Full-width horizontal bar with dark separator line above and below (#1e3050)
Background: #0f1f3d
Three equal columns, centered content, padding 48px 0

Stat 1:
  Number: "19" — Space Grotesk 700, 72px, color #c9a84c
  Label: "Years Leading Telecom" — Space Grotesk 400, 13px, #8a9ab5, letter-spacing 0.15em, UPPERCASE

Stat 2:
  Number: "1" — Space Grotesk 700, 72px, color #c9a84c
  Sub: "ISP" — Space Grotesk 400, 32px, color #f0ece4 (inline with number)
  Combined: "1 ISP" — large
  Label: "Built from Ground Up" — Space Grotesk 400, 13px, #8a9ab5

Stat 3:
  Number: "18" — Space Grotesk 700, 72px, color #c9a84c
  Label: "Person Team Managed" — Space Grotesk 400, 13px, #8a9ab5

Vertical dividers between columns: 1px solid #1e3050

**SECTION 4: Expertise Preview (teaser)**

Section header:
  "Areas of Expertise" — Space Grotesk 400, 11px, letter-spacing 0.3em, #8a9ab5, UPPERCASE
  Followed by: horizontal gold line (#c9a84c) 1px, width 60px

Three horizontal card rows (not grid — stacked horizontally on desktop):

Card 1: 
  Icon area: Left-aligned square 48×48, background #1e3050, gold border 1px
  Icon: Network/node SVG icon, color #c9a84c
  Title: "Telecom Operations" — Fraunces 700, 22px, #f0ece4
  Desc: "Full-cycle ISP management: infrastructure, billing, regulatory compliance, P&L"
  — Space Grotesk 400, 15px, #8a9ab5

Card 2:
  Icon: Team/people SVG
  Title: "Team & Operations Leadership"
  Desc: "19 years building and managing technical teams, vendor relationships, and multi-year capex plans"

Card 3:
  Icon: Circuit/AI SVG
  Title: "AI-Enhanced Operations"
  Desc: "Deploying LLM tools and automation pipelines into operational workflows"

Card hover effect: background transition to #0f1f3d, left border 3px solid #c9a84c

Link at bottom: "Full expertise →" — Space Grotesk 500, #c9a84c, hover underline

**SECTION 5: Footer Strip**
Minimal: one line
Left: "© 2026 Alexey Zhuykov" — Space Grotesk 400, 13px, #8a9ab5
Right: "alexeyzhuykov.ru" — same
Center: dot separators between "About · Expertise · Resume · Contact" links
Background: #060e1d (darker than main bg)
Top border: 1px solid #1e3050
Padding: 24px 0

### Responsive Breakpoints
- Desktop: 1200px+ (two-column hero)
- Tablet: 768-1199px (two-column hero, reduced sizes)  
- Mobile: <768px (single column, H1 56px, stats stack vertically)

### Technical Notes
- All fonts loaded via @import from Google Fonts
- CSS custom properties for all colors (easy theming)
- Intersection Observer for scroll animations (not just load animations)
- No JavaScript frameworks — pure HTML/CSS/vanilla JS
- Meta tags: og:title, og:description, og:image for LinkedIn sharing

---

## PAGE 2: ABOUT

Create the ABOUT page for alexeyzhuykov.ru. Use the same design system as the Home page
(same colors, fonts, nav, footer).

### Page-specific content and layout

**Page Header:**
Below the nav, full-width header section:
  Label: "ABOUT" — Space Grotesk 400, 11px, letter-spacing 0.3em, #8a9ab5
  H1: "The Long Way Around" — Fraunces 900, 72px desktop / 44px mobile, #f0ece4
  Subhead: "Nineteen years isn't a number. It's a decision made once, and kept every year."
  — Fraunces 400 italic, 24px, #8a9ab5
  Horizontal gold separator line below

**Section: Career Timeline**

Header: "Career Timeline" — same style as Expertise Preview section header

Timeline layout: vertical timeline on left side (gold vertical line 2px #c9a84c)
Each entry: dot on the line (circle 10px, filled #c9a84c), content to the right

Timeline Entry 1:
  Year: "2007 — 2026" — Space Grotesk 700, 14px, #c9a84c
  Role: "CEO & General Director" — Fraunces 700, 28px, #f0ece4
  Company: "АО ТЕЛСИ + ЗАО ТЕЛСИ 2, Saint Petersburg" — Space Grotesk 500, 15px, #8a9ab5
  Body (Space Grotesk 400, 15px, #f0ece4, max-width 600px):
  "Joined the telecom group and was appointed CEO within the first two weeks. 
  For the next 19 years, served as the sole executive authority over all company functions: 
  network engineering, customer operations, regulatory compliance, finance, and team management.
  
  Built fiber-optic infrastructure from scratch, navigated Russian telecom regulation 
  (Roskomnadzor, FSB licensing, SORM), managed billing systems (BGBilling), and kept 
  a lean 18-person team running efficient, profitable operations through nearly two decades 
  of market changes.
  
  In later years: modernized infrastructure with Docker containerization, deployed monitoring 
  stacks (Prometheus + Grafana), and introduced AI-powered automation into operational workflows."

Timeline Entry 2:
  Year: "2021 — 2026"
  Role: "CEO (concurrent)"
  Company: "ООО Технопарк Треугольник"
  Body: "Concurrent executive role managing a commercial real estate technopark. 
  Oversaw tenant operations, administrative management, and regulatory interactions."

Timeline Entry 3:
  Year: "2025 — present"
  Role: "CEO (concurrent)"
  Company: "ООО ЕвроСтройИнвест"
  Body: "Investment asset and real estate management, concurrent role."

Timeline Entry 4:
  Year: "2014 — 2019"
  Role: "Digital Publisher"
  Company: "Yandex Advertising Network Partner (concurrent)"
  Body: "Built and monetized content websites via Yandex RSY. 
  First hands-on experience with SEO, web analytics, and digital audience building."

Timeline Entry 5:
  Year: "2001"
  Role: "Research"
  Company: "FSBSI Institute for Problems in Mechanical Engineering, Russian Academy of Sciences"
  Body: "Early career, scientific research environment."

**Section: What I Believe**

Three-column philosophy cards (same card style as expertise cards):

Card 1 — Title: "Depth over breadth"
Text: "19 years in one industry isn't a limitation — it's the only way to actually understand something. I know telecom end-to-end because I had to. There was no one else."

Card 2 — Title: "Own the whole thing"
Text: "When you're a 18-person company, you learn not to specialize. The CEO also configures the routers, reviews the contracts, and handles the FSB inspector. That habit doesn't go away."

Card 3 — Title: "Technology as leverage"
Text: "AI doesn't replace operations expertise — it amplifies it. I've seen what automation can do when the person building it actually understands the operations being automated."

**Section: Technical Profile**
(Bridge to AI competencies — brief, not a full stack listing)

Paragraph: "Alongside executive work, I've maintained deep technical practice. The server room was always mine. Docker deployments, monitoring stacks, and in recent years — LLM infrastructure and AI product development. See the full technical portfolio at cyberdub.su"

Link: "cyberdub.su →" styled as gold button

**Contact CTA at bottom:**
Centered call to action:
  Text: "Open to remote operations leadership and AI roles"
  Button: "Get in touch" — primary gold button
  Secondary: "Download Resume" — secondary outlined button

---

## PAGE 3: EXPERTISE

Create the EXPERTISE page for alexeyzhuykov.ru. Use the same design system.

### Content

**Page Header:**
  Label: "EXPERTISE"
  H1: "What 19 Years Teaches You"
  Subhead: "Not a list of tools. A map of what I can actually do."

**Expertise Area 1: Telecom Operations**

Large section header: "Telecom Operations" — Fraunces 900, 48px, #f0ece4
Gold left border accent (4px solid #c9a84c, 60px tall, left-aligned)

Two-column grid of skill cards (4 cards total):

Card A — "Network Infrastructure"
Body: "Designed and operated fiber-optic networks (GPON, Ethernet, IP routing). 
Hands-on with Eltex platforms, Mikrotik RouterOS, Cisco IOS basics. 
Built networks that have been running for 15+ years without major incidents."
Tags: [GPON] [IP Routing] [Eltex] [Mikrotik] [Fiber Optics]

Card B — "Billing & BSS"
Body: "Full cycle BGBilling administration: tariff design, subscriber management, 
payment integration, reporting. Built custom tariff logic and automation scripts 
for subscriber lifecycle management."
Tags: [BGBilling] [BSS] [Tariff Design] [Subscriber Management]

Card C — "Regulatory Compliance"
Body: "19 years of Russian telecom regulatory compliance: Roskomnadzor licensing, 
FSB SORM system deployment and maintenance, TSPU integration, annual regulatory inspections. 
Zero violations in 19 years."
Tags: [SORM] [TSPU] [Licensing] [Roskomnadzor] [FSB]

Card D — "Network Inventory"
Body: "Implemented and maintained NetBox as the single source of truth for all 
network assets. NEXUS for additional inventory management. Full documentation culture."
Tags: [NetBox] [NEXUS] [Asset Management]

**Expertise Area 2: Operations Leadership**

Section header: "Operations & Team Leadership" — same style

Card A — "P&L Management"
Body: "Full financial ownership: budgeting, capex planning, opex optimization, 
vendor negotiations, pricing strategy. Maintained profitability through 19 years 
of market changes including two major economic cycles."
Tags: [P&L] [Budgeting] [Capex Planning] [Vendor Management]

Card B — "Team Building"
Body: "Hired, trained, and retained a 18-person technical team: network engineers, 
customer service, administrative staff. Built a culture where people stayed for years 
in a competitive market."
Tags: [Team Leadership] [Hiring] [Operations Management]

Card C — "Vendor & Regulatory Relations"
Body: "Long-term relationships with equipment vendors (Eltex, Mikrotik), 
upstream providers, government regulators (FSB, Roskomnadzor, FAS). 
Experience negotiating and managing multi-year contracts."
Tags: [Vendor Management] [Government Relations] [Contract Negotiation]

**Expertise Area 3: AI-Enhanced Operations**

Section header: "AI & Modern Infrastructure" — Fraunces 900, 48px
Subtext: "Practical tooling built and deployed, not theoretical knowledge"

Card A — "LLM Deployment"
Body: "Private LLM server running Ollama with multiple models in production: 
qwen2.5:32b, devstral:24b, llava (vision). Experience with model selection, 
GPU memory management, inference optimization for multi-model environments."
Tags: [Ollama] [LLM] [GPU] [Private AI]

Card B — "RAG Systems"
Body: "Built production RAG pipelines: document ingestion, chunking strategies, 
embedding model selection (bge-m3, nomic-embed-text), Qdrant vector database, 
retrieval tuning, generation quality evaluation."
Tags: [RAG] [Qdrant] [Embeddings] [bge-m3]

Card C — "Automation Pipelines"
Body: "Complex multi-step automation using n8n and Python: webhook integrations, 
Telegram bot backends, LLM-powered data processing workflows, 
scheduled AI tasks."
Tags: [n8n] [Python] [FastAPI] [Automation] [Docker]

**Bottom CTA:**
  Text: "Want the full AI engineering portfolio?"
  Link button: "Visit cyberdub.su →" — gold outlined button

---

## PAGE 4: RESUME / DOWNLOADS

Create the RESUME page for alexeyzhuykov.ru. Same design system.

### Content

**Page Header:**
  Label: "RESUME"
  H1: "Download My CV"
  Subhead: "Available in Russian and English. PDF format."

**Download Cards:**

Two large cards, side by side (desktop), stacked (mobile):

Card 1 — Russian Resume:
  Flag emoji or RU icon
  Title: "Резюме — Русский"
  Subtitle: "Для российских работодателей и ES-агентств"
  Content preview list (Space Grotesk 400, 14px, #8a9ab5):
    • Полный опыт работы · 4 страницы
    • Компетенции и технические навыки
    • Формат: PDF, А4
  Download Button: "Скачать резюме (RU)" — primary gold
  File info: "resume-zhuykov-ru.pdf · ~250kb" — tiny text below button

Card 2 — English Resume:
  Flag emoji or EN icon
  Title: "Resume — English"
  Subtitle: "For international opportunities and LinkedIn"
  Content preview list:
    • Full work history · 4 pages
    • Skills and technical competencies
    • Format: PDF, A4
  Download Button: "Download Resume (EN)" — primary gold
  File info: "resume-zhuykov-en.pdf · ~250kb"

**Section: Key Highlights (below download cards)**

Four-item stat strip (same as home page stats bar style):
  • 19 years executive experience
  • Full-cycle ISP operations
  • Team leadership (18 people)
  • Remote-ready / Saint Petersburg

**Contact Section:**
  Heading: "Prefer to reach out directly?"
  Email: info@sntpilot.ru (mailto link, gold colored)
  Phone: +7 (921) 946-85-35
  LinkedIn: linkedin.com/in/alexeyzhuykov
  Location note: "Saint Petersburg, Russia — Available for remote roles worldwide"

---

## PAGE 5: CONTACT

Create the CONTACT page for alexeyzhuykov.ru. Same design system.

### Content

**Page Header:**
  Label: "CONTACT"
  H1: "Let's Talk"
  Subhead: "Available for operations leadership and consulting discussions."

**Two-column layout:**

Left column (60%): Contact form
  Fields (Space Grotesk 400, inputs with dark bg #0f1f3d, gold focus border):
    - Name (text input): placeholder "Your name"
    - Email (email input): placeholder "your@email.com"  
    - Company/Organization (text): placeholder "Company (optional)"
    - Message (textarea, 5 rows): placeholder "What are you looking for?"
    - Subject radio group: 
      ○ Operations Leadership Role
      ○ Technical Consulting
      ○ Just getting in touch
  Submit button: "Send Message" — full-width gold button
  Note below: "Usually respond within 24 hours"

Right column (40%): Direct contacts
  Section title: "Direct Contacts" — Fraunces 700, 24px
  
  Contact row 1: Email
    Icon: envelope SVG (gold)
    Label: "Email" — Space Grotesk 500, 13px, #8a9ab5
    Value: "info@sntpilot.ru" — Space Grotesk 500, 16px, #f0ece4, link

  Contact row 2: Phone
    Icon: phone SVG
    Label: "Phone"
    Value: "+7 (921) 946-85-35"

  Contact row 3: LinkedIn
    Icon: LinkedIn SVG
    Label: "LinkedIn"
    Value: "linkedin.com/in/alexeyzhuykov" — external link with ↗

  Contact row 4: AI Portfolio
    Icon: terminal SVG (gold)
    Label: "AI Engineering"
    Value: "cyberdub.su" — external link

  Separator

  Location block:
    "Based in: Saint Petersburg, Russia"
    "Timezone: UTC+3 (Moscow)"
    "Available: Remote worldwide"

