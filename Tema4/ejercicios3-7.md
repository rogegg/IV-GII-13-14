###Ejercicio3 - Crear imágenes de almacenamiento y manipularlas.

La primera imagen para el amacenamiento virtual vamos a crearla con formato RAW, este formato evita los espacios sin asignar. 

> $ dd of=ddvirtual.img bs=1k seek=5242879 count=0

!["Ejercicio3"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema3/capturas/ej3.png)


Vamos a probar a crear usando otros formatos como VMDK.

> $ qemu-img create -f vmdk ddvirtual2.vmdk 5G

Y a usarlo en una máquina virtual creada desde VirtualBox.

!["Ejercicio3b"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema3/capturas/ej3b.png)

!["Ejercicio3c"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema3/capturas/ej3c.png)

Vemos cómo aparece como unidad de almacenamiento virtual, y su tamaño real es mucho menor que su tamaño virtual.




###Ejercicio4 - Crear uno o vario sistemas de ficheros en bucle.

Los pasos a seguir, como se describe en los apuntes de la asignatura, son los siguientes:
- Crear la imagen.
- Convertir el sistema de ficheros en *loop*.
- Darle formato.
- Montarlo.


> qemu-img create -f raw xfs.img 5M
sudo losetup -v -f xfs.img
sudo mkfs.xfs /dev/loop0
sudo mount /dev/loop0 /mnt/loop0/


NOTA: si no podemos usar mkfs.xfs instalaremos el paquete *xfsprogs*

> sudo apt-get install xfsprogs


Vemos como tenemos montado el sistema /dev/loop0 en /mnt/xfs

!["Ejercicio4"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema3/capturas/ej4.png)



###Ejercicio5 - Instalando Cepth

> $ sudo apt-get install ceph-mds


###Ejercicio6 - Crear un dispositivo Ceph usando BTRFS o XFS

Siguiendo los apuntes tenemos que para crear un dispositivo lo primero que debemos hacer es crear los directorios donde almacenar la información de CEPH

> $ mkdir -p /srv/ceph/{osd,mon,mds}

La configuración de ceph la llevaremos a cabo manualmente creando un fichero de configuración:

> [global]
log file = /var/log/ceph/$name.log
pid file = /var/run/ceph/$name.pid
[mon]
mon data = /srv/ceph/mon/$name
[mon.mio]
host = penny
mon addr = 127.0.0.1:6789
[mds]
[mds.mio]
host = penny
[osd]
osd data = /srv/ceph/osd/$name
osd journal = /srv/ceph/osd/$name/journal
osd journal size = 1000 ; journal size, in megabytes
[osd.0]
host = penny
xfs devs = /dev/loop1


*mio* será el nombre corto que le damos a la máquina y *penny* el nombre local de nuestra máquina.


Creamos el directorio */srv/ceph/osd/osd.0*:

> $ sudo mkdir /srv/ceph/osd/osd.0

Y a continuación creamos el sistema de ficheros indicándole la ruta de nuestro fichero de configuración:

> $ sudo /sbin/mkcephfs -a -c /etc/ceph/ceph.conf

Para iniciar el servicio:

> $ sudo /etc/init.d/ceph -a start

Ya sólo nos queda montarlo con la orden mount en un directorio previamente creado, en este caso */mnt/ceph*:

> $ sudo mount -t ceph penny:/ /mnt/ceph



###Ejercicio7 - Almacenar objetos y directorios usando ceph y rados



