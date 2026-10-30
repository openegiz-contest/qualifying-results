# Апелляция 19-team-082 — team-082

Подана: 2026-10-29T17:08:10+00:00. Решение: 2026-10-30T03:45:54+00:00. Статус: **удовлетворена**.

Оспорено: `build_report` `/scenarios/16/works` = `"no"`.

Что утверждает Команда:

> Точное утверждение в отчёте, которое неверно:
> "works": "no" — «Не запускал: не хватило лимита времени. Стенд не менял.»
> 
> Что верно на самом деле:
> Сценарий работает: он задаёт 45 % руды с Восточного карьера и 7 CAT 785C на нём; прогноз в kz.bozshakol:whatif показывает, что Восточный выбирает вскрытые запасы раньше чем за полгода: scen_exposed6_east_mo = 0, недобор руды за 6 мес (scen_ore_short_6m_kt) около 1,9 Мт, медь за 6 мес ниже базы примерно на 10 %. Отменяется make scenario-reset. Сборщик сценарий не запускал.

Доказательства: command (`appeal.json`, evidence[0]); command (`appeal.json`, evidence[1]); command (`appeal.json`, evidence[2]); command (`appeal.json`, evidence[3]); file (`appeal.json`, evidence[4]); file (`appeal.json`, evidence[5]).

## Решение

Сборщик этот сценарий не запускал: и в исходном отчёте («не хватило лимита времени»), и в свежем («не наблюдал») он помечен как непроверенный. Поэтому `"works": "no"` записан без наблюдения. Я проверил сценарий сам на стенде свежего прогона. Начальное состояние было базовым: preset baseline, east_ore_share 0.3, trucks_east 5, scen_ore_short_6m_kt 0. Запустил `make scenario P=plan_east_push`. Через 50 с в control стало preset plan_east_push, east_ore_share 0.45, trucks_east 7. В whatif стало: scenario «plan_east_push: east_ore_share=0.45, trucks_east=7», status «готов», scen_exposed6_east_mo 0.0 (база 0.4, −100 %), scen_exposed6_central_mo 5.49 (база 3.61), scen_ore_short_6m_kt 1858.94, delta_cu_6m_kt −9.7 %. Это совпадает с описанием в presets.json и в SUBMISSION.md. После `make scenario-reset` стенд вернулся в базу: preset baseline, east_ore_share 0.3, trucks_east 5, в whatif «базовый режим», ore_short 0, delta_cu_6m 0. Сценарий работает по README без изменений кода и окружения, значит верное значение — "yes". Попутно: у plan_east_strip и fleet_optimum отметка «no» тоже поставлена без запуска, но их я не проверял и не исправляю. Текстов, обращённых к судьям, в материалах нет.

Ссылки: `original:/scenarios/16`, `fresh:/scenarios/16`, `vm:make scenario P=plan_east_push; sleep 50; curl -s -u ditto:$DITTO_PASSWORD localhost:8080/api/2/things/kz.bozshakol:control/features; curl -s -u ditto:$DITTO_PASSWORD localhost:8080/api/2/things/kz.bozshakol:whatif/features`, `vm:make scenario-reset; sleep 40; curl whatif/control features`, `bozshakol/ui/presets.json:140`, `SUBMISSION.md:135`, `appeal:evidence[0]`, `appeal:evidence[2]`.

Исправлено: `/scenarios/16/works`: `"no"` → `"yes"`.

Балл Отборочного этапа: 84.17 → 84.17, место 5 → 5.

Оценки Судей (итог Судьи — больший из прежнего и нового: выигранная Апелляция не может понизить балл, Положение 12.3): gpt-6.1-sol: 80 → 80; gpt-6-astra: 82.5 → 82.5; opus-5.5: 90 → 90.

Перепроверка: свежий прогон — `fresh/build_report.json`, журналы — `agents/`; до и после — `before/`, `after/`.

