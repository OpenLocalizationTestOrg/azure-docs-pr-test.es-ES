---
title: "especificaciones técnicas de aaaStorSimple | Documentos de Microsoft"
description: "Describe las especificaciones técnicas de hello e información de compatibilidad de estándares de regulación de componentes de hardware de StorSimple de Hola."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 98fa3307e2a929551c74e8b3179bb0fb61c0ab53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="technical-specifications-and-compliance-for-hello-storsimple-device"></a>Especificaciones técnicas y cumplimiento de normas para el dispositivo StorSimple Hola

## <a name="overview"></a>Información general

componentes de hardware de Hello de dispositivo de Microsoft Azure StorSimple cumplen las especificaciones técnicas de toohello y estándares de regulación que se describen en este artículo. especificaciones técnicas de Hola describen los alojamientos y capacidad de almacenamiento de información de módulos de alimentación y refrigeración (PCM), las unidades de disco, Hola. información de compatibilidad de Hola trata aspectos tales como las normas internacionales, la seguridad y las emisiones y cableado.

## <a name="power-and-cooling-module-specifications"></a>Especificaciones del módulo de alimentación y refrigeración

dispositivo de StorSimple de Hello tiene dos 100-240 V módulos ventilador doble, conformes a SBB alimentación y refrigeración (PCM). Esto proporciona una configuración de alimentación redundante. Si se produce un error en un PCM, dispositivo Hola continúa toooperate con normalidad en hello otro PCM hasta que hello no pudo módulo se reemplaza.

Hola alojamiento de EBOD usa un PCM de 580 W y alojamiento principal usa un PCM de 764 W. Hello las tablas siguientes se especificaciones técnicas de lista Hola asociadas Hola PCM.

| Especificación | PCM de 580 W (EBOD) | PCM de 764 W (principal) |
| --- | --- | --- |
| Potencia de salida máxima |580 W |764 |
| Frecuencia |50/60 Hz |50/60 Hz |
| Selección del intervalo de voltaje |Intervalo automático: 90-264 V CA, 47/63 Hz |Intervalo automático: 90-264 V CA, 47/63 Hz |
| Corriente de entrada máxima |20 A |20 A |
| Corrección del factor de potencia |>95% del voltaje de entrada nominal  |>95% del voltaje de entrada nominal  |
| Armónicos |Cumple la norma EN 61000-3-2 |Cumple la norma EN 61000-3-2 |
| Salida |Voltaje en espera de 5 V a 2,0 A |Voltaje en espera de 5 V a 2,7 A |
| +5 V a 42 A |+5 V a 40 A | |
| +12 V a 38 A |+12 V a 38 A | |
| Conectable en funcionamiento |Sí |Sí |
| Conmutadores y LED |Conmutador de encendido y apagado de CA y cuatro LED indicadores de estado |Conmutador de encendido y apagado de CA y seis LED indicadores de estado |
| Refrigeración del revestimiento |Ventiladores axiales de refrigeración con control de velocidad del ventilador variable |Ventiladores axiales de refrigeración con control de velocidad del ventilador variable |

## <a name="power-consumption-statistics"></a>Estadísticas de consumo de energía

Hello en la tabla siguiente enumera datos de consumo de energía típico Hola (los valores reales pueden variar de hello publicado) de hello varios modelos de dispositivo de StorSimple.

| Condiciones | 240 V CA | 240 V CA | 240 V CA | 110 V CA | 110 V CA | 110 V CA |
| --- | --- | --- | --- | --- | --- | --- |
|  Ventiladores lentos, unidades inactivas |1,45 A |0,31 kW |1057,76 BTU/h |3,19 A |0,34 kW |1160,13 BTU/h |
|  Ventiladores lentos, unidades accediendo |1,54 A |0,33 kW |1126,01 BTU/h |3,27 A |0,36 kW |1228,37 BTU/h |
|  Ventiladores rápidos, unidades inactivas, dos fuentes de alimentación activas |2,14 A |0,49 kW |1671,95 BTU/h |4,99 A |0,54 kW |1842,56 BTU/h |
|  Ventiladores rápidos, unidades inactivas, una fuente de alimentación activa y una inactiva |2,05 A |0,48 kW |1637,83 BTU/h |4,58 A |0,50 kW |1706,07 BTU/h |
|  Ventiladores rápidos, unidades accediendo, dos fuentes de alimentación activas |2,26 A |0,51 kW |1740,19 BTU/h |4,95 A |0,54 kW |1842,56 BTU/h |
|  Ventiladores rápidos, unidades accediendo, una fuente de alimentación activa y una inactiva |2,14 A |0,49 kW |1671,95 BTU/h |4,81 A |0,53 kW |1808,44 BTU/h |

