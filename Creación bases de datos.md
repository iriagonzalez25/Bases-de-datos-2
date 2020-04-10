# Creación de bases de datos en MySQL

- [Ejercicio 1 - Proyectos de investigación](#e1)
- [Ejercicio 2 - Naves espaciales](#e2)

<a name="e1"></a>
## Proyecto de investigación 🔍
Vamos a crear una base de datos llamada *Proxecto_Investigacion* a partir de este [enunciado](https://github.com/davidgchaves/first-steps-with-git-and-github-wirtz-asir1-and-dam1/tree/master/exercicios-ddl/1-proxectos-de-investigacion). 

Abrimos la terminal y entramos en MySQL con el siguiente comando:
>mysql -u root -p

Primero de todo, vamos a crear la base de datos con `CREATE DATABASE Proxecto_Investigacion;`:

![Creacion db Proyecto Investigación](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/crear%20proyecto%20de%20investigacion.png)

Y nos cambiamos a ella, con `USE Proxecto_Investigacion;` para empezar a trabajar sobre ella:

![Usar db Proyecto Investigación](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/usar%20proyecto%20investigacion.png)

Ya podemos empezar a crear las tablas de la base de datos siguiendo el enunciado del ejercicio:

![Tabla Sede](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/sede.png)
![Tabla Departamento](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/departamento.png)
![Tabla Ubicacion](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/ubicacion.png)
![Tabla Grupo](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/grupo.png)
![Tabla Profesor](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/profesor.png)

Una vez tenemos creada la tabla `Profesor`, podemos añadir a `Departamento` y a `Grupo` las claves foráneas de `Profesor`, las cuales no pudimos añadir al crearlas ya que todavía no teníamos esta tabla:

![FK Departamento](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/fk%20departamento.png)
![FK Grupo](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/fk%20grupo.png)

Seguimos creamos las tablas:

![Tabla Proxecto](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/proxecto.png)
![Tabla Participa](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/participa.png)
![Tabla Programa](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/programa.png)
![Tabla Financia](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/Fotos/financia.png)

<a name="e2"></a>
## Naves espaciales 🛸
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
