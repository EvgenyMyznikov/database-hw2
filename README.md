# Домашнее задание к занятию «Работа с данными (DDL/DML)» - Evgeny Myznikov

### Задание 1
1.1. Поднимите чистый инстанс MySQL версии 8.0+.

sudo dnf update
sudo dnf -y install https://dev.mysql.com/get/mysql80-community-release-fc38-1.noarch.rpm

Это запишет файл репозитория в /etc/yum.repos.d/mysql-community.repo
Проверяем: 

cat /etc/yum.repos.d/mysql-community.repo

После того, как мы добавили репозиторий и подтвердили его включение, приступаем к установке MySQL 8.0, выполнив:

sudo dnf install mysql-community-server

После установки информацию о пакете можно увидеть из:

rpm -qi mysql-community-server

Запускаем и включаем mysqld службу:

sudo systemctl start mysqld.service
sudo systemctl enable mysqld.service

Скопируем сгенерированный случайный пароль для пользователя root:

sudo grep 'A temporary password' /var/log/mysqld.log |tail -1

Запускаем безопасную установку MySQL, чтобы изменить пароль root, запретить удаленный вход в систему root, удалить анонимных пользователей и удалить тестовую базу данных(ответить на контрольные вопросы по своему усмотрению или просто сказать YES всем из них.):

sudo mysql_secure_installation

Подключитесь к базе данных MySQL как пользователь root и создайте базу данных:

sudo mysql -u root -p

1.2. Создайте учётную запись sys_temp.

CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY 'password';

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

![task1.3](https://github.com/EvgenyMyznikov/database-hw2/blob/main/img/task1.3.png?raw=true)

1.4. Дайте все права для пользователя sys_temp.

GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost';

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

show grants for 'sys_temp'@'localhost';

![task1.5.1](https://github.com/EvgenyMyznikov/database-hw2/blob/main/img/task1.5.1.png?raw=true)
![task1.5.2](https://github.com/EvgenyMyznikov/database-hw2/blob/main/img/task1.5.2.png?raw=true)

1.6. Переподключитесь к базе данных от имени sys_temp.

mysql -u sys_temp -p

1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.7. Восстановите дамп в базу данных.

![task1.7](https://github.com/EvgenyMyznikov/database-hw2/blob/main/img/task1.7.png?raw=true)

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

![task1.8.1](https://github.com/EvgenyMyznikov/database-hw2/blob/main/img/task1.8.1.png?raw=true)
![task1.8.2](https://github.com/EvgenyMyznikov/database-hw2/blob/main/img/task1.8.2.png?raw=true)

use sakila;
show tables;

Как посмотреть список таблиц и их структуру в MySQL:

SHOW DATABASES; - список баз данных
SHOW TABLES [FROM db_name]; -  список таблиц в базе 
SHOW COLUMNS FROM таблица [FROM db_name]; - список столбцов в таблице
SHOW CREATE TABLE table_name; - показать структуру таблицы в формате "CREATE TABLE"
SHOW INDEX FROM tbl_name; - список индексов
SHOW GRANTS FOR user [FROM db_name]; - привилегии для пользователя.


SHOW VARIABLES; - значения системных переменных
SHOW [FULL] PROCESSLIST; - статистика по mysqld процессам
SHOW STATUS; - общая статистика
SHOW TABLE STATUS [FROM db_name]; - статистика по всем таблицам в базе

*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*


### Задание 2
Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц.

![task2](https://github.com/EvgenyMyznikov/database-hw2/blob/main/img/task2.png?raw=true)