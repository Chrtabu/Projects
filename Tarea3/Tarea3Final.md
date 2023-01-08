# Arch on VirtualBox
[Guía de la instalación](https://wiki.archlinux.org/title/installation_guide)

# Definiciones

- **Conceptos:**

**EFI:** Fue desarollada por Intel y es una capa entre el hardware y el Sistema Operativo, se usa en los equipos más actuales, es similar a la UEFI pero sin las mejoras que presenta esta última.

**UEFI:** A diferencia de la BIOS la UEFI tiene mejoras (mayor tamaño de memoria y un rendimiento mas rápido) y se encarga de iniciar el istema operativo cuando un equipo se está encendiendo, además proporciona interfaz grafica mientras el S.O se inicia.

**BIOS:** Es un software de sistema  que se encarga de iniciar y controlar el hardaware del equipo cuando se enciende, la BIOS se almacena en la ROM y se carga en la RAM, este a la vez carga el sistema. Es un sistema antiguo aunque todavía se sigue utilizando en nuevos equipos aunque la gran mayoria usa la UEFI.

**GPT:** Es una tabla de particiones que se utiliza en equios con S.O modernos, se utiliza para dividir el disco duro en particiónes (Son secciónes independientes del disco que pueden usarse para almacenar datos).

**GUID:** Es un número de identificación único de 128 bits asignados a los objetos del Sistema Operativo (Discos duros, particiones de disco, controladores de dispositivos, aplicaciónes....) El GUID se genera utilizando un algoritmo que garantiza que cada numero generado es único en todo el mundo.

**MBR:** Es una zona del disco duro que almacena información importante sobre como se dividen las particiones de un disco duro, la MBR se encarga de cargar el sistema operativo en la RAM cuando se enciende el equipo y proporciona una serie de funciónes básicas par el sistema, como la configuración del reloj del sistema y el control de la entrada y salida de datos.

- Diferenciar claramente cando nos atopamos na ISO de instalación e na partición(s) instalada(s).

Cuando nos encontramos en la ISO de instalación estamos trabajando directamente sobre el sistema de instalación, es decir, aun estamos configurando el sistema que **aun vamos a instalar**. En cambio cuando nos encontramos en una particion significa que el sistema ya se ha instalado y estamos configurando el sistema en un sistema operativo **ya instalado**

- Que é reflector?
Un reflector es un software (o dispositivo) que redirige paquetes de datos de una red a otra, se usan normalmente para ampliar la cobertura de una red inalámbrica o para crear una conexión segura a través de una VPN (Red Privada Virtual).

## 1. Create and Configure a Virtual Machine
Antes de nada  tendremos que descargar la Iso de archlinux, para ello podemos acceder al siguiente [enlace](https://archlinux.org/download/)
### 1.1 Creation
El primer paso que tendremos que hacer será crear la máquina virtual desde VirtualBox, a continuación mostraré paso a paso como crear la máquina de ArchLinux.

-Paso 1: En VirtualBox clikaremos en "Nuevo"y nos aparecerá la siguiente pestaña, el la cual tendremos que añadir un nombre a la máquina y añadiremos la ISO del sistema que querramos instalar, en este caso será la de un archlinux.

![Instalación paso 1](./ImagenesFinal/Paso1Instalacion.png)

-Paso 2: El siguiente paso será poner cuanta RAM  queremos usar para nuestra máquina, en mi caso pondre 2 GB de Ram.

* **Nota**: En la parte de nucleos del procesador le he puesto 2 nucleos, ya que si se le deja en default coge 1 y no deja iniciar las máquinas.

![Instalación paso 2](./ImagenesFinal/Paso2Instalacion.png)

-Paso 3: Una vez indicada la RAM tendremos que configurar el espacio de disco que queremos utilizar para la máquina Virtual, en mi caso le he puesto 20GB.

![Instalación paso 3](./ImagenesFinal/Paso3Instalacion.png)

-Paso 4: Ahora nos aparecerá una pestaña donde nos resumira las configuraciónes que hemos hecho a la máquina, le daremos a terminar ya que un tenemos que configurar un par de opciones mas.

![Instalación paso 4](./ImagenesFinal/Paso4Instalacion.png)

-Paso 5: Ahora nos dirigiremos a la configuración de la máquina (Clik derecho en la maquina y le daremos a "Configuraciones") en el partado de "Sistema" habilitamos la opción "Habilitar EFI" 

![Instalación paso 5](./ImagenesFinal/Paso5Instalacion.png)

### 1.3 Plugging in Arch ISO

***Nota :** En la versión más reciente de VirtualBox ya nos obliga a añadir al crear una máquina la Iso que queremos utilizar, aun  que hay versiones mas antiguas que la ISO se añade posteriormente, luego de la creación, en este apartado explicaré como añadir la ISO, en caso de que tengamos una version de VirtualBox anterior.

**-Paso 1:** Tendremos que dirigirnos a la configuración de la máquina, para ello tendremos que darle clik derecho a la máquina e ir a "configuración", una vez ahí buscaremos el apartado de "Almacenamiento", nos debreia aparecer esta pestaña.

![Nos dirijimos a configuracionde almacenamiento de la máquina](./ImagenesFinal/a%C3%B1adir%20iso%201.png)

**-Paso 2:** 
Una vez estemos en la confihuración, nos ririgiremos al apartado que tiene una imagen de un Cd, clikamos y añadimos la ISO de la siguiente manera:

![Añadimos la ISO a la máquina que hemos creado](./ImagenesFinal/Inicio%20Iso%202.png)

Una vez hecho esto aplicaremos los cambios y saldremos.

## 2. Start the VM
Ahora clikaremos dos veces en la máquina virtual que hemos creado y nos iniciará la máquina, cuando haya arrancado nos aparecerá lo siguiente:

![Inicio de la máquina Virtual](./ImagenesFinal/Iniciomaquina.png)

## 3. Keyboard 
 En este apartado cargaremos el idioma del teclado ya que la distribucion por defecto es el inglés, para ello usaremos el siguente comando.

 ~~~
 loadkeys es
 ~~~

![Cambio de distribución de teclado](./ImagenesFinal/Imagen1loadkeys.png)

## 4. Configuración del reloj

En este paso vamos a sincronizar la hora del reloj de nuestro equipo con el servidor de sistema de reloj, para ello usaremos los siguientes comandos:

~~~
timedatectl set-ntp true
timedatectl status
~~~

![Sincronización con el servidor del reloj](./imagenesfinal/configuracion%20reloj.png)

## 5. Configuracion de `ssh` y `passwd de root`
Para poder hacer una instalacion a través de otro equipo deberemos tener el `ssh` configurado, para ello usaremos el siguiente comando:

~~~
systemctl start sshd
~~~

![Configuración del ssh](./imagenesfinal/ssh1.png)

Ahora configuraremos la contraseña de `root`, para ello usaremos el siguiente comando:

~~~
passwd root
~~~

y nos dirijiremos al terminal de nuestra máquina real (en nuestro caso) y comprobaremos que se conecta por ssh

![Configuracion de la contraseña de root](.imagenesfinal/../ImagenesFinal/passwd.png)

## 6. Instalación de `reflector`
-`Reflector:` Reflector es un script que puede recuperar la última lista de servidores de réplicas desde la página MirrorStatus, filtrar la mayoría de los servidores de réplicas actualizados, ordénarlos por velocidad y sobrescribir el archivo.

-`Syy:` El flag `-S` indica que queremos sincronizar paquetes e instalarlos; el flag `-yy` obliga a descargar paquetes actualizados aunque ya existan.

![Instalación de reflector con pacman -Syy](./ImagenesFinal/reflector.png)

## 7. Particionado de los discos
**-Paso 1**: Comprobaremos las particiones de nuestro disco usando el siguiente comando:

~~~
gdisk /dev/sda
~~~

Y crearemos las particiones de la siguiente manera:

![Configuración de las particiones](./imagenesfinal/particiones1.png)

Lo siguinete que tendremos que hacer será dar formato a las particiones de la siguiente manra:

![Formato de las particiones](ImagenesFinal/formato%20particiones.png)

Y ahora creareos y montaremos los sistemas de ficheros con los siguientes comandos:

~~~
mkdir -p /mnt/boot
mkdir -p /mnt/etc
mount /dev/sda2 /mnt
mount /dev/sda1 /mnt/boot
~~~

![Creacion y montaje](imagenesfinal/creacion%20y%20montaje.png)

## 5. Extra packages needed

Ahora vamos a instalar los paquetes que vamos a necesitar, en este caso serán: Base, Kernel y firmware, para ello tendremos que configurar lo instalaremos con el siguiente script:

~~~
pacstrap -K /mnt base linux linux-firmware
~~~



## 5. Which is my IP?



### 5.1 Start ssh daemon
### 5.2 Password for the ISO's root user
### 5.3 The IP

## 6. `ssh` from terminal

## 7. sync Network Time Protocol

## 8. `reflector`, mirror list, fastest server available AKA _Refresh the servers with `pacman -Syy`_

### 8.1 Get the _best_ servers (_reflector_)

Explicación Flags:

- `-c`
- `-a`
- `--sort rate`
- `--save <mirror-list-directory>`

### 8.2 Refresh servers

Explicación Flags:
- `-S` or `--sync`
- `-y` or `--refresh`

## 9 Disks and partitions

### 9.1 Check status
### 9.2 Partitions for a EFI system
### 9.3 `gdisk`, utility to create GPT Tables

## 10 Formating partitions

## 11 Mounting partitions

### 11.1 `sda1`
### 11.2 `sda2`

## 12 Installation of the base packages to `/mnt` with `pacstrap`

## 13 Generating the FileSystem Table (`fstab`)

Recorda explicar o flag:

- `-U`:

## 14 Enter the installation AKA _Chroot in with arch-chroot `/mnt`_

## 15 Create a 2GB swap file

### 15.1 A 2GB swap file
### 15.2 Permissions
### 15.3 Formatting as swap
### 15.4 Activating the `/swapfile`
### 15.5 Generating its FileSystem Table Entry (`fstab`)

## 16 Timezone

### 16.1 What's my timezone (GOTCHA)
### 16.2 Setting the timezone

Recorda explicar os flags:

- `-s` or `--symbolic`
- `-f`or `--force`

### 16.3 Syncing the HW Clock & the System Clock
### 16.4 Setting which locales to be generated

Recorda explicar:

- Qué é un _locale_.?

### 16.5 Generating the locales
### 16.6 `/etc/locale.conf`
### 16.7 `/etc/vconsole.conf`

## 17 The `/etc/hostname` file

## 18 The `/etc/hosts` file

```sh
127.0.0.1   localhost
::1         localhost
127.0.1.1   <hostame>.localdomain    <hostname>
```

## 19 A password for the `root` user

## 20 Bootloader & some moar packages

Explicaciónes:

- grub
- efibootmgr
- networkmanager
- network-manager-applet
- dialog
- os-prober
- mtools
- dosfstools
- base-devel
- linux-headers
- cups
- reflector
- openssh
- git
- xdg-utils
- xdg-user-dirs
- virtualbox-guest-utils

## 21 Installing and setting up `grub`

### 21.1 Installing grub
### 21.2 Configuring grub

## 22 Enabling some services

### 22.1 `NetworkManager`
### 22.2 `sshd`
### 22.3 `cupsd` (GOTCHA)

## 23 Create a new user

### 23.1 Creation

Explicación:

- O grupo `wheel`.
- O flag `-m`.
- O flag `-G`.

### 23.2 Password
### 23.3 `sudo` privileges

`visudo`:

## 24 EXIT the installation!!!!

## 25 Unmounting and Rebooting

### 25.1 `umount` all the partions
### 25.2 Reboot

## 26 Log into Arch ...and check if we have an IP

## 27 `ssh` into the VM ...again

## 28 Desktop environment

### 28.1 Installation of xfce4

Instala e explica brevemente que fan os seguintes paquetes:

- `xf86-video-vmware`
- `xorg`
- `lightdm` and `lightdm-gtk-greeter`
- `xfce4` and `xfce4-goodies`
- `materia-gtk-theme` and `papirus-icon-theme`


### 28.2 Enable `lightdm` display manager

## 29 Exit ssh and reboot

## 30 Moar

### 30.1 Install `nano`

```sh
$ pacman -S nano
```

### 30.2 Install some other desktop environment

- [Suxerencia paquetes gnome](https://gitlab.com/eflinux/arch-basic/-/blob/master/gnome.sh)
