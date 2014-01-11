###Ejercicio8 - Instalar las herramientas de línea de órdenes de Azure

Una vez creada una cuenta en Azure vamos a instalar las herramientas necesarias.

Vamos a seguir las indicaciones que nos da [Windows Azure](http://www.windowsazure.com/en-us/documentation/articles/xplat-cli/) para las instalaciones.

Vamos a necesitar *npm*, por lo que lo instalaremos desde los repositorios:

> $ sudo apt-get install npm

Una vez terminado podemos pasar a instalar el cliente de azure:

> $ sudo npm install azure-cli

!["Ejercicio8"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema4/capturas/ej8a.png)


NOTA: En mi caso tuve problemas con la instalación de  azure, ya que la versión de nodejs parece que no era la adecuada, reinstalé nodejs desde el siguiente repositorio:

> $ sudo add-apt-repository ppa:chris-lea/node.js

> $ sudo apt-get update

> $ sudo apt-get install nodejs

NOTA2: En la versión 12.10 de ubuntu (como es mi caso) necesité actualizar los siguientes paquetes:

> $ sudo apt-get install python-software-properties

> $ sudo apt-get install software-properties-common


Pdemos ver que está instalado:

> $ azure

!["Ejercicio8"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema4/capturas/ej8c.png)


Acabada la instalación del cliente, sus dependencias y recomendaciones tendremos que descargar la configuración de publicación de la cuenta:

> $ azure account download

Se nos abrirá el explorador para iniciar sesion en windows azure y nos descargará el archivo de configuración *Azpad\*.publishsettings*

Lo importamos:

> $ azure account import ~/Azpad*.publishsettings

!["Ejercicio8"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema4/capturas/ej8d.png)


Vemos como aparece *account import command OK* y comprobamos que la cuenta está importada.

> $ azure account list

!["Ejercicio8"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema4/capturas/ej8e.png)

Ahora nos queda crear una cuenta de almacenamiento y como ubicación seleccionaremos Europa.

> $ azure account storage create ivirtual

Si necesitamos las claves de dicha cuenta, las obtendremos así:

> $ azure account storage keys list ivirtual


También podemos verla desde el panel web de Windows Azure

!["Ejercicio8"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema4/capturas/ej8f.png)


###Ejercicio9 - Crear varios contenedores en la cuenta usando a línea de órdenes.


Creamos un contenedor para las imágenes:

> $ azure storage container create contenedorimg -p blob

!["Ejercicio9"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema4/capturas/ej9a.png)


Ahora vamos a subir las capturas al contenedor:

> $ azure storage blob upload ej9a.png contenedorimg ej9a.png

Podemos acceder a él desde la dirección.
[http://ivirtual.blob.core.windows.net/contenedorimg/ej9a.png](http://ivirtual.blob.core.windows.net/contenedorimg/ej9a.png)

Y también podemos ver la imagen dentro del contenedor en el web panel:

!["Ejercicio9"](https://raw.github.com/rogegg/IV-GII-13-14/master/Tema4/capturas/ej9b.png)


###Ejercicio10



