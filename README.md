# Домашнее задание к занятию "`Индексы`" - `Никулин Михаил Сергеевич`



---

### Задание 1

 

```
select sum(t.INDEX_LENGTH) /  sum(t.DATA_LENGTH) *100 as 'Отношение'  
from information_schema.TABLES t 
```

![task_1.png](img%2Ftask_1.png)


---

### Задание 2

`При проверке исполнения запроса выяснилось, что наибольшее время теряется на определении оконной функции. В данном запросе
нет необходимости использовать таблицу film и вычленять из нее данные по столбцу f.title, т.к. это не дает никакой дополнительной информации для запроса. 
Удаление данной таблицы привело к снижению времени запроса с 4523,745 ms до 9,861 ms, при тех же результатах. 
Так же была попытка добавить индекс на столбец payment_date таблицы payment, по которому происходит фильтрация, это привело к увеличению времени отработки запроса в 7 раз до 64.001 ms`


![task_2_1.png](img%2Ftask_2_1.png)
![task_2_2.png](img%2Ftask_2_2.png)

```
explain analyze
select distinct concat(c.last_name, ' ', c.first_name), sum(p.amount) over (partition by c.customer_id)
from payment p, rental r, customer c, inventory i
where date(p.payment_date) = '2005-07-30' and p.payment_date = r.rental_date and r.customer_id = c.customer_id and i.inventory_id = r.inventory_id
```

![task_2.png](img%2Ftask_2.png)



---
## Дополнительные задания (со звездочкой*)


### Задание 3*


![task_3.png](img%2Ftask_3.png)