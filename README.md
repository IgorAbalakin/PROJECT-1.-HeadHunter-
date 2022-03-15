# PROJECT-1. Анализ вакансий из HeadHunter 

### Оглавление 
[1. Описание проекта](https://github.com/IgorAbalakin/HH_data_project/blob/main/README.md#Описание-проекта) 

[2. Базовый анализ структуры данных](https://github.com/IgorAbalakin/HH_data_project/blob/main/README.md#Базовый-анализ-структуры-данных) 

[3. Преобразование данных](https://github.com/IgorAbalakin/HH_data_project/Project0/blob/main/README.md#Преобразование-данных) 

[4. Исследование зависимостей в данных](https://github.com/IgorAbalakin/HH_data_project/Project0/blob/main/README.md#Исследование-зависимостей-в-данных) 

[5. Очистка данных](https://github.com/IgorAbalakin/HH_data_project/blob/main/README.md#Очистка-данных) 
 
____
### Описание проекта 
⭐ Компания HeadHunter хочет построить модель, которая бы автоматически определяла примерный уровень заработной платы, подходящей пользователю, исходя из информации, которую он указал о себе. Прежде чем построить модель, данные необходимо преобразовать, исследовать и очистить.
 
:arrow_up: [к оглавлению](https://github.com/IgorAbalakin/HH_data_project/blob/main/README.md#Оглавление)

 ____
### Базовый анализ структуры данных
[hh.csv](https://drive.google.com/file/d/1IH_0aL3kU0N08PTw4wsdGGJUX-foeqjD/view?usp=sharing)

Исходный файл представляет собой dataframe из 44744 объектов (резюме соискателей) с 12 признаками (пол, возраст, город, опыт работы и т.д., Dtype = 'object'). В трех из них присутствуют пропуски.

:arrow_up: [к оглавлению](https://github.com/IgorAbalakin/HH_data_project/blob/main/README.md#Оглавление)

____
### Преобразование данных

1. Преобразование признака "Образование и ВУЗ"
Изначальный формат: *<Уровень образования год выпуска ВУЗ специальность...>*
Создан новый признак "Образование", который должен иметь 4 категории: "высшее", "неоконченное высшее", "среднее специальное" и "среднее".

2. Преобразование признака "Пол, возраст"
Изначальный формат: *<Пол , возраст , дата рождения >*
Созданы два новых признака "Пол" (значения "М" и "Ж") и "Возраст" (целое число).

3. Преобразование признака "Опыт работы"
Изначальный формат: *<Опыт работы: n лет m месяцев, периоды работы в различных компаниях…>*
Создан новый признак "Опыт работы (месяц)", содержащий информацию о том, сколько месяцев проработал соискатель.

4. Преобразование признака "Город, переезд, командировки"
Изначальный формат: *<Город , (метро) , готовность к переезду (города для переезда) , готовность к командировкам>*
Созданы три новых признака:
- "Город", который должен иметь 4 категории: "Москва", "Санкт-Петербург", "город-миллионник" и "другие"
- "Готовность к переезду" (True/False)
- "Готовность к командировкам" (True/False)

5. Преобразование признаков "Опыт работы" "Занятость" и "График"
Изначальный формат: набор категорий желаемой занятости *<полная занятость, частичная занятость, проектная работа, волонтерство, стажировка>* и желаемого графика работы *<полный день, сменный график, гибкий график, удаленная работа, вахтовый метод>*
Созданы признаки-мигалки для каждой категории (метод преобразования категориальных признаков One Hot Encoding)

6. Преобразование признака "ЗП"
Изначальный формат (пример):
- 30000 руб.
- 50000 грн.
- 550 USD

С помощью dataframe [ExchangeRate.csv](https://drive.google.com/file/d/1B2o74P-ScqCo7zHp3pPV1u-m5CEKawLV/view?usp=sharing) создан признак "ЗП (руб)" - заработная плата в рублях.

:arrow_up: [к оглавлению](https://github.com/IgorAbalakin/HH_data_project/blob/main/README.md#Оглавление)

 ____
### Исследование зависимостей в данных 

1. Распределение возраста соискателей 

![](https://github.com/IgorAbalakin/HH_data_project/blob/main/png/age%20distribution.png?raw=true) 

Наиболее встречающийся возраст - 30 лет. Предельные значения признака - 14 и 100 лет, именно их можно отнести к аномалиям данного признака. Возраст большинства соискателей лежит в интервале от 27 до 36 лет, что может быть связано с наибольшей активностью и трудоспособностью людей в данный жизненный период.

2. Распределение опыта работы соискателей

![](https://github.com/IgorAbalakin/HH_data_project/blob/main/png/work%20experience%20distribution.png?raw=true)

Наиболее встречающийся опыт работы - 81 месяц. Предельные значения признака - 1 и 1188 месяцев, второе значение можно отнести к аномалиям данного признака. Опыт работы большинства соискателей лежит в интервале от 57 до 154 месяцев, что напрямую связано с возрастом соискателей.

3. Распределение заработной платы соискателей

![](https://github.com/IgorAbalakin/HH_data_project/blob/main/png/wages%20distribution.png?raw=true) 
Предельные значения уровня заработной платы - 1 рубль и 24 миллиона рублей. Значения менее тысячи и более миллиона рублей можно отнести к аномалиям данного признака. Желаемая зарплата большинства соискателей лежит в интервале от 37 до 95 тысяч рублей, высокий разброс может быть связан с разницей оплаты по профессиям и регионам.

4. Медианная заработная плата в зависимости от уровня образования

![](https://github.com/IgorAbalakin/HH_data_project/blob/main/png/median%20salary%20vs%20education%20level.png?raw=true)

Ожидаемо наибольший уровень доходов наблюдается для людей с высшим образованием, а наименьший для людей со средним образованием. Признак определенно играет роль при прогнозировании ЗП, т.к. медианные значения отличаются на 50%.

5. Заработная плата по городам

![](https://github.com/IgorAbalakin/HH_data_project/blob/main/png/wages-city%20distribution.png?raw=true)

Наибольший уровень медианной ЗП наблюдается в Москве, и падает с убыванием населения. То же самое можно сказать про размах: чем больше население города, тем больше разброс значений уровня заработной платы. Признак определенно играет роль при прогнозировании ЗП, т.к. медианные значения отличаются более чем, на 50%.

6. Зависимость медианной заработной платы от готовности к переезду и командировкам

![](https://github.com/IgorAbalakin/HH_data_project/blob/main/png/median%20salary%20vs%20moving%20and%20trips.png?raw=true)

Признак играет роль при прогнозировании ЗП. Ожидаемая зарплата кандидатов, готовых к переезду и командировкам выше более чем на 60%, чем у неготовых кандидатов. Готовность к командировкам существеннее влияет на уровень ЗП, чем готовность к переезду.

7. Зависимость медианной заработной платы, возраста и уровня образования

![](https://github.com/IgorAbalakin/HH_data_project/blob/main/png/median%20salary%20vs%20education%20level%20and%20age.png?raw=true)

У категории соискателей с высшим образованием быстрее всего растет ЗП. Люди с неоконченным высшим и средним образованием после 60 лет не занимаются поиском работы. Пик по уровню ЗП у высшего и неоконченного высшего образований достигается на уровне 40 лет, у других категорий пик не выражен. Максимальный возраст соискателей со средним специальным образованием несколько выше, что может быть связано с ограниченным количеством подобных специалистов.

8. Зависимость опыта работы от возраста

![](https://github.com/IgorAbalakin/HH_data_project/blob/main/png/age%20vs%20work%20experience.png?raw=true)

Основная масса точек лежит ниже уровня прямой Y ≈ X-20. Этот сдвиг может означать порог возраста начала профессиональной деятельности. 7 точек лежат выше прямой Y = X (опыт работ больше возраста), что является явной аномалией.

9. Зависимость заработной платы от опыта работы

![](https://github.com/IgorAbalakin/HH_data_project/blob/main/png/mean%20salary%20vs%20work%20experience.png?raw=true)

Данная гистограмма показывает, что наиболее дорогими являются специалисты с опытом работы на уровне 20 лет. Дальнейший спад средней зарплаты вероятно связан с возрастом соискателей и снижением требований к уровню ЗП. Выбросы со средней ЗП более 100 тыс. рублей связаны с малой выборкой для данных возрастных групп.

10. Зависимость медианной заработной платы от готовности работать полный день на полную занятость

![](https://github.com/IgorAbalakin/HH_data_project/blob/main/png/median%20salary%20vs%20total%20busyness.png?raw=true)

Диаграмма демонстрирует, что медианная ЗП соискателей готовых работать полный день на полную занятость больше в два раза, чем у соискателей неготовых к таким условиям. Отказ от одного из пунктов приводит к падению ЗП на треть.

11. Медианная заработная плата в зависимости от желаемой должности

![](https://github.com/IgorAbalakin/HH_data_project/blob/main/png/median%20salary%20vs%20job%20position.png?raw=true)

Топ-4 должностей связаны с управлением проектами. Уровень ожидаемого дохода руководителя на 50 % больше, чем у менеджера. После менеджмента три позиции занимают IT должности, затем три позиции технических специальностей, что, в общем и целом, отражает современные реалии рынка труда.

:arrow_up: [к оглавлению](https://github.com/IgorAbalakin/HH_data_project/blob/main/README.md#Оглавление)
 
____
### Очистка данных

1. Удалены полные дубликаты (158 записей)
2. Пропуски в столбце с опытом работы заполнены медианным значением
3. Удалены строки, где есть пропуск в столбцах с местом работы и должностью
4. Удалены резюме, в которых указана заработная плата либо выше 1 млн. рублей, либо ниже 1 тыс. рублей (89 записей)
5. Удалены резюме, в которых опыт работы в годах превышал возраст соискателя (7 записей)
6. Удалены выбросы признака "Возраст" по методу z-отклонения (3 записи, предельные значения признака).
Распределение возраста соискателей в логарифмическом масштабе

![](https://github.com/IgorAbalakin/HH_data_project/blob/main/png/age%20distribution%20(logarithmic%20scale).png?raw=true)

Логарифмическое распределение асимметрично в левую сторону (количество соискателей), но хвост длиннее в правой стороне. Это может быть связано с бОльшим количеством молодых соискателей с возрастом менее среднего (группа от 20 до 30 лет), и более широким диапазоном значений возраста выше среднего (группа от 30 до 60 лет).

:arrow_up: [к оглавлению](https://github.com/IgorAbalakin/HH_data_project/blob/main/README.md#Оглавление)
 
