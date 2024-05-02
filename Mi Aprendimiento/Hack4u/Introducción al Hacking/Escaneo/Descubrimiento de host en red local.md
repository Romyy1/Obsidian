
- nmap -sn iprouter/máscarared  

- Con arp-scan -I ens33 --localnet (ens33 es solo si cuando hacemos ifconfig, nuestra ip aparece en ens33) si añadimos --ignoredups nos ignora los duplicados

- Con masscan hacemos una búsqueda de hosts y de puertos a gran escala en menos tiempo, esto nos permite descubrir hosts diferentes que no habíamos visto previamente.