
Es una plataforma de **contenedores** de software que permite crear, distribuir y ejecutar aplicaciones en entornos aislados.

Es como una máquina dentro de otra máquina para probar según que cosas.

En caso de hackeo del contenedor, solo te hackean eso, no la máquina "original", además en ese caso se puede volver a un backup del contenedor.

Una imagen de docker es un archivo que contiene todo lo necesario para que una aplicación se pueda ejecutar en un contenedor.

**Comandos docker**

- **FROM**: se utiliza para especificar la imagen base desde la cual se construirá la nueva imagen.
- **RUN**: se utiliza para ejecutar comandos en el interior del contenedor, como la instalación de paquetes o la configuración del entorno.
- **COPY**: se utiliza para copiar archivos desde el sistema host al interior del contenedor.
- **CMD**: se utiliza para especificar el comando que se ejecutará cuando se arranque el contenedor.

![[Pasted image 20230918155647.png]]

Ejemplo de estructura básica donde le decimos que queremos un ubuntu de la última versión y que la persona que lo va a mantener soy yo, añado mi aka y un correo electrónico.

Una vez creado, hacemos lo siguiente:

![[Pasted image 20230918160116.png]]

Aquí le decimos que vamos a construir un docker, que lo vamos a llamar my_first_image, **IMPORANTE** El nombre el minúsculas para que no de error, y ponemos un . para que busque dentro de donde estamos situados. 

**IMPORTANTE** Es importante que el archivo que se llame Dockerfile tal y como esta escrito, si no puede darnos error.

Con docker images, vemos las imágenes docker que tenemos.
![[Pasted image 20230919111213.png]]
**Por cada cambio que hagamos tenemos que hacer un docker build**

Con docker run arrancamos el contenedor 

-d --> Corre el docker en segundo plano

-i --> Le decimos que sea interactivo 

-t --> Le decimos que disponga de una consola virtual para poder interactuar

--name --> Le damos el nombre que queramos

![[Pasted image 20230919111454.png]]

Lo que vemos abajo es el identificador del docker

Con docker ps vemos el docker que esta activo

![[Pasted image 20230919111528.png]]

![[Pasted image 20230919111612.png]]

De esta manera accedemos al docker, donde ponemos bash podemos poner el comando que queramos ejecutar, pero de esta manera nos da una consola.

**De base no viene nada instalado y hay que instalar todo lo que necesitamos** 

Pasos:

-apt update
-apt install net-tools -y 
-apt install aputils-ping
-Salimos y vamos al Dockerfile y ponemos lo siguiente para que lo aplique y se instale todo lo aplicado 
![[Pasted image 20230919112202.png]]

![[Pasted image 20230919112409.png]]
Hacemos el build para que lo aplique y ponemos :v2 para que en versión ponga v2.

***Algunos comandos***

Para parar un contener docker stop id del docker

docker ps -a --> Es un registro de los dockers tanto abiertos como cerrados

Para borrar los contenedores --> docker rm id del docker --force

Para borrar alguna imagen --> docker rmi id de la imagen 


![[Pasted image 20230919114134.png]]

Añadimos eso para crear un servidor por el puerto 80 nada más iniciemos la imagen




