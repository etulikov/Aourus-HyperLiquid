# Список академических работ по алготрейдингу

## Теги

Список тегов:
| Тег | Описание тега |
| -------- | ------- |
| PUBLIC-HL | можно тестировать на публичных bbo / l2Book / trades / asset context. |
| CROSS | требует публичных фидов других venues (Binance/Bybit/Coinbase/CME и т.п.). |
| EXEC | placement, market making, inventory, fill/adverse selection. |
| L3/L4 | per-order/order-id данные; для HL это optional research track, а не prerequisite. |
| PERP/FUNDING | механика perpetuals, funding, basis, liquidation. |
| VALIDATION/REGIME | защита от backtest overfitting и non-stationarity.
| BBO | Best Bid / Best Offer. Только лучший bid и лучший ask: цена, размер, иногда число ордеров. Самый лёгкий top-of-book feed. |
| TRADES | поток сделок: цена, размер, сторона агрессора, timestamp, trade id и т.п. |
| ORDER-FLOW | поток действий, которые меняют рынок: market trades, limit adds, cancels, updates. Это шире, чем просто trades. |
| L2 | агрегированный стакан по уровням цены. Например: price -> total size, без отдельных order IDs. |
| MARKET-MAKING | работы про выставление bid/ask, управление inventory, spread, adverse selection, quoting. |
| HAWKES | модели Hawkes process, где события увеличивают вероятность новых событий вскоре после них. Часто применяют к trades/cancels/limit orders для моделирования clustering/self-excitation. |
| SHORT-ALPHA | краткосрочный предиктивный сигнал: вероятность движения цены через условно 10–500 мс или несколько событий вперёд. |
| RISK | inventory risk, liquidation risk, drawdown, adverse selection, tail risk, leverage и т.д. |
| LATENCY | задержка данных/исполнения: кто раньше увидел событие, сколько времени идёт feed, order ack, fill и т.п. |

## Структура

Работы сгруппированы по роли в торговом стеке: сигнал → котировка → риск → валидация → площадка.

| Категория | О чём | Работ |
| --- | --- | --- |
| [`1-signals/`](1-signals/) | что можно предсказать по данным: fair value, короткий горизонт, импакт потока | 2 |
| [`2-quoting/`](2-quoting/) | как превратить сигнал в bid/ask: спред, инвентарь, placement | 1 |
| [`3-risk/`](3-risk/) | inventory risk, drawdown, хвосты, плечо, ликвидация | — |
| [`4-validation/`](4-validation/) | overfitting, нестационарность, честная оценка издержек | — |
| [`5-venue/`](5-venue/) | специфика Hyperliquid: perps, funding, ликвидации, фиды, латентность | — |

Внутри категории каждая работа — самодостаточный пакет `<slug>/`:

```
library/<категория>/<slug>/
├── document.md     — основной текст: заголовки, проза, формулы в LaTeX, относительные ссылки на ассеты
├── metadata.json   — машиночитаемый манифест (авторы, дата, источник, теги, список ассетов и таблиц)
├── README.md       — что лежит в пакете, в каком он состоянии и где конверсия намеренно не правит источник
├── assets/*.png    — фигуры, диаграммы и превью таблиц из PDF
└── tables/*.csv    — таблицы в машиночитаемом виде (+ `tables.md` — они же в Markdown)
```

`assets/` и `tables/` есть не у всех работ — только там, где в исходной статье есть что извлекать.
Теги работы указаны строкой `**Tags: ...**` в шапке `document.md` и продублированы в `metadata.json`.
Работа лежит в одной категории — той, ради чего её читают; смежные темы ловятся тегами, а не копиями папок.

## Содержание

### 1-signals

| Работа | Год | Авторы | Теги |
| --- | --- | --- | --- |
| [The price impact of order book events](1-signals/price-impact-ob-events-cont-kukanov-stoikov/document.md) | 2011 | Cont, Kukanov, Stoikov | PUBLIC-HL, L2, TRADES |
| [The Micro-Price: A High Frequency Estimator of Future Prices](1-signals/microprice-stoikov/document.md) | 2018 | Stoikov | PUBLIC-HL, L2, BBO, SHORT-ALPHA |

**The price impact of order book events.** Cont, Kukanov & Stoikov, март 2011 (arXiv:1011.6402v3). На TAQ-данных по 50 акциям США показано, что на коротких интервалах цену двигает order flow imbalance (OFI) на лучших котировках, а не объём сделок. Связь OFI → изменение цены линейная, наклон обратно пропорционален глубине рынка; результат устойчив к внутридневной сезонности, к выбору масштаба времени и к выбору бумаги. Отсюда же выводится эмпирический «square-root» закон для объёма.
Пакет: `document.md`, `tables.md`, `metadata.json`, 15 фигур в `assets/`, 6 таблиц в `tables/`.

**The Micro-Price.** Stoikov, апрель 2018 (SSRN id3165260). Микроцена — предел последовательности ожидаемых mid-price, мартингал по построению, то есть «справедливая» цена при данном стакане. Выражается как поправка к mid, зависящая от спреда и imbalance на лучших уровнях; оценивается по high-frequency данным как марковская цепь на конечном пространстве состояний. Эмпирически предсказывает цену на горизонте 10 с – 3 мин лучше, чем mid и weighted mid, причём поправка ведёт себя по-разному для large-tick (BAC) и small-tick (CVX) бумаг.
Пакет: `document.md`, `metadata.json`, 5 фигур в `assets/`. Таблиц в статье нет.

### 2-quoting

| Работа | Год | Авторы | Теги |
| --- | --- | --- | --- |
| [High-frequency trading in a limit order book](2-quoting/hft-limit-ob-avellaneda-stoikov/document.md) | 2006 | Avellaneda, Stoikov | EXEC, MARKET-MAKING |

**High-frequency trading in a limit order book.** Avellaneda & Stoikov, октябрь 2006. Оптимальные bid/ask котировки маркет-мейкера при inventory risk: mid-price — броуновское движение, приход маркет-ордеров — пуассоновский с интенсивностью, убывающей по расстоянию от mid. Решение в два шага: indifference price по текущему инвентарю, затем калибровка спреда к стакану. Симуляции показывают меньшую дисперсию P&L и конечного инвентаря против симметричного квотирования.
Пакет: `document.md`, `metadata.json`, 4 фигуры в `assets/`. Три таблицы симуляций — Markdown-таблицы внутри `document.md`, CSV нет.

### 3-risk, 4-validation, 5-venue

Пока пусто — см. README внутри каждой категории.
