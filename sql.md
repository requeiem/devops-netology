# Домашнее задание к занятию 2. «SQL»

## Введение

Перед выполнением задания вы можете ознакомиться с 
[дополнительными материалами](https://github.com/netology-code/virt-homeworks/blob/virt-11/additional/README.md).

## Задача 1

Используя Docker, поднимите инстанс PostgreSQL (версию 12) c 2 volume, 
в который будут складываться данные БД и бэкапы.

Приведите получившуюся команду или docker-compose-манифест.

![alt text](https://github.com/requeiem/devops-netology/blob/main/psql/images/8.jpg)

## docker-compose-манифест
version: '3.5'

services:
  postgres:
    container_name: postgres_container
    image: postgres:12-bullseye
    environment:
      POSTGRES_USER: ${POSTGRES_USER:-postgres}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD:-changeme}
      PGDATA: /var/lib/posgresql/data
    volumes:
       - postgres:/var/lib/posgresql/data
       - postgres_backup:/backup
    networks:
      - postgres
    restart: unless-stopped

networks:
  postgres:
    driver: bridge

volumes:
    postgres:
    postgres_backup:

## Задача 2

В БД из задачи 1: 

- создайте пользователя test-admin-user и БД test_db;
- в БД test_db создайте таблицу orders и clients (спeцификация таблиц ниже);
- предоставьте привилегии на все операции пользователю test-admin-user на таблицы БД test_db;
- создайте пользователя test-simple-user;
- предоставьте пользователю test-simple-user права на SELECT/INSERT/UPDATE/DELETE этих таблиц БД test_db.


Таблица orders:

- id (serial primary key);
- наименование (string);
- цена (integer).

Таблица clients:

- id (serial primary key);
- фамилия (string);
- страна проживания (string, index);
- заказ (foreign key orders).

Приведите:

- итоговый список БД после выполнения пунктов выше;

![alt text](https://github.com/requeiem/devops-netology/blob/main/psql/images/1.jpg)

- описание таблиц (describe);

![alt text](https://github.com/requeiem/devops-netology/blob/main/psql/images/2.jpg)

- SQL-запрос для выдачи списка пользователей с правами над таблицами test_db;
- список пользователей с правами над таблицами test_db.

![alt text](https://github.com/requeiem/devops-netology/blob/main/psql/images/3.jpg)

## Задача 3

Используя SQL-синтаксис, наполните таблицы следующими тестовыми данными:

Таблица orders

|Наименование|цена|
|------------|----|
|Шоколад| 10 |
|Принтер| 3000 |
|Книга| 500 |
|Монитор| 7000|
|Гитара| 4000|

Таблица clients

|ФИО|Страна проживания|
|------------|----|
|Иванов Иван Иванович| USA |
|Петров Петр Петрович| Canada |
|Иоганн Себастьян Бах| Japan |
|Ронни Джеймс Дио| Russia|
|Ritchie Blackmore| Russia|

Используя SQL-синтаксис:
- вычислите количество записей для каждой таблицы.

Приведите в ответе:

    - запросы,
    - результаты их выполнения.

![alt text](https://github.com/requeiem/devops-netology/blob/main/psql/images/4.jpg)

![alt text](https://github.com/requeiem/devops-netology/blob/main/psql/images/5.jpg)

## Задача 4

Часть пользователей из таблицы clients решили оформить заказы из таблицы orders.

Используя foreign keys, свяжите записи из таблиц, согласно таблице:

|ФИО|Заказ|
|------------|----|
|Иванов Иван Иванович| Книга |
|Петров Петр Петрович| Монитор |
|Иоганн Себастьян Бах| Гитара |

Приведите SQL-запросы для выполнения этих операций.

Приведите SQL-запрос для выдачи всех пользователей, которые совершили заказ, а также вывод этого запроса.
 
Подсказка: используйте директиву `UPDATE`.

![alt text](https://github.com/requeiem/devops-netology/blob/main/psql/images/6.jpg)

## Задача 5

Получите полную информацию по выполнению запроса выдачи всех пользователей из задачи 4 
(используя директиву EXPLAIN).

Приведите получившийся результат и объясните, что значат полученные значения.

![alt text](https://github.com/requeiem/devops-netology/blob/main/psql/images/7.jpg)

- Так как условие WHERE был применен как "фильтр" у узлу плана Sed Scan (последовательное сканирование), это означает что узел плана проверяет условие для 
каждого просканированного им узла и выводит только те строки которые удовлетворяют ему. Условие WHERE повлияло на итоговый результат вывода запроса.
Приблизительная стоимость  на выполнение запроса равно 13.15 , а приблизительная стоимость запуска равна 0. Запланированое время выполнение запроса
равно 0.077 ms, а время выполнения самого запроса равно 0.040 ms. Ожидаемое число строк, которое должен вывести этот узел плана = 348 (rows), а ожидаемый
средний размер строк = 204 byte (width).

## Задача 6

Создайте бэкап БД test_db и поместите его в volume, предназначенный для бэкапов (см. задачу 1).

![alt text](https://github.com/requeiem/devops-netology/blob/main/psql/images/9.jpg)

Остановите контейнер с PostgreSQL, но не удаляйте volumes.

![alt text](https://github.com/requeiem/devops-netology/blob/main/psql/images/10.jpg)

Поднимите новый пустой контейнер с PostgreSQL.

![alt text](https://github.com/requeiem/devops-netology/blob/main/psql/images/11.jpg)

Восстановите БД test_db в новом контейнере.

![alt text](https://github.com/requeiem/devops-netology/blob/main/psql/images/12.jpg)

![alt text](https://github.com/requeiem/devops-netology/blob/main/psql/images/13.jpg)

![alt text](https://github.com/requeiem/devops-netology/blob/main/psql/images/14.jpg)

Приведите список операций, который вы применяли для бэкапа данных и восстановления. 

---

### Как cдавать задание

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
