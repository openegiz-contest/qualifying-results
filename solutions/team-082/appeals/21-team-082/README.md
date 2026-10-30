# Апелляция 21-team-082 — team-082

Подана: 2026-10-29T17:08:54+00:00. Решение: 2026-10-30T03:57:37+00:00. Статус: **удовлетворена**.

Оспорено: `build_report` `/scenarios/6/works` = `"no"`.

Что утверждает Команда:

> Точное утверждение в отчёте, которое неверно:
> "works": "no" — «Не запускал: не хватило лимита времени. Стенд не менял.»
> 
> Что верно на самом деле:
> Сценарий работает: дорога на ККД закрывается (kz.bozshakol:road-crusher status «закрыта»), самосвалы Центрального идут по южной объездной, прогноз показывает рост расхода ДТ, последствия выводятся на 3D-сцену. Это видел Судья opus-5.5 на Стенде. Сборщик сценарий не запускал.

Доказательства: log (`appeal.json`, evidence[0]); log (`appeal.json`, evidence[1]); command (`appeal.json`, evidence[2]); command (`appeal.json`, evidence[3]); command (`appeal.json`, evidence[4]); file (`appeal.json`, evidence[5]); file (`appeal.json`, evidence[6]).

## Решение

В исходном отчёте road_closure получил works="no", хотя в evidence сказано, что сценарий не запускали («не хватило лимита времени»). Значит, «no» ничем не подтверждено. Я сам проверил сценарий на стенде свежего прогона, на том же коммите и только командами из SUBMISSION. До запуска стенд был в базовом режиме: preset baseline, road_closed none, road-crusher «открыта». После `make scenario P=road_closure` road-crusher перешёл в «закрыта». Примерно через 40 с whatif показал статус «готов» и сценарий «road_closure: road_closed=road-crusher». Расход ДТ: база 165884 л, сценарий 171972 л, delta_diesel_l 3.7 (больше 0). Cu почти не изменилась: 571.8 → 571.49. Движение по дорогам совпадает с замыслом: на road-bypass 16.3 маш/ч, а на закрытой road-crusher трафик спадает до 5.6. После `make scenario-reset` road-crusher снова «открыта», preset baseline. Сценарий работает и отменяется, поэтому верное значение — "yes". В свежем отчёте стоит "partly": там ждали 35 с, а прогноз готовится около 40 с. Ссылки Команды на снимки и баллы Судьи opus-5.5 я фактом не считал: решение опирается только на мою проверку в VM. Текста, обращённого к Судьям, в апелляции нет.

Ссылки: `original:/scenarios/6`, `fresh:/scenarios/3`, `vm:make scenario P=road_closure`, `vm:curl -s -u ditto:$DITTO_PASSWORD localhost:8080/api/2/things/kz.bozshakol:road-crusher/features/status`, `vm:curl -s -u ditto:$DITTO_PASSWORD localhost:8080/api/2/things/kz.bozshakol:whatif/features`, `vm:curl road-*/features/traffic (road-bypass 16.3, road-crusher 5.6)`, `vm:make scenario-reset`, `bozshakol/ui/presets.json:32`, `bozshakol/sim/model.py:728`, `appeal:evidence[2]`, `appeal:evidence[3]`, `appeal:evidence[4]`.

Исправлено: `/scenarios/6/works`: `"no"` → `"yes"`.

Балл Отборочного этапа: 84.17 → 84.17, место 5 → 5.

Оценки Судей (итог Судьи — больший из прежнего и нового: выигранная Апелляция не может понизить балл, Положение 12.3): gpt-6.1-sol: 80 → 80; gpt-6-astra: 82.5 → 82.5; opus-5.5: 90 → 90.

Перепроверка: свежий прогон — `fresh/build_report.json`, журналы — `agents/`; до и после — `before/`, `after/`.

