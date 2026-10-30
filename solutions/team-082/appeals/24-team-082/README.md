# Апелляция 24-team-082 — team-082

Подана: 2026-10-29T17:16:19+00:00. Решение: 2026-10-30T04:13:19+00:00. Статус: **удовлетворена**.

Оспорено: `build_report` `/scenarios/7/works` = `"no"`.

Что утверждает Команда:

> Точное утверждение в отчёте, которое неверно:
> "works": "no" — «Не запускал: не хватило лимита времени. Стенд не менял.»
> 
> Что верно на самом деле:
> Сценарий работает: ограничение 30 км/ч на магистралях: самосвалы на дорогах едут не быстрее 30 км/ч, цикл рейса длиннее, прогноз в whatif пересчитывается (delta_waste_t около −0,7 %). Отменяется make scenario-reset. Сборщик сценарий не запускал, поэтому «no» — не результат проверки.

Доказательства: command (`appeal.json`, evidence[0]); command (`appeal.json`, evidence[1]); command (`appeal.json`, evidence[2]); command (`appeal.json`, evidence[3]); file (`appeal.json`, evidence[4]); file (`appeal.json`, evidence[5]).

## Решение

В исходном отчёте значение «no» не было результатом проверки: в evidence сказано, что сценарий не запускали из-за лимита времени. В свежем прогоне сценарий запущен: haulage.speed_limit сменился с 50 на 30, прогноз показал Cu −1,0 %, после reset значение вернулось к 50 (там оценка «partly», потому что прогноз появился с задержкой).

Я проверил сам на работающем стенде. До запуска: control.speed_limit_kmh=50, haulage.speed_limit=50, preset baseline. Запустил `make scenario P=speed_limit` и через 45 с увидел:
- control.speed_limit_kmh=30;
- haulage.speed_limit=30;
- whatif.scenario «speed_limit: speed_limit_kmh=30»;
- прогноз пересчитан: delta_cu_t −1,0 %, delta_ore_t −1,6 %, delta_waste_t −1,3 %, delta_moved_t −1,5 %, delta_margin −0,8 %.

После `make scenario-reset` haulage.speed_limit снова 50, стенд вернулся в baseline.

Сценарий работает: модель приняла ограничение, а прогноз пересчитался и дал ожидаемые отрицательные изменения. Скорость каждого самосвала ht-* отдельно я не проверял. Цифра Команды «delta_waste_t около −0,7 %» не совпала с моей (−1,3 %), но знак тот же, и на вывод это не влияет.

Значение «no» неверно, правильное — «yes». Обращений к ИИ в материалах Апелляции нет.

Ссылки: `original:/scenarios/7`, `fresh:/scenarios/4`, `vm:make scenario P=speed_limit; curl -s -u ditto:$P localhost:8080/api/2/things/kz.bozshakol:whatif/features`, `vm:curl -s -u ditto:$P localhost:8080/api/2/things/kz.bozshakol:haulage/features`, `bozshakol/ui/presets.json:40`, `appeal:evidence[0]`, `appeal:evidence[3]`.

Исправлено: `/scenarios/7/works`: `"no"` → `"yes"`.

Балл Отборочного этапа: 84.17 → 84.17, место 5 → 5.

Оценки Судей (итог Судьи — больший из прежнего и нового: выигранная Апелляция не может понизить балл, Положение 12.3): gpt-6.1-sol: 80 → 80; gpt-6-astra: 82.5 → 82.5; opus-5.5: 90 → 90.

Перепроверка: свежий прогон — `fresh/build_report.json`, журналы — `agents/`; до и после — `before/`, `after/`.

