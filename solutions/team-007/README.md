# team-007 — Prime Genesis

Коммит Заморозки: `70ca457fd02e6544732cdc82a760d625f714358a`. Статус: оценено. Балл Отборочного этапа: 3.75 (место 39).

Потолок применён: not_built_on_openegiz.

## Отчёт сборки

Поднялось по README: да. Построено на OpenEgiz: no — Платформа поднялась (Ditto, Mosquitto, Telegraf, InfluxDB, Grafana; соединение mosquitto-source-connection open), но на Стенде работает только Example Mine Шаблона. Двойников рудника Команды в Ditto нет (horizon-1-section-a, ventilation-fan-01 → 404), сервис Команды (my_simulator.py) по README не запускается и в MQTT не публикует, дашборда Команды в Grafana нет. По коду симулятор задуман корректно (PUT в Ditto, MQTT telemetry/<name> в формате Ditto Protocol), но на Стенде это не наблюдается.

Полностью: `build_report.json`, логи шагов — `logs/`, проверки — `healthchecks/`, журнал Сборщика — `agents/`.

## Здоровье Стенда

Платформу OpenEgiz на Стенде проверял скрипт: 7 проверок (после сборки или восстановления, до и после каждого Судьи), из них с отказом — 0. Все проверки — `stand-health.jsonl`.


## Детектор инъекций

Вердикт: **clean** (`injection_verdict.json`).

## Оценки Судей

### gpt-6.1-sol: 3.75/100

| Критерий | Уровень | Баллы | Обоснование | Ссылки |
|---|---|---|---|---|
| model | 0/4 | 0/25 | Самостоятельно проверил API Ditto и иерархию в OpenEgiz: присутствуют только пять объектов Example Mine. Заявленные участок газового контроля и ГВУ отвечают 404. Их определения есть в коде, но собственных двойников Команды на Стенде нет. | ditto:org.openegiz.mine:horizon-1-section-a, ditto:org.openegiz.mine:ventilation-fan-01, team/my_simulator.py:54, screenshot:team007-twins-children.png |
| behavior | 0/4 | 0/20 | Повторные чтения с интервалом 70 секунд подтвердили живое поведение только Example Mine: у truck-01 число рейсов выросло с 1 до 2, топливо снизилось с 81,8 до 79,7%. Оба двойника Команды остались недоступны с 404; поведение газового контроля на Стенде не наблюдается. | ditto:org.openegiz.mine:truck-01, ditto:org.openegiz.mine:horizon-1-section-a, ditto:org.openegiz.mine:ventilation-fan-01, build_report:modules[3] |
| visualization | 0/4 | 0/25 | В браузере проверил Grafana: поиск заявленного дашборда «Мониторинг» не дал результатов; API перечисляет только Example Mine. В SUBMISSION визуализацией названы приборы и графики, а геометрия выработок и работа предприятия не представлены. | screenshot:team007-dashboard-search.png, SUBMISSION.md:60, build_report:modules[2], presentation.pdf:10 |
| scenarios | 0/4 | 0/10 | Сам выполнил из team/ указанную команду python3 ~/team-007/team/my_simulator.py: завершение с кодом 2, файл по этому пути отсутствует. До и после попытки участок и ГВУ отвечали 404; последствий нет. Процесс не запустился, отменять нечего, режим Стенда не изменён. | SUBMISSION.md:37, ditto:org.openegiz.mine:horizon-1-section-a, ditto:org.openegiz.mine:ventilation-fan-01, build_report:scenarios[0] |
| modules | 0/4 | 0/5 | В коде есть пороговое включение форсажа при CH4 > 1,0%, однако симулятор описанной командой не запускается, двойников и дашборда Команды на Стенде нет. Работающее предупреждение или автоматическое решение самостоятельно не наблюдал. | team/my_simulator.py:147, SUBMISSION.md:37, build_report:modules[0], ditto:org.openegiz.mine:ventilation-fan-01 |
| concept | 1/4 | 3.75/15 | Названы конкретная подсистема, пользователи и задача автоматического форсажа вентиляции. Презентация читается и объясняет замысел, но Стенд от него не зависит: работает только Example Mine. Заявления о сквозном работающем контуре, реакции за 2 секунды и автономной защите не подтверждены; конкретное реальное предприятие и данные калибровки не представлены. Поэтому уровень не выше 1. | SUBMISSION.md:5, SUBMISSION.md:14, SUBMISSION.md:47, presentation.pdf:10, presentation.pdf:11, README.md:14, ditto:org.openegiz.mine:horizon-1-section-a |

