##Ejercicio 3
###Escribir en YAML la siguiente estructura de datos en JSON
###{ uno: &quot;dos&quot;,tres: [ 4, 5, &quot;Seis&quot;, { siete: 8, nueve: [ 10, 11 ] } ] }

En YAML vamos a introducir los miembros de las listas con " - " quedando de esta forma:


	{
    	- uno: "dos"
        - tres: 
        	- 4
            - 5
            - "Seis"
            -
            	- siete: 8
                - nueve:
                	- 10
                    - 11
    
    }

