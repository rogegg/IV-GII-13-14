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
  
	-> Consultamos los resultados en los archivos correspondientes. 
	En la carpeta cpuacct encontramos el tiempo consumido por la CPU:
		
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
