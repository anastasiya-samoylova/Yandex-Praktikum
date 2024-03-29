# NLP, Обработка естественного языка,  Классификация комментариев

Статус проекта: Завершен

## Описание проекта

Интернет-магазин запускает новый сервис. Теперь пользователи могут редактировать и дополнять описания товаров, как в вики-сообществах. То есть клиенты предлагают свои правки и комментируют изменения других. Магазину нужен инструмент, который будет искать токсичные комментарии и отправлять их на модерацию. 

**Цель проекта**: Необходимо обучить модель классифицировать комментарии на позитивные и негативные. 
В нашем  распоряжении набор данных с разметкой о токсичности правок.

Криетрий успешности: значение метрики качества *F1* модели должно быть не меньше 0.75. 


**Описание данных**

Данные находятся в файле `---.csv`. Столбец *text* в нём содержит текст комментария, а *toxic* — целевой признак.



## Ход исследования


1. Загрузка данных;
2. ПОдгтовка данных:
- перевести все в нижний регистр;
- оставить только латиницу; 
- удалить stop_words;
3. Лемматизация (WordNetLemmatizer);
4. Обучение моделей, подобор гиперпараметры кросс-валидацией: 
- LogisticRegression;
- LGBMClassifier;
5. Проверка лучшей модели на тестовой выборке.


## Выводы по результатам проекта

Нашей целью было найти и обучить модель, которая способна классифицировать комментарии на позитивные и негативные для того, чтобы в дальнейшем токсичные отзывы на сайте магазина отправлялись на модерацию. При этом достигуть результата предсказания наилучшей модели по метрике *F1*  не меньше  0.75

В нашем распоряжении был набор данных с разметкой о токсичности комментариев, но для правильной работы предсказательных алгоритмов моделей нам пришлось очистить комментарии от лишних символов.

Для определения наилучшей модели мы остановили наш выбор на двух моделях *LogisticRegression*, *LGBMClassifier*. По итогам сравнеиня лучшей оказалась модель **LogisticRegression** с гиперпараметрами(-  C': 9, 'max_iter': 15),  значение *f1* метрики 0.761.

Таким образом мы можем  рекомендовать к использованию данную модель для классифицирования комментариев на позитивные и негативные в магазине.



[Тетрадка проекта](https://github.com/anastasiya-samoylova/Yandex-Praktikum/blob/main/n11_ml_nlp_comments_classification/npl_comments_classification.ipynb)
