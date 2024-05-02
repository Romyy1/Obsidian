
Como siempre hacemos primero un ping a la máquina para comprobar que tenemos conectividad con esta:

![[Pasted image 20240427113649.png]]

Como vemos, tiene un ttl de 63, que es cercano a 64 por lo que estamos frente a una máquina Linux.

![[Pasted image 20240427114301.png]]

Hemos modificado un poco el modo de escaneo, de esta manera, no hacemos que nos muestre la información y un escaneo más exhaustivo a todos los puertos, si no que así hacemos que nos muestre todos los puertos y luego una vez tenemos los puertos que están abiertos, los vamos a escanear. Además, con -oG guardamos el escaneo en un archivo llamado allPorts y así tenemos guardado el escaneo por si queremos consultarlo.

![[Pasted image 20240427114523.png]]

Como vemos solo tiene dos puertos abiertos, por lo que vamos a hacer el escaneo más exhaustivo de estos dos puertos.

![[Pasted image 20240427114715.png]]

Ahora lanzamos este comando y lo enviamos a un archivo targeted para guardar la información.

![[Pasted image 20240427114759.png]]

Así de primeras vemos que la versión de ssh es superior a la 7.7 por lo que no es vulnerable a la explotación de nombres de usuarios. Vemos que la ip no nos redirecciona a http://cozyhosting.htb, por lo que vamos a cambiarlo en el /etc/hosts

![[Pasted image 20240427115022.png]]

Y ahora comprobamos la web

![[Pasted image 20240427121327.png]]

Esta es la web, donde vemos un login y demás cosas.

Si usamos gobuster para descubrir otros directorios, vemos lo siguiente:

![[Pasted image 20240427121514.png]]

Si observamos, el /error es raro, ya que el status nos tramita un error desde el backend, si entramos vemos lo siguiente:

![[Pasted image 20240427121553.png]]

Ahora buscamos en internet "Whitelabel error page" y encontraremos que esta web esta hecha con spring boot, y este, puede tener directorios abiertos en los que conseguir información, por lo que hacemos fuzzing de nuevo para ver si encontramos mas información.

![[Pasted image 20240427121717.png]]

![[Pasted image 20240427121727.png]]

El /actuator/sessions parece interesante, y si lo buscamos:

![[Pasted image 20240427121756.png]]

Ya tenemos un usuario y sus cookies de sesion, y con esto podemos acceder a admin.

Ahora entramos a la web habiendo copiado las cookies de sesion y accedemos a inspeccionar y a storage:

![[Pasted image 20240427123003.png]]

Ahora cambiamos las cookies de sesión por las actuales y recargamos dentro de la consola.

![[Pasted image 20240427123042.png]]

Vemos como se ha quitado el login, por lo que ya hemos iniciado sesión y entramos a admin:

![[Pasted image 20240427123114.png]]

![[Pasted image 20240427123126.png]]

Y vemos esto, donde podemos darnos acceso al ssh:

![[Pasted image 20240427123341.png]]

Por mas que lo intentamos nos da error, por lo que vamos a abrirnos burpsuite para interceptar lo que esta pasando.

