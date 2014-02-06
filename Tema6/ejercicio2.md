###Ejercicio 1

Para instalar *Chef* vamos a necesitar ruby, por lo que lo primero a instalar en la máquina virtual serán los siguientes paquetes:

	sudo apt-get install ruby1.9.1 ruby1.9.1-dev rubygems

![ejercicio1_installruby](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema6/capturas/ej1_installruby.png)



Chef no se encuentra en los repositorios por lo que para descargarlo lo haremos así:

	curl -L https://www.opscode.com/chef/install.sh | bas
    
![ejercicio1_installchef](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema6/capturas/ej1_installchef.png)    



###Ejercicio2

Chef usa recetas con las que podemos configurar nuestra máquina virtual, para ello necesitamos tener una estructura de directorios como la que sigue:

![ej2_arbol]()

Para este ejemplo se va a instalar emacs en la máquina virtual, para ello dentro de la carpeta _cookbooks_ tenemos una carpeta _emacs_ y dentro _recipes_ donde se alojará el fichero _default.rb_ que indica cómo instalar emacs.

En la carpeta _cookbooks_ tenemos dos ficheros: _node.json_ y _solo.rb_.

- node.json se usará para indicar qué recetas ejecutar.
- En solo.rb indicaremos las rutas necesarias de chef y las rutas de recetas.



