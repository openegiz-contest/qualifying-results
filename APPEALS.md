# Appeals procedure

## English

The Qualifying Round reports are published at https://github.com/openegiz-contest/qualifying-results.

### Where and when

An Appeal is filed as an issue in that repository, by the form: https://github.com/openegiz-contest/qualifying-results/issues/new?template=appeal.yml.

The Appeals window is 48 hours: from 2026-10-28 09:38 to 2026-10-30 09:38 (Astana time; Rules, clause 12.1). The time of an Appeal is the time the issue was created. An Appeal filed outside the window is not accepted.

### What may be disputed

Rules, clause 12.2: "An Appeal is accepted only in respect of a factual error in a Build Report or in a finding on an attempt to influence the AI Jury — for example, if the Build Report states that a Module does not start and the Team presents a log confirming that it starts. Disagreement with the points awarded is not grounds for an Appeal."

Disputed may be:

- a fact in the Build Report of your Team: `came_up`, `steps`, `healthchecks`, `modules`, `scenarios`, `concept`, `built_on_openegiz`, `notes`;
- the finding on an attempt to influence the AI Jury: `verdict`, `evidence`.

Not disputed: the points, the Judges' reasoning, the place, the Team, the commit and the times in the report.

### How to file

One issue per disputed fact. The form asks for:

- Team repository (`team-NNN`);
- what is disputed: a Build Report fact or the detector's finding;
- the location in the report (optional; if not given, the field is determined from the quote): the path to the field in `build_report.json` or `injection_verdict.json`, for example `/modules/1/works`;
- the exact statement in the report that is wrong, quoted;
- what is actually true;
- evidence: commands, logs, file paths with a line, a commit in the frozen Team Repository;
- a confirmation that the Appeal concerns a factual error, not the points awarded.

An Appeal without evidence is not accepted. A fact already rechecked on another Appeal is not rechecked again: the result is final (Rules, clause 12.3).

### Review and result

Rules, clause 12.3: "Appeals are reviewed automatically: the Submission is run again, and the dispute is resolved by a separate Judge. If an Appeal is upheld, the Judges re-evaluate the Submission on the basis of the corrected Build Report; the final score cannot be lowered as a result. The outcome of the review is published and is final."

The result is posted in the same issue and published in the results repository. The Finalists are determined after all Appeals filed in time have been reviewed (Rules, clause 12.1).

## Русский

Отчёты Отборочного этапа опубликованы по адресу https://github.com/openegiz-contest/qualifying-results.

### Где и когда

Апелляция подаётся задачей (issue) в этом репозитории по форме: https://github.com/openegiz-contest/qualifying-results/issues/new?template=appeal.yml.

Срок подачи Апелляций — 48 часов: с 2026-10-28 09:38 до 2026-10-30 09:38 (время Астаны; п. 12.1 Положения). Временем подачи считается время создания задачи. Апелляция, поданная вне срока, не принимается.

### Что можно оспорить

П. 12.2 Положения: «Апелляция принимается только в отношении фактической ошибки Отчёта сборки или заключения о попытке повлиять на ИИ-жюри — например, если Отчёт сборки указывает, что Модуль не запускается, а Команда представляет журнал, подтверждающий его запуск. Несогласие с выставленными баллами основанием для Апелляции не является.»

Оспорить можно:

- факт в Отчёте сборки вашей Команды: `came_up`, `steps`, `healthchecks`, `modules`, `scenarios`, `concept`, `built_on_openegiz`, `notes`;
- заключение о попытке повлиять на ИИ-жюри: `verdict`, `evidence`.

Нельзя оспорить: баллы, рассуждения Судей, место, Команду, коммит и время в отчёте.

### Как подать

Одна задача — один оспариваемый факт. В форме указываются:

- Репозиторий команды (`team-NNN`);
- что оспаривается: факт Отчёта сборки или заключение детектора;
- место в отчёте (необязательно; если не указано, поле определяется по цитате): путь к полю в `build_report.json` или `injection_verdict.json`, например `/modules/1/works`;
- точное утверждение в отчёте, которое неверно, в виде цитаты;
- что верно на самом деле;
- доказательства: команды, логи, пути к файлам со строкой, коммит в замороженном Репозитории команды;
- подтверждение, что Апелляция касается фактической ошибки, а не баллов.

