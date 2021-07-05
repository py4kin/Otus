<a id="contents"></a>
# MySQL_Otus
[Домашнее задание №1 (Создаем базу данных в докере) ](#1)

[Домашнее задание №2 (Типы данных) ](#2)

<a id="1">

## Домашнее задание №1 (Создаем базу данных в докере).

1. Поднять сервер, файл docker-compose.yml приложил:

>docker-compose up

2. Файл init.sql приложил.

3. Сервер запускается.

>docker@default:~$ ps -e | grep my <br>
 2468 ?        00:00:12 mysqld

>docker@default:~$ docker ps <br>
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                    PORTS                                     NAMES<br>
668ae6a75830        1504607f1ce7        "/entrypoint.sh --in…"   5 days ago          Up 30 minutes (healthy)   33060-33061/tcp, 0.0.0.0:3308->3306/tcp   mysql

4. Подключение с помощью Workbench

![Схема](Workbench.png)

5. Файл my.cnf приложил

6. Sysbench.

InnoDB:

>SQL statistics:<br>
    queries performed:<br>
        read:                            10416<br>
        write:                           2974<br>
        other:                           1487<br>
        total:                           14877<br>
    transactions:                        743    (70.45 per sec.)<br>
    queries:                             14877  (1410.65 per sec.)<br>
    ignored errors:                      1      (0.09 per sec.)<br>
    reconnects:                          0      (0.00 per sec.)<br>

>General statistics:<br>
    total time:                          10.5430s<br>
    total number of events:              743<br>

>Latency (ms):<br>
         min:                                  312.97<br>
         avg:                                  890.60<br>
         max:                                 2226.10<br>
         95th percentile:                     1213.57<br>
         sum:                               661715.47<br>

>Threads fairness:<br>
    events (avg/stddev):           11.6094/0.80<br>
    execution time (avg/stddev):   10.3393/0.14<br>
	
MyiSAM:

>SQL statistics:<br>
    queries performed:<br>
        read:                            15302<br>
        write:                           2065<br>
        other:                           4493<br>
        total:                           21860<br>
    transactions:                        1093   (109.21 per sec.)<br>
    queries:                             21860  (2184.11 per sec.)<br>
    ignored errors:                      0      (0.00 per sec.)<br>
    reconnects:                          0      (0.00 per sec.)<br>

>General statistics:<br>
    total time:                          10.0056s<br>
    total number of events:              1093<br>

>Latency (ms):<br>
         min:                                    5.23<br>
         avg:                                    9.14<br>
         max:                                   33.61<br>
         95th percentile:                       13.22<br>
         sum:                                 9986.88<br>

>Threads fairness:<br>
    events (avg/stddev):           1093.0000/0.00<br>
    execution time (avg/stddev):   9.9869/0.00<br>	
</a>

[Оглавление](#contents)

<a id="2">

## Домашнее задание №2 (Типы данных).

>DROP TABLE otus.clients;<br>
CREATE TABLE otus.clients <br>
(<br>
  id INT UNSIGNED NOT NULL AUTO_INCREMENT, -- чтобы не было отрицательных значений. AUTO_INCREMENT автозаполнение.<br>
  name VARCHAR(40) NOT NULL, -- нефиксированная длинна<br>
  phone_number VARCHAR(20) NOT NULL,<br>
  address VARCHAR(255) NOT NULL,<br>
  PRIMARY KEY (id)<br>
)<br>
ENGINE = InnoDB<br>
CHARACTER SET utf8mb4<br>
COLLATE 'utf8mb4_0900_ai_ci';<br>


>DROP TABLE otus.completed_work;<br>
CREATE TABLE otus.completed_work<br>
(<br>
    id INT UNSIGNED NOT NULL AUTO_INCREMENT,<br>
    id_clients INT UNSIGNED NOT NULL, -- UNSIGNED чтобы не попало отрицательное значение<br>
    id_works INT UNSIGNED NOT NULL,<br>
    works VARCHAR(255) NOT NULL, -- краткое описание выполненой работы<br>
    date_works TIMESTAMP NOT NULL, -- учитывает часовой пояс<br>
    type_of_equipment CHAR(17) NOT NULL, -- либо стиральная холодильник, либо стиральная машина, возможно это поле вообще стоит убрать т.к. есть таблица vocabulary_1<br>
    price_part DECIMAL  NOT NULL,<br>
    price_works DECIMAL   NOT NULL,<br>
    total_price DECIMAL  NOT NULL,<br>
	PRIMARY KEY (id)<br>
)<br>
ENGINE = InnoDB<br>
CHARACTER SET utf8mb4<br>
COLLATE 'utf8mb4_0900_ai_ci';<br>

>DROP TABLE otus.contracted_works;<br>
CREATE TABLE otus.contracted_works<br>
(<br>
    id INT UNSIGNED NOT NULL AUTO_INCREMENT, -- UNSIGNED чтобы не попало отрицательное значение<br>
    id_clients INT UNSIGNED NOT NULL, -- UNSIGNED чтобы не попало отрицательное значение<br>
    insertdate TIMESTAMP NOT NULL,<br>
    breaking VARCHAR(255) NOT NULL, -- краткое описание поломки со слов заказчика<br>
    type_of_equipment CHAR(17) NOT NULL, -- либо стиральная холодильник, либо стиральная машина, возможно это поле вообще стоит убрать т.к. есть таблица vocabulary_1<br>
    departure TIMESTAMP NOT NULL,<br>
	PRIMARY KEY (id)<br>
)<br>
ENGINE = InnoDB<br>
CHARACTER SET utf8mb4<br>
COLLATE 'utf8mb4_0900_ai_ci';<br>

>DROP TABLE otus.parts;<br>
CREATE TABLE otus.parts<br>
(<br>
    id INT UNSIGNED NOT NULL AUTO_INCREMENT,<br>
    type_of_equipment CHAR(17) NOT NULL, -- либо стиральная холодильник, либо стиральная машина, возможно это поле вообще стоит убрать т.к. есть таблица vocabulary_1<br>
    id_vendor INT UNSIGNED NOT NULL, -- поставщик<br>
    manufacturer VARCHAR(10) NOT NULL, -- фирма/производитель<br>
    name VARCHAR(20) NOT NULL, -- название запчасти<br>
    qty INT NOT NULL, -- кол-во в шт<br>
    price_thing DECIMAL NOT NULL,<br>
    total_price DECIMAL NOT NULL,<br>
    date_supply TIMESTAMP NOT NULL,<br>
    PRIMARY KEY (id)<br>
)<br>
ENGINE = InnoDB<br>
CHARACTER SET utf8mb4<br>
COLLATE 'utf8mb4_0900_ai_ci';<br>

>DROP TABLE otus.provider;<br>
CREATE TABLE otus.provider<br>
(<br>
    id INT UNSIGNED NOT NULL AUTO_INCREMENT,<br>
    name VARCHAR(20) NOT NULL,<br>
    phone_number VARCHAR(20) NOT NULL,<br>
    address VARCHAR(255) NOT NULL,<br>
    PRIMARY KEY (id)<br>
)<br>
ENGINE = InnoDB<br>
CHARACTER SET utf8mb4<br>
COLLATE 'utf8mb4_0900_ai_ci';<br>

>DROP TABLE otus.vocabulary_1;<br>
CREATE TABLE otus.vocabulary_1<br>
(<br>
	id INT UNSIGNED NOT NULL AUTO_INCREMENT,<br>
	name CHAR(17) NOT NULL,<br>
	PRIMARY KEY (id)<br>
)<br>
ENGINE = InnoDB<br>
CHARACTER SET utf8mb4<br>
COLLATE 'utf8mb4_0900_ai_ci';<br>

1. Для всех id сделал INT UNSIGNED NOT NULL AUTO_INCREMENT.
2. Время сделал в TIMESTAMP.
3. Для денежных сумм сделал DECIMAL.
4. Номера телефонов сделал VARCHAR.
5. Практически во всех таблицах есть строка type_of_equipment тип даннх сделал CHAR(17), т.к. тут должны хранится только два значения.
Может эту строчку вообще убрать и связать с таблицей vocabulary_1, т.к. эта табилца содержит эти же самые значения?
6. Везде где исползую Int и не хочу иметь отрицательные значения, целессообразно использовать UNSIGNED?

JSON:<br>
1.Создал новую таблицу в которой содержится описание конечного оборудования (Холодильников).

>CREATE TABLE equipment<br>
(<br>
    id INT UNSIGNED NOT NULL AUTO_INCREMENT,<br>
    name JSON NOT NULL,<br>
    PRIMARY KEY (id)<br>
)<br>
ENGINE = InnoDB<br>
CHARACTER SET utf8mb4<br>
COLLATE 'utf8mb4_0900_ai_ci';<br>

2. Заполнил данными: название ,цвет, размер:
Варииант №1
>insert into otus.equipment (name)<br>
values ('{"name":"Айсберг","color":"white","size":"6.11 x 3.59 x 0.46 cm"}');

Варииант №2
>insert into otus.equipment (name)<br>
values ( <br>
JSON_OBJECT (<br>
"Холодильник",<br>
JSON_ARRAY ("LG","sumsung","Sony"),<br>
"color","white",<br>
"size","6.11 x 3.59 x 0.46 cm"));<br>

Выборка:

![Схема](json.png)
</a>

[Оглавление](#contents)
