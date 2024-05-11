**BurpSuite** es una herramienta de prueba de penetración utilizada para encontrar vulnerabilidades de seguridad en aplicaciones web. Es una de las herramientas de prueba de penetración más populares y utilizadas en la industria de la seguridad informática. BurpSuite se compone de varias herramientas diferentes que se pueden utilizar juntas para identificar vulnerabilidades en una aplicación web.

Las principales herramientas que componen BurpSuite son las siguientes:

- **Proxy**: Es la herramienta principal de BurpSuite y actúa como un intermediario entre el navegador web y el servidor web. Esto permite a los usuarios interceptar y modificar las solicitudes y respuestas HTTP y HTTPS enviadas entre el navegador y el servidor. El Proxy también es útil para la identificación de vulnerabilidades, ya que permite a los usuarios examinar el tráfico y analizar las solicitudes y respuestas.
- **Scanner**: Es una herramienta de prueba de vulnerabilidades automatizada que se utiliza para identificar vulnerabilidades en aplicaciones web. El Scanner utiliza técnicas de exploración avanzadas para detectar vulnerabilidades en la aplicación web, como inyecciones SQL, cross-site scripting (XSS), vulnerabilidades de seguridad de la capa de aplicación (OSWAP Top 10) y más.
- **Repeater**: Es una herramienta que permite a los usuarios reenviar y repetir solicitudes HTTP y HTTPS. Esto es útil para probar diferentes entradas y verificar la respuesta del servidor. También es útil para la identificación de vulnerabilidades, ya que permite a los usuarios probar diferentes valores y detectar respuestas inesperadas.
- **Intruder**: Es una herramienta que se utiliza para automatizar ataques de fuerza bruta. Los usuarios pueden definir diferentes payloads para diferentes partes de la solicitud, como la URL, el cuerpo de la solicitud y las cabeceras. Posteriormente, Intruder automatiza la ejecución de las solicitudes utilizando diferentes payloads y los usuarios pueden examinar las respuestas para identificar vulnerabilidades.
- **Comparer**: Es una herramienta que se utiliza para comparar dos solicitudes HTTP o HTTPS. Esto es útil para detectar diferencias entre las solicitudes y respuestas y analizar la seguridad de la aplicación.

Se trata de una herramienta extremadamente potente, la cual puede ser utilizada para identificar una amplia variedad de vulnerabilidades de seguridad en aplicaciones web. Al utilizar las diferentes herramientas que componen BurpSuite, los usuarios pueden identificar vulnerabilidades de forma automatizada o manual, según sus necesidades. Esto permite a los usuarios encontrar vulnerabilidades y corregirlas antes de que sean explotadas por un atacante.


Ahora vamos a hacer ejemplos sobre el manejo de burpsuite, utilizaremos un docker en el que se puede practicar SQLI para verlo.

Para abrir burpsuite es mejor abrirlo así:

![[Pasted image 20240509192323.png]]

El proxy de burpsuite por defecto siempre esta en el puerto 8080:

![[Pasted image 20240509192423.png]]

Esto nos sirve para interceptar las peticiones y ver la información gracias al foxyproxy que nos cambia el proxy para ver todo.

Hemos hecho un ejemplo en la web de intercepción de un login y esto es lo que nos ha llegado al apartado proxy de burpsuite:

![[Pasted image 20240509192648.png]]

Ahora usamos CTRL+R para remitirlo todo al repeater.

El repeater siempre lo vamos a utilizar para tener una traza de la petición y poder jugar con ella:

![[Pasted image 20240509192814.png]]

Podemos cambiar el nombre para que en caso de tener varias pestañas, diferenciarlas entre sí.

**Si cancelamos la petición cambiando a intercept is off, esta fluirá** 

Ahora podemos movernos a target:

![[Pasted image 20240509193129.png]]

Aquí vemos todo el historial de peticiones el cual se ha borrado.

Ahora podemos ir a scope dentro de target y veremos lo siguiente:

![[Pasted image 20240509193320.png]]

Ahora podemos poner un scope si le damos a add dentro de "include in scope"

![[Pasted image 20240509193424.png]]

Nos sale esta pequeña ventana y contemplamos la url que queremos auditar, en este caso localhost:8000

Ahora si nos movemos por la web y vamos a target de nuevo, en el site map veremos lo siguiente:

![[Pasted image 20240509193647.png]]

Aquí vemos todas las peticiones que se han ido haciendo, y si hacemos click en las peticiones que vemos a la izquierda desplegadas, veremos la información de cada petición en el medio, y vemos también la respuesta que han dado esas peticiones.