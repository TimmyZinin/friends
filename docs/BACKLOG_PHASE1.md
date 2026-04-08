# Phase 1 Backlog — от документации до работающего MVP

> Цель Phase 1: работающий скилл `/friends` + matching server + 30-50 alpha-пользователей
> Срок: 4-6 недель (5 спринтов)
> Команда: Тим + Денис + Claude Code

---

## Sprint 1: Skill Prototype (1 неделя)
> Цель: рабочий скилл, который извлекает темы из markdown и генерирует Bloom filter

| # | Задача | Приоритет | Размер | Acceptance Criteria |
|---|--------|-----------|--------|-------------------|
| 1.1 | Создать Claude Code skill scaffold (TypeScript, SKILL.md) | HIGH | S | Скилл устанавливается через `/friends`, выводит приветствие |
| 1.2 | File scanner: рекурсивный поиск `*.md` файлов с whitelist директорий | HIGH | M | Находит все md-файлы, показывает список для подтверждения |
| 1.3 | NLP pipeline: TF-IDF extraction тегов тем (EN + RU) | HIGH | L | Из 10 md-файлов извлекает 30-50 осмысленных тегов |
| 1.4 | Bloom filter encoder: 1024 бит, MurmurHash3 x 5 | HIGH | M | Входные теги → 128-байтный bit array, reproducible |
| 1.5 | Ed25519 keypair: генерация, сохранение в `~/.friends/` | HIGH | S | Keypair создаётся при первом запуске, переиспользуется |
| 1.6 | Подпись Bloom filter приватным ключом | MEDIUM | S | Signed payload готов для отправки на сервер |
| 1.7 | Unit tests: NLP extraction + Bloom filter correctness | HIGH | M | >80% coverage, тесты проходят |

**Deliverable:** скилл `/friends` извлекает темы → кодирует → подписывает. Пока без сервера.

---

## Sprint 2: Matching Server (1 неделя)
> Цель: рабочий FastAPI сервер с matching engine на Contabo

| # | Задача | Приоритет | Размер | Acceptance Criteria |
|---|--------|-----------|--------|-------------------|
| 2.1 | FastAPI scaffold: `/v1/register`, `/v1/match`, `/v1/profile`, `/v1/graph` | HIGH | M | Все 4 эндпоинта отвечают (можно stub) |
| 2.2 | Ed25519 signature verification middleware | HIGH | M | Невалидная подпись → 401, валидная → pass |
| 2.3 | SQLite storage: Bloom filter + pubkey + display name + TG handle | HIGH | S | Профиль сохраняется и читается |
| 2.4 | Matching engine: Jaccard similarity на Bloom filters | HIGH | M | Для 2 профилей возвращает корректный score |
| 2.5 | Top-K selection с threshold >0.15 | MEDIUM | S | Возвращает отсортированный список max 20 результатов |
| 2.6 | Rate limiting (in-memory, per pubkey и per IP) | MEDIUM | S | Превышение лимита → 429 |
| 2.7 | DELETE endpoint (GDPR right to erasure) | HIGH | S | Профиль полностью удаляется |
| 2.8 | Docker Compose + deploy на Contabo VPS 30 | HIGH | M | Сервер доступен по HTTPS |
| 2.9 | Integration tests: register → match → delete cycle | HIGH | M | Полный цикл проходит без ошибок |

**Deliverable:** сервер на Contabo принимает регистрации, вычисляет матчи, возвращает результаты.

---

## Sprint 3: Skill + Server Integration (1 неделя)
> Цель: скилл общается с сервером, пользователь видит матчи

| # | Задача | Приоритет | Размер | Acceptance Criteria |
|---|--------|-----------|--------|-------------------|
| 3.1 | Skill → Server: POST register (отправка Bloom filter) | HIGH | M | Профиль создаётся на сервере через скилл |
| 3.2 | Skill → Server: POST match (запрос матчей) | HIGH | M | Скилл получает Top-K результатов |
| 3.3 | Skill → Browser: открытие D3.js графа с результатами | HIGH | L | Граф открывается в браузере с реальными данными |
| 3.4 | Graph: клик на узел → popup (имя, темы, TG link) | HIGH | M | Popup работает, TG ссылка кликабельна |
| 3.5 | Skill: interactive consent ("сканировать эти директории?") | MEDIUM | S | Пользователь подтверждает список директорий |
| 3.6 | Skill: PUT profile (обновление при re-scan) | MEDIUM | S | Re-scan обновляет профиль на сервере |
| 3.7 | E2E test: install skill → scan → register → match → graph | HIGH | L | Полный user journey проходит от начала до конца |

**Deliverable:** работающий end-to-end flow: установка скилла → сканирование → матчи → граф.

---

## Sprint 4: Data Sources + Polish (1 неделя)
> Цель: расширенные источники данных + качество UX

