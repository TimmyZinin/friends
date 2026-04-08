# Friends Protocol -- Анализ лицензирования и IP-стратегия

> Версия: 1.0
> Дата: 2026-04-08
> Основатели: Tim Zinin, Denis Govorunov

## Контекст

Friends -- knowledge networking protocol, распространяемый как open-source Claude Code skill. Ядро ценности -- алгоритм matching на основе Bloom filter + Jaccard similarity. Код должен быть открыт (доверие, аудит, community), но основатели должны сохранить возможность монетизации и защиту от враждебных форков.

---

## 1. Обзор лицензий

| Лицензия | Открытость кода | Copyleft | SaaS-защита | Коммерческая защита | Patent grant | Сложность |
|----------|:-:|:-:|:-:|:-:|:-:|:-:|
| MIT | Полная | Нет | Нет | Нет | Нет | Минимальная |
| Apache 2.0 | Полная | Нет | Нет | Нет | Да | Низкая |
| GPL v3 | Полная | Да | Нет | Частичная | Да | Средняя |
| AGPL v3 | Полная | Да | Да | Средняя | Да | Средняя |
| BSL 1.1 | Чтение/изучение | Нет | Да | Сильная | Нет (добавляемо) | Средняя |
| SSPL | Полная | Агрессивный | Максимальная | Сильная | Нет | Высокая |
| Custom (Uniswap-style) | Чтение/изучение | Кастомная | Да | Максимальная | Кастомная | Высокая |

### MIT

Полная свобода. Кто угодно берет код, делает closed-source SaaS, зарабатывает миллионы -- и ничего не должен основателям. Для протокола, где ядро ценности в алгоритме matching -- это подарок конкурентам.

**Вердикт:** не подходит для Friends.

### Apache 2.0

Как MIT, но с явным patent grant (пользователи получают лицензию на патенты контрибьюторов) и защитой от патентных троллей (если контрибьютор подает патентный иск -- теряет лицензию). Код все равно можно закрыть и коммерциализировать без отчислений.

**Вердикт:** хороший Change License для BSL (см. рекомендацию), но сам по себе не защищает.

### GPL v3

Copyleft: любой fork обязан открыть исходники. Но есть SaaS-лазейка: если код работает на сервере и пользователи взаимодействуют через API, а не скачивают бинарник -- GPL не требует раскрытия. Google, Amazon и другие крупные компании годами используют GPL-код в своих сервисах, не открывая ничего.

**Вердикт:** не закрывает главную угрозу (SaaS-клон).

### AGPL v3

GPL + network use clause: если код выполняется на сервере и пользователи взаимодействуют с ним через сеть, модифицированный код обязан быть раскрыт. Это закрывает SaaS-лазейку. MongoDB начинала с AGPL (до перехода на SSPL). Grafana, Nextcloud, Mastodon используют AGPL.

**Плюсы:** форки обязаны открывать код; крупные компании избегают AGPL-кода (compliance-отделы блокируют), что снижает риск клонирования.

**Минусы:** не запрещает коммерческое использование -- только требует открытости; community может опасаться AGPL (некоторые компании запрещают его в своих стеках).

**Вердикт:** сильный вариант, особенно в связке с CLA.

### BSL 1.1 (Business Source License)

Изобретена MariaDB. Модель: код открыт для чтения, изучения, тестирования и некоммерческого использования. Коммерческое использование (production) -- только по отдельной лицензии от правообладателя. Через фиксированный срок (обычно 2-4 года) код автоматически переходит под Change License (обычно Apache 2.0 или GPL).

**Кто использует:**
- **MariaDB** -- BSL, Change License = GPL v2, delay = 4 года
- **CockroachDB** -- BSL, Change License = Apache 2.0, delay = 3 года
- **Sentry** -- BSL, Change License = Apache 2.0, delay = 3 года
- **Uniswap v3** -- BSL, Change License = GPL v2, delay = 2 года
- **HashiCorp (Terraform, Vault)** -- BSL, Change License = MPL 2.0, delay = 4 года

**Плюсы:** код виден всем (аудит, доверие); нельзя взять и запустить конкурирующий SaaS; через N лет код становится полностью открытым; не пугает community так сильно, как SSPL.

**Минусы:** технически не является open-source по определению OSI (OSI не одобряет BSL); некоторые разработчики принципиально не контрибьютят в BSL-проекты.

