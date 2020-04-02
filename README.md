Iria González Peteiro

# Apuntes SQL 2 📝

## Índice 🎬

- [Introducción SQL](#intro)
- [Tipos de datos](#tiposDatos)
- [Anotaciones generales](#anotaciones)
- [DDL](#ddl)
   - [Crear dominios](#dominios)
   - [Crear tablas](#crearT)
   - [Borrar tablas](#borrarT)
   - [Modificar tablas](#modificarT)
   - [Restricciones](#restricciones)
   - [Bases de datos](#basesDatos)
   - [Esquemas](#esquemas)
- [DML](#dml)
   - [Insertar datos](#insertarD)
   - [Modificar datos](#modificarD)
   - [Eliminar datos](#eliminarD)

<a name="intro"></a>
## Introducción SQL 🚼 

SQL es un lenguaje declarativo (declara la intención) para gestionar bases de datos relacionales, pero aunque tenga seis sublenguajes, SQL es solamente uno. Recordamos que los sublenguajes son los siguientes:

|**Sublenguaje**                                                                    |**Instrucciones del sublenguaje**      |
|-----------------------------------------------------------------------------------|---------------------------------------|
|**DQL (Data Query Language)** - Opera sobre los datos                              |`SELECT`                               |
|**DML (Data Manipulation Language)** - Opera sobre los datos                       |``INSERT``, ``UPDATE``, ``DELETE``     |
|**DDL (Data Definition Language)** - Opera sobre los objetos de la base de datos   |`CREATE`, `ALTER`, `DROP`              |
|**TCL (Transaction Control Language)**                                             |`COMMIT`, `ROLLBACK`                   |
|**DCL (Data Control Language)**                                                    |`GRANT`, `REVOKE`                      |
|**SCL (Session Control Language)**                                                 |`ALTER SESSION`                        |

>En este documento, vamos a ver DDL y DML. 

<a name="anotaciones"></a>
## Anotaciones generales ✏️ 

Los textos literales se ponen entre comillas. 

El dominio es donde puede tomar valores un atributos (`INTEGER`, por ejemplo). 

Para establecer las claves primarias, preferiblemente no usar `ALTER TABLE` y establecerlas al crear la tabla. 

Para borrar una tabla, se utiliza `DROP`, pero para borrar columnas hay que usar `DELETE`. 

Para las restricciones, mejor utilizar siempre el formato con `CONSTRAINT` al final, ya que de esta forma sirve siempre, si se pone detrás del atributo solo sirve cuando hay una única clave. Así evitamos confusiones. 

Además, la forma con `CONSTRAINT` puede ser poniendo o no `CONSTRAINT`, pero mejor ponerlo también porque así se hace siempre de la misma forma y no hay confusiones. 

Se utiliza `NULL` o `NOT NULL` para que algo no sea nulo, no `IS NULL` o `IS NOT NULL` (`IS NOT NULL` sería si por ejemplo queremos poner `CHECK (column_name IS NOT NULL)`.

En `INSERT INTO`, en algunos casos no es necesario poner las columnas, pero mejor ponerlas siempre para no confundirse. 

En los enunciados, el asterisco significa `NULL`.

>A lo largo del documento habrá anotaciones específicas para cada apartado, que estarán en este formato. 

<a name="tiposDatos"></a>
## Tipos de datos 💯

Aquí tenemos los tipos de datos (el dominio) que vamos a utilizar. 

|**Numéricos**    |**Texto**      |**Fechas**     |**Otros**       |**Otros**|
|-----------------|---------------|---------------|----------------|---------|
|``INTEGER``      |``CHAR(n)``    |``DATE``       |``BOOLEAN``     |``CIDR`` |
|``DECIMAL``      |``VARCHAR(n)`` |``TIME``       |``MONEY``       |``JSON`` |
|``REAL``         |``TEXT``       |``DATETIME``   |``INET``        |``UUID`` |


A continuación, vamos a ver para qué se utiliza cada uno de ellos. 

`INTEGER` --> para número enteros. También hay `BIGINT` y `SMALLINT`.

`DECIMAL` y `REAL` --> es lo mismo pero `DECIMAL` es preciso y `REAL` es no preciso. 

`CHAR` --> para textos de lonigtud limitada fija.

`VARCHAR` --> para textos de longitud limitada variable.

`TEXT` --> para textos de longitud ilimitada variable.

`DATE` --> formato: AAAA-MM-DD.

`TIME` --> formato: hh:mm:ss...

`DATETIME` --> formato: AAAA-MM-DD hh:mm:ss.

`BOOLEAN` --> posibles valores, true o 1, false o 0, NULL. 

`MONEY` --> para trabajar con dinero.

`INET` --> contiene una dirección de host IPv4 o IPv6 y, opcionalmente, su subred, todo en un campo.

`CIDR` --> contiene una especificación de red IPv4 o IPv6. 

`JSON` --> se usa para intercambiar datos en las aplicaciones web y móviles modernas. 

`UUID` --> muestra un identificador único universal aleatorio como un string. 

>En `VARCHAR`, poner como longitud máxima una que sepas que te va a sobrar, no tirar por lo bajo porque después puedes tener problemas.

>Usar `TEXT` solo cuando sean textos muy largos. No es recomendable usarlo por cuestión de rendimiento. 

>Diferencia entre `INET` y `CIDR`: `INET` acepta valores con bits distintos de cero a la derecha de la máscara de red y `CIDR` no. 

>Si solo se quieren aceptar redes, usar `CIDR`. 

Ejemplo: *si lo que queremos es un texto de longitud 10, usaremos `CHAR(10)`; si lo que queremos es un texto de como máximo longitud 10, usaremos `VARCHAR(10)`.*

<a name="ddl"></a>
## DDL - Data Definition Language 1️⃣👅 

DDL es el lenguaje que se encarga de la definición de datos. Crea, modifica y elimina los objetos de la base de datos. 

Se pueden crear bases de datos, esquemas y tablas. Una base de datos contiene uno o más esquemas con nombre, que a su vez contienen tablas.

<a name="dominios"></a>
### Crear dominios 🔨 

Se pueden **crear dominios** diferentes a los que ya existen. Para ello, hay que utilizar ``CREATE DOMAIN``. 

	CREATE DOMAIN nombreDom tipo_Datos;

Tenemos el siguiente ejemplo,  ``CREATE DOMAIN tipo_DNI CHAR(9)``. Ahora, será lo mismo poner tipo_DNI que CHAR(9). 

<a name="crearT"></a>
### Crear tablas 👷‍♂️

El comando para **crear una tabla** es `CREATE TABLE`, y la sintaxis para hacerlo es la siguiente:

	CREATE TABLE nombreTabla (
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

<a name="ifNot"></a>
#### IF NOT EXISTS 

Al crear una tabla se puede poner `IF NOT EXISTS`. Así, se creará una nueva tabla, solo si la tabla no existe actualmente en el conjunto de datos especificado. La sintaxis es la siguiente: 

	CREATE TABLE IF NOT EXISTS nombreTabla: 

<a name="borrarT"></a>
### Borrar tablas 🙅‍♀️

El comando para **borrar una tabla** es `DROP TABLE`. La sintaxis para hacerlo es la siguiente:
	
	DROP TABLE nombreTabla;
	
Podemos borrar dos tablas a la vez:

	DROP TABLE tabla1, tabla2;
	
Tenemos dos opciones a la hora de borrar, ``CASCADE``y ``RESTRICT``, que irían después del nombre de la tabla pero no es necesario ponerlo. 

	DROP TABLE tabla CASCADE;
	
	DROP TABLE tabla RESTRICT;
	

Si utilizamos ``CASCADE``, al borrar un dato en un tabla, todo lo que está asociado a ese dato se borrará también. En el siguiente ejemplo (comprobarlo) ``dept (id, name)``, ``teacher (id, name, dept, IBAN)``, el id de dept es lo mismo que el dept de teacher, por lo que si borras un id de dept, se borrará también el dept de teacher y pasará a ser NULL.

``RESTRICT``, sin embargo, no permite eliminar la tabla si algún objeto depende de ella. Este es el valor predeterminado. 

>No hay comando para recuperar una tabla tras borrarla. 

<a name="if"></a>
#### IF EXISTS 
	
Al contrario que en la creación de tablas, podemos poner `IF EXISTS`, de manera que se borrará una tabla, solo si la tabla ya existe. La sintaxis es la siguiente: 

	CREATE TABLE IF EXISTS nombreTabla;
	
Por supuesto, también se podrá poner `CASCADE` o `RESTRICT` después. 

<a name="modificarT"></a>
### Modificar tablas ♻️ 

El comando para modificar una tabla es `ALTER TABLE`.

Para **modificar el nombre** de una tabla hay que utilizar `RENAME TO`. La sintaxis es la siguiente:

	ALTER TABLE nombreTabla RENAME TO nuevoNombre;

Para **añadir columnas** a una tabla hay que utilizar `ADD`, la sintaxis es parecida a la de `CREATE TABLE` y es la siguiente:

	ALTER TABLE nombreTabla ADD COLUMN (nombreColumna tipoDatos [Propiedades], ...);

Para **borrar columnas** a una tabla hay que utilizar `DROP` siguiendo la sintaxis siguiente:

	ALTER TABLE nombreTabla DROP COLUMN (columna, ...) [CASCADE | RESTRICT];

>El borrado de columnas es irreversible. 

También se pueden **añadir o borrar restricciones** a una tabla. Aún no las hemos visto (las veremos a continuación), pero la sintaxis sería la siguiente, (siguiendo la línea de las columnas): 

	ALTER TABLE nombreTabla ADD <restricción>;
	
	ALTER TABLE nombreTabla DROP <restricción>;

<a name="restricciones"></a>
### Restricciones 🚫 

Pueden colocarse restricciones para limitar el tipo de dato que se ingresa en una tabla. Esto se hace con ``CONSTRAINT``, aunque no es necesario poner ``CONSTRAINT``(lo veremos a continuación a través de ejemplos). Estas restricciones pueden especificarse al crear la tabla, o modificándola. 

Los tipos comunes de restricciones son ``NOT NULL``, ``UNIQUE``, ``CHECK``, ``PRIMARY KEY`` y ``FOREIGN KEY``, y pueden ser inmediatas o diferidas.

- [NOT NULL](#notNull)
- [UNIQUE](#unique)
- [CHECK](#check)
- [PRIMARY KEY](#pk)
- [FOREIGN KEY](#fk)
- [Restricciones inmediatas o diferidas](#inmediatasDiferidas)


<a name="notNull"></a>
#### NOT NULL 

Por defecto, una columna puede ser `NULL`, así que ponemos `NOT NULL` si no queremos que lo sea:

	CREATE TABLE ejemplo (
		id CHAR(3) NOT NULL, 
		nombre VARCHAR(10) NOT NULL,
		apellido VARCHAR(20)
	);	

<a name="unique"></a>
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

>Una columna que se especifica como clave primaria también puede ser única, pero una columna que es única no tiene por qué ser clave primaria.

<a name="check"></a>
#### CHECK 
Esta restricción sirve para que todos los valores en una columna cumplan ciertas condiciones.

	CREATE TABLE ejemplo (
		numero INTEGER CHECK (numero>0), 
		nombre VARCHAR(10),
		precio INTEGER NOT NULL CHECK (precio>10)
	);
	
Otra manera, utilizando `CONSTRAINT`:	

	CREATE TABLE ejemplo (
    		numero INTEGER,
		precio INTEGER CONSTRAINT positivo_precio CHECK (precio > 0),
    		nombre VARCHAR(10)
	);
	
Es muy común poner los `CONSTRAINT`al final:

	CREATE TABLE ejemplo (
    		numero INTEGER,
		precio INTEGER 
    		nombre VARCHAR(10),
		CONSTRAINT positivo_precio CHECK (precio > 0)
	);
	
>Para asegurarse de que un atributo tiene una longitud determinada (por ejemplo, 9), habrá que poner: 
>>`CONSTRAINT ck_atb CHECK LENGHT (atb) = 9;` 

<a name="pk"></a>
#### PRIMARY KEY 	
La clave primaria se utiliza para identificar en forma única cada línea en la tabla y puede consistir en uno o más campos en una tabla (en este caso se los denomina claves compuestas). En caso de que solo haya una clave primaria:

	CREATE TABLE ejemplo (
		id INTEGER PRIMARY KEY
		nombre VARCHAR(10),
		apellido VARCHAR(20)
	);

Cuando hay más de una clave primaria (también sirve si hay una solo), se utiliza lo siguiente (y no se puede usar la forma anterior).

En caso de que sea solamente una clave primaria:

	CREATE TABLE ejemplo (
		id INTEGER,
		nombre VARCHAR(10),
		apellido VARCHAR(20),
		CONSTRAINT PK_ejemplo PRIMARY KEY (id)
	);

En caso de que haya varias claves primarias:

	CREATE TABLE ejemplo (
		id INTEGER,
		nombre VARCHAR(10),
		apellido VARCHAR(20),
		CONSTRAINT PK_ejemplo PRIMARY KEY (id, nombre)
	);

Es mejor establecer las claves primarias en ``CREATE TABLE``, pero en caso de que queramos añadir esta restricción una vez creada la tabla, utilizaríamos `ALTER TABLE`, que lo vimos anteriormente pero no ejemplificamos las restricciones porque todavía no las habíamos visto (separamos por comas los atributos si son más de uno):

	ALTER TABLE ejemplo ADD PRIMARY KEY (id);


<a name="fk"></a>
#### FOREIGN KEY 
La clave foránea sirve para señalar la clave primaria de otra tabla para asegurar la integridad referencial de los datos. Puede haber más de una clave foránea en una tabla.

		CREATE TABLE producto (
  			producto_numero INTEGER PRIMARY KEY, 
  			nombre VARCHAR(10),
			precio INTEGER
		);
		
		CREATE TABLE pedido (
    			pedido_id INTEGER PRIMARY KEY,
    			numero_producto INTEGER REFERENCES producto (producto_numero),
			factura INTEGER
		);

En caso de que utilicemos `CONSTRAINT`:

	CREATE TABLE producto (
  			producto_numero INTEGER PRIMARY KEY, 
  			nombre VARCHAR(10),
			precio INTEGER
		);
		
	CREATE TABLE pedido (
		pedido_id INTEGER PRIMARY KEY,
		numero_producto INTEGER 
		factura INTEGER,
		CONSTRAINT FK_pedido 
		    FOREIGN KEY (numero_producto) 
		    REFERENCES producto (producto_numero),
	);

>Usar siempre la forma con `CONSTRAINT` al final (en todo, no solo aquí), para evitar confusiones. 

Utilizamos `ALTER TABLE`, podríamos añadir la restricción así:

	ALTER TABLE Departamento
  	    ADD CONSTRAINT FK_pedido
    		FOREIGN KEY (Director)
                REFERENCES Profesor (DNI)
    		ON DELETE SET NULL
   		ON UPDATE CASCADE;

##### MATCH

La cláusula `MATCH` de una clave externa se usa para especificar el grado de coincidencia requerida entre claves externas y la clave referenciada. Ésta puede ser ``MATCH FULL``, ``MATCH PARTIAL`` y ``MATCH SIMPLE`` (que es el valor predeterminado), y estas opciones son válidas cuando la clave externa tiene valores nulos. 

Por una parte, ``MATCH FULL`` no permite que una columna de una clave externa de varias columnas sea nula a menos que todas las columnas de clave externa sean nulas. 

``MATCH SIMPLE`` permite que algunas columnas de clave externa sean nulas, mientras que otras partes de la clave externa no lo son. 

``MARCH PARTIAL`` es válida si al menos una columna de la clave externa es nula y el resto de las columnas no nulas coinciden con las de las tablas referenciadas, o si todas las columnas de clave externa no son nulas y coinciden con la tabla referenciada.

Se pondría así:

	CREATE TABLE ejemplo (
		id INTEGER PRIMARY KEY,
		num INTEGER REFERENCES producto (otro_num) MATCH FULL
	);


##### ON DELETE y ON UPDATE

`ON DELETE` y `ON UPDATE` (es opcional) sirve para especificar lo que pasará cuando borras o modificas, respectivamente, un dato de una tabla. Las acciones permitidas para `ON DELETE` y `ON UPDATE` son:

- ``CASCADE``. Al borrar o actualizar un dato en una tabla, todo lo que está asociado a ese dato se borrará o actualizará también. 

- `NO ACTION`, sin embargo, no permite eliminar o actualizar la tabla si algún objeto depende de ella. Este es el valor predeterminado. 

- `SET NULL`. El cambio está permitido y las columnas de clave externa de la fila secundaria se establecen en NULL.

- `SET DEFAULT`. Es similar a `SET NULL`, pero las columnas de clave externa se establecieron en sus valores predeterminados. Si los valores predeterminados no existen, se produce un error.

Veamos un ejemplo:

	CREATE TABLE producto (
		producto_numero INTEGER PRIMARY KEY, 
		nombre VARCHAR(10),
		precio INTEGER
	);
		
	CREATE TABLE pedido (
		pedido_id INTEGER PRIMARY KEY,
		numero_producto INTEGER 
		factura INTEGER,
		CONSTRAINT FK_REFERENCES 
		   FOREIGN KEY (numero_preducto) 
		   REFERENCES producto (producto_numero) 
		   ON DELETE SET NULL
		   ON UPDATE CASCADE
	);

<a name="inmediatasDiferidas"></a>
#### Restricciones inmediatas o diferidas

Las restricciones pueden ser inmediatas (``INITIALLY INMEDIATE``), que es el comportamiento por defecto, y que se verifican al final de cada declaración, es decir, al momento, o también pueden ser diferidas (``INITIALLY DEFERRABLE``), en donde la comprobación de la restricción se puede posponer hasta el final de la transacción. Cada restricción tiene su propio modo inmediato o diferido.

La sintaxis es la siguiente:

	CONSTRAINT nombreRestriccion
		CHECK predicado (atributos)
		[[NOT] DEFERRABLE] 
		[INITIALLY INMEDIATE|DEFERRABLE]
	;

>Cuando se establece que no es diferido, es decir, `NOT DEFERRABLE`, debería ir con `INITIALLY INMEDIATE`, y cuando se establece como `DEFERRABLE`, debería ser `INITIALLY DEFERRABLE`.

<a name="basesDatos"></a>
### Bases de datos 🔆 

Es parecido que a las tablas. El comando para crear bases de datos es `CREATE DATABASE`, y la sintaxis es la siguiente:

	CREATE DATABASE [IF NOT EXISTS] nombreDB [CHARACTER SET <nome-do-Charget>];

Para borrarlas, el comando es `DROP DATABASE`, con la sintaxis:
	
	DROP DATABASE [IF EXISTS] nombreDB;

<a name="esquemas"></a>
### Esquemas 🔅 

Una base de datos contiene uno o más esquemas con nombre, que a su vez contienen tablas. Para crear, borrar... los esquemas, se utiliza la misma sintaxis que en con las tablas:

	CREATE SCHEMA [IF NOT EXISTS] esquema [CHARACTER SET <nome-do-Charget>];;
	
Para crear una tabla en el esquema:

	CREATE TABLE esquema.tabla (...);
	
Para borrar un esquema:

	DROP SCHEMA [IF EXISTS] esquema;
	
>Al igual que las tablas, podemos poner `CASCADE` al final si lo queremos borrar incluyendo todos sus objetos, poner `IF NOT EXISTS` después de `CREATE SCHEMA`... 


<a name="dml"></a>
## DML - Data Manipulation Language 2️⃣👅 

DDL era para el manejo de datos. DML es para el manejo de estructuras. Los tres comandos de este sublenguaje son `INSERT`, `UPDATE` y `DELETE`. 

<a name="insertarD"></a>
### Insertar datos ↪️ 

Para **insertar datos** en un tabla hay que usar `INSERT INTO` y `VALUES`, siguiendo la sintaxis:

	INSERT INTO nombreTabla (nombreColumna1, nombreColumna2, ...) VALUES ("valor1", "valor2", ...);
	
Otra sintaxis posible sería la siguiente:

	INSERT INTO nombreTabla (nombreColumna1, nombreColumna2, ...) SELECT...;

Si usamos `SELECT` hay ciertas restricciones:
- Tiene que tener el mismo número de columnas que la tabla en cuestión (es decir, si pone _INSERT INTO tabla (columna1, columna2)_, el _SELECT_ sólo podrá seleccionar dos columnas.
- Los atributos no tienen que llamarse igual.
- Mismos dominimos (tipo de datos) que los de la tabla.

<a name="modificarD"></a>
### Modificar datos 🔄 

Para **modificar los datos** de una tabla, hay que usar `UPDATE` y `SET`, con la sintaxis siguiente:

	UPDATE nombreTabla SET atributo1 = valor1, atributo2 = valor2, ... WHERE predicado;

La parte de _WHERE ..._ es opcional. 

Ejemplo: ``UPDATE world SET name='España', continent='Africa' WHERE name='Spain';``

<a name="eliminarD"></a>
### Eliminar datos ↩️ 

Para **eliminar datos** de una tabla hay que utilizar `DELETE FROM`, y la sintaxis que debemos usar es:

	DELETE FROM nombreTabla WHERE predicado;
	
En este caso, la parte de _WHERE_ también es opcional. 

Ejemplo: ``DELETE FROM world WHERE population>100000000;``


