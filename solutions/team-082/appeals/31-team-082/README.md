# Апелляция 31-team-082 — team-082

Подана: 2026-10-29T17:18:57+00:00. Решение: 2026-10-30T04:53:48+00:00. Статус: **удовлетворена**.

Оспорено: `build_report` `/scenarios/14/works` = `"no"`.

Что утверждает Команда:

> Точное утверждение в отчёте, которое неверно:
> "works": "no" — «Не запускал: не хватило лимита времени. Стенд не менял.»
> 
> Что верно на самом деле:
> Сценарий работает: ТО по состоянию и 2 CAT 785C в резерве: в двойнике control trucks_parked 2, два самосвала уходят в состояние parked, прогноз в whatif: вскрыша около +7 %, расход ДТ ниже базы. Отменяется make scenario-reset. Сборщик сценарий не запускал, поэтому «no» — не результат проверки.

Доказательства: command (`appeal.json`, evidence[0]); command (`appeal.json`, evidence[1]); command (`appeal.json`, evidence[2]); command (`appeal.json`, evidence[3]); file (`appeal.json`, evidence[4]); file (`appeal.json`, evidence[5]).

## Решение

Ни исходный, ни свежий Сборщик результат fleet_optimum не наблюдал: в исходном отчёте написано «не запускал», в свежем — «запущен в фоне, результаты не наблюдал». Поэтому «no» — не результат проверки. Я запустил сценарий сам на свежем стенде из базового режима (preset baseline, trucks_parked 0, preventive) командой `make scenario P=fleet_optimum`, как указано в SUBMISSION.md:133.

Что увидел через 50 с:
- В control: preset fleet_optimum, trucks_parked 2, maintenance_strategy predictive.
- whatif пересчитался под этот сценарий (status «готов», scenario «fleet_optimum: trucks_parked=2, maintenance_strategy=predictive»): вскрыша +5,3 %, ДТ −1,8 %, Cu −0,1 %, КТГ +1,1 %, очередь −48,8 %.
- Самосвал ht-15 ушёл в to_park, а через 90 с — в parked.

Это совпадает с обещанным: preset из presets.json:120, в SUBMISSION «ДТ −0,4 %, вскрыша +7 %». Знак эффектов тот же, величина близкая. Значит, сценарий работает.

Отмена `make scenario-reset` вернула preset baseline, trucks_parked 0, preventive, whatif «базовый режим».

Замечание: вместе со сценарием число самосвалов в standby/to_reserve выросло с 0 до 16 и после reset за 30 с не спало. Похоже на побочный эффект PdM: в свежем отчёте для pdm то же самое. Это касается поля undone, а оно не оспорено. Текста, обращённого к Судьям, в апелляции нет.

Ссылки: `vm:make scenario P=fleet_optimum`, `vm:curl -u ditto:… localhost:8080/api/2/things/kz.bozshakol:control/features`, `vm:curl -u ditto:… localhost:8080/api/2/things/kz.bozshakol:whatif/features`, `vm:curl -u ditto:… localhost:8080/api/2/search/things?filter=like(thingId,"kz.bozshakol:ht-*")`, `vm:make scenario-reset`, `bozshakol/ui/presets.json:120`, `SUBMISSION.md:133`, `fresh:/scenarios/14`, `original:/scenarios/14`, `appeal:evidence[0]`, `appeal:evidence[1]`, `appeal:evidence[2]`.

Исправлено: `/scenarios/14/works`: `"no"` → `"yes"`.

Балл Отборочного этапа: 84.17 → 84.17, место 5 → 5.

Оценки Судей (итог Судьи — больший из прежнего и нового: выигранная Апелляция не может понизить балл, Положение 12.3): gpt-6.1-sol: 80 → 80; gpt-6-astra: 82.5 → 82.5; opus-5.5: 90 → 90.

Перепроверка: свежий прогон — `fresh/build_report.json`, журналы — `agents/`; до и после — `before/`, `after/`.

