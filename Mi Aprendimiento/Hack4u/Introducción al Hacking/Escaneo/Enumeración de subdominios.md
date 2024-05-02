Con Phonebook.cz ([https://phonebook.cz/](https://phonebook.cz/)) podemos variar entre domains y url ( actúa de la misma manera que Gobuster ) lo que nos permitirá descubrir nuevos dominios. 

Tenemos instalados ctfr y sublist3r en la carpeta opt, pero es más cómodo usar Gobuster .

En Gobuster el modo vhost es para atacar por fuerza bruta, y dir es para buscar directorios dentro de la página

Wfuzz es similar que Gobuster pero más cómoda a priori 

**Tanto en wfuzz como en gobuster podemos usar -t 20 y de esta manera aplicamos 20 hilos para que vaya más rápido, además la herramienta FUZZ es para sustituir las palabras de los diccionarios dentro de la url** 




