### 1. Фильтрация «хороших» валют (USD, EUR, RUB), подсчёт суммарной суммы транзакций по каждой валюте
<code>select currency, 
&nbsp;&nbsp;sum(amount) as currency_amount
from transactions_v2 
where currency in ('RUB', 'USD', 'EUR')
group by currency</code>

<img width="424" alt="image" src="https://github.com/user-attachments/assets/c4cccd5c-47b1-4a24-9d12-32b850b645eb" />

### 2. Подсчёт количества мошеннических (is_fraud=1) и нормальных (is_fraud=0) транзакций, суммарной суммы и среднего чека
<code>select is_fraud,
&nbsp;&nbsp;count(1), 
&nbsp;&nbsp;sum(amount) as sum_amount, 
&nbsp;&nbsp;avg(amount) as avg_amount
from transactions_v2
group by is_fraud</code>

<img width="434" alt="image" src="https://github.com/user-attachments/assets/cacac264-4e83-46ad-bc12-812131067ee0" />

### 3. Группировка по датам с вычислением ежедневного количества транзакций, суммарного объёма и среднего amount
<code>select date(transaction_date), 
&nbsp;&nbsp;count(1),
&nbsp;&nbsp;sum(amount) as sum_amount, 
&nbsp;&nbsp;avg(amount) as avg_amount
from transactions_v2
group by date(transaction_date)</code>

<img width="456" alt="image" src="https://github.com/user-attachments/assets/fc1200c3-5d3e-4df4-8df5-eb56ee985d8a" />

### 4. Использование временных функций (например, извлечение дня/месяца из transaction_date) и анализ транзакций по временным интервалам
<code>select date_format(transaction_date, 'yyyy-MM-dd HH') hour_interval,
&nbsp;&nbsp;count(1) as count_by_hour
from transactions_v2
group by date_format(transaction_date, 'yyyy-MM-dd HH')
order by hour_interval</code>

<img width="562" alt="image" src="https://github.com/user-attachments/assets/276f1125-b679-4ab2-8fb6-aa1ad518ea2b" />

### 5. JOIN с таблицей logs_v2 по transaction_id, чтобы посчитать количество логов на одну транзакцию, выделить самые частые категории category и т.д
<code>select tr.transaction_id, count(1) as cnt
from transactions_v2 as tr
inner join logs_v2 as l
on tr.transaction_id = l.transaction_id
group by tr.transaction_id
order by cnt desc</code>

<img width="400" alt="image" src="https://github.com/user-attachments/assets/c3e17740-0d46-49ad-b617-d88897d512b5" />