**Вердикт:** оптимальный баланс для Friends.

### SSPL (Server Side Public License)

Изобретена MongoDB после того, как AWS начал продавать MongoDB-as-a-service. Суть: если ты предоставляешь код как сервис -- ты обязан открыть весь свой стек (включая оркестрацию, мониторинг, деплой). Это де-факто делает коммерческое SaaS-использование невозможным без лицензии от правообладателя.

**Проблемы:** OSI отвергла SSPL как open-source; Debian, Fedora, Red Hat удалили SSPL-пакеты из репозиториев; community воспринимает SSPL враждебно; Elasticsearch отказался от SSPL и вернулся к AGPL.

**Вердикт:** слишком агрессивно для Friends на текущей стадии. Вредит community-building.

### Custom Protocol License (Uniswap-style)

Uniswap v3 использовал BSL с дополнительным условием: коммерческое использование требует интеграции с Uniswap Protocol (protocol fee). По сути: "можешь использовать код, но часть revenue идет через наш протокол".

**Для Friends это значит:** можно добавить к BSL условие, что коммерческое использование matching engine обязывает направлять трафик через Friends Protocol API (и платить per-match fee).

**Проблема:** требует юриста для drafting ($3-5K), сложнее enforce.

**Вердикт:** преждевременно для MVP. Рассмотреть на Phase 3 при масштабировании.

---

## 2. Рекомендация: BSL 1.1

### Параметры лицензии

```
License:           Business Source License 1.1
Licensor:          Tim Zinin & Denis Govorunov (или Friends Protocol LLC/ИП)
Licensed Work:     Friends Protocol (matching engine, skill code, server)
Change Date:       3 года с даты каждого релиза
Change License:    Apache License 2.0
Additional Use Grant: Non-production use (testing, development, education, 
                      personal non-commercial) is permitted without restriction.
```

### Что это означает на практике

| Действие | Разрешено? |
|----------|:-:|
| Прочитать код, изучить, форкнуть для обучения | Да |
| Запустить локально для тестирования и разработки | Да |
| Использовать в академических исследованиях | Да |
| Контрибьютить (pull requests) | Да |
| Использовать в production для коммерческого продукта | Нет (нужна лицензия от основателей) |
| Форкнуть и запустить конкурирующий SaaS | Нет (нужна лицензия от основателей) |
| Все вышеперечисленное через 3 года после релиза | Да (Apache 2.0) |

### Почему именно BSL для Friends

1. **Код виден всем.** Пользователи могут аудитить privacy claims (Bloom filter не обратим, данные не утекают). Это критично для продукта, построенного на доверии к приватности.

2. **Защита от клонов.** Amazon/Google/кто угодно не может взять matching engine и запустить "Amazon Friends" без лицензии. Именно эту проблему решала MariaDB (AWS Aurora), MongoDB (AWS DocumentDB), Elastic (AWS OpenSearch).

3. **Монетизация сохранена.** Основатели могут продавать коммерческие лицензии (flat fee, revenue share, per-seat) компаниям, которые хотят использовать протокол в production.

4. **Community-friendly.** Через 3 года код становится Apache 2.0. Это дает четкий сигнал: "мы не жадные, просто хотим head start". Разработчики это понимают и принимают.

5. **Precedent.** CockroachDB, Sentry, HashiCorp -- крупные и успешные проекты на BSL. Модель проверена.

### Почему Change License = Apache 2.0, а не GPL

- Apache 2.0 дает максимальную свободу после истечения срока -- привлекает больше enterprise-пользователей
- Patent grant в Apache 2.0 защищает пользователей от патентных исков
- GPL отпугивает корпоративных пользователей (compliance-отделы)
- Apache 2.0 -- стандарт де-факто для cloud-native проектов

### Почему 3 года, а не 2 или 4

- 2 года (Uniswap): слишком мало для протокола, который еще не монетизирован. Код станет открытым до того, как основатели получат revenue.
- 4 года (MariaDB, HashiCorp): слишком долго для нового проекта. Community может потерять терпение.
- 3 года (CockroachDB, Sentry): баланс. Достаточно для выхода на monetization (Phase 2-3), но не отпугивает early adopters.

---

## 3. Альтернатива: AGPL v3 + CLA

