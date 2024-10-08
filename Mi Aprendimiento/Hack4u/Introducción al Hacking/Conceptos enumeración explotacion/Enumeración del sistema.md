
**ANTES DE TODO REVISAR CARPETAS, EN ESPECIAL HOME, OPT Y EN CASO DE SERVIDOR WEB VAR/WWW**

Son los pasos a seguir una vez comprometemos el equipo

LSE-> Linux Smart Enumeration. Es un script que nos ayuda a la hora de hacer la enumeración una vez hemos vulnerado una máquina.

Este script se encuentra en github, y una vez lo tenemos, si lo ejecutamos con -h nos saldrá un menú de ayuda:

![[Pasted image 20240502190352.png]]


Ahora lo ejecutamos tal cual, sin ningún parámetro, ya que por defecto te muestra lo más relevante:

![[Pasted image 20240502190534.png]]

Aquí vemos como nos va mostrando información relevante del sistema, y hay mucha información ya que es un reconocimiento profundo.

**Ahora en procesos más manuales:

Primero hacemos un whoami para ver quienes somos, ya que si somos root no nos interesa indagar en escalar privilegios.

Luego hacemos un id para ver los grupos a los que pertenece el usuario ya que alguno puede ser interesante o puede estar en un grupo docker ya que se pueden jugar con los contenedores para obtener una bash temporal.

Ahora podemos hacer **sudo -l** para ver si tenemos algún privilegio en algún archivo a nivel de sudoers, si nos pidiera la contraseña no podríamos comprobar esto

Después podemos ir a la raíz del sistema y buscar por privilegios suid, ya que si hay algún archivo del que es propietario root y que podemos ejecutar comando de alguna manera, si fuera un script podemos modificarlo y así llegar a obtener una bash, el comando es: **find -perm -4000 -ls 2>/dev/null**

*Python es un ejemplo de binario crítico para poder ser root* Ejemplo:

Si python tiene permisos suid, podemos ejecutarlo siendo cualquier usuario, y haciendo lo siguiente podemos darnos una bash:

- import os (librería de python )
- os.system("whoami") (os.system nos permite ejecutar comandos a nivel de sistema, en este caso nos reportará que somos el usuario corriente con el que hemos accedido ya que es suid, pero se puede cambiar)
- os.setuid(0) (De esta manera nos cambiamos el usuario a root dentro de la terminal de python actual)
- os.system("whoami") (Nos saldrá que somos root)
- os.system("bash") (Nos dará una bash como root)


Podemos observar las capabilities, que son capacidades que pueden darte permiso para ejecutar ciertas tareas privilegiadas. Desde la raíz ejecutamos **getcap -r / 2>/dev/null**. Es similar al anterior, podemos tener python con la capabilitie cap_setuid, lo cual nos deja ejecutar comandos de la misma manera que en el anterior ejemplo, podemos settear el uid con **os.setuid(0)** y de esta manera darnos root en la terminal de python y darnos una bash como root.

También podemos ver las tareas cron que se ejecutan de manera regular en el sistema con el comando  **crontab -l** o con cat /etc/crontab
si podemos tener acceso a alguna de estas tareas y modificar un archivo para darnos una bash ya lo tendríamos.


Con **systemctl list-timers** también podemos ver tareas que se van a ejecutar y el tiempo que quede para que se ejecute.

Existe una herramienta llamada **pspy** que nos permite como atacantes, ver comandos y tareas que se ejecuten con diferentes intervalos de tiempo en el sistema.

Podemos ver procesos del sistema con **ps -faux**. 

**ss -tlnp** para poder ver los puertos abiertos