Полностью: `scores/gpt-6.1-sol.json`, журнал Судьи — `agents/judge-gpt-6.1-sol.jsonl`.

### gpt-6-astra: 3.75/100

| Критерий | Уровень | Баллы | Обоснование | Ссылки |
|---|---|---|---|---|
| model | 0/4 | 0/25 | Через API Ditto и Children в OpenEgiz проверены только пять объектов Example Mine. Заявленные участок газового контроля и ГВУ отвечают 404. Их состояния и родительская связь описаны в коде, но собственных двойников команды на Стенде нет. | ditto:org.openegiz.mine:horizon-1-section-a, ditto:org.openegiz.mine:ventilation-fan-01, team/my_simulator.py:54, screenshot:screenshots/team-007-twins.png |
| behavior | 0/4 | 0/20 | За 61 секунду truck-01 изменился: hauling → loading, груз 90 → 87.8 т, рейсы 2 → 3. Это поведение Примера рудника, которое не засчитывается. Двойники команды отсутствуют; фазовая симуляция выброса и продувки существует в коде, но живое поведение газового контроля на Стенде не наблюдается. | ditto:org.openegiz.mine:truck-01, ditto:org.openegiz.mine:horizon-1-section-a, team/my_simulator.py:121, build_report:modules[3] |
| visualization | 0/4 | 0/25 | В браузере адрес дашборда команды показывает Dashboard not found; API Grafana перечисляет только Example Mine. Заявленная визуализация состоит из Gauge, Stat и Time Series, а геометрия выработок и работа предприятия на Стенде не представлены. | screenshot:screenshots/team-007-dashboard-missing.png, SUBMISSION.md:60, build_report:modules[2] |
| scenarios | 0/4 | 0/10 | Лично выполнена команда из SUBMISSION.md: python3 ~/team-007/team/my_simulator.py из каталога team. Она завершилась с кодом 2: файл /home/judge/team-007/team/my_simulator.py не найден. До и после оба затрагиваемых двойника отвечают 404; последствий нет. Процесс не запустился, поэтому отменять через Ctrl+C нечего; режим Стенда не изменён. | SUBMISSION.md:37, ditto:org.openegiz.mine:horizon-1-section-a, ditto:org.openegiz.mine:ventilation-fan-01, build_report:scenarios[0] |
| modules | 0/4 | 0/5 | В коде найдено пороговое включение EMERGENCY_BOOST при CH4 > 1.0%, но на Стенде нет ни соответствующих двойников, ни дашборда, а описанный запуск симулятора завершается ошибкой. Работающего предупреждения или автоматического управления лично не наблюдал. | team/my_simulator.py:146, ditto:org.openegiz.mine:ventilation-fan-01, screenshot:screenshots/team-007-dashboard-missing.png |
| concept | 1/4 | 3.75/15 | Названы конкретная подсистема, пользователи и задача автоматического форсажа вентиляции. Собственный код соответствует этой теме, однако работающий Стенд содержит только Example Mine и от замысла не зависит. Презентация читается и понятна, но заявления о действующих двойниках, оперативном пульте и 100% автономности защиты не подтверждаются Стендом. Конкретное реальное предприятие и источники параметров не указаны. | SUBMISSION.md:5, SUBMISSION.md:14, SUBMISSION.md:17, presentation.pdf:4, presentation.pdf:10, presentation.pdf:11, screenshot:screenshots/team-007-twins.png, screenshot:screenshots/team-007-dashboard-missing.png |

