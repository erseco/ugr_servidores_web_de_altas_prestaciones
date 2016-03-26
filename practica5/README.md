#Practica 5: Replicación de bases de datos MySQL

##Tarea a realizar:

1. Crear una BD con al menos una tabla y algunos datos.
2. Realizar la copia de seguridad de la BD completa usando mysqldump.
3. Restaurar dicha copia en la segunda máquina (clonado manual de la BD).
4. Realizar la configuración maestro-esclavo de los servidores MySQL para que la replicación de datos se realice automáticamente.
5. Configuración maestro-maestro entre las dos máquinas de bases de datos.

-

Vamos a reutilizar una tabla de codigos postales de españa de otro proyecto, el archivo se llama **zipcodes.sql**

copiamos el archivo **zipcodes.sql** a **swap1**
```
bender:practica5 ernesto$ scp zipcodes.sql swap1:~/
```

Volcamos el archivo .sql a la  de la base de datos

```
ernesto@swap1:~$ mysql -u root -p < zipcodes.sql
```
Tip: Este dump ya crea la base de datos **swap** y la selecciona

Vemos que efectivamente en la base de datos **swap** tenemos la tabla **zipcodes**

```
mysql> SHOW TABLES;
+----------------+
| Tables_in_swap |
+----------------+
| zipcodes       |
+----------------+
1 row in set (0.00 sec)
```

Hacemos un dump de la base de datos

```
ernesto@swap1:~$ mysqldump -u root -p --single-transaction swap zipcodes > zipcodes.backup.sql
```
Tip: Para el bloqueo hemos usado **--single-transaction** porque estamos usando el motor InnoDB, si estuvieramos usando MyISAM usariamos el parametro **--lock-tables**, estos parametros son similares a usar ***FLUSH TABLES WITH READ LOCK***



Copiamos los archivos al servidor **swap2**
ernesto@swap1:~$ scp zipcodes.backup.sql swap2:~/zipcodes.backup.sql

Entramos al mysql de **swap2** para crear la base de datos **swap**

```
mysql -u root -p
mysql> CREATE DATABASE swap;
mysql -u root -p swap < zipcodes.backup.sql
```

Editamos el archivo de configuracion de mysql de **swap1** para desactivar/activar las lineas indicadas y reiniciar el demonio

```
ernesto@swap1:~$ sudo vim /etc/mysql/my.cnf

#bind-address 127.0.0.1
server-id               = 1
log_bin                 = /var/log/mysql/mysql-bin.log

ernesto@swap1:~$ sudo /etc/init.d/mysql restart
```

Garantizamos acceso al esclavo:

```
mysql> CREATE USER esclavo IDENTIFIED BY 'esclavo';
GRANT REPLICATION SLAVE ON *.* TO 'esclavo'@'%' IDENTIFIED BY 'esclavo';
FLUSH PRIVILEGES;
FLUSH TABLES;
FLUSH TABLES WITH READ LOCK;

mysql> SHOW MASTER STATUS;
+------------------+----------+--------------+------------------+
| File             | Position | Binlog_Do_DB | Binlog_Ignore_DB |
+------------------+----------+--------------+------------------+
| mysql-bin.000001 |      517 |              |                  |
+------------------+----------+--------------+------------------+
1 row in set (0.00 sec)
```

Ahora configuramos **swap2**, editamos el archivo de configuracion de mysql de **swap2**

```
ernesto@swap2:~$ sudo vim /etc/mysql/my.cnf
#bind-address 127.0.0.1
server-id               = 2
log_bin                 = /var/log/mysql/mysql-bin.log

ernesto@swap2:~$ sudo /etc/init.d/mysql restart

mysql> CHANGE MASTER TO MASTER_HOST='swap1', MASTER_USER='esclavo', MASTER_PASSWORD='esclavo', MASTER_LOG_FILE='mysql-bin.000001', MASTER_LOG_POS=517, MASTER_PORT=3306;
START SLAVE;

mysql> SHOW SLAVE STATUS\G
*************************** 1. row ***************************
               Slave_IO_State: Waiting for master to send event
                  Master_Host: swap1
                  Master_User: esclavo
                  Master_Port: 3306
                Connect_Retry: 60
              Master_Log_File: mysql-bin.000001
          Read_Master_Log_Pos: 517
               Relay_Log_File: mysqld-relay-bin.000002
                Relay_Log_Pos: 253
        Relay_Master_Log_File: mysql-bin.000001
             Slave_IO_Running: Yes
            Slave_SQL_Running: Yes
              Replicate_Do_DB:
          Replicate_Ignore_DB:
           Replicate_Do_Table:
       Replicate_Ignore_Table:
      Replicate_Wild_Do_Table:
  Replicate_Wild_Ignore_Table:
                   Last_Errno: 0
                   Last_Error:
                 Skip_Counter: 0
          Exec_Master_Log_Pos: 517
              Relay_Log_Space: 410
              Until_Condition: None
               Until_Log_File:
                Until_Log_Pos: 0
           Master_SSL_Allowed: No
           Master_SSL_CA_File:
           Master_SSL_CA_Path:
              Master_SSL_Cert:
            Master_SSL_Cipher:
               Master_SSL_Key:
        Seconds_Behind_Master: 0
Master_SSL_Verify_Server_Cert: No
                Last_IO_Errno: 0
                Last_IO_Error:
               Last_SQL_Errno: 0
               Last_SQL_Error:
  Replicate_Ignore_Server_Ids:
             Master_Server_Id: 1
1 row in set (0.00 sec)
```

Desbloqueamos las tablas y borramos unos cuantos registros en el master

```
mysql> UNLOCK TABLES;
Query OK, 0 rows affected (0.00 sec)

mysql> DELETE FROM zipcodes WHERE state != '01';
Query OK, 64033 rows affected (0.34 sec)
```

En el servidor slave hacemos un select y vemos que ya no hay codigos postales con un state diferente de '01'

```
mysql> SELECT * FROM zipcodes;
```


##Configuración mastro-maestro

Para realizar esta configuración solo tenemos que configurar otro maestro-esclavo pero invirtiendo **swap1** y **swap2**, es decir:

Crear el usuario en **swap2**

```
mysql> CREATE USER esclavo IDENTIFIED BY 'esclavo';
GRANT REPLICATION SLAVE ON *.* TO 'esclavo'@'%' IDENTIFIED BY 'esclavo';
FLUSH PRIVILEGES;
FLUSH TABLES;
FLUSH TABLES WITH READ LOCK;
```

Crear el esclavo en **swap1**

```
mysql> CHANGE MASTER TO MASTER_HOST='swap2', MASTER_USER='esclavo', MASTER_PASSWORD='esclavo', MASTER_LOG_FILE='mysql-bin.000001', MASTER_LOG_POS=517, MASTER_PORT=3306;
START SLAVE;
```


Borramos en **swap2** un registro y comprobamos que se borra tambien de **swap1**:

```
mysql> DELETE FROM zipcodes WHERE city LIKE '%ZURBANO%';
```