## <a name="disk-drive-specifications"></a>Especificaciones de la unidad de disco

El dispositivo StorSimple admite hasta unidades de disco de too12 formato de 3,5 pulgadas factor Serial Attached SCSI (SAS). unidades reales de Hello pueden ser una combinación de unidades de estado sólido (SSD) o unidades de disco duro (HDD), dependiendo de la configuración del producto Hola. las ranuras de unidad de disco 12 Hola se encuentran en una configuración de 3 por 4 delante de alojamiento de Hola. Hola alojamiento de EBOD permite almacenamiento adicional para otro 12 unidades de disco. Estas son siempre unidades de disco duro.

## <a name="storage-specifications"></a>Especificaciones de almacenamiento

dispositivos de StorSimple de Hello tengan una combinación de unidades de disco duro y unidades de estado sólido para ambos hello 8100 y 8600. capacidad utilizable total de Hola para hello 8100 y 8600 son aproximadamente 15 TB y 38 TB respectivamente. Hello en la tabla siguiente documenta los detalles de Hola de SSD y HDD, capacidad de nube en el contexto de Hola de hello capacidad de la solución de StorSimple.

| Modelo de dispositivo/capacidad | 8100 | 8600 |
| --- | --- | --- |
| Número de unidades de disco duro (HDD) |8 |19 |
| Número de unidades de estado sólido (SSD) |4 |5 |
| Capacidad de un solo HDD |4 TB |4 TB |
| Capacidad de un solo SSD |400 GB |800 GB |
| Capacidad de reserva |4 TB |4 TB |
| Capacidad de HDD utilizable |14 TB |36 TB |
| Capacidad de SSD utilizable |800 GB |2 TB |
| Capacidad total utilizable* |~ 15 TB |~ 38 TB |
| Capacidad máxima de la solución (incluida la nube) |200 TB |500 TB |

<sup>* </sup>- *capacidad total utilizable de Hello incluye capacidad Hola disponible para los datos y metadatos, búferes.*

## <a name="enclosure-dimensions-and-weight-specifications"></a>Especificaciones de dimensiones y peso del revestimiento

Hola después de la lista de tablas Hola especificaciones del alojamiento para dimensiones y peso.

### <a name="enclosure-dimensions"></a>Dimensiones del revestimiento

Hello tabla siguiente enumeran las dimensiones de hello del alojamiento de hello en milímetros y pulgadas.

| Revestimiento | Milímetros | Pulgadas |
| --- | --- | --- |
| Alto |87,9 |3,46 |
| Ancho en brida de montaje |483 |19,02 |
| Ancho en el cuerpo del revestimiento |443 |17,44 |
| Profundidad de tooextremity de brida de montaje frontal del cuerpo del alojamiento |577 |22,72 |
| Profundidad de las operaciones de extremo lejano toofurthest del alojamiento del panel |630,5 |24,82 |
| Profundidad de extremo lejano de toofurthest bridas del alojamiento de montaje |603 |23,74 |

### <a name="enclosure-weight"></a>Peso del revestimiento

Según la configuración de hello, un alojamiento principal completamente cargado puede pesar entre 21 kg too33 y requiere dos toohandle de las personas.

| Revestimiento | Peso |
| --- | --- |
| Peso máximo (depende de la configuración de hello) |30 kg - 33 kg |
| Vacío (sin unidades instaladas) |21 kg - 23 kg |

## <a name="enclosure-environment-specifications"></a>Especificaciones medioambientales del revestimiento

Esta sección muestra el entorno de alojamiento de hello especificaciones toohello relacionados. temperatura de Hello, humedad, altitud, choque, vibración, orientación, seguridad y compatibilidad electromagnética (CEM) se incluyen en esta categoría.

### <a name="temperature-and-humidity"></a>Temperatura y humedad

| Revestimiento | Intervalo de temperatura ambiente | Humedad relativa del ambiente | Temperatura máxima de termómetro húmedo |
| --- | --- | --- | --- |
| Operativo |5 °C - 35 °C (41 °F - 95 °F) |20% - 80% sin condensación |28 °C (82 °F) |
| No operativo |-40 °C - 70 °C (40 °F - 158 °F) |5% - 100% sin condensación |29 °C (84 °F) |

### <a name="airflow-altitude-shock-vibration-orientation-safety-and-emc"></a>Flujo de aire, altitud, golpes, vibraciones, orientación, seguridad y CEM

