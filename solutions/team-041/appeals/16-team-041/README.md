# Апелляция 16-team-041 — team-041

Подана: 2026-10-29T10:04:18+00:00. Решение: 2026-10-29T22:29:54+00:00. Статус: **удовлетворена**.

Оспорено: `build_report` `/modules/2/works` = `"partly"`.

Что утверждает Команда:

> The exact statement in the report that is wrong / Точное утверждение в отчёте, которое неверно
> "name": "Модуль управления фабрикой (module-plant)", "works": "partly",
> "evidence": "module-plant online; mill.setpoint_source=plant-control, feed_setpoint_tph=3557; last_decision «Уставка питания 3557 т/ч: склад заполнен на 59 %… пик начинается при складе от 65 %». В логе sim set-feed-rate → mill {'tph': 3557.0}. Пик до 3900 т/ч не наблюдался (склад < 65 % за время проверки) — это заявленное поведение, увидеть его не удалось."
> 
> What is actually true / Что верно на самом деле
> Модуль работает так, как заявлено в SUBMISSION.md:123: при складе дроблёной руды ниже 65 % он держит устойчивый потолок 3 557 т/ч, пик до 3 900 т/ч начинается только со склада от 65 %. Отчёт сборки сам фиксирует склад 59 % и уставку 3 557 т/ч, то есть ровно заявленное поведение («это заявленное поведение»); пик при таком складе и не должен был начаться.

Доказательства: file (`appeal.json`, evidence[0]); file (`appeal.json`, evidence[1]); file (`appeal.json`, evidence[2]); file (`appeal.json`, evidence[3]); file (`appeal.json`, evidence[4]).

## Решение

Я проверил стенд свежего прогона на коммите 56f1f69 через шлюз :8088. Двойник mill: feed_setpoint_tph=3557, setpoint_source=plant-control, peak_min_shift=0, max_feed_tph=4079. Склад stockpile заполнен на 60 % (25616 т). Модуль module-plant: enabled=true, status=online, last_decision «Уставка питания 3557 т/ч: склад заполнен на 59 %, уставка на устойчивом потолке модуля (пик начинается при складе от 65 %)…». Именно это правило записано в SUBMISSION.md (строка module-plant): пик до 3900 т/ч только при складе от 65 %, иначе устойчивый потолок 3557 т/ч. В коде mine/modules/plant/core.py пик включается только при level_pct не ниже порога peak_from_pct, а в params.yaml peak_from_pct=65 и peak_hold_pct=55. Свежий Сборщик увидел то же самое и поставил works="yes". Исходный Сборщик тоже сам назвал увиденное заявленным поведением. Он поставил "partly" только потому, что пик не наступил, но при складе ниже 65 % пика и не должно быть. Ни одного отклонения от заявленного не нашлось ни в одном прогоне. Поэтому утверждение "partly" неверно, верное значение — "yes". Ветку с пиком (склад от 65 %) не видел ни один прогон, и я её тоже не наблюдал. Текстов, обращённых к судье, в апелляции и в данных нет.

Ссылки: `fresh:/modules/2`, `original:/modules/2/evidence`, `vm:curl -s localhost:8088/ditto/api/2/things/kz.bozshakol:mill`, `vm:curl -s localhost:8088/ditto/api/2/things/kz.bozshakol:module-plant`, `vm:curl -s localhost:8088/ditto/api/2/things/kz.bozshakol:stockpile`, `mine/modules/plant/core.py:148`, `mine/model/params.yaml:743`, `appeal:evidence[0]`.

Исправлено: `/modules/2/works`: `"partly"` → `"yes"`.

Балл Отборочного этапа: 89.58 → 89.58, место 2 → 2.

Оценки Судей (итог Судьи — больший из прежнего и нового: выигранная Апелляция не может понизить балл, Положение 12.3): gpt-6.1-sol: 87.5 → пересмотр 85 → итог 87.5; gpt-6-astra: 87.5 → пересмотр 75 → итог 87.5; opus-5.5: 93.75 → пересмотр 90 → итог 93.75.

Перепроверка: свежий прогон — `fresh/build_report.json`, журналы — `agents/`; до и после — `before/`, `after/`, новые оценки Судей — `rescored/`.

