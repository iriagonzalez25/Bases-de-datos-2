# Apuntes SQL 2 - iria gonzález peteiro -

## Índice

## Recordamos

SQL es un lenguaje declarativo (declara la intención) para gestionar bases de datos relacionales, pero aunque tenga seis sublenguajes, SQL es solamente uno. Los sublenguajes son los siguientes:

|**Sublenguaje**                                                                    |**Instrucciones del sublenguaje**      |
|-----------------------------------------------------------------------------------|---------------------------------------|
|**DQL (Data Query Language)** - Opera sobre los datos                              |`SELECT`                               |
|**DML (Data Manipulation Language)** - Opera sobre los datos                       |``INSERT``, ``UPDATE``, ``DELETE``     |
|**DDL (Data Definition Language)** - Opera sobre los objetos de la base de datos   |`CREATE`, `ALTER`, `DROP`              |
|**TCL (Transaction Control Language)**                                             |`COMMIT`, `ROLLBACK`                   |
|**DCL (Data Control Language)**                                                    |`GRANT`, `REVOKE`                      |
|**SCL (Session Control Language)**                                                 |`ALTER SESSION`                        |

## A tener en cuenta

En VARCHAR2, es mejor poner longitud máxima que sepas que te va a sobrar, no tirar por lo bajo y que después tengas problemas.

Los textos literales se ponen entre comillas. 

NUMBER(8) sería lo mismo que NUMBER(8,0). 

Si borras una tabla, no hay comando para recuperarla. 

En `INSERT INTO`, en algunos casos no es necesario poner las columnas, pero mejor ponerlas siempre para no confundirse. 

El dominio es donde puede tomar valores un atributos.

Tipos de datos: Además de INTEGER, tenemos BIGINT y SMALLINT, pero vamos a utilizar unicamente INTEGER. FLOAT es para MySQL y REAL es para Postgres; nosotros vamos a utilizar FLOAT. No es recomendable utilizar TEXT por defecto por una cuestión de rendimiento. Creo que el time puede llevar detrás la zona horaria. El boolean considera 0 como falso, true como 1 y hay varias cosas más. 

## Tipos de datos

Aquí tenemos los tipos de datos que vamos a utilizar. 

|**Numéricos**    |**Texto**      |**Fechas**     |**Otros**       |**Otros**|
|-----------------|---------------|---------------|----------------|---------|
|``INTEGER``      |``CHAR(n)``    |``DATE``       |``BOOLEAN``     |``CIDR`` |
|``DECIMAL``      |``VARCHAR(n)`` |``TIME``       |``MONEY``       |``JSON`` |
|``REAL``         |``TEXT``       |``DATETIME``   |``INET``        |``UUID`` |


- INTEGER --> para número enteros. También hay BIGINT y SMALLINT.
- DECIMAL y REAL, es lo mismo pero DECIMAL es preciso y REAL es no preciso. 
- CHAR --> para textos de lonigtud limitada fija.
- VARCHAR --> para textos de longitud limitada variable.
- TEXT --> para textos de longitud ilimitada variable.
- DATE --> formato: AAAA-MM-DD.
- TIME --> formato: hh:mm:ss...
- DATETIME --> formato: AAAA-MM-DD hh:mm:ss.
- BOOLEAN --> posibles valores, true o 1, false o 0, NULL. 
- MONEY --> para trabajar con dinero. 
- **El resto no tengo ni idea la vd** --> buscarlo nel internete

Ejemplos: 
- Texto de longitud 10 --> CHAR(10). 
- VARCHAR(20) --> texto de como máximo longitud 20. 

rollo para asegurarse de que un dni tiene longitud 9 --> CONSTRAINT ck_dni CHECK LENGHT(dni)=9; 

## DDL - Data Definition Language

DDL es el lenguaje que se encarga de la definición de datos. Crea, modifica y elimina los objetos de la base de datos. 

`CREATE` es un comando o una instrucción usada para crear bases de datos, tablas o usuarios.

El comando para crear una base de datos es `CREATE DATABASE`. Ejemplo: _CREATE DATABASE nombreBD;_ 

### Crear tablas

