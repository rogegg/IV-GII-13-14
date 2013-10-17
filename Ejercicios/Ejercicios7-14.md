### Ejercicio 7

    1. Crear diferentes grupos de control sobre un sistema operativo Linux. Ejecutar 
    en uno de ellos el navegador, en otro un procesador de textos y en uno último 
    cualquier otro proceso. Comparar el uso de recursos de unos y otros durante un 
    tiempo determinado.

    
	Para la gestión de grupos de control vamos a usar la libreria "libcgroup".

    -> Creamos un grupo llamado "teestoyviendo":

		sudo cgcreate -a roge -g memory,cpu,cpuacct:teestoyviendo

    -> Creamos 3 subgrupos dentro del principal: navegador, editor, explorador:
      
		sudo cgcreate -g memory,cpu,cpuacct:teestoyviendo/navegador
		sudo cgcreate -g memory,cpu,cpuacct:teestoyviendo/editor
		sudo cgcreate -g memory,cpu,cpuacct:teestoyviendo/explorador
      
    -> Una vez creados los subgrupos, lanzamos la aplicación desde su correspondiente:
      
		sudo cgexec -g memory,cpu,cpuacct:teestoyviendo/navegador firefox
		sudo cgexec -g memory,cpu,cpuacct:teestoyviendo/editor gedit
		sudo cgexec -g memory,cpu,cpuacct:teestoyviendo/explorador nautilus
  
	-> Consultamos los resultados en los archivos correspondientes. En la carpeta cpuacct encontramos el tiempo 
	   consumido por la CPU:
		
		cat /sys/fs/cgroup/cpuacct/teestoyviendo/navegadores/cpuacct.stat
		cat /sys/fs/cgroup/cpuacct/teestoyviendo/navegadores/cpuacct.usage
		cat /sys/fs/cgroup/cpuacct/teestoyviendo/navegadores/cpuacct.usage_percpu
		
	-> El archivo cpuacct.stat nos muestra el tiempo consumido por el sistema y por el usuario.
	-> El archivo cpuacct.usage nos muestra el tiempo consumido por la CPU.
	-> El archivo cpuacct.usage_percpu nos muestra el tiempo consumido por cada CPU, en este caso tenemos dos.
   
	-> Tabla comparativa de varios procesos:



 | Nautilus | Firefox | Gedit
----- |----- | ----- | -----
cpuacct.stat | user: 43893 system: 22668 | user: 1804 system: 290 | user: 111 system: 2
cpuacct.usage | 779684786842 | 21310284946 | 1147859936
cpuacct.usage_percpu |CPU0: 393322866912 CPU1: 386540802436 | CPU0: 11361191987 CPU1: 9949177200 | CPU0: 312070552 CPU1: 835789384



### Ejercicio 8
	2. Implementar usando el fichero de configuración de cgcreate una política que dé menos prioridad a los procesos 
	   de usuario 	que a los procesos del sistema (o viceversa).

	La configuración se realiza mediante la edición de los dos archivos siguientes:
		/etc/cgconfig.conf 
	Utilizado por libcgroup para definir los grupos de control, sus parámetros y puntos de montaje.
		/etc/cgrules.conf
	Utilizado por libcgroup para definir los grupos de control a la que pertenece el proceso. 

	La configuración de <<cgconfig.conf>> tendrá la siguiente forma:
		group <name> {
			[permissions]
			<controller> {
				<param name> = <param value>;
				...
			}
			...
		}
	La configuración de <<cgrules.conf>> tendrá la siguiente forma:
		<user>	<controllers>	<destination>


	Ejemplo:
	 - Fichero cgconfig.conf
		group usuarios{
			perm{
				task{
					uid = pepe;
					gid = pepe;
				}
				admin {
					uid = root;
					uid = root;
				}
			}
			cpu{
				cpu.shares=10;
			}
		}

		mount{
			cpu = /dev/cgroups/cpu;
			cpuacct = /dev/cgroups/cpuacct;
		}

	 - Fichero cgrules.conf
		pepe	cpu		usuarios/
	
	El grupo "usuarios" utilizará el 10% de la CPU.
	El uso de la CPU por parte del usuario "pepe" utilizará las configuraciones del grupo "usuarios".
	


### Ejercicio 9
	Comprobar si el procesador o procesadores instalados lo tienen. ¿Qué modelo de procesador es?
	¿Qué aparece como salida de esa orden?
	
>!["Modelo del procesador"](https://raw.github.com/rogegg/IV-GII-13-14/master/Ejercicios/Ejercicio9.png)

	Como podemos ver en la captura de pantalla el modelo de procesador es:
		Pentium(R) Dual-Core CPU T4200 @ 2.00GHz
		
	También podemos ver que al realizar la orden 
		egrep '^flags.*(vmx|svm)' /proc/cpuinfo
	no nos muestra ningún resultado, por lo que este modelo de procesador no posee la tecnología VT-x de Intel

	
### Ejercicio 10
	Comprobar si el núcleo instalado en tu ordenador contiene este módulo del kernel usando la orden kvm-ok.


>!["kvm-ok"](https://raw.github.com/rogegg/IV-GII-13-14/master/Ejercicios/ejercicio10.png)

	En la captura podemos ver que al ejecutar la orden el resutado es:
		INFO: Your CPU does not support KVM extensions
		KVM acceleration can NOT be used
	Lo que nos indica que no está soportado por la cpu.



### Ejercicio 11
	Comentar diferentes soluciones de Software as a Service de uso habitual.

Link al *"issues"* [aquí](https://github.com/IV-GII/GII-2013/issues/11)


### Ejercicio 12
	Instalar un entorno virtual para tu lenguaje de programación favorito (uno de los mencionados arriba, obviamente).

	Hemos instalado *virtual env para Python*. Para ello desde el terminal:
		$sudo apt-get install python-virtualenv python-dev
	Para crear un espacio para trabajar:
		$virtualenv mi_proyecto
	Y para activar el entorno:
		$cd mi_proyecto
		$source bin/activate
	Vemos como el prompt cambia, lo que nos indica que ya está activado.

*fuentes: http://www.virtualenv.org/en/latest/*
*http://rukbottoland.com/tutoriales/tutorial-de-python-virtualenv/*

### Ejercicio 13

### Ejercicio 14
