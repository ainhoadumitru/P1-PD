# Práctica 1 – Control de LED y comunicación por puerto serie

## 1. Objetivo

El objetivo de esta práctica es programar un microcontrolador (ESP32/Arduino) para controlar un LED y enviar información por el puerto serie.
El programa debe encender y apagar un LED cada 500 milisegundos y enviar mensajes al monitor serie indicando el estado del LED.

---

# 2. Funcionamiento del programa

El programa realiza las siguientes acciones:

1. Inicializa el pin del LED como salida.
2. Inicializa la comunicación por el puerto serie.
3. Ejecuta un bucle infinito donde:

   * Enciende el LED.
   * Envía el mensaje **"ON"** por el puerto serie.
   * Espera 500 ms.
   * Apaga el LED.
   * Envía el mensaje **"OFF"** por el puerto serie.
   * Espera 500 ms.

Este proceso se repite continuamente.

---

# 3. Código del programa

```cpp
#include <Arduino.h>

#define LED_BUILTIN 2
#define DELAY 500

void setup() {
  pinMode(LED_BUILTIN, OUTPUT);   // Configurar LED como salida
  Serial.begin(115200);           // Iniciar comunicación serie
}

void loop() {

  digitalWrite(LED_BUILTIN, HIGH);   // Encender LED
  Serial.println("ON");              // Mensaje por puerto serie
  delay(DELAY);                      // Esperar 500 ms

  digitalWrite(LED_BUILTIN, LOW);    // Apagar LED
  Serial.println("OFF");             // Mensaje por puerto serie
  delay(DELAY);                      // Esperar 500 ms

}
```

---

# 4. Diagrama de flujo

```
Inicio
  |
  v
Configurar pin LED como salida
  |
  v
Iniciar comunicación serie
  |
  v
Encender LED
  |
  v
Enviar "ON"
  |
  v
Esperar 500 ms
  |
  v
Apagar LED
  |
  v
Enviar "OFF"
  |
  v
Esperar 500 ms
  |
  v
Repetir bucle
```

---

# 5. Diagrama de tiempos

```
Tiempo (ms)

0 ms        500 ms        1000 ms        1500 ms

LED
ON  ─────────────
OFF               ─────────────
ON                               ─────────────
OFF                                              ─────────────
```

El LED permanece encendido durante 500 ms y apagado durante otros 500 ms.
El ciclo completo dura 1000 ms (1 segundo) y se repite continuamente.

---

# 6. Tiempo libre del procesador

El programa utiliza dos retardos:

* `delay(500)`
* `delay(500)`

El tiempo total de cada ciclo es:

```
500 ms + 500 ms = 1000 ms
```

Durante la ejecución de `delay()` el procesador permanece en espera, por lo que no realiza otras tareas.

Por lo tanto, el tiempo libre del procesador es aproximadamente **1000 ms por ciclo**, descontando el pequeño tiempo necesario para ejecutar las instrucciones del programa.

---

# 7. Conclusión

En esta práctica se ha aprendido a:

* Configurar pines digitales como salida.
* Controlar un LED mediante programación.
* Utilizar el puerto serie para enviar mensajes al ordenador.
* Comprender el funcionamiento de los retardos (`delay`) y su efecto en el uso del procesador.

El resultado es un sistema simple que permite observar tanto el comportamiento físico del LED como la comunicación con el ordenador a través del monitor serie.
