# Input Shaper

Una de las grandes funcionalidades de Klipper, y que vamos a ver próximamente en otros firmwares como Marlin o Duet, es el soporte a **Input Shaping** que es una **técnica que permite reducir las vibraciones/ondas** (ringing, echoin, ghosting, rippling son otros nombres de ese tipo de artefactos).

![](https://2779286893-files.gitbook.io/\~/files/v0/b/gitbook-legacy-files/o/assets%2F-MTqLw6KI5FruaRNEMZD%2F-MlBDr0zKVSYS7o5qRDK%2F-MlEsn2D3yoymItclUyH%2Fimage.png?alt=media\&token=72aafc78-4bb2-4bb5-8fe3-08a7c6833e57)

Ejemplo de vibraciones/ondas en nuestras impresiones.

Este tipo de artefactos están **producidos por vibraciones mecánicas** originadas normalmente por los movimientos bruscos en los cambios de direcciones. Algo **ocasionado normalmente por... un chasis no suficientemente rigido, correas muy o poco tensas, problemas de alineación en partes del chasis o cinemática, movimientos de masas grandes en los ejes de movimiento, etc**... por lo que es aconsejable que antes de comenzar en estos ajustes nos aseguremos que hemos intentado solventar lo máximo posible los fallos más comunes comentados.

Dado que es un proceso muy extenso os vamos a explicar las dos formas de poder ajustar Input Shaping facilitando links a la documentación oficial, recordaros que **en nuestro caso usamos un sensor para medir las resonancias** de nuestra máquina:

![](https://2779286893-files.gitbook.io/\~/files/v0/b/gitbook-legacy-files/o/assets%2F-MTqLw6KI5FruaRNEMZD%2F-MlBDr0zKVSYS7o5qRDK%2F-MlEuuerZG4AgP-fWYkr%2Fimage.png?alt=media\&token=4bd272b9-f098-4a9e-a7d6-d2efeccd851a)

Ajuste de Input Shaping manual.

* **​**[**Compensación de resonancias usando un acelerómetro**](https://www.klipper3d.org/Measuring\_Resonances.html), en nuestro caso al usarlo en otras máquinas nos decantamos por usar un **acelerómetro ADXL345 para la medición automática** de resonancias que podéis encontrar el proceso en el link anterior. El proceso es un poco laborioso en la instalación de ciertos componentes software y require de un cableado extra pero por los resultados obtenidos creemos que vale la pena.
