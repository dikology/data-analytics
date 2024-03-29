# Описание проекта
В нашем распоряжении данные сервиса Яндекс Недвижимость — архив объявлений за несколько лет о продаже квартир в Санкт-Петербурге и соседних населённых пунктах.
Ваша задача — выполнить предобработку данных и изучить их, чтобы найти интересные особенности и зависимости, которые существуют на рынке недвижимости.
О каждой квартире в базе содержится два типа данных: добавленные пользователем и картографические. Например, к первому типу относятся площадь квартиры, её этаж и количество балконов, ко второму — расстояния до центра города, аэропорта и ближайшего парка. 

# Описание данных
`airports_nearest` — расстояние до ближайшего аэропорта в метрах (м)
`balcony` — число балконов
`ceiling_height` — высота потолков (м)
`cityCenters_nearest` — расстояние до центра города (м)
`days_exposition` — сколько дней было размещено объявление (от публикации до снятия)
`first_day_exposition` — дата публикации
`floor` — этаж
`floors_total` — всего этажей в доме
`is_apartment` — апартаменты (булев тип)
`kitchen_area` — площадь кухни в квадратных метрах (м²)
`last_price` — цена на момент снятия с публикации
`living_area` — жилая площадь в квадратных метрах (м²)
`locality_name` — название населённого пункта
`open_plan` — свободная планировка (булев тип)
`parks_around3000` — число парков в радиусе 3 км
`parks_nearest` — расстояние до ближайшего парка (м)
`ponds_around3000` — число водоёмов в радиусе 3 км
`ponds_nearest` — расстояние до ближайшего водоёма (м)
`rooms` — число комнат
`studio` — квартира-студия (булев тип)
`total_area` — общая площадь квартиры в квадратных метрах (м²)
`total_images` — число фотографий квартиры в объявлении

#### Краткий обзор проведённой работы. 
В приведённом исследовании стояла задача изучить данные объявлений о продаже квартир в Санкт-Петербурге и соседних населённых пунктов за несколько лет и установить параметры, помогающие определить рыночную стоимость квартир.

В первой части мы готовили данные для исследования:
- Мы обнаружили достаточно большое количество пропусков в некоторых параметрах.
что сделали:
  - приняли высоту потолков за среднюю там, где они не были указаны
  - удалили строки, в которых не указана высота дома (всего этажей), так как их было очень мало
  - если не указано количество балконов - приняли за 0
  - если не указано название населённого пункта - указали `'unknown'`
  - приняли жилую площадь равной средней жилой площади в аналогичных по количеству комнат квартирах там, где значения не были указаны
  - приняли 0 парков и прудов рядом, если они не указаны
  - признак апартаментов приняли False, если ничего не указано

- В данных наблюдаются редкие значения, которые смещают выборки и могут быть ошибочными, так как выходят за рамки ожидаемых распределений. 
Мы обработали явные выбросы и аномалии в данных - редкие значения отбросили, а аномальные постарались привести к исходным или таким, которые не влияют на искажение исследования.
Влияние параметров на цену объекта изменилось численно, но порядок основных не поменялся.

Также для целей исследования добавили некоторые категории и параметры.

#### Главные выводы. 
Параметры, помогающие определить рыночную стоимость квартир, можно разделить на три категории:
1. Параметры объекта
    - общая площадь - наиболее важный показатель
    - жилая площадь
    - площадь кухни
    - количество комнат
2. Расположение
  - близость парков и прудов
  - близость к центру города
  - населённый пункт
3. Время публикации
  - ближе к концу недели выкладываются более дешёвые предложения (пт, сб и вс)
  - в начале и конце года цены самые высокие (с ноября по февраль), также летом есть подъём (июль-сентябрь)

  
Продажи в течение месяца можно считать быстрыми, а то, что не продаётся в течение года и более - необычайно долго.

#### Рекомендации.
В данных достаточно много пропусков, значения для которых должны были быть получены автоматически на основе картографических данных, или вычислены на основе разницы дат.
- airports_nearest         5532
- city_centers_nearest     5509
- parks_nearest           15568
- ponds_nearest           14552
- days_exposition          3172

Эти пропуски достаточно сложно обработать, также они могут означать как то, что рядом этих объектов нет, так и то, что объекты очень близко. Заменять их на 0 значит определить их в категорию "очень близко". Рекомендуем проверить формирование этих данных и какие-то значения, помогающие определить, что этот параметр нужно игнорировать (слишком далеко/близко)

Некоторые параметры, вроде количества балконов, могут иметь значения по-умолчанию, чтобы, например, если не указано количество балконов - вариант был по-умолчанию 0, или 0 парков и прудов рядом, если они не указаны.

Есть некоторые ошибки в типах данных, которые стоило бы исправить при формировании выгрузки. Для целей исследования мы их заменили:
- `balcony` — стоит поменять тип данных на `int`
- `days_exposition` — стоит поменять тип данных на `int`
- `first_day_exposition` — дата публикации имеет строковый формат - надо поменять на `datetime`
- `floors_total` — можно поменять тип данных на `int`
- `is_apartment` — в описании указано, что это `bool`, но тут это строка
- `parks_around3000` — стоит поменять тип данных на `int`
- `ponds_around3000` — стоит поменять тип данных на `int`

Названия населённых пунктов рекомендуется делать выбором из списка, а не ручным вводом - в данных были встречены неявные дубликаты

