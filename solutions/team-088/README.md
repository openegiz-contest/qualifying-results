# team-088 — Kaznu23

Коммит Заморозки: `8984e65243e357d7e13e778ad1278e6ef867d870`. Статус: оценено. Балл Отборочного этапа: 2.5 (место 44).

Потолок применён: not_built_on_openegiz.

## Отчёт сборки

Поднялось по README: да. Построено на OpenEgiz: no — Своих двойников рудника SmartMine AI у Команды нет. В коммите 8984e65 от Шаблона изменён только SUBMISSION.md, team/ содержит только README.md Шаблона, README не изменён. На Стенде работает только Example Mine из Шаблона, а сам README называет её «not a basis for the Submission». Технически этот пример проходит все три проверки: 5 вещей org.openegiz.mine:* в Ditto, их признаки меняются между снимками с разницей 35 с, соединение mosquitto-source-connection (mqtt-5, telemetry/#) в статусе open, симулятор публикует в MQTT, дашборд читает из InfluxDB. Но тоннелей, вентиляторов, газовых датчиков и подземных машин, описанных в Замысле, как двойников в Ditto нет.

Полностью: `build_report.json`, логи шагов — `logs/`, проверки — `healthchecks/`, журнал Сборщика — `agents/`.

## Здоровье Стенда

Платформу OpenEgiz на Стенде проверял скрипт: 5 проверок (после сборки или восстановления, до и после каждого Судьи), из них с отказом — 0. Все проверки — `stand-health.jsonl`.


## Детектор инъекций

Вердикт: **clean** (`injection_verdict.json`).

## Оценки Судей

### gpt-6.1-sol: 3.75/100

| Критерий | Уровень | Баллы | Обоснование | Ссылки |
|---|---|---|---|---|
| model | 0/4 | 0/25 | Через API Ditto и приложение OpenEgiz проверены пять двойников Example Mine: рудник, экскаватор, два самосвала и дробилка. Собственных двойников тоннелей, вентиляции и датчиков нет. По истории Git изменён только SUBMISSION.md; модель Примера не является работой Команды. | ditto:org.openegiz.mine:mine-01, examples/mine/README.md:35, build_report:built_on_openegiz |
| behavior | 0/4 | 0/20 | Два чтения API с интервалом более минуты подтвердили живое поведение только Примера: тоннаж вырос с 450 до 540 т, truck-01 перешёл из returning в hauling. Собственного симулятора подземного рудника нет; поведение неизменённого Примера не засчитывается. | ditto:org.openegiz.mine:mine-01, ditto:org.openegiz.mine:truck-01, examples/mine/simulator.py:3, build_report:notes |
| visualization | 0/4 | 0/25 | В браузере открыт Example Mine: показаны числовые показатели и графики тоннажа, положения, загрузки и топлива. Геометрии подземного рудника и собственной визуализации Команды нет; соответствующий раздел SUBMISSION.md пуст. | screenshot:team-088-example-dashboard.png, SUBMISSION.md:65, examples/mine/README.md:21 |
| scenarios | 0/4 | 0/10 | Таблица сценариев пуста, способов запуска и отмены нет. Проверяемых сценариев Команды не обнаружено; вмешательств в Стенд не выполнял. | SUBMISSION.md:44, SUBMISSION.md:48, build_report:scenarios |
| modules | 0/4 | 0/5 | Работающих Модулей Команды нет. На Стенде доступны показатели Примера; заявленные в Замысле решения по вентиляции, остановке оборудования и газовым тревогам не реализованы. | SUBMISSION.md:13, SUBMISSION.md:48, examples/mine/README.md:55, build_report:modules[0] |
| concept | 1/4 | 3.75/15 | Названы вымышленный подземный медный рудник, пользователи и конкретные решения по безопасности и вентиляции. Однако Стенд от этого Замысла не зависит: работает только Example Mine, а описание прямо откладывает реализацию двойников на будущее. Презентация отсутствует по presentation_info; оснований для уровня 2 нет. | SUBMISSION.md:9, SUBMISSION.md:13, SUBMISSION.md:17, SUBMISSION.md:42, build_report:notes |

Полностью: `scores/gpt-6.1-sol.json`, журнал Судьи — `agents/judge-gpt-6.1-sol.jsonl`.

### gpt-6-astra: 3.75/100

| Критерий | Уровень | Баллы | Обоснование | Ссылки |
|---|---|---|---|---|
| model | 0/4 | 0/25 | Через API Ditto и приложение OpenEgiz проверены пять объектов: рудник, экскаватор, два самосвала и дробилка. Это неизменённый Example Mine с состояниями и родительскими связями. Собственных двойников тоннелей, вентиляции и датчиков SmartMine AI нет. | ditto:org.openegiz.mine:mine-01, examples/mine/twins.json:2, screenshot:team-088-openegiz.png, SUBMISSION.md:42 |
| behavior | 0/4 | 0/20 | Сняты состояния в 20:58:02 и 20:59:16 UTC: truck-01 перешёл из returning в hauling, загрузка выросла с 0 до 90 т; число проходов экскаватора — с 49 до 59. Поведение живое, но полностью обеспечивается неизменённым симулятором Примера. Собственной модели поведения Команды нет. | ditto:org.openegiz.mine:truck-01, ditto:org.openegiz.mine:excavator-01, examples/mine/simulator.py:94, build_report:modules[0] |
| visualization | 0/4 | 0/25 | В браузере открыт Example Mine: показатели и графики тоннажа, содержания, положения, загрузки и топлива. Геометрии рудника и собственной визуализации SmartMine AI нет; раздел визуализации в заявке не заполнен. | screenshot:team-088-example-dashboard.png, SUBMISSION.md:65, README.md:32 |
| scenarios | 0/4 | 0/10 | Таблица сценариев пуста, способов запуска и отмены нет. Проверяемых сценариев Команды не обнаружено. Ничего не запускал и состояние Стенда не менял. | SUBMISSION.md:44, SUBMISSION.md:50, build_report:scenarios |
| modules | 0/4 | 0/5 | Работающих Модулей Команды не обнаружено: таблица пуста, на Стенде только телеметрия Примера. Задуманные предупреждения и управление вентиляцией не реализованы; графики существующих данных Модулями не являются. | SUBMISSION.md:13, SUBMISSION.md:48, examples/mine/README.md:55, screenshot:team-088-example-dashboard.png |
| concept | 1/4 | 3.75/15 | Названы вымышленный подземный медный рудник, пользователи и конкретные решения по вентиляции и безопасности; выбор объяснён. Однако Стенд от Замысла не зависит: работает только карьерный Пример, реализация собственных двойников отложена в тексте. Источники параметров не представлены. presentation_info подтвердил отсутствие presentation.pdf. Для уровня 2 нужна реализация Замысла на Стенде. | SUBMISSION.md:9, SUBMISSION.md:15, SUBMISSION.md:17, SUBMISSION.md:42, ditto:org.openegiz.mine:mine-01 |

Полностью: `scores/gpt-6-astra.json`, журнал Судьи — `agents/judge-gpt-6-astra.jsonl`.

### opus-5.5: 0/100

| Критерий | Уровень | Баллы | Обоснование | Ссылки |
|---|---|---|---|---|
| model | 0/4 | 0/25 | Своих двойников нет. В Ditto только 5 вещей Примера рудника из Шаблона: crusher-01, excavator-01, mine-01, truck-01, truck-02. В git-истории от Initial commit изменён только SUBMISSION.md, в team/ лежит только README.md Шаблона. Тоннелей, вентиляторов, газовых датчиков и подземных машин из Замысла в Ditto нет. | ditto:org.openegiz.mine:truck-01, build_report:built_on_openegiz, SUBMISSION.md:28 |
| behavior | 0/4 | 0/20 | Данные на Стенде даёт только симулятор Примера рудника из Шаблона. Своего симулятора или поведения у Команды нет: кроме SUBMISSION.md, в коде ничего не изменено. | build_report:modules[0], ditto:org.openegiz.mine:mine-01 |
| visualization | 0/4 | 0/25 | Своей визуализации нет, в разделе Mine visualization ничего не написано. В Grafana есть только дашборд openegiz-example-mine из Шаблона. На скриншоте — экран входа в Grafana Стенда, своих видов у Команды нет. | screenshot:grafana-dashboards.png, build_report:modules[0], SUBMISSION.md:62 |
| scenarios | 0/4 | 0/10 | Таблица Modules and What-if Scenarios пуста, сценариев нет, запускать нечего. | SUBMISSION.md:46, build_report:scenarios |
| modules | 0/4 | 0/5 | Модули не заявлены, в коде и на Стенде их нет. | SUBMISSION.md:46, build_report:modules[0] |
| concept | 0/4 | 0/15 | Замысел — вымышленный подземный медный рудник SmartMine AI с контролем вентиляции и газа; названы пользователи и решение. Но Стенд от Замысла никак не зависит: ничего из него не реализовано, раздел Mine говорит, что определения двойников будут описаны после реализации. Источников цифр нет. presentation.pdf отсутствует (presentation_info: missing), поэтому выше уровня 1 оценка быть не может. Из-за полного отсутствия реализации ставлю 0: Замысел остался на бумаге и в скобках-заготовках Шаблона. | SUBMISSION.md:7, SUBMISSION.md:40, build_report:concept |

Полностью: `scores/opus-5.5.json`, журнал Судьи — `agents/judge-opus-5.5.jsonl`.

### sonnet-5.5: 3.75/100 (не учтена: Судья исключён из Отборочного этапа до публикации состава)

| Критерий | Уровень | Баллы | Обоснование | Ссылки |
|---|---|---|---|---|
| model | 0/4 | 0/25 | У Команды нет своих двойников. На Стенде только Example Mine из Шаблона: 5 вещей org.openegiz.mine:*. Тоннелей, вентиляторов и газовых датчиков из Замысла в Ditto нет. | build_report:built_on_openegiz, build_report:modules[0] |
| behavior | 0/4 | 0/20 | Живое поведение есть только у Примера рудника из Шаблона. Своей симуляции Команда не сделала. | build_report:modules[0] |
| visualization | 0/4 | 0/25 | Своей визуализации нет. Есть только стандартный дашборд Grafana из Примера рудника. | screenshot:grafana.png, build_report:modules[0] |
| scenarios | 0/4 | 0/10 | Таблица сценариев в SUBMISSION.md пуста. Сборщик сценариев не нашёл. | build_report:scenarios |
| modules | 0/4 | 0/5 | Заявленных и работающих Модулей нет. | build_report:modules |
| concept | 1/4 | 3.75/15 | Замысел о вымышленном подземном медном руднике SmartMine AI написан, с пользователями и решениями. Но Стенд от него не зависит: из Шаблона изменён только SUBMISSION.md. Модели, визуализации и сценариев под Замысел нет. Презентацию не открывал. | build_report:concept, build_report:built_on_openegiz |

Полностью: `scores/sonnet-5.5.json`, журнал Судьи — `agents/judge-sonnet-5.5.jsonl`.

