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

![Comprobación modulos Kernel](./ImagenesFinal/)

3. Qué paquete teriamos que instalar se non tivésemos eses módulos kernel instalados?

## 3 Onde debemos activar/declarar as cuotas de usuario e grupo

- Fai os cambios pertinentes ao(s) ficheiro(s) adecuado(s)
- Que hai que facer co disco afectado? (FAINO 😁)
- Comproba que as opcións de disco son correctas (**PISTA**: qué hai en `/proc/mounts`)?

## 4 Activando as cuotas (tanto de usuario coma de grupo)

- Creación de ficheiros necesarios
- **Recorda**: verifica que se crearon os ficheiros adecuados
- Engade os módulos de quota ao kernel (se fose necesario)
- Activa o sistema de cuotas

## 5 Cuotas de usuario e de grupo

**NOTA**: ⚠️☣️☢️ non usar `setquota` ☢️☣️⚠️

Cada vez que establezas unha cuota comproba cun comando que a estableciches correctamente.

- Creade as usuarias `veronica-lake`, `gene-tierney`, `ada-lovelace` e `hedy-lamarr`.
- Creade os grupos de usuarias `actresses` e `scientists`.
- Incluide a `veronica-lake`, `gene-tierney` e `hedy-lamarr` no grupo `actresses`
- Incluide a `ada-lovelace` e `hedy-lamarr` no grupo `scientists`.
- Establece as seguintes cuotas de usuario:
   - `veronica-lake` 100M soft e 150M hard.
   - `gene-tierney` 200M soft e 250M hard.
   - `ada-lovelace` 500M soft e 600M hard.
   - `hedy-lamarr` 800M soft e 1G hard.
- Establecede as seguintes cuotas de grupo:
   - `actresses` 400M soft e 450M hard
   - `scientist` 900M soft e 1G hard

Comprobade os efectos que ten o solapamento das cuotas entre grupos e usuarias e explicádeos:

1. Cómo funcionan as cuotas nun grupo?
2. Cómo afectan aos usuarios do grupo?
3. Posibilidades:
   - A cuota do grupo afecta aos membros do grupo (sumada)
   - A cuota do grupo afecta a cada membro do grupo (individualmente)

## 6 Informes de cuotas

Xera un informe global das cuotas creadas

## 7 Entrega

Cando remates, establece un `tag` chamado `v4` e con mensaxe `"Entrega actividade 4"` 👇

```sh
git tag -a v4 <derradeiro-hash-commit> -m "Entrega actividade 4"
git push origin v4
```