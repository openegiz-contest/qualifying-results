# Апелляция 20-team-082 — team-082

Подана: 2026-10-29T17:08:29+00:00. Решение: 2026-10-30T03:52:08+00:00. Статус: **удовлетворена**.

Оспорено: `build_report` `/scenarios/17/works` = `"no"`.

Что утверждает Команда:

> Точное утверждение в отчёте, которое неверно:
> "works": "no" — «Не запускал: не хватило лимита времени. Стенд не менял.»
> 
> Что верно на самом деле:
> Сценарий работает: он задаёт 25 % руды с Восточного, вскрышу EX-01 900 т/ч и 4 CAT 785C на Восточном; прогноз в kz.bozshakol:whatif показывает рост вскрытых запасов Восточного через полгода (около 1,2 мес против 0,2–0,5 в базе) и снижение запасов Центрального. Отменяется make scenario-reset. Сборщик сценарий не запускал.

Доказательства: command (`appeal.json`, evidence[0]); command (`appeal.json`, evidence[1]); command (`appeal.json`, evidence[2]); command (`appeal.json`, evidence[3]); file (`appeal.json`, evidence[4]); file (`appeal.json`, evidence[5]).

## Решение

Работа сценария проверена на стенде свежего прогона, тот же коммит. Код и данные Решения не менялись. Исходный и свежий Сборщики сценарий plan_east_strip не наблюдали: исходный его не запускал, в свежем он стоял последним в фоновой очереди. Поэтому «no» в отчёте означает только «не проверено», а не что сценарий не работает.

Что я сделал и увидел:
1. До запуска стенд был в базовом режиме: preset=baseline, east_ore_share 0.3, trucks_east 5, waste_east_tph 500. В whatif разницы нет: базовый и сценарный прогноз совпадают.
2. Выполнил `make scenario P=plan_east_strip` и подождал 50 с. Двойник control: preset=plan_east_strip, east_ore_share 0.25, trucks_east 4, waste_east_tph 900. Это совпадает с presets.json:149–157.
3. Whatif пересчитался (status «готов», scenario «plan_east_strip: east_ore_share=0.25, trucks_east=4, waste_east_tph=900.0»):
   - запасы Восточного (scen_exposed6_east_mo) — 1.19 мес против 0.27 в базе, +340.7 %;
   - запасы Центрального (scen_exposed6_central_mo) — 3.29 мес против 3.76 в базе, −12.5 %.
   Это ровно тот эффект, который описан в SUBMISSION.
4. `make scenario-reset` вернул всё к базе: preset baseline, 0.3/5/500, в whatif разница 0.

Сценарий работает так, как заявлено, и отменяется. Обращений к ИИ или Судьям в материалах Апелляции нет.

Другие расхождения в опубликованном отчёте я не исправляю, только отмечаю. В /scenarios/15 и /scenarios/16 поле works исправлено на «yes» по Апелляциям 18 и 19, но поле evidence там всё ещё «Не запускал».

Ссылки: `vm:make scenario P=plan_east_strip`, `vm:curl -s -u ditto:$DITTO_PASSWORD localhost:8080/api/2/things/kz.bozshakol:control/features`, `vm:curl -s -u ditto:$DITTO_PASSWORD localhost:8080/api/2/things/kz.bozshakol:whatif/features`, `vm:make scenario-reset`, `bozshakol/ui/presets.json:149`, `fresh:/scenarios/17`, `original:/scenarios/17`, `appeal:evidence[0]`, `appeal:evidence[2]`.

Исправлено: `/scenarios/17/works`: `"no"` → `"yes"`.

Балл Отборочного этапа: 84.17 → 84.17, место 5 → 5.

Оценки Судей (итог Судьи — больший из прежнего и нового: выигранная Апелляция не может понизить балл, Положение 12.3): gpt-6.1-sol: 80 → 80; gpt-6-astra: 82.5 → 82.5; opus-5.5: 90 → 90.

Перепроверка: свежий прогон — `fresh/build_report.json`, журналы — `agents/`; до и после — `before/`, `after/`.