Если BSL кажется слишком ограничительным для community-building на ранней стадии, рабочий вариант -- AGPL v3 + CLA.

### Как это работает

1. **Код под AGPL v3.** Любой fork обязан открыть исходники, включая SaaS-деплои. Это предотвращает закрытые клоны.

2. **CLA (Contributor License Agreement)** дает основателям право лицензировать код коммерчески. Контрибьюторы подписывают CLA при первом PR -- соглашаются, что их вклад может быть лицензирован основателями под любой лицензией.

3. **Dual licensing.** Основатели предлагают две опции:
   - AGPL v3 (бесплатно, но код обязан быть открыт)
   - Коммерческая лицензия ($X/месяц) -- для компаний, которые не хотят открывать свой код

### Кто так делает

- **GitLab** -- MIT (CE) + проприетарный (EE), но ранние версии были AGPL
- **Grafana** -- AGPL v3 + коммерческая лицензия
- **Nextcloud** -- AGPL v3 + enterprise subscriptions
- **MongoDB** (до SSPL) -- AGPL v3 + коммерческая лицензия

### Плюсы AGPL + CLA vs BSL

| Критерий | AGPL + CLA | BSL 1.1 |
|----------|:-:|:-:|
| OSI-approved (формально open-source) | Да | Нет |
| Community perception | Лучше | Хуже |
| Привлечение контрибьюторов | Проще | Сложнее |

### Минусы AGPL + CLA vs BSL

| Критерий | AGPL + CLA | BSL 1.1 |
|----------|:-:|:-:|
| Защита от SaaS-клонов | Средняя (можно обойти) | Сильная |
| Enforcement сложность | Высокая (нужно доказать нарушение) | Низкая (нарушение очевидно) |
| Enterprise-восприятие | Многие компании блокируют AGPL | BSL более предсказуема |
| Зависимость от CLA | Да (без CLA нельзя менять лицензию) | Нет |

### Вердикт по альтернативе

AGPL + CLA -- хороший запасной вариант, если community-building является абсолютным приоритетом на ранней стадии. Но для Friends, где ядро ценности в алгоритме matching, BSL дает более четкую защиту.

---

## 4. Патентная стратегия

### Что патентовать

Ядро IP Friends Protocol -- метод matching на основе ZK Bloom filter:
- Извлечение тематических тегов из markdown-файлов (TF-IDF + keyword extraction)
- Кодирование тегов во взвешенный Bloom filter на устройстве пользователя
- Вычисление Jaccard similarity на Bloom filter без деобфускации данных
- Feedback loop для коррекции весов в matching

### Provisional Patent (US)

**Что это:** заявка, фиксирующая дату приоритета (priority date) на 12 месяцев. За это время нужно подать полную заявку или priority date теряется.

**Зачем:** если кто-то подаст патент на аналогичный метод после вашей provisional -- ваша дата приоритета раньше.

| Этап | Стоимость | Срок |
|------|----------|------|
| Provisional patent application (US) | $1,500-2,000 (с юристом) | 1-2 недели на подготовку |
| Full patent application (US) | $8,000-15,000 | Подать в течение 12 мес после provisional |
| PCT (международная заявка) | $3,000-5,000 (сверху) | Подать в течение 12 мес после provisional |
| Examination + prosecution | $5,000-10,000 | 2-4 года |

**Итого до выдачи патента US:** $15,000-25,000 и 2-4 года.

### Альтернатива: Defensive Publication

**Что это:** публикация описания изобретения в открытом доступе (например, на arXiv, Zenodo, или через Defensive Patent License). Это создает "prior art" -- после публикации никто (включая вас) не может запатентовать этот метод.

**Зачем:** если цель -- не монетизация через патент, а предотвращение патентования конкурентами. Бесплатно.

**Как:**
1. Написать техническое описание алгоритма (3-5 страниц)
2. Опубликовать на arXiv или Zenodo (с DOI)
3. Дополнительно: зарегистрировать через IP.com Prior Art Database

**Стоимость:** $0 (если писать самим) или $500-1,000 (если с юристом для правильной формулировки).

### Рекомендация по патентам

**Стадия MVP (сейчас):** defensive publication. Денег на патент нет, но prior art зафиксировать критично -- это бесплатная страховка от patent trolls и крупных компаний.