Апелляция без доказательств не принимается. Факт, уже перепроверенный по другой Апелляции, повторно не перепроверяется: результат окончателен (п. 12.3 Положения).

### Рассмотрение и результат

П. 12.3 Положения: «Апелляция рассматривается автоматически: Решение запускается повторно, спор разрешает отдельный Судья. При удовлетворении Апелляции Судьи повторно оценивают Решение по исправленному Отчёту сборки; итоговый балл при этом не может быть снижен. Результат рассмотрения публикуется и является окончательным.»

Результат публикуется в той же задаче и в репозитории с результатами. Финалисты определяются после рассмотрения всех Апелляций, поданных в срок (п. 12.1 Положения).

## Қазақша

Іріктеу кезеңінің есептері https://github.com/openegiz-contest/qualifying-results мекенжайында жарияланған.

### Қайда және қашан

Апелляция осы репозиторийде issue ретінде форма бойынша беріледі: https://github.com/openegiz-contest/qualifying-results/issues/new?template=appeal.yml.

Апелляция беру мерзімі — 48 сағат: 2026-10-28 09:38 – 2026-10-30 09:38 аралығы (Астана уақыты; Ереженің 12.1-тармағы). Апелляция беру уақыты — issue құрылған уақыт. Мерзімнен тыс берілген Апелляция қабылданбайды.

### Нені даулауға болады

Ереженің 12.2-тармағы: «Апелляция Жинақ есебіндегі немесе ЖИ қазылар алқасына ықпал ету әрекеті туралы қорытындыдағы нақты қатеге қатысты ғана қабылданады — мысалы, Жинақ есебінде Модуль іске қосылмайды деп көрсетілсе, ал Команда оның іске қосылғанын растайтын журнал ұсынса. Қойылған балдармен келіспеу Апелляцияға негіз болып табылмайды.»

Даулауға болады:

- Командаңыздың Жинақ есебіндегі факті: `came_up`, `steps`, `healthchecks`, `modules`, `scenarios`, `concept`, `built_on_openegiz`, `notes`;
- ЖИ қазылар алқасына ықпал ету әрекеті туралы қорытынды: `verdict`, `evidence`.

Даулауға болмайды: балдар, Төрешілердің негіздемелері, орын, Команда, коммит және есептегі уақыт.

### Қалай беру керек

Бір issue — бір даулалатын факт. Формада мыналар көрсетіледі:

- Команда репозиторийі (`team-NNN`);
- не даулалады: Жинақ есебінің фактісі немесе детектордың қорытындысы;
- есептегі орын (міндетті емес; көрсетілмесе, өріс дәйексөз бойынша анықталады): `build_report.json` немесе `injection_verdict.json` ішіндегі өріске апаратын жол, мысалы, `/modules/1/works`;
- есепте қате болып табылатын нақты тұжырым, дәйексөз түрінде;
- шын мәнінде қалай екені;
- дәлелдер: командалар, журналдар, жолы көрсетілген файл жолдары, Мұздатудан кейінгі Команда репозиторийіндегі коммит;
- Апелляцияның берілген балдарға емес, нақты қатеге қатысты екенін растау.

Дәлелсіз Апелляция қабылданбайды. Басқа Апелляция бойынша қайта тексерілген факт қайта тексерілмейді: нәтиже түпкілікті (Ереженің 12.3-тармағы).

### Қарау және нәтиже

Ереженің 12.3-тармағы: «Апелляция автоматты түрде қаралады: Шешім қайта іске қосылады, дауды бөлек Төреші шешеді. Апелляция қанағаттандырылған жағдайда Төрешілер Шешімді түзетілген Жинақ есебі бойынша қайта бағалайды; бұл ретте қорытынды балл төмендетілмейді. Қарау нәтижесі жарияланады және түпкілікті болып табылады.»

Нәтиже сол issue-де және нәтижелер репозиторийінде жарияланады. Финалистер мерзімінде берілген барлық Апелляциялар қаралғаннан кейін анықталады (Ереженің 12.1-тармағы).
