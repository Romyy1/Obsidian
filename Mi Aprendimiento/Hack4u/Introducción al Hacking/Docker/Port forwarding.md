
Nos permite **redirigir el tráfico de red** desde un puerto específico en el host a un puerto específico en el contenedor. Esto nos permitirá acceder a los servicios que se ejecutan dentro del contenedor desde el exterior.

![[Pasted image 20230919114318.png]]

![[Pasted image 20230919114348.png]]

![[Pasted image 20230919114549.png]]

Añadiendo esto lo que hacemos es que en el build no interactúe ya que puede dar problemas

![[Pasted image 20230919114747.png]]

Con -p 80:80 le decimos que queremos que nuestro puerto 80 sea el puerto 80 del docker

![[Pasted image 20230919115037.png]]

De esta manera vemos como el puerto 80 del docker es nuestro puerto 80

![[Pasted image 20230919115112.png]]

Y de esta manera también lo vemos en nuestra máquina

![[Pasted image 20230919115155.png]]

Y si vemos el localhost de nuestra máquina, vemos que el apache del docker, entonces en caso de reconocimiento y hackeo por el puerto 80, accederían al docker.

![[Pasted image 20230919120105.png]]

Con esto en el run lo que hacemos es montar la carpeta que ponemos antes de los puntos en la que está después. Si en el docker cambiamos el contenido, también se cambia en nuestra máquina.





