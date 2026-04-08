# Friends — Expert Panel Results

> Date: 2026-04-09
> Panel type: Custom (Product/Startup concept evaluation)
> Input: docs/SDD.md, docs/origin-transcript.md
> Requested by: Tim Zinin

---

## Scope

**What:** Evaluate viability and refine the concept of "Friends" — a knowledge-graph-based matching protocol that connects people through AI conversations, markdown files, wearables, and DNA data. Distributed as a Claude Code skill with privacy-first architecture.

**Constraints:**
- Two-person founding team (Tim + Denis)
- Existing infrastructure: Contabo VPS 30, GitHub Pages (timzinin.com), Claude Code skill ecosystem
- Budget: minimal (bootstrap, free-tier preference)
- Timeline: MVP landing page first, then iterate

**Blast radius:** `business-critical` — involves personal data, DNA, health info, potential GDPR/HIPAA implications

**Decision type:** Designing from scratch + stress-testing the concept

---

## Panel Roster

| # | Role | Expert | Bias |
|---|------|--------|------|
| 1 | Product Strategist | PS | Product-market fit & positioning |
| 2 | Privacy/Crypto Architect | PCA | Zero-trust & regulatory compliance |
| 3 | Growth Engineer | GE | Distribution & viral mechanics |
| 4 | System Architect | SA | Technical feasibility & scalability |
| 5 | Behavioral Psychologist | BP | User motivation & trust dynamics |
| 6 | Monetization Expert | ME | Revenue sustainability |
| 7 | Devil's Advocate | DA | Failure modes & ethics |

---

## Transcript Idea Map — Дословный разбор каждой концепции

> Ниже — каждая идея из разговора Tim + Denis (Standard Recording 10), с точным цитированием и экспертной оценкой панели.

---

### ИДЕЯ 1: Дейтинг-приложение на основе скиллов в Claude
**Цитата:** *"мы обсуждаем дейтинг приложение которое будет мэчить людей мужчин и женщин основании скилла в клоде"*
**Таймкод:** 0:00–0:06

| Эксперт | Оценка |
|---------|--------|
| PS | Сильная стартовая точка — "matching by how you think" уникально. Но слово "дейтинг" сразу ставит продукт в crowded market с 99% failure rate. |
| DA | Прямой конкурент — весь dating app рынок. Отстроиться фразой "по скиллам" недостаточно. OkCupid тоже матчил "по совместимости" — не помогло. |
| **Вердикт** | **Переформулировать: не "дейтинг", а "knowledge networking protocol".** Дейтинг = регуляции, модерация, safety. Networking = свобода. |

---

### ИДЕЯ 2: Не только романтика — просто партнёры, друзья, интересные контакты
**Цитата:** *"просто партнеров... не обязательно чтобы должна быть личная романтическая история это может быть просто интересный контакт то есть который друг о котором ты даже не знал что существует в мире"*
**Таймкод:** 0:06–0:37

| Эксперт | Оценка |
|---------|--------|
| PS | Это ПРАВИЛЬНЫЙ framing. "Друг, о котором ты не знал" — это killer hook. Гораздо сильнее, чем "дейтинг по markdown". |
| BP | Психологически точно: люди хотят serendipity (случайных открытий). "Друг, о котором не знал" = дофаминовый триггер новизны. |
| GE | Эта формулировка вирусна. "I found a friend I didn't know existed" — идеальный Twitter-пост. |
| **Вердикт** | **КЛЮЧЕВОЙ HOOK продукта. Использовать в landing page дословно: "Find the friend you didn't know existed."** |

---

### ИДЕЯ 3: Данные из markdown-файлов (Claude + любые)
**Цитата:** *"собирается опустосированная информация по markdown файлам которые человек обсуждал с клодом или не только клодом вообще markdown файлом на его компьютере"*
**Таймкод:** 0:13–0:23

| Эксперт | Оценка |
|---------|--------|
| SA | Технически реализуемо. `~/.claude/` содержит session history. Markdown files — glob `**/*.md`. Парсинг дешёвый. |
| PCA | ВНИМАНИЕ: markdown может содержать пароли, API-ключи, личные дневники. Нужен whitelist/blacklist путей + preview перед отправкой. |
| DA | Проблема аудитории: кто кроме разработчиков имеет markdown-файлы? Это ограничивает TAM. |
| **Вердикт** | **Для MVP — только markdown. Но обязательно: 1) preview что будет анализироваться, 2) exclude patterns (.env, credentials), 3) user consent per-directory.** |

---

### ИДЕЯ 4: Название "Friends" (как сериал)
**Цитата:** *"может быть скилл friends ok friends хорошие названия может быть даже friends да все любят сериал friends прикольно"*
**Таймкод:** 0:37–0:52

| Эксперт | Оценка |
|---------|--------|
| PS | Название тёплое, запоминающееся, без технического жаргона. Ассоциация с сериалом — бонус для узнаваемости. НО: trademark issues — "Friends" принадлежит Warner Bros. |
| GE | `/friends` как команда — идеально. Короткое, интуитивное. SEO будет адский (конкуренция с сериалом). |
| DA | Warner Bros. не подаст в суд на open-source skill, но если это станет коммерческим продуктом — риск C&D letter. |
| **Вердикт** | **Использовать "Friends" для MVP/skill. При коммерциализации — ребрендинг (Frens? Minds? Resonance?). Trademark check перед Phase 2.** |

---

### ИДЕЯ 5: Параметры матчинга — локация, статус, доход
**Цитата:** *"локация описание статусные какие-то вещи статусные да то есть деньги уровень уровень дохода должен быть должен калькулироваться"*
**Таймкод:** 1:00–1:14

| Эксперт | Оценка |
|---------|--------|
| BP | Локация — разумно (proximity matching). Статус и доход — **красный флаг**. Это превращает продукт в инструмент стратификации. |
| PCA | Доход = PII (personally identifiable information). Даже инферированный доход — это profiling по GDPR Article 22. |
| DA | Если продукт матчит богатых с богатыми — это элитистское приложение, а не "друзья". Противоречит "friend you didn't know existed". |
| **Вердикт** | **Локация — ДА (city-level, opt-in). Доход — НЕТ. Это противоречит core value proposition и создаёт legal risk.** |

---

### ИДЕЯ 6: Доход должен вычисляться автоматически, не спрашиваться
**Цитата:** *"он не должен напрямую задаваться... люди будут обманывать но важно чтобы это степень дохода или качество уровень жизни высчитывался автоматически"*
**Таймкод:** 1:14–1:30

