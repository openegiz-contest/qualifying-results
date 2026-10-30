# Апелляция 30-team-082 — team-082

Подана: 2026-10-29T17:18:42+00:00. Решение: 2026-10-30T04:47:17+00:00. Статус: **удовлетворена**.

Оспорено: `build_report` `/scenarios/13/works` = `"no"`.

Что утверждает Команда:

> Точное утверждение в отчёте, которое неверно:
> "works": "no" — «Не запускал: не хватило лимита времени. Стенд не менял.»
> 
> Что верно на самом деле:
> Сценарий работает: ремонт по отказу: плановых простоев на ТО нет, прогноз в whatif пересчитывается (готовность парка delta_fleet_avail выше базы). Отменяется make scenario-reset. Сборщик сценарий не запускал, поэтому «no» — не результат проверки.

Доказательства: command (`appeal.json`, evidence[0]); command (`appeal.json`, evidence[1]); command (`appeal.json`, evidence[2]); command (`appeal.json`, evidence[3]); file (`appeal.json`, evidence[4]); file (`appeal.json`, evidence[5]).

## Решение

Исходное значение «no» — не результат проверки. В evidence прямо написано, что сценарий не запускали из-за лимита времени. Я проверил сам. До запуска стенд был в базовом режиме: preset baseline, maintenance_strategy preventive. После `make scenario P=reactive` в control.maintenance_strategy стало reactive. Двойник whatif перешёл в статус «расчёт», а через ~30 с — в «готов», со scenario «reactive: maintenance_strategy=reactive». Получилось base_fleet_avail 91.8 против scen_fleet_avail 91.82: delta_fleet_avail округляется до 0.0, scen_cu_t 568.9 при base 568.97. Это совпадает с SUBMISSION (строка 132: «за 48 ч разница в отказах не проявилась»). `make scenario-reset` вернул стенд в базовый режим: preset baseline, strategy preventive, delta 0. Значит, сценарий применяется, прогноз пересчитывается и отмена работает, так что «no» неверно. Ставлю «partly», а не «yes», по двум причинам. Во-первых, заметного эффекта в прогнозе нет: утверждение Команды, что delta_fleet_avail «больше 0», верно лишь на +0.02 до округления. Во-вторых, что плановые ТО в живой модели действительно исчезают, я сам не видел. Свежий прогон тоже дал «partly». В материалах Апелляции текста, обращённого к Судьям, нет.

Ссылки: `original:/scenarios/13`, `fresh:/scenarios/13`, `vm:make scenario P=reactive`, `vm:curl -s -u ditto:*** localhost:8080/api/2/things/kz.bozshakol:control/features`, `vm:curl -s -u ditto:*** localhost:8080/api/2/things/kz.bozshakol:whatif/features`, `vm:make scenario-reset`, `bozshakol/ui/presets.json:112`, `SUBMISSION.md:132`, `appeal:evidence[0]`, `appeal:evidence[2]`.

Исправлено: `/scenarios/13/works`: `"no"` → `"partly"`.

Балл Отборочного этапа: 84.17 → 84.17, место 5 → 5.

Оценки Судей (итог Судьи — больший из прежнего и нового: выигранная Апелляция не может понизить балл, Положение 12.3): gpt-6.1-sol: 80 → 80; gpt-6-astra: 82.5 → 82.5; opus-5.5: 90 → 90.

Перепроверка: свежий прогон — `fresh/build_report.json`, журналы — `agents/`; до и после — `before/`, `after/`.

