
# SWAP - Ejercicios Tema 7

### Ejercicio 7.1: ¿Qué tamaño de unidad de unidad RAID se obtendrá al configurar un RAID 0 a partir de dos discos de 100 GB y 100 GB?

200GB (raid0 no es redundante como tal, es simplemente sumar los discos)

### ¿Qué tamaño de unidad de unidad RAID se obtendrá al configurar un RAID 0 a partir de tres discos de 200 GB cada uno?

600GB (raid0 no es redundante como tal, es simplemente sumar los discos)

### Ejercicio 7.2: ¿Qué tamaño de unidad de unidad RAID se obtendrá al configurar un RAID 1 a partir de dos discos de 100 GB y 100 GB?

100 GB (es espejo)

### ¿Qué tamaño de unidad de unidad RAID se obtendrá al configurar un RAID 1 a partir de tres discos de 200 GB cada uno?
200GB (es espejo)

### Ejercicio 7.3: ¿Qué tamaño de unidad de unidad RAID se obtendrá al configurar un RAID 5 a partir de tres discos de 120 GB cada uno?
120GB

### Ejercicio 7.4: Buscar información sobre los sistemas de ficheros en red más utilizados en la actualidad y comparar sus
características. Hacer una lista de ventajas e inconvenientes de todos ellos, así como grandes sistemas en los que se utilicen.

A nivel domestico los sistemas de ficheros de red son SMB (microsoft), NFS (unix), AFP (apple), aunque apple ha empezado a utilizar por defecto SMB2 en OSX 10.9 y en linux tambien se recomienda SAMBA en lugar de NFS por su mejores características
SMB1 era propietario, NFS se ha quedado desfasado, ademas de ser lento, AFP no incorpora el sistema de cuotas de disco y las opciones de seguridad de SMB2, por lo que todo el mundo recomienda usar SMB2 ya que es un estandar abierto