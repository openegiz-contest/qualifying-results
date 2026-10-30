# Апелляция 23-team-082 — team-082

Подана: 2026-10-29T17:09:26+00:00. Решение: 2026-10-30T04:08:25+00:00. Статус: **удовлетворена**.

Оспорено: `build_report` `/scenarios/5/works` = `"no"`.

Что утверждает Команда:

> Точное утверждение в отчёте, которое неверно:
> "works": "no" — «Не запускал: не хватило лимита времени. Стенд не менял.»
> 
> Что верно на самом деле:
> Сценарий работает: диспетчер переходит с оптимизации на закрепление самосвалов за экскаваторами (kz.bozshakol:haulage dispatch_policy «fixed» вместо «blend»), у экскаваторов меняется состав закреплённых самосвалов (link_trucks), прогноз «что если» пересчитывается: Cu в питании и расход ДТ выше базы, медь за 6 мес ниже. Сборщик сценарий не запускал.

Доказательства: command (`appeal.json`, evidence[0]); command (`appeal.json`, evidence[1]); command (`appeal.json`, evidence[2]); command (`appeal.json`, evidence[3]); file (`appeal.json`, evidence[4]); file (`appeal.json`, evidence[5]).

## Решение

В исходном отчёте стоит works «no», но в evidence сказано, что сценарий не запускали. Значит, это не результат проверки. На стенде свежего прогона я выполнил `make scenario P=dispatch_fixed`. До запуска были base: dispatch_policy blend, preset baseline, whatif delta 0. Через 30 с haulage.dispatch_policy стал «fixed». У sh-01 в link_trucks закреплены 13 самосвалов, у sh-02 — ht-07; это соответствует ветке policy == "fixed" в `_dispatch` (bozshakol/sim/model.py:1324). Через 60 с прогноз whatif был готов («dispatch_fixed: dispatch_policy=fixed»): delta_feed_grade +8.8, delta_diesel_l +11.5, delta_cu_t +8.3, delta_inband_pct −87.5, delta_cu_6m_kt −3.5. Это совпадает с описанием пресета (bozshakol/ui/presets.json:24): за 48 ч меди больше, но питание выходит из коридора качества и падает медь за 6 мес. Смену состава link_trucks во времени отдельно не сравнивал: снимок до запуска есть только для sh-02. После `make scenario-reset` стенд вернулся в базу: blend, preset baseline. В свежем отчёте (fresh:/scenarios/2) стоит «partly» только потому, что прогноз не успел за 45 с; при более долгом ожидании он готов. Обращений к ИИ в материалах апелляции нет. Попутно замечу: в исходном отчёте у других непроверенных сценариев (speed_limit, pf_* и др.) тоже стоит «no» при «Не запускал»; здесь это не исправляю.

Ссылки: `original:/scenarios/5`, `fresh:/scenarios/2`, `vm:make scenario P=dispatch_fixed; sleep 30; curl .../things/kz.bozshakol:haulage/features/dispatch_policy`, `vm:curl .../things/kz.bozshakol:whatif/features`, `vm:make scenario-reset`, `bozshakol/ui/presets.json:24`, `bozshakol/sim/model.py:1324`, `appeal:evidence[0]`, `appeal:evidence[1]`, `appeal:evidence[2]`.

Исправлено: `/scenarios/5/works`: `"no"` → `"yes"`.

Балл Отборочного этапа: 84.17 → 84.17, место 5 → 5.

Оценки Судей (итог Судьи — больший из прежнего и нового: выигранная Апелляция не может понизить балл, Положение 12.3): gpt-6.1-sol: 80 → 80; gpt-6-astra: 82.5 → 82.5; opus-5.5: 90 → 90.

Перепроверка: свежий прогон — `fresh/build_report.json`, журналы — `agents/`; до и после — `before/`, `after/`.

