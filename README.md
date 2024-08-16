# Домашнее задание к занятию «Работа с данными (DDL/DML)»

---
## Ахмадеев Булат Наилевич

---

## Задание 1

1. Я поднял MySQL локально.

2. Создал учетную запись ```sys_temp```:

```
CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY 'password';
```

3. Выполнил запрос на получение списка пользователей:

```
SELECT user, host FROM mysql.user;
```

![alt text](<images/Снимок экрана 2024-08-16 в 03.30.43.png>)

4. Дал все права пользователю ```sys_temp```:

```
GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

5. Выполнил запрос на получение списка прав для пользователя ```sys_temp```:

```
SHOW GRANTS FOR 'sys_temp'@'localhost';
```

![alt text](<images/Снимок экрана 2024-08-16 в 03.34.22.png>)

```
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Grants for sys_temp@localhost                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, RELOAD, SHUTDOWN, PROCESS, FILE, REFERENCES, INDEX, ALTER, SHOW DATABASES, SUPER, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, REPLICATION SLAVE, REPLICATION CLIENT, CREATE VIEW, SHOW VIEW, CREATE ROUTINE, ALTER ROUTINE, CREATE USER, EVENT, TRIGGER, CREATE TABLESPACE, CREATE ROLE, DROP ROLE ON *.* TO `sys_temp`@`localhost` WITH GRANT OPTION                                                                                                                                                                                                                                                                                                                                                                                     |
| GRANT APPLICATION_PASSWORD_ADMIN,AUDIT_ABORT_EXEMPT,AUDIT_ADMIN,AUTHENTICATION_POLICY_ADMIN,BACKUP_ADMIN,BINLOG_ADMIN,BINLOG_ENCRYPTION_ADMIN,CLONE_ADMIN,CONNECTION_ADMIN,ENCRYPTION_KEY_ADMIN,FIREWALL_EXEMPT,FLUSH_OPTIMIZER_COSTS,FLUSH_STATUS,FLUSH_TABLES,FLUSH_USER_RESOURCES,GROUP_REPLICATION_ADMIN,GROUP_REPLICATION_STREAM,INNODB_REDO_LOG_ARCHIVE,INNODB_REDO_LOG_ENABLE,PASSWORDLESS_USER_ADMIN,PERSIST_RO_VARIABLES_ADMIN,REPLICATION_APPLIER,REPLICATION_SLAVE_ADMIN,RESOURCE_GROUP_ADMIN,RESOURCE_GROUP_USER,ROLE_ADMIN,SENSITIVE_VARIABLES_OBSERVER,SERVICE_CONNECTION_ADMIN,SESSION_VARIABLES_ADMIN,SET_USER_ID,SHOW_ROUTINE,SYSTEM_USER,SYSTEM_VARIABLES_ADMIN,TABLE_ENCRYPTION_ADMIN,TELEMETRY_LOG_ADMIN,XA_RECOVER_ADMIN ON *.* TO `sys_temp`@`localhost` WITH GRANT OPTION |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
2 rows in set (0,00 sec)
```

6. Переподключился к базе данных под пользователем ```sys_temp```:

```
mysql -u sys_temp -p
```

![alt text](<images/Снимок экрана 2024-08-16 в 03.36.21.png>)

7. Скачал и восстановил дамп базы данных ```sakila```:

```
mysql -u sys_temp -p < sakila-schema.sql
mysql -u sys_temp -p < sakila-data.sql
```

База появилась в MySQL:

![alt text](<images/Снимок экрана 2024-08-16 в 03.41.33.png>)

8. Создал ER-диаграммы и получил список таблиц:

ER-диаграмма:

![alt text](<images/Снимок экрана 2024-08-16 в 03.49.30.png>)

Список таблиц командой ```SHOW TABLES IN sakila;```:

![alt text](<images/Снимок экрана 2024-08-16 в 03.50.41.png>)

---

## Задание 2

Сначала я вывел список таблиц и их первичный ключ:

```
SELECT 
    table_name, 
    column_name AS primary_key
FROM 
    information_schema.key_column_usage
WHERE 
    table_schema = 'sakila' 
    AND constraint_name = 'PRIMARY';
```

![alt text](<images/Снимок экрана 2024-08-16 в 03.55.57.png>)

Текстовый документ:

[text](New_table.txt)

