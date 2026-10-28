# Qualifying Round results / Результаты Отборочного этапа / Іріктеу кезеңінің нәтижелері

## English

### Contents

These are the Qualifying Round reports (Rules, clause 12.1).

- [`results.md`](results.md): the ranking with the total of every Judge.
- `solutions/team-NNN/`: the Build Report with logs, the detector's finding, each Judge's Scores and reasoning per criterion, screenshots.

### AI Jury of the Qualifying Round

Judges: Opus 5.5, GPT 6.1 sol, GPT 6 astra.

Pipeline commit: `3d6a1293aa79e0dc9c88cf1c9b28ec8794e0fe8c`. SHA-256: `bde3b76abb4f2692513b23bb9d882b6a569989041ad8eaf1fc1bd91cdafe7076` (announced in https://github.com/openegiz-contest/openegiz-contest.github.io/discussions/3). The pipeline code and the Judges' prompts: https://github.com/openegiz-contest/judge-pipeline.

The Qualifying run started on 27 October 2026 at 14:36 (Astana) with a pipeline version that differs from the published one only in that Sonnet 5.5 was also a Qualifying Judge and in the old score-counting rule; the prompts, the Rubric, the models and the Builder were the same. The results are computed by the published version: the Scores of Sonnet 5.5 are published in the Solution folders and are not counted.

### Stands re-run by the Organizer

The Stand failed through no fault of the Team. Before publication the Organizer repeated the run on a new VM; the earlier Scores and Build Report, where named below, are void, and the new result counts.

- team-035: the platform container telegraf was stopped for lack of memory and restarted. The Scores of all three Judges obtained on that Stand are void; the Organizer repeated the runs on a new VM. There the same container kept restarting; after two restores the Submission was evaluated on the Stand as is, marked "Stand degraded" in the Build Report. The Team may file an Appeal.
- team-037: the platform containers (mongodb, things) were restarted, the Stand degraded. The Score of the Judge opus-5.5 obtained on that Stand is void; the Organizer repeated its run on a new VM. There the platform service things kept restarting for lack of memory; after two restores the Judge opus-5.5 evaluated the Submission on the Stand as is, marked "Stand degraded" in the Build Report. The Scores of the Judges gpt-6.1-sol and gpt-6-astra were obtained on a working Stand and are kept. The Team may file an Appeal.
- team-051: the build was interrupted by a broken download from GitHub, the Stand did not start. The Submission was built again; the Build Report and the Scores of all three Judges were obtained again.
- team-060: the build was interrupted by a broken download from GitHub, the Stand did not start. The Submission was built again; the Build Report and the Scores of all three Judges were obtained again.

### Empty Team Repositories

A Team Repository identical to a Template version is listed with 0: no work.

### Appeals

The Appeals window is 48 hours from 2026-10-28 09:38 (Astana). The procedure is in [`APPEALS.md`](APPEALS.md). The form: https://github.com/openegiz-contest/qualifying-results/issues/new?template=appeal.yml.

## Русский

### Содержание

Здесь опубликованы отчёты Отборочного этапа (п. 12.1 Положения).

- [`results.md`](results.md): рейтинг с итогом каждого Судьи.
- `solutions/team-NNN/`: Отчёт сборки с логами, заключение детектора, Баллы и рассуждения каждого Судьи по критериям, скриншоты.

### ИИ-жюри Отборочного этапа

Судьи: Opus 5.5, GPT 6.1 sol, GPT 6 astra.

Коммит конвейера: `3d6a1293aa79e0dc9c88cf1c9b28ec8794e0fe8c`. SHA-256: `bde3b76abb4f2692513b23bb9d882b6a569989041ad8eaf1fc1bd91cdafe7076` (объявлены в https://github.com/openegiz-contest/openegiz-contest.github.io/discussions/3). Код конвейера и промпты Судей: https://github.com/openegiz-contest/judge-pipeline.

Прогон Отборочного этапа начат 27 октября 2026 г. в 14:36 (Астана) версией конвейера, которая отличается от опубликованной только тем, что Sonnet 5.5 был также Судьёй Отборочного этапа, и прежним правилом подсчёта баллов; промпты, Рубрика, модели и Сборщик те же. Итоги посчитаны опубликованной версией: Баллы Sonnet 5.5 опубликованы в папках Решений и не учитываются.

### Стенды, перезапущенные Организатором

Стенд сломался не по вине Команды. Организатор до публикации повторил прогон на новой VM; прежние оценки и Отчёт сборки, если они названы ниже, недействительны, в итог идёт новый результат.

- team-035: контейнер платформы telegraf остановлен по нехватке памяти и перезапускался. Оценки всех трёх Судей, полученные на этом Стенде, аннулированы; Организатор повторил прогоны на новой VM. Там тот же контейнер снова перезапускался; после двух восстановлений Решение оценено на Стенде как есть, с пометкой «Стенд деградировал» в Отчёте сборки. Команда может подать Апелляцию.
- team-037: контейнеры платформы (mongodb, things) перезапускались, Стенд деградировал. Оценка Судьи opus-5.5, полученная на этом Стенде, аннулирована; Организатор повторил его прогон на новой VM. Там сервис платформы things снова перезапускался по нехватке памяти; после двух восстановлений Судья opus-5.5 оценил Решение на Стенде как есть, с пометкой «Стенд деградировал» в Отчёте сборки. Оценки Судей gpt-6.1-sol и gpt-6-astra получены на исправном Стенде и сохранены. Команда может подать Апелляцию.
- team-051: сборка прервалась из-за обрыва загрузки с GitHub, Стенд не поднялся. Решение собрано заново; Отчёт сборки и оценки всех трёх Судей получены заново.
- team-060: сборка прервалась из-за обрыва загрузки с GitHub, Стенд не поднялся. Решение собрано заново; Отчёт сборки и оценки всех трёх Судей получены заново.

### Пустые Репозитории команд

Репозиторий команды, совпадающий с версией Шаблона, указан с 0: работы нет.

### Апелляции

Срок подачи Апелляций — 48 часов с 2026-10-28 09:38 (Астана). Порядок подачи — в [`APPEALS.md`](APPEALS.md). Форма: https://github.com/openegiz-contest/qualifying-results/issues/new?template=appeal.yml.

## Қазақша

### Мазмұны

Мұнда Іріктеу кезеңінің есептері жарияланған (Ереженің 12.1-тармағы).

- [`results.md`](results.md): әр Төрешінің қорытындысы бар рейтинг.
- `solutions/team-NNN/`: журналдары бар Жинақ есебі, детектордың қорытындысы, әр Төрешінің критерийлер бойынша балдары мен негіздемелері, скриншоттар.

### Іріктеу кезеңінің ЖИ қазылар алқасы

Төрешілер: Opus 5.5, GPT 6.1 sol, GPT 6 astra.

Пайплайн коммиті: `3d6a1293aa79e0dc9c88cf1c9b28ec8794e0fe8c`. SHA-256: `bde3b76abb4f2692513b23bb9d882b6a569989041ad8eaf1fc1bd91cdafe7076` (https://github.com/openegiz-contest/openegiz-contest.github.io/discussions/3 бөлімінде хабарланған). Пайплайн коды мен Төрешілердің промпттары: https://github.com/openegiz-contest/judge-pipeline.

Іріктеу кезеңінің іске қосылуы 2026 жылғы 27 қазанда 14:36-да (Астана) басталды. Ол жарияланған нұсқадан тек Sonnet 5.5 де Іріктеу кезеңінің Төрешісі болуымен және балдарды есептеудің бұрынғы ережесімен ерекшеленетін пайплайн нұсқасымен жүргізілді; промпттар, Рубрика, модельдер және Жинаушы бірдей болды. Нәтижелер жарияланған нұсқамен есептелген: Sonnet 5.5 балдары Шешімдер папкаларында жарияланған және ескерілмейді.

### Ұйымдастырушы қайта іске қосқан Стендтер

Стенд Команданың кінәсінен емес бұзылды. Ұйымдастырушы жариялауға дейін жаңа VM-де іске қосуды қайталады; төменде аталған болса, бұрынғы бағалар мен Жинақ есебі жарамсыз, қорытындыға жаңа нәтиже кіреді.

- team-035: платформаның telegraf контейнері жад жетіспегендіктен тоқтатылып, қайта іске қосылды. Осы Стендте алынған үш Төрешінің бағалары жарамсыз; Ұйымдастырушы іске қосуларды жаңа VM-де қайталады. Онда сол контейнер қайтадан қайта іске қосылды; екі қалпына келтіруден кейін Шешім Стендте сол күйінде бағаланды, Жинақ есебінде «Стенд нашарлады» белгісі бар. Команда Апелляция бере алады.
- team-037: платформаның контейнерлері (mongodb, things) қайта іске қосылды, Стенд нашарлады. Осы Стендте алынған Төреші opus-5.5 бағасы жарамсыз; Ұйымдастырушы оның іске қосылуын жаңа VM-де қайталады. Онда платформаның things сервисі жад жетіспегендіктен қайтадан қайта іске қосылды; екі қалпына келтіруден кейін Төреші opus-5.5 Шешімді Стендте сол күйінде бағалады, Жинақ есебінде «Стенд нашарлады» белгісі бар. Төрешілер gpt-6.1-sol және gpt-6-astra бағалары жарамды Стендте алынған және сақталған. Команда Апелляция бере алады.
- team-051: GitHub-тан жүктеу үзілгендіктен жинау тоқтады, Стенд көтерілмеді. Шешім қайта жиналды; Жинақ есебі және үш Төрешінің де бағалары қайта алынды.
- team-060: GitHub-тан жүктеу үзілгендіктен жинау тоқтады, Стенд көтерілмеді. Шешім қайта жиналды; Жинақ есебі және үш Төрешінің де бағалары қайта алынды.

### Бос Команда репозиторийлері

Шаблонның бір нұсқасымен бірдей Команда репозиторийі 0 балмен көрсетіледі: жұмыс жоқ.

### Апелляциялар

Апелляция беру мерзімі — 2026-10-28 09:38 (Астана) сәтінен бастап 48 сағат. Беру тәртібі — [`APPEALS.md`](APPEALS.md) файлында. Форма: https://github.com/openegiz-contest/qualifying-results/issues/new?template=appeal.yml.
