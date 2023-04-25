# ML, Прогнозирование оттока клиентов телеком компании,  Задача классификации 

Статус проекта: Завершен

## Описание проекта

**О компании:**  Заказчик - оператор связи, предоставляет услуги стационарной телефонной связи, подключение к иентренету, сопутствующие услуги (антивирус, выделенная линия технической поддержки, облачное хранилище файлов, стриминговое телевидение).
<br>
<br> **Цель проекта:** создать модель, которая сможет определять клиентов, которые могут отказаться от услуг компании. Модель будет использоваться для  удержания таких клиентов в дальнейшем, способы удержания, например,  промокоды или специальные условия. 
<br>
<br> **Исходные данные:** персональные данные клиентов актуальные на 01.02.2020, информация о подключенных услугах, условия оплаты. Исходные данные содержатся в  4 датасетах:

1. информация о договоре;
2. персональные данные клиентов;
3. данные о подключенных интернет услугах;
4. данные о услугах телефонии.
<br>
<br> **Требование к модели:**  Метрика AUC_ROC на тестовых данных должна иметь значение не менее 0.85.



## Ход исследования

1. Импорт библиотек.
2. Первичное знакомство с данными:
- Импорт данных; 
- Изучение 4-х таблиц по отдельности (методы describe, info, sample);
3. Предобработка:
-  Объединение таблиц при помощи merge по customer_id; 
-  Создание новых столбцов:
    - целевой признак (клиент ушел или нет);
    - как долго является клиентом в днях (до даты окончаняи или до 01.02.2020);
- Обработка пропусков, аномалий и дубликатов;
- Изменение формата данных, где требуется;
- Удаление избыточных столбцов:
    - begin_date;
    - end_date;
    - customer_id;
4. Исследовательский анализ данных:
- Постороение графиков в разрезе оттока;
- Проверка данных на мультиколлинеарность.
5. Разделение данных на выборки (0.25 test).
6. Кодирование OHE.
7. Подбор гиперпараметров при помощи GridSearch у следующих моделей:
- RandomForestClassifier;
- LogisticRegression;
- CatBoostClassifier.
8. Выбор лучшей модели.
9. Тестирование:
- Проверка качества лучшей модели на тестовой выборке (показатель успешности AUC_ROC >= 0.85).
- Исследование важности признаков лучшей модели;
- ROC-кривая;
- Матрица ошибок.


## Выводы по результатам проекта

В ходе роботы был выполнен:
<br>
1. Первичное знакомство с данными.
2. Предобработка, в которой мы объединили 4 датасета в один, создали дополнительные признаки, заполнили пропуски.
3. Исследовательских анализ данных, в котором построили графики в разрезе оттока и тепловую карту с взаимосвязями признаков. В ходе ИАД замечено, что:
- ушедшие клиенты плтили в месяц больше, оставшихся (60-100 у.е. против 20 у.е.)
- большинство использовало ежемесяный тип оплаты;
- большинство использовало электронные чеки;
- не использовали такие сервисы как антивирус (`device_protection`), блокировка небезопасных сайтов (`online_security`), выделенная линия технической поддержки (`tech_support`);
- большинство было клиенатми менее 100 дней.
4. Моделирование. При помощи кросс-валидации были были обучены 3 модели RandomForestClassifier, LogisticRegression, CatBosstClassifier. 
5. В результате обучения лучше всех себя показала модель CatBosstClassifier, на тестовых данных метрика ROC_AUC = 0.926.



[Тетрадка проекта]()