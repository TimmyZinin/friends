# Алгоритм матчинга

## Jaccard Similarity на Bloom Filters

```mermaid
flowchart LR
    A["Bloom Filter A<br/>(1024 бит)"] --> AND["A AND B<br/>(bitwise)"]
    B["Bloom Filter B<br/>(1024 бит)"] --> AND
    A --> OR["A OR B<br/>(bitwise)"]
    B --> OR
    AND --> J["Jaccard = popcount(AND)<br/>÷ popcount(OR)"]
    J --> SCORE["Score: 0.0 — 1.0"]
    SCORE --> THRESH{"> 0.15?"}
    THRESH -->|Да| MATCH["✅ Матч!"]
    THRESH -->|Нет| SKIP["❌ Пропуск"]

    style MATCH fill:#00D4FF,color:#000
    style SKIP fill:#333,color:#fff
```

## Формула

```
similarity(A, B) = |A ∩ B| / |A ∪ B|

Для Bloom filters:
  intersection = bitwise_AND(A, B)
  union        = bitwise_OR(A, B)
  similarity   = popcount(intersection) / popcount(union)
```

## Интерпретация

| Score | Значение | Действие |
|-------|---------|---------|
| 0.00 — 0.10 | Нет общих тем | Не показывать |
| 0.10 — 0.15 | Минимальное сходство | Не показывать (ниже threshold) |
| 0.15 — 0.25 | Есть общие интересы | Показать в графе (далёкий узел) |
| 0.25 — 0.40 | Среднее сходство | Показать (средний узел) |
| 0.40 — 0.60 | Сильное сходство | Показать рядом (близкий узел) |
| 0.60 + | Очень похожие | Выделить особо |

## Top-K Selection

```mermaid
flowchart TD
    INPUT["Bloom filter пользователя"]
    DB["Все Bloom filters в базе (N шт)"]
    CALC["Вычислить Jaccard vs каждый"]
    FILTER["Отфильтровать score < 0.15"]
    SORT["Сортировать по убыванию"]
    TOPK["Взять первые 20"]
    RESULT["Вернуть [{name, tg, city, score}]"]

    INPUT --> CALC
    DB --> CALC
    CALC --> FILTER
    FILTER --> SORT
    SORT --> TOPK
    TOPK --> RESULT
```

## Производительность

| Масштаб | Bloom filters в RAM | Время матчинга | Подход |
|---------|-------------------|----------------|--------|
| 100 users | 12.8 KB | <1ms | Linear scan |
| 1,000 users | 128 KB | <10ms | Linear scan |
| 10,000 users | 1.28 MB | <100ms | Linear scan |
| 100,000 users | 12.8 MB | ~1s | LSH (Locality-Sensitive Hashing) |
| 1,000,000 users | 128 MB | ~100ms с LSH | LSH + sharding |

## Feedback Loop (Phase 2)

```mermaid
flowchart LR
    MATCH["Матч показан"] --> RATE{"Пользователь<br/>оценил?"}
    RATE -->|👍| UP["Увеличить вес<br/>общих тегов"]
    RATE -->|👎| DOWN["Уменьшить вес<br/>общих тегов"]
    RATE -->|💬 Connected| STRONG["Сильно увеличить<br/>вес"]
    UP --> WEIGHTS["Персональные веса<br/>(хранятся на клиенте)"]
    DOWN --> WEIGHTS
    STRONG --> WEIGHTS
    WEIGHTS --> NEXT["Следующий запрос<br/>матчей учитывает веса"]
```
