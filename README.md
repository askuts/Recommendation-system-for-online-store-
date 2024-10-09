# Рекомендательная система для онлайн магазина
Инициатор проекта - онлайн-магазин Rex London, в котором продаются уникальные сувениры на все случаи жизни.

Компания заинтересована в **повышении клиентской лояльности** за счет **персонализированного подхода** к рекомендациям покупок. В связи с этим онлайн-магазин стремится создать **эффективную рекомендательную систему**, которая будет способна создать персонализированный и удовлетворительный покупательский опыт для клиентов.

# Бизнес-цели, гипотезы задачи для ML
 
## Бизнес -заказчик сформулировал основные бизнес-цели для онлайн-магазина:
<details>
<summary>Нажмите, чтобы раскрыть</summary>
 
1. **Рост объема продаж** за счет увеличения:
-  	среднего количества покупок;
-  	среднего чека покупок;
-  	количества возвращений пользователей на сайт. 
3. **Оптимизация закупок** во времени: уменьшение лишних запасов и снижение риска низкой ликвидности (кассового разрыва).
4. **Рост EBITDA** за счет оптимизации расходов на человеческие ресурсы в течение года.

</details>

## Командой были сформулированы гипотезы, которые требуется проверить для более детальной проработки ML.

<details>
<summary>Нажмите, чтобы раскрыть</summary>

| №  | Гипотеза | Как будем проверять | Метод |
|----|----------|---------------------|-------|
| 1  | **Гипотеза 1:** Наиболее высокая потребительская активность достигается в декабре в преддверии Рождества и Нового года. Необходимо выровнять загрузку человеческих ресурсов магазина и нанять дополнительный персонал на упаковку и отправку товаров в декабре или определить иные пиковые сезоны. | Сравнить объемы продаж по месяцам | Аналитический и графический метод (Power BI) |
| 2  | **Гипотеза 2:** Вечером люди склонны делать более дорогие покупки. Это происходит из-за снижения фокуса и внимания после количества принимаемых решений днем. Рекомендательная система будет предлагать более дорогие альтернативы и сопутствующие товары в вечернее время для увеличения среднего чека. | Сравнить количество покупок в чеке в разрезе времени суток, сравнить средний чек в разрезе времени суток | Аналитический и графический метод (Power BI) |
| 3  | **Гипотеза 3:** Продажи (в объемах и в выручке) увеличиваются за некоторое время до праздников. Необходимо проанализировать динамику и выяснить, когда наступает пик продаж, с целью оптимизации закупок и снижения риска низкой ликвидности. | Рассчитать выручку до праздников и посмотреть на динамику по дням | Аналитический и графический (Power BI) |
| 4  | **Гипотеза 4:** Популярная группа товаров также имеет пики продаж. Необходимо проанализировать динамику продаж для объективного планирования закупок. | Проанализировать динамику продаж популярной категории товара «t-lights» по неделям | Аналитический и графический (Excel) |
| 5  | **Гипотеза 5:** Инфляция негативно влияет на выручку и продажи, так как онлайн-магазин продает продукт не первой необходимости. При растущей инфляции потребители сокращают покупки таких товаров. | Построить корреляцию между помесячной инфляцией в Великобритании в 2010-2011 годах и проверить корреляцию с основными показателями продаж | Корреляция (Python) |

</details>

## Постановка задач для ML

<details>
<summary>Нажмите, чтобы раскрыть</summary>
1. Определить ассоциативные правила для увеличения продаж (среднего чека и среднего количества позиций в покупке):

1. Опираясь на кластеризацию пользователей, вывести ассоциативные правила для кластера “среднячки” с целью увеличения среднего чека и кластера “привидения” с целью возвращения пользователей на платформу после длительной паузы в покупках;

2. Внедрить полученные ассоциативные правила в рекомендательную систему на сайте, которая будет наиболее эффективно предлагать сопутствующие товары пользователям

</details>

# ОБРАБОТКА ДАННЫХ

Мы решили, что заказчику важно понимать устройство кода Python, поэтому в пакете документов будет прикреплен отдельный файл [“Обработка данных”](/data_processing/Data_processing.ipynb) с подробным описанием кода. 

Предлагаем далее рассмотреть основные моменты обработки данных:

- **Загрузка библиотек:** pandas, numpy, datetime, seaborn, matplotlib, sklearn, yellowbrick, pycountry, calendar, warnings.

- **Столбцы датасета:** 
  - Invoice 
  - StockCode 
  - Description 
  - InvoiceDate 
  - Quantity 
  - Price 
  - Customer ID 
  - Country 

После проверки типа данных и просмотра статистики данных было принято решение:

1. Проверить данные на наличие полностью идентичных строк в случае, если транзакции задублировались, и удалить их.
2. Удалить все строки с операциями по возвратам товара.
3. Удалить строки с пропущенными значениями в столбце 'CustomerID'.
4. Проверить отрицательные и нулевые значения в столбцах 'Quantity’ и ‘Price’.
5. Удалить строки с ручным вводом данных ‘Manual’, которые не содержат релевантной информации.
6. Удаление выбросов в данных по 'Quantity’ и ‘Price’.
7. Удалить неопределенные страны и союзы.

Для проверки поставленных гипотез нам потребовалось добавить в датасет следующие данные:

