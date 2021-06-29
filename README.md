<a id="contents"></a>
# MySQL_Otus
[Домашнее задание №1 (Создаем базу данных в докере) ](#1)

<a id="1">

## Домашнее задание №1 (Создаем базу данных в докере).

1. Поднять сервер:

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

</a>

[Оглавление](#contents)
