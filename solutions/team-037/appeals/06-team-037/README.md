# Апелляция 06-team-037 — team-037

Подана: 2026-10-28T11:45:20+00:00. Решение: 2026-10-29T20:33:01+00:00. Статус: **удовлетворена**.

Оспорено: `build_report` `/scenarios/8/works` = `"no"`.

Что утверждает Команда:

> Точное утверждение в отчёте, которое неверно (цитата):
> "name": "Сценарии снабжения (fuel_shortage, no_tyres, kpp_closed)", "works": "no", "evidence": "Не запускал из-за времени и ненадёжного канала команд. fuel-depot.supply_cut 0, repair-shop.tyre_cut 0, checkpoint.closed_left 0."
> 
> Что верно на самом деле:
> Сценарии работают. Доказательство в Отчёте прямо говорит, что их не запускали, а перечисленные нулевые значения — это и есть ожидаемое состояние двойников при незапущенном Сценарии, а не признак неработоспособности. Отчёт противоречит сам себе: в /modules/20 те же объекты признаны работающими.

Доказательства: file (`appeal.json`, evidence[0]); file (`appeal.json`, evidence[1]); file (`appeal.json`, evidence[2]); file (`appeal.json`, evidence[3]).

## Решение

В исходном отчёте эти сценарии вообще не запускались. Нулевые supply_cut, tyre_cut и closed_left — это обычное состояние до запуска, а не наблюдаемый отказ. В свежем отчёте Решение не поднялось (came_up=false) из-за сетевого сбоя при git-клоне. Но к моменту проверки Стенд на этой VM работал на коммите 76f36ae: контейнеры запущены, в Ditto 158 двойников.

Я сам запустил сценарии документированным PUT в org.aktogay:control/features/command (способ описан в SUBMISSION.md:153-156): fuel_shortage, no_tyres и kpp_closed, у каждого dur 120. Все три запроса вернули 204. В status появились last_scenario «КПП закрыт на 120 мин» и active_scenarios ['Перебои с топливом', 'Нет шин на складе РМЦ', 'КПП закрыт'].

Последствия видны в обоих вариантах (smart и fixed):
- fuel-depot: supply_cut=6746 с, state=low;
- repair-shop: tyre_cut=6776 с;
- checkpoint: closed_left=6806 с, state=closed.

Затем я отменил сценарии командами fuel_restore, tyres_restore и kpp_open. После этого active_scenarios=[], supply_cut, tyre_cut и closed_left равны 0, checkpoint вернулся в state=auto. fuel-depot остался в state=low, вероятно из-за запаса, израсходованного за время перебоя.

Итог: сценарии запускаются, дают последствия и отменяются, утверждение works="no" неверно. Довод Команды о противоречии с /modules/20 сам по себе ничего не доказывал, вывод основан на моей перепроверке. Инъекций в Апелляции и выводе команд не заметил.

Ссылки: `original:/scenarios/8`, `fresh:/came_up`, `vm:curl -X PUT .../org.aktogay:control/features/command/properties {fuel_shortage|no_tyres|kpp_closed, dur 120} -> 204; status.active_scenarios=['Перебои с топливом','Нет шин на складе РМЦ','КПП закрыт']`, `vm:curl .../org.aktogay.{smart,fixed}:fuel-depot/features/supply_cut -> 6746; repair-shop tyre_cut 6776; checkpoint closed_left 6806 state closed`, `vm:PUT fuel_restore/tyres_restore/kpp_open -> active_scenarios=[], supply_cut/tyre_cut/closed_left 0, checkpoint state auto`, `team/aktogay/app/src/platform/scenarios.ts:72`, `SUBMISSION.md:153`.

Исправлено: `/scenarios/8/works`: `"no"` → `"yes"`.

Балл Отборочного этапа: 73.33 → 73.33, место 11 → 11.

Оценки Судей (итог Судьи — больший из прежнего и нового: выигранная Апелляция не может понизить балл, Положение 12.3): gpt-6.1-sol: 68.75 → 68.75; gpt-6-astra: 68.75 → 68.75; opus-5.5: 82.5 → 82.5.

Перепроверка: свежий прогон — `fresh/build_report.json`, журналы — `agents/`; до и после — `before/`, `after/`.

