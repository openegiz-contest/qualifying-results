# team-096 — Cool Thanks

Коммит Заморозки: `1ef64a51bb132843d4610a988ab8544d2557d76b`. Статус: оценено. Балл Отборочного этапа: 2.5 (место 45).

Потолок применён: not_built_on_openegiz.

## Отчёт сборки

Поднялось по README: да. Построено на OpenEgiz: no — The Team has built nothing of its own on the platform. Ditto (GET /api/2/search/things) holds only the 5 Template Example Mine twins (org.openegiz.mine:mine-01, crusher-01, excavator-01, truck-01, truck-02). They do update via MQTT: in two snapshots 35 s apart, excavator-01 went from state loading to idle, passes_total from 9 to 10 and face_grade from 0.677 to 0.784, and mine-01 trucks_hauling went from 1 to 2. The connection mosquitto-source-connection (mqtt-5) is open. Grafana has only the Template's 'Example Mine' dashboard. The repository has no Team code: team/ contains only README.md, and the only commits after 'Initial commit' change SUBMISSION.md. SUBMISSION.md describes no Team twins. The Template marks the Example Mine as 'not a basis for the Submission'. So the platform works, but there are no Team copper-mine twins, data flow or interface that could be counted as the Submission built on OpenEgiz.

Полностью: `build_report.json`, логи шагов — `logs/`, проверки — `healthchecks/`, журнал Сборщика — `agents/`.

## Здоровье Стенда

Платформу OpenEgiz на Стенде проверял скрипт: 6 проверок (после сборки или восстановления, до и после каждого Судьи), из них с отказом — 0. Все проверки — `stand-health.jsonl`.


## Детектор инъекций

Вердикт: **clean** (`injection_verdict.json`).

## Оценки Судей

### gpt-6.1-sol: 3.75/100

| Критерий | Уровень | Баллы | Обоснование | Ссылки |
|---|---|---|---|---|
| model | 0/4 | 0/25 | Через API Ditto и приложение OpenEgiz проверены пять двойников: рудник, экскаватор, два самосвала и дробилка. Все соответствуют Примеру рудника; собственных объектов и состояний Команды нет. История изменений содержит только правки SUBMISSION.md. | ditto:org.openegiz.mine:mine-01, examples/mine/twins.json:2, build_report:built_on_openegiz |
| behavior | 0/4 | 0/20 | Состояния прочитаны в 21:20:57 и 21:22:00 UTC: passes_total экскаватора вырос с 10 до 20, truck-01 сменил returning на hauling, payload вырос с 0 до 90 т. Однако это поведение неизменённого симулятора Примера, а не работа Команды. | ditto:org.openegiz.mine:excavator-01, ditto:org.openegiz.mine:truck-01, examples/mine/simulator.py:3, build_report:built_on_openegiz |
| visualization | 0/4 | 0/25 | В браузере открыт Example Mine: показатели и графики тоннажа, содержания, положения и загрузки самосвалов. Геометрии рудника и собственной визуализации Команды нет; раздел визуализации оставлен пустым. | screenshot:team-096-example-dashboard.png, SUBMISSION.md:50, README.md:22 |
| scenarios | 0/4 | 0/10 | Таблица сценариев пуста, способов запуска и отмены нет. Проверять нечего; сценарии не запускались, Стенд не изменялся. | SUBMISSION.md:33, build_report:scenarios |
| modules | 0/4 | 0/5 | Модули не заявлены и в интерфейсе не обнаружены. Доступный дашборд Примера показывает существующие данные, но не выдаёт планов, прогнозов или рекомендаций. | SUBMISSION.md:33, screenshot:team-096-example-dashboard.png, build_report:modules |
| concept | 1/4 | 3.75/15 | Назван вымышленный медный карьер по аналогии с Актогаем и Бозшаколем и задача снижения экологического ущерба и рекультивации. Пользователь определён широко, источники параметров только обещаны. На Стенде замысел не реализован: работает лишь Пример рудника. presentation.pdf отсутствует, что также ограничивает уровень единицей. | SUBMISSION.md:7, SUBMISSION.md:9, SUBMISSION.md:13, SUBMISSION.md:15, build_report:built_on_openegiz, build_report:notes |

Полностью: `scores/gpt-6.1-sol.json`, журнал Судьи — `agents/judge-gpt-6.1-sol.jsonl`.

### gpt-6-astra: 3.75/100

| Критерий | Уровень | Баллы | Обоснование | Ссылки |
|---|---|---|---|---|
| model | 0/4 | 0/25 | Через API Ditto и приложение OpenEgiz проверены только пять двойников Примера: рудник, экскаватор, два самосвала и дробилка. Их состояния и иерархия соответствуют examples/mine/twins.json. Собственных двойников нет; изменения после начального коммита затрагивают только SUBMISSION.md. | ditto:org.openegiz.mine:mine-01, examples/mine/twins.json:2, build_report:built_on_openegiz |
| behavior | 0/4 | 0/20 | Два чтения API с интервалом 65 секунд подтвердили обновления: tonnes_mined выросло с 270 до 360 т, passes_total — с 20 до 30, truck-01 перешёл из returning в hauling. Однако это поведение неизменённого симулятора Примера; собственной реализации поведения нет. | ditto:org.openegiz.mine:mine-01, ditto:org.openegiz.mine:excavator-01, ditto:org.openegiz.mine:truck-01, examples/mine/simulator.py:3 |
| visualization | 0/4 | 0/25 | В браузере открыт Example Mine: только числовые показатели и временные графики тоннажа, положения, загрузки и топлива. Геометрии рудника и собственной визуализации Команды нет; соответствующий раздел заявки пуст. | screenshot:team-096-example-mine.png, SUBMISSION.md:50, examples/mine/README.md:21 |
| scenarios | 0/4 | 0/10 | Таблица сценариев пуста, способов запуска и отмены Команда не описала. Проверяемых сценариев нет. Ничего не запускал, состояние Стенда не изменял. | SUBMISSION.md:29, SUBMISSION.md:35 |
| modules | 0/4 | 0/5 | Модули не заявлены и не обнаружены в коде или интерфейсе. На Стенде работают только двойники и дашборд Примера; отображение существующих показателей самостоятельным Модулем не является. | SUBMISSION.md:33, screenshot:team-096-example-mine.png, build_report:modules |
| concept | 1/4 | 3.75/15 | Назван вымышленный медный карьер по аналогии с Актогаем и Бозшаколем и задача уменьшения экологического ущерба и планирования восстановления земель. Пользователь определён широко, источники параметров только обещаны. Стенд от замысла не зависит: экологическая модель, визуализация и сценарии отсутствуют. presentation_info подтвердил отсутствие presentation.pdf. Для уровня 2 нужна реализация собственной задачи на Стенде. | SUBMISSION.md:7, SUBMISSION.md:9, SUBMISSION.md:13, SUBMISSION.md:15, ditto:org.openegiz.mine:mine-01 |

