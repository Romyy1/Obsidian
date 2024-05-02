
Primero de todo hacemos ping a la máquina
![[Pasted image 20230621195318.png]]

Vemos que está conectada, y que tiene una TTL cercana a 64, por lo que estamos frente a una máquina Linux.

Ahora vamos a hacer un escaneo de puertos

![[Pasted image 20230621195441.png]]

![[Pasted image 20230621195459.png]]

Vemos que tiene abierto el puerto 80, cuyo servicio es el http, por lo que veremos una web y vamos a ello.
![[Pasted image 20230621195650.png]]

Esta es la web que nos muestra.

Para hacer la intrusión, vamos a usar Gobuster, y a mayores nos instalamos a partir de GitHub un repositorio en el cual están albergados diferentes usuarios, contraseñas, etc...

![[Pasted image 20230621201312.png]]

Comprobando con algunos de los repositorios no encontramos nada, por lo que vamos a comprobar con algunos de los comunes, como root:root, admin:admin, etc... 

Estos vemos que no funcionan, pero poniendo '# después de admin, vemos que si que nos deja entrar, y es que esto es algo común en las inyecciones SQL, ya que si encontramos un usuario y añadimos '#, nos dejará entrar sea cual sea la contraseña.

![[Pasted image 20230621202050.png]]