| Эксперт | Оценка |
|---------|--------|
| PCA | Automated profiling of financial status from personal files = GDPR Article 22 violation (automated decision-making). Штрафы до 4% мирового оборота. |
| SA | Технически: как вычислить доход из markdown? По упоминаниям брендов? По стоимости обсуждаемых проектов? Это ML-задача с чудовищным noise-to-signal ratio. |
| BP | Психологически: если пользователь узнает, что приложение "вычислило его доход" из личных файлов — это воспринимается как **слежка**, не как фича. Trust = destroyed. |
| DA | Представьте заголовок: "App covertly estimates users' income from their private notes." Один такой leak — и продукт мёртв. |
| **Вердикт** | **КАТЕГОРИЧЕСКИ НЕТ. Удалить из концепции полностью. Нет технического способа надёжно инферировать доход из markdown, и это этически/юридически токсично.** |

---

### ИДЕЯ 7: Параметр безопасности для женщин
**Цитата:** *"параметр безопасности то что если женщина знакомится мужчина хочет чтобы он был безопасен для нее и не не представлял угрозы"*
**Таймкод:** 1:30–1:43

| Эксперт | Оценка |
|---------|--------|
| BP | Критически важная тема. Но knowledge graph НЕ МОЖЕТ определить безопасность человека. Серийный убийца может иметь идеальный knowledge graph. |
| DA | Если продукт **обещает** безопасность — это liability. Если женщина пострадает, "ваш алгоритм сказал, что он безопасен" = судебный иск. |
| PS | Безопасность = table stakes для dating. Но если это networking (не dating) — бремя безопасности снижается (как LinkedIn, не Tinder). |
| **Вердикт** | **НЕ обещать безопасность. Вместо этого: 1) Telegram username = верифицируемая identity, 2) optional LinkedIn link, 3) дисклеймер "meet in public places". Networking framing снижает risk.** |

---

### ИДЕЯ 8: Физические параметры — рост, вес, размер груди → "не важно"
**Цитата:** *"фотография рост вес размер груди мне кажется это не важно нет не важно"*
**Таймкод:** 1:43–1:57

| Эксперт | Оценка |
|---------|--------|
| BP | Правильное решение. Физические параметры = дискриминация и objectification. Это то, чем Friends ОТЛИЧАЕТСЯ от Tinder. |
| PS | Это differentiator: "No photos. No bios. No swiping. Just minds." |
| **Вердикт** | **ПОДТВЕРЖДЕНО. Никаких физических параметров. Это core positioning.** |

---

### ИДЕЯ 9: Некрасивый, но богатый/харизматичный мужчина — как учесть?
**Цитата:** *"мужчина некрасивый но у него много бабосов его так все любят или он может быть харизматичными некрасивым"*
**Таймкод:** 2:05–2:20

| Эксперт | Оценка |
|---------|--------|
| BP | Это описывает реальную проблему dating apps — фильтр по фото отсеивает харизматичных людей. Friends РЕШАЕТ эту проблему by design: матчинг по мышлению, а не по внешности. |
| PS | Использовать как marketing message: "The most interesting people don't photograph well." |
| **Вердикт** | **Это АРГУМЕНТ в пользу концепции. Использовать в landing page storytelling.** |

---

### ИДЕЯ 10: Машина скрыто учитывает предпочтения (не нравятся короткие стрижки)
**Цитата:** *"идея в том чтобы человек не думает он пришел а при этом машина уже учла то что ему не нравится женщины с короткой стрижкой или что ему не нравится женщина у которых 43 размер ноги"*
**Таймкод:** 2:20–2:39

| Эксперт | Оценка |
|---------|--------|
| PCA | Скрытый сбор физических предпочтений = profiling. Откуда машина узнает про "не нравятся короткие стрижки"? Из markdown? Это невозможно без явного ввода. |
| BP | Implicit preference learning работает в e-commerce (рекомендации товаров). Но в people matching "скрытые предпочтения" = "алгоритм решил за тебя" = creepy factor. |
| SA | Для реализации нужен feedback loop: показывать профили → user реагирует → модель обучается. Это требует МНОГО данных и итераций. Не MVP. |
| **Вердикт** | **Отложить на Phase 3+. Для MVP — только explicit topic matching. Implicit preference learning = слишком complex и ethically murky.** |

---

### ИДЕЯ 11: Динамический алгоритм с обратной связью, корректировка весов
**Цитата:** *"динамический алгоритм который подстраиваться под собственные зависимости и с обратной связью... какой-то алгоритм с обратной связью который будет этом корректировать немножко веса"*
**Таймкод:** 2:39–2:56

| Эксперт | Оценка |
|---------|--------|
| SA | Классический collaborative filtering + reinforcement from user feedback. Технически стандартно: user rates match → weight adjustment → next batch улучшается. |
| DA | Для обратной связи нужны ПОЛЬЗОВАТЕЛИ. Chicken-and-egg: нет пользователей → нет feedback → плохой matching → нет пользователей. |
| **Вердикт** | **Архитектурно заложить, но НЕ реализовывать в MVP. Phase 2: добавить thumbs up/down на matches. Phase 3: полноценный feedback loop.** |

---

### ИДЕЯ 12: Децентрализованная технология
**Цитата:** *"был бы классно сделать чтобы это было либо децентрализованная технология"*
**Таймкод:** 2:56–3:10

| Эксперт | Оценка |
|---------|--------|
| SA | Децентрализация добавляет 10x complexity к каждому компоненту. Matching на блокчейне медленный (>1 sec per query vs <10ms centralized). |
| ME | Farcaster (децентрализованная соцсеть) потерял momentum к 2025, Lens Protocol жив но нишевый. Рынок SocialFi = $5B, но 90% — спекуляция токенами. |
| DA | "Decentralized" в 2026 = niche audience of crypto enthusiasts. Mainstream users не понимают и не ценят децентрализацию. |
| **Вердикт** | **НЕТ для MVP и public messaging. Внутренняя архитектурная заметка для Phase 3. Centralized = 100x faster to build, 10x easier to debug.** |

---

### ИДЕЯ 13: GitHub как первый канал дистрибуции → потом масштабирование
**Цитата:** *"привлечь внимание через такой гитхаб а следующим шагом когда люди забурдились ну как бы переносить мощности на вычисления"*
**Таймкод:** 3:10–3:38

| Эксперт | Оценка |
|---------|--------|
| GE | ОТЛИЧНАЯ стратегия. GitHub repo → stars → visibility → installs. Eco-system: 85K+ Claude skills, top ones get 277K installs. GitHub IS the app store for dev tools. |
| PS | Это "engineering as marketing": продукт сам себя продвигает через open-source. Zero CAC. |
| **Вердикт** | **ПОДТВЕРЖДЕНО. GitHub = primary distribution. README = landing page. Stars = social proof.** |

---

### ИДЕЯ 14: Не привязываться только к Claude — слой между LLM
**Цитата:** *"завязываться не завязываться же только на кладу потому что донышки конкурируют а между ними должно быть это какая-то как это слой слой какой-то передачи информации"*
**Таймкод:** 3:34–3:55

