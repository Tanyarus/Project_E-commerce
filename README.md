# Project_E-commerce
Проект e-commerce:
Нас попросили проанализировать совершенные покупки и ответить на следующие вопросы:
1. Сколько у нас пользователей, которые совершили покупку только один раз?
2. Сколько заказов в месяц в среднем не доставляется по разным причинам (вывести детализацию по причинам)?
3. По каждому товару определить, в какой день недели товар чаще всего покупается.
4. Сколько у каждого из пользователей в среднем покупок в неделю (по месяцам)?
5. Используя pandas, проведи когортный анализ пользователей. В период с января по декабрь необходтмо выявить когорту с самым высоким retention на 3й месяц. Описание подхода можно найти тут.
6. Необходимо построить RFM-сегментацию пользователей, чтобы качественно оценить свою аудиторию. В кластеризации можешь выбрать следующие метрики: R - время от последней покупки пользователя до текущей даты, F - суммарное количество покупок у пользователя за всё время, M - сумма покупок за всё время.
   Подробно опиши, как ты создавал кластеры. Для каждого RFM-сегмента построй границы метрик recency, frequency и monetary для интерпретации этих кластеров. Пример такого описания: RFM-сегмент 132 (recency=1, frequency=3, monetary=2) имеет границы метрик recency от 130 до 500 дней, frequency от 2 до 5 заказов в неделю, monetary от 1780 до 3560 рублей в неделю.
   
Файлы:
olist_customers_datase.csv — таблица с уникальными идентификаторами пользователей

olist_orders_dataset.csv — таблица заказов

olist_order_items_dataset.csv — товарные позиции, входящие в заказы

olist_orders_dataset - Уникальные статусы заказов в таблице¶

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Для начала проведем разведывательный анализ данных. Посмотрим на типы данных и приведем их нужным по необходимости, проверим размерность таблиц, есть ли пропущенные значения и дубликаты.
# загружаем нужные библиотеки
import pandas as pd

import numpy as np

from operator import attrgetter

import datetime

import seaborn as sns

import matplotlib.pyplot as plt

%matplotlib inline

# считываем датасеты. Все данные с датами приводим к формату дат.
customers_df   = pd.read_csv('olist_customers_dataset.csv')

orders_df      = pd.read_csv('olist_orders_dataset.csv', parse_dates=['order_purchase_timestamp','order_approved_at',
                                                                           'order_delivered_carrier_date', 'order_delivered_customer_date',
                                                                           'order_estimated_delivery_date'])
                                                                           
order_items_df = pd.read_csv('olist_order_items_dataset.csv', parse_dates = ['shipping_limit_date'])


customer_state              object
dtype: object

