# Домашнее задание к занятию «SQL. Часть 2»

<details> 
  
### Инструкция по выполнению домашнего задания

1. Сделайте fork [репозитория c шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование этого репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и ваши фамилию и имя;
   - в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
   - для корректного добавления скриншотов воспользуйтесь инструкцией [«Как вставить скриншот в шаблон с решением»](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
   - при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в [инструкции по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`).
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.

Желаем успехов в выполнении домашнего задания.

</details> 
  
---

Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

### *Ответ*

<details> 

```
select concat(sotr.first_name , ' ', sotr.last_name) as сотрудник,  c2.city as город, COUNT(c.customer_id) as "покупатели"
from staff sotr
join store s2 on s2.store_id = sotr.store_id 
join customer c on c.store_id = s2.store_id
join address a on a.address_id = s2.address_id 
join city c2 on c2.city_id = a.city_id 
group by sotr.staff_id, c2.city_id 
having COUNT(c.customer_id) > 300;
```

![image](https://github.com/Ivashka80/12-03_SQL_Part_2/assets/121082757/0c2b1b20-c89e-4c55-a092-9c8e9239b66d)

</details> 

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

### *Ответ*

<details> 

```
select count(film_id) as "кол-во фильмов" from film 
where length > (select AVG(length) from film);
```

![image](https://github.com/Ivashka80/12-03_SQL_Part_2/assets/121082757/e6c346b0-5948-45cc-9b4d-03a2a1806ba1)

</details> 

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

### *Ответ*

<details> 

```
select month(payment_date) as месяц, SUM(p.amount) "сумма платежей", COUNT(p.rental_id) "кол-во аренд" 
from payment p
group by MONTH(payment_date)
order by SUM(p.amount ) 
desc limit 1;
```

![image](https://github.com/Ivashka80/12-03_SQL_Part_2/assets/121082757/cc591c01-c056-49ee-917e-5199505c76db)

</details> 

---

<details> 

## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 4*

Посчитайте количество продаж, выполненных каждым продавцом. Добавьте вычисляемую колонку «Премия». Если количество продаж превышает 8000, то значение в колонке будет «Да», иначе должно быть значение «Нет».

### Задание 5*

Найдите фильмы, которые ни разу не брали в аренду.

</details> 
