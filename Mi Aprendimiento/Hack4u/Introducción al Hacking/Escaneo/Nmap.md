
Se utiliza para ver los puertos que hay abiertos dentro de los 65535 que existen. 

Con route -n vemos la ip que tiene nuestro router, en este caso lo usaremos para coger la ip y escanearla para ver que puertos tiene abiertos.

![[Pasted image 20230830110002.png]]

En este caso la IP es 192.168.0.1

*Información de puertos*

Un puerto puede estar abierto o filtrado, filtrado quiere decir que por varias cosas no puede decirnos si está abierto o no.

**Parámetros**

-p -> Con este parámetro especificamos los puertos que queremos escanear 

![[Pasted image 20230830110203.png]]

Por ejemplo con ese parámetro le decimos que queremos solo los 100 primeros puertos 

![[Pasted image 20230830110311.png]]

De esta manera englobamos todo el rango de puertos

![[Pasted image 20230830110340.png]]

En cambio si solo lo ponemos así, solo nos enumerará los 1000 más comunes 

![[Pasted image 20230830111034.png]]

Con este parámetro le decimos que queremos buscar entre los 500 puertos más comunes. Nmap tiene un listado con los puertos más comunes, en este caso le decimos que coja los 500 primeros de esa lista.

![[Pasted image 20230830111324.png]]

Añadiendo esto le decimos que solo queremos que nos filtre los puertos abiertos, los filtrados no.
//
-v --> Este parámetro se usa para que nos vaya poniendo información según la vaya encontrando.
//

![[Pasted image 20230830111636.png]]

Al ver eso vemos que nos está aplicando resolución de DNS, lo cual ralentiza mucho el escaneo y a priori no lo necesitamos.

La resolución de DNS es para que no tengamos que buscar las cosas a través de su IP, si no que podemos buscarlas por su nombre.

![[Pasted image 20230830111910.png]]

//

-T --> Esto aplica una plantilla de temporizado para que lo haga más rápido. Van desde el 0 hasta el 5, donde 1 es un escaneo más sigiloso y 5 el cual es el modo loco, va más rápido.

![[Pasted image 20230830112356.png]]

//


-sT --> Esto lo que hace es aplicar el modelo Three-Way Handshake. Enviamos un SYN, nos puede contestar con un RST en caso de que un puerto este cerrado, pero si no, nos contesta con un SYN/ACK que quiere decir que igual está abierto y luego emitir un ACK de vuelta para ver que tenemos conectividad.

//

-Pn --> Se usa para que de base de por hecho que el host está activo y no tiene que hacer descubrimiento de hosts.

//

Para hacer un escaneo por UDP y no por TCP como hemos estado haciendo es manteniendo todo pero poniendo -sU 

![[Pasted image 20230830114319.png]]

Es un escaneo más lento que por TCP

//

Un escaneo en local va a ser más rápido que a un tercero.

//

-O --> Lo usamos para ver la información del sistema operativo.

No recomendable porque hace muchas peticiones por detrás y es lento.

// 

-sV --> Con este parámetro averiguamos el servicio y versión de los puertos 



