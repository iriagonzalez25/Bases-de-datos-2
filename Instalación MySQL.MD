# Instalación MySQL

Tras descargar el archivo DMG de MySQL (para es sistema operativo macOS) a través del siguiente enlace https://dev.mysql.com/downloads/mysql/, lo abrimos e instalamos.

Una vez nos aparece en la ventana de instalación el mensaje "Instalación completada" y un check verde, abrimos preferencias del sistema y vemos que aparece el icono de MySQL en la última fila:

![Logo MySQL](https://github.com/iriagonzalez25/Apuntes-2/blob/master/logo.png)

Le damos e iniciamos si no está iniciado. 

Una vez hecho esto, abrimos la terminal y escribimos lo siguiente: 

>/usr/local/mysql/bin/mysql -u root -p.

Le damos a enter y nos pedirá la contraseña, la cual establecimos durante el proceso de instalación y, tras introducirla, ya estaríamos preparados para empezar:

![Foto final](https://github.com/iriagonzalez25/Bases-de-datos-2/blob/master/comando%20final.png) 

## Habilitar comando mysql

La próxima vez que entremos a la terminal, si ponemos el comando mysql nos dirá que no existe, por lo que tenemos que habilitarlo. Para ello, vamos a crear un archivo .bash_profile, utilizando el siguiente comando:

>sudo nano .bash_profile

Se nos abrirá el archivo y le añadiremos la ruta donde tenemos mysql. Guardamos los cambios y cerramos la terminal. Ahora, si la abrimos y ponemos `mysql -u root -p` (tendremos que introducir también la contraseña), ya podremos empezar a trabajar con MySQL:

![Comando mysql habilitado]()




