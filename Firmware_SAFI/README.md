# 🧠 Firmware y Protocolos de Comunicación - Aviónica LANIAKEA

<p align="center">
  <img src="[PON_AQUI_TU_FOTO_DE_PORTADA.jpg]" alt="Banner de Firmware SAFI" width="800">
</p>

Bienvenido al directorio de programación de la computadora de vuelo **LANIAKEA** del **Capítulo SAFI**. 

El objetivo de esta sección es centralizar los códigos fuente, librerías y diagramas de conexión necesarios para la telemetría, el control de actuadores y el registro de datos de nuestro cohete experimental rumbo al **Latin American Space Challenge (LASC)** (Apogeo objetivo: 3km).

---

## 🚀 Arquitectura de Microcontroladores (MCUs)

Nuestra computadora de vuelo modular distribuye el procesamiento para evitar cuellos de botella durante el ascenso. Haz clic en el nombre de cada placa para ver sus códigos de inicialización:

* **[ESP32]([PON_AQUI_EL_ENLACE_A_LA_CARPETA_DEL_ESP32]):** Computadora central. Encargada del procesamiento pesado, filtros matemáticos y empaquetado de telemetría.
  <p align="center">
    <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/ESP32.jpg" alt="ESP32" width="200">
  </p>

* **[Arduino Nano]([PON_AQUI_EL_ENLACE_A_LA_CARPETA_DEL_NANO]):** Nodos satélite y redundancia. Manejo de actuadores (transistores, ignición, despliegue).
  <p align="center">
    <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/ARDUINONANO.jpg" alt="Arduino Nano" width="200">
  </p>

* **[Raspberry Pi Pico]([PON_AQUI_EL_ENLACE_A_LA_CARPETA_DE_LA_PICO]):** Adquisición de datos a alta velocidad y manejo de E/S.
  <p align="center">
    <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/raspberry.jpg" alt="Raspberry Pi Pico" width="200">
  </p>

---

## 📡 Protocolos de Comunicación y Módulos de Vuelo

Para garantizar la lectura de sensores sin bloqueos de código, utilizamos tres protocolos principales. *⚠️ Nota para el equipo: Revisen siempre los voltajes lógicos (3.3V vs 5V) antes de conectar cualquier pin.*

### 1. Bus I2C (Inter-Integrated Circuit)
**¿Cómo funciona?** Es un protocolo síncrono maestro-esclavo ideal para conectar múltiples sensores en la misma placa usando solo dos cables (SDA y SCL). Requiere resistencias Pull-Up.

<p align="center">
  <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/I2C.jpg" alt="Diagrama I2C" width="400">
</p>

**Módulos I2C en la computadora de vuelo:**

* 🧭 **IMU MPU6050:** Detección de orientación, aceleración y giroscopio.
  <p align="center">
    <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/MPU6050.jpg" alt="MPU6050" width="100">
  </p>

* ☁️ **Barómetro MS5611:** Cálculo de altitud para eventos de recuperación.
  <p align="center">
    <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/MS5611.jpg" alt="MS5611" width="100">
  </p>

* 📁 **[Haz clic aquí para ver los códigos y librerías I2C]([PON_AQUI_EL_ENLACE_A_LA_CARPETA_I2C])**

---

### 2. Bus UART (Serial Asíncrono)
**¿Cómo funciona?** Es una comunicación asíncrona punto a punto. Solo pueden hablar dos dispositivos a la vez. <br>
⚠️ **Regla de oro:** ¡Se conectan cruzados! El **TX** del sensor va al **RX** del microcontrolador, y viceversa.

<p align="center">
  <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/UART.png" alt="Diagrama UART" width="400">
</p>

**Módulos UART en la computadora de vuelo:**

* 📡 **Radio XBee Pro S2C:** Telemetría de largo alcance hacia la estación terrena.
  <p align="center">
    <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/Radio%20XBee%20Pro%20S2C.jpg" alt="Radio XBee Pro S2C" width="100">
  </p>

* 📍 **GPS RYS352A:** Obtención de coordenadas para la fase de recuperación.
  <p align="center">
    <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/GPS%20RYS352A.webp" alt="GPS RYS352A" width="100">
  </p>

* 📁 **[Haz clic aquí para ver los códigos de Telemetría UART]([PON_AQUI_EL_ENLACE_A_LA_CARPETA_UART])**

---

### 3. Bus SPI (Serial Peripheral Interface)
**¿Cómo funciona?** Es un protocolo síncrono de muy alta velocidad, ideal para enviar o recibir bloques masivos de información de forma simultánea (Pines: MOSI, MISO, SCK, CS).

<p align="center">
  <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/SPI.png" alt="Diagrama SPI" width="400">
</p>

**Módulos SPI en la computadora de vuelo:**

* 💾 **Módulo Adaptador MicroSD:** Datalogger ("Caja Negra") para registrar todas las variables a alta frecuencia durante el ascenso.
  <p align="center">
    <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/SD.jpg" alt="Módulo MicroSD" width="100">
  </p>

* 📁 **[Haz clic aquí para ver los códigos del Datalogger SPI]([PON_AQUI_EL_ENLACE_A_LA_CARPETA_SPI])**

---

## 📜 Reglas de Contribución para el Equipo

Si vas a subir el código de un nuevo sensor para la aviónica, sigue estos pasos:
1. **Sincroniza primero:** Antes de modificar un código, abre tu terminal y ejecuta `git pull origin main`.
2. **Comenta tus pines:** Todo archivo `.ino` o `.cpp` debe indicar en sus primeras líneas qué pines físicos se usaron para probar el módulo.
3. **Dependencias:** Si requiere una librería externa de Arduino/C++, incluye el enlace de descarga en los comentarios del código.
4. **No subas basura compilada:** Nuestro repositorio usa un archivo `.gitignore`. Solo sube el código fuente, no los archivos ejecutables temporales.

*Ad Astra!* ✨
