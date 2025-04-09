### 1.
<code>select currency, 
sum(amount) as currency_amount
from transactions_v2 
where currency in ('RUB', 'USD', 'EUR')
group by currency</code>

<img width="424" alt="image" src="https://github.com/user-attachments/assets/c4cccd5c-47b1-4a24-9d12-32b850b645eb" />

### 2. 
<code>select is_fraud, 
sum(amount) as sum_amount, 
avg(amount) as avg_amount
from transactions_v2
group by is_fraud</code>

<img width="392" alt="image" src="https://github.com/user-attachments/assets/5221d9be-9031-413d-83e5-5a06b3d931f3" />

### 3.
<code>select date(transaction_date), 
count(1),
sum(amount) as sum_amount, 
avg(amount) as avg_amount
from transactions_v2
group by date(transaction_date)</code>

<img width="456" alt="image" src="https://github.com/user-attachments/assets/fc1200c3-5d3e-4df4-8df5-eb56ee985d8a" />

### 4.
<code></code>

### 5. 
<code>select tr.transaction_id, count(1) as cnt
from transactions_v2 as tr
inner join logs_v2 as l
on tr.transaction_id = l.transaction_id
group by tr.transaction_id
order by cnt desc</code>

<img width="400" alt="image" src="https://github.com/user-attachments/assets/c3e17740-0d46-49ad-b617-d88897d512b5" />
