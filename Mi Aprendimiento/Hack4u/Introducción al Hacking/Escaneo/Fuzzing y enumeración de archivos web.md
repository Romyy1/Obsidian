
Para averiguar rutas diferentes dentro de la web, podemos pasar el ratón por encima de algunas rutas dentro de la web y abajo a la izquierda nos saldrá la url.

Gobuster es una herramienta que nos ayuda a buscar archivos, directorios, etc, lo utilizamos previamente en la enumeración de subdominios. La diferencia es que para enumerar subdominios utilizamos vhost, y en este caso usaremos dir.

Un ejemplo seria:

gobuster dir -u https://miwifi.com -w /usr/shares/SecLists/web-content/directory-list-2.4-medium-txt -t 200 ( *Pueden ser demasiados hilos, algunas veces si nos da error hay que disminuir a, por ejemplo, 50* ) Si queremos añadir barras al final de lo que nos salga, simplemente es añadir --add-slash. Para que solo nos pongan las direcciones que tengan un código de estatus 200, es decir, exitoso, añadimos -b 403,404 el 403 ( *Es que nos deniegan el acceso* ) es el que más sale, pero si solo ponemos ese da un error y hay que añadir el 404. Si queremos especificar extensiones, usamos -x y podemos poner php, html, txt entre otras, pero son de las más usadas 


Otra herramienta en wfuzz, si ponemos -c nos pondrá colores para que sea más visual, -t 200 para especificar los hilos, -w para poner el diccionario y luego ponemos directamente la url pero con una diferencia, donde queremos fuzzear, hay que poner fuzz, ejemplo: https://miwifi.com/FUZZ esto lo que hará es cambiar FUZZ por palabras del diccionario. Para ocultar los códigos 404 hay que poner --hc=404,403 

***Importante***
Una vez acabemos el wfuzz, hay que usar kill %. Esto se usa para matarlo y que pare, esto se hace a parte del ctrl+C. 

Si vemos que la página tiene ids listando productos, podemos mirar los que hay de la siguiente manera: wfuzz -c -t 200-z range,1-20000 https://mi.com/shop/buy/detail?product_id=FUZZ 

Con phonebook.cz también podemos ver diferentes subdominios y archivos web. Pero es más interesante usar wfuzz o gobuster

**Burpsuite**

Actúa como intermediario para que las consultas pasen por burpsuite y ver como se envían las solicitudes y registrar todas las consultas.

Una vez lo abrimos tenemos que ir a la pestaña donde dice proxy, de base está seteado en escucha y hay que quitarlo. De base escucha por el puerto 8080. Con la extensión foxyproxy, añadimos el proxy de burpsuite. Una vez lo conectemos y recarguemos, veremos información en donde dice target y veremos toda la información que va por detrás, y si volvemos a activar en proxy el modo escucha con intercept, y recargamos, veremos más información.
