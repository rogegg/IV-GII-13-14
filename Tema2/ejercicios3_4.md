##Ejercicio3
###Apartado a)
Usar debootstrap (o herramienta similar en otra distro) para crear un sistema mínimo que se pueda ejecutar más adelante.

Con la siguiente orden creamos un sistema mínimo con debootstrap, las opciones que le pasamos son: debootstrap [arquitectura] [distribución] [directorio_local] [direccion_remota]

>$ sudo debootstrap --arch=i386 saucy /home/jaulas/saucy/ http://archive.ubuntu.com/ubuntu

![Ejercicio3a](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema2/capturas/ejercicio3a.png)

Vemos el directorio donde tenemos alojado el sistema.

###Apartado b)
Experimentar con la creación de un sistema Fedora dentro de Debian usando Rinse.

A rinse como a debootstrap le pasamos la arquitectura distribución y el directorio donde alojar la jaula. Rinse buscará la distribución en "http://ftp.heanet.ie/pub/fedora/"

>$ sudo rinse --arch=i386 --distribution fedora-core-7 --directory /home/jaulas/fedora/

Vemos unas capturas de la instalación:

![Ejercicio3b1](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema2/capturas/ejercicio3b1.png)

![Ejercicio3b2](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema2/capturas/ejercicio3b2.png)

![Ejercicio3b3](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema2/capturas/ejercicio3b3.png)

##Ejercicio4
Instalar alguna sistema debianita y configurarlo para su uso. Trabajando desde terminal, probar a ejecutar alguna aplicación o instalar las herramientas necesarias para compilar una y ejecutarla.

Ubuntu Saucy instalado en el ejercicio 3 es un sistema basado en debian, vamos a usarlo pero no tenemos total utilidad del sistema ya que proc no está montado.

![Ejercicio3a](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema2/capturas/ejercicio3a.png)

Montando proc
>$ mount -t proc proc /proc

![Ejercicio4a](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema2/capturas/ejercicio4a.png)

También podemos usar git 

![Ejercicio4a2](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema2/capturas/ejercicio4a2.png)


