# Arch on VirtualBox
[Guía de la instalación](https://wiki.archlinux.org/title/installation_guide)

# 0 Recorda tratar

- **Conceptos:**

**EFI:** Fue desarollada por Intel y es una capa entre el hardware y el Sistema Operativo, se usa en los equipos más actuales, es similar a la UEFI pero sin las mejoras que presenta esta última.

**UEFI:** A diferencia de la BIOS la UEFI tiene mejoras (mayor tamaño de memoria y un rendimiento mas rápido) y se encarga de iniciar el istema operativo cuando un equipo se está encendiendo, además proporciona interfaz grafica mientras el S.O se inicia.

**BIOS:** Es un software de sistema  que se encarga de iniciar y controlar el hardaware del equipo cuando se enciende, la BIOS se almacena en la ROM y se carga en la RAM, este a la vez carga el sistema. Es un sistema antiguo aunque todavía se sigue utilizando en nuevos equipos aunque la gran mayoria usa la UEFI.

**GPT:** Es una tabla de particiones que se utiliza en equios con S.O modernos, se utiliza para dividir el disco duro en particiónes (Son secciónes independientes del disco que pueden usarse para almacenar datos).

**GUID:** Es un número de identificación único de 128 bits asignados a los objetos del Sistema Operativo (Discos duros, particiones de disco, controladores de dispositivos, aplicaciónes....) El GUID se genera utilizando un algoritmo que garantiza que cada numero generado es único en todo el mundo.

**MBR:** Es una zona del disco duro que almacena información importante sobre como se dividen las particiones de un disco duro, la MBR se encarga de cargar el sistema operativo en la RAM cuando se enciende el equipo y proporciona una serie de funciónes básicas par el sistema, como la configuración del reloj del sistema y el control de la entrada y salida de datos.

- Diferenciar claramente cando nos atopamos na ISO de instalación e na partición(s) instalada(s).



- Que é reflector?


## 1. Create and Configure a Virtual Machine
Antes de nada  tendremos que descargar la Iso de archlinux, para ello podemos acceder al siguiente [enlace](https://archlinux.org/download/)
### 1.1 Creation

### 1.2 Extra Configuration
### 1.3 Setting up SSH
### 1.4 Plugging in Arch ISO

## 2. Start the VM

## 3. Keyboard

## 4. Extra packages needed

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
