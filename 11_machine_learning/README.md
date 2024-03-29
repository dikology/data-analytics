# Описание проекта

Сеть фитнес-центров «Культурист-датасаентист» разрабатывает стратегию взаимодействия с клиентами на основе аналитических данных. 

Распространённая проблема фитнес-клубов и других сервисов — отток клиентов. Для фитнес-центра можно считать, что клиент попал в отток, если за последний месяц ни разу не посетил спортзал. 

Чтобы бороться с оттоком, отдел по работе с клиентами «Культуриста-датасаентиста» перевёл в электронный вид множество клиентских анкет. Наша задача — провести анализ и подготовить план действий по удержанию клиентов.  

А именно: 
- научиться прогнозировать вероятность оттока (на уровне следующего месяца) для каждого клиента;
- сформировать типичные портреты клиентов: выделить несколько наиболее ярких групп и охарактеризовать их основные свойства;
- проанализировать основные признаки, наиболее сильно влияющие на отток;
- сформулировать основные выводы и разработать рекомендации по повышению качества работы с клиентами:
1) выделить целевые группы клиентов;
2) предложить меры по снижению оттока;
3) определить другие особенности взаимодействия с клиентами

# Описание данных

- Данные клиента за предыдущий до проверки факта оттока месяц:
  - '`gender`' — пол;
  - '`Near_Location`' — проживание или работа в районе, где находится фитнес-центр;
  - '`Partner`' — сотрудник компании-партнёра клуба (сотрудничество с компаниями, чьи сотрудники могут получать скидки на абонемент — в таком случае фитнес-центр хранит информацию о работодателе клиента);
  - `Promo_friends` — факт первоначальной записи в рамках акции «приведи друга» (использовал промо-код от знакомого при оплате первого абонемента);
  - '`Phone`' — наличие контактного телефона;
  - '`Age`' — возраст;
  - '`Lifetime`' — время с момента первого обращения в фитнес-центр (в месяцах).
- Информация на основе журнала посещений, покупок и информация о текущем статусе абонемента клиента:
  - '`Contract_period`' — длительность текущего действующего абонемента (месяц, 6 месяцев, год);
  - '`Month_to_end_contract`' — срок до окончания текущего действующего абонемента (в месяцах);
  - '`Group_visits`' — факт посещения групповых занятий;
  - '`Avg_class_frequency_total`' — средняя частота посещений в неделю за все время с начала действия абонемента;
  - '`Avg_class_frequency_current_month`' — средняя частота посещений в неделю за предыдущий месяц;
  - '`Avg_additional_charges_total`' — суммарная выручка от других услуг фитнес-центра: кафе, спорттовары, косметический и массажный салон.
- '`Churn`' — факт оттока в текущем месяце.

<a id="conclusion"></a>
# Выводы и базовые рекомендации по работе с клиентами

## Проделанная работа
- в датасете 4000 строк, пропусков нет.
- большинство признаков принимают значения 0 и 1
- в двух группах — тех, кто ушел в отток и тех, кто остался:
  - среднее значение периода контракта меньше у тех, кто ушёл
  - средний возраст ушедших - ниже
  - средняя частота посещений и выручка от доп. услуг меньше у ушедших
- Построили столбчатые гистограммы и распределения признаков для тех, кто ушёл (отток) и тех, кто остался (не попали в отток)
- Построли матрицу корреляций

- научились прогнозировать вероятность оттока (на уровне следующего месяца) для каждого клиента; модель логистической регрессии в этом случае превзошла классификатор случайного леса.

Метрики:
Accuracy: 0.93
Precision: 0.86
Recall: 0.83

- Посмотрели на средние значения признаков для кластеров. 
- Построили распределения признаков для кластеров. 

## 1. Выделим целевые группы клиентов:

### Группа 1: "Партнёры и долгосрочные контракты" (Кластер 3)

Часто являются сотрудниками компаний-партнёров.
Предпочитают контракты на 12 месяцев.
В этой группе наблюдается низкий уровень оттока.
Важно поддерживать сотрудничество с партнёрами и продвигать долгосрочные контракты.
### Группа 2: "Молодежь с высокой активностью" (Кластер 4)

Молодые клиенты с более низким возрастом.
Часто не используют групповые занятия, но активны в дополнительных услугах центра.
Склонны к короткосрочным контрактам.
Эта группа имеет наивысший уровень оттока. Важно разработать стратегию для удержания молодых клиентов, например, через привлекательные программы лояльности и акции.
### Группа 3: "Активные посетители среднего возраста" (Кластер 1)

Регулярно посещают занятия, в том числе групповые.
Средний возраст, более стабильные контракты.
Отток в этой группе низкий.
Важно поддерживать их активность и предлагать персонализированные программы тренировок.

## 2. Меры по снижению оттока:

Продвижение долгосрочных контрактов: Акцент на привлечении клиентов к долгосрочным контрактам, возможно, с бонусами или скидками для тех, кто заключает контракт на 6 или 12 месяцев.

Улучшение вовлечённости молодых клиентов: Разработка специальных программ и мероприятий для молодежи, включая интересные групповые тренировки, соревнования и социальные события.

Персонализированный подход: Анализ предпочтений клиентов и предоставление персонализированных тренировочных программ и рекомендаций.

Стимулирование активности в групповых занятиях: Продвижение и поощрение участия в групповых занятиях, например, через бонусы или скидки.

Мониторинг частоты посещений: Предупреждение клиентов о возможных последствиях нерегулярных тренировок и предложение индивидуальных планов поддержки.

## 3. Особенности взаимодействия с клиентами:

Контроль долгосрочных клиентов: Регулярная связь с клиентами с долгосрочными контрактами для поддержания их мотивации и интереса.

Мониторинг активности молодых клиентов: Систематический анализ активности молодых клиентов и оперативные меры по предотвращению оттока.

Повышение вовлечённости в групповые занятия: Организация интересных и разнообразных групповых тренировок, а также предоставление индивидуальных планов для тех, кто еще не участвует в них.

Поддержка среднего возраста: Предоставление дополнительных услуг, которые могут быть интересны этой группе, такие как индивидуальные консультации тренера или скидки на дополнительные услуги.

## Возможные основные признаки, влияющие на отток:

1. Длительность контракта (Contract_period):

Клиенты с короткосрочными контрактами могут быть более склонны к оттоку.

2. Время с момента первого обращения в фитнес-центр (Lifetime):

Клиенты с более длительным временем с момента первого обращения могут иметь более низкую вероятность оттока.

3. Средняя частота посещений в неделю за предыдущий месяц (Avg_class_frequency_current_month):

Клиенты, которые реже посещают занятия, вероятно, более подвержены оттоку.

4. Проживание или работа в районе, где находится фитнес-центр (Near_Location):

Клиенты, проживающие или работающие рядом с фитнес-центром, могут иметь более низкую вероятность оттока.

5. Участие в групповых занятиях (Group_visits):

Клиенты, участвующие в групповых занятиях, могут иметь более высокую лояльность.

6. Возраст (Age):

Молодые клиенты (25-30) или клиенты возраста (30-35) могут иметь различные паттерны оттока.

7. Суммарная выручка от дополнительных услуг (Avg_additional_charges_total):

Клиенты, которые чаще используют дополнительные услуги, могут быть более лояльными.