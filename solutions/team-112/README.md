# team-112 — Shansharkhan Zhandos

Коммит Заморозки: `b16c867146602459c01d8dac8f5e858c295e664f`. Статус: оценено. Балл Отборочного этапа: 0 (место 46).

## Отчёт сборки

Поднялось по README: да. Построено на OpenEgiz: yes — На поднятом Стенде все три части выполнены, но только для Example Mine Организатора; своего кода у Команды нет. (1) GET /api/2/search/things возвращает 5 двойников org.openegiz.mine:* (crusher-01, excavator-01, mine-01, truck-01, truck-02). (2) Признаки меняются через 40 с: truck-01 перешёл из hauling в dumping, route_position 1.215→3.2, fuel 88.1→86.2; у mine-01 trucks_hauling 2→1. Соединения mosquitto-source-connection (telemetry/#) и mosquitto-target-connection открыты (connectionStatus и liveStatus open). Симулятор публикует в mqtt://mosquitto:1883. (3) Источник данных Grafana — InfluxDB opentwins-influxdb, панели дашборда Example Mine используют Flux-запросы from(bucket:"default"). В InfluxDB есть измерение mqtt_consumer с topic opentwins/twin/events/org.openegiz.mine/... — это события Ditto, которые туда пишет Telegraf. Всё это — немодифицированные make up и make example-mine из Шаблона.

Полностью: `build_report.json`, логи шагов — `logs/`, проверки — `healthchecks/`, журнал Сборщика — `agents/`.

## Здоровье Стенда

Платформу OpenEgiz на Стенде проверял скрипт: 7 проверок (после сборки или восстановления, до и после каждого Судьи), из них с отказом — 0. Все проверки — `stand-health.jsonl`.


## Детектор инъекций

Вердикт: **clean** (`injection_verdict.json`).

## Оценки Судей

### gpt-6.1-sol: 0/100

| Критерий | Уровень | Баллы | Обоснование | Ссылки |
|---|---|---|---|---|
| model | 0/4 | 0/25 | Через API Ditto прочитал пять двойников, в OpenEgiz осмотрел иерархию: рудник, экскаватор, два самосвала и дробилка. Все соответствуют неизменённому Example Mine Организатора. Своих двойников Команда не создала. | ditto:org.openegiz.mine:mine-01, examples/mine/twins.json:2, build_report:notes |
| behavior | 0/4 | 0/20 | Два чтения API с интервалом более минуты подтвердили живую симуляцию: truck-01 перешёл из loading в returning, число рейсов выросло с 1 до 2, тоннаж дробилки — со 180 до 270 т. Однако это поведение неизменённого примера Организатора; собственной симуляции Команды нет. | ditto:org.openegiz.mine:truck-01, ditto:org.openegiz.mine:crusher-01, examples/mine/simulator.py:3, build_report:notes |
| visualization | 0/4 | 0/25 | В браузере открыл Example Mine: показаны числовые показатели и временные графики положения, загрузки, содержания и топлива. Геометрии рудника и собственной визуализации Команды нет. Открытый дашборд принадлежит примеру Организатора. | screenshot:team-112-example-mine.png, examples/mine/README.md:21, SUBMISSION.md:52 |
| scenarios | 0/4 | 0/10 | Таблица сценариев пустая, способы запуска и отмены не описаны. Проверяемых сценариев нет; вмешательств в Стенд не выполнял. | SUBMISSION.md:35, build_report:scenarios |
| modules | 0/4 | 0/5 | Модули не заявлены, собственного функционального кода Команды не обнаружено. На Стенде увидел только двойники и показатели Example Mine; работающих функций, выдающих план, прогноз или решение, нет. | SUBMISSION.md:35, team/README.md:3, build_report:modules[0] |
| concept | 0/4 | 0/15 | Раздел Concept остался заготовкой: предприятие, пользователь, решение и обоснование не заполнены. README также шаблонный. presentation_info подтвердил отсутствие presentation.pdf. Собственного Замысла нет. | SUBMISSION.md:9, SUBMISSION.md:13, README.md:1, build_report:concept |

Полностью: `scores/gpt-6.1-sol.json`, журнал Судьи — `agents/judge-gpt-6.1-sol.jsonl`.

### gpt-6-astra: 0/100

| Критерий | Уровень | Баллы | Обоснование | Ссылки |
|---|---|---|---|---|
| model | 0/4 | 0/25 | Через API Ditto и приложение OpenEgiz проверены пять двойников: рудник, экскаватор, два самосвала и дробилка. Состояния и иерархия есть, но полностью относятся к Example Mine Организатора. Проверка истории кода подтвердила отсутствие изменений модели командой; собственных двойников нет. | ditto:org.openegiz.mine:mine-01, examples/mine/twins.json:2, screenshot:team-112-twins.png, build_report:notes |
| behavior | 0/4 | 0/20 | За 68 секунд truck-01 перешёл из loading в hauling: загрузка 0→90 т, позиция 0→3,101 км, топливо 80,1→77,3%. Поведение живое, но обеспечено неизменённым симулятором Example Mine. Собственной реализации команды нет, поэтому пример не засчитывается. | ditto:org.openegiz.mine:truck-01, examples/mine/simulator.py:101, build_report:notes |
| visualization | 0/4 | 0/25 | В браузере открыт Example Mine: показатели тоннажа и содержания, графики положения, загрузки и топлива самосвалов. Это штатный дашборд Организатора, без визуализации геометрии рудника. Собственная визуализация команды отсутствует. | screenshot:team-112-example-mine.png, SUBMISSION.md:52, examples/mine/README.md:21 |
| scenarios | 0/4 | 0/10 | Таблица сценариев пустая; способов запуска и отмены команда не описала. Проверяемых сценариев нет. Вмешательств в работу Стенда не выполнял. | SUBMISSION.md:31, SUBMISSION.md:37 |
| modules | 0/4 | 0/5 | Работающих собственных модулей не обнаружено: таблица заявления пустая, код команды не добавлен, на Стенде только пример и отображение его телеметрии. Графики существующих данных модулем не являются. | SUBMISSION.md:35, screenshot:team-112-example-mine.png, build_report:notes |
| concept | 0/4 | 0/15 | Раздел Concept остался заготовкой: предприятие, пользователь, решение и обоснование не заполнены. Стенд содержит только пример Организатора. Инструмент presentation_info подтвердил отсутствие presentation.pdf. Собственного замысла нет. | SUBMISSION.md:5, SUBMISSION.md:9, SUBMISSION.md:17, README.md:14 |

Полностью: `scores/gpt-6-astra.json`, журнал Судьи — `agents/judge-gpt-6-astra.jsonl`.

### opus-5.5: 0/100

| Критерий | Уровень | Баллы | Обоснование | Ссылки |
|---|---|---|---|---|
| model | 0/4 | 0/25 | В Ditto только 5 двойников Примера рудника Организатора (crusher-01, excavator-01, mine-01, truck-01, truck-02). Коммиты Команды затрагивают только LICENSES/ и REUSE.toml, своих двойников и кода нет. | ditto:org.openegiz.mine:truck-01, build_report:notes, build_report:built_on_openegiz |
| behavior | 0/4 | 0/20 | Состояние меняет только симулятор Примера рудника из Шаблона. Своего поведения Команда не сделала, поэтому по Рубрике это уровень 0. | build_report:modules[0], ditto:org.openegiz.mine:mine-01 |
| visualization | 0/4 | 0/25 | На Стенде открывается только дашборд Grafana «Example Mine» Организатора. Своей визуализации у Команды нет, раздел Mine visualization в SUBMISSION.md пуст. | screenshot:team112-example-mine.png, SUBMISSION.md:52 |
| scenarios | 0/4 | 0/10 | В таблице Modules and What-if Scenarios только пустая строка. Сценариев нет, поэтому запускать было нечего. | SUBMISSION.md:34, build_report:scenarios |
| modules | 0/4 | 0/5 | Модули не заявлены и не реализованы, работает только Пример рудника из Шаблона. | SUBMISSION.md:34, build_report:modules[0] |
| concept | 0/4 | 0/15 | Раздел Concept остался заготовкой Шаблона: заполнены только метки и комментарии-подсказки. presentation.pdf в Решении нет, presentation_info возвращает статус missing. | SUBMISSION.md:5, build_report:concept |

Полностью: `scores/opus-5.5.json`, журнал Судьи — `agents/judge-opus-5.5.jsonl`.