Полностью: `scores/gpt-6-astra.json`, журнал Судьи — `agents/judge-gpt-6-astra.jsonl`.

### opus-5.5: 3.75/100

| Критерий | Уровень | Баллы | Обоснование | Ссылки |
|---|---|---|---|---|
| model | 0/4 | 0/25 | Я сам запросил двойников через API Ditto. На Стенде только двойники Примера рудника: crusher-01, excavator-01, mine-01, truck-01, truck-02. Двойников Команды horizon-1-section-a и ventilation-fan-01 нет, Сборщик получил на них 404. В коде (team/my_simulator.py:54-86) задуманы всего два двойника: участок газового контроля с 4 датчиками и ГВУ с fan_status, rpm и power_kw, оба с _parents mine-01. Но они не созданы: симулятор по README не запускается. Путь ~/team-007 в VM не существует, paho-mqtt не установлен. Своих двойников на Стенде нет, поэтому уровень 0. Даже в коде было бы не выше уровня 1: два объекта. | ditto:org.openegiz.mine:mine-01, build_report:modules[1], team/my_simulator.py:54 |
| behavior | 0/4 | 0/20 | На Стенде меняется только Пример рудника Шаблона. Двойники газа и ГВУ не существуют, их состояние не обновляется. По коду (team/my_simulator.py:121-150) поведение — синусоида плюс шум, а выброс метана включается по расписанию: каждые 20 шагов. На Стенде я этого не наблюдал, поэтому уровень 0. | build_report:modules[0], team/my_simulator.py:125 |
| visualization | 0/4 | 0/25 | В Grafana есть только папка «OpenEgiz Examples» с дашбордом Example Mine. Дашборд Команды «Мониторинг газовой безопасности и ГВУ» не загружен, это видно на скриншоте. По SUBMISSION визуализация Команды — это вообще только панели Gauge, Stat и Time Series, без плана выработок. Это уровень 0 даже при работающем дашборде. | screenshot:team007-dashboards-list.png, build_report:modules[2] |
| scenarios | 0/4 | 0/10 | Единственный сценарий — выброс метана и форсаж ГВУ. По SUBMISSION он запускается командой `python3 ~/team-007/team/my_simulator.py`, но путь ~/team-007 в VM не существует (проверил ls), а модуля paho в Python нет. Сценарий запустить нельзя, состояние Стенда я не менял. Кроме того, «сценарий» встроен в симулятор как периодическое событие и не управляется пользователем. | build_report:scenarios[0], team/my_simulator.py:24 |
| modules | 0/4 | 0/5 | Задуман один простой Модуль: пороговое правило CH4 > 1.0% → EMERGENCY_BOOST (team/my_simulator.py:147). На Стенде он не работает: симулятор не запущен, двойников и дашборда нет. Работающих Модулей нет. | build_report:modules[0], team/my_simulator.py:147 |
| concept | 1/4 | 3.75/15 | Замысел есть и выходит за типовой карьер: аэрогазовый контроль и ГВУ шахты на горизонте -200 м, пользователи — диспетчеры и инженеры ПБ, решение — авто-форсаж ГВУ. Но объект не назван, и ссылок на источники цифр нет. «Decision» описан как архитектура стека, а не как решение пользователя. Главное — на Стенде от Замысла ничего нет. SUBMISSION и презентация утверждают, что сквозной пайплайн работает «без критических ошибок» (presentation.pdf:5, presentation.pdf:10, presentation.pdf:11), а это противоречит Стенду. Поэтому не выше уровня 1. Попыток повлиять на Судью не нашёл. | SUBMISSION.md:3, presentation.pdf:11, presentation.pdf:5, build_report:concept |

Полностью: `scores/opus-5.5.json`, журнал Судьи — `agents/judge-opus-5.5.jsonl`.

