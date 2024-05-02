
Primero de todo hacemos un ping a la máquina
![[Pasted image 20230621203743.png]]

La máquina está conectada y tiene una TTL cercana a 64 por lo que es una máquina Linux.

Ahora vamos a realizar escaneo de puertos.
![[Pasted image 20230621203835.png]]

![[Pasted image 20230621204458.png]]

Como vemos, tiene abierto el puerto 3306 el cual pertenece a SQL.

La versión instalada es MariaDB, la cual es poco segura ya que podemos acceder directamente como root

![[Pasted image 20230621205207.png]]

Ahora miramos todas las tablas etc. Y descubrimos la flag en una de las tablas

![[Pasted image 20230621205356.png]]



