# Actividade 4: cuotas de disco

## 1 Cal é o páquete que permite manexar cuotas
El paquete que nos permite establecer y controlar las cuotas del disco de llama "quota".

## 2 Cómo saber se o noso sistema ten instalados os módulos do kernel que permiten o manexo de cuotas

Axuda:

1. Explica o comando `find`, e os flags:
   - `find`: Sirve parq buscar archivos y directorios por nombre, tamaño, tipo, propietario, fecha... 
   - `-type`: Se usa para buscar archivos   y directorios que coinciden con un criterio determinado.
   - `-name`: Sirve para buscar un archivo o un directorio que coinciden con un nombre determinando. 
2. Cómo podemos utilizar o comando `find` para saber se o noso sistema ten instalados os módulos do kernel que permiten o manexo de cuotas?

Podriamos saberlo usando el anterior comando de la siguiente manera:

~~~
find /lib/modules/$(uname -r) -name "*quota*.ko
~~~

![Comprobación modulos Kernel](./ImagenesFinal/comprobacion%20cuotas.png)

3. Qué paquete teriamos que instalar se non tivésemos eses módulos kernel instalados?

En caso de que no tengamos instalado el módulo kernel tendremos que instalarlo con el siguiente comando:

~~~
sudo apt-get install quota
~~~

![Instalación del "quota"](./ImagenesFinal/Instalacion%20de%20modulo%20kernenl.png)

Si queremos comprobar la versión del paquete `quota` usaremos el siguiente comando:

~~~
quota --version
~~~

![Comprobación de la versión de quota](./ImagenesFinal/version%20del%20paquete%20quota.png)

## 3 Onde debemos activar/declarar as cuotas de usuario e grupo

El primer paso para la activación de la cuotas será diirijirnos a `/etc/fstab` y editaremos el fichero con mucho cuidado ya que en caso de que eliminemos algo podemos eliminar el sistema **(como recomendación: si es la primera vez que se dita esto crear una instantánea de la máquina para evitar perder todo el sistema)** , para ello usaremos el siguiente comando:

~~~
nano /etc/fstab
~~~

![Configuración del archivo en /etc/fstab](./ImagenesFinal/%C3%A7configuracion%20fstab.png)

Ahora montaremos el disco

~~~
sudo mount -o remount /
~~~

![Remount](./ImagenesFinal/Paso%20remount.png)

Para comprobar que lo hemos hecho bien usaremos el siguiente comando

~~~
cat /proc/mounts | grep /dev/sda
~~~

![Comprobación con el error](./ImagenesFinal/Error%20que%20sale%20en%20la%20comprobaci%C3%B3n.png)

## 4 Activado as cuotas (tanto de usuario coma de grupo)

**Explicaciónes:**

`-u:` Indica que se deben mostrar los límites de cuota del usuario.

`-g:` indica que se deben mostrar los límites de cuota para el/los grupo
(s) afectados. 

`-m:` Sirve para alertar de que un usuario o grupo se esta acercando al límite de la cuota y se le notificará por correo electrónico.

`-c:` Indica los cambios que se han realizado a los límites de cuota de disco; sirve para apreciar todos los cambios hacia usuarios y grupos.

Crearemos los ficheros que necesitamos para usar `quota`, para ello usaremos el siguiente comando:

~~~
sudo quotacheck -cugm /
~~~

![Paso del comando quotacheck](./ImagenesFinal/Paso%20quotachek.png)

Verificaremos los ficheros, para ello lanzaremos el comando siguiente:

~~~
ls /
~~~

![Verificación de ficheros necesarios de quota](./ImagenesFinal/verificacion%20de%20ficheros.png)

Ahora añadiremos los módulos kernel, para ello usaremos el siguiente comando:

~~~
sudo apt install linux-image-extra-virtual
~~~

![Instalación del módulo kernel](./ImagenesFinal/intalacion%20modulos%20kernel.png)

El siguiente paso será activar las cuotas, para ello pondremos este comando:

~~~
sudo quotaon -v /
~~~

`-v`: Define mas información

![Activación de las cuotas](./ImagenesFinal/activacion%20de%20cuotas.png)

## 5 Cuotas de usuario e de grupo

**NOTA**: ⚠️☣️☢️ non usar `setquota` ☢️☣️⚠️

Cada vez que establezas unha cuota comproba cun comando que a estableciches correctamente.

- Creade as usuarias `veronica-lake`, `gene-tierney`, `ada-lovelace` e `hedy-lamarr`.

~~~
sudo useradd <nombre del usuario>
~~~

![Verificación de la creación de los usuarios](./ImagenesFinal/verificacion%20de%20usuarios.png)

- Creade os grupos de usuarias `actresses` e `scientists`.

~~~
sudo addgroup <nombre del grupo>
~~~

![Creacion de los grupos](./ImagenesFinal/verificacion%20de%20creacion%20de%20los%20grupos.png)

- Incluide a `veronica-lake`, `gene-tierney` e `hedy-lamarr` no grupo `actresses`

~~~
sudo usermod -a -G <grupos> <usuario>
~~~

![verificacion añadir usuarios al grupo](./ImagenesFinal/actresses.png)

- Incluide a `ada-lovelace` e `hedy-lamarr` no grupo `scientists`.

***Nota**: El comando es igual que para añadir usuarios colo que cambiando el grupo.

Confirmaremos que lo hayamos hecho bien con el siguiente comando:

~~~
cat /etc/group | grep scientists
~~~

![verificación de añadir usuarios al grupo](./ImagenesFinal/scientists.png)

- Establece as seguintes cuotas de usuario:

Para añadir las cuotas a los usuarios o grupos usaremos el siguiente comando:

~~~
edquota -u (y el nombre de usuario)
~~~

`u`: 

   - `veronica-lake` 100M soft e 150M hard.
   - `gene-tierney` 200M soft e 250M hard.
   - `ada-lovelace` 500M soft e 600M hard.
   - `hedy-lamarr` 800M soft e 1G hard.

![Creacion de las cuotas para los usuarios](./ImagenesFinal/cuotas%20creadas%201.png)

- Establecede as seguintes cuotas de grupo:
   - `actresses` 400M soft e 450M hard
   - `scientist` 900M soft e 1G hard



Comprobade os efectos que ten o solapamento das cuotas entre grupos e usuarias e explicádeos:

1. Cómo funcionan as cuotas nun grupo?
- Se limita el uso del disco al espacio maximo en el que estea configurado para un grupo en específico.

2. Cómo afectan aos usuarios do grupo?
-Todos los usuarios que estean dentro de un grupo tendrán el límite de la cuota del grupo.

3. Posibilidades:
   - A cuota do grupo afecta aos membros do grupo (sumada)
   Una cuota sumada es la cantidad total de cuotas que se han establecido para un período de tiempo determinado, se usa para regular el espacio u otros servicios.

   - A cuota do grupo afecta a cada membro do grupo (individualmente)
   Los usuarios que pertenezcan a un grupo tendrán que cumplir una cuota individual de cada usuario, y este debe estar dentro de la cuota del grupo al que pertenece.

## 6 Informes de cuotas

Xera un informe global das cuotas creadas

## 7 Entrega

Cando remates, establece un `tag` chamado `v4` e con mensaxe `"Entrega actividade 4"` 👇

```sh
git tag -a v4 <derradeiro-hash-commit> -m "Entrega actividade 4"
git push origin v4
```