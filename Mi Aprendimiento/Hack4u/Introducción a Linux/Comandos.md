

- 2>/dev/null --> Se utiliza cuando vayamos a ejecutar un comando, en caso de que sea erróneo, no nos mostrará el error y lo enviará directamente al /dev/null, este fichero funciona como agujero negro. Y el 2 lo ponemos porque  así se referencia al stderr, el cual es la definición del error.

- >/dev/null --> Se utiliza '>' para referenciar al stout el cual es el output que nos muestra el comando que estemos introduciendo.

- &>/dev/null --> De esta manera no nos mostrará ni el stout ni el stderr 

- ¿Utilidad de los anteriores comandos? Por ejemplo cuando ejecutemos algún programa (Ej: wireshark), nos mostrará alguna información de la ejecución la cual no nos interesa.

- & --> Si al finalizar los comandos, por ejemplo de ejecución de programas ponemos un &, se nos abrirá en segundo plano y podremos seguir usando sin problema la consola. En este caso nos mostrará un número, el cual es el PID*.

- PID --> Es el número de ejecución que da el sistema para ese proceso, y este número es único.

- disown --> Este comando se pone al final de una ejecución para que sea independiente, es decir, que por ejemplo si ejecuto el wireshark y cierro la consola, este, al ser independiente, no se cierra.

-Descriptores de archivo:

- exec --> Ponemos por ejemplo exec 3 <>file. Esto nos creará un archivo llamado file, el cual tiene permisos de lectura gracias al < y de escritura también gracias al >. Ahora por ejemplo si queremos enviar lo que nos diga un comando, por ejemplo whoami, tenemos que hacer whoami >&3 esto no nos  mostrará nada porque gracias al & si nos da error o output, lo enviará al archivo file que hemos creado, ya que se lo hemos dicho con el 3 ya que tiene asociado este archivo, y con > le hemos dicho que lo pase a esa dirección. Todo lo que pasemos nos lo guardará en la siguiente línea, es decir, si ahora ejecutamos otro comando, lo guardará en la segunda línea.

- exec >&3--> Nos cerrará el descriptor de archivo previamente creado.

- exec 8>&3 --> Nos creará un nuevo descriptor en el 8 como estamos indicando, pero copiará lo que haya actualmente en el descriptor 3. En este caso si añadimos un - al final, nos cerrará el descriptor 3 y nos mantendrá el 8.

//

-file --> Comando independiente al archivo nombrado anteriormente pero se utiliza para ver que tipo de archivo es el que le pasamos.

//


- > --> Sobrescribe el archivo

- >> --> Pone todo en formato compilado, es decir, no sobrescribe si no que lo pone debajo
- -V --> Verbose, es para que cuando ejecutemos un comando nos printe lo que ocurre por detrás 

- xargs --> Se utiliza para usar comandos de forma paralela(Ej: which python3.9 | xargs ls -l).

- -type --> Se usa para especificar un tipo de archivo (d directorio f file)

- find --> Se usa para buscar algo específico en una ruta que indiquemos

- -perm -->Se usa para en el caso de hacer un find, lo que estemos buscando, buscarlo con unos permisos concretos
- -name --> Se usa en el find para especificar un nombre de un archivo o directorio
- -group --> Se usa en el find para especificar el grupo

- Si a la hora de usar el find no recordamos la parte anterior, ejemplo; hay un dexdump.sh, pero no recuerdo bien, hacemos find -name dex\*, y de esta manera me buscará todos los archivos y directorios que comiencen por dex, y si recuerdo el fina funciona de la misma manera, find -name \*ex .