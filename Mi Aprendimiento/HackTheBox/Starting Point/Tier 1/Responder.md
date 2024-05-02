Primero de todo como siempre comprobamos conectividad con la máquina

![[Pasted image 20230810232205.png]]

Vemos que hay conectividad y en este caso vemos que el ttl es de 127, cercano a 128, por lo que estamos ante una máquina Windows.

Ahora comprobamos los puertos con el siguiente comando

![[Pasted image 20230810232319.png]]

![[Pasted image 20230810232450.png]]

Nos reporta esto, vemos que el puerto 5985 corre el protocolo HTTP también pero este parece estar conectado a un servidor.

Vamos a ver la página web

![[Pasted image 20230810232657.png]]

Nos sale esto, pero como vemos, arriba la IP se cambia por una URL.

Lo que tenemos que hacer es ir a /etc/hosts y añadir abajo la ip de la máquina y a la derecha poner esa url, de esta manera ya nos redireccionara a la web

![[Pasted image 20230810233532.png]]

![[Pasted image 20230810233543.png]]

Una vez dentro de la web usamos Wappalyzer para ver diferente información sobre la web

![[Pasted image 20230810233614.png]]


Vemos que en la web nos da la opción de cambiar el idioma y que esto nos pone que hay un .HTML 

![[Pasted image 20230810234123.png]]

Eso nos quiere decir que lo que hay después del = ejecuta comando, esto es un LFI y gracias a esto podremos colarnos dentro

![[Pasted image 20230810234310.png]]

Si ponemos ../../../../../../../../windows/system32/drivers/etc/hosts y nos lo ejecuta, el LFI se podrá ejecutar

Nos bajamos un recurso de GitHub hecho para esta máquina, es cual es responder.

Lo activamos de la siguiente manera

![[Pasted image 20230810235122.png]]

Y ahora iremos a la web y pondremos lo siguiente **La ip es la vpn**
 
![[Pasted image 20230810235243.png]]

Esto lo que hace es gracias a la herramienta, sube un archivo SMB infectado y lo que nos da lo que activamos antes es lo siguiente

![[Pasted image 20230810235336.png]]

El usuario Administrator y su contraseña hasheada  

De la siguiente manera metemos todo en un archivo txt para su posterior uso

![[Pasted image 20230810235500.png]]

Ahora usando john, que es la app john the ripper, y el archivo rockyou para ver el contenido

![[Pasted image 20230811000034.png]]

(Con -w le proveemos una wordlist)

Nos da lo siguiente 

![[Pasted image 20230811000227.png]]

Y ya vemos como la contraseña de Administrator es badminton

Ahora usaremos una herramienta llamada evil-winrm. WinRM es creado por microsoft para manejar servers de forma remota.

La instalamos y la usamos para acceder

![[Pasted image 20230811000858.png]]

Y ahora una vez hemos accedido buscamos la flag


![[Pasted image 20230811001355.png]]

Encontramos la flag en otro usuario.
