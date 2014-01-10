###Ejercicio2
En la siguiente captura vemos las interfaces puente creadas al arrancar el contenedor. Vemos que al parar el contenedor esa interfaz puente desaparece.

> $ brctl show

!["Ejercicio2"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema3/capturas/ej2.png)

> Interfaz: vethhdUXeK
> Puente: 8000.fe2659b716ab



###Ejercicio3
###3.1. Contenedor basado en Debian.
Creamos un contenedor con ubuntu-cloud y lo llamaremos "nubecilla", similar a la que se usa en EC2 de Amazon, un sistema más ligero que Ubuntu.

> $ sudo lxc-create -t ubuntu-cloud -n nubecilla

!["Ejercicio3_1"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema3/capturas/ej3_1.png)

Como vemos en la captura el contenedor está arrancado y funcionando.


###3.2. Contenedor basado en otra distribución.

Vamos a crear un contenedor con el sistema fedora. Para ello igual que en el paso anterior usamos "lxc-create":

> $ sudo lxc-create -t fedora -n fedora

!["Ejercicio3_2"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema3/capturas/ej3_2.png)


Arrancamos el contenedor llamado fedora:

> $ sudo lxc-start -n fedora
> user:root
> password: root

!["Ejercicio3_2a"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema3/capturas/ej3_3.png)

Y ya tenemos en funcionamiento nuestro contenedor con el sistema Fedora.



###Ejercicio4
###4.1
Vamos a instalar lxc-webpanel y usarlo para gestionar las máquinas virtuales que hemos instalado.

> ¡OJO!Debemos ser root para la instalación y actualización:

Para instalar automáticamente:

> $ wget http://lxc-webpanel.github.io/tools/install.sh -O - | bash

Para actualizar automáticamente:

> $ wget http://lxc-webpanel.github.io/tools/update.sh -O - | bash

!["Ejercicio4_1a"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema3/capturas/ej4_1a.png)

Nos conectamos desde el explorador de internet a:

> http://localhost:5000/

!["Ejercicio4_1b"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema3/capturas/ej4_1b.png)

Usuario: admin		Contraseña: admin

!["Ejercicio4_1c"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema3/capturas/ej4_1c.png)

Vemos como aparecen nuestras máquinas virtuales nubecilla y fedora, creadas anteriormente con lxc.

Fuente: [http://lxc-webpanel.github.io/install.html](http://lxc-webpanel.github.io/install.html)


###4.2
Vamos a limitar la máquina virtual por ejemplo de nubecilla.

Vemos como desde el webpanel se nos permite limitar el uso de la cpu y memoria.


!["Ejercicio4_2"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema3/capturas/ej4_2.png)



