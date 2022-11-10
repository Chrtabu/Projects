## 1. Definicion de conceptos
### ¿Que es la EFI,UEFI,BIOS,GPT,GUID Y MBR?
### Diferenciación entre la Iso y la partición
### ¿Que es un reflector?
### 

## 2. Configuración de la maquina virtual
### 2.1 Configuración de la RAM
Lo primero será configurar la máquina virtual, lo primero sera indicar cuanta memoria RAM vamos a utilizar, en mi caso serán 4096 MB

![Configuracion del uso de la RAM](./imagenes/ram.png)

### 2.2 Configuración del disco virtual 
Ahora configuraremos cuanto almacenamiento queremos añadir para la máquina virtual, en mi caso serán 30 GB.

![COnfiguración del disco virtual](./imagenes/disco.png)

### 2.3 Otras configuraciónes de la máquina
Ahora realizaremos otras configuraciones de la máquina, para ello no dirigiremos a la configuración de la máquina y haremos lo siguiente:

- En el apartado de sistema habilitaremos lel apartado "Habilitar EFI"

![Configuración EFI](./imagenes/efi.png)

- Ahora configuraremos la pantalla, para ello nos dirigiremos a pantalla y pondremos la memoria de video al máximo y en el controlador grafico usaremos VBoxSVGS.

![Configuración de la pantalla](./imagenes/pantalla.png)

- Lo siguiente será añadir la iso a la máquina, para ello nos dirigiremos a Almacenamiento y añadiremos la ISO.

![Añadimos la ISO a la máquina](./imagenes/iso.png)

## 3. Instalación de la máquina virtual
Lo primero será cammbiar la distribución de teclado para el español, para ello usaremos el siguiente comando.

~~~
loadkeys es
~~~

![Cambio de distribucio de teclado](./imagenes/loadkeys.png)

Ahora comprobaremos si tenemos conexión a Internet, para ello haremos un ping a google y comprobaremos si hay conexión

~~~
ping google.com
~~~

![Ping a google](./imagenes/ping.png)

## 4. Configuración de los discos

Lo siguiente que tendremos que hacer será configurar el disco, para ello usaremos gdisk, con este comando podremos particionar el disco de la siguiente manera

~~~
gdisk /dev/sda
~~~

![configuración del disco](./imagenes/conf_disco.png)

Una vez particionado el disco ahora le daremos formato, para ello usaremos los siguientes comandos:

~~~
mkfs.ext4 /dev/sda2
~~~

![Formato ext4](./imagenes/mkfs1.png)

~~~
mkfs.fat -F 32 /dev/sda1
~~~

![Formato fat32](./imagenes/mkfs2.png)

El siguiente paso será montar los discos, para ello usaremos los siguientes comandos

~~~
mount /dev/sda1 /mnt
~~~

![Mount sda1](./imagenes/mount1.png)

~~~
mount --mkdir /dev/efi_system_partition /mnt/boot
~~~

Y comprobaremos que estea correctamente con el comando:

~~~
lsblk
~~~

![lsblk](./imagenes/lsblk.png)

## 5. Instalación del SO
Una vez hayamos montado y particionado los discos empezaremos con la instalación, para ello usaremos el siguiente comando.

~~~
pacstrap -K /mnt base linux linux-firmware
~~~

![packstrap](./imagenes/pacstrap.png)

Ahora configura## Instalación de paquetes KDE
Ahora vamos a instalar por paquetes kde, para ello usaremos los siguientes comandos.

~~~
pacman -S kf5 kf5-aids
~~~
![Instalacion kde 1](./imagenes/kda1.png)

~~~
pacman -S ttf-freefont
~~~

![instalacion kde 2](./imagenes/kde2.png)

~~~
pacman -S sddm sddm-kcm
~~~

![Instalacion kde 3](./imagenes/kde3.png)

~~~
genfstab -U /mnt >> /mnt/etc/fstab
arch-chroot /mnt
~~~

![Comfiguración del sistema](./imagenes/genfstab.png)

Lo siguiente será configurarv la hora local con el siguiente comando

~~~
ln -sf /usr/share/zoneinfo/Spain /etc/localtime
hwclock --systohc
locale-gen
~~~

![locale-gen](./imagenes/localegen.png)

Ahora nos dirigiremos a /etc/locale.gen y decomentaremos el idioma que querramos usar, para el Español será el siguiente:

~~~
vim /etc/locale.gem
~~~

![elecion de español](./imagenes/es_es.png)

luego lo escribiremos en /etc/locale.conf y añadiremos lo siguiente:

~~~
vim /etc/locale.conf
~~~

![lang=es](./imagenes/lang.png)

Luego iremos a /etc/vconsole.conf y añadiremos lo siguiente:

![kaymap](./imagenes/keymap.png)

Ahora vamos a hacer la instalación de paquetes, para ello usaremos el siguiente comando

~~~
pacman -S grub efibootmgr network-manager network-manager-applet dialog os-probe mtools dosfstools base-devel linux-headers cups reflector openssh xdg-utils xdg-user-dirs virturalbox-guest-utils
~~~

![Instalacion de paquetes](./imagenes/instalacion%20de%20paquetes.png)

~~~
grub-install
grub-mkconfig -o /boot/grub/grub.cfg
~~~

![Grub](./imagenes/grub.png)

~~~
systemctl enable NetworkManager
systemctl enable ssh
~~~

![enable services](./imagenes/enable.png)

6. Creación de los usuarios
En este punto tendremos que crear un usuario y ponerle una contraseña, lo cual tenemos la explicación en la tarea 2 en la cuál nos dedicamos íntegramente a la creación y modificación de los usuarios en un sistema. Igualmente voy poner los comandos a continuación.

~~~
adduser alumno
passwd alumno
~~~

## 7. Instalación del entorno gráfico
Una vez hayamos reado el usuario que tenemos anteriormente, tendremos que instalar el entorno gráfico, para ello usaremos los siguientes comandos.

~~~
sudo pacman -S xf86-video-vmware xorg lightdm lightdm-gtk-greeter xfce4 xfce4-goodies firefox materia-gtk-theme papirus-icon-theme
~~~

![Entorno grafico 1](./imagenes/grafico1.png)

~~~
sudo systemctl enable lightdm
~~~

![Entorno grafico 2](./imagenes/grafico2.png)

Una vez hayamos hecho eso reiniciarenos el sistema y veremos que nos aparecerá el usuario que hemos creado y nos pedirá la contraseña, solo tendremos que introducirla y ya nos iniciara sesion.

![inicio de sesion](./imagenes/user1.png)


## 8. Instalacion nano
Lo primero que tendremos que hacer será conectarnos por SH, para ello usaremos el siguiente comando

~~~
ssh [usuario]@[direccion ip de la maquina]
~~~
![Conexion ssh](./imagenes/ssh2.png)


Luego ejecutaremos el siguiente comando:
~~~
 sudo pacman -Syy
~~~

![Obtencion del paquete](./imagenes/nano1.png)

Lo siguiente sera ejecutar el siguiente comando

~~~
 sudo pacman -S nano
~~~
 ![Instalacion de nano](./imagenes/nano3.png)



