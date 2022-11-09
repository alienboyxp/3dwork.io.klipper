# Instalación

## Que necesitamos?

* Raspberry Pi
* SD, aconsejable que sea rápida y con espacio suficiente para almacenar el sistema y archivos gcode
* Cable conexión entre nuestra Pi y nuestra impresora

## **Antes de comenzar!!!**

![](<.gitbook/assets/image (3).png>)

Por favor entiende que instalar Klipper en tu impresora require de cierta experiencia con impresoras 3d, hardware y software. Puede no ser una tarea trivial para gente que se acaba de iniciar en el mundo 3D o que no dispone de unos minimos conocimientos ya que puedes romper tu impresora o pi durante el proceso

Lee antes la guía completa y entiende todos los pasos que explicamos. Si tienes cualquier duda del proceso por favor te aconsejamos unirte al grupo de Telegram [https://t.me/Klipper\_Firmware\_ES](https://t.me/Klipper\_Firmware\_ES) donde seguro te echaran una mano.

{% hint style="danger" %}
**No nos hacemos  cargo de cualquir daño, problema o fallo que se pueda ocasionar siguiendo estas guías, todos los pasos han sido probados o son las instrucciones de los propios fabricantes/desarrolladores y no deberían de ocasionar fallos.**

**Se intentan mantener al día pero puede darse el caso que, por actualizaciones, estos pasos puedan variar sin previo aviso.**

**Estás haciendo estos cambio bajo tu propia responsabilidad!!!**
{% endhint %}

## Preparación de nuestra pi

Para poder instalar Klipper debemos preparar nuestra Pi. Esta guía no va a entrar en detalle este paso tan solo haremos un listado rápido de los pasos a seguir:

1. Descargaremos una imagen de [Raspberry Pi OS Lite](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) y la "quemaremos2 en nuestra SD usando balenaEtcher o similar. Tienes información detallada de los pasos a seguir [aqui](https://3dwork.qitec.net/octoprint/instalacion/instalando-octoprint).
2. Verificaremos que nuestra pi arranca y podemos conectarnos por red wifi o cable
3. Habilitaremos SSH y verificaremos que podemos conectar por SSH
4. Ejecutaremos `sudo raspi-config` :
   1. Haremos un reset del password por defecto
   2. configuraremos el hostname si queremos
5. Ejecutaremos `sudo apt-get update` y `sudo apt-get upgrade` para actualizar nuestra pi

## Instalando Klipper usando Kiauh

Kiauh es un grandisimo avance para Klipper. Kiauh permite mediante unos sencillos menus instalar Klipper y sus principales componentes de una forma sencilla:

* Instalación de Klipper
* Instalar Moonraker (API que permite interactuar con Klipper por terceros como Mailsail, Fluidd o KlipperScreen)
* Instalación de diferentes interfaces web como Mailsail, Fluidd, Duet Web Control o Octoprint
* Instalar KlipperScreen (un fork de OctoScreen para Klipper)
* Actualizar todos los componentes (Octoprint de ser instalado se gestionará directamente desde el mismo)
* Eliminar cualquier componente
* Hacer un backup del sistema
* Preparar el firmware Klipper para nuestra MCU (placa de la impresora)
* Detectar el serial donde comunicar con nuestras MCU

Puedes encontrar un listado completo de las características [aquí](https://github.com/th33xitus/kiauh/blob/master/docs/features.md).

### Instalando Kiauh

Ahora que ya tenemos el sistema base en nuestra PI, esta actualizado y podemos conectarnos por SSH a ella comenzaremos a instalar Kiauh

```
sudo apt-get install git -y
cd ~
git clone https://github.com/th33xitus/kiauh.git
cd kiauh
chmod +x kiauh.sh scripts/*
./kiauh.sh
```

{% hint style="info" %}
Con estos comandos hacemos...

* Instalamos git para la gestión de repositorios
* Clonamos el repositorio de Kiauh
* Permitimos que los scripts descargados puedan ser ejecutados
* Ejecutamos Kiauh

Si necesitamos volver a lanzar Kiauh en el futuro podemos ir a `home/pi/kiauh y ejecutar ./kiauh.sh`
{% endhint %}

Una vez hemos realizado el proceso completo y lanzamos Kiauh deveriamos ver un menú como este:

![](<.gitbook/assets/image (14).png>)

### Instalando Klipper y Moonraker

Para nuestra guía vamos a usar Klipper que es el core del sistema y Moonraker que va a crear una API para poder gestionar la comunicación entre Klipper.

De las opciones del menú elegiremos la opción 1 para acceder al menú de instalación

![](<.gitbook/assets/image (19).png>)

Volveremos a elegir la opción 1 y comenzaremos el proceso de instalación:

* Eligiremos compilar nuestro firmware
* Por ahora no elegiremos actualizar nuestra MCU

![](<.gitbook/assets/image (8).png>)

### Instalando un interfaz para acceder a Klipper

Existen diferentes formas de gestionar Klipper, recomendamos el uso de Mainsail o Fluidd, es posible usar Octoprint también pero creemos que no es la mejor opción salvo casos puntuales ya que es más de uso general y Mainsail/Klipper son desarrollos específicos para Klipper.

![](<.gitbook/assets/image (10).png>)

La instalación es bastante sencilla y similar a la que realizamos en el punto anterior tan solo seleccionando el interfaz que más nos guste y seguir el asistente/indicaciones.

Es importante comentar que podemos instalar diferentes interfaces siempre y cuando usemos un puerto diferente para cada uno, aquí Kiauh también nos ayuda.

Otra función muy interesante, en este caso de Mainsail, es que podemos usar el interfaz online y dar de alta nuestra impresora sin necesitar nada instalado aunque en ocasiones podemos perder alguna funcionalidad.

{% embed url="http://my.mainsail.xyz" %}

{% hint style="info" %}
Para permitir que [my.mainsail.xyz](http://my.mainsail.xyz/) acceda a nuestra instalación local tenemos que permitir en nuestro moonraker.conf añadiendo o revisando que tengamos el siguiente codigo:

```
[authorization]
cors_domains:
    https://my.mainsail.xyz
    http://my.mainsail.xyz
    http://*.local
trusted_clients:
 10.0.0.0/8
 127.0.0.0/8
 169.254.0.0/16
 172.16.0.0/12
 192.168.0.0/16
 FE80::/10
 ::1/128
```
{% endhint %}

## Instalando Klipper usando imágenes preconfiguradas

Aunque os hemos enseñado como instalar el sistema usando un sistema base de Raspberry también disponemos de distribucciones de Klipper con todo preinstalado.

### MainsailOS

Una de las opciones es usar la distribución de Mainsail llamada MainsailOS:

1. Descargaremos la última versión de MainsailOS desde [**aquí**](instalacion.md#que-necesitamos).
2. Descomprimiremos el zip donde obtendremos un .img
3. Utilizando [**BalenaEtcher**](https://www.balena.io/etcher/) escribiremos .img a nuestra SD (8GB o mayor además de idealmente que sea una SD de alta velocidad)

{% hint style="danger" %}
**ESTE PROCESO BORRARÁ TODO EL CONTENIDO DE NUESTRA SD.**
{% endhint %}

i usamos wifi, editaremos el fichero _mainsailos-wpa-supplicant.txt_ donde añadiremos la información de nuestra red wifi.

### FluiddOS

Al igual que Mainsail Fluidd también ha creado una distribución con todo instalado.

1. Descargaremos la última versión de MainsailOS desde [**aquí**](https://github.com/cadriel/FluiddPI/releases).
2. Descomprimiremos el zip donde obtendremos un .img
3. Utilizando [**BalenaEtcher**](https://www.balena.io/etcher/) escribiremos .img a nuestra SD (8GB o mayor además de idealmente que sea una SD de alta velocidad)

{% hint style="danger" %}
**ESTE PROCESO BORRARÁ TODO EL CONTENIDO DE NUESTRA SD.**
{% endhint %}

* Si usamos wifi, editaremos el fichero _fluiddpi-wpa-supplicant.txt_ donde añadiremos la información de nuestra red wifi.

## Creando nuestro firmware Klipper

Una vez a tenemos nuestro OS instalado y con Klipper, Moonraker y la interfaz que mas nos guste instalada es hora de pasar a crear nuestro firmware Klipper.

Ya que hemos Klipper este nos va a permitir de una forma muy sencilla a los diferentes pasos para realizar el proceso.

### Creando el firmware

Accederemos a Kiauh desde SSH

![](<.gitbook/assets/image (11).png>)

Elegiremos la opción más adecuada para nuestra placa ya que en ocasiones nos interesará solamente hacer el Build del firmware para después extraerlo, Flash to aplicarlo a nuestra placa si es compatible con el proceso o Build + Flash que realizaría todo el proceso.

{% hint style="info" %}
Podemos lanzar el proceso desde linea de comandos directamente:

```
 sudo apt install make
 cd ~/klipper
 make clean
 make menuconfig
```
{% endhint %}

Os facilitamos la configuración para las electrónicas que hemos probado:

{% tabs %}
{% tab title="SKR Octopus (PRO)" %}
Elegiremos las siguientes opciones dependiendo del procesador/version de nuestra Octopus:

![](<.gitbook/assets/image (15).png>)

![](<.gitbook/assets/image (5).png>)

Una vez tengamos todas las opciones ajustadas pulsaremos _**q**_ para salir y "_**Yes**_" para almacenar la configuracion, si lanzamos el proceso desde Kiauh nos realizará directamente el comando _**make**_.

Una vez terminado el compilado del firmware podremos encontrar el binario _**klipper.bin**_ en el directorio _**/home/pi/klipper/out**_  el cual podremos aplicar directamente por DFU o usando la SD tal como tenemos en [**nuestra guía**](broken-reference).
{% endtab %}

{% tab title="Fysetc Spider" %}
Elegiremos las siguientes opciones dependiendo del procesador/version de nuestra Spider:

![](<.gitbook/assets/image (20).png>)

{% hint style="info" %}
**Si tu Spider es posterior al 23/6/2021 elige como Bootloader offset 32KiB bootloader.**

**Si tu Spider es anterior al 23/6/2021 elige como Bootloader offset 64KiB bootloader.**
{% endhint %}

Una vez tengamos todas las opciones ajustadas pulsaremos _**q**_ para salir y "_**Yes**_" para almacenar la configuracion, si lanzamos el proceso desde Kiauh nos realizará directamente el comando _**make**_.

Una vez terminado el compilado del firmware podremos encontrar el binario _**klipper.bin**_ en el directorio _**/home/pi/klipper/out**_  el cual podremos aplicar directamente por DFU o usando la SD tal como tenemos en [**nuestra guía**](broken-reference).
{% endtab %}
{% endtabs %}

### Verificando la conexión

Ahora que tenemos nuestro firmware Klipper en nuestra electrónica procederemos a verificar que tenemos comunicación con ella, un paso previo y necesario antes de continuar con la configuración de Klipper.

![](<.gitbook/assets/image (9).png>)

Elegiremos el tipo de conexión entre nuestra electrónica y la Pi, normalmente y aconsejable USB:

![](<.gitbook/assets/image (2).png>)

{% hint style="info" %}
**En el caso que usemos Klipper por los pines GPIO deberemos habilitar la comunicación serial en nuestra pi, para simplificar el proceso teneis aqui unos comandos para que sea más sencillo:**

**sudo raspi-config nonint do\_serial 2**&#x20;

**echo dtoverlay=pi3-disable-bt | sudo tee -a /boot/config.txt**&#x20;

**sudo reboot**
{% endhint %}

En el caso que no detecte nuestra electrónica deberemos verificar el proceso de aplicar el firwmare Klipper o el cableado:

![](<.gitbook/assets/image (12).png>)

&#x20;En el este correcto nos listará un dispositivo, es importante anotarse este ya que lo necesitaremos más adelante:

![Deberemos copiar lo marcado para usarlo en los ficheros de configuración de Klipper](<.gitbook/assets/image (18).png>)

{% hint style="info" %}
En el caso que no realicemos el proceso desde Kiauh podemos usar el comando _**ls /dev/serial/by-id**_ para listar los dispositivos conectados.
{% endhint %}

