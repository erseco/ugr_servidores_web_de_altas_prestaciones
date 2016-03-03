#Practica 2: Clonar la información de un sitio web

##Pasos:
###1. Descargar Ubuntu 12.04.5 LTS (Precise pangolin) para 32 bits (i386)
```
wget http://cdimage.ubuntu.com/ubuntu-server/precise/daily/current/precise-server-i386.iso
```

###2. Configurar dos maquinas virtuales con VMWare Fusion, a la primera la llamaremos swap1 y a la segunda swap2

###3. Instalar las utilidades para máquinas virtuales
```
sudo apt-get install open-vm-tools
```

###4. Definir password root
```
sudo passwd root
```

###5. Hemos configurado el archivo hosts de nuestra máquina para que resuelva swap1 y swap2 sin tener que recordar la ip

###6. Hemos creado el archivo "hola.html" en /var/www/hola.html
```
sudo touch /var/www/hola.html
sudo vim /var/www/hola.html
```

##Resultados:
###1. Obtener el numero de versión del apache instalado:

![Version apache](img/01.png)

###2. Consultar si hay algun proceso en el sistema con nombre apache:

![psaux apache](img/02.png)

###3. Consultamos la web desde el navegador

![captura chrome](img/03.png)

###4. Obtenemos la web mediante curl

![obtener con curl](img/04.png)
