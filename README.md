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
В запросе происходит преобразование payment_date с datetime в date, что требует времени и приводит к невозможности использования индексов. 
Поменял запрос на вариант с between без преобразования, добавил индексы для payment_date и rental_date. Это привело снижение времени обработки запроса до 5,513 ms`

```
select distinct concat(c.last_name, ' ', c.first_name), sum(p.amount) over (partition by c.customer_id)
from payment p, rental r, customer c, inventory i
where p.payment_date between  '2005-07-30 00:00:00' and '2005-07-30 23:59:59' and p.payment_date = r.rental_date and r.customer_id = c.customer_id and i.inventory_id = r.inventory_id
```


![task_2_1.png](img%2Ftask_2_1.png)

---

![task_2_3.png](img%2Ftask_2_3.png)


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