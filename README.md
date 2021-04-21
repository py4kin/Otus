<a id="contents"></a>
# Otus
[Домашнее задание №1 (Проектирование БД)](#1)

[Домашнее задание №2 (Компоненты современной СУБД)](#2)

[Домашнее задание №6 (Внутренняя архитектура СУБД PostgreSQL)](#6)

[Домашнее задание №7 (DDL: создание, изменение и удаление объектов в PostgreSQL)](#7)
<a id="1">
## Домашнее задание №1 (Проектирование БД)
### 1. Схема <br>		
<p style="margin-left: 20px">
	Понимаю что хорошим тоном является использовать латиские слова, буквы, обозначения, но это моя первая практика по этому сделано так (в будущем буду переделывать).
	Схему накидал в dbforgestudio, он почему требует подключение к БД. 
	БД у меня старая MySQL, не поддерживаются внешние ключи.</p>

![Схема](1.png)

### 2. Документация
*Не разобрался я как делать документация "простую" через ПО, поэтому сделал так))))*
 * ***Таблица "Клиенты"*** <br>
	В данную таблицу заносится информация о клиенте. Столбец ID - Первычный ключ.
	Таблица связанна с таблицей "Договоренность работ" по "Номер клиента"(client_id - внешний ключ) и с таблицей "Выполненые работы(чек) по "Номер клиента"(client_id).
 * ***Таблица "Договоренность работ"*** <br>
	В данной таблице содержится информация о дате обращения клиента, описание проблемы, согласование выезда спецаилиста. Столбец ID - Первычный ключ. Столбец "Номер клиента" client_id - внешний ключ.
	Связана с таблице "Клиенты" по Id.
 * ***Таблица "Выполненые работы(чек)"***<br>
	Таблица о выполненой работы специалистом. Предполагается что из данной таблице можно формировать "чек". Столбец ID - Первычный ключ. Столбец "Номер клиента" (client_id)и столбец "Тип обозначения" - внешние ключи.
	Связан с таблицей "Клиенты" по Id и с таблицей "Запчасти" по "Тип оборудование".
 * ***Таблица "Поставщики"***<br>
	В данную таблицу заносится информация о поставщикке запчастей. Столбец ID - Первычный ключ.
	Таблица связанна с таблицей "Запчасти" по "Номер_поставщика"(supplier_id).
 * ***Таблица "Запчасти"***<br>
	В данной таблице содержится описание запчастей, дата поставки, цена за штуку, тип. Столбец ID и "Тип оборудования" - Первычные ключи. Столбец "Номер_поставщика" - внешний ключ.
	Таблица связанна с таблицей "Поставщики" по Id и с таблицей "Выполненые работы(чек)" по "Тип оборудование".
 
### 3. Примеры бизнес-задач которые решает база.
<p style="margin-left: 20px">Есть не большой город и близ лежашие деревни. В данном районе осуществляется ремонт, покупка и продажа Стиральных машин и Холодильного оборудования.
	Данный проект (БД) осуществляет сбор, хранения и обработку инфорции о проделанной, текущей и будущей работы.
	Позвонили "нам" рассказыли что сломалось, где сломалось. Договариваемся о дате выезда специалиста для ремонта, продажи, покупки оборудования.
	БД должна уметь хранить и выводить в читабельной форме информация о работах для предоставления тем или иным лицам.</p>

### 4. Рекомендации к использованию репликации.
___Пока что не могу дать ответа.___ <br>
<p style="margin-left: 20px">Для данного объема работ думаю репликация будет излишней.
Я понимаю что такое репликация и как отличаются, но не могу сообразить как и какую применить для данного проекта.
### 5. Рекомендации к резервному копированию.
___Пока что не могу дать ответа.___
</a>

[Оглавление](#contents)
<a id="2">
## Домашнее задание №2 (Компоненты современной СУБД)
</a>

[Оглавление](#contents)
<a id="6">
## Домашнее задание №6 (Внутренняя архитектура СУБД PostgreSQL)
<p style="margin-left: 20px">

Сервер PostgreSQL был установлен на Windows.<br>
Созданы:
1.	Новый сервер (postgres13)
2.	БД "New","db"
3.	Пользователь "py4kin" с ограниченными правами. (Фамилия моя Ручкин, поэтому py4kin))))<br>
### 1. SQL Shell (Командная строка) <br>
![Схема](SQLShell_6.png)

На первом скриншоте подключение к серверу у базе данных "db" через пользователя "py4kin".<br>
P.s. Кодировку не менял.

### 2. pgAdmin <br>
![Схема](pgAdmin_6.png)<br>

На втором скриншоте подключение к серверу через pgAdmin.
</a>

