###Ejercicio1
Para crear un espacio de nombres para montaje, donde se aislan los recursos declarados con mount:
>$ sudo unshare -m /bin/bash 

Para montar una iso:

>$ mount -o loop /home/roge/tails-i386-0.20.1.iso /mnt/montaje/

Dejamos una captura por aquí.

!["Ejercicio1"]()



###Ejercicio2
El único puente que tenemos es el creado durante la lectura de los ejercicios como prueba. Vemos que no existía otro puente antes.

!["Ejercicio2a"]()

Hemos creado un interfaz virtual, pero no se ha podido enlazar con la conexión wifi. Por lo que se ha asignado a la tarjeta de red eth0.

!["Ejercicio2a"]()