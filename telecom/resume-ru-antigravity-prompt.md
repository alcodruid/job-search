# Anti-Gravity Prompt — Резюме RU (Telecom направление)

---

## ⚠️ DEPLOYMENT RULES — READ BEFORE GENERATING ANY DEPLOY CODE

This site runs on a home server (cyberdub-ai, Ubuntu 24.04). Follow these rules exactly.

**Architecture:** Internet → Caddy (80/443) → Docker containers (internal `n8n_net` network)
**Reverse proxy: CADDY ONLY.** Never nginx, never Apache, never any other proxy.
**Network:** n8n_net (external, already exists). Use `expose:` not `ports:`.
**Occupied ports (do not use):** 80, 443, 3000, 3001, 3020-3025, 3040, 3056, 3070-3096, 5432-5435, 5678, 6333, 6379-6385, 8050-8090, 8118-8119, 9090, 11434, 19999
**Full deploy rules:** `~/job-search/deploy-rules.md`

---

## ЗАДАЧА

Создай красивую **одностраничную HTML-страницу резюме** для Алексея Жуйкова.
Стиль: **Telecom Executive, Bloomberg Terminal gold** — соответствует бренду alexeyzhuykov.ru.

Страница должна:
- Выглядеть как профессиональный представительный документ (executive-level)
- Поддерживать **печать в PDF** через браузер (Ctrl+P или кнопка на странице)
- Быть standalone (один HTML-файл или Vite/React — на выбор Nano Banana)
- Содержать **кнопку "Скачать PDF"** — при клике вызывает `window.print()`

---

## DESIGN SYSTEM

MOOD: Bloomberg Terminal meets executive biography. Authoritative, earned depth.
Like a serious person's CV told through architecture, not a marketing brochure.

**COLOR PALETTE:**
```
Background primary:   #0a1628  (deep navy, near-black)
Background secondary: #0f1f3d  (card background)
Background tertiary:  #1e3050  (borders, hover)
Accent primary:       #c9a84c  (warm aged brass/gold)
Accent secondary:     #e8d5a3  (light gold for highlights)
Text primary:         #f0ece4  (warm off-white)
Text secondary:       #8a9ab5  (muted blue-grey)
Text dim:             #4a5568  (placeholders)
Border:               #1e3050
```

**TYPOGRAPHY:**
```
Headlines H1/H2: Fraunces 800-900 (editorial serif)
Body text:       Space Grotesk 400-500, 15px
Stats/Numbers:   Space Grotesk 700 (oversized)
```

Google Fonts: `Fraunces:wght@800;900` + `Space+Grotesk:wght@400;500;600;700`

**DECORATIVE ELEMENTS:**
- Gold accent lines: 1px solid #c9a84c (section dividers)
- Subtle diagonal line pattern on bg: SVG, 2px lines, 15% opacity #1e3050
- Faint radial gradient: rgba(201,168,76,0.06) at 20% 50%

**LAYOUT:**
- Max content width: 860px, centered
- Print: @media print → white bg, black text, no shadows, no background patterns

---

## PRINT STYLES

```css
@media print {
  body { background: white; color: #1a1a1a; }
  .no-print { display: none !important; }
  .section { page-break-inside: avoid; }
  a { color: #1a1a1a; text-decoration: none; }
  .gold-line { border-color: #1a1a1a; }
}
@page {
  margin: 15mm 20mm;
  size: A4;
}
```

---

## СТРУКТУРА СТРАНИЦЫ

### HEADER

Логотип и навигация (скрыты при печати):
- Лого: "АЖ" в Fraunces 700, #c9a84c, letter-spacing 0.3em
- Правое: "alexeyzhuykov.ru" Space Grotesk 400, #8a9ab5

---

### SECTION 1: HERO

**Имя:** `Жуйков Алексей Юрьевич`
- Fraunces 900, 48px, #f0ece4
- Над именем: gold line 40px + label "РЕЗЮМЕ · АПРЕЛЬ 2026" Space Grotesk 400, 11px, letter-spacing 0.25em, #8a9ab5

**Должность под именем:**
"Директор по операциям · Технический директор · Директор по ИТ"
Space Grotesk 500, 18px, #c9a84c

**Контакты:**
```
📍 Санкт-Петербург (удалённо)  📧 alexey.zhuykov@gmail.com  📱 +7 (921) 946-85-35
🔗 alexeyzhuykov.ru  💼 linkedin.com/in/alexeyzhuykov
```
Space Grotesk 400, 13px, #8a9ab5. Ссылки: #c9a84c.

