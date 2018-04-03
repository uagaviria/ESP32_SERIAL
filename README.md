# ESP32_SERIAL


Si usas el IDE de Arduino para programar el ESP32, es posible que el uso del UART 1. requiera un cambio de pines para que funcione.

Solo obtener acceso a los UART adicionales no es dif�cil. Simplemente usa uno de los objetos de puerto en serie adicionales disponibles. Sin embargo, habilitar UART 1 hace que el ESP32 se bloquee. La raz�n es que, de manera predeterminada, UART 1 usa los mismos pines que la memoria flash ESP32.

Afortunadamente, el chip tiene un interruptor de matriz que puede colocar casi cualquier pin de E / S l�gico en cualquier pin de E / S f�sico.para no ir a modificar el c�digo HardwareSerial.cpp, y asignar al UART 1 los pines no utilizados, lo que hace que todo funcione. es un cambio simple, reemplazando dos par�metros en el propio codigo, entre otras cosas, mapea los pines de E / S. Puede usar la t�cnica para reubicar los UART en otros lugares si lo desea.
