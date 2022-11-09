# Configuración Klipper en laminadores

\[gcode\_macro START\_PRINT]

\#Get Printer built volume dimensions

\{% set X\_MAX = printer.toolhead.axis\_maximum.x|default(100)|float %\}

\{% set Y\_MAX = printer.toolhead.axis\_maximum.y|default(100)|float %\}

\{% set Z\_MAX = printer.toolhead.axis\_maximum.z|default(100)|float %\}

\#Get Nozzle diameter and filament width for conditioning

\{% set NOZZLE = printer.extruder.nozzle\_diameter|default(0.4)|float %\}

\{% set FILADIA = printer.extruder.filament\_diameter|default(1.75)|float %\}

\#Set Start coordinates of priming lines

\{% set X\_START = 10.0|default(10.0)|float %\}

\{% set Y\_START = 20.0|default(20.0)|float %\}

\#Calculate Primer line extrusion volume and filament length

\{% set PRIMER\_WIDTH = 0.75 \* NOZZLE %\}

\{% set PRIMER\_HEIGHT = 0.70 \* NOZZLE %\}

\{% set PRIMER\_SECT = PRIMER\_WIDTH \* PRIMER\_HEIGHT %\}

\{% set PRIMER\_VOL = PRIMER\_SECT \* (X\_MAX - 3 \* X\_START) %\}

\{% set FILA\_SECT = 3.1415 \* ( FILADIA / 2.0)\*\*2 %\}

\{% set FILA\_LENGTH = 1.55 \* PRIMER\_VOL / FILA\_SECT %\}

\#Get Bed and Extruder temperature from Slicer GCode

\{% set BED\_TEMP = params.BED\_TEMP|default(60)|float %\}

\{% set EXTRUDER\_TEMP = params.EXTRUDER\_TEMP|default(190)|float %\}

G1 Y{Y\_MAX - 20} Z{Z\_MAX/4.0} F6000

G1 X{X\_START} Y{Y\_START} Z{PRIMER\_HEIGHT} F6000.0

G1 X{X\_MAX - 2 \* X\_START} Y{Y\_START} Z{PRIMER\_HEIGHT} F2000.0

G1 X{X\_MAX - 2 \* X\_START} Y{Y\_START + PRIMER\_WIDTH} Z{PRIMER\_HEIGHT}

G1 X{X\_START} Y{Y\_START + PRIMER\_WIDTH} Z{PRIMER\_HEIGHT} F2000.0
