# Anti-Gravity Prompt — Резюме RU (AI-направление)

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
  resume-ru:
    build: .
    container_name: resume-ru
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

## ЗАДАЧА

Создай красивую **одностраничную HTML-страницу резюме** (resume page) для Алексея Жуйкова.
Стиль: **AI-инженер, dark terminal aesthetic** — соответствует бренду cyberdub.su.

Страница должна:
- Выглядеть как профессиональный документ с высокохудожественным дизайном
- Поддерживать **печать в PDF** через браузер (Ctrl+P или кнопка на странице)
- Быть standalone (один HTML-файл или Vite/React — на выбор Nano Banana)
- Содержать **кнопку "Скачать PDF"** — при клике вызывает `window.print()`

---

## DESIGN SYSTEM

MOOD: "Private GPU server meets hacker's portfolio meets senior engineering blog"
Feeling: Не стартап, не академический. Человек, который реально шипит продукты.

**COLOR PALETTE:**
```
Background primary:   #0d1117  (GitHub dark — near-black)
Background secondary: #161b22  (чуть светлее, для карточек)
Background tertiary:  #1c2128  (code blocks, hover states)
Accent primary:       #00d4ff  (electric cyan — активное состояние)
Accent secondary:     #00ff88  (neon green — успех, "работает")
Accent warning:       #ffb347  (amber — статистика, выделения)
Text primary:         #e6edf3  (near-white)
Text secondary:       #7d8590  (muted grey — как комментарии в коде)
Text dim:             #484f58  (очень muted — placeholders, рамки)
Border:               #30363d  (dark grey, GitHub-style)
Code text:            #a5d6ff  (light blue — syntax highlighting)
```

**TYPOGRAPHY:**
```
Headlines H1/H2: "Space Grotesk" 700-800
Body text:       "Space Grotesk" 400-500, 15px
Code/Technical:  "JetBrains Mono" 400-500
                 (имена технологий, теги, числа-статистика)
```

Google Fonts: Space Grotesk 400,500,700,800 + JetBrains Mono 400,500

**TAG CHIPS для технологий:**
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
- Максимальная ширина контента: 860px, центрированный
- Два варианта раскладки: для web (с боковым отступом и тенями) и print (белый фон, чёрный текст)
- На web: тёмный фон, свечение, тени
- На печать (@media print): белый фон, чёрный текст, никаких теней и анимаций

---

## PRINT STYLES

```css
@media print {
  body { background: white; color: #1a1a1a; }
  .no-print { display: none !important; }
  .section { page-break-inside: avoid; }
  a { color: #1a1a1a; text-decoration: none; }
  /* убрать все свечения, анимации, box-shadows */
}
@page {
  margin: 15mm 20mm;
  size: A4;
}
```

---

## СТРУКТУРА СТРАНИЦЫ

### HEADER (шапка)

Терминальная строка вверху:
```
> cv.cyberdub.su                                          [RU] [EN]
```
- Логотип: `> cv.cyberdub.su` в JetBrains Mono, #00d4ff
- Переключатель языка (декоративный): [RU] активный amber, [EN] #7d8590
- Sticky только на web-версии, на печати — скрыт

---

### SECTION 1: HERO — Личные данные

**Имя:** `Жуйков Алексей Юрьевич`
- Размер: 42px, Space Grotesk 800, #e6edf3
- Декоративная строка перед именем: `$ whoami` в JetBrains Mono, #7d8590, 14px

**Должность под именем:**
```
Senior AI Engineer · LLM Infrastructure Engineer · Head of AI
```
- Space Grotesk 500, 18px, #00d4ff

**Контакты — горизонтальная строка:**
```
📍 Санкт-Петербург (удалённо)
📧 alexey.zhuykov@gmail.com
📱 +7 (921) 946-85-35
🔗 cyberdub.su
🐙 github.com/alcodruid
💼 linkedin.com/in/alexeyzhuykov
```
- JetBrains Mono 400, 13px, #7d8590
- Ссылки: #00d4ff, hover: underline

