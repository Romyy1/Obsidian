
**Payload staged** -> Envían el payload ( nuestra carga útil ) de manera fragmentada. Suelen ser menos estables. El payload es más pequeño y más fácil de transmitir y más difícil de detectar. Pueden ser personalizados y por ello son más flexibles.

Ejemplo:

* *Para este ejemplo hay una máquina windows desplegada

![[Pasted image 20231115115247.png]]

Con -p le indicamos la plataforma en la que vamos a trabajamos, meterpreter/reverse_tcp es un ejemplo de carga fragmentada. -f exe es para que sea ejecutable y -o para indicarle que quiero que lo envíe como reverse.exe. LHOST le indico que el localhost sea mi IP y LPORT le indico el puerto local que quiero usar.

Suele salir un error, para que no salga hay que añadir --platform windows -a x64 y quedaría lo siguiente:

![[Pasted image 20231115115953.png]]

Y ya tendríamos el ejecutable.

Ahora creamos un server con python en cualquier puerto que no sea el del ejecutable creado.

Ahora en la máquina víctima tendríamos que meternos en el servidor creado con python y descargarnos el .exe creado.

Ahora en nuestra máquina atacante usamos metasploit:

![[Pasted image 20231115120243.png]]

Y creamos el listener ahora:

![[Pasted image 20231115120909.png]]

Ahora especificamos el payload usado en msfvenom

![[Pasted image 20231115120957.png]]

Le damos a show options para ver que podemos hacer:

![[Pasted image 20231115121049.png]]

Y ahora lo modificamos poniendo los parámetros que hemos puesto nosotros en el archivo reverse.exe 
![[Pasted image 20231115121141.png]]

En LHOST poner la IP que pusimos en el archivo y en LPORT el puerto especificado.

Y ahora ejecutamos:

![[Pasted image 20231115121408.png]]

Y nos saldrá lo siguiente:

![[Pasted image 20231115121428.png]]

Esto quiere decir que ya está en escucha. 

Ahora volvemos a la máquina víctima y ejecutamos el reverse.exe que le pasamos. Ejecutamos de todas formas, ya que nos avisará windows de que es un archivo peligroso, y veremos como que no pasa nada, pero si volvemos a nuestro parrot a la ventana donde teníamos el metasploit veremos lo siguiente:

![[Pasted image 20231115121624.png]]

Como vemos tenemos acceso a la máquina.

Lo cómodo de metasploit es que podemos hacer capturas de pantalla de la máquina y se guardan en nuestra máquina atacante:

![[Pasted image 20231115121913.png]]

Ahí vemos la ruta donde ha guardado la screenshot, y para ejecutarlo y ver la captura sería:

![[Pasted image 20231115122011.png]]

También podemos ver en tiempo real la máquina con screenshare.

A mayores podemos meterle un keylogger:

![[Pasted image 20231115122118.png]]

Y si ahora por ejemplo abrimos un blog de notas en la máquina víctima y escribimos, podremos verlo :

![[Pasted image 20231115122253.png]]

Se usó la tecla windows para buscar y luego buscamos bloc y dimos enter y posteriormente se escribió "Hola esto es una prueba"

-----------------

**Payload non-staged** -> Envían el payload ( nuestra carga útil ) de una sola vez, es más largo y no siempre funciona. El payload es más grande y se envía de una vez, por lo que es más rápido.

Ejemplo:

![[Pasted image 20231115122605.png]]

Si nos fijamos, la diferencia es que aquí a la hora de usar -p, no usamos /meterpreter/reverse_tcp, si no que lo hacemos directamente con meterpreter_reverse_tcp. *Recordamos que -p era para especificar la plataforma con la que vamos a trabajar*

El resto funcionaría igual, ya que solo cambia a la hora de entablar conexión con el servidor.

Si quisiéramos hacerlo con netcat sería:

![[Pasted image 20231115123026.png]]

La diferencia es que en vez de meterpreter, usamos shell, para que directamente nos de una shell, ya que con meterpreter nos daría cosas raras, ya que no está adaptado para trabajar con netcat si no solo con meterpreter de metasploit.

El resto sería igual, pero en vez de abrir metasploit usaríamos netcat:

![[Pasted image 20231115123305.png]]

Ahora ejecutamos el archivo en la máquina víctima y veríamos la consola:

![[Pasted image 20231115123403.png]]

Para tener una consola más interactiva y usar ctrl+L por ejemplo, usaríamos rlwrap una herramienta que tendríamos que instalar y se usaría:

![[Pasted image 20231115123505.png]]

Y así podríamos usar ya diferentes utilidades, como ctrl+L o inicio entre otras, pero si usamos ctrl+C se no cierra.