Полностью: `scores/gpt-6-astra.json`, журнал Судьи — `agents/judge-gpt-6-astra.jsonl`.

### opus-5.5: 0/100

| Критерий | Уровень | Баллы | Обоснование | Ссылки |
|---|---|---|---|---|
| model | 0/4 | 0/25 | В Ditto (search/things) только 5 двойников Примера рудника из Шаблона: org.openegiz.mine:mine-01, crusher-01, excavator-01, truck-01, truck-02. Своих двойников у Команды нет. В team/ лежит только README.md, а коммиты после Initial commit меняют только SUBMISSION.md. Раздел Mine пуст. Модели медного карьера из Замысла нет. | ditto:org.openegiz.mine:excavator-01, build_report:built_on_openegiz, SUBMISSION.md:30 |
| behavior | 0/4 | 0/20 | Обновляется только симулятор Примера рудника из Шаблона: по Отчёту сборки состояние excavator-01 и mine-01 меняется, но это не работа Команды. Своей симуляции или данных в репозитории нет, на Стенде только Пример рудника. | build_report:built_on_openegiz, ditto:org.openegiz.mine:mine-01 |
| visualization | 0/4 | 0/25 | В Grafana есть только папка OpenEgiz Examples с дашбордом Example Mine из Шаблона. Своей визуализации Команды нет, раздел Mine visualization в SUBMISSION.md пуст, README остался заготовкой Шаблона. | screenshot:team096-dashboards.png, SUBMISSION.md:50 |
| scenarios | 0/4 | 0/10 | В таблице Modules and What-if Scenarios одна пустая строка. Сценариев нет, запускать нечего, Стенд я не менял. | SUBMISSION.md:38, build_report:scenarios |
| modules | 0/4 | 0/5 | Модулей нет ни в SUBMISSION.md, ни в коде, ни на Стенде (в Отчёте сборки modules: []). | build_report:modules, SUBMISSION.md:38 |
| concept | 0/4 | 0/15 | Замысел написан: вымышленный медный карьер по образцу Актогая и Бозшаколя, задача — снизить вред земле и окружающей среде и спланировать рекультивацию. Но пользователь назван общими словами («все заинтересованные»), а источники цифр только обещаны («будут использоваться»), в данные они не перенесены. Главное: из Замысла на Стенде не сделано ничего — нет ни модели, ни визуализации, ни сценариев, Стенд от Замысла не зависит. presentation.pdf в Решении отсутствует (presentation_info: missing), поэтому потолок — уровень 1. Раз из Замысла ничего не реализовано, ставлю 0. | SUBMISSION.md:5, build_report:concept, presentation.pdf:0 |

Полностью: `scores/opus-5.5.json`, журнал Судьи — `agents/judge-opus-5.5.jsonl`.

### sonnet-5.5: 3.75/100 (не учтена: Судья исключён из Отборочного этапа до публикации состава)

| Критерий | Уровень | Баллы | Обоснование | Ссылки |
|---|---|---|---|---|
| model | 0/4 | 0/25 | В Ditto только 5 двойников Примера рудника из Шаблона. Своих двойников у Команды нет: в team/ лежит один README.md, а разделы Mine и Modules в SUBMISSION.md пусты. | build_report:built_on_openegiz, build_report:notes |
| behavior | 0/4 | 0/20 | Меняются только данные Примера рудника, то есть работа Шаблона. Своей симуляции или данных у Команды нет. | build_report:built_on_openegiz |
| visualization | 0/4 | 0/25 | Своей визуализации нет. В Grafana есть только дашборд Example Mine из Шаблона, раздел Mine visualization в SUBMISSION.md пуст. Я открыл Grafana (страница входа), но своей визуализации Команды там не нашёл. | screenshot:grafana.png, build_report:notes |
| scenarios | 0/4 | 0/10 | Сценариев нет: список scenarios в Отчёте сборки пуст, а строка таблицы в SUBMISSION.md пустая. | build_report:scenarios |
| modules | 0/4 | 0/5 | Работающих Модулей нет: список modules в Отчёте сборки пуст. | build_report:modules |
| concept | 1/4 | 3.75/15 | Замысел написан: вымышленный карьер по мотивам Актогая и Бозшокола, цель — меньше вреда земле и рекультивация. Но на Стенде от него ничего не сделано, а остальные разделы SUBMISSION.md пусты. README остался шаблонным. | build_report:concept, build_report:notes |

Полностью: `scores/sonnet-5.5.json`, журнал Судьи — `agents/judge-sonnet-5.5.jsonl`.

