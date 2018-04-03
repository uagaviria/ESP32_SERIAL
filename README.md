# ESP32_SERIAL


Si usas el IDE de Arduino para programar el ESP32, es posible que el uso del UART 1. requiera un cambio de pines para que funcione.

Solo obtener acceso a los UART adicionales no es difícil. Simplemente usa uno de los objetos de puerto en serie adicionales disponibles. Sin embargo, habilitar UART 1 hace que el ESP32 se bloquee. La razón es que de manera predeterminada, UART 1 usa los mismos pines que la memoria flash ESP32.

Afortunadamente, el chip tiene un interruptor de matriz que puede colocar casi cualquier pin de E / S lógico en cualquier pin de E / S físico.para no ir a modificar el código HardwareSerial.cpp, y asignar al UART 1 los pines no utilizados, lo que hace que todo funcione. es un cambio simple, reemplazando dos parámetros en el propio codigo, entre otras cosas, mapea los pines de E / S. Puede usar la técnica para reubicar los UART en otros lugares si lo desea.

```C++
#include <Arduino.h>
HardwareSerial Serial1(1);
HardwareSerial Serial2(2);

#define RXD1 4
#define TXD1 2

#define RXD2 16
#define TXD2 17

void setup() {
  // Note the format for setting a serial port is as follows: Serial2.begin(baud-rate, protocol, RX pin, TX pin);
  Serial.begin(115200); // El TXD Y RXD del modulo son los de la programacion (debug)
  Serial1.begin(115200, SERIAL_8N1, RXD1, TXD1);// serial1 pines 4 y 2
  Serial2.begin(115200, SERIAL_8N1, RXD2, TXD2);// serial2 pines 16 y 17

}

void loop() { //Choose Serial1 or Serial2 as required

  Serial.println("ESTE MENSAJE ES ENVIADO POR EL USB SERIAL: ");
  Serial1.println("ESTE MENSAJE ES ENVIADO POR SERIAL1: ");
  Serial2.println("ESTE MENSAJE ES ENVIADO POR SERIAL2: ");
  delay(1000);
  // while (Serial2.available()) {
  //   Serial.print(char(Serial2.read()));
  // }
}


/* Baud-rates available: 300, 600, 1200, 2400, 4800, 9600, 14400, 19200, 28800, 38400, 57600, or 115200, 256000, 512000, 962100
 *
 *  Protocols available:
 * SERIAL_5N1   5-bit No parity 1 stop bit
 * SERIAL_6N1   6-bit No parity 1 stop bit
 * SERIAL_7N1   7-bit No parity 1 stop bit
 * SERIAL_8N1 (the default) 8-bit No parity 1 stop bit
 * SERIAL_5N2   5-bit No parity 2 stop bits
 * SERIAL_6N2   6-bit No parity 2 stop bits
 * SERIAL_7N2   7-bit No parity 2 stop bits
 * SERIAL_8N2   8-bit No parity 2 stop bits
 * SERIAL_5E1   5-bit Even parity 1 stop bit
 * SERIAL_6E1   6-bit Even parity 1 stop bit
 * SERIAL_7E1   7-bit Even parity 1 stop bit
 * SERIAL_8E1   8-bit Even parity 1 stop bit
 * SERIAL_5E2   5-bit Even parity 2 stop bit
 * SERIAL_6E2   6-bit Even parity 2 stop bit
 * SERIAL_7E2   7-bit Even parity 2 stop bit
 * SERIAL_8E2   8-bit Even parity 2 stop bit
 * SERIAL_5O1   5-bit Odd  parity 1 stop bit
 * SERIAL_6O1   6-bit Odd  parity 1 stop bit
 * SERIAL_7O1   7-bit Odd  parity 1 stop bit
 * SERIAL_8O1   8-bit Odd  parity 1 stop bit
 * SERIAL_5O2   5-bit Odd  parity 2 stop bit
 * SERIAL_6O2   6-bit Odd  parity 2 stop bit
 * SERIAL_7O2   7-bit Odd  parity 2 stop bit
 * SERIAL_8O2   8-bit Odd  parity 2 stop bit
*/
```
<img src='https://github.com/uagaviria/ESP32_SERIAL/blob/master/img/SERIAL1.png' />