| Эксперт | Оценка |
|---------|--------|
| SA | Правильная интуиция. MCP protocol — это именно такой "слой". MCP уже поддерживается в Claude, Cursor, Windsurf, Copilot. Friends skill может работать через MCP → platform-agnostic. |
| GE | НО: запуск через Claude Code skill даёт максимальный охват прямо сейчас (85K skills, активное community). Мульти-платформенность — Phase 2. |
| **Вердикт** | **Строить на MCP protocol (platform-agnostic), но МАРКЕТИРОВАТЬ как Claude Code skill (максимальный текущий охват). Cursor/Windsurf support = Phase 2.** |

---

### ИДЕЯ 15: Не хранить данные в централизованной базе
**Цитата:** *"не хотелось бы хранить в какой-то централизованной базе вообще не хочет"*
**Таймкод:** 3:55–4:06

| Эксперт | Оценка |
|---------|--------|
| PCA | Правильная интуиция для privacy. Реализация: matching engine получает ТОЛЬКО хэши/Bloom filters. Никаких raw данных на сервере. Сервер = stateless matching функция. |
| SA | SQLite per-user на клиенте + centralized matching endpoint (FastAPI) = данные НЕ хранятся на сервере, но matching работает. Best of both worlds. |
| **Вердикт** | **ПОДТВЕРЖДЕНО. Server = stateless matching engine. Client = all data storage. Server хранит только Bloom filter hashes (не invertible).** |

---

### ИДЕЯ 16: Блокчейн или P2P сеть
**Цитата:** *"это либо блокчейн либо это какой-то ну или какая-то своей пи-ту-пи сеть"*
**Таймкод:** 4:06–4:24

| Эксперт | Оценка |
|---------|--------|
| SA | P2P mesh = Bluetooth/WiFi Direct. Технически кошмар: NAT traversal, connectivity, discoverability. Ни одна P2P social app не масштабировалась (Briar, Scuttlebutt — <10K users). |
| DA | Blockchain: Solana = $0.00025/tx, быстрый. НО: зачем блокчейн для matching? Какую проблему он решает, которую не решает простой сервер? "Censorship resistance" для dating? |
| **Вердикт** | **НИ ТО, НИ ДРУГОЕ для MVP. Centralized FastAPI server. Blockchain — Phase 3 only if trust/immutability becomes a real user need, not ideological choice.** |

---

### ИДЕЯ 17: Proximity alerts — "рядом с тобой подходящий человек"
**Цитата:** *"можно людям подсказывать что рядом с тобой человек оттекающий себя по интересам такой человек прям вот с таким же"*
**Таймкод:** 4:24–4:50

| Эксперт | Оценка |
|---------|--------|
| BP | МОЩНАЯ фича. Real-time serendipity = дофамин. "Рядом с тобой кто-то, кто думает как ты" — это магия. |
| PCA | ОПАСНАЯ фича. Real-time proximity = stalking tool. Нужно: 1) city-level only (не GPS), 2) opt-in, 3) rate limiting, 4) нельзя видеть одного конкретного человека в реальном времени. |
| DA | Happn (proximity dating app) имел именно эту проблему — используется для stalking. Uber тоже имел "God View" скандал. |
| **Вердикт** | **Как концепция — да. Как реализация: ТОЛЬКО city-level, ТОЛЬКО opt-in, ТОЛЬКО при взаимном match (обе стороны согласны). НЕ real-time GPS. Phase 2 minimum.** |

---

### ИДЕЯ 18: Генетический анализ, ДНК-тест, совместимость для здорового потомства
**Цитата:** *"генетический анализ даже может загружается... ты можешь загрузить туда свой ДНК тест или через нас его заказать... совместимость на генетическом уровне максимально здоровое потомство"*
**Таймкод:** 4:50–5:53

| Эксперт | Оценка |
|---------|--------|
| PCA | **СТОП.** ДНК-данные = GDPR Special Category Data (Article 9). + GINA (US). + Biotech regulations per country. Apple App Store в 2019 ЗАПРЕТИЛ Pheramor именно за сбор ДНК. 23andMe обанкротился в 2024, ДНК-данные стали toxic liability. |
| ME | Pheramor (ДНК-дейтинг) закрылся в 2019. GenePartner — статус неясен, нишевый. Рынок ДНК-дейтинга = проверенный failure. |
| BP | "Максимально здоровое потомство" — это евгенический нарратив. Пресса разорвёт. Один заголовок "App matches people for optimal breeding" — и продукт отменяют. |
| DA | Заказ ДНК-теста "через нас" = мы становимся healthcare intermediary. Лицензирование, страховка, compliance. Для двух человек? |
| **Вердикт** | **УБРАТЬ ПОЛНОСТЬЮ из всех фаз. Даже из внутренних документов. ДНК-matching = proven failure market + legal minefield + PR disaster. Если когда-нибудь — через партнёрство с лицензированной лабораторией, Phase 5+, с $50K+ legal review.** |

---

### ИДЕЯ 19: Данные с wearables — Oura, анализ крови, стресс
**Цитата:** *"анализ крови... Oura... все эти источники информации можно собирать вместе... насколько еще часто стрессует"*
**Таймкод:** 5:53–6:17

| Эксперт | Оценка |
|---------|--------|
| SA | Технически: Oura API, Apple Health API — доступны. Но это medical data → HIPAA (US), GDPR Article 9 (EU). |
| PCA | Health data = special category data. Даже в обезличенном виде — если можно re-identify (а в matching это возможно) — это violation. |
| PS | Интересный differentiator, но не для MVP. "Match by stress levels" — нишевая фича, не core value. |
| **Вердикт** | **Phase 3 earliest. MVP = markdown ONLY. Wearables добавлять после product-market fit с basic matching.** |

---

### ИДЕЯ 20: Bluetooth mesh / P2P база данных → отвергнуто
**Цитата:** *"может быть в виде приложения который хранит базу неструктурированных данных и она общается с другой базой которая находится по блютузе... мэш мы заебемся это делать"*
**Таймкод:** 6:17–6:47

| Эксперт | Оценка |
|---------|--------|
| SA | Денис прав: mesh = unreliable. Bluetooth range 10m, WiFi Direct = connection management hell. Apple ограничивает background Bluetooth. |
| **Вердикт** | **Правильно отвергнуто в разговоре. Не возвращаться к этому.** |

---

### ИДЕЯ 21: Telegram как канал коммуникации после match
**Цитата:** *"telegram хороший мессенджер поэтому в принципе сварить людей для общения дальше в telegram нормально"*
**Таймкод:** 6:58–7:15

| Эксперт | Оценка |
|---------|--------|
| GE | Отличное решение. Не нужно строить свой чат. Telegram = 900M+ MAU, все есть, нет friction. |
| SA | Реализация: после match показать Telegram username (если user opted in). Deep link: `t.me/username`. |
| **Вердикт** | **ПОДТВЕРЖДЕНО. Telegram = communication layer. Не строить свой мессенджер. Never.** |

---

