###Ejercicio6
###Instalamos juju

Para instalar juju vamos a seguir los pasos indicados en ["https://juju.ubuntu.com/docs/config-local.html"](https://juju.ubuntu.com/docs/config-local.html). Esto es:

Añadimos los repositorios de la versión estable de juju:

> $ sudo apt-add-repository ppa:juju/stable
> $ sudo apt-get update

Instalamos juju:

> $ sudo apt-get install juju

Configuramos juju para usar como local:

> $ juju generate-config
> $ juju switch local

!["Ejercicio6_1"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema3/capturas/ej6_1.png)


NOTA: Para trabajar en local hace falta instalar MongoDB

###Instalamos Mysql en un táper.

Creamos un táper e instalamos mysql:

> $ sudo juju bootstrap
> $ sudo juju deploy mysql

Si vemos el estado de juju, vemos cómo en la máquina por defecto encontramos el servicio Mysql, lo podemos ver en la siguiente captura:

!["Ejercicio6_2"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema3/capturas/ej6_2.png)


###Ejercicio7
###Destruir toda la configuración creada anteriormente.

Para desmontar los servicios hay que hacerlo en orden inverso a su creación, primero hay que destruir las unidades y luego las máquinas.

> $ sudo juju destroy-unit mysql/0
> $ sudo juju destroy-machine 1

###Crear la máquina anterior con mediawiki y una relación entre ellos.


Volvemos a iniciar una máquina e instalamos mediawiki, mysql y la relación entre ellos:

> $ sudo juju deploy mysql
> $ sudo juju deploy mediawiki
> $ sudo juju add-relation mediawiki:slave mysql:db

La exponemos para su uso publico:

> $ sudo juju expose mediawiki


###Crear un script

> #!/bin/bash
> juju add-machine
> juju deploy mediawiki
> juju deploy mysql
> juju add-relation mediawiki:slave mysql:db
> juju expose mediawiki


###Ejercicio8

Vamos a instalar libvirt, para ello:

> $ sudo apt-get install kvm libvirt-bin

Necesitamos añadir el usuario que va a trabajar con las máquinas virtuales al grupo:

> $ sudo adduser $USER libvirtd




###Ejercicio9
Instalar un contenedor usando >virt-install< .
Para ello en la consola:

> $ sudo virt-install --name flash-linux --ram 512 
> --disk path=/home/flash-linux,size=4 
> -c /home/roge/Descargas/flashlinux-0.3.4-RC2.iso

Donde como parámetros indicamos el nombre de la máquina virtual creada, la memoria ram en bytes utilizada, el lugar donde se va a alojar y el tamaño en gygabytes que le asignaremos, por último el lugar donde se encuentra la iso de la distribución que vamos a utilizar, en este caso una distribución ligera de linux (flash-linux).


!["Ejercicio9"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema3/capturas/ej9.png)