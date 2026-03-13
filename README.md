# KiCad 
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAV8AAACPCAMAAABqIigoAAABF1BMVEX///8bK2MxTLAdLWj/dwDP0dsAEl0ZKmYyTrQhM3cXKGYtO3AuSKctR6QAG1xATHq/ws8AFl4jN34eP6yWmq+6weGxuNyqsdk/V7UqN2oqSLCLkKgAAFQQJGAWO6sJIF7c4PB6gJsAF1oAC1bs7fEABlW1uMb/bQAlRK3c3uX09fiqrr8jMmhudZQxPm/k5/OTntF5h8efpLdRWoFzephaY4dMYbj/4Mz/gycAAFj/ewCfqdYHNanX2eFYa7xneMGFksv/9/H/6Nv/t47/n2P/2MH/qnb/yKjlnnvOYRwtIlcAJ2zobx1VPVndax9KOFwAM4K+YkCPXoCiYXLFaVFIUKSrY2nVbUJlVZa7Z1mCWobL0OgAKKZh9JJzAAAOsElEQVR4nO2deX/bxhGGSdokHFcBiYqSLQIQjIMMCR6ySVG2bNNXkp5p2tSOm9T9/p+jPMRz31nsLrGCJeH9J79YxMGHi9nZmdlBoZArV65cuXLlyvV16/2H58/fZ30Tt1Xvv3/x3Uz3f/gx61u5jfrTlOyVvnvxPOu7uW36cH9Fd074+6xv6Hbp+RbdGeAfsr6l26QPu3jzEZyqXjB4p4BzG5yW/swO36leZH1bt0aI7nQA525aOmImtyvdqSkuqmnTXzDe+y8Xf46y/urXofplxdKky78SfO//bX5Nx876y+tX7fKeNv39J2r8/sOYf+CylfXX166xlyHfh6Osv752VR9q5PszxfefC77GH7L++to15/vNH7XoX79Q9nd2wbvDt3jwQIsa/ybw/tx+8OCgeHf4flvSowOC78fG9G85373V/oT5HpRyvmnowa8Q7+dGzjcdNT6+ZPH+NMOb801FyEL8evP5lvs+0jm7XtLMt9T+fXcEL/DebL6FUeABhXXmg7r5ltpbTtrLX0oLvDecb+QUgcwM+JYaB59XeP/zW3v5zzebb6HvfS18p4Qbv338/dOnz//9tt1Y/aMs32hSa3WnapU7cYqcVFWz5PhePKZ1AZhxPg6OaCy0+U8SfKOWX710QiuYyao0Hbc/LGcMOQql+LZfcc513C7tqv2Ue/VXDeaIXYny7dQHoeW521/ENUNz3MoScSxpH15/IU91dgoe+We8i785TMQryLdbdUwDTSVTxlbYr4mg0CN0Vzz72yDP9BYMxvY7+spnJXa8q/GtVwIXfI014vDeMKtBjO6Hx/fwEXEiNHxLh8fkhc/aycZBiG/XDHhw5zICs54N4R4YwNzxe0Gc6BF62E/J3KQg3kS+kwGaoYECcyjLJg2dSPItnRLjAJoH0vxGDTG8SXxth2sZdgh3r38Mn4Ab4fN9gk8Eh+8ZddnHgnj5fKNqsmnYJnztU50030PsQUSvWTaHpHf2RmRqS+Rb5k9rSM51F1PI8z2C53nCTm+Nx9RFnwk4Zsl8u3Bxz1Xz2jP9afH9wvKlLEnhFXI1pPnW5fF6fVVMypLni12uI2ZInlJrvS/AlMjzteXxFs0bML+J8m2/Ja4IHWVpvnZTHq+TwTpOF99GibqisOvA4ztUGb3ne3BSlS6+pGsm7jpw+NYU8Bq9vUApShPf13gWLBSeirsONF8Y9dsg6Xqey7huzmQ/UmrSw/fwHXG5IynjS/Ed0H6vYYbmYNw/71eNirUZHAyyqXLVwrf9hrga8JIV+Prkqs1t

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