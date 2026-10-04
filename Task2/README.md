# Task2. Проектирование RTB и интеграции с DSP

Сервис ставок и его взаимодействие с новым DSP-партнёром: не менее 18 000 RPS, ответ не дольше 80 ms, штрафы за деградацию и простои. Целевая архитектура – [Task1/TO-BE.md](../Task1/TO-BE.md).

## Документы

| Файл | Содержание |
|---|---|
| [bidding-service.md](bidding-service.md) | Спецификация сервиса ставок: границы, API, зависимости, модель данных, паттерны надёжности |
| [interaction.md](interaction.md) | Протоколы взаимодействия: gRPC внутри, HTTPS / OpenRTB с партнёрами, Kafka для показов и кликов, выбор API Gateway |
| [api-gateway.md](api-gateway.md) | Дизайн API Gateway (Envoy): маршрутизация, rate limiting, аутентификация, Circuit Breaker, мониторинг времени отклика |
| [diagrams/sequence-bid-request.puml](diagrams/sequence-bid-request.puml) | Sequence: обработка bid request, включая промах кеша и no-bid |
| [diagrams/sequence-impression-click.puml](diagrams/sequence-impression-click.puml) | Sequence: регистрация показа или клика с повтором и идемпотентностью |
| [diagrams/component-bidding-service.puml](diagrams/component-bidding-service.puml) | C4 Component: устройство Bidding Service |

## Ключевые решения

- Bidding Service объединяет бывшие Ad Server и Auction Engine: меньше сетевых вызовов на пути bid request.
- Одна операция API: bid request → bid response; при отказе ставить – no-bid, партнёр получает HTTP 204.
- Внутри gRPC, с партнёрами HTTPS / OpenRTB, показы и клики через Kafka.
- API Gateway – Envoy: нужные функции есть из коробки.
- На пути bid request повторов нет; Circuit Breaker на вызовах Campaign Service; резервная стратегия – no-bid.
- Показы и клики повторяются на шлюзе с тем же идентификатором запроса – деньги не спишутся дважды.
