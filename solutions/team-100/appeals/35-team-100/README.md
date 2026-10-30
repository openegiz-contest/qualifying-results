# Апелляция 35-team-100 — team-100

Подана: 2026-10-29T20:15:35+00:00. Решение: 2026-10-30T04:28:02+00:00. Статус: **удовлетворена**.

Оспорено: `build_report` `/scenarios/7/works` = `"partly"`.

Что утверждает Команда:

> The exact statement in the report that is wrong / Точное утверждение в отчёте, которое неверно
> /scenarios/7/works = "partly" (элемент /scenarios/7, "name": "Беда безопасности «Пьезометр дамбы» (safety=1)").
> /scenarios/7/evidence целиком: "Запускал вместе с fork (safety=1, site.scenario = fork+safety). В прогоне s42-scen-0008 создана вещь issue-2 kind=dam_alarm. К моему снимку в 10:05 она уже была RESOLVED, piezo-1..3 alarm 0, ~116 кПа при уставке 150. Что она стояла первой в очереди, сам не видел. После POST /api/cancel scenario пуст, бед нет."
> 
> What is actually true / Что верно на самом деле
> Верное значение /scenarios/7/works — "yes": оба последствия, заявленные в SUBMISSION.md:161, видны в данных двойников — около 08:10 модели (≈1–2 мин после запуска при ×60) у piezo-1 и piezo-2 kpa выше sp_kpa 150 и alarm = 1, water.state = ALARM, и появляется беда issue-N kind=dam_alarm, safety_class S0, ответственный «Технолог хвостов и оборотной воды» (вещь issue-2 kind=dam_alarm Сборщик видел сам). К его снимку 10:05 беда была уже закрыта, потому что при auto=1 модуль в такте её появления сам вызвал технолога, а симулятор снимает тревогу после его прибытия и проверки дамбы — это штатная работа сценария, а не отсутствие последствий.

Доказательства: command (`appeal.json`, evidence[0]); command (`appeal.json`, evidence[1]); log (`appeal.json`, evidence[2]); log (`appeal.json`, evidence[3]); log (`appeal.json`, evidence[4]); file (`appeal.json`, evidence[5]); file (`appeal.json`, evidence[6]); file (`appeal.json`, evidence[7]).

## Решение

На стенде свежего прогона я выполнил команду Команды из evidence[0]. Это тот же POST /api/scenario, что делал Сборщик (fork, auto=1, safety=1, плюс seed=42 и speed=60). Решение при этом не менялось. Начался прогон s42-scen-0002, site.scenario = fork+safety.

Что видно в данных двойников:
- В 08:15 модели water.state = ALARM.
- С 08:20 у piezo-1 153–154 кПа и alarm=1, у piezo-2 156–158 кПа и alarm=1 при уставке 150. Значения держатся до 09:05.
- В 08:20 появилась беда issue-2 kind=dam_alarm, safety_class S0, ответственный «Технолог хвостов и оборотной воды». Модуль её уже вызвал: status CALLED, rank 99.
- В 09:10 давление вернулось к ≈116/120 кПа, water NORMAL. С 09:15 беда RESOLVED.

Оба последствия, заявленные в SUBMISSION.md:161, проявились: пьезометр выше уставки через ≈10–20 мин модели и беда S0 для технолога хвостов. Сборщик поставил partly, потому что к его снимку в 10:05 тревога уже была снята. Это штатная развязка после автовызова, а не отсутствие последствий. Свежий Сборщик тоже поставил fork+safety works=yes и в 08:15 видел S0 dam_alarm (П-1 155, П-2 160 кПа).

То, что беда стояла в очереди первой, я напрямую не видел. Мой опрос раз в 4 с застал её уже вызванной (rank 99). Слова «впереди всего» есть в тексте модуля, его приводит свежий отчёт в /modules/2. Заявленное поведение подтверждено и без этого.

После проверки я выполнил POST /api/cancel: site.scenario пуст, стенд в свободном ходе. Текста, обращённого к Судьям или к ИИ, в апелляции не нашёл.

Ссылки: `vm:curl -s -X POST http://127.0.0.1:8000/api/scenario -d '{"id":"fork","preset":"fork","kip":1,"auto":1,"safety":1,"seed":42,"speed":60}' + цикл опроса /api/state`, `vm:curl -s -X POST http://127.0.0.1:8000/api/cancel`, `fresh:/scenarios/0`, `fresh:/modules/2`, `original:/scenarios/7/evidence`, `appeal:evidence[0]`, `SUBMISSION.md:161`.

Исправлено: `/scenarios/7/works`: `"partly"` → `"yes"`.

Балл Отборочного этапа: 89.17 → 89.17, место 3 → 3.

Оценки Судей (итог Судьи — больший из прежнего и нового: выигранная Апелляция не может понизить балл, Положение 12.3): gpt-6.1-sol: 88.75 → 88.75; gpt-6-astra: 88.75 → 88.75; opus-5.5: 90 → 90.

Перепроверка: свежий прогон — `fresh/build_report.json`, журналы — `agents/`; до и после — `before/`, `after/`.

