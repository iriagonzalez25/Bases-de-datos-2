# Apuntes SQL 2 - iria gonzález peteiro -

# Índice

# Recordamos

SQL es un lenguaje declarativo (declara la intención) para gestionar bases de datos relacionales, pero aunque tenga seis sublenguajes, SQL es solamente uno. Los sublenguajes son los siguientes:

|**Sublenguaje**                                                                    |**Instrucciones del sublenguaje**      |
|-----------------------------------------------------------------------------------|---------------------------------------|
|**DQL (Data Query Language)** - Opera sobre los datos                              |`SELECT`                               |
|**DML (Data Manipulation Language)** - Opera sobre los datos                       |``INSERT``, ``UPDATE``, ``DELETE``     |
|**DDL (Data Definition Language)** - Opera sobre los objetos de la base de datos   |`CREATE`, `ALTER`, `DROP`              |
|**TCL (Transaction Control Language)**                                             |`COMMIT`, `ROLLBACK`                   |
|**DCL (Data Control Language)**                                                    |`GRANT`, `REVOKE`                      |
|**SCL (Session Control Language)**                                                 |`ALTER SESSION`                        |


# DDL - DATA DEFINITION LANGUAGE

`CREATE` es un comando o una instrucción usada para crear bases de datos, tablas o usuarios.

Lo de crear usuarios nos recuerda a DCL, que cuenta con ``GRANT`` y ``REVOKE``. 

La creación de una base de datos permite CREATE SCHEMA y CREATW DATABASE. Un ejemplo de creación de bases de datos sería el siguiente:
_CREATE DATABASE myDB;_
_CREATE SCHEMA myOtherDB;_







Unha das fórmulas da instrucción CREATE é: 
CREATE (SCHEMA|DATABASE) [IF NOT EXISTS] <nome-da-base> [CHARACTER SET <nome-do-Charget>]

O de (SCHEMA|DATABASE) permite elixir entre ambos. O if not exists pode ir ou non ir, e entre <> hai que poñer o nome da base de datos. Lo de character set no sé qué es la vd.

	Un ejemplo de creación de una tabla podría ser:
CREATE TABLE Alumno (
	id INTEGER PRIMARY KEY,
	nome NCHAR (50),
	apelidos NCHAR (200),
	nacido DATA
);

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