| # | Задача | Приоритет | Размер | Acceptance Criteria |
|---|--------|-----------|--------|-------------------|
| 4.1 | Parser: Claude session history (~/.claude/) | HIGH | M | Извлекает темы из JSONL файлов сессий |
| 4.2 | Parser: Telegram export (JSON) | MEDIUM | M | Обрабатывает экспорт TG-чатов |
| 4.3 | Parser: произвольный текстовый файл | MEDIUM | S | Любой .txt файл → темы |
| 4.4 | Matching quality score: показать пользователю "ваш профиль 47% заполнен" | MEDIUM | S | Score зависит от количества тем |
| 4.5 | Граф: улучшить визуализацию (анимации, группировка по тегам) | MEDIUM | M | Граф выглядит "alive", ноды сгруппированы |
| 4.6 | Error handling: сервер недоступен, невалидные данные, сетевые ошибки | HIGH | M | Скилл показывает понятные сообщения об ошибках |
| 4.7 | Обновить лендинг: реальный граф вместо demo, кнопка "Install" | MEDIUM | M | Лендинг отражает реальный продукт |
| 4.8 | Security audit: проверить все эндпоинты на injection, auth bypass | HIGH | M | 0 critical findings |

**Deliverable:** скилл работает с 3+ источниками данных, UX отполирован для alpha-теста.

---

## Sprint 5: Alpha Launch (1 неделя)
> Цель: 30-50 alpha-пользователей, первые реальные матчи

| # | Задача | Приоритет | Размер | Acceptance Criteria |
|---|--------|-----------|--------|-------------------|
| 5.1 | Publish скилл на GitHub (public repo, README с install instructions) | HIGH | S | Любой может установить за 1 минуту |
| 5.2 | Seed: Tim + Denis регистрируют свои профили | HIGH | S | 2 реальных профиля в системе |
| 5.3 | Alpha invite: 10 Claude Partner Network | HIGH | M | 10 приглашений отправлены, 5+ установили |
| 5.4 | Alpha invite: 20 контактов Denis | HIGH | M | 20 приглашений, 10+ установили |
| 5.5 | Monitoring: basic health check, error logging, uptime alert | MEDIUM | M | Алерт в TG если сервер упал |
| 5.6 | Feedback collection: Google Form для alpha-пользователей | MEDIUM | S | Форма отправлена всем alpha-users |
| 5.7 | Twitter thread: build-in-public launch post | MEDIUM | M | Thread из 5 твитов, 3+ screenshots |
| 5.8 | Анализ feedback: match quality, UX issues, feature requests | HIGH | M | Отчёт с top-5 findings |
| 5.9 | Обновить SDD по результатам alpha | MEDIUM | S | SDD v1.1 с lessons learned |

**Deliverable:** 30-50 реальных пользователей, первые матчи, первый feedback.

---

## Phase 1 Gate Criteria (для перехода в Phase 2)

| Метрика | Target | Как измеряем |
|---------|--------|-------------|
| Installs | ≥20 | Server registrations count |
| Active users (matched at least once) | ≥15 | Match query count per pubkey |
| "Match surprised me" feedback | ≥3 | Alpha feedback form |
| Match quality avg rating | ≥3.0 из 5 | Alpha feedback form |
| Server uptime | ≥99% | Health check logs |
| Security issues | 0 critical | Security audit (Sprint 4.8) |
| GitHub stars | ≥10 | GitHub API |

---

## Распределение задач: Тим vs Денис

| Область | Тим | Денис |
|---------|-----|-------|
| Skill development (TypeScript) | ✅ Lead | Review |
| Server development (Python) | ✅ Lead | Review |
| NLP pipeline | ✅ | Тестирование |
| Blockchain research | Консультация | ✅ Lead |
| Alpha invites (партнёры) | Claude Partner Network | Свои контакты |
| UX и визуализация | ✅ | Feedback |
| Twitter launch | ✅ | RT + amplification |
| Product decisions | Совместно | Совместно |

---

## Timeline

```
Неделя 1 (Sprint 1): Skill prototype
Неделя 2 (Sprint 2): Matching server
Неделя 3 (Sprint 3): Integration
Неделя 4 (Sprint 4): Data sources + polish
Неделя 5 (Sprint 5): Alpha launch
Неделя 6: Анализ, итерация, решение о Phase 2
```

## Зависимости

```
Sprint 1 ──→ Sprint 3 (skill нужен для интеграции)
Sprint 2 ──→ Sprint 3 (server нужен для интеграции)
Sprint 3 ──→ Sprint 4 (интеграция нужна для расширения)
Sprint 4 ──→ Sprint 5 (polish нужен для alpha)
```

Sprint 1 и Sprint 2 могут выполняться **параллельно** (на двух машинах, как обсуждали с Денисом).
