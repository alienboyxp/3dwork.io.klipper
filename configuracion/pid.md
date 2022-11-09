# PID

![](https://2779286893-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MTqLw6KI5FruaRNEMZD-887967055%2Fuploads%2FRsW9JxjLjQ3pbX6X4RMe%2Fimage.png?alt=media\&token=fc3753f9-f6bb-455c-9de8-91474588405e)

### &#x20;<a href="#ajuste-pid" id="ajuste-pid"></a>

Klipper con sus comandos extendidos Gcode hacen que el proceso para ajustar el PID sea muy sencillo. Podemos seguir los siguientes pasos para realizarlos:

* Desde la ventana de CONSOLA lanzaremos los comandos necesarios para realizar el proceso.
* Primero nos aseguraremos de que nuestros calentadores estén apagados con el comando TURN\_OFF\_HEATERS y esperaremos a que estos se encuentren a temperatura ambiente.
* Lanzaremos el comando PID_CALIBRATE HEATER=\<nombrecalentador> TARGET=\<temperatura> donde para nombre_\_calentador usaremos el nombre asignado al calentador que queramos realizar el PID, normalmente extruder o bed, y en temperatura la temperatura a la cual queramos realizar el PID.

En el caso de calibrar el hotend/extrusor es aconsejable colocar el nozzle a unos 5mm de la cama, activar los ventiladores de capa al 100% y calentar la cama a la temperatura normal de impresión. De esta forma realizará el PID en las peores condiciones posibles para asegurarnos un ajuste óptimo.

* Esperaremos a que el proceso termine, y usaremos SAVE\_CONFIG para guardar nuestro nuevo PID

![](https://2779286893-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MTqLw6KI5FruaRNEMZD-887967055%2Fuploads%2F4wVV8DgZXYpPVY6QjYEV%2Fimage.png?alt=media\&token=7ac053bb-0d2e-4293-a9cd-20019732c87b)

Durante el proceso veremos como varía la gráfica de temperaturas y al finalizar nos muestra los valores PID calculados y la opción de guardarlos con SAVE\_CONFIG

* Para asegurarnos que los valores nuevos de PID se aplican es aconsejable reiniciar el firmware de la impresora.

![](https://2779286893-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MTqLw6KI5FruaRNEMZD-887967055%2Fuploads%2FDXzEhF2Z6Z2Kxn3CJOyT%2Fimage.png?alt=media\&token=b5bb0019-5be1-441b-a037-af4c42647c6c)

A continuación puedes ver información extendida con referencia al PID:

* **Nombres de nuestros calentadores configurados,** Si no estas seguro del nombre de tus calentadores ves al fichero de configuración y busca los nombres... normalmente se usa extruder para el hotend y heater\_bed para la cama.
* **Log**, en caso de tener problemas para calcular el PID es aconsejable activar el log del proceso. Para hacer esto añadiremos WRITE_FILE=1 al final de la lina PID_\_CALIBRATE. Esto creará un fichero de log llamado /tmp/heattest.txt con información detallada del proceso que seguro que nos ayudará a encontrar el problema.
* **Comando PID no funciona**, en el caso que el comando de calibración del PID no haga nada deberemos buscar en los ficheros de configuración por la clase PIDCalibrate el cual habilita el comando PID\_CALIBRATE.
* **Valores PID no se actualizan**, si al hacer el SAVE_CONFIG no actualiza automáticamente nuestros valores PID podemos añadirlos de forma manual. Abriremos nuestro printer.cfg y buscaremos dichos valores en las secciones de extruder o heater\_bed y actualizaremos manualmente a los nuevos valores._
* _**PID sin resultados**, si no encontramos los valores nuevos del PID en nuestra consola gcode o en la configuración es aconsejable revisar el klippy.log para encontrarlos y ponerlos de forma manual en nuestro printer.cfg._

### &#x20;<a href="#links" id="links"></a>

Klipper: PID Tuning – Simply Explained

Fuente de información original
