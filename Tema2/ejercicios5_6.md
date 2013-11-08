
#Ejercicio 5
###Instalar una jaula chroot para ejecutar el servidor web de altas prestaciones nginx.

Instalamos una jaula como ya hicimos en ejercicios anteriores, en este caso instalaremos una distribución mínima de quantal con arquitectura 32 bits

>$ sudo debootstrap --arch=i386 quantal /home/jaulas/nginx/ http://archive.ubuntu.com/ubuntu



Añadimos un usuario que accederá a la jaula al ingresar en el sistema.

>$ sudo useradd -s /bin/bash -m -d /home/jaulas/nginx/./home/rogegg -c "Raring roge" -g users rogegg



Instalamos el servidor web de altas prestaciones nginx.

>$ sudo apt-get install nginx

![Ejercicio5a](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema2/capturas/Ejercicio5a.png)

Iniciamos el servicio de nginx y comprobamos que está instalado con curl, que nos permite ejecutar aplicaciones web y nos va a permitir ver la plantilla de ejemplo de nginx.

>$ sudo service nginx start

>$ curl localhost


![Ejercicio5b](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema2/capturas/ejercicio5b.png)



#Ejercicio6
###Crear una jaula y enjaular un usuario usando `jailkit`, que previamente se habrá tenido que instalar.

Para instalar jailkit lo descargamos de la página:

>http://olivier.sessink.nl/jailkit/index.html#download

Nos vamos al directorio de la descarga y procedemos a su instalación con la siguiente secuencia:

>$ ./configure

>$ make

>$ sudo make install


Ahora creamos un sistema de ficheros "poseído" por root:

>$ sudo mkdir -p /seguro/jaulas/dorada

>$ sudo chown -R root:root /seguro



Ahora vamos a iniciar jailkit con:

>$ jk_init -v -j /seguro/jaulas/dorada jk_lsh basicshell netutils editors

>-v  (verbose) nos muestra los mensajes.

>-j  indicamos la ruta de la jaula.

>Los siguientes comandos son alias de lo que se va a instalar en la jaula.


![Ejercicio6a](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema2/capturas/ejercicio6a.png)


Esta jaula se puede usar directamente con chroot, pero jailkit también permite enjaular usuarios. Creamos el usuario y lo asignamos a nuestra jaula.

>$ sudo adduser pepe

>$ sudo jk_jailuser -m -j /seguro/jaulas/dorada pepe

![Ejercicio6b](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema2/capturas/ejercicio6b.png)



Aunque este usuario existe en la jaula, no se podrá conectar con el shell limitado que tiene. Habrá que editar la configuración del usuario (que estará en /seguro/jaulas/dorada/etc/passwd) y cambiar jk_lsh por /bin/bash, el shell habitual.


![Ejercicio6b](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema2/capturas/ejercicio6c.png)



Para conectarnos como el usuario creado y enjaulado haremos:

>$ ssh pepe@localhost
