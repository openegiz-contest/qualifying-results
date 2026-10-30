# Апелляция 28-team-082 — team-082

Подана: 2026-10-29T17:17:58+00:00. Решение: 2026-10-30T04:36:46+00:00. Статус: **удовлетворена**.

Оспорено: `build_report` `/scenarios/11/works` = `"no"`.

Что утверждает Команда:

> Точное утверждение в отчёте, которое неверно:
> "works": "no" — «Не запускал: не хватило лимита времени. Стенд не менял.»
> 
> Что верно на самом деле:
> Сценарий работает: цель шихтовки 0,45 % Cu: диспетчер отправляет больше рейсов на SH-02 (богатая руда), прогноз в whatif: Cu в питании около +6 %, медь за 48 ч около +5,8 %. Отменяется make scenario-reset. Сборщик сценарий не запускал, поэтому «no» — не результат проверки.

Доказательства: command (`appeal.json`, evidence[0]); command (`appeal.json`, evidence[1]); command (`appeal.json`, evidence[2]); command (`appeal.json`, evidence[3]); file (`appeal.json`, evidence[4]); file (`appeal.json`, evidence[5]).

## Решение

Исходный Сборщик сценарий high_grade не запускал («не хватило лимита времени»). Значит, works="no" — это не результат проверки. На стенде свежего прогона я выполнил `make scenario P=high_grade`, как предлагает Команда, и опрашивал двойник whatif каждые 15 с. В двойнике control grade_target стал 0.45, gc-01 был в состоянии running. Первые ~30 с whatif показывал статус «расчёт» и нулевые дельты. Потом статус сменился на «готов», сценарий «high_grade: grade_target=0.45», calc_s 20.9. Результат прогноза: base_feed_grade 0.43 → scen_feed_grade 0.45 (delta_feed_grade +6.0 %), медь 569.05 → 604.84 т (delta_cu_t +6.3 %), delta_margin +5.8, delta_queue_min −27, delta_ore_east_pct −8.8. Это сходится с описанием в presets.json:96 (больше руды с SH-02) и в строке high_grade раздела SUBMISSION.md. После `make scenario-reset` grade_target снова 0.42, preset baseline. Сценарий меняет управление и даёт ожидаемый прогноз, отмена тоже работает. В свежем отчёте стоит "partly" только потому, что за время наблюдения прогноз не успел посчитаться; при ожидании ~45 с он готов. Отдельно я не проверял, что диспетчер в живой модели фактически шлёт больше рейсов на SH-02. Но эффект виден по прогнозу (дельты по Восточному и по очередям), поэтому оцениваю как "yes". Текстов, обращённых к судьям или ИИ, в апелляции нет.

Ссылки: `original:/scenarios/11`, `fresh:/scenarios/11`, `vm:make scenario P=high_grade; curl -s -u ditto:$DITTO_PASSWORD localhost:8080/api/2/things/kz.bozshakol:whatif/features`, `vm:curl -s -u ditto:$DITTO_PASSWORD localhost:8080/api/2/things/kz.bozshakol:control/features/grade_target`, `vm:make scenario-reset`, `bozshakol/ui/presets.json:96`, `SUBMISSION.md:130`, `appeal:evidence[0]`, `appeal:evidence[2]`.

Исправлено: `/scenarios/11/works`: `"no"` → `"yes"`.

Балл Отборочного этапа: 84.17 → 84.17, место 5 → 5.

Оценки Судей (итог Судьи — больший из прежнего и нового: выигранная Апелляция не может понизить балл, Положение 12.3): gpt-6.1-sol: 80 → 80; gpt-6-astra: 82.5 → 82.5; opus-5.5: 90 → 90.

Перепроверка: свежий прогон — `fresh/build_report.json`, журналы — `agents/`; до и после — `before/`, `after/`.

