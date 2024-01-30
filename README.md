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

#### ОТВЕТ:
```sql
SELECT CONCAT(s.last_name, ' ', s.first_name) AS staff, c.city, COUNT(c2.store_id) AS custumers
FROM customer c2
INNER JOIN store s2 ON s2.store_id = c2.store_id
INNER JOIN staff s ON s.staff_id = s2.manager_staff_id 
INNER JOIN address a ON s.address_id = a.address_id
INNER JOIN city c ON c.city_id = a.city_id
GROUP BY c2.store_id
HAVING COUNT(c2.store_id) > 300;
```
---
### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

#### ОТВЕТ:
```sql
SELECT COUNT(f.title) 
FROM film f
WHERE f.`length` > (SELECT AVG(`length`) FROM film)
```
---
### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

#### ОТВЕТ:
```sql
SELECT MONTH(payment_date), SUM(p.amount), COUNT(p.rental_id) 
FROM payment p
GROUP BY MONTH(payment_date)
ORDER BY SUM(p.amount ) DESC
LIMIT 1;
```
---
