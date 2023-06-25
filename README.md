# 12.3-HW
### Домашнее задание к занятию 12.3 - "SQL. Часть 1" - Семкин Вячеслав
***
### Задание 1

Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

**Ответ:**
```
select district 
from address
where district like 'K%' and not district like '% %' and district like '%a';
```
***
### Задание 2

Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года **включительно** и стоимость которых превышает 10.00.

**Ответ:**
```
select *
from payment
where date(payment_date) between  '2005-06-15' and '2005-06-18';
```

***
### Задание 3

Получите последние пять аренд фильмов.

**Ответ:**

```
select *
from payment
order by payment_date desc
limit 5;
```

***
### Задание 4

Одним запросом получите активных покупателей, имена которых Kelly или Willie. 

Сформируйте вывод в результат таким образом:
- все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
- замените буквы 'll' в именах на 'pp'.

**Ответ:**

```
select replace(lower(first_name), 'll', 'pp')
from customer
where active = 1 and first_name = 'Kelly' or first_name = 'Willie';
```

***
### Задание 5*

Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.

**Ответ:**

```
select first_name, 
       last_name, 
       substr(email, 1, position('@' in email)-1) as email_1_часть, 
       substr(email, position('@' in email)+1) as email_2_часть
from customer;
```

***
### Задание 6*

Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.

**Ответ:**

```
select first_name, 
       last_name, 
       concat(upper(left(email ,1)),lower(substr(email,2, position('@' in email)-2))) as email_1_часть, 
       concat(upper(left(substr(email, position('@' in email)+1),1)),substr(email, position('@' in email)+2)) as email_2_часть
from customer;
```