**Стадия Phase 2 (после первого revenue):** пересмотреть необходимость provisional patent. Если matching algorithm станет ядром монетизации -- имеет смысл. Если monetization через event matching / B2B -- патент менее важен.

**Стадия Phase 3 (масштабирование):** если revenue > $50K/год -- full patent + PCT.

---

## 5. Trademark

### Что регистрировать

- **"Friends Protocol"** -- словесный знак
- **Логотип** (когда появится) -- изобразительный знак
- **"Friends"** отдельно -- сложнее (слово общеупотребительное), но в контексте "networking protocol software" может пройти

### Классы NICE

- **Класс 9:** Software, mobile apps, downloadable computer programs
- **Класс 42:** SaaS, cloud computing, software as a service
- **Класс 38:** Telecommunications services (если будет messaging)

### Стоимость

| Юрисдикция | Стоимость (1 класс) | Срок регистрации |
|------------|:--:|:--:|
| US (USPTO) | $250-350 (TEAS Plus) | 8-12 мес |
| EU (EUIPO) | EUR 850 (1 класс) | 4-6 мес |
| РФ (Роспатент) | 35,000 руб (~$350) | 12-18 мес |

**Для 2 классов (9 + 42) в US + EU:** ~$2,000-2,500.

### Рекомендация по трademarks

**Сейчас:** ничего не регистрировать. Стоимость не оправдана до product-market fit. Но зафиксировать дату первого публичного использования (GitHub repo, лендинг) -- это дает common law trademark rights в US.

**После PMF (Phase 2):** зарегистрировать "Friends Protocol" в US (USPTO), класс 9 + 42. ~$500-700.

**При международном масштабировании (Phase 3):** добавить EU (EUIPO). ~$1,500.

---

## 6. CLA (Contributor License Agreement)

### Зачем нужен CLA

Без CLA каждый контрибьютор сохраняет copyright на свой код. Это означает:
- Нельзя сменить лицензию без согласия КАЖДОГО контрибьютора
- Нельзя предложить dual licensing (AGPL + коммерческая) без согласия КАЖДОГО
- Один несогласный контрибьютор может заблокировать изменение лицензии навсегда

С CLA контрибьюторы заранее соглашаются, что основатели могут лицензировать их вклад под любой лицензией. Это стандарт для проектов с dual licensing.

### Кто использует CLA

- **Apache Foundation** -- Apache ICLA (Individual CLA)
- **Google** -- Google CLA для всех open-source проектов
- **Facebook/Meta** -- CLA для React, PyTorch и др.
- **HashiCorp** -- CLA (после перехода на BSL)
- **CockroachDB** -- CLA
- **GitLab** -- DCO (Developer Certificate of Origin) -- упрощенная версия

### Как внедрить

