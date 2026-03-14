<h1 align="center">SISTEMAS DE AVIÓNICA Y COMUNICACIONES</h1>
<h3 align="center">Proyecto LANIAKEA | Capítulo SAFI</h3>

<p align="center">
  <img src="[PON_AQUI_TU_FOTO_DE_PORTADA.jpg]" alt="Banner de Firmware SAFI" width="800">
</p>

> **Misión Principal:** Centralizar los códigos fuente, librerías y diagramas de conexión necesarios para la telemetría, el control de actuadores y el registro de datos de nuestro cohete experimental rumbo al **Latin American Space Challenge (LASC)**.
> 
> **Apogeo Objetivo:** `3,000 metros`

---

## Arquitectura de Microcontroladores

Nuestra computadora de vuelo modular distribuye el procesamiento para evitar cuellos de botella durante la fase de ascenso y recuperación. 

Selecciona el núcleo para acceder a sus códigos de inicialización:

### ![ESP32](https://img.shields.io/badge/Computadora_Central-ESP32-black?style=for-the-badge&logo=espressif)
**[Directorio de Código ESP32]([PON_AQUI_EL_ENLACE_A_LA_CARPETA_DEL_ESP32])** | [Documentación Oficial](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/)
<br>Encargada del procesamiento pesado, la aplicación de filtros matemáticos y el empaquetado del tren de telemetría.
<p align="center">
  <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/ESP32.jpg" alt="ESP32" width="200">
</p>

### ![Arduino Nano](https://img.shields.io/badge/Nodos_Satélite-Arduino_Nano-00979D?style=for-the-badge&logo=arduino)
**[Directorio de Código Nano]([PON_AQUI_EL_ENLACE_A_LA_CARPETA_DEL_NANO])** | [Documentación Oficial](https://docs.arduino.cc/hardware/nano)
<br>Sistema de redundancia y manejo directo de actuadores (conmutación de transistores, ignición, sistemas de despliegue).
<p align="center">
  <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/ARDUINONANO.jpg" alt="Arduino Nano" width="200">
</p>

### ![Raspberry Pi Pico](https://img.shields.io/badge/Adquisición_de_Datos-RPi_Pico-C51A4A?style=for-the-badge&logo=raspberrypi)
**[Directorio de Código Pico]([PON_AQUI_EL_ENLACE_A_LA_CARPETA_DE_LA_PICO])** | [Documentación Oficial](https://www.raspberrypi.com/documentation/microcontrollers/raspberry-pi-pico.html)
<br>Manejo de entradas/salidas de alta velocidad y temporización de precisión.
<p align="center">
  <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/raspberry.jpg" alt="Raspberry Pi Pico" width="200">
</p>

---

## Protocolos de Comunicación y Periféricos

Para garantizar la lectura de sensores sin bloqueos en el hilo principal de ejecución, la arquitectura LANIAKEA se divide en tres buses principales.

> **ADVERTENCIA DE INTEGRACIÓN:** Verifique estrictamente los niveles lógicos de voltaje (`3.3V` vs `5V`) antes de interconectar módulos. Ignorar esto resultará en daño permanente al silicio.

### 1. Bus I2C (Inter-Integrated Circuit)
Protocolo síncrono maestro-esclavo implementado para el arreglo de sensores en placa. Utiliza dos líneas de datos: `SDA` y `SCL`. Requiere la implementación física de resistencias Pull-Up.

<p align="center">
  <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/I2C.jpg" alt="Diagrama I2C" width="400">
</p>

**Módulos Integrados:**
* **IMU MPU6050:** Orientación espacial, aceleración y giroscopio de 6 ejes.
  <p align="center">
    <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/MPU6050.jpg" alt="MPU6050" width="100">
  </p>
* **Barómetro MS5611:** Altímetro de alta precisión para la detección del apogeo y activación de eventos de recuperación.
  <p align="center">
    <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/MS5611.jpg" alt="MS5611" width="100">
  </p>

**[> Consultar librerías e implementaciones I2C]([PON_AQUI_EL_ENLACE_A_LA_CARPETA_I2C])**

---

### 2. Bus UART (Serial Asíncrono)
Comunicación asíncrona punto a punto. La topología de conexión exige el cruce de las líneas lógicas: el pin `TX` (Transmisión) del periférico debe ir al `RX` (Recepción) del microcontrolador, y viceversa.

<p align="center">
  <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/UART.png" alt="Diagrama UART" width="400">
</p>

**Módulos Integrados:**
* **Radio XBee Pro S2C:** Enlace de telemetría de largo alcance hacia la Estación Terrena.
  <p align="center">
    <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/Radio%20XBee%20Pro%20S2C.jpg" alt="Radio XBee Pro S2C" width="100">
  </p>
* **GPS RYS352A:** Adquisición de coordenadas geoespaciales para la fase de descenso y recuperación.
  <p align="center">
    <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/GPS%20RYS352A.webp" alt="GPS RYS352A" width="100">
  </p>

**[> Consultar algoritmos de telemetría UART]([PON_AQUI_EL_ENLACE_A_LA_CARPETA_UART])**

---

### 3. Bus SPI (Serial Peripheral Interface)
Protocolo síncrono de alta velocidad (Full-Duplex), dedicado exclusivamente a la transferencia masiva de bloques de datos. Emplea las líneas `MOSI`, `MISO`, `SCK` y `CS`.

<p align="center">
  <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/SPI.png" alt="Diagrama SPI" width="400">
</p>

**Módulos Integrados:**
* **Módulo Adaptador MicroSD:** Datalogger primario ("Caja Negra"). Registra las matrices de variables físicas a alta frecuencia durante todo el perfil de vuelo.
  <p align="center">
    <img src="https://raw.githubusercontent.com/ElesMiranda/KiCad/main/Imag/SD.jpg" alt="Módulo MicroSD" width="100">
  </p>

**[> Consultar rutinas de escritura del Datalogger SPI]([PON_AQUI_EL_ENLACE_A_LA_CARPETA_SPI])**

---

## Directivas de Contribución para el Equipo

Para mantener la integridad del repositorio, todo miembro del Capítulo debe adherirse al siguiente protocolo antes de realizar un `push` a la rama principal:

1. **Sincronización Previa:** Ejecutar `git pull origin main` en el entorno local antes de iniciar cualquier modificación.
2. **Mapeo de Hardware:** Todo archivo fuente (`.ino`, `.cpp`, `.h`) debe incluir en su cabecera un bloque de comentarios detallando los pines físicos exactos utilizados durante las pruebas de validación.
3. **Gestión de Dependencias:** Si un periférico requiere bibliotecas externas, el enlace directo al repositorio oficial debe adjuntarse en la documentación del código.
4. **Control de Compilados:** Este repositorio opera bajo un escudo `.gitignore`. Queda estrictamente prohibido forzar la subida de archivos ejecutables, binarios o archivos temporales de compilación.

<br>
<p align="center">
  <i>Ad Astra!</i>
</p>
