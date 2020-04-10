# Comandos MySQL 
## es que no sé si para la tarea 4 hay que hacer esto  

A continuación vamos a ver una serie de comandos que permiten ver la estructura y datos de una base de datos en MySQL desde la terminal. 

#### Listar las bases de datos

Si queremos ver una lista de todas las bases de datos que tenemos, usaremos en comando `SHOW DATABASES;`. 

#### Utilizar una base de datos

Para conectarnos a una base de datos y trabajar sobre ella, usaremos `CONNECT nombreDB;` o `USE nombreDB;`. 

#### Listar las tablas de una base de datos

Para ver una lista de las tablas de la base de datos en la que estamos, debemos poner `SHOW TABLES;`. 

#### Ver información de una tabla

Si lo que queremos es ver la información de las tablas de la base de datos, hay que usar `SHOW TABLE STATUS;`. 

#### Ver la estructura de una tabla

Para ver la estructura de una tabla en concreto, usaremos `DESCRIBE nombreTabla;`. 

#### Ver las columnas de una tabla

Para ver las columnas de una tabla, usaremos el comando `SHOW COLUMNS FROM nombreTabla;`. 

#### Ver la creación de una tabla 

También podemos ver cómo hemos creado una tabla utilizando `SHOW CREATE TABLE nombreTabla;`. 

#### Ver registros de una tabla 

Para ver registros de una tabla, usaremos `SELECT algo FROM nombreTabla;`. Ese "algo" puede ser desde un *, que muestra todos los registros de la tabla, hasta un dato específico.


### Bibliografía

------ meter los enlaces si tal 
