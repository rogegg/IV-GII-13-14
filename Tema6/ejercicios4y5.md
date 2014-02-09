##Ejercicio 4

###Desplegar los fuentes de la aplicación de DAI o cualquier otra aplicación que se encuentre en un servidor git público en la máquina virtual Azure (o una máquina virtual local) usando ansible.

Vamos a desplegar la aplicación utilizada en la práctica 3 de esta asignatura. Los fuentes están alojados en el repositorio de github [https://github.com/rogegg/IV_Practica3.git](https://github.com/rogegg/IV_Practica3.git).

Ansible se instala como un módulo de Python, vamos a usar pip para la instalación de módulos.

> sudo pip install paramiko PyPYAML jinja2 httplib2 ansible

- NOTA: si no tienes instalado pip.
	> sudo apt-get install python-pip

Una vez instalado Ansible hay que indicar las máquinas que queremos gestionar. Para ello añadiremos las direcciones de las máquinas a un fichero *inventario* :

> echo "rogeivtema6.cloudapp.net" > ~/ansible\_hosts

Hemos creado un fichero *ansible_hosts* con la dirección de nuestra máquina virtual.

El lugar de este fichero es arbitrario por lo que habrá qeu avisar a Ansible donde se encuentra mediante una variable de entorno:

> export ANSIBLE\_HOSTS=~/ansible\_hosts

Ya tenemos una máquina asociada, probamos si tenemos acceso a ella:

> ansible all -u roge -m ping


- NOTA: Para conectar con la máquina virtual hemos configurado la conexión ssh para no introducir contraseñas. Tendremos que añadir **--ask-pass** si no se ha configurado la máquina remota para poder acceder a ella sin clave.


![ejercicio4_ping](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema6/capturas/ej4_ping.png)




Como podemos ver tenemos conexión con la máquina virtual.

Ya que sólo hemos añadido una máquina al fichero de hosts, al usar la opción *all* sólo hacemos referencia a esa máquina. En caso de tener varias, las agruparíamos para desplegar las aplicaciones.

Ahora ya tenemos todo preparado para el despliegue:
> ansible all -m git -a "repo=https://github.com/rogegg/IV\_Practica3.git dest=~/IV\_Practica3"

Y así hemos descargado de git el repositorio de los fuentes de la aplicación directamente en la máquina virtual.


![ejercicio4_git](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema6/capturas/ej4_git.png)



##Ejercicio 5
###Desplegar la aplicación de DAI con todos los módulos necesarios usando un playbook de Ansible.



Ya que este año no he cursado la asignatura DAI, voy a desplegar la aplicación de la práctica 3.

###### Playbook:

En los playbooks vamos a crear las reglas para instalar los paquetes  y configuraciones necesarias para correr nuestra aplicación. Estos playbooks se encuentran en formato YAML.

[practica3.yml](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema6/mvirtual/ansible/practica3.yml)

Una vez creado el playbook lo lanzamos desde el anfitrión:

> ansible-playbook practica3.yml

![ejercicio5_playbook](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema6/capturas/ej5_yaml.png)

Vemos cómo indica los cambios en naranja y las revisiones que no se han modificado aparecen en verde.

Ya tenemos funcionando la aplicación.

![ejercicio5_app](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema6/capturas/ej5_app.png)


###2. ¿Ansible o Chef?

Al realizar los ejercicios Chef me ha resultado más complejo de aprender y al configurarlo he tenido más problemas. Ansible ha sido más fácil e intuitivo.

Para proyectos en los que vayamos a desplegar varias máquinas de test, desarrollo y producción con una base similar, creo que Ansible nos facilita más el trabajo y nos puede ser más últil que Chef.



