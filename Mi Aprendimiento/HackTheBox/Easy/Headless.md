
![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513190650.png]]

Ttl cercana a 64 por lo que es máquina Linux.

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513190847.png]]

Ahora buscamos más información acerca de los puertos.

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513191145.png]]

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513191201.png]]

Parece como que podemos acceder a alguna página web por el puerto 5000, además de que tenemos la cookie de admin al parecer.

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513191253.png]]

Nos aparece esto en la web.

Si le damos a for questions nos aparece para subir algo pero no hace nada, vamos a hacer fuzzing y buscar directorios.

Encontramos esto:

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513192000.png]]

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513192010.png]]


Podemos intentar ver algo con burpsuite.

No vemos nada a priori, pero retomando el for questions, al parecer se puede ejecutar código en la parte del mensaje:

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513192744.png]]

Podemos hacerlo de la siguiente manera:


![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513192915.png]]

Esto se debe a que si lo interceptábamos con Burpsuite, veríamos que el código se intercepta, y ahí podemos ejecutar un XSS para darnos una bash.

Al parecer, como nos han dado la cookie de admin, podemos ejecutar código con ese comando gracias a fetch ya que se comunica con el servidor, y utilizando, con document.cookie la cookie de admin que teníamos.

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513193241.png]]

Nos ha salido esto, y tenemos que abrir burpsuite para que funcione correctamente y cambiamos parámetros:

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513194217.png]]

Cambiamos a POST y ponemos el código que estábamos intentando en donde dice User-Agent.

Cambiamos porque no teníamos todo al completo, y enviamos una nueva petición:

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513194529.png]]

Y la mandamos al repeater y volvemos a intentar de la siguiente manera:


![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513195154.png]]


![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513195204.png]]

Y vemos como nos ha dado la cookie de admin, ahora vamos a intentar entrar en el dashboard con ella.

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513195300.png]]

Y estamos dentro.

Si le damos a generate report sale esto:

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513195348.png]]


Ahora vamos a interceptar la petición con burpsuite.

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513195540.png]]

Y ahora desde aquí podemos ejecutar código para darnos una bash.

Pero vamos a crear un shell.sh para poner ahí el código y subir el código mediante curl o wget.

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513195946.png]]


![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513200045.png]]


![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513200324.png]]

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513200340.png]]

Ahí ya hemos metido la shell.sh y ahora nos abrimos el puerto 443 y ejecutamos:

Ahora funcionará de la siguiente manera, sin hacer falta el shell.sh que hemos creado:

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513202405.png]]

Ahora estamos dentro, y vemos que tenemos permiso de sudo para ejecutar syscheck, y que tiene lo siguiente:

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513203154.png]]

Ese init.db es intersante, y no aparece cuadno hacemos ls, podemos crearlo y mandarnos una bash:

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513203407.png]]

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513204755.png]]

Le damos permisos de ejecución

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513204818.png]]

Ejecutamos syscheck y ahora:

![[Obsidian/Mi Aprendimiento/Imagenes/Pasted image 20240513204834.png]]

Ya somos root.






