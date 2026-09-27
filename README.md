# Solution-AdScale

Проектная работа: эволюция архитектуры AdScale – SaaS-платформы для RTB-рекламы – под интеграцию с новым DSP-партнёром (18 000 RPS, ответ не дольше 80 ms) и рост до 50 000 RPS через год.

| Задание | Содержание |
|---|---|
| [Task1](Task1/README.md) | Архитектурная диагностика (AS-IS), драйверы, целевая архитектура (TO-BE), ADR-001 |
| [Task2](Task2/README.md) | Сервис ставок, протоколы взаимодействия, API Gateway для DSP |
| [Task3](Task3/README.md) | Данные: БД по сервисам, масштабирование, кеширование, Kafka, отказоустойчивость |

Диаграммы – PlantUML с локальной копией библиотеки [C4-PlantUML](C4PlantUML/). PNG-картинки генерирует GitHub Actions ([plantuml.yml](.github/workflows/plantuml.yml)).
