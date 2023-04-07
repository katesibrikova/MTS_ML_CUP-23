# MTS_ML_CUP-23
https://ods.ai/competitions/mtsmlcup

Cоревнование от МТС Digital Big Data по определению пола/возраста владельца cookie

Решение вошло в топ-25% лидерборда конкурса: private 117 место, public 120 место.

Определение пола и возраста владельца HTTP cookie по истории активности пользователя в интернете на основе синтетических данных.
В моем распоряжении находится база данных в которой хранится информация об активности 400к+ пользователей на уровне даты+времени суток. 
Для формирования рабочего датасета я аггрегирую данные на уровне пользователя: user_id + [параметры/характеристики, полученные из данных ]

mts_ml_cup_sibrikova_main_body.ipynb: В данном ноутбуке я составляю таблицу с параметрами для каждого пользователя (его основной регион пребывания, основная модель устройства и пр), а так же добавляю данные по посещаемости сайтов-кластеров (эту задачу я выполнила ранее - см в mts_ml_cup_sibrikova_url_claster.ipynb). Далее Полученные данные разбиваю на обучающую и тестовую выборку и произвожу поиск наилучшей модели для поставленной задачи (Параллельно тестируя несколько вариантов кластеризации сайтов и подходы к определению возраста - задачей классификации или регрессией с последующим бакетированием на необходимые возрастные подгруппы)


mts_ml_cup_sibrikova_url_cluster.ipynb: аггрегируются данные по результатам парсинга заголовков имеющихся url-страниц. Производится фильтрация корректно собранных заголовков, приведение к единому языку с последующим переводом в векторы и кластеризацией сайтов на 50-150-300-500 подгрупп. Также производится разделение сайтов с отсуствующими заголовками на две подгруппы - с высокой популярностью среди пользователей ( топ-500 - далее используются как самостоятельные параметры), и с низкой - сжатие до 150 параметров методом FaissAlternatingLeastSquares.


MTS_ML_CUP_sibrikova_public_submition: финальный этап работы над проектом: получение результата для публичного теста + подбор гиперпараметров модели с целью повышения качества определения таргетов.

Используемые модели: Linear Regression, Logistic Regression, Random Forest classifier+regression, Catboost Classifier+regressor, LightGBM classifier+regressor.

Дополнительные инструменты: implicit.approximate_als.FaissAlternatingLeastSquares, CountVectorizer, k-mean clusterisation