| Revestimiento | Especificaciones operativas |
| --- | --- |
| Flujo de aire |Flujo de aire del sistema es toorear frontal. El sistema debe funcionar con una instalación de baja presión y escape trasero. La contrapresión creada por puertas del revestimiento y los obstáculos no debe superar los 5 pascales (medidor de agua de 0,5 mm). |
| Altitud (operativo) |-30 metros too3045 metros (de-100 pies too10, 000 pies) con la temperatura de funcionamiento máxima reducida en 5 ° C por encima de los 7000 pies. |
| Altitud (no operativo) |too12 305 metros, 192 metros (too40 – 1.000 pies, 000 pies) |
| Golpes (operativo) |5 g 10 ms ½ seno |
| Golpes (no operativo) |30 g 10 ms ½ seno |
| Vibraciones (operativo) |0,21 g RMS 5-500 Hz aleatorio |
| Vibraciones (no operativo) |1,04 g RMS 2-200 Hz aleatorio |
| Vibraciones (reubicación) |3 g 2-200 Hz seno |
| Orientación y montaje |Montaje en bastidor de 19 pulgadas (2 unidades EIA) |
| Guías del bastidor |toofit soportes de profundidad mínima de 700 mm (31,50 pulgadas) conformes a IEC 297 |
| Seguridad y homologaciones |CE y UL EN 61000-3, CEI 61000-3, UL 61000-3 |
| CEM |EN 55022 (CISPR - A), FCC A |

## <a name="international-standards-compliance"></a>Cumplimiento de normas internacionales

El dispositivo de StorSimple de Microsoft Azure cumple con hello siguiendo estándares internacionales:  

* CE - EN 60950-1
* TooIEC de informe CB 60950-1
* UL y cUL tooUL 60950-1

## <a name="safety-compliance"></a>Cumplimiento de seguridad

El dispositivo de StorSimple de Microsoft Azure cumple Hola siguientes calificaciones de seguridad:

* Homologación del tipo de producto de sistema: UL, cUL, CE
* Cumplimiento de seguridad: UL 60950, CEI 60950, EN 60950

## <a name="emc-compliance"></a>Cumplimiento de normas de CEM

El dispositivo de StorSimple de Microsoft Azure cumple Hola siguiendo las clasificaciones de EMC.

### <a name="emissions"></a>Emisiones

dispositivo de Hello es compatible con EMC para los niveles de emisiones radiadas y conducidas.

* Niveles límite de emisiones conducidas: CFR 47 parte 15B clase A, EN 55022 clase A, CISPR clase A
* Niveles límite de emisiones radiadas: CFR 47 parte 15B clase A, EN 55022 clase A, CISPR clase A

### <a name="harmonics-and-flicker"></a>Armónicos y parpadeo

dispositivo de Hello cumple con EN61000-3-2/3.

### <a name="immunity-limit-levels"></a>Niveles límite de inmunidad

dispositivo de Hello cumple con EN55024.

## <a name="ac-power-cord-compliance"></a>Cumplimiento de cable de alimentación de CA

enchufe de Hola y Hola completa cable de alimentación debe cumplir los estándares de hello apropiados para el país de hello en qué Hola se está utilizando el dispositivo, y deben tener las aprobaciones de seguridad que son aceptables en ese país. Hola las tablas siguientes se estándares de lista de Estados Unidos de Hola y Europa.

### <a name="ac-power-cords---usa-must-be-nrtl-listed"></a>Cables de alimentación de CA - Estados Unidos (debe estar contemplado por NRTL)

| Componente | Especificación |
| --- | --- |
| Tipo de cable |SV o SVT, AWG 18 como mínimo, 3 conductores, longitud máxima de 2,0 metros |
| Enchufe |Enchufe de toma de tierra NEMA 5-15P para 120 V, 10 A; o CEI 320 C14, 250 V, 10 A |
| Toma de corriente |CEI 320 C-13, 250 V, 10 A |

### <a name="ac-power-cords---europe"></a>Cables de alimentación de CA - Europa

| Componente | Especificación |
| --- | --- |
| Tipo de cable |Armonizado, H05-VVF-3G1.0 |
| Toma de corriente |CEI 320 C-13, 250 V, 10 A |

## <a name="supported-network-cables"></a>Cables de red admitidos

Para las interfaces de red de hello 10 GbE, DATA 2 y 3 de datos, consulte toohello [lista de cables de red admitidos y los módulos](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).

## <a name="next-steps"></a>Pasos siguientes

Ya estás listo toodeploy un dispositivo StorSimple en su centro de datos. Para más información, vea [Implementar un dispositivo local](storsimple-8000-deployment-walkthrough-u2.md).

