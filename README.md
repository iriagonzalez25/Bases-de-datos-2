# Apuntes SQL - iria gonzález peteiro -

SQL es un lenguaje para gestionar bases de datos relacionales, pero aunque tenga seis sublenguajes, SQL es solamente uno.
Los sublenguajes son los que se mencionan en la primera parte de los apuntes. 

# DDL - DATA DEFINITION LANGUAGE

CREATE es un comando o una instrucción usada para crear bases de datos, tablas o usuarios

Lo de crear usuarios nos recuerda a DCL, que cuenta con GRANT y REVOKE. 

La creación de una base de datos permite CREATE SCHEMA y CREATW DATABASE. Un ejemplo de creación de bases de datos sería el siguiente:
_CREATE DATABASE myDB;_
_CREATE SCHEMA myOtherDB;_







Unha das fórmulas da instrucción CREATE é: 
CREATE (SCHEMA|DATABASE) [IF NOT EXISTS] <nome-da-base> [CHARACTER SET <nome-do-Charget>]

O de (SCHEMA|DATABASE) permite elixir entre ambos. O if not exists pode ir ou non ir, e entre <> hai que poñer o nome da base de datos. Lo de character set no sé qué es la vd.

	Un exemplo de creación dunha táboa podería ser:
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




