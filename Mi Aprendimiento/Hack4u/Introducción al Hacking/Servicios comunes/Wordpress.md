
Wordpress tiene un fallo y es que cuando estamos en el wp-admin y ponemos un usuario y una contraseña cualquiera, si la contraseña está mal, nos dirá que la contraseña para ese usuario es incorrecta, lo que nos dice que el usuario si que existe.

En el buscador si ponemos localhost:31337/?autor=0 nos reportará los diferentes autores que puede haber, esto solo funciona si está todo por defecto y no se ha modificado demasiado.

Para enumerar usuarios podemos usar searchsploit wordpress user enumeration. Esta herramienta está vinculada con la web de exploit-db.com donde hay un montón de exploits interesantes. 
![[Pasted image 20231019093830.png]]

![[Pasted image 20231019094111.png]]


En este caso hemos encontrado algo pero que solo es para versiones inferiores a la 4.7.1, y nosotros tenemos la 5.3, por lo que no podemos aplicarla

Si nos hubiera sido útil, podriamos hacer searchsploit -x y poner el identificador que aparece a la derecha, en este caso 41497.

La herramienta wpscan nos ayudará a hacer un escaneo a un wordpress.

![[Pasted image 20231019094621.png]]

Con esto nos reportará un informe del wordpress.

![[Pasted image 20231019095019.png]]

Si le añadimos esto, le decimos que queremos que nos numere usuarios y plugins vulnerables.

![[Pasted image 20231019095206.png]]

Como vemos nos ha encontrado otro usuario que no habíamos contemplado previamente, para comprobarlo podemos intentar acceder en wp-admin y ver si nos dice que la contraseña es errónea.

![[Pasted image 20231019095828.png]]

Con esto añadimos nuestro api token tras habernos registrado en wpscan y así nos dará más información

![[Pasted image 20231019100053.png]]

Como vemos nos brinda diferente información para que podamos acceder a los exploits directamente o a información para poder informarnos simplemente.

![[Pasted image 20231019100446.png]]

Con curl y haciendo grep por plugins, podemos ver en el código fuente los diferentes plugins que hay, esta es otra manera de ver los plugins que tiene instalados

![[Pasted image 20231019100552.png]]

![[Pasted image 20231019101144.png]]

Con este atajo de curl nos reportará solo los nombres de los plugins y no todo lo que vemos arriba.

Con grep -oP es para hacer una búsqueda específica, con \K le decimos que no queremos que ponga el plugins/  y con [ ^/ ] le decimos que nos reporte hasta la siguiente barra y el + para que nos ponga todo.

![[Pasted image 20231019101516.png]]

Con este lo que hacemos es añadir sort -u para que no nos printe repeticiones.

Ahora con la herramienta searchsploit buscamos por ejemplo para el warfare y vemos lo siguiente:
![[Pasted image 20231019101815.png]]

En este caso solo nos interesa el de wordpress.

![[Pasted image 20231019102319.png]]

Con xmlrpc.php podemos hackearlo, ya que hay una manera de numerar credenciales válidas
![[Pasted image 20231019102401.png]]

En este caso vemos que sí

![[Pasted image 20231019102505.png]]

Con esto nos responde con un error ya que lo que quiere es una estructura de xml.

Ahora lo que hacemos es buscar exploits del xmlrpc.php de wordpress

En este caso teníamos que pasarle archivos xml para que nos reportara las cosas. Hemos creado un archivo xml con el contenido que decía la página y hemos hecho el siguiente comando:
![[Pasted image 20231019103228.png]]

Y esto nos devuelve información de directorio donde si existen, podremos enumerar los usuarios.

![[Pasted image 20231019103342.png]]

En este caso si que está y es este archivo.

****La web que estoy usando es: https://nitesculucian.github.io/2019/07/01/exploiting-the-xmlrpc-php-on-all-wordpress-versions/**

Ahora vamos a aplicar fuerza bruta con otro xml que hemos extraído de la web, y hemos puesto de usuario romy y contraseña romy

![[Pasted image 20231019103806.png]]

Como vemos, o contraseña o usuario es incorrecto, pero en este caso sabemos que es la contraseña porque el usuario lo hemos reportado previamente en el wp-admin y era correcto.

![[Pasted image 20231019103921.png]]

Si probamos la contraseña correcta nos saldrá esto.

Ahora vamos a hacer un script para poder sacar la contraseña en caso de no saberla.

![[Pasted image 20231019115020.png]]

Este es el script creado.

También funciona con wpscan

![[Pasted image 20231019115134.png]]

Esta manera es muchísimo más facil e intuitiva.



