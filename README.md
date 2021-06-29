<a id="contents"></a>
# MySQL_Otus
[Домашнее задание №1 (Создаем базу данных в докере) ](#1)

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