- Добавление столбцов с информацией по времени, месяцу, дню-месяцу-году.
- Добавление столбца с днями недели, в которые была произведена транзакция.
- Добавление дополнительного территориального признака в виде территории и региона, основываясь на информации о стране. В данном пункте нам потребовалось изменить наименование некоторых стран для корректной работы кода.
- Добавили категориальную переменную по времени суток, времени года и кварталам.
- Добавили столбец по подсчету выручки по каждой транзакции.
- Добавили данные по праздникам для каждой страны и посчитали в новом столбце сколько дней от дня транзакции до ближайшего праздника в стране, в которой произошла транзакция.
- Добавляем в датасет продаж в Великобритании данные по инфляции на каждый месяц.

# Проверка гипотез графическим методом

Был проведен анализ в рамках сформулированных гипотез. Ниже опишем его результаты. C отчетом в MS Power BI можно ознакомиться по [ссылке](data_visualization/online_retail_II_power_bi.pdf)

## Гипотеза 1
**«Наиболее высокая потребительская активность достигается в декабре в преддверии Рождества и Нового года»** не подтвердилась.

![Рис.4.1. Объем продаж по месяцам](/data_visualization/images/image1.png) 
![Рис.4.2. Объем продаж по кварталам](/data_visualization/images/image2.png) 

Анализ продаж помесячно показал, что самый большой объем приходится на ноябрь, а не декабрь. 

При этом в рамках анализа продаж поквартально можно сделать вывод, что самые высокие продажи достигаются в Q4 и растут по сравнению с Q3 на 35,8%.

Таким образом, в четвертом квартале магазин будет особенно нуждаться в человеческом ресурсе. Предлагаем нанимать в этот период дополнительный персонал на аутстаффинг. Такое решение позволит сократить расходы на персонал в невысокий сезон и увеличить годовую EBITDA.

## Гипотеза 2
**«Вечером люди склонны делать более дорогие покупки»** не подтвердилась. Покупатели склонны совершать дорогие покупки не вечером, а утром.

Среднее количество совершенных покупок утром также выше, чем вечером. Поэтому необходимо настроить рекомендательную систему таким образом, чтобы она предлагала более дорогие товары в утреннее время.

![Рис.4.3. Количество товаров в чеке (шт.) и средний чек (£) в разрезе времени суток](/data_visualization/images/image3.png)

## Гипотеза 3
Подтвердилась: количество продаж зависит от количества дней, оставшихся до праздника. Явно видно, что при уменьшении оставшегося времени до праздника продажи растут.

Пик продаж по количеству и выручке приходится на 25-ый день до праздника. По мере приближения праздника (до 25-го дня) количество продаж снижается, но остается сравнительно высоким относительно остального отрезка времени (после 25-го дня). Таким образом, можно сделать вывод о том, что в интернет-магазине пользователи делают покупки заранее до праздников.

![Рис.4.4. Объем продаж (тыс. товаров) и Выручки (£) в зависимости от дней, оставшихся до праздника](/data_visualization/images/image4.png)

Мы проанализировали и отметили, что график объема продаж и выручки в зависимости от дней, оставшихся до праздника, волатилен. При углубленном анализе было выявлено, что в дата сете почти нет данных продаж за пятницу. Такая динамика связана с внутренними особенностями бизнес-процессов онлайн-магазина.

## Гипотеза 4
Подтвердилась: популярная категория товаров продается активнее в ноябре, что соответствует общей динамике. Пик продаж приходится на 47 неделю года. Следовательно, необходимо планировать закупки и увеличивать запасы в ноябре в данной категории.

![Рис.4.5. Выручка популярной категории товаров «t-lights», фунтов](/data_visualization/images/image5.png)

Таким образом, опираясь на выводы по гипотезам 3 и 4, предлагаем следующее управленческое решение: спланировать закупки с увеличением запасов товаров в ноябре и в среднем за месяц (за 25-30 дней) до крупных праздников. При этом активно наращивать запасы в другие месяцы и сокращать ликвидность, доступную бизнесу, не рекомендуется, для снижения рисков кассового разрыва.

## Гипотеза 5
Не подтвердилась: сильной негативной связи с показателями продаж при росте инфляции не выявлено. Корреляция инфляции со всеми показателями по модулю < 0.1, поэтому можно сделать вывод о том, что сильной корреляции нет.

![Рис.4.6. Корреляционная матрица инфляции и показателей продаж](/data_visualization/images/image6.png)

Для проверки данной гипотезы мы провели дополнительную работу с датасетом продаж в Великобритании. Была произведена группировка данных по месяцам каждого года, для этого были подсчитаны следующие показатели: среднее количество товаров в чеке, сумма количества всех товаров в чеке, количество покупателей, количество уникальных покупателей, общая выручка, средняя выручка, количество чеков всего, количество уникальных чеков. 

Годовая инфляция за 2010 год в Англии составила 3,64%, в 2011 году - 4,28%, что является достаточно высоким показателем для фунта в начале 10-х годов. При этом, средняя выручка сокращается при росте инфляции на фоне сохранения среднего количества продаж: таким образом, можно сделать вывод, что потребители начали выбирать более дешёвые товары. 

В бизнесе преобладают B2C отношения, мы можем сделать вывод, что при увеличении инфляции потребительские привычки клиентов остаются неизменными. Наши товары остаются востребованными на рынке, и даже в условиях экономического кризиса люди не считают наши продукты чрезмерно дорогими для отказа от них.

Количество уникальных покупателей и чеков также не зависит от инфляции, что подчеркивает привлекательность нашего магазина даже в условиях экономического кризиса, поскольку он продолжает привлекать клиентов.
