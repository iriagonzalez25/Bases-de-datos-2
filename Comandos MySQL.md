# Comandos MySQL 

A continuación vamos a ver una serie de comandos que permiten ver la estructura y datos de una base de datos en MySQL desde la terminal. 

#### Listar las bases de datos

Si queremos ver una lista de todas las bases de datos que tenemos, usaremos el comando `SHOW DATABASES;`. 

![Lista bases de datos]()

#### Utilizar una base de datos

Para conectarnos a una base de datos y trabajar sobre ella, usaremos `CONNECT nombreDB;` o `USE nombreDB;`. 

![CONNECT]()

![USE]()

#### Listar las tablas de una base de datos

Para ver una lista de las tablas de la base de datos en la que estamos, debemos poner `SHOW TABLES;`. 

![SHOW TABLES]()

#### Ver información de las tablas

Si lo que queremos es ver la información de las tablas de la base de datos, hay que usar `SHOW TABLE STATUS;`. 

![SHOW TABLE STATUS]()

#### Ver la estructura de una tabla

Para ver la estructura de una tabla en concreto, usaremos `DESCRIBE nombreTabla;` o `DESC nombreTabla`. El comando `SHOW COLUMNS FROM nombreTabla;` mostraría lo mismo. 

![DESCRIBE]()

![SHOW COLUMNS FROM]()

#### Ver la creación de una tabla 

También podemos ver cómo hemos creado una tabla utilizando `SHOW CREATE TABLE nombreTabla;`. 

![SHOW CREATE TABLE]()

