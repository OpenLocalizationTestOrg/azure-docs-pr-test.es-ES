---
title: supervisar los indicadores de aaaStorSimple | Documentos de Microsoft
description: Describe Hola diodos emisores de luz (LED) y alarmas audibles usa toomonitor Hola estado de dispositivo de StorSimple Hola.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 59dee7b9-ca6d-4fd9-96e6-a0071e8d248e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: e690b8f4727272f5fbb8886a594a046f794a1380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-monitoring-indicators-toomanage-your-device"></a>Usar el dispositivo de StorSimple toomanage de indicadores de supervisión
## <a name="overview"></a>Información general
El dispositivo de StorSimple incluye diodos emisores (LED) y alarmas que se puede usar toomonitor Hola módulos y estado general del dispositivo de StorSimple Hola. Hola indicadores de supervisión puede encontrarse en componentes de hardware de Hola de alojamiento principal del dispositivo de Hola y el alojamiento EBOD Hola. Hola indicadores de supervisión puede ser LED o alarmas sonoras.

Hay tres LED Estados que se usan tooindicate Hola estado de un módulo: verde, parpadeo toored verde-ámbar, o rojo-ámbar.  

* Los LED verdes señalan un estado operativo correcto.  
* Parpadea en verde toored-ámbar LED representan la presencia de Hola de condiciones no críticas que pueden requerir la intervención del usuario.  
* Los LED rojo-ámbar indican que hay un error crítico en el módulo de Hola.  

Hola que queda de este artículo describe Hola varios indicadores LED de supervisión, sus ubicaciones en el dispositivo de StorSimple de hello, estado del dispositivo Hola según Hola Estados de LED y cualquier alarmas sonoras.

## <a name="front-panel-indicator-leds"></a>Indicadores LED en el panel frontal
panel frontal de Hello, también conocido como hello *panel de operaciones* o *del panel de operaciones*, muestra hello estado global de todos los módulos de hello sistema Hola. panel frontal de Hello es idéntico en hello alojamiento de EBOD y hello StorSimple principal y se muestra a continuación.  

   ![Panel frontal del dispositivo][1]

panel frontal de Hello contiene Hola siguientes indicadores:  