### ИДЕЯ 22: Матчинг внутри Telegram-чата ("среди участников, кто тебе подходит")
**Цитата:** *"среди участников чата кто тебе больше подходит для общения это просто дополнительное мне кажется параметры"*
**Таймкод:** 7:15–7:42

| Эксперт | Оценка |
|---------|--------|
| GE | KILLER FEATURE для конференций и community чатов. "Who in this 500-person Telegram group should I talk to?" — это $$ (event matching). |
| ME | Это и есть event matching revenue model: конференция платит $2/participant, Friends анализирует участников и рекомендует connections. |
| **Вердикт** | **Записать как Phase 2 feature. Требует Telegram bot integration + group member analysis (with consent). Потенциально — основной revenue stream.** |

---

### ИДЕЯ 23: Client-side кодирование, zero-knowledge
**Цитата:** *"вопрос в том чтобы это было закодировано на стороне человека и никак не могло быть разгадано то есть некий zero-knowledge lock"*
**Таймкод:** 7:42–8:16

| Эксперт | Оценка |
|---------|--------|
| PCA | Правильный принцип, но "zero-knowledge" = конкретный криптографический протокол (ZK-SNARK, ZK-STARK). Для MVP: Bloom filters = "good enough" privacy без ZK overhead. Real ZK-proofs для matching = research problem, не engineering task. |
| SA | ZK-proof для "эти два профиля совместимы" без раскрытия данных — это cutting-edge crypto. Papers существуют (Private Set Intersection), но production-ready implementations = единицы. |
| **Вердикт** | **Принцип верный. Реализация для MVP: topic tags → Bloom filter → server-side Jaccard. Это "privacy-preserving" (не invertible), но НЕ zero-knowledge в строгом смысле. True ZK = research project, Phase 4+.** |

---

### ИДЕЯ 24: Цифровая подпись для согласия на публикацию
**Цитата:** *"человек должен дать свою какую-то подпись цифровую"*
**Таймкод:** 8:16–8:37

| Эксперт | Оценка |
|---------|--------|
| PCA | Хорошая идея. Keypair на клиенте: private key подписывает consent, public key верифицирует. Стандартная PKI. |
| SA | Реализация: при первом запуске `/friends` генерирует Ed25519 keypair, хранит в `~/.friends/`. Sign каждый data submission. |
| **Вердикт** | **Включить в MVP. Keypair generation + signed consent — это и GDPR compliance (documented consent) и foundation для будущего blockchain (если дойдёт).** |

---

### ИДЕЯ 25: Smart-контракт на каждого пользователя
**Цитата:** *"человек создает на себя смарт-контракт публикует его эти контракты матчатся... движок который нажимаешь я хочу и эта технология ищет тебя"*
**Таймкод:** 8:37–10:07

| Эксперт | Оценка |
|---------|--------|
| SA | Красивая концепция. Но smart contract = $0.01-$1 per deployment на Solana. 10K users = $100-$10K. Matching on-chain = gas costs per query. При 100 queries/day = $30-$3K/day. Нерентабельно без токеномики. |
| ME | Smart contracts для identity = Lens Protocol / ENS. Работает, но adoption = crypto-native audience only (<1% internet users). |
| DA | "Мой публичный адрес хочет найти друга" — это beautiful metaphor, но чудовищно непрактичная архитектура для социального продукта. |
| **Вердикт** | **Phase 4+. Красивая архитектурная vision для pitch deck. Не для MVP, не для Phase 2, не для Phase 3. Если дойдёте до 10K users — пересмотреть.** |

---

### ИДЕЯ 26: MCP-сервер или "Friends protocol"
**Цитата:** *"можно это назвать MCP сервером или каким-то универсальным friends протоколом коммуникации"*
**Таймкод:** 9:10–9:30

| Эксперт | Оценка |
|---------|--------|
| SA | MCP (Model Context Protocol) уже стандарт для AI tool communication. Friends КАК MCP server = правильная архитектура. Skill → MCP → matching server. |
| PS | "Friends Protocol" — мощный branding. Не просто app, а protocol. Как "ActivityPub" для Mastodon. Open standard > closed app. |
| GE | Protocol = other people build on top of it. Third-party clients, integrations, plugins. Network effect через developer adoption. |
| **Вердикт** | **"Friends Protocol" = long-term vision. MVP = MCP-based skill that talks to centralized server. Open-source protocol spec → Phase 2. Это USP: не app, а protocol.** |

---

### ИДЕЯ 27: Начать centralized, потом blockchain
**Цитата:** *"начать с централизованного решения которое просто висит на серваке... а потом мы туда уже добавляем блокчейн следующим шагом"*
**Таймкод:** 9:30–9:50

