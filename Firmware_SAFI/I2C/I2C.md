# Sistema de Telemetría Aeroespacial (MPU6050 + BMP180)

Un dashboard profesional en Python para visualización en tiempo real de datos inerciales y atmosféricos adquiridos mediante un microcontrolador. Este proyecto integra una IMU de 6 ejes (MPU6050) y un sensor barométrico/altímetro (BMP180) en una sola interfaz gráfica con modelado 3D y gráficas de auto-scroll.

## Arquitectura y Protocolos de Comunicación

Este proyecto utiliza dos capas principales de comunicación para lograr la transmisión de datos en tiempo real (50Hz) sin cuellos de botella:

### 1. Comunicación Hardware a Sensores: I2C (Inter-Integrated Circuit)
Tanto el MPU6050 como el BMP180 utilizan el protocolo **I2C**. Este es un bus de comunicación síncrona que permite conectar múltiples dispositivos usando solo dos cables:
* **SDA (Serial Data Line):** Transmite los datos.
* **SCL (Serial Clock Line):** Sincroniza la transmisión.

**¿Cómo funciona sin colisiones de datos?**
El protocolo I2C funciona mediante una arquitectura de "Maestro y Esclavos". El microcontrolador actúa como Maestro y los sensores como Esclavos. Cada sensor tiene una dirección hexadecimal única grabada de fábrica:
* Dirección I2C del **MPU6050**: `0x68`
* Dirección I2C del **BMP180**: `0x77`

Al solicitar datos, el microcontrolador "llama" a la dirección específica en el bus compartido, asegurando que solo ese sensor responda. Esto nos permite conectar ambos módulos en paralelo a los mismos pines físicos.

### 2. Comunicación Microcontrolador a PC: UART (Serial USB)
Una vez que el microcontrolador recolecta los datos de ambos sensores, los empaqueta y los transmite a la computadora mediante el puerto Serie (UART) a una alta velocidad de **115200 baudios**. 

El formato de transmisión es un **CSV (Valores Separados por Comas)** estricto. Cada paquete (línea) contiene 9 variables seguidas de un salto de línea (`\n`):
`ax, ay, az, gx, gy, gz, temperatura, presion, altitud\n`

El programa en Python lee este buffer serial, separa los valores por las comas, aplica filtros matemáticos (Kalman y Filtro Complementario) y actualiza la interfaz gráfica.

---

## Esquema de Conexión (Hardware)

Puedes utilizar la placa de desarrollo de tu preferencia. Las conexiones I2C estándar para nuestra arquitectura son las siguientes:

| Pin del Sensor | Arduino Uno / Nano | ESP32 | Raspberry Pi Pico |
| :--- | :--- | :--- | :--- |
| **VCC** | 5V / 3.3V* | 3.3V | 3.3V (Pin 36 - 3V3 Out) |
| **GND** | GND | GND | GND |
| **SDA** | A4 | GPIO 21 | GP4 (I2C0 SDA) |
| **SCL** | A5 | GPIO 22 | GP5 (I2C0 SCL) |

> **ADVERTENCIA ELÉCTRICA:** Verifique rigurosamente si sus módulos MPU6050 y BMP180 cuentan con regulador de voltaje integrado (LDO) antes de conectarlos a `5V` (Arduino). Si utiliza el **ESP32** o la **Raspberry Pi Pico**, conecte los sensores **exclusivamente a 3.3V** para evitar daños irreversibles a los pines lógicos.

---

## Estructura del Directorio

En la misma ubicación que este documento (`I2C.md`), se encuentran tres subdirectorios dedicados a la prueba y ejecución modular de cada sensor. 

Cada carpeta contiene tanto el firmware de adquisición en C++ (`.ino`) como el software de telemetría en Python (`.py`) correspondientes a su nivel de integración:

* 📁 **`/MPU`**: Archivos `MPU.ino` y `MPU.py` (Adquisición y visualización exclusiva de la IMU de 6 ejes).
* 📁 **`/MBP`**: Archivos `MBP.ino` y `MBP.py` (Adquisición y visualización exclusiva del barómetro/altímetro).
* 📁 **`/MPUMBP`**: Archivos `MPUMBP.ino` y `MPUMBP.py` (Integración y fusión total de ambos sensores).

---

## Requisitos y Guía de Ejecución (Software)

### 1. Preparar el Microcontrolador (C++)
Asegúrate de tener instalado el **Arduino IDE** y descargar la siguiente biblioteca desde el *Gestor de Librerías*:
* `Adafruit BMP085 Library` (Compatible con el sensor BMP180).

Abre la carpeta de la prueba que deseas realizar (ej. `MPUMBP`), carga el código fuente `.ino` en tu placa y **cierra el Monitor Serie** del Arduino IDE. Si lo dejas abierto, el puerto quedará bloqueado y Python no podrá interceptar los datos.

### 2. Preparar el Entorno Python
El Dashboard fue construido para ser ligero y de alto rendimiento. Requiere Python 3.7 o superior. Abre tu terminal (en Windows o Ubuntu) e instala las dependencias necesarias ejecutando:

### 3. Ejecución de la Interfaz Gráfica
Una vez instaladas las bibliotecas y con el microcontrolador conectado por USB, sigue estos pasos en tu terminal (Símbolo del sistema, PowerShell o Bash) para lanzar la telemetría:

**Navega a la ruta exacta del directorio:**
   Debes usar el comando `cd` para moverte a la ubicación específica de tu computadora donde descargaste o clonaste la carpeta que contiene el archivo de Python. Por ejemplo:
   ```bash ejemplo
   C:\Users\elesi> cd Downloads
C:\Users\elesi\Downloads> python MPU.py
```bash

pip install pyqt5 pyqtgraph PyOpenGL pyserial numpy
