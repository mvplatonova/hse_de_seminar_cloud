### 1. Группировка по payment_status: подсчитываем количество заказов, сумму (total_amount), среднюю стоимость заказа
<code>SELECT payment_status, 
&nbsp;&nbsp;COUNT(1) AS cnt, 
&nbsp;&nbsp;SUM(total_amount) AS sum, 
&nbsp;&nbsp;AVG(total_amount) AS avg 
FROM orders 
GROUP BY payment_status</code>

<img width="724" alt="image" src="https://github.com/user-attachments/assets/e3ee6368-6023-4d7f-afbb-d8f94ad825b3" />

### 2. JOIN с order_items: подсчитать общее количество товаров, общую сумму, среднюю цену за продукт
<code>SELECT order_id, user_id, cnt_items, sum_items_price, avg_items_price 
FROM orders 
LEFT JOIN (
&nbsp;&nbsp;SELECT order_id, 
&nbsp;&nbsp;&nbsp;&nbsp;COUNT(1) AS cnt_items, 
&nbsp;&nbsp;&nbsp;&nbsp;SUM(product_price * quantity) AS sum_items_price, 
&nbsp;&nbsp;&nbsp;&nbsp;SUM(product_price * quantity) / SUM(quantity) AS avg_items_price 
&nbsp;&nbsp;FROM order_items 
&nbsp;&nbsp;GROUP BY order_id) grouped_items 
ON orders.order_id = grouped_items.order_id </code>

<img width="827" alt="image" src="https://github.com/user-attachments/assets/3d46d2a0-e4dd-444e-9a01-788f7b7f2673" />

### 3. Отдельно посмотреть статистику по датам (количество заказов и их суммарная стоимость за каждый день)
<code>SELECT date(order_date), 
&nbsp;&nbsp;COUNT(1) AS cnt, 
&nbsp;&nbsp;SUM(total_amount) AS sum 
FROM orders 
GROUP BY date(order_date)</code>

<img width="829" alt="image" src="https://github.com/user-attachments/assets/b2f2ea5f-8f03-4ba5-95e0-159e01a6b5d7" />

### 4. Выделить «самых активных» пользователей (по сумме заказов или по количеству заказов)
<code>SELECT user_id, 
&nbsp;&nbsp;SUM(total_amount) AS sum 
FROM orders 
GROUP BY user_id 
ORDER BY sum DESC 
LIMIT 10 </code>

<img width="825" alt="image" src="https://github.com/user-attachments/assets/0db7d266-f73c-44f4-b9b7-fb63dce9b000" />
