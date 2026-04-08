# Friends Protocol

**Найди друга, о котором ты не знал.**

Friends Protocol — открытый протокол нетворкинга по знаниям. Соединяет людей по интеллектуальному отпечатку — из markdown-файлов, AI-диалогов, переписок и заметок. Без фото, без анкет, без свайпов.

## Как это работает

1. Установи скилл `/friends` в Claude Code
2. Скилл извлекает темы из твоих локальных файлов (на устройстве)
3. Темы кодируются в **Bloom filter** (необратимый битовый массив)
4. Только Bloom filter отправляется на matching server
5. Видишь **интерактивный граф** совместимых людей
6. Кликни на узел → свяжись через Telegram

## Приватность

Извлечение тем и кодирование происходят **полностью на устройстве**. Сервер получает только Bloom filter — битовый массив фиксированного размера, который невозможно обратить в исходные темы. Сервер не видит, не хранит и не обрабатывает файлы, текст или сырые данные.

## Документация (SDD)

| Документ | Описание |
|---------|---------|
| [SDD.md](docs/SDD.md) | System Design Document v1.0 — полная спецификация |
| [PRODUCT_VISION.md](docs/PRODUCT_VISION.md) | Видение продукта, персоны, конкуренты |
| [ZK_ARCHITECTURE.md](docs/ZK_ARCHITECTURE.md) | Zero-Knowledge архитектура: Bloom → PSI → FHE → ZK-proofs |
| [PROTOCOL_SPEC.md](docs/PROTOCOL_SPEC.md) | Спецификация Friends Protocol (5 слоёв) |
| [API_SPEC.md](docs/API_SPEC.md) | REST API — 7 эндпоинтов |
| [BLOCKCHAIN_ROADMAP.md](docs/BLOCKCHAIN_ROADMAP.md) | Блокчейн: смарт-контракты, токеномика, фазы |
| [LICENSING.md](docs/LICENSING.md) | Лицензирование и IP-защита |
| [DIGITAL_DNA.md](docs/DIGITAL_DNA.md) | Концепция Цифрового ДНК (брейндамп Дениса) |
| [DNA_STRUCTURE.md](docs/DNA_STRUCTURE.md) | 3 слоя ДНК: структурный + социальный + интенциональный |
| [SECURITY.md](docs/SECURITY.md) | Модель угроз + GDPR compliance |
| [BACKLOG_PHASE1.md](docs/BACKLOG_PHASE1.md) | Phase 1: 5 спринтов, 43 задачи |
| [launch-strategy.md](docs/launch-strategy.md) | GTM: 5 фаз, каналы, метрики |
| [expert-panel-results.md](docs/expert-panel-results.md) | 35 идей из брейншторма — экспертная оценка |

## Wiki

Страницы с Mermaid-диаграммами: [wiki/](wiki/)

## Лендинг

[timzinin.com/friends](https://timzinin.com/friends/) — интерактивный граф (EN/RU)

## Статус

- ✅ SDD документация v1.0
- ✅ MVP лендинг с графом
- 🔧 Claude Code скилл (в разработке)
- 📋 Matching server (планируется)

## Авторы

- [Тим Зинин](https://github.com/TimmyZinin)
- Денис Говорунов
