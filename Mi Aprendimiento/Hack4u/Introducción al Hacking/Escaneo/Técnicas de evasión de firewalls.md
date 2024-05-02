Un firewall es un sistema de seguridad de red que controla el trafico de red entrante y saliente en función de reglas determinadas.

//

-f --> Cuando manda un paquete lo manda de forma fragmentadas. Con esto podemos ver puertos que de primeras aparecían filtrados o no aparecían y con esto podemos ver que realmente estaban abiertos.

--mtu --> Se usa poniendo --mtu acompañado de un numero múltiplo de 8. De esta manera especificamos el tamaño de los paquetes que queremos mandar. 

//

**-D**--> Permite al usuario enviar paquetes falsos junto con los paquetes reales a la red para confundir a los sistemas de detección de intrusos y evitar la detección del firewall. Va acompañado de una IP que pongamos manualmente.

//

**--source-port**--> Con esto lo que hacemos es que el puerto por el que nos comunicamos a la hora de hacer el escaneo lo especificamos nosotros.

//

Hay firewalls que tienen un listado de un número de length y que reconocen que pueden estar siendo escaneados, con el comando **-data-length** acompañado de un número, modificamos el length para que sea diferente y evadir esos listados.

//

--spoof-mac -->Esta técnica de evasión se basa en **cambiar la dirección MAC** del paquete para evitar la detección del Firewall. Nmap permite al usuario configurar manualmente la dirección MAC para evitar ser detectado por el Firewall. 

//

-sS --> Es el escaneo más sigiloso a la par que rápido. Esto lo que hace es que el Three-Way Handshake es diferente, ya que es SYN -> RST(cerrado) | SYN/ACK (abierto) -> RST, es decir, que si esta abierto, no mandamos un ACK al final, si no que lo cierra directamente para dejar las menos huellas posibles

//

--min-rate --> Controlas el total de paquetes que vas a enviar, lo normal es poner 5000 ya que es bastante ágil y preciso.

//

Escaneo común:

nmap -p- --open -sS --min-rate 5000 -v -n -Pn **IP** 

//

-sC --> Manda unos determinados scripts básicos de reconocimiento que nos pueden brindar más información.

*Ejemplo* --> ftp-anon.nse  busca si está habilitado el usuario anonymous en un ftp 

-sV --> Nos brinda la versión de por ejemplo apache.

//

--script --> le especificamos que tipo de scripts queremos usar, por ejemplo: 
--script="vuln and safe"
**Cada script tiene una categoría** , encontramos unas 14 categorías, pero las 5 más comunes son las siguientes 5:

-Default

-Discovery

-Safe

-Intrusive

-Vuln 