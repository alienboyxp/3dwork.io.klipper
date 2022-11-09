# Nivelación cama

Como paso previo a otros tests debemos asegurarnos que nuestra cama o base de impresión esté completamente nivelada.&#x20;

## Nivelación Manual

Para ello usaremos la función SCREWS\_TILT\_CALCULATE de Klipper.

### Definición de puntos de ajuste

Para poder realizar una nivelación manual con los tornillos de ajuste de nuestra base de impresión lo primero que deberemos hacer es definir los puntos donde emplazar nuestro hotend para poder realizar el ajuste dentro de nuestro fichero de configuración printer.cfg o en el caso de usar includes en el que queramos definir esta parte de nuestra configuración:

{% tabs %}
{% tab title="Ejemplo" %}
```
[bed_screws]
screw1: 70,213
screw1_name: trasero izquierdo
screw2: 235,213
screw2_name: trasero derech0
screw3: 70,47
screw3_name: frontal izquierdo
screw4: 235,47
screw4_name: frontal derecho
```


{% endtab %}

{% tab title="Voron0.1" %}
```
[bed_screws]
screw1: 65,5
screw1_name: front screw
screw2: 10,110
screw2_name: back left
screw3: 110,110
screw3_name: back right
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Deberemos definir estos puntos dependiendo de nuestra máquina, la ubicación de los tornillos de ajuste de nuestra cama y el tamaño de nuestro hotend asegurando que mecánicamente es viable la ubicación del punto de sondeo.**
{% endhint %}

### Proceso de nivelación:

Una vez realizado el cambio en nuestra configuración y validada que no de problemas comenzaremos con el proceso que podemos hacer desde la ventana terminal/consola:

```
# Hacemos un home de todos los ejes

G28

# Lanzamos el asistente de nivelación de cama

BED_SCREWS_ADJUST
```

La máquina moverá el cabezal de impresión al primer punto de sondeo y con el típico papel ajustaremos el tornillo a nuestro gusto.

Si hemos tenido que ajustar el tornillo más de 1/8 de giro de tornillo usaremos en la termina/consola el comando ADJUSTED y si no hemos necesitado apenas ajuste ACCEPT.

Cuando terminemos el asistente o ciclo de nivelación finalizaremos con ABORT y ya podremos realizar los siguientes pasos en nuestra calibración!!!.

## Nivelación con sensor

### Nivelación manual cama con sensor

En el caso que dispongamos un sensor de nivelación podemos usarlo para simplificar y hacer más fiable la nivelación manual de nuestra cama.

Klipper nos facilita dos macros que nos van a ayudar en la nivelación asistida de nuestra cama:

* BED\_TILT va a mover entre los puntos de lectura predefinidos para nivelar o ajustar las alturas de los motores de Z
* SCREWS\__TILT\__CALCULATE realiza un check de los puntos de lecturas definidos en _\[screws\_tilt\_adjust section]_  de nuestro printer.cfg para nivelación, una vez realizadas las lecturas en esos puntos nos sugerirá el ajuste manual en los tornillos de ajuste de nuestra cama. Realizaremos este proceso varias veces hasta que no sugiera apenas correcciones

Una vez hayamos realizado ambos procesos ejecutaremos Z\__ENDSTOP\__CALIBRATE que llevara nuestro nozzle a la posición Z =0 correcta

### Ajuste del Z-Offset (usando papel o galga)

Encenderemos nuestra impresora

Turn on the printer, home all axis and perform Quad Gantry Level aka QGL (Diagram 1.1). Check that Current Offset value in “Z Baby Stepping” panel is 0.

Please note that Z Offest calibration is performed at room temperature, with heatbed and hotend heaters off (set to 0). Ensure that there is no filament on the nozzle before calibrating Z Offset. You may want to heat the hotend, clear the nozzle and/or unload the filament and let it cool down before proceeding.

Place regular piece of copy machine paper between the printer's bed and nozzle (Diagram 1.2). Note that there should be a gap of 5-6 millimeters between the nozzle and the paper at this stage.

Go to the “Console” panel, type PROBE\_CALIBRATE command and press “Send” button (Diagram 1.3). Responses like “Starting manual Z probe...” identify that you are in manual (Z Offset) probe calibration mode now.

Now start lowering the nozzle, until it is just touching the paper. To do that you will typing a series of TESTZ Z=\[nnn] commands into the Console (pressing the “Send” button after each one), replacing \[nnn] with a positive value in mm when you need to raise the nozzle or negative value in mm when you need to lower the nozzle.

You can use Copy & Past to avoid manual typing or press the Up Arrow key on your keyboard while in the Console to recall previously entered command.

Baby Step Offset

Home and QGL&#x20;
