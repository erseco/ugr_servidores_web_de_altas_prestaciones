
# SWAP - Ejercicios Tema 5

###Ejercicio 5.1: Buscar información sobre cómo calcular el número de conexiones por segundo.

Podemos saber en un momento dado cuantas peticiones esta sirviendo apache ejecutando: ```apache2ctl status |grep request```


###Ejercicio 5.2: Instalar wireshark y observar cómo fluye el tráfico de red en uno de los servidores web mientras se le hacen peticiones HTTP.

Instalamos wireshark para Mac usando brew, recordar que hara falta tener instalado X11, tambien podemos descargar la versión para windows o instalarla en Debian/ubuntu mediante apt-get install wireshark

Si seleccionamos "capture" en el menú veremos como fluyen los datos en la ventana, nos rellenará un montón de datos del tipo:

```
dst port 80 or dst port 80 or dst port 1433  and tcp[tcpflags] & (tcp-syn) != 0 and tcp[tcpflags] & (tcp-ack) = 0 and src net 192.168.0.0/24

```


###Ejercicio 5.3: Buscar información sobre herramientas para monitorizar las prestaciones de un servidor.

Tenemos varias herramientas para monitorizar un servidor, como por ejemplo **pandora-fms**, o uno muy vistoso llamado **netdata** que podemos encontrar en https://github.com/firehol/netdata
