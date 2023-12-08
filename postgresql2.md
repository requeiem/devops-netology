# Домашнее задание к занятию 4. «PostgreSQL»

## Задача 1

Используя Docker, поднимите инстанс PostgreSQL (версию 13). Данные БД сохраните в volume.

Подключитесь к БД PostgreSQL, используя `psql`.

Воспользуйтесь командой `\?` для вывода подсказки по имеющимся в `psql` управляющим командам.

**Найдите и приведите** управляющие команды для:

- вывода списка БД,

\l[+]   [PATTERN]      list databases

- подключения к БД,

 \c[onnect] {[DBNAME|- USER|- HOST|- PORT|-] | conninfo}
                         connect to new database (currently "postgres")

- вывода списка таблиц,

\dt[S+] [PATTERN]      list tables

- вывода описания содержимого таблиц,

\d[S+]  NAME           describe table, view, sequence, or index

- выхода из psql.

\q                     quit psql

## Задача 2

Используя `psql`, создайте БД `test_database`.

Изучите [бэкап БД](https://github.com/netology-code/virt-homeworks/tree/virt-11/06-db-04-postgresql/test_data).

Восстановите бэкап БД в `test_database`.

Перейдите в управляющую консоль `psql` внутри контейнера.

Подключитесь к восстановленной БД и проведите операцию ANALYZE для сбора статистики по таблице.

Используя таблицу [pg_stats](https://postgrespro.ru/docs/postgresql/12/view-pg-stats), найдите столбец таблицы `orders` 
с наибольшим средним значением размера элементов в байтах.

**Приведите в ответе** команду, которую вы использовали для вычисления, и полученный результат.

![alt text](https://github.com/requeiem/devops-netology/blob/main/psql/psql2/Screenshot_1.jpg)

![alt text](https://github.com/requeiem/devops-netology/blob/main/psql/psql2/Screenshot_2.jpg)

![alt text](https://github.com/requeiem/devops-netology/blob/main/psql/psql2/Screenshot_3.jpg)

## Задача 3

Архитектор и администратор БД выяснили, что ваша таблица orders разрослась до невиданных размеров и
поиск по ней занимает долгое время. Вам как успешному выпускнику курсов DevOps в Нетологии предложили
провести разбиение таблицы на 2: шардировать на orders_1 - price>499 и orders_2 - price<=499.

Предложите SQL-транзакцию для проведения этой операции.

Можно ли было изначально исключить ручное разбиение при проектировании таблицы orders?

## Ответ: Да, на стадии создания таблицы можно было шардировать по партициям.
 
![alt text](https://github.com/requeiem/devops-netology/blob/main/psql/psql2/Screenshot_4.jpg)

## Задача 4

Используя утилиту `pg_dump`, создайте бекап БД `test_database`.

Как бы вы доработали бэкап-файл, чтобы добавить уникальность значения столбца `title` для таблиц `test_database`?

## Ответ: Использовал бы UNIQUE на столбце `title`. Ограничения уникальности гарантируют, что данные в определённом столбце или группе столбцов уникальны среди всех строк таблицы.

![alt text](https://github.com/requeiem/devops-netology/blob/main/psql/psql2/Screenshot_5.jpg)

---

### Как cдавать задание

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