El comando para **crear una tabla** es `CREATE TABLE`, y la sintaxis para hacerlo es la siguiente:

	CREATE TABLE [esquema.] nombreTabla (
		nombreColumna1 tipoDatos [DEFAULT valor] 
        	[restricciones]  [, ...]
	);

Un ejemplo de creación de tabla podría ser el siguiente:

	CREATE TABLE Alumno (
		id INTEGER PRIMARY KEY,
		nome NCHAR (50),
		apelidos NCHAR (200),
		nacido DATA
	);

### Borrar tablas

El comando para borrar una tabla es `DROP TABLE`. 

La sintaxis para **borrar una tabla** es la siguiente:
	
	DROP TABLE nombreTabla;
	
### Modificar tablas

El comando para modificar una tabla es `ALTER TABLE`.

Para **modificar el nombre** de una tabla hay que utilizar `RENAME TO`. La sintaxis es la siguiente:

	ALTER TABLE nombreTabla RENAME TO nuevoNombre;

Para **añadir columnas** a una tabla hay que utilizar `ADD`, la sintaxis es parecida a la de `CREATE TABLE` y es la siguiente:

	ALTER TABLE nombreTabla ADD(nombreColumna tipoDatos [Propiedades])
	
En caso de que se quisiera añadir más de una columna, simplemente habría que volver a poner _nombreColumna tipoDatos [Propiedades]_ otra vez dentro de los paréntesis. 
	
***** Algunas cosas requieren poner COLUMN después de ADD y de DROP y MODIFY --> mirar si lo nuestro 

Para **borrar columnas** a una tabla hay que utilizar `DROP`siguiendo la sintaxis siguiente:

	ALTER TABLE nombreTabla DROP(columna);

En caso de que se quisiera borrar más de una columna, simplemente habría que poner separadas por comas todas las comunas que se quieran borrar: _(columna, otraColumna, otraColumnaMás)_. 

El borrado de columnas es irreversible. 
	



### Restricciones

Pueden colocarse restricciones para limitar el tipo de dato que se ingresa en una tabla. Esto se hace con ``CONSTRAINT``. Estas restricciones pueden especificarse al crear la tabla, o modificándola. 

Los tipos comunes de restricciones son ``NOT NULL``, ``UNIQUE``, ``CHECK``, ``PRIMARY KEY`` y ``FOREIGN KEY. 

#### NOT NULL
Por defecto, una columna puede ser NULL, así que ponemos NOT NULL si no queremos que lo sea

	CREATE TABLE ejemplo (
		id CHAR(3) NOT NULL, 
		nombre VARCHAR(10) NOT NULL,
		apellido VARCHAR(20)
	);

#### UNIQUE
Esta restricción sirve para que todos los valores de una columna sean distintos. 

	CREATE TABLE ejemplo (
		id CHAR(3) UNIQUE, 
		nombre VARCHAR(10),
		apellido VARCHAR(20)
	);
	
Una columna que se especifica como clave primaria también puede ser única, pero una columna que es única no tiene por qué ser clave primaria.

#### CHECK
Esta restricción sirve para que todos los valores en una columna cumplan ciertas condiciones.

	CREATE TABLE ejemplo (
		id INTEGER CHECK(id>0), 
		nombre VARCHAR(10),
		apellido VARCHAR(20)
	);
	
#### PRIMARY KEY	
La clave primaria se utiliza para identificar en forma única cada línea en la tabla y puede consistir en uno o más campos en una tabla (en este caso se los denomina claves compuestas). 

	CREATE TABLE ejemplo (
		id INTEGER PRIMARY KEY
		nombre VARCHAR(10),
		apellido VARCHAR(20)
	);

En caso de que queramos añadir esta restricción una vez creada la tabla, haríamos lo siguiente:

	ALTER TABLE ejemplo ADD PRIMARY KEY (id);

#### FOREIGN KEY
La clave foránea sirve para señalar la clave primaria de otra tabla para asegurar la integridad referencial de los datos. 





La creación de una base de datos permite CREATE SCHEMA y CREATW DATABASE. Un ejemplo de creación de bases de datos sería el siguiente:
_CREATE DATABASE myDB;_
_CREATE SCHEMA myOtherDB;_








Unha das fórmulas da instrucción CREATE é: 
CREATE (SCHEMA|DATABASE) [IF NOT EXISTS] <nome-da-base> [CHARACTER SET <nome-do-Charget>]

