
Pertenecen al protocolo SMB

Se usan \\\\ porque hay que usar el doble que de normal, ejemplo:

http://wer.com/sln

Aquí solo utilizamos dos primero y luego una, en SMB hay que doblarlas, es decir:

\\\\\\\\10.10.10.10\\\\hola 

para acceder usamos:

smbclient \\\\172.17.0.2\\ jon -U jon%seacercaelinvierno

luego para ver que hay, usamos dir o ls

IMPORTANTE ACCEDER COMO ROOT PARA QUE NOS DEJE OBTENER LAS COSAS

