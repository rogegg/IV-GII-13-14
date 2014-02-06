##Ejercicio 1

Para instalar *Chef* vamos a necesitar ruby, por lo que lo primero a instalar en la máquina virtual serán los siguientes paquetes:

	sudo apt-get install ruby1.9.1 ruby1.9.1-dev rubygems

![ejercicio1_installruby](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema6/capturas/ej1_installruby.png)



Chef no se encuentra en los repositorios por lo que para descargarlo lo haremos así:

	curl -L https://www.opscode.com/chef/install.sh | bas
    
![ejercicio1_installchef](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema6/capturas/ej1_installchef.png)    



##Ejercicio2

Chef usa recetas con las que podemos configurar nuestra máquina virtual, para ello necesitamos tener una estructura de directorios como la que sigue:

![ejercicio2_arbol](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema6/capturas/ej2_treeemacs.png)  

Para este ejemplo se va a instalar emacs en la máquina virtual, para ello dentro de la carpeta *cookbooks* tenemos una carpeta *emacs* y dentro *recipes* donde se alojará el fichero *default.rb* que indica cómo instalar emacs.

En la carpeta *cookbooks* tenemos dos ficheros: _node.json_ y _solo.rb_:

- En el fichero **node.json** se usará para indicar qué recetas ejecutar.
- En **solo.rb** indicaremos las rutas necesarias de chef y las rutas de recetas.


Para instalar emacs, nginx y un directorio de trabajo como nos indica el ejercicio tendremosel siguiente árbol de directorios con los siguientes ficheros:

![ejercicio2_arbol](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema6/capturas/ej2_tree.png)  



####nginx
default.rb:

	 package 'nginx' 


####emacs
default.rb:

	 package 'emacs' 


####iv (directorio de trabajo)
default.rb:

	directory '/home/roge/iv'
	file "/home/roge/iv/readme" do
		owner "roge"
		group "roge"
		mode 00544
		action :create
		content "Directorio para la asignatura IV dentro de la máquina virtual"
	end
    
    
    
####node.json

	{
		"run_list": [
			"recipe[emacs]", "recipe[nginx]", "recipe[iv]"
		]
	}	

####solo.rb

	file_cache_path "/home/roge/chef"
	cookbook_path "/home/roge/chef/cookbooks"
	json_attribs "/home/roge/chef/node.json"
    
    

Ahora sólo nos queda lanzar las recetas con chef:

> sudo chef-solo -c solo.rb


![ejercicio2_install](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema6/capturas/ej2_install.png)  


Podemos comprobar que *nginx* y *emacs* están instalados.


![ej2](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema6/capturas/ej2.png)  
