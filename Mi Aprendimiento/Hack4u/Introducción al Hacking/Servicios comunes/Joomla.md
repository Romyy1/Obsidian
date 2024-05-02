
Para escanear tenemos joomscan que es un script hecho en pearl

![[Pasted image 20231022124430.png]]

Lo activamos de esta manera, y con -u le indicamos la URL.

La parte más importante del reporte es la del Core Joomla, ya que aquí nos reporta todas las vulnerabilidades que hay:

![[Pasted image 20231022124527.png]]

Algo muy interesante es que nos abre una carpeta en reports donde nos pone la información que ha sacado, en la última línea nos indica donde se ubica

![[Pasted image 20231022124720.png]]

![[Pasted image 20231022124754.png]]

Ahora para ver el html podemos hacer lo siguiente:

-Primero creamos un servidor Python en mi caso pero puede ser en php también en el puerto 8081:

![[Pasted image 20231022124924.png]]

![[Pasted image 20231022125002.png]]

Accediendo nos sale esto y abrimos el html:

![[Pasted image 20231022125018.png]]

Nos lo representa así, y es más cómodo para ver mejor la información o reportarlo mejor a la hora de un auditoría.

