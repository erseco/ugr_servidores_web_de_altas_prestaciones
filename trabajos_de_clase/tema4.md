
# SWAP - Ejercicios Tema 4

### Ejercicio 4.1. Buscar información sobre cuánto costaría en la actualidad un mainframe. Comparar precio y potencia entre esa máquina y una granja web de unas prestaciones similares.

Normalmente ya no se suelen utilizar mainframes como tal (multiprocesador), se suelen usar nodos (multicomputadores) pues son mas tolerantes a fallos, mas faciles de ampliar y demás, aun así haciendo una pregunta a quora nos devuelve que un mainframe básico IBM puede costar alrededor de 75.000 dólares.

### Ejercicio 4.2. Buscar información sobre precio y características de balanceadores hardware específicos. Compara las prestaciones que ofrecen unos y otros.

Por lo que hemos visto suelen rondar los 500 euros los mas básicos y nos ofrecen todo lo que nos ofrece un switch/router con el añadido del balanceo

Lancom LANCOM 1611+ lancom lancom 1611+voip ready vpn router, firewal 568,55 €
Load balance traffic in HTTP, FTP, DNS, SIP, RTSP, POP/IMAP, etc.,
Load balance SSL traffic,
Define a "weight" for each of your servers or VM,
Configure monitoring sensors,
Manage NAT/DNAT for your Virtual rack,
View statements and performance with SNMP.

Kemp Loadmaster 2200 Lm-2200 Servidor Carga Balanceador De - 523,95 €
Load balance traffic in HTTP, FTP, DNS, SIP, RTSP, POP/IMAP, etc.,
Load balance SSL traffic,
Define a "weight" for each of your servers or VM,
Configure monitoring sensors,
Manage NAT/DNAT for your Virtual rack,
View statements and performance with SNMP.

### Ejercicio 4.3. Buscar información sobre los métodos de balanceo que implementan los dispositivos recogidos en el ejercicio 4.2

Todos los vistos implementan por lo menos roun-robin y la gran mayoría de los vistos en teoría, algunos balanceadores CISCO tienen algoritmos propios de balanceo

### Ejercicio 4.4. Instala y configura en una máquina virtual el balanceador ZenLoadBalancer.

Descargamos la iso de la community edition desde https://sourceforge.net/projects/zenloadbalancer/files/latest/download la instalamos e instalamos el sistema, que está basado en Debian GNU/Linux, una vez configurado podemos acceder dsede otra maquían a su url de administración en https://<ip_address>:444

### Ejercicio 4.5. Probar las diferentes maneras de redirección HTTP.
¿Cuál es adecuada y cuál no lo es para hacer balanceo de carga global? ¿Por qué?

301, 302 etcétera


### Ejercicio 4.6. Buscar información sobre los bloques de IP para los distintos países o continentes.
Implementar en JavaScript o PHP la detección de la zona desde donde se conecta un usuario

Se puede implementar de varias maneras, lo mas optimo es usando un servicio de terceros, porque la base de datos GeoIP.dat suele agregar mucho peso a las paginas

### Ejercicio 4.7. Buscar información sobre métodos y herramientas para implementar GSLB.

Lo primero para eso deberiamos tener dos localizaciones en ubicaciones distintas, a poder ser continentes (no tiene sentido montar un GLSB en la misma ciudad)

Lo primero tenemos que crear una VPN para que ambos servidores se comuniquen de forma segura, así nos evitamos que nos puedan atacar via ssh

Luego configuramos lo tipico para que esté balanceado entre ambos, y que detected la localizacion del usuario para intentar servir contenido del mas cercano

