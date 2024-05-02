
Con whatweb vemos las tecnologías de detrás de la página, pero también tenemos wappalyzer. Luego podemos usar gobuster o wfuzz para aplicar fuzzing a la web y descubrir directorios y otras páginas.

HTTPS

Las páginas que tienen el candado es que son securas, por lo que son HTTPS, podemos ver el certificado de la página y es por donde podemos ver información.

En el ejemplo de tinder.com vemos que en el nombre del certificado ponen Let´s encrypt, que es para encriptar de forma gratuita. 

También tenemos openssl dentro de la consola y podemos hacer lo siguiente:
![[Pasted image 20231006110736.png]]

Donde veremos información del certificado.

 Otras herramientas son:
![[Pasted image 20231006110829.png]]

![[Pasted image 20231006110847.png]]

Suele ser mejor sslscan ya que nos da información y vemos si es vulnerable a diferentes cosas.

En el ejemplo con docker una vez instalado usamos sslscan y vemos lo siguiente:

![[Pasted image 20231006111234.png]]

Por lo que es vulnerable a heartbleed

![[Pasted image 20231006111626.png]]

Con esto nos aseguramos al 100% de que es vulnerable y vemos que sí.

![[Pasted image 20231006111818.png]]

Usando este script no saldrá información y a veces podremos ver información sobre cookies que nos puede ser útil