1. Botón Silencio
2. Indicador LED de alimentación (verde/rojo-ámbar)
3. Indicador LED de error de módulo (encendido rojo-ámbar/apagado)
4. Indicador LED de error lógico (encendido rojo-ámbar/apagado
5. Pantalla de identificación de la unidad  

Hello diferencia principal entre el panel frontal de hello LED para el dispositivo de Hola y los de hello alojamiento de EBOD es hello **número de identificación de unidad de sistema** se muestra en pantalla de hello LED. unidad de Hello predeterminada es el identificador que se muestra en el dispositivo de hello **00**, mientras que el identificador de unidad predeterminado hello muestra de Hola alojamiento de EBOD es **01**. Esto le permite diferenciar los tooquickly entre dispositivos de Hola y alojamiento de EBOD Hola al Hola dispositivo está activado. Si el dispositivo está desactivado, use información de hello proporcionada en [activar un nuevo dispositivo](storsimple-turn-device-on-or-off.md#turn-on-a-new-device) toodifferentiate dispositivo Hola Hola alojamiento de EBOD.  

## <a name="front-panel-led-status"></a>Estado de los LED del panel frontal
Usar hello después de estado de hello tooidentify de tabla indicado por hello LED en el panel frontal de hello de dispositivo de Hola o alojamiento de EBOD Hola.  

| Alimentación del sistema | Error de módulo | Error lógico | Alarma | Estado |
| --- | --- | --- | --- | --- |
| Rojo-ámbar |Apagado |Apagado |N/D |La pérdida de corriente Alterna, funcionando con alimentación de reserva o corriente Alterna en o se quitaron los módulos de controlador de Hola. |
| Verde |ACTIVAR |ACTIVAR |N/D |Alimentación del panel de operaciones en estado de prueba (5 s) |
| Verde |Apagado |Apagado |N/D |Encendido, todas las funciones correctas |
| Verde |ACTIVAR |N/D |LED de error del PCM, LED de error del ventilador |Cualquier error del PCM, error del ventilador, exceso o defecto de temperatura |
| Verde |ACTIVAR |N/D |LED del módulo de E/S |Cualquier error del módulo de controlador |
| Verde |ACTIVAR |N/D |N/D |Error lógico del revestimiento |
| Verde |Intermitente |N/D |LED de estado de módulo en módulo del controlador. LED de error del PCM, LED de error del ventilador |Tipo de módulo de controlador desconocido instalado, error de bus I2C, error de configuración de datos de producto vitales del módulo de controlador |

## <a name="power-cooling-module-pcm-indicator-leds"></a>Indicadores LED del módulo de refrigeración de alimentación (PCM)
Alimentación y refrigeración (PCM) LED indicadores del módulo pueden encontrarse en hello parte posterior del alojamiento principal de Hola o alojamiento de EBOD en cada módulo PCM. Este tema se describe cómo hello toouse después de estado del LED toomonitor Hola del dispositivo StorSimple.  

* LED del PCM para el alojamiento principal Hola
* LED del PCM para hello alojamiento de EBOD

## <a name="pcm-leds-for-hello-primary-enclosure"></a>LED del PCM para el alojamiento principal Hola
dispositivo de StorSimple de Hello tiene un módulo PCM de 764 w con una batería adicional. Hello mostramos aquí panel de LED de hello de dispositivo de Hola.  

   ![LED del PCM en el alojamiento principal Hola][2]

Leyenda de LED:

1. Error de corriente alterna
2. Error del ventilador
3. Error de la batería
4. PCM correcto
5. Error de corriente continua
6. Batería correcta  

panel de LED de estado de Hola de hello que PCM se indica en Hola. panel de LED del PCM de dispositivo de Hello tiene seis LED. Cuatro de estos LED Mostrar estado de Hola de Hola de alimentación y ventiladores de Hola. Hola restantes dos LED indica Estados de Hola de módulo de batería de reserva de Hola Hola PCM. Puede usar Hola siguiendo el estado de las tablas toodetermine Hola de hello PCM.  

### <a name="pcm-indicator-leds-for-power-supply-and-fan"></a>Indicadores LED del PCM relativos a la fuente de alimentación y el ventilador
| Estado | PCM correcto (verde) | Error de corriente alterna (ámbar) | Error de ventilador (ámbar) | Error de corriente continua (ámbar) |
| --- | --- | --- | --- | --- |
| No hay corriente alterna (tooenclosure) |Apagado |Apagado |Apagado |Apagado |
| No hay corriente alterna (solo en este PCM) |Apagado |ACTIVAR |Apagado |ACTIVAR |
| Hay corriente alterna y el PCM está encendido: todo correcto |ACTIVAR |Apagado |Apagado |Apagado |
| Error de PCM (error de ventilador) |Apagado |Apagado |ACTIVAR |N/D |
| Error de PCM (exceso de amperaje, de voltaje o de corriente) |Apagado |ACTIVAR |ACTIVAR |ACTIVAR |
| PCM (ventilador fuera de tolerancia) |ACTIVAR |Apagado |Apagado |ACTIVAR |
| Modo de espera |Intermitente |Apagado |Apagado |Apagado |
| Descarga del firmware del PCM |Apagado |Intermitente |Intermitente |Intermitente |

### <a name="pcm-indicator-leds-for-hello-backup-battery"></a>LED indicadores del PCM para la batería de reserva Hola
| Estado | Batería correcta (verde) | Error de batería (ámbar) |
| --- | --- | --- |
| No hay batería |Apagado |Apagado |
| Hay batería y está cargada |ACTIVAR |Apagado |
| Batería en carga o en descarga de mantenimiento |Intermitente |Apagado |
| Error flexible de la batería (recuperable) |Apagado |Intermitente |
| Error severo de la batería (recuperable) |Apagado |ACTIVAR |
| Batería desarmada |Intermitente |Apagado |

## <a name="pcm-leds-for-hello-ebod-enclosure"></a>LED del PCM para hello alojamiento de EBOD
Hola alojamiento de EBOD tiene un PCM de 580 w y sin batería adicional. panel del PCM Hola para hello alojamiento de EBOD tiene indicadores LED solo para las fuentes de alimentación de Hola y el ventilador de Hola. Hello en la ilustración siguiente se muestra estos LED.

   ![LED del PCM en hello alojamiento de EBOD][3] 

Puede usar Hola después de estado de tabla toodetermine Hola de hello PCM.  

| Estado | PCM correcto (verde) | Error de corriente alterna (ámbar) | Error de ventilador (ámbar) | Error de corriente continua (ámbar) |
| --- | --- | --- | --- | --- |
| No hay corriente alterna (tooenclosure) |Apagado |Apagado |Apagado |Apagado |
| No hay corriente alterna (solo en este PCM) |Apagado |ACTIVAR |Apagado |ACTIVAR |
| Hay corriente alterna y el PCM está encendido: todo correcto |ACTIVAR |Apagado |Apagado |Apagado |
| Error de PCM (error de ventilador) |Apagado |Apagado |ACTIVAR |X |
| Error de PCM (exceso de amperaje, de voltaje o de corriente) |Apagado |ACTIVAR |ACTIVAR |ACTIVAR |
| PCM (ventilador fuera de tolerancia) |ACTIVAR |Apagado |Apagado |ACTIVAR |
| Modo de espera |Intermitente |Apagado |Apagado |Apagado |
| Descarga del firmware del PCM |Apagado |Intermitente |Intermitente |Intermitente |

## <a name="controller-module-indicator-leds"></a>Indicadores LED del módulo del controlador
dispositivo de StorSimple de Hello contiene LED para el controlador principal de Hola y módulos de controlador EBOD Hola.   

### <a name="monitoring-leds-for-hello-primary-controller"></a>LED de supervisión para el controlador principal de Hola
Hello en la ilustración siguiente se le ayuda a identificar los LED de hello en el controlador principal de Hola. (Todos los componentes de hello son tooaid enumerado en la orientación).  

   ![LED de supervisión: controlador principal][4]

Usar hello después toodetermine de tabla si el módulo del controlador de hello funciona correctamente.  

### <a name="controller-indicator-leds"></a>Indicadores LED de controlador
| LED | Description |
| --- | --- |
| LED de identificación (azul) |Indica que se está identificando ese módulo Hola. Si hello LED azul parpadea en un controlador en ejecución, a continuación, hello es Hola active controlador y hello otro es Hola de controlador en espera. Para obtener más información, consulte [controlador activo de identificación hello en el dispositivo](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device). |
| LED de error (ámbar) |Indica un error en el controlador de Hola. |
| LED correcto (verde) |Verde fijo indica que el controlador de hello es correcto. La intermitencia en verde indica un error de configuración de VPD del controlador. |
| LED de actividad SAS (verde) |Un color verde fijo señala una conexión sin ninguna actividad actual. Verde parpadeante indica la conexión de hello tiene actividad en curso. |
| Indicadores LED de estado de Ethernet |El lado derecho indica la actividad de vínculo/red: (verde fijo) vínculo activo, (intermitencia en verde) actividad de red. El lado izquierdo indica la velocidad de la red: (amarillo) 1000 Mb/s, (verde) 100 Mb/s y (apagado) 10 Mb/s. Según el modelo de componente de hello, esta luz podría parpadear incluso si no está habilitada la interfaz de red de Hola. |
| LED POST |Indica el progreso de arranque de hello al controlador de hello está encendido. Si el dispositivo de StorSimple de hello no tooboot, este LED ayudará a Microsoft Support identificar Hola punto Hola proceso de arranque en que se produjo el error de Hola. |

> [!IMPORTANT]
> Si se enciende el LED de error de hello, hay un problema con el módulo de controlador de Hola que se puede resolver reiniciando controlador Hola. Póngase en contacto con Microsoft Support si reiniciar controlador hello no resuelve este problema.  
> 
> 

### <a name="monitoring-leds-for-hello-ebod-ebod-enclosure"></a>LED de supervisión para hello EBOD (alojamiento de EBOD)
Cada uno de Hola 6 Gb/controladores de EBOD SAS s tiene unos LED que indican su estado como se muestra en hello siguiente ilustración.  

  ![LED de supervisión: revestimiento de EBOD][5]

Usar hello después toodetermine de tabla si el módulo de controlador EBOD Hola funciona con normalidad.  

### <a name="ebod-controller-module-indicator-leds"></a>Indicadores LED del módulo de controlador de EBOD
| Estado | Módulo de E/S correcto (verde) | Error del módulo de E/S (ámbar) | Actividad de puerto del host (verde) |
| --- | --- | --- | --- |
| Módulos de controladores OK |ACTIVAR |Apagado |- |
| Error en módulo de controlador |Apagado |ACTIVAR |- |
| Sin conexión de puerto de host externo |- |- |Apagado |
| Conexión de puerto de host externo: sin actividad |- |- |ACTIVAR |
| Conexión de puerto de host externo: actividad |- |- |Intermitente |
| Error de metadatos del módulo de controlador |Intermitente |- |- |

## <a name="disk-drive-indicator-leds-for-hello-primary-enclosure-and-ebod-enclosure"></a>Indicadores LED de la unidad de disco para alojamiento principal de Hola y el alojamiento EBOD
dispositivo de StorSimple de Hello tiene unidades de disco en el alojamiento principal de Hola y el alojamiento de EBOD Hola. Cada una de ellas cuenta con varios indicadores LED de supervisión, como se describe en esta sección. 

Las unidades de disco de hello, estado de la unidad de Hola se indica mediante una de color verde LED y un LED rojo-ámbar montados en la parte delantera de Hola de cada módulo portador de unidades. Hello en la ilustración siguiente se muestra estos LED.

  ![LED de unidad de disco][6]

Usar hello después de estado de hello toodetermine de tabla de cada unidad de disco, lo que a su vez afecta al estado del LED del panel frontal de Hola.  

### <a name="disk-drive-indicator-leds-for-hello-ebod-enclosure"></a>LED indicadores de unidad de disco para hello alojamiento de EBOD
| Estado | LED de actividad correcta (verde) | LED de error (rojo-ámbar) | LED del panel de operaciones asociado |
| --- | --- | --- | --- |
| No hay unidades instaladas |Apagado |Apagado |None |
| Unidad instalada y operativa |Intermitencia con actividad |X |None |
| Conjunto de identidad de dispositivo de los servicios de SCSI Enclosure (SES) |ACTIVAR |Intermitente 1 segundo sí/1 segundo no |None |
| Conjunto de bits de error de dispositivo SES |ACTIVAR |ACTIVAR |Error lógico (rojo) |
| Error de circuito de control de alimentación |Apagado |ACTIVAR |Error del módulo (rojo) |

## <a name="audible-alarms"></a>Alarmas audibles
Un dispositivo de StorSimple contiene alarmas sonoras asociadas con alojamiento principal de Hola y el alojamiento de EBOD Hola. Una alarma audible se encuentra en el panel frontal (también conocido como panel de operaciones de hello) Hola de ambos alojamientos. alarma audible Hola indica cuando está presente una condición de error. Hola condiciones siguientes activará la alarma de hello:  

* Error o avería del ventilador
* Voltaje fuera del intervalo
* Condición de exceso o defecto de temperatura
* Saturación térmica
* Error del sistema
* Error lógico
* Error de la fuente de alimentación
* Eliminación de un módulo de refrigeración de alimentación (PCM)  

Hello tabla siguiente describen Hola distintos Estados de alarma.  

### <a name="alarm-states"></a>Estados de alarma
| Estado de alarma | Acción | Acción cuando el botón Silenciar está presionado |
| --- | --- | --- |
| S0 |Modo normal: silencioso |Pitido doble |
| S1 |Modo de error: 1 segundo activado/1 segundo desactivado |Transición tooS2 o S3 (vea las notas) |
| S2 |Modo de recordatorio: pitido intermitente |None |
| S3 |Modo en silencio: silencioso |None |
| S4 |Modo de error crítico: alarma continua |No disponible: silencio no activo |

> [!NOTE]
> * En estado de alarma S1, si no presiona Silenciar en dos minutos, Hola estado pasa automáticamente tooS2 o S3.  
> * Estados de alarma S1 tooS4 devolver tooS0 una vez borrada la condición de error de Hola.  
> * Se puede pasar a un estado de error crítico S4 desde cualquier otro estado.  


Puede silenciar la alarma audible Hola presionando el botón Silenciar hello en el panel de ops Hola. La desactivación automática se producirá después de dos minutos si no se opera manualmente interruptor de silencio de Hola. Cuando Hola alarma está silenciada, seguirá toosound con tooindicate pitidos intermitentes breves que aún existe un problema. alarma de Hello será silenciosa cuando se corrijan todos los problemas de Hola.

Hello tabla siguiente describen Hola diversas condiciones de alarma.

### <a name="alarm-conditions"></a>Condiciones de alarma
| Estado | Gravedad | Alarma | LED del panel de operaciones |
| --- | --- | --- | --- |
| Alerta de PCM: pérdida de corriente continua de un único PCM |Error: no hay pérdida de redundancia |S1 |Error de módulo |
| Alerta de PCM: pérdida de corriente continua de un único PCM |Error: pérdida de redundancia |S1 |Error de módulo |
| Error de ventilador del PCM |Error: pérdida de redundancia |S1 |Error de módulo |
| El módulo SBB detectó un error de PCM |Error |S1 |Error de módulo |
| PCM extraído |Error de configuración |None |Error de módulo |
| Error de configuración del revestimiento |Error: crítico |S1 |Error de módulo |
| Alerta de advertencia temperatura baja |Warning (Advertencia) |S1 |Error de módulo |
| Alerta de advertencia temperatura alta |Warning (Advertencia) |S1 |Error de módulo |
| Alarma de exceso de temperatura |Error: crítico |S1 |Error de módulo |
| Error de bus I2C |Error: pérdida de redundancia |S1 |Error de módulo |
| Error de comunicación del panel de operaciones (I2C) |Error: crítico |S1 |Error de módulo |
| Error de controlador |Error: crítico |S1 |Error de módulo |
| Error del módulo de la interfaz SBB |Error: crítico |S1 |Error de módulo |
| Error del módulo de la interfaz SBB: no quedan módulos en funcionamiento |Error: crítico |S4 |Error de módulo |
| Módulo de interfaz SBB extraído |Warning (Advertencia) |None |Error de módulo |
| Error de control de alimentación de la unidad |Advertencia: sin pérdida de alimentación de la unidad |S1 |Error de módulo |
| Error de control de alimentación de la unidad |Error: crítico; pérdida de alimentación de la unidad |S1 |Error de módulo |
| Unidad extraída |Warning (Advertencia) |None |Error de módulo |
| Alimentación insuficiente disponible |Warning (Advertencia) |None |Error de módulo |

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre los [componentes de hardware de StorSimple y su estado](storsimple-8000-monitor-hardware-status.md).

[1]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE01.png
[2]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE02.png
[3]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE03.png
[4]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE04.png
[5]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE05.png
[6]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE06.png