**Кнопка "Скачать PDF"** (класс .no-print):
- `[⬇ Скачать PDF]` — gold (#c9a84c) bg, text #0a1628, Space Grotesk 600
- onclick: `window.print()`

---

### SECTION 2: КЛЮЧЕВЫЕ КОМПЕТЕНЦИИ

3 stat-блока горизонтально (как на главной alexeyzhuykov.ru):
```
19 лет                    1 ISP                     18 чел.
В телекоме               Построен с нуля            Команда
```
Числа: Space Grotesk 700, 56px, #c9a84c.
Подписи: Space Grotesk 400, 12px, letter-spacing 0.15em, UPPERCASE, #8a9ab5.

---

### SECTION 3: ЦЕЛЕВАЯ ПОЗИЦИЯ И ПРОФИЛЬ

**Заголовок:** "Целевая позиция" + gold line 40px

**Позиции:**
"Директор по операциям / Технический директор / Директор по ИТ"
"Телеком, ISP, инфраструктурные компании"

**Профиль (текст):**
"19 лет управлял телекоммуникационной компанией — от построения инфраструктуры до управления командой и взаимодействия с регуляторами. Знаю телеком изнутри: от физического уровня сети до лицензионных требований и финансовой модели оператора. Параллельно развиваю экспертизу в AI и автоматизации — внедряю современные инструменты в операционные процессы."

Space Grotesk 400, 16px, #f0ece4, line-height 1.75.

---

### SECTION 4: КЛЮЧЕВЫЕ КОМПЕТЕНЦИИ (список)

4 колонки:

**Операционное управление:**
- Управление оператором полного цикла (сеть → клиент → P&L)
- Команда до 18 человек: найм, обучение, управление
- Бюджетирование, финансовое планирование, P&L
- Корпоративное управление АО

**Сетевая инфраструктура:**
- Оптоволокно, IP/MPLS, GPON, Ethernet
- Eltex, Mikrotik RouterOS, Cisco IOS
- BGP/AS (RIPE), NetBox, NEXUS, AutoCAD, Visio

**Регуляторика:**
- Лицензирование РКН, ФАС, Россвязь
- СОРМ/ТСПУ: проектирование, сдача ФСБ, эксплуатация
- ГРЧЦ / АС «Ревизор», реестры РКН
- Ресурс нумерации, договоры присоединения

**Биллинг и автоматизация:**
- BGBilling (администрирование, тарифы, шаблоны)
- Docker, Linux, CI/CD
- AI-инструменты в операционной деятельности
- n8n автоматизация, Python-скрипты

---

### SECTION 5: ОПЫТ РАБОТЫ

Вертикальный timeline (gold вертикальная линия 2px #c9a84c слева).

**Позиция 1:**
```
2007 — 2026  ·  19 лет
Генеральный директор
АО «ТЕЛСИ» · Санкт-Петербург
```
Описание: "Телекоммуникационная компания, оператор связи в СПб. Полное операционное руководство: техника, коммерция, финансы, административная часть."

Буллеты (gold ▸):
- Построил и масштабировал сетевую инфраструктуру GPON/Ethernet с нуля
- Получил AS RIPE, развернул BGP на межоператорских стыках
- Внедрил BGBilling: тарифные планы, шаблоны договоров, CRM-интеграция
- Построил и сдал СОРМ/ТСПУ по требованиям ФСБ и РКН — 0 нарушений за 19 лет
- Вёл 10+ договоров присоединения с операторами (разработка ТУ, переговоры)
- Прошёл все плановые и внеплановые проверки РКН, ФСБ без нарушений
- Мигрировал инфраструктуру на Docker/Docker Compose
- Развернул мониторинг: Prometheus + Grafana + Uptime Kuma
- Управлял командой 18 человек: техника, абонентская служба, администрация

**Позиция 2:**
```
2021 — 2026  ·  по совместительству
Генеральный директор
ООО «Технопарк Треугольник» · Санкт-Петербург
```
- Управление объектами коммерческой недвижимости (технопарк)
- Координация арендных отношений, взаимодействие с регуляторами

**Ранний опыт (2003–2007):**
- ООО «Формат» / «Аспект-плюс» — Директор розничной сети
- ООО «Фидес» — Менеджер, доменный регистратор (.com/.net, US-партнёры)
- Media Markt — Руководитель отдела продаж (первый магазин в России, от отделки до запуска)

---

### SECTION 6: СОБСТВЕННЫЕ ПРОЕКТЫ

Одна карточка с gold border-left 4px:

```
TelecomExpert.ru — Маркетплейс материалов для операторов связи
─────────────────────────────────────────────────────────────────
Маркетплейс нормативных документов, шаблонов договоров и технических условий,
руководств по СОРМ/ТСПУ и методических материалов для малых операторов связи РФ.
Поиск — RAG-пайплайн (Qdrant + Ollama). Открыт для участия операторов.

[Присоединиться → telecomexpert.ru]
```

---

### SECTION 7: ОБРАЗОВАНИЕ

Две карточки рядом:
```
СПбГУАП                              ИПМаш РАН
Санкт-Петербургский ГУАП             Институт проблем машиноведения РАН
Диплом, 2000                         Аспирантура, 2003
```

---

### SECTION 8: ЯЗЫКИ

```
Русский      ████████████  Родной
Английский   ████████░░░░  Профессиональный (техническая документация, переписка)
```

---

### FOOTER

"© 2026 Жуйков Алексей Юрьевич · alexeyzhuykov.ru · alexey.zhuykov@gmail.com"
Space Grotesk 400, 12px, #8a9ab5.

---

## ТЕХНИЧЕСКИЕ ТРЕБОВАНИЯ

- `<title>Жуйков Алексей — Резюме Telecom Executive</title>`
- `<meta name="description" content="Резюме директора по операциям, 19 лет телеком">`
- Кнопка: `onclick="window.print()"`
- Responsive: 320px+
- Dockerfile + nginx для деплоя на сервер
