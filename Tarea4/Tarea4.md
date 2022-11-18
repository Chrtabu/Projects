# Actividad 4, cuotas de disco

- [1. Definicion](#1-definicion)
- [2. Como saber si nuestro S.O tiene instalado los modulos kernel para el uso de las cuotas](#2-como-saber-si-nuestro-so-tiene-instalado-los-modulos-kernel-para-el-uso-de-las-cuotas)
  - [2.1 Explicación del comando `find`, y los flags:](#21-explicación-del-comando-find-y-los-flags)
  - [2.2 Como podemos utilizar el comando `find` para saber si nuestro SO tiene instalado los módulos de kernel que permiten el manejo de las cuotas?](#22-como-podemos-utilizar-el-comando-find-para-saber-si-nuestro-so-tiene-instalado-los-módulos-de-kernel-que-permiten-el-manejo-de-las-cuotas)
  - [2.3 Que paquete tendriamos que instalar si no tuviésemos esos módulos kernel instalados?](#23-que-paquete-tendriamos-que-instalar-si-no-tuviésemos-esos-módulos-kernel-instalados)
- [3. Donde activar las cuotas de un usuario y grupo](#3-donde-activar-las-cuotas-de-un-usuario-y-grupo)
  - [3.1 Haz los cambios pertinentes a los ficheros adecuados](#31-haz-los-cambios-pertinentes-a-los-ficheros-adecuados)
  - [3.2 que hay que hacer con el disco afectado? (si fuese necesario)](#32-que-hay-que-hacer-con-el-disco-afectado-si-fuese-necesario)
  - [3.3 Comproba que las opciones de disco son correctas](#33-comproba-que-las-opciones-de-disco-son-correctas)
- [4.Activación de las cuotas](#4activación-de-las-cuotas)
  - [4.1 Creación de ficheros necesarios](#41-creación-de-ficheros-necesarios)
  - [4.2 Verificación de la creación de los ficheros adecuados](#42-verificación-de-la-creación-de-los-ficheros-adecuados)
  - [4.3 Añadir los módulos de quota al kernel (si fuese necesario)](#43-añadir-los-módulos-de-quota-al-kernel-si-fuese-necesario)
  - [4.4 Activa el sistema de cuotas](#44-activa-el-sistema-de-cuotas)
- [5. Cuotas de usuario y de grupo](#5-cuotas-de-usuario-y-de-grupo)
- [6. Informes de cuotas](#6-informes-de-cuotas)
- [Información](#información)

## 1. Definicion
Las cuotas de disco son límites que son creados por el administrador de sistemaque limita el uso del sistema de archivos en los sistemas operativos. El paquete para manejar cuaotas es "quota quotatool"

## 2. Como saber si nuestro S.O tiene instalado los modulos kernel para el uso de las cuotas

### 2.1 Explicación del comando `find`, y los flags:
Es un comando que sirve para buscar archivos en el gestor de gestión de archivos a través de los parametros que le pongamos, por ejemplo, los siguientes

`-type`: Filtra por el tipo de archivo


`-name`: Filtra por el nombre

### 2.2 Como podemos utilizar el comando `find` para saber si nuestro SO tiene instalado los módulos de kernel que permiten el manejo de las cuotas?

Si queremos saber si nuestro equipo tiene instalado los modulos de kernel de cuotas usaremos el siguiente comando:

~~~
find /lib/modules/`uname -r` -type f -name '*quota_v*.ko*'
~~~

![Busqueda de los paquetes de quota](Imagenes/cap1.png)

### 2.3 Que paquete tendriamos que instalar si no tuviésemos esos módulos kernel instalados?

Tendríamos que user el siguiente comando:

~~~
sudo apt install quota
~~~

![Instalación de quota](Imagenes/cap2.png)

## 3. Donde activar las cuotas de un usuario y grupo

### 3.1 Haz los cambios pertinentes a los ficheros adecuados

Ahora nos dirijiremos a `/etc/fstab` y editaremos los datos de manera que quede como tenemos en la siguiente imagen:

** Nuestro UUID en esta maquina es 126970b1-346a-475a-af3e-d2cbbb27d3ee

~~~
sudo nano /etc/fstab
~~~
![Configuración de /fstab](Imagenes/cap3.png)


### 3.2 que hay que hacer con el disco afectado? (si fuese necesario)

Ahora tendremos que montarel sistema para aplicar los cambios, para ello usaremos el siguiente comando.

~~~
sudo mount -o remount /
~~~

![montaje del disco con la configuración de quotas](Imagenes/cap6.png)

### 3.3 Comproba que las opciones de disco son correctas

Para comprobar que los comandos anteriores han funcionado usaremos los siguientes comandos.

~~~
cat /proc/mounts | grep ' / '
~~~

![comprobacion de las opciones de disco](Imagenes/cap5.png)

## 4.Activación de las cuotas

### 4.1 Creación de ficheros necesarios

Ahora habilitaremos las cuotas, para ello usaremos los siguientes comandos:

~~~
quotacheck -cum /
quotacheck -cgm /
quotacheck -cugm /
~~~
![habilitación de cuotas](Imagenes/cap7.png)

### 4.2 Verificación de la creación de los ficheros adecuados
Ahora vamos a verificar que tengamos los ficheros creados, para ello haremos un `ls /`

![Verificación de la creacion](Imagenes/cap9.png)

### 4.3 Añadir los módulos de quota al kernel (si fuese necesario)
El comando es el siguiente.

~~~
sudo apt install linux-image-extra-virtual
~~~

![Añadimos los modulos kernel](Imagenes/cap8.png)

### 4.4 Activa el sistema de cuotas
Ahora vamos a activar las cuotas en root, para ello vamos usar los siguientes comandos:

~~~
sudo quotaon -v /
~~~

![activacion de las cuotas](Imagenes/cap10.png)

## 5. Cuotas de usuario y de grupo



## 6. Informes de cuotas



## Información
En este apartado voy a añadir las diferentes fuentes que he usado para realizar la tearea.

