# Исследование поведения пользователей в приложении для продажи продуктов
(Воронки продаж, A/A/B-тесты, поправк Холма)

Данный проект посвящен изучению поведения пользователей в приложении для покупки продуктов. Дизайнеры решили поменять визуал интерфейса – сменить стиль шрифта. Для исследования влияния данных изменений понадобилось проведение теста. 

Для проведения A/A/B теста пользователи были разбиты на 3 группы – 2 контрольные, собранные со старого интерфейса, и 1 экспериментальная – собранная с нового.

## **Цели проектного исследования**
1.	Выявить проблемные этапы на которых пользователи сходят с пути, ведущего к совершению покупки.
2.	Провести A/A/B-эксперимент, чтобы определить, как изменение шрифтов влияет на пользовательское поведение и конверсии.
3.	Составить рекомендации по повышению конверсии пользователей.

## **Итоги проекта**

По итогам исследования были сделаны следующие выводы: 
1.	Воронка продаж:
- Выявлена последовательность событий: главный экран → экран с товарами → корзина → успешная оплата.
- Проблемный этап: переход с главного экрана на экран с товарами (конверсия 61%). Общая конверсия от первого события до покупки составляет 47%.
2.	A/A/B-эксперимент:
- Три группы: две контрольные (246, 247) и одна экспериментальная (248).
- Статистически значимых различий в конверсиях между группами не выявлено, включая поправку Холма.

**Итог**: Проблемным шагом является переход пользователей с Главного экрана на Экран с товарами. Замена шрифта не влияет на пользовательский опыт и конверсии.

## **Рекомендации**
1.	Для повышения конверсии следует поработать над переходом с главного экрана на экран с товарами:
- Обновить интерфейс главного экрана, поработать над его UX-дизайном.
- Проверить техническую составляющую загрузки страницы товаров.
2.	Внедрить новый шрифт без опасений, так как он не оказывает негативного влияния на вовлечённость и конверсии.

# Ниже я представил план работы, описание данных, использовнных инструментов и ход моей работы.

## План работы
1. Загрузка данных.
2. Подготовка данных.
3. Исследовательский анализ данных.
4. Изучение воронки событий.
5. Проведение эксперимента и исследование результатов
6. Общий вывод.

## Описание данных:
- EventName — название события;
- DeviceIDHash — уникальный идентификатор пользователя;
- EventTimestamp — время события;
- ExpId — номер эксперимента (246 и 247 — контрольные группы, 248 — экспериментальная).

## Использованные инструменты и их назначение:
- Pandas — обработка и анализ табличных данных
- Matplotlib/Seaborn — статичная визуализация данных
- Plotly — интерактивная визуализация (графики и диаграммы)
- NumPy — математические операции с массивами
- SciPy — статистический анализ (тесты, распределения)
- Statsmodels — Z-тест для пропорций
- Datetime — работа с датами и временем

## **Ход работы**
### 1.	Исследовательский анализ данных:
- Данные охватывают период с 25.07.2019 по 07.08.2019.
- Общее количество событий: 243 713, из них 5 уникальных событий.
- Количество уникальных пользователей: 7 551.
- На одного пользователя в среднем приходится 32,3 события, медиана — 20 событий. В нормальном диапазоне 1–80 событий.
- Динамика событий показала, что полнота данных начинается с 01.08.2019. В связи с этим события до этой даты были отсечены, что составило всего 1,16% данных.
- После очистки данных распределение событий, пользователей и их активности осталось равномерным.
### 2.	Построение воронки продаж:
- В исходной последовательности событий было исключено событие Tutorial из-за его редкости (0,1% всех событий).
- Итоговая последовательность событий:
1.	Главный экран (MainScreenAppear): 117 328 событий, 7 419 пользователей (доля 98,5%).
2.	Экран с товарами (OffersScreenAppear): 46 333 события, 4 593 пользователя (доля 61%).
3.	Корзина (CartScreenAppear): 42 303 события, 3 734 пользователя (доля 49,6%).
4.	Успешная оплата (PaymentScreenSuccessful): 33 918 событий, 3 539 пользователей (доля 47%).
- Конверсия с главного экрана на экран с товарами составляет 61%, что является самой уязвимой точкой воронки.
- Общая конверсия от первого события до покупки составляет 47%.
### 3.	Проведение A/A/B-эксперимента:
- В эксперименте участвовали три группы: две контрольные (246, 247) и одна экспериментальная (248).
- Анализ распределения данных по группам:
1) Группа 246: 80 181 событий, 2 489 пользователей.
2) Группа 247: 77 950 событий, 2 520 пользователей.
3) Группа 248: 85 582 событий, 2 542 пользователя.
- Доля пользователей, совершивших каждое событие, для всех групп оказалась практически идентичной.
### 4.	Гипотезы и статистический тест:
- Для проверки гипотез использовались t-тесты с уровнем значимости 0,05.
- Проверенные гипотезы:
1.	H0: Конверсии групп 246 и 247 равны. (p-value = 0,75 — гипотеза не отвергается).
2.	H0: Конверсии групп 246 и 248 равны. (p-value = 0,07 — гипотеза не отвергается).
3.	H0: Конверсии групп 247 и 248 равны. (p-value = 0,45 — гипотеза не отвергается).
4.	H0: Конверсии объединённых контрольных групп (246 и 247) и группы 248 равны. (p-value = 0,18 — гипотеза не отвергается).

### (С полной моей работой Вы можете ознакомиться в файле под названием "Исследование поведения пользователей в приложении для продажи продуктов", хранящемся в данной папке.)
