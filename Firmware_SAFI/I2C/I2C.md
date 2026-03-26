# 🚀 Sistema de Telemetría Aeroespacial (MPU6050 + BMP180)

Un dashboard profesional en Python para visualización en tiempo real de datos inerciales y atmosféricos adquiridos mediante un Arduino. Este proyecto integra una IMU de 6 ejes (MPU6050) y un sensor barométrico/altímetro (BMP180) en una sola interfaz gráfica con modelado 3D y gráficas de auto-scroll.

## 📡 Arquitectura y Protocolos de Comunicación

Este proyecto utiliza dos capas principales de comunicación para lograr la transmisión de datos en tiempo real (50Hz) sin cuellos de botella:

### 1. Comunicación Hardware a Sensores: I2C (Inter-Integrated Circuit)

Tanto el MPU6050 como el BMP180 utilizan el protocolo **I2C**. Este es un bus de comunicación síncrona que permite conectar múltiples dispositivos usando solo dos cables:
*   **SDA (Serial Data Line):** Transmite los datos.
*   **SCL (Serial Clock Line):** Sincroniza la transmisión.

**¿Cómo funciona sin que los datos choquen?**
El protocolo I2C funciona mediante un sistema de "Maestro y Esclavos". El Arduino actúa como Maestro y los sensores como Esclavos. Cada sensor tiene una dirección hexadecimal única grabada de fábrica:
*   Dirección I2C del **MPU6050**: `0x68`
*   Dirección I2C del **BMP180**: `0x77`

Al solicitar datos, el Arduino "llama" a la dirección específica en el bus compartido, asegurando que solo ese sensor responda. Esto nos permite conectar ambos módulos en paralelo a los mismos pines del Arduino.

### 2. Comunicación Arduino a PC: UART (Serial USB)
Una vez que el Arduino recolecta los datos de ambos sensores, los empaqueta y los transmite a la computadora mediante el puerto Serie (UART) a una velocidad alta de **115200 baudios**. 

El formato de transmisión es un **CSV (Valores Separados por Comas)** estricto. Cada paquete (línea) contiene 9 variables seguidas de un salto de línea (`\n`):
`ax, ay, az, gx, gy, gz, temperatura, presion, altitud\n`

El programa en Python lee este buffer serial, separa los valores por las comas, aplica filtros matemáticos (Kalman y Filtro Complementario) y actualiza la GUI.

---

## 🛠️ Esquema de Conexión (Hardware)

Puedes utilizar un Arduino Uno, Nano o Mega. Las conexiones I2C estándar son:

| Sensor (Pin) | Arduino Uno/Nano | Arduino Mega 2560 |
| :--- | :--- | :--- |
| **VCC** (Ambos) | 5V / 3.3V* | 5V / 3.3V* |
| **GND** (Ambos) | GND | GND |
| **SDA** (Ambos) | A4 | Pin 20 (SDA) |
| **SCL** (Ambos) | A5 | Pin 21 (SCL) |

*\*Nota: Si tus módulos MPU6050/BMP180 tienen regulador de voltaje integrado, conéctalos a 5V. Si son módulos puramente de 3.3V, usa el pin de 3.3V del Arduino para evitar daños lógicos.*

---

## 💻 Requisitos y Configuración (Software)

### 1. Preparar el Arduino (C++)
Asegúrate de tener instalado el **Arduino IDE** y descargar la siguiente librería desde el *Gestor de Librerías*:
*   `Adafruit BMP085 Library` (Compatible con BMP180)

Carga el código fuente `telemetria_sensores.ino` en tu placa.

### 2. Preparar el Entorno Python
El Dashboard fue construido para ser ligero y de alto rendimiento. Requiere Python 3.7 o superior.

Abre tu terminal o símbolo del sistema e instala las dependencias necesarias ejecutando:

```bash
pip install pyqt5 pyqtgraph PyOpenGL pyserial numpy
