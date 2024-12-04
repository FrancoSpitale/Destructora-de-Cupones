Este programa corresponde a un sistema diseñado por Franco Spitale, estudiante de Ingeniería Electrónica, para la gestión y destrucción de tickets en un centro de entretenimiento. A continuación, te proporciono un desglose de los principales elementos funcionales y las variables clave, junto con una descripción técnica del sistema:

Función del Programa
El programa controla una "Destructora de Tickets", que utiliza un PIC16F876 para automatizar la gestión de:

Detección y conteo de tickets mediante sensores.
Almacenamiento de datos en una memoria EEPROM.
Visualización de datos en displays de 7 segmentos y un display LCD.
Interacción del usuario a través de pulsadores para grabar, leer, resetear y visualizar datos almacenados.
Componentes Principales
Sensores:

sensor_1: Conectado al pin A0 del PIC, detecta el estado del primer sensor que "enciende" el motor al activarse.
sensor_2: Detecta el paso de tickets y realiza el conteo correspondiente.
Pulsadores:

Grabar: Almacena un número de 32 bits en la memoria EEPROM del PIC, dividiéndolo en 4 partes debido a las limitaciones del tamaño de la EEPROM.
Read: Permite leer los 7 últimos números almacenados en la memoria. El pulsador debe activarse 7 veces para salir del modo de lectura.
Reset: Borra la cuenta actual mostrada en los displays de 7 segmentos.
Reset + Grabar: Cuando se presionan ambos pulsadores simultáneamente, se resetea la cuenta acumulada y esta se actualiza en el display LCD.
Memoria EEPROM:

Los datos de los últimos 7 días se almacenan utilizando una estructura de memoria tambor.
Cuando la memoria llega al día 6, la próxima grabación sobrescribe los datos del día 0.
Timer 0:

Utilizado para generar la interrupción que permite la multiplexación de los displays de 7 segmentos, a través de la función Visualizar.
Displays:

7 Segmentos: Muestran la cuenta actual.
LCD: Muestra la cuenta acumulada y otros datos relevantes.
Flujo de Operación
Modo Normal:

El sistema utiliza los sensores para detectar y contar tickets.
Los displays de 7 segmentos muestran la cuenta actual.
El LCD muestra la cuenta acumulada de todos los tickets procesados.
Grabación:

Presionando el pulsador "Grabar", se almacena un número de 32 bits (como la cuenta de tickets procesados) en la memoria EEPROM. Este número se divide en 4 bloques para ajustarse al tamaño de la EEPROM.
Lectura:

El pulsador "Read" permite recorrer los últimos 7 números almacenados. Cada pulsación muestra un número en los displays.
Reset:

Borra la cuenta actual en los displays de 7 segmentos.
Si se presionan "Reset" y "Grabar" simultáneamente, se borra la cuenta acumulada.
Ciclo de Memoria Tambor:

Los datos almacenados en la memoria EEPROM utilizan un esquema circular.
Al llegar al día 6, el próximo dato se almacena sobrescribiendo el registro correspondiente al día 0.
Interrupción Timer 0:

Maneja la multiplexación de los displays de 7 segmentos para optimizar el uso de pines del PIC y garantizar una visualización estable.
