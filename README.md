### Задание 1

Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

```
SELECT DISTINCT district FROM address WHERE district LIKE 'K%a' AND district NOT LIKE '% %';
```

<img width="304" alt="Снимок экрана 2023-10-21 в 19 48 23" src="https://github.com/otuzi/sqlpart1/assets/61628386/71c63f45-db60-4ca6-b456-45cff92439b5">


### Задание 2

Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года **включительно** и стоимость которых превышает 10.00.

```
SELECT amount, payment_date FROM payment WHERE amount > 10 AND payment_date BETWEEN '2005-06-15 00:00:00' AND '2005-06-18 23:59:59';
```

<img width="607" alt="Снимок экрана 2023-10-21 в 19 49 02" src="https://github.com/otuzi/sqlpart1/assets/61628386/7392483f-c8b6-4794-aa4a-546d66e9405f">


### Задание 3

Получите последние пять аренд фильмов.

```
SELECT rental_id, rental_date, last_update  FROM rental ORDER BY rental_date DESC, rental_id DESC LIMIT 5;
```

<img width="822" alt="Снимок экрана 2023-10-21 в 19 49 48" src="https://github.com/otuzi/sqlpart1/assets/61628386/43e1266a-8ddf-4dcb-aca7-febafdcddf14">


### Задание 4

Одним запросом получите активных покупателей, имена которых Kelly или Willie. 

Сформируйте вывод в результат таким образом:
- все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
- замените буквы 'll' в именах на 'pp'.

```
SELECT LOWER(first_name), LOWER(last_name), REPLACE(LOWER(first_name), 'll', 'pp')as ll_TO_pp FROM customer WHERE first_name LIKE 'Kelly' OR  first_name  LIKE 'Willie';
```

<img width="815" alt="Снимок экрана 2023-10-21 в 19 50 27" src="https://github.com/otuzi/sqlpart1/assets/61628386/ff6fed4c-7197-4efb-811e-d93cfca4e35a">


## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 5*

Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.

```
SELECT email, SUBSTRING_INDEX(email,'@',1) AS BEFORE_AT_SIGN, SUBSTR(email, INSTR(email, '@') + 1) AS AFTER_AT_SIGN FROM customer;
```
<img width="821" alt="Снимок экрана 2023-10-21 в 19 51 17" src="https://github.com/otuzi/sqlpart1/assets/61628386/98e7df74-c0b0-41b3-ae94-559d3c4abcd5">


### Задание 6*

Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.

```
SELECT email, CONCAT(UPPER(LEFT(SUBSTRING_INDEX(email,'@',1),1)), LCASE(SUBSTRING(SUBSTRING_INDEX(email,'@',1), 2))) AS BEFORE_AT_SIGN, CONCAT(UPPER(LEFT(SUBSTR(email, INSTR(email, '@') + 1),1)), LCASE(SUBSTRING(SUBSTR(email, INSTR(email, '@') + 1), 2))) AS AFTER_AT_SIGN FROM customer;
```

<img width="813" alt="Снимок экрана 2023-10-21 в 19 51 46" src="https://github.com/otuzi/sqlpart1/assets/61628386/25bf759c-845f-427b-b261-5ac4db47d00e">
