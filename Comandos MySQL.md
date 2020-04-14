# Comandos MySQL 

A continuación vamos a ver una serie de comandos que permiten ver la estructura y datos de una base de datos en MySQL desde la terminal. 

### Listar las bases de datos

Si queremos ver una lista de todas las bases de datos que tenemos, usaremos el comando `SHOW DATABASES;`. 

![Lista bases de datos](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/show%20databases.png)

### Utilizar una base de datos

Para conectarnos a una base de datos y trabajar sobre ella, usaremos `CONNECT nombreDB;` o `USE nombreDB;`. 

![CONNECT](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/connect%20naves%20espaciais.png)

![USE](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/use%20proyecto%20investigacion.png)

### Listar las tablas de una base de datos

Para ver una lista de las tablas de la base de datos en la que estamos, debemos poner `SHOW TABLES;`. 

![SHOW TABLES](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/show%20tables.png)

### Ver información de las tablas

Si lo que queremos es ver la información de las tablas de la base de datos, hay que usar `SHOW TABLE STATUS;`. 

![SHOW TABLE STATUS](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/show%20table%20status.png)

### Ver la estructura de una tabla

Para ver la estructura de una tabla en concreto, usaremos `DESCRIBE nombreTabla;` o `DESC nombreTabla`. El comando `SHOW COLUMNS FROM nombreTabla;` mostraría lo mismo. 

![DESCRIBE](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/describe.png)

![SHOW COLUMNS FROM](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/show%20columns%20from.png)

### Ver la creación de una tabla 

También podemos ver cómo hemos creado una tabla utilizando `SHOW CREATE TABLE nombreTabla;`. 

![SHOW CREATE TABLE](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/show%20create%20table.png)

