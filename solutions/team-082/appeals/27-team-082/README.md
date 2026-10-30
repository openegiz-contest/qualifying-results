# Апелляция 27-team-082 — team-082

Подана: 2026-10-29T17:17:35+00:00. Решение: 2026-10-30T04:30:38+00:00. Статус: **удовлетворена**.

Оспорено: `build_report` `/scenarios/10/works` = `"no"`.

Что утверждает Команда:

> Точное утверждение в отчёте, которое неверно:
> "works": "no" — «Не запускал: не хватило лимита времени. Стенд не менял.»
> 
> Что верно на самом деле:
> Сценарий работает: удельный расход ВВ 0,45 кг/м³: крупнее кусок x80, установившийся потенциал МПСИ около −7 %, экономия ВВ; прогноз в whatif пересчитывается (delta_waste_t около −5 %). Отменяется make scenario-reset. Сборщик сценарий не запускал, поэтому «no» — не результат проверки.

Доказательства: command (`appeal.json`, evidence[0]); command (`appeal.json`, evidence[1]); command (`appeal.json`, evidence[2]); command (`appeal.json`, evidence[3]); file (`appeal.json`, evidence[4]); file (`appeal.json`, evidence[5]).

## Решение

В исходном отчёте у pf_down стоит «no», но в evidence сказано: «Не запускал: не хватило лимита времени». Значит, «no» — не результат проверки. Я проверил сценарий сам на стенде свежего прогона. До запуска: control.powder_factor 0.62, preset baseline; у drill-blast m2m_x80_cm 70.4 и m2m_sag_tph 3110; whatif в «базовом режиме», delta 0. Запустил `make scenario P=pf_down`. Через 30 с powder_factor 0.45. У drill-blast: x80 90.9 см (кусок крупнее), sag_tph 2902, скважин на 100 кт 49.1 вместо 67.6, затраты на ВВ 87.3 вместо 120.3 ₸/т (экономия ВВ и бурения). Whatif пересчитан, статус «готов», scenario «pf_down: powder_factor=0.45», delta_cu_t −0.3 %, delta_waste_t −4.6 %. Через 60 с значения те же. Так и обещают presets.json:88 и строка в SUBMISSION.md. Потом выполнил `make scenario-reset`: preset baseline, powder_factor 0.62, x80 70.4, sag_tph 3110, whatif снова «базовый режим», delta_waste_t 0. Стенд остался в исходном состоянии. Свежий отчёт поставил «partly», потому что «прогноз не готов, прямых эффектов нет». Но он, похоже, смотрел не те признаки или не дождался: эффекты есть в признаках m2m_* двойника drill-blast, а прогноз готов в пределах 30 с. Сценарий делает всё, что заявлено, поэтому верное значение — «yes». Текста, обращённого к Судье, в Апелляции нет.

Ссылки: `original:/scenarios/10`, `fresh:/scenarios/10`, `appeal:evidence[0]`, `appeal:evidence[1]`, `appeal:evidence[2]`, `appeal:evidence[3]`, `bozshakol/ui/presets.json:88`, `vm:make scenario P=pf_down; curl -u ditto:$P localhost:8080/api/2/things/kz.bozshakol:{control,drill-blast,whatif}/features`, `vm:make scenario-reset; curl ... kz.bozshakol:{control,drill-blast,whatif}/features`.

Исправлено: `/scenarios/10/works`: `"no"` → `"yes"`.

Балл Отборочного этапа: 84.17 → 84.17, место 5 → 5.

Оценки Судей (итог Судьи — больший из прежнего и нового: выигранная Апелляция не может понизить балл, Положение 12.3): gpt-6.1-sol: 80 → 80; gpt-6-astra: 82.5 → 82.5; opus-5.5: 90 → 90.

Перепроверка: свежий прогон — `fresh/build_report.json`, журналы — `agents/`; до и после — `before/`, `after/`.