O de (SCHEMA|DATABASE) permite elixir entre ambos. O if not exists pode ir ou non ir, e entre <> hai que poñer o nome da base de datos. Lo de character set no sé qué es la vd.



O de INTEGER e así é o dominio
Valores para fechas → DATA (data), TIME (hora), TIMESTAMP (data e hora).

CHAR, VARCHAR, NCHAR, NCHAR VARYING, TEXT

**Fijarse que aquí es NOT NULL, no IS NOT NULL. 



[ON DELETE
	NO ACTION | CASCADE
	SET NULL | SET DEFAULT
]


CASCADE --> cuando borras un dato en un tabla, todo lo que está asociado a ese dato se borrará también. 
Ejemplo (comprobarlo):
	dept (_id_, name)
	teacher (id, name, _dept_, IBAN)
	_El id de dept es lo mismo que el dept de teacher, por lo que si borras un id de dept, se borrará también el dept de teacher y será null_ 

definir el resto

[MATCH FULL | PARTIAL]



[CONSTRAINT <nomeDaRestriccion>]
	UNIQUE (<atributos>),
	
	
UNIQUE (PRIMARY KEY) --> restricción de unicidad 

--------> solo vamos a ver 4 tipos de restriccion en CREATE table (esta es la cuarta) 

[CONSTRAINT <nombreDaRestriccon>]
	CHECK predicado (atributos)
[[NOT] DEFERRABLE]
[INITIALLY INMEDIATE|DEFERRABLE] --> esto fuera (hay que elegir entre inmediate y deferrable creo) 

...
Si es DEFERRABLE, la comporbación de la restricción se puede posponer hasta el final de la transacción.

Comportamiento por defecto - que se haga al momento --> INITIALLY INMEDIATE
Posponerlo --> INITIALLY DEFERRABLE

Ejemplo:
	CHECK saldo >= (
		SELECT saldo
		FROM empregado
		WHERE departamento='A');





DROP SCHEMA
[] <nomeDaBase>; 
	
DROP SCHEMA
[IF EXISTS] <nomeDaBD>;
	
	
DROP TABLE
[IF EXISTS] <nombreDaTaboa>
[CASCADE | RESTRICT]
	
	
ALTER TABLE:
	
	ADD [COLUMN] <atributo> <dominio> .. 

	DROP COLUMN <atributo> [CASCADE | RESTRICT]
	
	ADD <restricción> 
	
	DROP <restricción>

## DML - Data Manipulation Language

DDL era para el manejo de datos. DML es para el manejo de estructuras. Los tres comandos de este sublenguaje son `INSERT`, `UPDATE` y `DELETE`. 

### Insertar datos

Para **insertar datos** en un tabla hay que usar `INSERT INTO` y `VALUES`, siguiendo la sintaxis:

	INSERT INTO nombreTabla (nombreColumna1, nombreColumna2, ...) VALUES ("valor1", "valor2", ...);
	
Otra sintaxis posible sería la siguiente:

	INSERT INTO nombreTabla (nombreColumna1, nombreColumna2, ...) SELECT...;

Si usamos `SELECT` hay ciertas restricciones:
- Tiene que tener el mismo número de columnas que la tabla en cuestión (es decir, si pone _INSERT INTO tabla (columna1, columna2)_, el _SELECT_ sólo podrá seleccionar dos columnas.
- Los atributos no tienen que llamarse igual.
- Mismos dominimos (tipo de datos) que los de la tabla.

### Modificar datos

Para **modificar los datos** de una tabla, hay que usar `UPDATE` y `SET`, con la sintaxis siguiente:

	UPDATE nombreTabla SET atributo1 = valor1, atributo2 = valor2, ... WHERE predicado;

La parte de _WHERE ..._ es opcional. 

Ejemplo: _UPDATE world SET name='España', continent='Africa' WHERE name='Spain';_

### Eliminar datos

Para **eliminar datos** de una tabla hay que utilizar `DELETE FROM`, y la sintaxis que debemos usar es:

	DELETE FROM nombreTabla WHERE predicado;
	
En este caso, la parte de _WHERE_ también es opcional. 

Ejemplo: _DELETE FROM world WHERE population>100000000;_
