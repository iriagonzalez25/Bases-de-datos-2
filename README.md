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


## DDL - Data Definition Language

DDL es el lenguaje que se encarga de la definición de datos. Crea, modifica y elimina los objetos de la base de datos. 

`CREATE` es un comando o una instrucción usada para crear bases de datos, tablas o usuarios.

El comando para crear una base de datos es `CREATE DATABASE`. Ejemplo: _CREATE DATABASE nombreBD;_ 

### Crear tablas

El comando para crear una tabla es `CREATE TABLE`. 

La sintaxis para **crear una tabla** es la siguiente:

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


Ahora vamos a ver los tipos de datos:
- Texto:
	- VARCHAR2(tamañoMaximoTexto)
	- CHAR(longitudTexto)
	- NCHAR
	- NVARCHAR2
- Números:
	- NUMBER(numeroDigitos, decimales)
	- NUMBER(numeroDigitos)
	- NUMBER(numeroMaximoDigitos) --> para enteros ???????????
	- NUMBER --> número en coma flotante (?)

etc etc


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

