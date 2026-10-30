# Апелляция 15-team-041 — team-041

Подана: 2026-10-29T10:04:16+00:00. Решение: 2026-10-29T21:05:46+00:00. Статус: **удовлетворена**.

Оспорено: `build_report` `/scenarios/7/works` = `"no"`.

Что утверждает Команда:

> The exact statement in the report that is wrong / Точное утверждение в отчёте, которое неверно
> "name": "Замена футеровки МПСИ (scenario-sag-reline)", "works": "no", "undone": "yes",
> "evidence": "activate {params:{cause:full,start:next-shift}} через шлюз страницы (тело как activateBody в control.js) — HTTP 202 (в логе nginx mine-ui), но за 2 мин status=inactive, mill-sag.reline_state пуст; в логе mine-sim сообщение не появилось. Повторил тот же запрос один раз — результат тот же. В журнале соединения Ditto mosquitto-target-connection есть записи «Message is dropped as a result of backpressure strategy!» — вероятная причина потери. Стенд не изменился, сценарий не включён."
> 
> What is actually true / Что верно на самом деле
> Сценарий работает. Отчёт сборки сам показывает, что запрос не дошёл до симулятора («в логе mine-sim сообщение не появилось»): Ditto отбросило сообщение в соединении Ditto → MQTT. Это потеря доставки на Стенде в тот момент, а не отказ Сценария. На том же Стенде Судья opus-5.5 запустил этот Сценарий через интерфейс, и он включился (`mill-sag reline_state=planned`). На чистой VM тот же запрос Сборщика доходит и включает Сценарий.

Доказательства: file (`appeal.json`, evidence[0]); file (`appeal.json`, evidence[1]); command (`appeal.json`, evidence[2]); log (`appeal.json`, evidence[3]); command (`appeal.json`, evidence[4]); log (`appeal.json`, evidence[5]); file (`appeal.json`, evidence[6]); file (`appeal.json`, evidence[7]); file (`appeal.json`, evidence[8]).

## Решение

В исходном прогоне сообщение activate до mine-sim не дошло: HTTP 202 был, но в логе симулятора записи нет, а в журнале соединения Ditto есть отбрасывания из-за backpressure. То есть Сценарий этой попыткой вообще не проверялся. Свежий прогон на том же коммите получил для scenario-sag-reline works=yes: сценарий стал active, phase=planned, у mill-sag reline_state=planned (26.10 20:00 → 29.10 20:00), после cancel всё вернулось. Я сам проверил лог симулятора на этом Стенде, и это подтвердилось: в 20:51:34 есть «live message activate -> scenario-sag-reline {'params': {'cause': 'full', 'start': 'next-shift'}}», в 21:02:18 — cancel. Итак, «no» в исходном отчёте вызвано случайной потерей доставки в Ditto (свежий отчёт описывает такие потери и для других сценариев), а не отказом Сценария. Оговорка: свежий прогон проверил только фазу плана, сама остановка мельницы не наступила. Логи с машины Команды (evidence[3], [5]) я фактами не считал. Другие замечания я не исправляю: в свежем прогоне crusher-stop и heavy-rain не запустились по той же причине, что и здесь. Инструкций, обращённых к Судье, в Апелляции нет.

Ссылки: `fresh:/scenarios/7`, `original:/scenarios/7/evidence`, `vm:docker logs openegiz-mine-sim-1 2>&1 | grep -n "scenario-sag-reline"`, `fresh:/built_on_openegiz/evidence`, `appeal:evidence[1]`.

Исправлено: `/scenarios/7/works`: `"no"` → `"yes"`.

Балл Отборочного этапа: 89.58 → 89.58, место 2 → 2.

Оценки Судей (итог Судьи — больший из прежнего и нового: выигранная Апелляция не может понизить балл, Положение 12.3): gpt-6.1-sol: 87.5 → 87.5; gpt-6-astra: 87.5 → 87.5; opus-5.5: 93.75 → 93.75.

Перепроверка: свежий прогон — `fresh/build_report.json`, журналы — `agents/`; до и после — `before/`, `after/`.

