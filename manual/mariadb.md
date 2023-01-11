### MariaDB

#### Editar el fichero de configuracion .env y establece las variables
```
$ vi .env

MARIADB_PORT=3306
PHPMYADMIN_PORT=8001
```

#### Iniciar el servicio e ir al log para ver la clave asiganda
```
$ docker compose up -d
$ docker compose logs mariadb | grep "ROOT PASSWORD"

mariadb  | 2023-01-10 19:59:58+01:00 [Note] [Entrypoint]: GENERATED ROOT PASSWORD: mi_clave_auto_generada
```

### Crear usuarios

Desde el host y con la clave obtenida podemos usar cliente mysql para crear usuarios y base de datos
```
$ mysql -u root -p -h localhost -P 3306 --protocol=tcp

mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.00 sec)

SELECT Host,User FROM mysql.user;
mysql> SELECT Host,User FROM mysql.user;
+-----------+-------------+
| Host      | User        |
+-----------+-------------+
| %         | jose        |
| %         | root        |
| localhost | mariadb.sys |
+-----------+-------------+
3 rows in set (0.00 sec)


#crear usuario
CREATE USER 'user'@'%' IDENTIFIED BY 'password';

# darle privilegios de super-usuario
GRANT ALL PRIVILEGES ON *.* TO 'jose'@'%';

# mostra privilegios
SHOW GRANTS FOR 'jose';

# cambiar la clave de un usuario
ALTER USER 'user'@'localhost' IDENTIFIED BY 'new_password';

# eliminar usuario root
REVOKE ALL PRIVILEGES ON * . * FROM 'root'
DROP USER 'root'@'localhost';

# hacer efectivos los cambios de privilegios
FLUSH PRIVILEGES;


# crear base de datos
CREATE DATABASE nextcloud
# crear usuario para acceder solo a esta base de datos
CREATE USER 'nextcloud'@'%' IDENTIFIED BY 'password';
# darle privilegios a la base de datos
GRANT ALL PRIVILEGES ON nextcloud.* TO 'nextcloud'@'%';

```

si arrancamos el servico de phpMyAdmin, podemos abrir un navegador y gestionar usuarios y bases de datos facilmente
```
# http://mydomain:8001
```
