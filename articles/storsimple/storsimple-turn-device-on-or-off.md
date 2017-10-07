---
title: aaaTurn el dispositivo de la serie 8000 de StorSimple o desactivar | Documentos de Microsoft
description: "Explica cómo activar un dispositivo que se cerró o se apagó tooturn en un nuevo dispositivo de StorSimple y desactivar un dispositivo en ejecución."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 8e9c6e6c-965c-4a81-81bd-e1c523a14c82
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 85434bde9377e330cd6ba4797fd5fd68bcee944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="turn-on-or-turn-off-your-storsimple-8000-series-device"></a>Activación o desactivación del dispositivo StorSimple serie 8000
## <a name="overview"></a>Información general
No se requiere apagar el dispositivo de Microsoft Azure StorSimple como parte del funcionamiento normal del sistema. Sin embargo, deberá tooturn en un dispositivo nuevo o un dispositivo que tuvo toobe apagar. Por lo general, se requiere apagar un dispositivo en casos en que se debe reemplazar algún hardware con error, mover físicamente una unidad o quitar un dispositivo del servicio. Este tutorial describe procedimiento Hola necesario para encender y apagar el dispositivo StorSimple en escenarios diferentes.

## <a name="turn-on-a-new-device"></a>Activar un dispositivo nuevo
Hello pasos para activar un dispositivo de StorSimple para hello la primera vez que dependen de si el dispositivo de hello es un 8100 o en un modelo de 8600. Hola 8100 tiene un único alojamiento principal, mientras que Hola 8600 es un dispositivo de doble alojamiento con un alojamiento principal y un alojamiento de EBOD. Hello pasos detallados para ambos modelos se explican en las secciones siguientes de Hola.

