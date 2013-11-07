
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






