
Comenzamos con el ping para ver la conectividad con la máquina
![[Pasted image 20240506195321.png]]

El ttl es cercano a 64 por lo que es una máquina Linux.

Ahora procedemos a hacer el reconocimiento con nmap, y primero vamos a utilizar el siguiente conjunto de comandos:

![[Pasted image 20240506195642.png]]

Lo hemos cambiado, esta vez no nos muestra la versión ni un escaneo exhaustivo para así tenerlo más limpio, además de que hemos pasado el escaneo a un archivo de formato grepeable el cual usaremos para obtener copiados los puertos que queremos solo.

![[Pasted image 20240506195740.png]]

Como vemos solo tiene dos puertos abiertos, ahora usamos un escaneo más profundo

![[Pasted image 20240506195826.png]]

Primero nos copiamos los puertos con el anterior script y ahora ejecutamos

![[Pasted image 20240506195930.png]]

Y nos lo pasamos a un archivo para así tener la info en todo momento.


![[Pasted image 20240506200023.png]]

Aquí tenemos la info, puntos importantes:

- Versión de SSH mayor a la 7.7, por lo que no podemos enumerar usuarios ,por ahí
- Tiene una redirección a una web que no funciona por lo que lo meteremos en /etc/hosts

![[Pasted image 20240506200215.png]]

Ahí lo tenemos metido ya y ahora abrimos la web en busca de información.

![[Pasted image 20240506200310.png]]

Esto puede ser interesante ya que a lo mejor podemos meter código por este lado.


![[Pasted image 20240506200347.png]]

Estas son las tecnologías que utiliza la web, a priori no llama nada la atención.

En el código fuente no hay nada interesante, por lo que vamos a utilizar gobuster para buscar directorios.

![[Pasted image 20240506200636.png]]

![[Pasted image 20240506200811.png]]

Nos da estos resultados, y si intentamos entrar en cualquiera, nos sale lo siguiente:

![[Pasted image 20240506200840.png]]

No encontramos nada, pero vamos a activar burpsuite para ver la información que tramita cuando enviamos la información en el anterior cuadro que hemos visto.

No hace nada, pero debajo encontramos esto también:

![[Pasted image 20240506201428.png]]

Probamos también y a priori no vemos nada.

Hay posibilidad de que haya subdominios en la web, por lo que vamos a probar de nuevo con gobuster pero esta vez buscando subdominios

Nos hemos tenido que instalar las Seclists para poder hacerlo correctamente.

![[Pasted image 20240506203357.png]]

Ahora ejecutamos este comando para descubrir vhost

![[Pasted image 20240506210530.png]]

*No ha funcionado el descubrimiento de vhost es captura de un video*

La pagina cambia mucho, y en el codigo fuente encontramos:

![[Pasted image 20240506210642.png]]

Podemos tener un posible usuario ahí, cassiopeia.

Ahora volvemos a buscar directorios en este nuevo subdominio.

![[Pasted image 20240506210958.png]]

Vemos que nos reporta muchos directorios que antes no, y resalta uno llamado plugins.

Si vemos el wappalyzer veremos lo siguiente:


![[Pasted image 20240506211457.png]]

Es una página que esta creada por joomla, por lo que podemos intentar hacer la intrusión por ahí.

Vamos a utilizar joomscan.

![[Pasted image 20240506211801.png]]



Nos ha reportado esto, nos indica que hay un txt que podemos utilizar y vamos a verlo, y de paso también vemos la página de administradores de joomla:

![[Pasted image 20240506211940.png]]

Y ahora el robots.txt:

![[Pasted image 20240506211959.png]]


Buscamos más info de robots.txt

No hemos encontrado más pero se nos ha olvidado lo más importante, la versión de joomla, si buscamos la versión 4.2.6 de joomla, hay un exploit ( CVE-2023-23752  ).

Hay un fallo en el que al añadir a la url lo siguiente:

api/index.php/v1/config/application?public=true

Buscamos información relevante:

![[Pasted image 20240506215954.png]]

Y ahí vemos user y contraseña

Ahora vamos a intentar entrar en joomla:

![[Pasted image 20240506220137.png]]

Y estamos dentro.

![[Pasted image 20240506220233.png]]

Y vemos que además somos administradores.

Ahora si nos vamos a system y entramos a site templates veremos lo siguiente:

![[Pasted image 20240506220902.png]]

Y si entramos:

![[Pasted image 20240506220926.png]]

Vemos scripts que se pueden ejecutar, si modificamos alguno para que nos de una reverse shell, podremos entrar, en este caso voy a intentar entrar a través de error.php

Vamos a intentar ejecutar comando a través de burpsuite.

Primero metemos el siguiente código en error.php para poder ejecutar código:

![[Pasted image 20240506222639.png]]

Y ahora vamos al burpsuite desde dev.devvortex y lo mandamos al repeater (CTRL+R):

Y en la parte del GET añadimos lo siguiente:

![[Pasted image 20240506222854.png]]

Después del = va el código que queramos ejecutar, ahora nos abrimos un puerto y nos mandamos una bash poniéndonos por escucha en un puerto en nuestra máquina:

![[Pasted image 20240506223118.png]]

Ahora vamos al burpsuite y hacemos click derecho y cambiamos la petición a POST y ejecutamos lo siguiente:

![[Pasted image 20240506224248.png]]

Y si vamos a nuestro puerto en escucha:

![[Pasted image 20240506224305.png]]

Ya tenemos conectividad.

Ahora tenemos que tratar la bash:

![[Pasted image 20240506224512.png]]

Hacemos CTRL + Z

![[Pasted image 20240506224601.png]]

![[Pasted image 20240506224624.png]]

![[Pasted image 20240506224712.png]]

![[Pasted image 20240506224915.png]]

Y con esto ya tendríamos la shell perfecta.


Ahora vamos a ver datos de la base de datos que está en el archivo configuration.php, y con less podemos buscar y ver mejor la información:

![[Pasted image 20240506225349.png]]

Vemos que los datos que vimos antes también y vamos a conectarnos ala base de datos:


![[Pasted image 20240506225454.png]]

Y estamos en la base de datos.

![[Pasted image 20240506225535.png]]


Usamos la tabla joomla:

![[Pasted image 20240506225706.png]]

La parte que dice users le echamos un ojo:

![[Pasted image 20240506225733.png]]

Ahora guardamos esta información en un txt:

![[Pasted image 20240506231008.png]]

Y utilizamos hashcat y el rockyou para descrifrar:

![[Pasted image 20240506231130.png]]

He utilizado el tipo 3200 porque se parecía más el código que al resto

Y aquí tenemos una:

![[Pasted image 20240506231251.png]]

Seguramente sea la de logan ya que la otra ya la tenemos.

Y ahora vamos a intentar conectarnos por ssh:

![[Pasted image 20240506231422.png]]

Y estamos dentro.

Ahora vemos que logan tiene permisos de root para ejecutar el siguiente archivo:

![[Pasted image 20240506232101.png]]

Y si buscamos en internet encontramos que apport-cli tiene una inclusión con la que nos dará una bash de root ( CVE-2023-1326 )

Hay otra manera que sería la siguiente:

![[Pasted image 20240506232750.png]]

Ejecutamos la anterior linea y luego ponemos lo siguiente:

![[Pasted image 20240506232804.png]]

Y ahora le damos al 5 y luego a la V

![[Pasted image 20240506232912.png]]

Y nos dejará ejecutar una bash

![[Pasted image 20240506232943.png]]

Y ya somos root.



















