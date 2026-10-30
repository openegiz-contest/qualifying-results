# Апелляция 17-team-082 — team-082

Подана: 2026-10-29T17:05:39+00:00. Решение: 2026-10-29T22:20:37+00:00. Статус: **удовлетворена**.

Оспорено: `build_report` `/modules/9/works` = `"partly"`.

Что утверждает Команда:

> Точное утверждение в отчёте, которое неверно:
> "works": "partly" — «Кнопки «Посчитать месяц» и «Подобрать план» в пульте я не запускал (браузера нет), plan_status «нет».»
> 
> Что верно на самом деле:
> Модуль работает полностью: «Подобрать план» на Стенде считает 8 расстановок и записывает рекомендацию в двойник kz.bozshakol:whatif (plan_status «готов», plan_options, plan_best). Это подтвердили Судьи на том же Стенде; «нет» в plan_status означает только, что подбор ещё не запускали.

Доказательства: log (`appeal.json`, evidence[0]); log (`appeal.json`, evidence[1]); log (`appeal.json`, evidence[2]); log (`appeal.json`, evidence[3]); command (`appeal.json`, evidence[4]); command (`appeal.json`, evidence[5]).

## Решение

Проверено на стенде свежего прогона, коммит 2305b48. До проверки у whatif plan_status был «нет», а признаков plan_best, plan_calc_s и plan_computed_at не было вовсе: подбор ещё не запускали. Оба Сборщика пишут, что «Подобрать план» не нажимали, поэтому «partly» — это непроверенная функция, а не обнаруженный сбой. Я нажал эту кнопку штатным CLI Решения: `twinctl set plan_optimize=1`. Это тот же счётчик-команда, что у кнопки (bozshakol/sim/main.py:169-180). Статус стал «подбор», затем примерно через 70 с — «готов»: plan_calc_s 68.3. В plan_options 8 вариантов. Записаны plan_best «Восточный: меньше руды, больше вскрыши» и plan_feasible true. У этого варианта запас через полгода 4.33/2.09 мес против 4.56/0.0 у текущей расстановки. Помесячные KPI (month_ore_kt, exposed6_*, plan_traj) и запасы pit-central/pit-east в whatif есть по обоим отчётам. Кнопка «Посчитать месяц» (bozshakol/ui/index.html:59) только отправляет параметры плана в штатный пересчёт whatif, а он работает. Значит, модуль работает полностью, а «нет» в plan_status означало лишь, что подбор не запускали. Логи и оценки других Судей (evidence[0–3]) я считал подсказкой, а не фактом; вывод сделан по собственному прогону. Побочные наблюдения, их я не исправляю: (1) на стенде остался preset plan_east_push из фоновой очереди свежего прогона, хотя отчёт говорит о reset; команда `twinctl set` перевела его в manual, а значения параметров остались по умолчанию. (2) В материалах обращений к ИИ не было.

Ссылки: `original:/modules/9/evidence`, `fresh:/modules/9`, `vm:python3 bozshakol/tools/twinctl.py set plan_optimize=1`, `vm:curl -s -u ditto:$P localhost:8080/api/2/things/kz.bozshakol:whatif/features/plan_status`, `vm:curl -s -u ditto:$P localhost:8080/api/2/things/kz.bozshakol:whatif/features/plan_options`, `bozshakol/sim/main.py:169`, `bozshakol/ui/index.html:59`, `appeal:evidence[4]`, `appeal:evidence[5]`.

Исправлено: `/modules/9/works`: `"partly"` → `"yes"`.

Балл Отборочного этапа: 84.17 → 84.17, место 5 → 5.

Оценки Судей (итог Судьи — больший из прежнего и нового: выигранная Апелляция не может понизить балл, Положение 12.3): gpt-6.1-sol: 80 → пересмотр 41.25 → итог 80; gpt-6-astra: 82.5 → пересмотр 41.25 → итог 82.5; opus-5.5: 90 → пересмотр 45 → итог 90.

Перепроверка: свежий прогон — `fresh/build_report.json`, журналы — `agents/`; до и после — `before/`, `after/`, новые оценки Судей — `rescored/`.

