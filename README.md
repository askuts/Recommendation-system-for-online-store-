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

Мы решили, что заказчику важно понимать устройство кода Python, поэтому в пакете документов будет прикреплен отдельный файл [“Обработка данных”](Предобработка%данных/Data_processing.ipynb) с подробным описанием кода. 

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
2. Удалить все строки с операциями по возвратам товара (код операции начинается с символа ‘C’).
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
