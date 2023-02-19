Итоговый проект
https://github.com/sat0304/future_sales

В данном задании необходимо предсказать
покупки товаров в ноябре 2015 года на основе
таблицы продаж за прошедшие 2 года с января
2013 по октябрь 2015.1.1.

Чтение исходных данных
from google.colab import drive
drive.mount('/content/drive')
pandas.read_csv

В таблицах содержится информация о
проданных товарах из категории: мелкая
электронная аппаратура, лазерные диски,
сувениры

1.2. Преобразование исходных
данных

Данные содержат символы * ! в начале строк наименований.
! ВО ВЛАСТИ НАВАЖДЕНИЯ (ПЛАСТ.)
D,0,40

Содержит ненужный символ «D» в конце некоторых строк.

Содержатся лишние пробелы между словами.

char = re.sub(r'^ +', '', char)
char = re.sub(r' +', ' ', char)

После преобразования все записи в таблицах имеют одинаковую структуру

0
1
2
3
4
"ВО ВЛАСТИ НАВАЖДЕНИЯ (ПЛАСТ.)"
0 40

"ABBYY FineReader 12 Professional Edition Full
1 76

"В ЛУЧАХ СЛАВЫ (UNV)"
2 40

"ГОЛУБАЯ ВОЛНА (Univ)"
3 40

"КОРОБКА (СТЕКЛО)"
4 40


![image](https://user-images.githubusercontent.com/73336464/219937317-7dbb6813-5d3f-4c54-bf7b-b2242116621f.png)


44 и 45 — аудиокниги по обучению
83 — элементы питания (батарейки)

В декабре количество проданных товаров самое большое.
![image](https://user-images.githubusercontent.com/73336464/219937361-40ed9fd2-c2da-4976-9fc3-a328a3bd32dc.png)


На гистограмме заметна тенденция по снижению продаж.

Основная масса продаваемых товаров не дороже 3000 рублейГистограмма показывает, что пик продаваемых товаров - 300 рублей

![image](https://user-images.githubusercontent.com/73336464/219937463-c9f55e0a-7660-437b-97b5-6ca20a5a24f8.png)


Количество ежедневно проданных товаров не более 10 в среднем.

Удаление наименований магазинов, которые отсутствуют в тестовой
выборке

train = train.loc[train.shop_id.isin(test["shop_id"].unique()), :]

Извлечение данных из таблицы продаж за "33" - октябрь 2015 года

Вычисление среднего размера продаж за последний месяц для магазина.

Вычисление среднего размера продаж за последний месяц
для категории товара.

Извлечение данных из таблицы продаж за "24 -33" - 2015 год

Вычисление среднего размера продаж за последний год для магазина.

Вычисление среднего размера продаж за последний год
для категории товара.

Создание столбца Ноябрь 2015 из значений октября 2015
+ случайные товары из средних значений

34 — ноябрь 2015 года.

Создание сводной таблицы

2.1. Создание модели

Создание обучающих и проверочных таблиц:

X = train_final.drop(columns=[('item_cnt_day',
'Nov2015')])
y = train_final[('item_cnt_day', 'Nov2015')]

Применение
LinearRegression
и
KNeighborsRegressor

Подстановка данных в полученную модель
LinearRegression, так как показал результат
проверки лучше:

MAE for LR: 0.00406212827439103
MAX ERROR for LR 2.9925310646262346

MAE for KNN: 0.14431950145995803
MAX ERROR for KNN 13.42962962962963

2.2 Создание модели бустинга

CB_model = cb.CatBoostRegressor()
LGB_model = lgb.LGBMRegressor()

CB_model.fit(X_train, y_train)
MAE test dataset for Catboost: 0.004110309578309225

LGB_model.fit(X_train, y_train)
MAE test dataset for LGB: 0.004700377967638779
