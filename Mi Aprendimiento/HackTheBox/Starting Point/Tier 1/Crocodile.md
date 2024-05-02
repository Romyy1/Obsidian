Primero de todo hacemos un ping a la máquina para ver si tenemos conectividad con esta

![[Pasted image 20230810224921.png]]

Como vemos, la máquina está conectada, también vemos que el ttl es de 63, y es cercano a 64, por lo que estamos frente a una máquina Linux.

Ahora escaneamos los puertos

![[Pasted image 20230810225315.png]]

![[Pasted image 20230810225414.png]]


Como vemos tiene el puerto 80 (HTTP) y el 21 (FTP) abiertos, y vemos como el 21, nos reporta dos archivos con usuarios y contraseñas.

Vamos a ver la web para ver que nos aparece.

![[Pasted image 20230810225626.png]]

Esta es la web que nos reporta la IP.

*Detalle importante*

En el escaneo pone que podemos acceder de forma anónima al FTP

![[Pasted image 20230810225849.png]]

Detalle muy importante mediante el cual podíamos haber sabido que podíamos acceder previamente

![[Pasted image 20230810225952.png]]

Y aquí vemos como hemos accedo fácilmente a la máquina

![[Pasted image 20230810230140.png]]

Con el comando get, visto anteriormente, nos descargamos esos archivos

![[Pasted image 20230810230159.png]]

Aquí los tenemos, y ahora los abrimos

![[Pasted image 20230810230236.png]]

Aquí los tenemos. Intuyo que van "matching", es decir, la contraseña del usuario aron es root y así sucesivamente. La que nos interesa es admin, por lo que voy a probar con admin y esa contraseña

Para el protocolo ftp no tenemos que usar contraseña y usuario, es decir, eso es de otro lado, por lo que vamos a usar el Gobuster para ver otras páginas que no estén puestas y que estén relacionadas con esta web, y usaremos el siguiente comando 

![[Pasted image 20230810231046.png]]

De esta manera le decimos que busque directorios en la siguiente url, usando la wordlist proporcionada y luego con el comando -x le decimos el tipo que directorios que buscamos, en este caso php y HTML (Este proceso tarda)

![[Pasted image 20230810231251.png]]

Ha reportado estas páginas asociadas, la más interesante es la de login.php, ya que podremos usar los credenciales ahí

![[Pasted image 20230810231409.png]]

Nos sale esto, por lo que ahora vamos a probar a entrar con admin


![[Pasted image 20230810231501.png]]

Conseguimos el acceso y tenemos la flag.


