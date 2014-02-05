###Ejercicio 1

Para instalar *Chef* vamos a necesitar ruby, por lo que lo primero a instalar en la máquina virtual serán los siguientes paquetes:

	sudo apt-get install ruby1.9.1 ruby1.9.1-dev rubygems

![ejercicio1_installruby]()



Chef no se encuentra en los repositorios por lo que para descargarlo lo haremos así:

	curl -L https://www.opscode.com/chef/install.sh | bas