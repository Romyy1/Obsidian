
Protocolo de Transferencia de Archivos (File Transfer Protocol) 

Se pueden dar dos casos, que pongas ftp IP y te puedas conectar como usuario anónimo, o que este usuario este capado y haya que acceder con usuario y contraseña.

Con hydra podemos hacer ataques de fuerza bruta.

![[Pasted image 20231005110946.png]]

Con -l indicamos es usuario, si ponemos -L, es que no sabemos el nombre de usuario y vamos a pasarle un diccionario con opciones, y con las contraseñas si usamos -P le pasamos un diccionario. Con -t le indicamos los hilos, es decir, que queremos que haga x tareas en paralelo, en este caso 15.

