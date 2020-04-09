# Creación de bases de datos en MySQL

- [Ejercicio 1 - Proyectos de investigación](#e1)
- [Ejercicio 2 - Naves espaciales](#e2)

<a name="e1"></a>
## Proyecto de investigación
Vamos a crear una base de datos llamada *Proxecto_Investigacion* a partir de este [enunciado](https://github.com/davidgchaves/first-steps-with-git-and-github-wirtz-asir1-and-dam1/tree/master/exercicios-ddl/1-proxectos-de-investigacion). 

Abrimos la terminal y entramos en MySQL con el comando `mysql -u root -p`. 

Primero de todo, vamos a crear la base de datos con `CREATE DATABASE Proxecto_Investigacion;`, y nos cambiamos a ella, con `USE Proxecto_Investigacion;` para empezar a trabajar sobre ella:



Ahora vamos a crear las tablas y las mostramos ....

**no sé si poner el create table de todo es que me parece tontería la verdad no sé aaaaa** 

Una vez hayamos creado todo, podemos ver todas las tablas de nuestra base de datos utilizando `SHOW TABLES;`: 

![Tablas]()

**igual en vez del proceso de creación es mejor poner la descripción de cada tabla meditar esto en camita** 

<a name="e2"></a>
## Naves espaciales
A partir de este [enunciado](https://github.com/davidgchaves/first-steps-with-git-and-github-wirtz-asir1-and-dam1/tree/master/exercicios-ddl/2-naves-espaciais), creamos una base de datos llamada *Naves_Espaciais*. 

Una vez estemos en MySQL desde la terminal, lo primero que hacemos es crear la base de datos, y cambiarnos a ella para poder empezar a crear las tablas:

![Creación db Naves Espaciais](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/crear%20naves%20espaciais.png) 

Ahora vamos a crear las tablas siguiendo las indicaciones del enunciado:

![Tabla Servizo](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/servizo.png) 
![Tabla Dependencia](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/dependencia.png) 
![Tabla Camara](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/camara.png) 
![Tabla Tripulacion](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/tripulacion.png) 
![Tabla Planeta](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/planeta.png) 
![Tabla Visita](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/visita.png) 
![Tabla Raza](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/raza.png) 
![Tabla Habita](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/habita.png) 

Ahora podemos comprobar que tenemos todas las tablas con `SHOW TABLES`:

![Tablas Naves Espaciais](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/tablas%20naves%20espaciais.png)