**Кнопка "Скачать PDF"** справа в шапке:
- `[⬇ Скачать PDF]` — amber (#ffb347), JetBrains Mono, border 1px solid #ffb347
- onclick: `window.print()`
- Класс `.no-print` — скрыта при печати

---

### SECTION 2: О себе (Профессиональный профиль)

Терминальный компонент (dark box с traffic-light dots):
```
╭─ about.md ──────────────────────────────────────────────────╮
│                                                              │
│  Практикующий AI-инженер с собственной GPU-инфраструктурой  │
│  в продакшне. Развернул и поддерживаю несколько AI-систем:  │
│  RAG-сервисы, LLM-агенты, автоматизационные пайплайны,       │
│  Telegram-боты с AI-ядром. Специализация — приватное          │
│  развёртывание LLM для enterprise: модели работают на        │
│  собственном железе клиента, данные не покидают контур.      │
│                                                              │
│  19 лет управленческого опыта в телекоме дают понимание     │
│  enterprise-требований: надёжность, compliance, SLA,         │
│  масштабируемость.                                           │
╰──────────────────────────────────────────────────────────────╯
```

Реализация: div с border 1px solid #30363d, background #161b22, border-radius 8px.
Шапка: `about.md` в JetBrains Mono + traffic-light dots (⬤ красный #ff5f57, ⬤ жёлтый #ffbd2e, ⬤ зелёный #28ca41).

---

### SECTION 3: Технический стэк

**Заголовок:** `$ cat stack.json` в JetBrains Mono, #7d8590

4 карточки в сетке 2×2 (на мобиле — 1 колонка):

**Карточка 1: LLM & AI**
```
LLM & AI
─────────────────────────────────
Ollama    vLLM    Hugging Face
qwen2.5:32b    devstral:24b
qwen3-coder:30b    llava (vision)
Fine-tuning · LoRA · PEFT
Prompt Engineering
RAG-архитектуры
Agentic системы · Function calling
```

**Карточка 2: Vector & Embeddings**
```
Vector Databases
─────────────────────────────────
Qdrant (production)
bge-m3 (1024-dim)
nomic-embed-text (768-dim)
mxbai-embed-large
Semantic search · Hybrid search
```

**Карточка 3: Автоматизация**
```
Automation & Orchestration
─────────────────────────────────
n8n    Python    FastAPI
asyncio · httpx · SQLAlchemy
Telegram Bot API (PTB 22+)
Docker    Docker Compose
Caddy    PostgreSQL    Redis
```

**Карточка 4: Инфраструктура**
```
Infrastructure
─────────────────────────────────
Linux (Ubuntu Server 24.04)
NVIDIA Tesla P40 24GB VRAM
CUDA · GPU memory management
Prometheus · Grafana
Netdata · Uptime Kuma
GitHub Actions · Bash
```

Каждая карточка: border #30363d, background #161b22, заголовок #00d4ff JetBrains Mono.
Технологии — tag chips (см. Design System).

---

### SECTION 4: AI-проекты

**Заголовок:** `$ ls ~/projects/` в JetBrains Mono, #7d8590

6 карточек проектов. Каждая:
- Верх: статус-строка `[PROD]` в зелёном / `[WIP]` в amber
- Название проекта: Space Grotesk 700, #e6edf3
- Одна строка описания: #7d8590, 14px
- Стэк: tag chips
- Hover: border #00d4ff, background #1c2128

**Проект 1:**
```
[PROD] Replyo — AI CRM для бизнеса
Умная CRM с RAG-ядром: обучение на базе знаний клиента, 
классификация обращений, генерация ответов, Telegram-интеграция.
Стэк: [qwen2.5:32b] [qwen2.5:7b] [nomic-embed-text] [Qdrant] [n8n] [Python] [Docker]
```

**Проект 2:**
```
[PROD] TelecomExpert — RAG по телеком-документации
Полный RAG-пайплайн: загрузка → чанкинг → индексирование → retrieval → генерация.
Стэк: [bge-m3 1024-dim] [Qdrant] [qwen2.5:32b] [FastAPI] [Docker]
```

**Проект 3:**
```
[PROD] Job Matcher — AI-сервис подбора вакансий
Telegram-бот: анализ резюме, сопоставление с вакансиями, подготовка к интервью.
Стэк: [qwen2.5:32b] [Python] [PTB 22.7] [PostgreSQL]
```

**Проект 4:**
```
[PROD] FinPulse — AI-дайджест финансовых новостей
Автосбор из Telegram-каналов → LLM-анализ → структурированный дайджест 2×/день.
Стэк: [n8n] [qwen2.5:32b] [Telegram Bot API] [Python]
```

**Проект 5:**
```
[WIP] SNT-Пилот — AI-сервис для управляющих СНТ
Мобильное приложение + backend: учёт участков, претензионная работа, уведомления.
Стэк: [React Native] [FastAPI] [PostgreSQL] [qwen2.5:32b]
```

**Проект 6:**
```
[WIP] AI-CFO — AI-ассистент финансового анализа
Маркетплейс AI-инструментов для финансовых директоров.
Стэк: [qwen2.5:32b] [Qdrant] [n8n] [React] [FastAPI]
```

---

### SECTION 5: Опыт работы

**Заголовок:** `$ cat experience.log` в JetBrains Mono, #7d8590

**Позиция 1:**
```
Генеральный директор / DevOps + AI практик
АО «ТЕЛСИ» · Санкт-Петербург · март 2007 — апрель 2026 (19 лет)
```
Телекоммуникационная компания, оператор связи.
Параллельно с управлением компанией: построение серверной инфраструктуры,
внедрение DevOps-практик, запуск AI-инструментов в операционной деятельности.

Буллеты (с иконкой `▸` в #00d4ff):
- Миграция всей инфраструктуры на Docker/Docker Compose (zero-downtime)
- Мониторинг-стэк: Prometheus + Grafana + Uptime Kuma
- Развёртывание приватного Ollama LLM-сервера для внутренних задач
- Автоматизация операционных процессов через n8n + Python-скрипты
- Управление командой 18 человек: техника, коммерция, финансы

---

### SECTION 6: GPU-инфраструктура

Терминальный компонент:
```
$ docker ps --format "{{.Names}}\t{{.Status}}"

cyberdub-ai infrastructure (running 24/7):
├── ollama          [UP] qwen2.5:32b · devstral:24b · qwen3-coder:30b · llava
├── qdrant          [UP] collections: telecom-docs · job-listings · kb-replyo
├── n8n             [UP] workflows: 47 active
├── prometheus      [UP] scraping: 12 targets
├── grafana         [UP] dashboards: 8
└── caddy           [UP] TLS: cyberdub.su · cv.cyberdub.su

GPU: NVIDIA Tesla P40 · 24GB VRAM · CUDA 12.x
OS:  Ubuntu Server 24.04 LTS
```

---

### SECTION 7: Образование

Две карточки рядом:

```
СПбГУАП                          ИПМаш РАН
Санкт-Петербургский ГУАП         Институт проблем машиноведения РАН
Диплом, 2000                     Аспирантура, 2003
```

---

### SECTION 8: Языки

```
Русский     ████████████  Родной
Английский  ████████░░░░  Профессиональный (техническая документация, переписка)
```

Полоски: #00d4ff заполнение, #30363d фон.

---

### FOOTER

```
> Последнее обновление: апрель 2026
> alexey.zhuykov@gmail.com · cyberdub.su · github.com/alcodruid
```

JetBrains Mono, #484f58, 12px.

---

## ТЕХНИЧЕСКИЕ ТРЕБОВАНИЯ

- Один `index.html` с инлайн-CSS или Vite+React — на выбор
- Google Fonts подключить через `<link>`
- Никаких внешних зависимостей кроме Google Fonts
- Кнопка печати: `onclick="window.print()"`
- `<title>Жуйков Алексей — AI Engineer</title>`
- `<meta name="description" content="Резюме AI-инженера Алексея Жуйкова">`
- Responsive: работает на мобиле (320px+) и десктопе

---

**Сохранить результат в:** `resume-ru/index.html` с Dockerfile для деплоя на nginx.
