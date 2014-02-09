##Ejercicio 6
###Instalar una máquina virtual Debian usando Vagrant y conectar con ella.

Tras instalar Vagrant:


elejimos una de las imágenes de la lista [www.vagrantbox.es](www.vagrantbox.es):

En nuestro caso
> http://dl.dropbox.com/u/40989391/vagrant-boxes/debian-squeeze-i386.box

Inicializamos la imagen con:

> vagrant box add debian http://dl.dropbox.com/u/40989391/vagrant-boxes/debian-squeeze-i386.box

> vagrant init debian




![ejercicio6_install](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema6/capturas/ej6_install.png)


Lanzamos la máquina:

> vagrant up


Nos conectamos: 

> vagrant ssh


![ejercicio6_run](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema6/capturas/ej6_run.png)