| Эксперт | Оценка |
|---------|--------|
| SA | Правильная стратегия: prove the concept centralized, decentralize if demand exists. Every successful decentralized product started centralized (Ethereum had a foundation, Bitcoin had Satoshi's node). |
| **Вердикт** | **ПОДТВЕРЖДЕНО. Phase 1: FastAPI on Contabo. Phase 2: Postgres. Phase 3: evaluate if decentralization adds value.** |

---

### ИДЕЯ 28: Claude Code skill как современная "установка приложения"
**Цитата:** *"скилл кодирует на вашей стороне в клиенте все потом через mcp передает... это анбординг это как современная установка приложений"*
**Таймкод:** 9:50–10:40

| Эксперт | Оценка |
|---------|--------|
| GE | КЛЮЧЕВОЙ ИНСАЙТ. Skill install = new app install for AI-native users. Zero friction: GitHub → one command → working. No App Store, no signup, no credit card. |
| PS | Это positioning statement: "Apps are installed from App Stores. Skills are installed from GitHub. Friends is the first skill that connects you to people." |
| **Вердикт** | **CORE of the MVP. Skill install UX = primary onboarding. Landing page → GitHub → install → `/friends` → graph. 4 clicks.** |

---

### ИДЕЯ 29: Граф-визуализация — видишь себя и соседние точки
**Цитата:** *"ты пропишешь фрэнс и он открывает в браузере граф который может быть обновлен но периодически обновляется но ты видишь себя в этом графе и соседние точки нажимаешь на точку и там появляется информация"*
**Таймкод:** 10:40–11:15

| Эксперт | Оценка |
|---------|--------|
| DA | ЭТО MVP. Красивый интерактивный граф, где ты — центр. Ближайшие ноды = ближайшие minds. Click = profile. Это **shareability**: скриншот графа → Twitter post → viral. |
| SA | D3.js force-directed graph. Each node = user. Edge weight = similarity score. Hover = preview. Click = full profile. Static HTML served from GitHub Pages. |
| BP | Obsidian-style graph на ЛЮДЯХ — это визуальная метафора "your mind, connected to other minds." Интуитивно понятно, эстетически привлекательно. |
| **Вердикт** | **ЦЕНТРАЛЬНЫЙ ЭЛЕМЕНТ MVP. Граф = продукт, граф = маркетинг, граф = demo. Вложить 60% усилий MVP в качество визуализации.** |

---

### ИДЕЯ 30: Больше данных = лучший matching (incentive для sharing)
**Цитата:** *"чем больше люди которые хотят участвовать на фронтах себе тем интереснее будет матчинг... ты хочешь предоставить больше информации для того чтобы получить как можно более интересных друзей"*
**Таймкод:** 11:15–12:00

| Эксперт | Оценка |
|---------|--------|
| GE | Positive feedback loop: more data → better matches → user shares more → even better matches. Gamify: "Your matching score: 34%. Add more files to improve." |
| PCA | Но privacy paradox: больше данных = больше risk. Нужен чёткий UI: "You're sharing X files. This improves matching by Y%." Transparency = trust. |
| **Вердикт** | **Реализовать как "matching quality score" (0-100%). Show users what improves their score. Gamification + transparency.** |

---

### ИДЕЯ 31: Matching engine не хранит личной информации
**Цитата:** *"engine который будет матчить он не должен хранить никакой личной информации... на стороне клиента должна происходить кодировка"*
**Таймкод:** 12:00–12:30

| Эксперт | Оценка |
|---------|--------|
| PCA | Правильная архитектура. Server = stateless function: input(bloom_filter_A, bloom_filter_B) → output(similarity_score). Ничего не хранит. |
| SA | В реальности server ДОЛЖЕН хранить Bloom filters для matching (иначе каждый запрос = full scan). Но Bloom filters ≠ personal data (не invertible). |
| **Вердикт** | **Server хранит: Bloom filter + public key + optional display name + optional Telegram handle. НЕ хранит: raw content, topics, files, location history. GDPR-compliant by design.** |

---

### ИДЕЯ 32: Client-side private key для редактирования своего hash
**Цитата:** *"на стороне клиента некий секрет который позволяет дописывать или редактировать то что хранится там"*
**Таймкод:** 12:30–13:30

| Эксперт | Оценка |
|---------|--------|
| PCA | Стандартный PKI pattern: Ed25519 private key подписывает updates, server верифицирует через public key. Only holder of private key can update their profile. |
| SA | Implementation: `~/.friends/keypair.json` (encrypted at rest). Every API call to update profile = signed with private key. |
| **Вердикт** | **ВКЛЮЧИТЬ в MVP. Standard asymmetric crypto. Simple, proven, foundation for future decentralization.** |

---

### ИДЕЯ 33: "Объявим рейз когда сервер ляжет" — proof of stake
**Цитата:** *"в момент когда сервер ляжет мы объявим рейс... давайте-ка вместе скинемся... порфа встайк"*
**Таймкод:** 13:30–14:20

| Эксперт | Оценка |
|---------|--------|
| ME | Crowdfunding infrastructure costs — charming but unreliable. Better: if the product is valuable, charge for it (event matching). If it's not, no amount of "рейз" helps. |
| DA | "Proof of stake" для social app = wrong tool. PoS решает consensus, а не funding. Не смешивать. |
| **Вердикт** | **Не включать в MVP plan. Если продукт нужен людям — монетизация через event matching / B2B. Если не нужен — crowdfunding не поможет.** |

---

### ИДЕЯ 34: Ночной спринт на двух машинах (Claude Code + Codex review)
**Цитата:** *"ночным спринтом это сделаем на двух машинах параллельно в одном случае это будет кладкод и ревью в кодексе"*
**Таймкод:** 14:20–15:10

| Эксперт | Оценка |
|---------|--------|
| SA | Workable workflow: Machine 1 = Claude Code implements, Machine 2 = Codex reviews. Parallel = faster. Но review gate = quality control. |
| **Вердикт** | **Применимо к MVP sprint. Claude Code → implement landing page + graph. Codex → review. Параллельно: один на frontend/viz, другой на backend/matching.** |

---

### ИДЕЯ 35: Архитектура + план с промптами в MD-файлах
**Цитата:** *"нужно архитектуру изначально которую надо обсудить для такого проекта"*
**Таймкод:** 15:10–15:25

| Эксперт | Оценка |
|---------|--------|
| SA | Правильный подход: architecture first, code second. SDD.md = source of truth. Sprint tasks в MD-файлах с промптами = reproducible. |
| **Вердикт** | **ВЫПОЛНЯЕТСЯ: SDD.md создан, expert panel проведён. Следующий шаг: sprint plan с task-level промптами.** |

---

## Summary: Какие идеи из разговора ПРОШЛИ экспертную панель

### ✅ ПОДТВЕРЖДЕНЫ (включить в MVP)
| # | Идея | Обоснование |
|---|------|-------------|
| 2 | "Друг, о котором не знал" | Core hook, viral messaging |
| 3 | Markdown files как источник данных | Реализуемо, privacy-preserving |
| 4 | Название "Friends" | Тёплое, запоминающееся (trademark check на Phase 2) |
| 8 | Нет физических параметров | Core differentiator: minds > photos |
| 13 | GitHub как дистрибуция | 85K+ skills, zero CAC |
| 15 | Нет централизованного хранения | Stateless server, client-side data |
| 21 | Telegram как канал | 900M+ MAU, zero friction |
| 24 | Цифровая подпись для consent | PKI, GDPR compliance, future-proof |
| 27 | Начать centralized, потом масштабировать | Proven strategy |
| 28 | Skill как "установка приложения" | Core UX innovation |
| 29 | Граф-визуализация | ЦЕНТРАЛЬНЫЙ ЭЛЕМЕНТ MVP |
| 30 | Больше данных = лучший matching | Positive feedback loop |
| 31 | Engine не хранит личных данных | Privacy by architecture |
| 32 | Client-side private key для updates | Standard PKI |
| 34 | Параллельная разработка (2 машины) | Sprint workflow |

### ⏸️ ОТЛОЖЕНЫ (Phase 2-3)
| # | Идея | Когда |
|---|------|-------|
| 10 | Implicit preference learning | Phase 3+ (нужны данные и feedback) |
| 11 | Динамический алгоритм с обратной связью | Phase 2 (thumbs up/down) |
| 14 | Мульти-платформенность (не только Claude) | Phase 2 (Cursor, Windsurf) |
| 17 | Proximity alerts | Phase 2 (city-level, opt-in, mutual only) |
| 19 | Wearables (Oura, health data) | Phase 3 (medical data regulations) |
| 22 | Матчинг внутри Telegram-чатов | Phase 2 (event matching = revenue) |
| 25 | Smart contracts per user | Phase 4+ (если 10K+ users) |
| 26 | "Friends Protocol" как стандарт | Phase 2 (open-source spec) |

### ❌ ОТКЛОНЕНЫ (убрать из концепции)
| # | Идея | Почему |
|---|------|-------|
| 5/6 | Автоматическое вычисление дохода | Ethically toxic, technically unproven, GDPR violation |
| 18 | ДНК-тест / генетическая совместимость | Legal minefield (GDPR Art.9, GINA), proven market failure (Pheramor), PR disaster ("eugenics app") |
| 12 | Децентрализация для MVP | 10x complexity, zero value at small scale |
| 16 | Blockchain для MVP | Scares mainstream users, signals "no business model" |
| 20 | Bluetooth mesh / P2P | Correctly rejected in the conversation itself |
| 33 | Crowdfunding / proof of stake для funding | Wrong tool for the problem |

---

## Step 3 — Individual Analysis

### 1. Product Strategist

**Assessment:** The core insight is powerful: people are more than their photos, and AI conversations reveal genuine intellectual compatibility. The timing is right — Claude Code has 85K+ skills, 277K+ installs on popular skills, and there's a growing "AI-native" demographic that lives in terminals. This is "Tinder for knowledge workers" but positioned as anti-Tinder. The key differentiator is that matching happens on *how you think*, not how you look.

**Risks:**
- The concept tries to be everything: dating + networking + friendship + DNA matching + blockchain. This scatters focus and confuses positioning.
- "Knowledge graph from markdown files" sounds technical and niche. Normal people don't have markdown files.
- DNA/genetics matching adds regulatory weight disproportionate to its value at MVP stage.

**Recommendation:** Ruthlessly narrow the MVP. Pick ONE use case: **professional networking for AI-native developers** (people who use Claude Code daily). This is the only audience that has markdown files AND will install a Claude Code skill. Dating comes later when the network exists. Frame it as: *"Find your next co-founder, not your next date."*

**Open question:** What's the actual TAM of "people who use Claude Code AND want to meet strangers"? Is this hundreds or hundreds of thousands?

---

### 2. Privacy/Crypto Architect

**Assessment:** The privacy architecture has the right instinct (client-side encoding, zero-knowledge matching) but the SDD is dangerously vague on implementation. "Hash/Embeddings" is not a privacy strategy — embeddings are partially invertible. Cosine similarity on raw embeddings leaks information. The DNA data component puts this squarely in GDPR Article 9 (special category data) territory, plus GINA (US), plus country-specific genetic data laws.

**Risks:**
- **Embedding inversion:** Modern research shows that text embeddings can be partially reversed to recover original content. Sending "privacy-preserving embeddings" to a central server is NOT zero-knowledge.
- **DNA data liability:** Storing or transmitting genetic data, even hashed, creates massive legal exposure. 23andMe's bankruptcy (2024) showed how toxic genetic data can become.
- **Key management:** "Private key stays on client" — what happens when the user loses their device? No recovery = lost profile. Recovery mechanism = attack vector.
- **GDPR compliance:** Even with client-side encoding, if the matching engine can infer personal attributes, you're a data controller.

**Recommendation:**
- Phase 1 MVP: **NO DNA, NO health data, NO wearables.** Only markdown/conversation-derived topic vectors.
- Use **Secure Multi-Party Computation (SMPC)** or **Private Set Intersection (PSI)** instead of sending embeddings to a server. Libraries: [MP-SPDZ](https://github.com/data61/MP-SPDZ), [OpenMined PySyft](https://github.com/OpenMined/PySyft).
- For MVP: simpler approach — **locally computed topic tags** (not embeddings) sent as Bloom filter. Server does intersection on Bloom filters. This is genuinely privacy-preserving and computationally cheap.
- DNA matching = Phase 4 minimum, with a dedicated legal review ($5-10K).

**Open question:** Are you willing to accept "good enough" privacy (topic tags + Bloom filters) for MVP, or is "real" zero-knowledge a hard requirement from day one?

---

### 3. Growth Engineer

**Assessment:** The Claude Code skill distribution channel is genius timing. The skill ecosystem is exploding (50 → 85K+ in 12 months). A `/friends` skill that's genuinely useful will spread through developer Twitter/X organically. The onboarding is frictionless: install skill → run → see graph. No app store, no signup form, no email verification.

**Risks:**
- **Cold start problem:** A matching network with 10 users is useless. You need critical mass in a specific geography/community first.
- **Claude Code lock-in:** Tying distribution to one platform is risky. Anthropic could change skill policies, deprecate features, or a competitor (Cursor, Windsurf) could win the market.
- **Retention:** People install, see an empty graph, leave. Never come back.

**Recommendation:**
- **Launch strategy: Concentric circles.**
  1. **Inner circle (Week 1):** 50 hand-picked Claude Code power users. Tim + Denis's networks. Seed the graph with real profiles.
  2. **Developer Twitter (Week 2-3):** Demo video showing the graph visualization. "I found my next co-founder through my Claude conversations." Controversial enough to go viral.
  3. **Hacker News / Product Hunt (Week 4):** Full launch with enough profiles to be useful.
- **Fake-it-till-you-make-it:** Pre-populate the graph with anonymized "ghost profiles" derived from public GitHub repos. Users see a populated graph on first launch, even before real users join. Clearly label these as "demo profiles."
- **Multi-agent support:** Don't just support Claude Code. Make it work with Cursor, Windsurf, any MCP-compatible agent. The MCP protocol IS the distribution channel, not Claude specifically.
- **Telegram as glue:** After matching, move conversation to Telegram. This is smart — everyone has it, no new app needed.

**Open question:** Can you get 50 real early adopters in Week 1 through your existing Claude Partner Network?

---

### 4. System Architect

**Assessment:** The core technical challenge is the matching engine. Doing cosine similarity on encrypted/hashed data is either impossible (if properly encrypted) or trivially breakable (if just hashed). The SDD needs to pick a concrete approach. The client-side skill → MCP → server pipeline is technically sound and fits existing infrastructure.

**Risks:**
- **Matching quality:** Topic tags or Bloom filters (PCA's suggestion) will give coarse matches. Embeddings give better matches but leak data. This is the fundamental tension.
- **Real-time matching:** Force-directed graph with live updates requires WebSocket connections. At scale, this becomes expensive.
- **Blockchain is premature:** Adding blockchain before having 1,000 users is pure overhead. It adds latency, complexity, and cost with zero benefit at small scale.

**Recommendation:**
- **MVP matching algorithm:**
  1. Client extracts **topic tags** from markdown files using local LLM (Llama 3 via Ollama or even keyword extraction)
  2. Tags are sent as **weighted Bloom filter** to server
  3. Server computes **Jaccard similarity** on Bloom filters
  4. Top-K matches returned
  5. User sees graph, clicks, connects
- **Tech stack for MVP:**
  - Skill: TypeScript (Claude Code native)
  - Server: FastAPI on Contabo VPS 30
  - Visualization: D3.js force-directed graph (static HTML on GitHub Pages)
  - Communication: REST API (not MCP for server — MCP is client-to-skill only)
  - DB: SQLite (seriously, you don't need Postgres for <10K users)
- **Kill blockchain until Phase 3.** It adds nothing at MVP and scares away non-crypto users.

**Open question:** Will users tolerate running a local LLM (Ollama) for tag extraction, or does this need a lighter approach (keyword extraction, TF-IDF)?

---

### 5. Behavioral Psychologist

**Assessment:** The concept taps into a genuine unmet need: people are tired of superficial matching. But the psychological dynamics of this product are complex. When you match people on "how they think," you create **intellectual intimacy before social comfort** — this can feel invasive. Also, the target demographic (AI-native devs) skews male, introvert, and high-anxiety — the exact population that struggles most with turning digital connections into real-world relationships.

**Risks:**
- **Uncanny valley of matching:** "This person thinks exactly like me" can feel creepy, not exciting. People often want complementary partners, not mirror images.
- **Safety concern (real):** The transcript mentions women's safety. Knowledge-graph matching provides ZERO safety signal. Someone can be intellectually compatible and physically dangerous.
- **The "empty profile" problem:** Developers who are most interesting (deep thinkers, prolific writers) are least likely to want their markdown analyzed. Selection bias: you'll get the people who WANT to be seen, not necessarily the most interesting ones.
- **Income inference is ethically fraught:** Auto-calculating income from context could be discriminatory and legally questionable. Rich people's markdown isn't structurally different from poor people's.

**Recommendation:**
- **Drop income inference entirely.** It's unprovable, ethically dubious, and adds zero value for MVP. Focus on intellectual compatibility only.
- **Add a "conversation starter" feature:** When two people match, the system generates a specific topic they'd both enjoy discussing. This bridges the gap between "you matched" and "now what."
- **Safety: Telegram username verification + optional LinkedIn connection.** Not foolproof, but establishes real-world identity.
- **Frame matches as "interesting people," NOT "compatible partners."** Remove all romantic language from MVP. Let users decide what the connection becomes.

**Open question:** Have you tested whether YOUR OWN markdown files produce a meaningful knowledge graph? If Tim and Denis run it on their files, does the matching make intuitive sense?

---

### 6. Monetization Expert

**Assessment:** Monetization is the weakest part of the concept. "Freemium + maybe blockchain + maybe DNA commissions" is not a business model. The target audience (developers) is notoriously resistant to paying for social tools. However, this could work as a **developer tool that accidentally builds a social network** — similar to how GitHub became social.

**Risks:**
- **Free forever trap:** If matching is free and works well, there's no upgrade path. What does "premium" matching even mean?
- **Token economics would kill adoption.** The moment you add a token, you attract speculators and repel genuine users.
- **DNA commission model requires medical-grade compliance.** Not worth the regulatory burden.

**Recommendation:**
- **MVP: Completely free.** No monetization. Goal is network effect, not revenue.
- **Phase 2 monetization options (pick ONE):**
  - **A. Verified profiles ($5/mo):** Pay to verify your identity, get a badge, appear higher in matching. Like Twitter Blue but useful.
  - **B. Team matching (B2B, $20/seat/mo):** Companies use Friends to match employees for projects, mentoring, cross-team collaboration. This is the real money.
  - **C. Event matching ($2/event):** Conference organizers pay to add Friends matching for attendees. "Who at this conference should I meet?"
- **Recommended: Start with C (event matching).** It's transactional, requires no subscription commitment, and conferences NEED this. It also solves cold-start — every event is a captive audience.

**Open question:** Would Denis's network include conference organizers who'd pilot event matching?

---

### 7. Devil's Advocate

**Assessment:** I'm going to be harsh because this concept needs it. The core idea ("match by knowledge graph") is intellectually appealing but practically untested. Every "smart matching" dating app has failed: OkCupid's compatibility scores didn't predict real chemistry, Coffee Meets Bagel's curated matches didn't beat Tinder's volume, and Pheramor's DNA matching shut down. The graveyard of "we're smarter than swiping" apps is enormous.

**Risks:**
- **Fundamental assumption is unproven:** "People who think similarly make good friends/partners." This is a hypothesis, not a fact. Research on relationship satisfaction shows complementarity matters as much as similarity.
- **Privacy as feature vs. privacy as friction:** "Your data never leaves your device" sounds good in a README but means nothing to users. They'll install it if it WORKS, not because of privacy promises. If it doesn't work well, privacy won't save it.
- **Blockchain is a red flag.** In 2026, adding "blockchain" to a social product signals "we don't know our business model." It repels mainstream users and attracts the wrong crowd.
- **Two-person team building a social network.** Social networks require constant moderation, trust & safety, abuse prevention, and community management. This is a full-time job for multiple people.
- **AI-native audience is tiny and homogeneous.** Matching developers with developers produces a monoculture. The most interesting connections are cross-domain.

**Recommendation:**
- **Drop blockchain from ALL public messaging.** Keep it as an internal architectural note if you want, but never mention it to users.
- **Don't call it a dating app.** Call it a "knowledge networking protocol." This is defensible, accurate, and avoids the dating app graveyard association.
- **Build the visualization FIRST.** The interactive knowledge graph is the one thing that's genuinely novel and demo-able. If the visualization is beautiful enough, people will share it on Twitter regardless of whether matching works. This IS the MVP: "See your mind, visualized. Find minds like yours."
- **Test the hypothesis before building.** Take 20 developers. Analyze their markdown files manually. Match them. Introduce them. Did they actually become friends? If not, the whole premise fails.

**Open question:** What happens when this product is used for stalking? If someone can see that "a person who thinks like X is near you," they can triangulate identities. How do you prevent this?

---

## Step 4 — Panel Conflicts

### ⚖️ Conflicts & Resolutions

| Topic | Position A | Position B | Resolution |
|-------|-----------|-----------|------------|
| **DNA/Health data in MVP** | SA, GE: "Cool differentiator" | PCA, DA, BP: "Legal nightmare, drop it" | **DROP for MVP.** Unanimous except originators. Legal risk is disproportionate. Revisit at Phase 3+ with $10K legal review. |
| **Blockchain mention** | Origin transcript: "core to the vision" | DA, ME, GE: "Repels users, signals no business model" | **Remove from public messaging.** Keep as internal Phase 3 architectural note. Never mention in landing page, README, or pitch. |
| **Income inference** | Origin transcript: "super important" | BP, DA: "Ethically dubious, technically unproven" | **DROP entirely.** No evidence markdown structure correlates with income. Discrimination risk too high. |
| **Use case: Dating vs. Networking** | Origin transcript: "dating + friends + everything" | PS, BP, DA: "Pick one, networking first" | **Networking first.** Frame as "find interesting people," not "find a partner." Romantic matching added later if network grows. |
| **Privacy approach** | SDD: "embeddings to server" | PCA: "Embeddings are invertible, use Bloom filters" | **Bloom filters for MVP.** Topic tags → weighted Bloom filter → Jaccard similarity. Simpler, genuinely private, computationally cheap. |
| **Monetization model** | Origin: "token + freemium + DNA commission" | ME: "Event matching ($2/event)" | **Free MVP, then event matching.** Token economics and DNA commissions rejected. B2B team matching as Phase 3. |
| **Blockchain architecture** | SA: "Premature, adds latency" | Origin: "Core feature" | **SA wins.** Centralized server for Phase 1-2. Blockchain only if >10K users AND proven demand. SQLite → Postgres → maybe blockchain. Never lead with it. |
| **Target audience** | GE: "Claude Code users specifically" | DA: "Too tiny, too homogeneous" | **Compromise.** Launch with Claude Code users but support MCP-compatible agents (Cursor, Windsurf) from day 1. Expand to broader "AI-native" audience. |

### Dissents Noted

- **DA dissents** on the entire concept: "The hypothesis that markdown-based matching produces meaningful connections is unproven. Recommend a manual test with 20 people before writing any code."
- **PCA dissents** on Bloom filter approach being "good enough": "At scale, Bloom filter intersection leaks information about set membership. This is acceptable for MVP but needs upgrading before 1K users."

---

## Step 5 — Converged Plan

### Recommended Plan

**Approach:** Friends is a **knowledge networking protocol** (NOT a dating app) that connects AI-native professionals based on their intellectual fingerprint — derived from markdown files, AI conversations, and local documents. MVP is a beautiful interactive landing page with a live graph visualization that demonstrates the concept and collects early adopters. Distribution through Claude Code skill ecosystem + MCP-compatible agents.

### Key Decisions

| # | Decision | Chosen | Rationale | Driven by |
|---|----------|--------|-----------|-----------|
| 1 | Primary use case | Professional networking | Avoids dating app graveyard, fits target audience, no safety/moderation burden | PS, BP, DA |
| 2 | Privacy approach | Topic tags → Bloom filters → Jaccard similarity | Genuinely private, simple, fast. Embeddings are invertible. | PCA, SA |
| 3 | Data sources for MVP | Markdown files + Claude sessions ONLY | DNA, wearables, income add legal risk with zero proven value | PCA, DA, BP |
| 4 | Distribution | Claude Code skill + MCP protocol (multi-agent) | 85K+ skills, frictionless install, viral potential on dev Twitter | GE |
| 5 | Visualization | D3.js force-directed 2D graph | Novel, demo-able, sharable. This IS the marketing. | DA, SA |
| 6 | Blockchain | Removed from MVP and public messaging | Repels mainstream users, zero value at small scale, signals "no business model" | DA, ME, SA |
| 7 | Monetization | Free MVP → Event matching ($2/event) → B2B team matching | Transactional, no subscription friction, solves cold start at events | ME |
| 8 | Tech stack | TypeScript skill + FastAPI server + SQLite + D3.js | Minimal, proven, deployable on existing Contabo infra | SA |
| 9 | Communication channel | Telegram after match | Everyone has it, no new app, existing integration | GE |
| 10 | Naming | "Friends" (knowledge networking protocol) | Warm, non-technical, memorable. Subtitle: "Find minds like yours." | PS |

### Refined Product Vision

```
Friends is a knowledge networking protocol.

You install a skill. It reads your local files — with your permission.
It builds a map of what you think about, what you know, what you care about.
Then it finds other people whose minds resonate with yours.

No photos. No bios. No swiping.
Just your ideas, meeting theirs.

You see a graph. Each node is a person.
The closer the node, the more your minds align.
Click. Connect. Start talking.

Your data never leaves your device.
The matching engine sees only encrypted fingerprints.
You own your mind. Always.
```

### Risk Register

| Risk | Severity | Mitigation |
|------|----------|------------|
| Cold start (empty graph) | HIGH | Pre-populate with demo profiles from public GH repos. Launch at specific event/community first. |
| Embedding/privacy leak | HIGH | Use Bloom filters, not embeddings. No raw data leaves client. |
| Matching quality too low | MEDIUM | Feedback loop: user rates matches, weights adjust. Manual testing with 20 people first. |
| Stalking and triangulation | HIGH | Approximate location only (city-level). No real-time proximity. Rate-limit profile views. |
| Regulatory (GDPR) | MEDIUM | No special category data in MVP. Privacy policy. Data processing agreement. |
| Claude Code dependency | MEDIUM | Support MCP protocol broadly, not just Claude. |
| Team too small for social product | MEDIUM | Automated moderation. Telegram for communication (their moderation, not ours). |
| Hypothesis wrong (similarity ≠ good matches) | HIGH | **Test with 20 real people manually before scaling.** This is the #1 risk. |

### Mitigations (from Security/Privacy review)

- No DNA data until Phase 3 + legal review
- No income inference — ever
- Bloom filters instead of embeddings
- Client-side processing only — server is stateless matching engine
- No blockchain until proven demand at scale
- GDPR-compliant by architecture (data minimization, purpose limitation)

### Open Items Requiring User Input

1. **Manual hypothesis test:** Will Tim + Denis run the matching algorithm on 20 real developers' files and manually test if matches make sense? (DA's recommendation, panel agrees this is critical)
2. **Event matching pilot:** Does Denis have access to conference organizers for a pilot? (ME's monetization strategy depends on this)
3. **Claude Partner Network:** Can Tim's 10-person Claude Partner cohort be the first test group? (GE's launch strategy)
4. **Legal review budget:** Is $5K available for Phase 2 privacy/GDPR review? (PCA requirement before any public data processing)

### Suggested Next Steps

1. **[DONE]** Create GitHub repo, SDD, source of truth
2. **[NOW]** Expert panel review ← you are here
3. **[NEXT]** Launch strategy development
4. **[NEXT]** Codex adversarial review of the refined concept
5. **[NEXT]** MVP Sprint: Landing page with interactive graph visualization on timzinin.com/friends/
6. **[NEXT]** Manual test: Run matching on 20 real profiles
7. **[NEXT]** Claude Code skill prototype (Phase 2)

---

## Appendix: Market Research Summary

### Competitors
- **Traditional dating apps (Tinder, Bumble, Hinge):** Photo-first, no knowledge matching. Different market.
- **OkCupid:** Had compatibility scores based on questionnaires. Abandoned advanced matching for simpler swipe UX. Lesson: complex matching didn't retain users.
- **Pheramor (DNA dating):** Launched 2018, shut down 2020. Couldn't solve cold start + regulatory burden.
- **GenePartner:** Still exists but niche. No mainstream adoption.
- **Lunar (decentralized dating on Lens Protocol):** Launched 2024, <5K users. Blockchain audience ≠ dating audience.
- **Farcaster Frames dating:** Experimental, never gained traction.

### Key insight
No one has tried **AI conversation-based matching** distributed through **developer tooling**. This is genuinely novel. The closest analog is Polywork (professional networking for builders) which raised $28M but pivoted to job search.

### Claude Code Ecosystem
- 85K+ indexed skills (March 2026)
- Popular skills: 277K+ installs (frontend-design)
- Distribution: GitHub → skill install → instant access
- Growing ~10% monthly
