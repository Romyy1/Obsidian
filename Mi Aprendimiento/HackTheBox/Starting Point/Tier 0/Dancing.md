*SMB --> (Server Message Block) Protocolo de red que permite compartir archivos, impresoras, etc... Entre nodos de una red de ordenadores que usan Windows*
Primero de todo hacemos ping a la máquina

![[Pasted image 20230620223714.png]]

Como vemos en este caso la TTL es de 127, próximo a 128, por lo que estamos ante una máquina Windows.

Realizamos un escaneo con nmap de la siguiente manera:

![[Pasted image 20230620223941.png]]

En este caso nos ha mostrado los siguiente puertos:

![[Pasted image 20230620224019.png]]

En este caso, nos interesa el puerto 445, aunque el protocolo smb usa tanto el 139 como el 445.

Ahora con smbclient, vamos a listar los contenidos de la máquina de la siguiente manera

![[Pasted image 20230620224440.png]]

En este caso, WorkShares no precisa de contraseña para entrar, por lo que lo utilizaremos para acceder de la siguiente manera

![[Pasted image 20230620225258.png]]

Como vemos ya hemos accedido, ahora vamos a listar lo que tiene y vamos investigando

![[Pasted image 20230620225436.png]]

Ahora vamos viendo cada ruta hasta encontrar la flag

![[Pasted image 20230620225535.png]]

Como vemos estaba en el directorio "James.P", por lo que salimos y vemos la flag
![[Pasted image 20230620225618.png]]


