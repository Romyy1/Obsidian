*Primero habría que haber realizado un ping para ver que la máquina estaba conectada*
Hemos realizado con un nmap con lo siguiente: 
![[Pasted image 20230620221801.png]]


El escaneo nos ha mostrado la siguiente información


![[Pasted image 20230620221710.png]]

Vemos que el puerto 21 está abierto, este corresponde al servicio FTP.

Donde pone "Anonymous", este se refiere que podemos entrar de forma anónima sin necesidad de contraseña por lo que hacemos lo siguiente:

*Teniendo instalado el ftp previamente*

![[Pasted image 20230620222911.png]]

De esta manera nos conectamos al servicio

*La ip es diferente porque lo cerré y lo volví a abrir*

Con ls vemos que ahí está la flag

![[Pasted image 20230620223238.png]]

Y ahora con get nos la descargamos de la siguiente manera

![[Pasted image 20230620223329.png]]

Ahora nos salimos y vamos hacemos cat al archivo y vemos la flag

![[Pasted image 20230620223407.png]]