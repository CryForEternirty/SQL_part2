# Домашнее задание к занятию «SQL. Часть 2»

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

### Решение:

```
SELECT c.store_id AS "Store_ID", count(c.customer_id) AS "Clients_count", CONCAT(s2.first_name, ' ',s2.last_name) AS "FI", c2.city as "Store's_city"  
FROM customer c  
JOIN store s ON c.store_id = s.store_id   
JOIN staff s2 ON s.manager_staff_id = s2.staff_id   
JOIN address a ON s.address_id = a.address_id   
JOIN city c2 ON a.city_id = c2.city_id  
GROUP BY c.store_id  
HAVING count(c.customer_id) > 300;
```
![answer1](image-1.png)

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

### Решение:
```
SELECT count(f.film_id)
from film f 
where f.`length` > (select avg(f2.`length`) from film f2);
```
![answer2](image-1.png)

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

### Решение:
```
SELECT DATE_FORMAT(p.payment_date, "%m") as mon, sum(p.amount) as summ, count(p.rental_id) as kol_arend
from payment p 
group by mon
ORDER BY summ DESC limit 1;
```
![answer3](image-2.png)
