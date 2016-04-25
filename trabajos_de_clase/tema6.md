
# SWAP - Ejercicios Tema 6

### Ejercicio 6.1: Aplicar con iptables una política de denegar todo el tráfico en una de las máquinas de prácticas.
Comprobar el funcionamiento.
Aplicar con iptables una política de permitir todo el tráfico en una de las máquinas de prácticas.
Comprobar el funcionamiento.

Bloquer todo:
```
iptable -F
iptables -P INPUT DROP
iptables -P OUTPUT DROP
iptables -P FORWARD DROP
```

Permitir todo:

```
iptables -F
iptables -I INPUT -j ACCEPT
``

### Ejercicio 6.2: Comprobar qué puertos tienen abiertos nuestras máquinas, su estado, y qué programa o demonio lo ocupa.

Las pruebas las hacemos con **nmap**

primero el servidor **home.ernesto.es** que solo tiene acceso ssh (y solo accesible mediante certificado)

```
[ernesto@ubuntu 19:26:30 ~]$ nmap home.ernesto.es -Pn

Starting Nmap 6.40 ( http://nmap.org ) at 2016-04-25 19:26 CEST
Nmap scan report for home.ernesto.es (85.62.20.254)
Host is up (0.013s latency).
Not shown: 999 filtered ports
PORT   STATE SERVICE
22/tcp open  ssh

Nmap done: 1 IP address (1 host up) scanned in 6.82 seconds
```

Tambinen probamos a acceder a un Time Capsule de apple solo accesible desde mi red interna

```
[ernesto@ubuntu 19:26:41 ~]$ nmap 192.168.0.2 -Pn

Starting Nmap 6.40 ( http://nmap.org ) at 2016-04-25 19:26 CEST
Nmap scan report for 192.168.0.2
Host is up (0.0019s latency).
Not shown: 995 closed ports
PORT      STATE SERVICE
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
548/tcp   open  afp
5009/tcp  open  airport-admin
10000/tcp open  snet-sensor-mgmt

Nmap done: 1 IP address (1 host up) scanned in 12.34 seconds
```


### Ejercicio 6.3: Buscar información acerca de los tipos de ataques más comunes en servidores web, en qué consisten, y cómo se pueden evitar.

SQL Injection: por entradas no "sanitizadas" de campos, para mas info ver la tira comica: https://xkcd.com/327/

DDoS: Ataque de denegacion de servicio distribudo

XSS: Cross Site Scripting, permitir parsear javascript cargado desde otro servidor, pudiendo embeber javascripts maliciosos para el usuario



