
- Con 'cat /etc/login.defs | grep 'ENCRYPT_METHOD'  vemos de que manera están encriptadas las contraseñas del /etc/shadow

- Estando como root si hacemos su nombreusuario, accedemos a ese usuario a pesar de no haber iniciado sesión con ese usuario. 

- AWK --> esto nos sirve para hacer búsquedas, por ejemplo si quiero que me printe solo mi ip, podemos hacer ifconfig | tail -n 1 (Con esto le decimos que queremos que nos printe la segunda línea) | awk '{print $2}' , de esta manera nos printará solo la IP ya que es el segundo valor.

- SSH --> Es el nombre de un protocolo y del programa que lo implementa cuya principal función es el acceso remoto a un servidor por medio de un canal seguro en el que toda la información está cifrada.
- *Practicar con overthewire varias veces para practicar todo un poco*

- En hexadecimal, si pones -ps quitas la parte que no interesa y solo deja la hexadecimal.
- Si queremos solo quedarnos con una parte de un archivo y queremos dejarlo en el mismo archivo, si lo redirigimos nos dará error, por lo que hay que jugar con sponge, ejemplo: cat test | awk '{print $3}' | sponge test

	Esto hace que nos muestre el tercer argumento ya que es lo que le pedimos con awk, y con sponge nos mete ese argumento en el mismo archivo sobrescribiendo este

- Locate sirve para buscar un archivo en el sistema que le especifiques, por ejemplo locate .nse 

  -En una búsqueda si usamos wc -l nos muestra el número de líneas que tiene el archivo 

- Si en una búsqueda o lo que sea usamos | grep -v "Lo que queramos quitar" no nos pondrá en pantalla todo lo que tenga relacionado eso que no queremos que aparezca 

- Con wget podemos descargarnos pdf de la web. Luego con exiftool podemos ver información de ese pdf.

- Si por algún motivo no podemos descargar algo de un repositorio, usar: ![[Pasted image 20230920111740.png]]
- Aquí lo que hacemos es poner esos comandos y cambiar tree/master por trunk 