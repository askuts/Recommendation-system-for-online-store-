# Рекомендательная система для онлайн магазина
Инициатор проекта - онлайн-магазин Rex London, в котором продаются уникальные сувениры на все случаи жизни.

Компания заинтересована в **повышении клиентской лояльности** за счет **персонализированного подхода** к рекомендациям покупок. В связи с этим онлайн-магазин стремится создать **эффективную рекомендательную систему**, которая будет способна создать персонализированный и удовлетворительный покупательский опыт для клиентов.

# Бизнес-цели, гипотезы задачи для ML
 
## Бизнес -заказчик сформулировал основные бизнес-цели для онлайн-магазина:
1. **Рост объема продаж** за счет увеличения:
-  	среднего количества покупок;
-  	среднего чека покупок;
-  	количества возвращений пользователей на сайт. 
3. **Оптимизация закупок** во времени: уменьшение лишних запасов и снижение риска низкой ликвидности (кассового разрыва).
4. **Рост EBITDA** за счет оптимизации расходов на человеческие ресурсы в течение года.

## Командой были сформулированы гипотезы, которые требуется проверить для более детальной проработки ML.

<details>
<summary><strong>Нажмите, чтобы раскрыть<strong></summary>

| №  | Гипотеза | Как будем проверять | Метод |
|----|----------|---------------------|-------|
| 1  | **Гипотеза 1:** Наиболее высокая потребительская активность достигается в декабре в преддверии Рождества и Нового года. Необходимо выровнять загрузку человеческих ресурсов магазина и нанять дополнительный персонал на упаковку и отправку товаров в декабре или определить иные пиковые сезоны. | Сравнить объемы продаж по месяцам | Аналитический и графический метод (Power BI) |
| 2  | **Гипотеза 2:** Вечером люди склонны делать более дорогие покупки. Это происходит из-за снижения фокуса и внимания после количества принимаемых решений днем. Рекомендательная система будет предлагать более дорогие альтернативы и сопутствующие товары в вечернее время для увеличения среднего чека. | Сравнить количество покупок в чеке в разрезе времени суток, сравнить средний чек в разрезе времени суток | Аналитический и графический метод (Power BI) |
| 3  | **Гипотеза 3:** Продажи (в объемах и в выручке) увеличиваются за некоторое время до праздников. Необходимо проанализировать динамику и выяснить, когда наступает пик продаж, с целью оптимизации закупок и снижения риска низкой ликвидности. | Рассчитать выручку до праздников и посмотреть на динамику по дням | Аналитический и графический (Power BI) |
| 4  | **Гипотеза 4:** Популярная группа товаров также имеет пики продаж. Необходимо проанализировать динамику продаж для объективного планирования закупок. | Проанализировать динамику продаж популярной категории товара «t-lights» по неделям | Аналитический и графический (Excel) |
| 5  | **Гипотеза 5:** Инфляция негативно влияет на выручку и продажи, так как онлайн-магазин продает продукт не первой необходимости. При растущей инфляции потребители сокращают покупки таких товаров. | Построить корреляцию между помесячной инфляцией в Великобритании в 2010-2011 годах и проверить корреляцию с основными показателями продаж | Корреляция (Python) |

</details>

# Постановка задач для ML
1. Определить ассоциативные правила для увеличения продаж (среднего чека и среднего количества позиций в покупке);
2. Опираясь на кластеризацию пользователей, вывести ассоциативные правила для кластера “среднячки” с целью увеличения среднего чека и кластера “привидения” с целью возвращения пользователей на платформу после длительной паузы в покупках;
3. Внедрить полученные ассоциативные правила в рекомендательную систему на сайте, которая будет наиболее эффективно предлагать сопутствующие товары пользователям

<details>
<summary>Нажмите, чтобы раскрыть</summary>

Это скрытый текст. Он станет видимым только при нажатии на заголовок.

</details>