[Оглавление](#contents)
<a id="7">
## Домашнее задание №7 (DDL: создание, изменение и удаление объектов в PostgreSQL)
1.	Создана БД - "Otus"

>DROP DATABASE otus;<br>
CREATE DATABASE otus<br>
    WITH <br>
    OWNER = py4kin<br>
    ENCODING = 'UTF8'<br>
    LC_COLLATE = 'Russian_Russia.1251'<br>
    LC_CTYPE = 'Russian_Russia.1251'<br>
    TABLESPACE = for_otus<br>
    CONNECTION LIMIT = -1;

2. Табличное пространство - "for_otus"

>DROP TABLESPACE for_otus;<br>
CREATE TABLESPACE for_otus<br>
  OWNER py4kin<br>
  LOCATION 'C:\Program Files\PostgreSQL\12\data';<br>
  
>ALTER TABLESPACE for_otus<br>
OWNER TO py4kin;<br>
		
3. Роль/пользователь - "py4kin"

>DROP ROLE py4kin;<br>
CREATE ROLE py4kin WITH<br>
  LOGIN<br>
  SUPERUSER<br>
  INHERIT<br>
  CREATEDB<br>
  CREATEROLE<br>
  REPLICATION<br>
  ENCRYPTED PASSWORD 'md5ab55bbce6782540fbdc80f2301ef24fd';<br>

>GRANT new_role TO py4kin;<br>
GRANT pg_monitor TO py4kin WITH ADMIN OPTION<br>


4. Схема данных - "for_otus"

>DROP SCHEMA for_otus ;<br>
CREATE SCHEMA for_otus<br>
    AUTHORIZATION py4kin;


5. Таблицы из домашнего задания №1

>DROP TABLE for_otus.clients;<br>
CREATE TABLE for_otus.clients<br>
(<br>
    "ID" integer[] NOT NULL,<br>
    "Name" "char" NOT NULL,<br>
    phone_number "char" NOT NULL,<br>
    address "char" NOT NULL,<br>
    CONSTRAINT clients_pkey PRIMARY KEY ("ID")<br>
        USING INDEX TABLESPACE for_otus<br>
)<br>
TABLESPACE for_otus;<br>
ALTER TABLE for_otus.clients<br>
OWNER to py4kin;
	
>DROP TABLE for_otus.completed_work;<br>
CREATE TABLE for_otus.completed_work<br>
(<br>
    id integer NOT NULL,<br>
    id_clients integer NOT NULL,<br>
    id_works integer NOT NULL,<br>
    works text COLLATE pg_catalog."default" NOT NULL,<br>
    date_works timestamp with time zone NOT NULL,<br>
    "Type_of_equipment" "char" NOT NULL,<br>
    price_part character(1) COLLATE pg_catalog."default" NOT NULL,<br>
    price_works character(1) COLLATE pg_catalog."default" NOT NULL,<br>
    total_price character(1) COLLATE pg_catalog."default" NOT NULL,<br>
    CONSTRAINT completed_work_pkey PRIMARY KEY (id)<br>
        USING INDEX TABLESPACE for_otus<br>
)<br>
TABLESPACE for_otus;<br>
ALTER TABLE for_otus.completed_work<br>
    OWNER to py4kin;
	
>DROP TABLE for_otus.contracted_works;<br>
CREATE TABLE for_otus.contracted_works<br>
(<br>
    id integer NOT NULL,<br>
    id_clients integer NOT NULL,<br>
    insertdate timestamp with time zone NOT NULL,<br>
    breaking text COLLATE pg_catalog."default" NOT NULL,<br>
    "Type_of_equipment" "char" NOT NULL,<br>
    " departure" timestamp with time zone NOT NULL,<br>
    CONSTRAINT "Contracted_works_pkey" PRIMARY KEY (id)<br>
        USING INDEX TABLESPACE for_otus<br>
)<br>
TABLESPACE for_otus;<br>
ALTER TABLE for_otus.contracted_works<br>
    OWNER to py4kin;
	
>DROP TABLE for_otus.parts;<br>
CREATE TABLE for_otus.parts<br>
(<br>
    id integer NOT NULL,<br>
    type_of_equipment "char" NOT NULL,<br>
    id_vendor integer NOT NULL,<br>
    manufacturer "char" NOT NULL,<br>
    name "char" NOT NULL,<br>
    qty integer NOT NULL,<br>
    price_thing "char" NOT NULL,<br>
    total_price "char" NOT NULL,<br>
    date_supply timestamp with time zone NOT NULL,<br>
    CONSTRAINT parts_pkey PRIMARY KEY (id)<br>
        USING INDEX TABLESPACE for_otus<br>
)<br>
TABLESPACE for_otus;<br>
ALTER TABLE for_otus.parts<br>
    OWNER to py4kin;
	
>DROP TABLE for_otus.provider;<br>
CREATE TABLE for_otus.provider<br>
(<br>
    id integer NOT NULL,<br>
    name "char" NOT NULL,<br>
    phone_number "char" NOT NULL,<br>
    address "char" NOT NULL,<br>
    CONSTRAINT provider_pkey PRIMARY KEY (id)<br>
        USING INDEX TABLESPACE for_otus<br>
)<br>
TABLESPACE for_otus;<br>
ALTER TABLE for_otus.provider<br>
    OWNER to py4kin;<br>

*Скриншоты выполненой работы.*

![Схема](db_role_tableplace.png)

![Схема](schemas_tables.png)

![Схема](tables.png)

</a>

[Оглавление](#contents)
