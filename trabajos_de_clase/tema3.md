---
title: SWAP Ejercicios Tema 3
layout: post
author: erseco
source-id: 1iDwACopRlMg3bRqWsKcgU5Px9qoQ7g3rvkcOD3GG8JE
published: true
---
# SWAP - Ejercicios Tema 3

### Ejercicio 3.1. Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el enrutamiento del tráfico de un servidor para pasar el tráfico desde una subred a otra.

* En windows podemos hacerlo con el comando "route"

* En linux podemos hacerlo tanto con el comando route como definiendo reglas en iptables (hay que recordar que activar el enrutamiento con**  ****sudo echo "1" > /proc/sys/net/ipv4/ip_forward**

### Ejercicio 3.2. Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el filtrado y bloqueo de paquetes.

* En windows podemos filtrar con el firewall de windows (a partir de windows xp sp1)

* En linux podemos hacerlo definiendo reglas en iptables