1. **Выбрать шаблон:** Apache ICLA -- наиболее проверенный и уважаемый в community
2. **Настроить CLA-бот:** [cla-assistant.io](https://cla-assistant.io) -- бесплатный GitHub App
3. **Workflow:** при первом PR бот просит подписать CLA (кликнуть "I agree"). Без подписи PR не может быть merged

### Текст CLA (основные пункты)

```
Контрибьютор предоставляет Лицензиару (Tim Zinin & Denis Govorunov):
1. Неисключительную, безотзывную, всемирную лицензию на copyright
2. Право сублицензировать контрибьюцию под любой лицензией
3. Патентный грант на патенты, покрываемые контрибьюцией
4. Подтверждение, что контрибьюция -- оригинальная работа
```

### Рекомендация по CLA

**Внедрить CLA с первого дня.** Это бесплатно (cla-assistant.io), занимает 15 минут на настройку, и без него любые будущие изменения лицензии станут юридическим кошмаром. Не ждать "когда будут контрибьюторы" -- CLA должен быть на месте ДО первого PR от внешнего разработчика.

---

## 7. Сравнительная таблица стратегий

Оценка по шкале 1-5 (5 = лучше).

| Критерий | MIT | Apache 2.0 | GPL v3 | AGPL v3 + CLA | BSL 1.1 | SSPL | Custom |
|----------|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| **Открытость кода** | 5 | 5 | 5 | 5 | 4 | 3 | 3 |
| **Защита от клонов** | 1 | 1 | 2 | 3 | 5 | 5 | 5 |
| **Монетизация** | 1 | 1 | 2 | 4 | 5 | 5 | 5 |
| **Community-friendliness** | 5 | 5 | 4 | 3 | 3 | 1 | 2 |
| **Enterprise adoption** | 5 | 5 | 2 | 2 | 4 | 1 | 2 |
| **Юридическая простота** | 5 | 5 | 3 | 2 | 3 | 2 | 1 |
| **Патентная защита** | 1 | 4 | 4 | 4 | 2 | 2 | 3 |
| **ИТОГО** | **23** | **26** | **22** | **23** | **26** | **19** | **21** |

**BSL 1.1 и Apache 2.0 набирают одинаково, но по разным причинам.** Apache 2.0 лидирует в openness и simplicity, BSL -- в защите и монетизации. Для Friends, где монетизация и защита алгоритма -- приоритет, BSL выигрывает.

---

## 8. Итоговый план действий

### Сейчас (Phase 1 -- MVP)

| Действие | Стоимость | Приоритет |
|----------|:-:|:-:|
| Добавить BSL 1.1 в репозиторий (LICENSE файл) | $0 | P0 |
| Настроить CLA через cla-assistant.io | $0 | P0 |
| Defensive publication алгоритма matching (arXiv/Zenodo) | $0 | P1 |
| Зафиксировать дату первого публичного использования "Friends Protocol" | $0 | P1 |

### Phase 2 (после первого revenue)

| Действие | Стоимость | Приоритет |
|----------|:-:|:-:|
| Provisional patent на matching algorithm (US) | $1,500-2,000 | P1 |
| Trademark "Friends Protocol" (USPTO, класс 9+42) | $500-700 | P2 |
| Юрист для review BSL-лицензии | $1,000-2,000 | P2 |

### Phase 3 (масштабирование, revenue > $50K/год)

| Действие | Стоимость | Приоритет |
|----------|:-:|:-:|
| Full patent application (US) | $8,000-15,000 | P1 |
| PCT международная заявка | $3,000-5,000 | P2 |
| Trademark EU (EUIPO) | $1,500 | P2 |
| Custom protocol license (юрист) | $3,000-5,000 | P3 |

---

## 9. Шаблон LICENSE файла (BSL 1.1)

Для немедленного добавления в репозиторий:

```
Business Source License 1.1

Parameters

Licensor:             Tim Zinin & Denis Govorunov
Licensed Work:        Friends Protocol
                      The Licensed Work is (c) 2026 Tim Zinin & Denis Govorunov
Additional Use Grant: You may make use of the Licensed Work, provided that
                      you do not use the Licensed Work for a Production Use.

                      A "Production Use" is any use of the Licensed Work that
                      provides commercial value, including but not limited to:
                      (a) offering the Licensed Work as a service;
                      (b) using the Licensed Work to provide a commercial
                          product or service to third parties;
                      (c) incorporating the Licensed Work into a commercial
                          product.

                      Non-production use (testing, development, education,
                      research, personal non-commercial) is permitted without
                      restriction.

Change Date:          [Дата релиза + 3 года, например: 2029-04-08]
Change License:       Apache License, Version 2.0

For information about alternative licensing arrangements for the Licensed Work,
please contact: [email контакт основателей]

Notice

Business Source License 1.1 is not an Open Source license. However, the
Licensed Work will eventually be made available under an Open Source license,
as stated in this License.

The text of the Business Source License 1.1 is available at:
https://mariadb.com/bsl11/
```

---

## Ссылки

- [BSL 1.1 Full Text](https://mariadb.com/bsl11/) -- MariaDB
- [CockroachDB BSL FAQ](https://www.cockroachlabs.com/blog/oss-relicensing-cockroachdb/)
- [Sentry BSL Announcement](https://blog.sentry.io/relicensing-sentry/)
- [HashiCorp BSL](https://www.hashicorp.com/bsl)
- [CLA Assistant](https://cla-assistant.io/) -- бесплатный GitHub CLA bot
- [Apache ICLA Template](https://www.apache.org/licenses/icla.pdf)
- [Defensive Patent License](https://defensivepatentlicense.org/)
- [arXiv](https://arxiv.org/) -- для defensive publication
- [USPTO TEAS Plus](https://www.uspto.gov/trademarks/apply) -- онлайн-регистрация trademark