* [Dispositivo nuevo solo con gabinete principal](#new-device-with-primary-enclosure-only)
* [Dispositivo nuevo con gabinete EBOD](#new-device-with-ebod-enclosure)

### <a name="new-device-with-primary-enclosure-only"></a>Dispositivo nuevo solo con gabinete principal
modelo de Hello StorSimple 8100 es un dispositivo de alojamiento. El dispositivo incluye módulos de alimentación y de refrigeración (PCM) redundantes. Ambos PCM debe estar instalado y conectado disponibilidad alta de toodifferent power orígenes tooensure.

Realizar Hola siguiendo los pasos toocable el dispositivo para alimentación.

[!INCLUDE [storsimple-cable-8100-for-power](../../includes/storsimple-cable-8100-for-power.md)]

> [!NOTE]
> Para el programa de instalación de dispositivos completa y cableado instrucciones, vaya demasiado[instalar el dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md). Asegúrese de seguir las instrucciones de hello exactamente.
> 
> 

### <a name="new-device-with-ebod-enclosure"></a>Dispositivo nuevo con gabinete EBOD
modelo de Hello 8600 StorSimple tiene un alojamiento principal y alojamiento de EBOD. Para ello, Hola unidades toobe cableado conjuntamente para alimentación y conectividad Serial Attached SCSI (SAS).

Al configurar este dispositivo para hello primera vez, realice los pasos de Hola para cableado de SAS y los pasos de hello, a continuación, completa para el cableado de alimentación.

[!INCLUDE [storsimple-sas-cable-8600](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

> [!NOTE]
> Para el programa de instalación de dispositivos completa y cableado instrucciones, vaya demasiado[instalar su dispositivo 8600 StorSimple](storsimple-8600-hardware-installation.md). Asegúrese de seguir las instrucciones de hello exactamente.

## <a name="turn-on-a-device-after-shutdown"></a>Activar un dispositivo después del apagado
Hola pasos para activar un dispositivo StorSimple después de que se ha apagado son diferentes dependiendo de si el dispositivo de hello es un 8100 o en un modelo de 8600. Hola 8100 tiene un único alojamiento principal, mientras que Hola 8600 es un dispositivo de doble alojamiento con un alojamiento principal y un alojamiento de EBOD.

* [Dispositivo solo con gabinete principal](#device-with-primary-enclosure-only)
* [Dispositivo con gabinete EBOD](#device-with-ebod-enclosure)

### <a name="device-with-primary-enclosure-only"></a>Dispositivo solo con gabinete principal
Después de un apagado, utilice Hola siguiendo el procedimiento tooturn en un dispositivo de StorSimple con un alojamiento principal y no alojamiento de EBOD.

#### <a name="tooturn-on-a-device-with-a-primary-enclosure-only"></a>tooturn en un dispositivo con un alojamiento principal únicamente
1. Asegúrese de que los interruptores de alimentación de Hola de ambos Power y módulos y refrigeración (PCM) están en la posición de apagado de Hola. Si Hola modificadores no están en posición de apagado de hello, a continuación, voltear ellos posición de apagado toohello y espere Hola luces toogo off.
2. Encienda el dispositivo de hello accionando los interruptores de alimentación de hello en la posición de ON toohello ambos PCM. debe activar el dispositivo de Hola.
3. Hola de comprobación siguientes tooverify que Hola dispositivo está completamente encendido:
   
   1. Hola Aceptar LED de ambos módulos PCM es verde.
   2. LED de estado de Hello en ambos controladores es verde sólido.
   3. Hello parpadea LED azul de uno de los controladores de hello, que indica que el controlador de hello está activo.
      
      Si alguna de estas condiciones no se cumple, el dispositivo no funciona correctamente. [Póngase en contacto con el soporte técnico de Microsoft](storsimple-8000-contact-microsoft-support.md).

### <a name="device-with-ebod-enclosure"></a>Dispositivo con gabinete EBOD
Después de un apagado, utilice Hola siguiendo el procedimiento tooturn en un dispositivo de StorSimple con un alojamiento principal y alojamiento de EBOD. Realice cada paso de la secuencia tal como se describe. Error toodo por lo que podría provocar pérdida de datos.

#### <a name="tooturn-on-a-device-with-a-primary-and-an-ebod-enclosure"></a>tooturn en un dispositivo con un elemento principal y alojamiento de EBOD
1. Asegúrese de que ese Hola alojamiento de EBOD está conectado toohello de alojamiento principal. Para obtener más información, consulte [Instalar el dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md).
2. Asegúrese de que ese Hola Power y módulos de refrigeración (PCM) en ambos Hola EBOD y contenedores principales están en la posición de apagado de Hola. Si Hola modificadores no están en posición de apagado de hello, a continuación, voltear ellos posición de apagado toohello y espere Hola luces toogo off.
3. Activar Hola alojamiento de EBOD primero accionando los interruptores de alimentación de hello en la posición de ON toohello ambos PCM. Hola LED del PCM debe ser verde. Un controlador EBOD LED verde en esta unidad indica que Hola alojamiento EBOD esté encendido.
4. Encienda el alojamiento principal de Hola accionando los interruptores de alimentación de hello en ambos posición de encendido de PCM toohello. Ahora debe ser todo el sistema Hello en.
5. Compruebe que Hola LED SAS sean verdes, lo que garantiza que esa conexión Hola entre Hola alojamiento de EBOD y alojamiento principal hello es bueno.

## <a name="turn-on-a-device-after-a-power-loss"></a>Activar un dispositivo después de una pérdida de energía
Una interrupción o una pérdida de energía puede apagar un dispositivo StorSimple. corte del suministro eléctrico Hola puede ocurrir en una de las fuentes de alimentación de Hola o ambas fuentes de alimentación. pasos de recuperación de Hello son diferentes dependiendo de si el dispositivo de hello es un 8100 o en un modelo de 8600. Hola 8100 tiene un único alojamiento principal, mientras que Hola 8600 es un dispositivo de doble alojamiento con un alojamiento principal y un alojamiento de EBOD. Esta sección describe el procedimiento de recuperación de Hola para cada escenario.

* [Dispositivo solo con gabinete principal](#8100)
* [Dispositivo con gabinete EBOD](#8600)

### <a name="device-with-primary-enclosure-only-a-name8100"></a>Dispositivo solo con gabinete principal <a name="8100">
sistema de Hello puede continuar su funcionamiento normal si hay tooone de pérdida de energía de las fuentes de alimentación. Sin embargo, tooensure alta disponibilidad del dispositivo de hello, restauración power toohello fuente de alimentación lo antes posible.

Si se produce un corte del suministro eléctrico o la interrupción de la energía en ambas fuentes de alimentación, sistema de Hola se apagará de forma ordenada y controlada. Cuando se restaura la alimentación de hello, sistema de Hola se encenderá automáticamente.

### <a name="device-with-ebod-enclosure-a-name8600"></a>Dispositivo con gabinete EBOD <a name="8600">
#### <a name="power-loss-on-one-power-supply"></a>Pérdida de energía en un sistema de alimentación
sistema de Hello puede continuar su funcionamiento normal si hay tooone de pérdida de energía de las fuentes de alimentación en el alojamiento principal de Hola o alojamiento de EBOD Hola. Sin embargo, tooensure alta disponibilidad del dispositivo de hello, restaure fuente de alimentación de energía toohello tan pronto como sea posible.

#### <a name="power-loss-on-both-power-supplies-on-primary-and-ebod-enclosures"></a>Pérdida de energía en ambos sistemas de alimentación en el gabinete principal y el gabinete EBOD
Si se produce una interrupción de interrupción o de alimentación de energía en ambas fuentes de alimentación, Hola alojamiento de EBOD se apagará inmediatamente y alojamiento principal Hola se apagará de forma ordenada y controlada. Cuando se restaura la alimentación, el dispositivo de Hola se iniciará automáticamente.

Si Hola se apaga manualmente, a continuación, tomar Hola siguiendo los pasos toorestore de alimentación toohello sistema.

1. Encienda el alojamiento de EBOD Hola.
2. Una vez Hola alojamiento de EBOD está activado, activarlo en el alojamiento principal Hola.

### <a name="power-loss-on-both-power-supplies-on-ebod-enclosure"></a>Pérdida de energía en ambos sistemas de alimentación en el gabinete EBOD
Al configurar los cables, debe asegurarse de que ese hello EBOD nunca está conectado por sí sola tooa separar PDU. Si se producen errores hello EBOD y el alojamiento principal en hello mismo tiempo, el sistema de Hola se recuperará.

Si solo se produce un error en hello alojamiento de EBOD en ambas fuentes de alimentación, sistema de hello no se recuperará automáticamente. Toman Hola siguiendo los pasos tooturn en sistema de Hola y restaurar estado correcto de tooa:

1. Si está activado el alojamiento principal de hello, optar por desactivar los módulos de alimentación y refrigeración (PCM).
2. Espere unos minutos para hello sistema tooshut hacia abajo.
3. Encienda el alojamiento de EBOD Hola.
4. Una vez Hola alojamiento de EBOD está activado, activarlo en el alojamiento principal Hola.

## <a name="turn-on-a-device-after-hello-primary-and-ebod-enclosure-connection-is-lost"></a>Activar un dispositivo después de hello principal y se pierde la conexión del alojamiento EBOD
Si se pierde entre el controlador en espera de Hola y controlador de EBOD correspondiente Hola Hola conexión, el dispositivo de hello continúa toowork. Si se pierde la conexión de hello entre el controlador activo del sistema de Hola y el controlador de EBOD correspondiente de hello, debe producirse la conmutación por error y Hola dispositivo continuar toowork como normal.

Cuando se quitan los cables Serial Attached SCSI (SAS) o se rompe la conexión de Hola entre Hola alojamiento de EBOD y el alojamiento principal de Hola, dispositivo Hola dejará de funcionar. En este punto, realice Hola pasos.

### <a name="tooturn-on-hello-device-after-connection-is-lost"></a>tooturn en dispositivo de hello después de que se pierde la conexión
1. Hola de acceso del dispositivo de Hola.
2. Si se interrumpe la conexión del cable SAS entre el alojamiento EBOD de Hola y alojamiento principal Hola Hola, todas las asociaciones de seguridad LED de la línea en el alojamiento de EBOD Hola estará desactivada.
3. Apague ambos módulos de alimentación y refrigeración (PCM) en el alojamiento de EBOD de Hola y el alojamiento principal Hola.
4. Espere hasta que todas las luces de Hola de hello reverso de ambos alojamientos Hola desactivar.
5. Vuelva a insertar los cables SAS hello y asegúrese de que hay una buena conexión entre el alojamiento EBOD de Hola y alojamiento principal Hola.
6. Activar Hola alojamiento de EBOD primero accionando ambos posición de encendido de PCM conmutadores toohello.
7. Asegúrese de que alojamiento de EBOD Hola esté encendido comprobando que los LED de hello verde esté encendido.
8. Encienda el alojamiento principal Hola.
9. Asegúrese de que alojamiento principal de Hola esté encendido comprobando que el LED verde del controlador de hello está activado.
10. Compruebe que esa conexión del alojamiento EBOD con alojamiento principal Hola Hola sea buena comprobando que los LED (cuatro por controlador de EBOD) de la línea SAS de hello están todas en.

> [!IMPORTANT]
> Si los cables de hello SAS son defectuosos o conexión de Hola entre Hola alojamiento de EBOD y el alojamiento principal de Hola no es buena, al activar el sistema de hello, pasará al modo de recuperación. Si esto sucede, [póngase en contacto con el soporte técnico de Microsoft](storsimple-8000-contact-microsoft-support.md) .


## <a name="turn-off-a-running-device"></a>Apagar un dispositivo activo
Un dispositivo StorSimple en ejecución que necesite toobe apagar si se mueve, deja fuera de servicio o tiene un componente en mal estado que necesita toobe reemplazado. Hola pasos son diferentes dependiendo de si el dispositivo de StorSimple de hello es un 8100 o en un modelo de 8600. Hola 8100 tiene un único alojamiento principal, mientras que Hola 8600 es un dispositivo de doble alojamiento con un alojamiento principal y un alojamiento de EBOD. En esta sección se detalla Hola pasos tooshut hacia abajo un dispositivo en ejecución.

* [Dispositivo con gabinete principal](#8100a)
* [Dispositivo con gabinete EBOD](#8600a)

### <a name="device-with-primary-enclosure-a-name8100a"></a>Dispositivo con gabinete principal <a name="8100a">
tooshut hacia abajo de dispositivo de Hola de forma ordenada y controlada, se puede hacer mediante Hola portal de Azure clásico o a través de hello Windows PowerShell para StorSimple. 

> [!IMPORTANT]
> No apague un dispositivo en ejecución mediante el uso de botón de encendido de hello en hello parte posterior del dispositivo de Hola.
> 
> Antes de apagar el dispositivo de hello, asegúrese de que todos los componentes del dispositivo de hello están en buenas condiciones. En el portal de Azure clásico de Hola, navegue demasiado**dispositivos** > **mantenimiento** > **estado del Hardware**y compruebe el estado del programa Hola a todos componentes es verde. Esto solo sucede si el sistema funciona correctamente. Si el sistema de hello está apagando tooreplace un componente en mal estado, verá una error (rojo) o degradado (amarillo) estado de componente respectivo de Hola Hola **estado del Hardware**.
> 
> 

Después de obtener acceso a Hola Windows PowerShell para StorSimple o hello portal de Azure clásico, siga los pasos de hello en [apagar un dispositivo de StorSimple](storsimple-manage-device-controller.md#shut-down-a-storsimple-device). 

### <a name="device-with-ebod-enclosure-a-name8600a"></a>Dispositivo con gabinete EBOD <a name="8600a">
> [!IMPORTANT]
> Antes de apagar el alojamiento principal de Hola y el alojamiento de EBOD hello, asegúrese de que todos los componentes del dispositivo de hello están en buenas condiciones. En la consulta Hola portal de Azure, navegue demasiado**dispositivos** > **Monitor** > **estado del Hardware**y compruebe que todos los componentes de hello están en buenas condiciones.


#### <a name="tooshut-down-a-running-device-with-ebod-enclosure"></a>tooshut hacia abajo un dispositivo en ejecución con alojamiento de EBOD
1. Siga todos los pasos de hello enumerados en [apagar un dispositivo de StorSimple](storsimple-8000-manage-device-controller.md#shut-down-a-storsimple-device) para alojamiento principal Hola.
2. Después de hello alojamiento principal se apaga, apagar hello EBOD accionando los conmutadores de alimentación y módulo de refrigeración (PCM).
3. tooverify que Hola EBOD se ha cerrado, compruebe que todas las luces indicadoras de actividad Hola parte posterior del alojamiento EBOD Hola están desactivadas.

> [!NOTE]
> no se deben quitar cables SAS de Hola que son utilizados tooconnect Hola alojamiento EBOD toohello alojamiento principal hasta que después se cierra el sistema de Hola.

## <a name="next-steps"></a>Pasos siguientes
[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) .

