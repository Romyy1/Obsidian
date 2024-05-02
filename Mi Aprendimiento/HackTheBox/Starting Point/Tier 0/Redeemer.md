Primero hacemos ping a la máquina para ver si está conectada
![[Pasted image 20230620225908.png]]

Como vemos la máquina está conectada y tiene una TTL de 63, por lo que es una máquina Linux

Ahora vamos a realizar un nmap

![[Pasted image 20230620230001.png]]

En este caso no nos muestra ningún puerto de esta manera, hay que añadir      -p- para que nos muestre todos, a tener en cuenta para ponerlo siempre

![[Pasted image 20230620230422.png]]

Con este escaneo revisamos todo y de forma más rápida, con -p- --open solo nos reportará aquellos puertos que estén abiertos, y con -min-rate 5000 lo que hacemos es mandar 5000 paquetes por segundo para que funcione rápido.

![[Pasted image 20230620230537.png]]

En este caso solo tenemos este puerto abierto, ahora accedemos de la siguiente manera:

![[Pasted image 20230620231327.png]]

Ahora con keys * listamos todas las llaves que haya

![[Pasted image 20230620231954.png]]

Ahora hacemos get flag y nos dará la flag

![[Pasted image 20230620232028.png]]
