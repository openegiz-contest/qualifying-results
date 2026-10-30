# Апелляция 26-team-082 — team-082

Подана: 2026-10-29T17:16:56+00:00. Решение: 2026-10-30T04:24:04+00:00. Статус: **удовлетворена**.

Оспорено: `build_report` `/scenarios/9/works` = `"no"`.

Что утверждает Команда:

> Точное утверждение в отчёте, которое неверно:
> "works": "no" — «Не запускал: не хватило лимита времени. Стенд не менял.»
> 
> Что верно на самом деле:
> Сценарий работает: удельный расход ВВ 0,85 кг/м³: двойник drill-blast пересчитывает сетку скважин и кусок x80 (Kuz-Ram), установившийся потенциал МПСИ около +7 %; прогноз в whatif пересчитывается. Отменяется make scenario-reset. Сборщик сценарий не запускал, поэтому «no» — не результат проверки.

Доказательства: command (`appeal.json`, evidence[0]); command (`appeal.json`, evidence[1]); command (`appeal.json`, evidence[2]); command (`appeal.json`, evidence[3]); file (`appeal.json`, evidence[4]); file (`appeal.json`, evidence[5]).

## Решение

В исходном отчёте стоит «no», но Сборщик сценарий не запускал («не хватило лимита времени»), так что это не результат проверки. В свежем прогоне pf_up запущен: powder_factor 0.62→0.85, прогноз Cu +0,1 %, после reset снова 0.62. Там стоит «partly» с пометкой «прямых изменений за 35 с нет», но двойник drill-blast Сборщик не смотрел. Я проверил сам на работающем Стенде. До запуска стенд был в базовом режиме: preset baseline, pf 0.62, whatif delta 0. Двойник drill-blast до запуска: pattern 5.7×6.5 м, m2m_x80_cm 70.4, m2m_sag_tph 3110, m2m_holes_per_100kt 67.6. Затем выполнил make scenario P=pf_up и через 60 с прочитал двойники. control.powder_factor 0.85. drill-blast: design_pf 0.85, pattern 4.8×5.6 м, x80 54.7 см, dig_rate 106.7 %, sag_tph 3330 (+7,1 %, как в SUBMISSION), holes 92.7, ВВ 164.9 ₸/т. whatif: status «готов», scenario «pf_up: powder_factor=0.85», delta_cu_t +0.1, delta_cost +2.9 %. Потом выполнил make scenario-reset: preset baseline, pf 0.62, pattern 5.7×6.5, x80 70.4, sag 3110, то есть всё вернулось. Сценарий делает то, что заявлено в SUBMISSION.md и presets.json, поэтому верное значение — «yes». Текста, обращённого к Судье, в Апелляции нет.

Ссылки: `original:/scenarios/9`, `fresh:/scenarios/9`, `vm:make scenario P=pf_up; sleep 60; curl -s -u ditto:$P localhost:8080/api/2/things/kz.bozshakol:drill-blast/features`, `vm:curl -s -u ditto:$P localhost:8080/api/2/things/kz.bozshakol:whatif/features`, `vm:make scenario-reset; curl -s -u ditto:$P localhost:8080/api/2/things/kz.bozshakol:control/features`, `bozshakol/ui/presets.json:80`, `SUBMISSION.md:128`, `appeal:evidence[0]`, `appeal:evidence[2]`.

Исправлено: `/scenarios/9/works`: `"no"` → `"yes"`.

Балл Отборочного этапа: 84.17 → 84.17, место 5 → 5.

Оценки Судей (итог Судьи — больший из прежнего и нового: выигранная Апелляция не может понизить балл, Положение 12.3): gpt-6.1-sol: 80 → 80; gpt-6-astra: 82.5 → 82.5; opus-5.5: 90 → 90.

Перепроверка: свежий прогон — `fresh/build_report.json`, журналы — `agents/`; до и после — `before/`, `after/`.

