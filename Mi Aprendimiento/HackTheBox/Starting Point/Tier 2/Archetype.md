
Lo primero de todo comprobamos conectividad con la máquina y ejecutamos el nmap :

![[Pasted image 20231102110226.png]]

Ttl de 127, por lo que es máquina Windows.

![[Pasted image 20231102110316.png]]


![[Pasted image 20231102111031.png]]
![[Pasted image 20231102111047.png]]

![[Pasted image 20231102111503.png]]

Nos conectamos por smb y con eso parámetros nos saldrán las carpetas que hay y con -N le decimos que no hay contraseña. En este caso, a  la carpeta backups puede entrar cualquiera, ya que no tiene el símbolo $.

Nos conectamos a la carpeta:

![[Pasted image 20231102111952.png]]

Hacemos intro en la password ya que no la necesitamos, y nos llevamos con get el archivo que hay:

![[Pasted image 20231102112031.png]]

Y hacemos cat del archivo:

![[Pasted image 20231102112046.png]]

Y vemos como pone password y ID, y aprovecharemos esto para entrar.

Para poder entrar, al MSSQL server, hay una herramienta llamada Impacket que incluye un script en python que nos va a ayudar a entrar.

Para poder usar la herramienta se usa la carpeta impacket que se encuentra en /usr/bin , y dentro de esta está examples, que es donde se encuentran los scripts de python. En nuestro caso vamos a usar el siguiente:

![[Pasted image 20231102114352.png]]

Y le indicamos la contraseña:

![[Pasted image 20231102114409.png]]

Y ya hemos entrado
Ahora vamos a ejecutar los siguiente comandos:
![[Pasted image 20231102114717.png]]


Con este comando comprobamos el rol que tenemos en la base, en este caso tenemos el rol de admin.

Ahora vamos a comprobar si xp_cmdshell esta activado:
![[Pasted image 20231102114831.png]]

Vemos que no, por lo que vamos a activarlo:

![[Pasted image 20231102114945.png]]

Primero esto y después lo siguiente:

![[Pasted image 20231102115017.png]]

Ahora podemos ejecutar comandos desde la db:

![[Pasted image 20231102115100.png]]

Ahora vamos a subir un binario para conseguir una shell estable:

Nos descargamos el archivo y nos abrimos un servidor en python y nos ponemos en escucha por el puerto 443:

![[Pasted image 20231102115500.png]]

![[Pasted image 20231106210945.png]]

Primero ejecutamos esto y después lo siguiente:

![[Pasted image 20231106211010.png]]

Y ahora ya tenemos una shell:

![[Pasted image 20231106211023.png]]


Y ahora tenemos que ejecutar lo siguiente:

![[Pasted image 20231106211342.png]]

Ahora ejecutamos winPEASx64.exe y al final vemos lo siguiente:

![[Pasted image 20231106212116.png]]

El historial de la consola, y ahí encontramos lo siguiente:

![[Pasted image 20231106212136.png]]

Admin y su contraseña, y a mayores si buscamos en el Desktop de este usuario encontramos la flag de user:

![[Pasted image 20231106212215.png]]

Ahora para entrar como admin tenemos que usar otro script de impacket de la siguiente manera:

![[Pasted image 20231106212247.png]]

Ponemos la contraseña y entramos, y en el escritorio de Administrator tenemos la flag de root:

![[Pasted image 20231106212318.png]]








