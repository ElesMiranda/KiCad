# ![KiCad](https://www.bing.com/images/search?view=detailV2&ccid=8ILZ%2fYK1&id=ACDD905002C9E5C050C2AB80D346DA6C3973F648&thid=OIP.8ILZ_YK1_tTLgrN8NUcsogHaDO&mediaurl=https%3a%2f%2fimage.pngaaa.com%2f670%2f3150670-middle.png&cdnurl=https%3a%2f%2fth.bing.com%2fth%2fid%2fR.f082d9fd82b5fed4cb82b37c35472ca2%3frik%3dSPZzOWzaRtOAqw%26pid%3dImgRaw%26r%3d0&exph=392&expw=900&q=kicad+logo&FORM=IRPRST&ck=3331EBC53B7FEAB6BC55D71E66B30AA0&selectedIndex=0&itb=0) 
# Diseño Electrónico en KiCad - SAFI

Bienvenido al repositorio oficial de recursos y diseño electrónico del **Capítulo Estudiantil SAFI**. 

Este espacio está dedicado a estandarizar, almacenar y documentar nuestros flujos de trabajo utilizando **KiCad EDA**. Nuestro objetivo principal es facilitar la colaboración entre todos los miembros del equipo, mantener una biblioteca unificada de componentes y optimizar nuestro proceso de fabricación interna de placas de circuito impreso (PCBs).

---

## Propósito del Repositorio

Para asegurar la calidad y compatibilidad en todos los proyectos de ingeniería del capítulo, este repositorio centraliza:
- **Bibliotecas Propias:** Símbolos esquemáticos y huellas (footprints) validados para los componentes que utilizamos frecuentemente.
- **Reglas de Diseño (DRC):** Configuraciones estandarizadas para garantizar que cualquier miembro diseñe placas que nuestra máquina CNC pueda fresar sin problemas.
- **Plantillas Base:** Archivos de KiCad pre-configurados para acelerar el desarrollo de nuevos circuitos.

## Flujo de Manufactura del Capítulo

Fomentamos una cultura de "Hazlo tú mismo" (DIY). Nuestro flujo de trabajo oficial para llevar los diseños de la pantalla a la placa de baquelita es:

1. **[KiCad](https://www.kicad.org/):** Creación del diagrama esquemático, ruteo de la PCB y exportación de archivos Gerber.
2. **FlatCAM:** Procesamiento de los Gerbers para generar las trayectorias de la herramienta (G-code) aislando las pistas.
3. **Candle (Router CNC):** Control de la máquina CNC para el fresado de pistas, perforación de agujeros (drill) y corte del contorno de la placa.

## 📁 Estructura del Repositorio

- 📂 `/Bibliotecas_Capitulo` - Archivos `.kicad_sym` (símbolos), `.kicad_mod` (huellas) y modelos 3D (`.step`).
- 📂 `/Plantillas_KiCad` - Proyectos base con los grosores de pista y separaciones correctas para nuestro router CNC.
- 📂 `/Guias_y_Tutoriales` - Documentación paso a paso para los nuevos miembros.

## Cómo Colaborar (Para Miembros)

Si eres parte del equipo de electrónica y vas a contribuir a este repositorio:
1. Sincroniza siempre tu carpeta local antes de abrir KiCad abriendo tu terminal y ejecutando: `git pull origin main`.
2. Si diseñas un símbolo o footprint nuevo, asegúrate de guardarlo en la carpeta `/Bibliotecas_Capitulo` para que el resto del equipo pueda aprovecharlo.
3. Guarda tus avances constantemente y haz commits descriptivos (ej. `git commit -m "Agregada guía de grosores de pista para FlatCAM"`).

---
*Repositorio mantenido por el área de Electrónica del Capítulo. ¡El limite son las estrellas!* 