# Список академических работ по алготрейдингу

## Теги

В каждом документе будет раздел `@TAGS: tag1, tag2, tag3`.
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
