![[Pasted image 20230619105905.png]]

- Dividimos en drwx | r-x | r-x 

- El primer grupo pertenece a los permisos del propietario del archivo, el segundo pertenece al grupo asignado, y el tercer grupo al resto de los usuarios. A la derecha vemos romy  romy, el primero se refiere al propietario del archivo/directorio, en este caso, el propietario romy tiene derecho de lectura (r), escritura (w) y ejecución (x), luego sigue de romy nuevamente, pero este se refiere al grupo al que pertenece, en este caso tiene permisos de lectura (r) y ejecución (x).

- Con chmod cambiamos todos los permisos:

	-o se refiere a otros
	-Con + y - damos o quitamos permisos (Ej: o+w,o+r,etc)
	-g se refiere a grupo
	-También podemos hacerlo en formato binario, rwx(421), si queremos hacer que un grupo tenga todos los permisos pero que el resto solo pueda leer, podemos hacer chmod 575 /home/romy/Desktop/ejemplo.txt

- Podemos crear usuarios con useradd, por ejemplo useradd pepe -s (Le asignamos una shell) /bin/bash -d (Le asignamos un directorio personal de usuario que hemos podido crear previamente) /home/pepe. Luego con passwd pepe asignamos una contraseña a pepe. En este caso, el directorio pepe (/home/pepe) el propiedad de root, para cambiarlo, hacemos chgrp pepe pepe y chown pepe pepe y ya estaría, pero también podriamos haber hecho chown pepe:pepe pepe y ya le decimos que queremos que el propietario sea pepe y en este caso, que el grupo también lo sea.

- Con groupadd creamos nuevos grupos. Para añadir usuarios hacemos usermod -a (mantiene el resto de grupos secundarios en caso de que hubiera) -G (pone el grupo como secundario, no como principal) nombregrupo nombreusuario
- Si hacemos chmod +t solo el propietario puede modificar lo de dentro, ya que +t solo se puede aplicar a directorios

- lsattr --> Sirve para ver los permisos especiales de directorios y archivos.

- chattr --> Sirve para asignar permisos especiales a directorios y archivos (Ej: chattr +i(En este caso le decimos que queremos que sea un archivo inmutable, es decir, que no se pueda eliminar) nombre archivo)

- SUID --> Se asigna poniendo por ejemplo chmod 4755 o chmod u+s. Esto se utiliza para indicar que el que ejecute el archivo, va a tener los mismos permisos que el propietario de este.

- SGID -->  Se asigna poniendo por ejemplo chmod 2755 o chmod g+s. Solo se puede aplicar a nivel de grupo, es decir, que cuando lo apliquemos, el usuario que lo abra, dando igual el grupo en el que esté, tendrá los mismos permisos que el grupo asignado al archivo.

- Capabilities --> Las Capabilities nos permiten gestionar que permisos tiene un proceso para acceder a las partes del kernel. Independientemente del usuario que lo lance. Con getcap nos da los recursos que tienen estas Capabilities, y con setcap las ponemos o las quitamos, con setcap -r la quitamos.



