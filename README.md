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

El dominio es donde puede tomar valores un atributos (INTEGER por ejemplo). 

Tipos de datos: Además de INTEGER, tenemos BIGINT y SMALLINT, pero vamos a utilizar unicamente INTEGER. FLOAT es para MySQL y REAL es para Postgres; nosotros vamos a utilizar FLOAT. No es recomendable utilizar TEXT por defecto por una cuestión de rendimiento. Creo que el time puede llevar detrás la zona horaria. El boolean considera 0 como falso, true como 1 y hay varias cosas más. 

**Fijarse que aquí es NOT NULL para definir que no sea nulo, no IS NOT NULL (IS NOT NULL sería si por ejemplo queremos poner  CHECK (column_name IS NOT NULL)**  

Para borrar una tabla, se utiliza ``DROP``, pero si solo queremos borrar columnas hay que usar ``DELETE``. 
## Tipos de datos

Aquí tenemos los tipos de datos (el dominio) que vamos a utilizar. 

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
- Texto de como máximo longitud 20 --> VARCHAR(20).

rollo para asegurarse de que un dni tiene longitud 9 --> CONSTRAINT ck_dni CHECK LENGHT(dni)=9; 

## DDL - Data Definition Language

DDL es el lenguaje que se encarga de la definición de datos. Crea, modifica y elimina los objetos de la base de datos. 

`CREATE` es un comando o una instrucción usada para crear bases de datos, tablas o usuarios.

El comando para crear una base de datos es `CREATE DATABASE`. Ejemplo: ``CREATE DATABASE nombreBD;`` 

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

#### IF NOT EXISTS

no se por k enbeces aparece el IF NOT EXISTS o nsq muvis


### Borrar tablas

El comando para borrar una tabla es `DROP TABLE`. 

La sintaxis para **borrar una tabla** es la siguiente:
	
	DROP TABLE nombreTabla;
	
Tenemos dos opciones a la hora de borrar, ``CASCADE``y ``RESTRICT`` **(creo que tablas y mas cosas)**, que irían después del nombre de la tabla pero no es necesario ponerlo ya que tiene como valor por defecto ``RESTRICT``(**COMPROBAR ESTO ULTIMO QUE NO SE SI ES ASI**. 

	DROP TABLE tabla CASCADE;
	
	DROP TABLE tabla RESTRICT;
	
Podemos borrar dos tablas a la vez:

	DROP TABLE tabla1, tabla2;

Si utilizamos ``CASCADE``, cuando borras un dato en un tabla, todo lo que está asociado a ese dato se borrará también. En el siguiente ejemplo (comprobarlo) ``dept (id, name)``, ``teacher (id, name, dept, IBAN)``, el id de dept es lo mismo que el dept de teacher, por lo que si borras un id de dept, se borrará también el dept de teacher y pasará a ser NULL.

``RESTRICT``, sin embargo, no permite eliminar la tabla si algún objeto depende de ella. Este es el valor predeterminado. 



DROP SCHEMA
[] <nomeDaBase>; 
	
DROP SCHEMA
[IF EXISTS] <nomeDaBD>;
	
	
DROP TABLE
[IF EXISTS] <nombreDaTaboa>
[CASCADE | RESTRICT]




### Modificar tablas

El comando para modificar una tabla es `ALTER TABLE`.

Para **modificar el nombre** de una tabla hay que utilizar `RENAME TO`. La sintaxis es la siguiente:

	ALTER TABLE nombreTabla RENAME TO nuevoNombre;

Para **añadir columnas** a una tabla hay que utilizar `ADD`, la sintaxis es parecida a la de `CREATE TABLE` y es la siguiente:

	ALTER TABLE nombreTabla ADD COLUMN (nombreColumna tipoDatos [Propiedades])
	
En caso de que se quisiera añadir más de una columna, simplemente habría que volver a poner _nombreColumna tipoDatos [Propiedades]_ otra vez dentro de los paréntesis. 

Para **borrar columnas** a una tabla hay que utilizar `DROP`siguiendo la sintaxis siguiente:

	ALTER TABLE nombreTabla DROP COLUMN (columna);

En caso de que se quisiera borrar más de una columna, simplemente habría que poner separadas por comas todas las columnas que se quieran borrar: ``(columna, otraColumna, otraColumnaMás)``. 

El borrado de columnas es irreversible. 


### Restricciones

Pueden colocarse restricciones para limitar el tipo de dato que se ingresa en una tabla. Esto se hace con ``CONSTRAINT``, pero no es necesario poner ``CONSTRAINT``(lo veremos a continuación a través de ejemplos). Estas restricciones pueden especificarse al crear la tabla, o modificándola. 

Los tipos comunes de restricciones son ``NOT NULL``, ``UNIQUE``, ``CHECK``, ``PRIMARY KEY`` y ``FOREIGN KEY``.

Las restricciones pueden ser inmediatas ``INITIALLY INMEDIATE`` o diferidas ``INITIALLY DEFERRABLE``. 


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

Otra manera utilizando ``CONSTRAINT``:

	CREATE TABLE ejemplo (
    		precio INTEGER CONSTRAINT precio_diferente UNIQUE,
    		nombre VARCHAR(20)
	);
	
Una columna que se especifica como clave primaria también puede ser única, pero una columna que es única no tiene por qué ser clave primaria.


#### CHECK
Esta restricción sirve para que todos los valores en una columna cumplan ciertas condiciones.

	CREATE TABLE ejemplo (
		numero INTEGER CHECK (numero>0), 
		nombre VARCHAR(10),
		precio INTEGER NOT NULL CHECK (precio>10)
	);
	
Otra manera:	

	CREATE TABLE ejemplo (
    		numero INTEGER,
    		nombre VARCHAR(10),
    		precio INTEGER CONSTRAINT positivo_precio CHECK (price > 0)
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
La clave foránea sirve para señalar la clave primaria de otra tabla para asegurar la integridad referencial de los datos. Puede haber más de una clave foránea en una tabla.

		CREATE TABLE producto (
  			producto_numero INTEGER PRIMARY KEY, 
  			nombre VARCHAR(10),
			precio INTEGER
		);
		
		CREATE TABLE pedido (
    			pedido_id INTEGER PRIMARY KEY,
    			numero_producto INTEGER REFERENCES producto (product_numero),
			factura INTEGER
		);


#### Restricciones inmediatas o diferidas

--------> solo vamos a ver 4 tipos de restriccion en CREATE table (esta es la cuarta) una es UNIQUE fijo osea q sobra uno entiendo. PARA NOSOTROS ES MEJOR LA MANERA CON CONSTRAINT?? 

SET CONSTRAINTS establece el comportamiento de la comprobación de restricciones dentro de la transacción actual. Las restricciones inmediatas (``INITIALLY INMEDIATE``), que es el comportamiento por defecto, se verifican al final de cada declaración, es decir, al momento. Las restricciones diferidas (``INITIALLY DEFERRABLE``), la comporbación de la restricción se puede posponer hasta el final de la transacción.. Cada restricción tiene su propio modo inmediato o diferido.


EJEMPLO MAL FIJO COMPROBARLO NO LO ENTIENDO LLORO
	[CONSTRAINT nombreRestriccion]
		CHECK predicado (atributos)
		[[NOT] DEFERRABLE] --> esq esto no lo entiendo jajaajaj
		[INITIALLY INMEDIATE|DEFERRABLE]
	;

Ejemplo: (me da q en este ejmplo falta toda la aprte que seria ejemplo de esto xd en fin) 
	CHECK saldo >= (
		SELECT saldo
		FROM empregado
		WHERE departamento='A'
	);



### Esquemas

**esq yo no se a que viene lo de esquemas la verdad** 

Una base de datos contiene uno o más esquemas con nombre, que a su vez contienen tablas. Para crear, borrar... los esquemas, se utiliza la misma sintaxis que en con las tablas:

	CREATE SCHEMA esquema;
	
Para crear una tabla en el esquema:

	CREATE TABLE esquema.tabla (...);
	
Para borrar un esquema:

	DROP SCHEMA esquema;
	
Si lo queremos borrar incluyendo todos sus objetos:

	DROP SCHEMA esquema CASCADE;

Un ejemplo de creación de bases de datos sería el siguiente:
_CREATE DATABASE myDB;_
_CREATE SCHEMA myOtherDB;_




#### MATCH

**No sé de que manera meter este apartado, si tres o cuatro almohadillas y si al principio o al final. 

Hay tres tipos: ``MATCH FULL``, ``MATCH PARTIAL`` y ``MATCH SIMPLE`` (valor predeterminado). Por una parte, ``MATCH FULL`` no permite que una columna de una clave externa de varias columnas sea nula a menos que todas las columnas de clave externa sean nulas. ``MATCH SIMPLE`` permite que algunas columnas de clave externa sean nulas, mientras que otras partes de la clave externa no lo son. ``MARCH PARTIAL`` aún no está implementado. **seguro???** 

	CREATE TABLE ejemplo (
		id INTEGER PRIMARY KEY,
		num INTEGER REFERENCES producto (otro_num) MATCH FULL
	);


### ordenar esto



Unha das fórmulas da instrucción CREATE é: 
CREATE (SCHEMA|DATABASE) [IF NOT EXISTS] <nome-da-base> [CHARACTER SET <nome-do-Charget>]

O de (SCHEMA|DATABASE) permite elixir entre ambos. O if not exists pode ir ou non ir, e entre <> hai que poñer o nome da base de datos. Lo de character set no sé qué es la vd.









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

Ejemplo: ``UPDATE world SET name='España', continent='Africa' WHERE name='Spain';``

### Eliminar datos

Para **eliminar datos** de una tabla hay que utilizar `DELETE FROM`, y la sintaxis que debemos usar es:

	DELETE FROM nombreTabla WHERE predicado;
	
En este caso, la parte de _WHERE_ también es opcional. 

Ejemplo: ``DELETE FROM world WHERE population>100000000;``
