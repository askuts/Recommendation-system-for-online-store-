# Рекомендательная система для онлайн магазина
Инициатор проекта - онлайн-магазин Rex London, в котором продаются уникальные сувениры на все случаи жизни.

Компания заинтересована в масштабировании за счет увеличения клиентской базы в других странах благодаря эффективному привлечению клиентов, а также заинтересована в повышении клиентской лояльности за счет персонализированного подхода к рекомендациям покупок. В связи с этим онлайн-магазин стремится создать эффективную рекомендательную систему, которая будет способна создать персонализированный и удовлетворительный покупательский опыт для клиентов.

# Бизнес-цели, гипотезы задачи для ML
 
## Бизнес -заказчик сформулировал основные бизнес-цели для онлайн-магазина:
1. Рост объема продаж за счет увеличения:
·  	среднего количества покупок;
·  	среднего чека покупок;
·  	количества возвращений пользователей на сайт. 
2. Оптимизация закупок во времени: уменьшение лишних запасов и снижение риска низкой ликвидности (кассового разрыва).
3. Рост EBITDA за счет оптимизации расходов на человеческие ресурсы в течение года.
 
## Командой были сформулированы гипотезы, которые требуется проверить для более детальной проработки ML.
*Гипотеза 1*: наиболее высокая потребительская активность достигается в декабре в преддверии Рождества и Нового года.
Необходимо выровнять загрузку человеческих ресурсов магазина и нанять дополнительный персонал на упаковку и отправку товаров в декабре или определить иные пиковые сезоны.

*Как будем проверять*: сравнить объемы продаж по месяцам

*Метод*: аналитический и графический метод (Power BI)
 
*Гипотеза 2*: вечером люди склонны делать более дорогие покупки.
Мы проанализировали потребительское поведение и сделали вывод о том, что вечером люди более склонны к импульсивным покупкам: это происходит из-за снижения фокуса и внимания после количества принимаемых решений днем. Таким образом, рекомендательная система будет предлагать более дорогие альтернативы и сопутствующие товары в вечернее время для увеличения среднего чека.
*Как будем проверять*: сравнить количество покупок в чеке в разрезе времени суток, сравнить средний чек в разрезе времени суток
*Метод*: аналитический и графический метод (Power BI)
 
Гипотеза 3: продажи (в объемах и в выручке) увеличиваются за некоторое время до праздников.
Так как магазин имеет определенную специфику (подарки и товары для праздников), то логично предположить, что потребительская активность возрастает перед праздниками. Необходимо проанализировать динамику и выяснить, когда наступает пик продаж, с целью оптимизации закупок и снижения риска низкой ликвидности. 
*Как будем проверять*: рассчитаем выручку до праздников и посмотрим на динамику по дням
*Метод*: аналитический и графический (Power BI)
 
Гипотеза 4: популярная группа товаров также имеет пики продаж.
Самая популярная категория товаров оказывает наиболее высокое влияние на продажи и планирование закупок. Следовательно, необходимо проанализировать динамику продаж для объективного планирования закупок.
*Как будем проверять*: возьмем популярную категорию товара «t-lights», проанализируем динамику продаж по неделям
*Метод*: аналитический и графический (Excel)

Гипотеза 5: Инфляция негативно влияет на выручку и продажи, так как онлайн-магазин продает продукт не первой необходимости. 
Так как основные товары, продаваемые в онлайн-магазине, не являются товарами первой необходимости, при растущей инфляции потребители сокращают покупки таких товаров. 
*Как будем проверять*: построим корреляцию между помесячной инфляцией в Великобритании в 2010-2011 годах и проверим корреляцию с основными показателями продаж.
*Метод*: корреляция (Python)

# Постановка задач для ML
Определить ассоциативные правила для увеличения продаж (среднего чека и среднего количества позиций в покупке);
Опираясь на кластеризацию пользователей, вывести ассоциативные правила для кластера “среднячки” с целью увеличения среднего чека и кластера “привидения” с целью возвращения пользователей на платформу после длительной паузы в покупках;
Внедрить полученные ассоциативные правила в рекомендательную систему на сайте, которая будет наиболее эффективно предлагать сопутствующие товары пользователям

