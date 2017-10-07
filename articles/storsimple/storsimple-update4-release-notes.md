---
title: "notas de la versión de aaaStorSimple 8000 Series Update 4 | Documentos de Microsoft"
description: "Describe nuevas características de hello, problemas y soluciones alternativas para StorSimple 8000 Series Update 4."
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
ms.date: 04/04/2017
ms.author: alkohli
ms.openlocfilehash: 4bca8ca222e6706fd6eaf56b702b0d34b6ffd1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-4-release-notes"></a>Notas de la versión de la serie StorSimple 8000 Update 4

## <a name="overview"></a>Información general

Hello siguientes notas de la versión describen características nuevas de hello e identifican problemas abiertos críticos de Hola para StorSimple 8000 Series Update 4. También contienen una lista de las actualizaciones de software de StorSimple Hola incluidos en esta versión. 

Actualización 4 puede ser dispositivo de StorSimple de tooany aplicado ejecutando versión (GA) o actualización 0,1 a través de la actualización 3.1. versión del dispositivo Hola asociado con la actualización 4 es 6.3.9600.17820.

Revise información Hola contenida en la versión de Hola notas antes de implementar Hola actualización de la solución StorSimple.

> [!IMPORTANT]
> * Update 4 tiene actualizaciones de software de dispositivo, firmware de USM, firmware y controlador LSI, firmware de disco, Storport y Spaceport, seguridad y otras actualizaciones de SO. Tarda aproximadamente 4 horas tooinstall esta actualización. La actualización del firmware de disco es una actualización perjudicial y provoca un tiempo de inactividad en el dispositivo. Se recomienda aplicar actualización 4 tookeep su dispositivo actualizado. 
> * Para cada versión nueva, quizás no pueda ver las actualizaciones inmediatamente porque se realiza una implementación por fases de actualizaciones de Hola. Espere unos días y luego busque actualizaciones de nuevo ya que estas estarán disponibles pronto.

## <a name="whats-new-in-update-4"></a>Novedades de la actualización 4

Hello siguientes claves mejoras y correcciones de errores se realizaron en la actualización 4.

* **Información más automatizada algoritmos de recuperación de espacio** : en la actualización 4, hello algoritmos de recuperación de espacio automatizadas son recuperación de espacio de hello tooadjust mejorada ciclos en función de hello esperada reclamar espacio disponible en la nube de Hola. 

* **Mejoras de rendimiento para volúmenes anclados localmente** – actualización 4 ha mejorado el rendimiento de Hola de volúmenes anclados localmente en escenarios que tienen la recopilación de datos de alta (tamaño de datos comparable toovolume).

* **Restauración basadas en el mapa térmico** : Hola anteriores versiones, después de una recuperación ante desastres (DR), datos de Hola se restauran desde hello en la nube basada en patrones de acceso de Hola que resulta en un rendimiento lento. 

    Se implementa una característica nueva en la actualización 4 que realiza un seguimiento de frecuencia de acceso a datos toocreate un mapa térmico cuando el dispositivo de hello esté en uso anterior tooDR (usados más fragmentos de datos tienen alta calor mientras que menor usar fragmentos tienen calor baja). Después de la recuperación ante desastres, StorSimple usa Hola mapa térmico tooautomatically restauración y rehidratar datos Hola de nube de Hola. 

    Todas las restauraciones de hello ahora serán en función de mapa térmico. Para obtener más información sobre cómo según el mapa térmico tooquery y Cancelar trabajos de restauración y rehidratación, vaya demasiado[de Windows PowerShell para StorSimple referencia del cmdlet](https://technet.microsoft.com/library/dn688168.aspx).

* **Herramienta de diagnóstico de StorSimple** : en Update 4, un diagnóstico de StorSimple se está herramienta publicado tooallow para diagnosticar fácil y solución de problemas relacionados con el estado de componentes de hardware, red, rendimiento y toosystem. Esta herramienta se ejecuta a través de hello Windows PowerShell para StorSimple. Para obtener más información, consulte demasiado[solucionar problemas con la herramienta de diagnóstico de StorSimple](storsimple-8000-diagnostics.md).

* **Herramienta de migración de StorSimple basada en interfaz de usuario** -toothis anteriores de la versión, migración de datos de la serie 5000-7000 necesario Hola usuarios tooexecute un elemento de flujo de trabajo de migración de hello mediante la interfaz de PowerShell de Azure de Hola. En esta versión, una fácil de usar herramienta queda disponible para compatibilidad con toofacilitate la migración de StorSimple basada en la interfaz de usuario Hola mismo flujo de trabajo de migración. Esta herramienta también permitiría para la consolidación de Hola de sectores de almacenamiento de recuperación. 

* **Cambios relacionados con el estándar FIPS** : esta versión y versiones posteriores, FIPS está habilitada de forma predeterminada en todos los dispositivos de la serie de hello StorSimple 8000 para ambos Hola Microsoft Azure Government y cuentas de nube pública de Azure.

* **Actualizar los cambios de** : en esta versión, tooupdate relacionados con errores se han corregido errores.

* **Alerta de errores de disco** -se agrega una nueva alerta que avisa al usuario de hello inminente de errores de disco en esta versión. Si se produce esta alerta, póngase en contacto con Microsoft Support tooship un disco de reemplazo. Para obtener más información, consulte demasiado[alertas de hardware en el dispositivo StorSimple](storsimple-manage-alerts.md#hardware-alerts).

* **Cambios de reemplazo de controlador** -se agregó un cmdlet que permite el estado de hello tooquery Hola de usuario del proceso de reemplazo de controlador de hello en esta versión. Para obtener más información, visite toohello [estado del reemplazo de controlador de cmdlet tooquery](https://technet.microsoft.com/library/dn688168.aspx).


## <a name="issues-fixed-in-update-4"></a>Problemas corregidos en Update 4

Hello tabla siguiente proporciona un resumen de los problemas corregidos en la actualización 4.    

| No | Característica | Problema | Se aplica a dispositivos toophysical | Se aplica a dispositivos toovirtual |
| --- | --- | --- | --- | --- |
| 1 |Conmutación por error |Hola versión anterior, después de hello conmutación por error, no existe era un problema relacionado con toocleanup observado al sitio de cliente de Hola. Este problema está corregido en esta versión. |Sí |Sí |
| 2 |Volúmenes anclados localmente |En la versión anterior de hello, hubo una creación de volúmenes de problema toorelated para volúmenes anclados localmente que pueda provocar errores de creación de volumen. La causa raíz de este problema se corrigió en esta versión. |Sí |No |
| 3 |Paquete de soporte |En la versión anterior, había paquete tooSupport relacionados de problemas que pueda provocar una excepción System.OutOfMemory u otros errores lo que produce un error de creación del paquete de soporte técnico. Estos errores se corrigieron en esta versión. |Sí |Sí |
| 4 |Supervisión |No existe en la versión anterior, en un problema relacionado con gráficos de toomonitoring para volúmenes anclados localmente que se mostró el consumo en EB. Este error se solucionó en esta versión. |Sí |Sí |
| 5 |Migración |En la versión anterior, hubo varios problemas relacionados toohello confiabilidad de la migración de dispositivos de la serie 5000-7000 serie too8000. Estos problemas se solucionaron en esta versión. |Sí |Sí |
| 6 |Actualizar |En versiones anteriores, si se produjo un error de actualización, controladores de hello entrarían en modo de recuperación y, por tanto, Hola usuario no puede continuar con la actualización de Hola y necesitaría toocontact Microsoft Support. <br> Este comportamiento se cambió en esta versión. Si el usuario hello tiene un error de actualización después de ambos controladores Hola ejecución Hola misma versión (actualización 4), Hola controladores no entra en modo de recuperación. Si el usuario de hello encuentra este error, se recomienda que espere un poco y, a continuación, vuelva a intentar Hola actualización. reintento de Hello podía realizarse correctamente. Si se produce un error de reintento de hello, a continuación, debe ponerse en contacto con Microsoft Support. |Sí |Sí |


## <a name="known-issues-in-update-4-from-previous-releases"></a>Problemas conocidos en Update 4 de las versiones anteriores

No hay ningún problema conocido en Update 4. Para obtener una lista de problemas que se realiza a través de tooUpdate 4 de las versiones anteriores, vaya demasiado[notas de la versión de actualización 3](storsimple-update3-release-notes.md#known-issues-in-update-3).

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-4"></a>Controlador SCSI conectado en serie (SAS) y actualizaciones de firmware en Update 4

Esta versión tiene actualizaciones de firmware y controlador LSI y controlador SAS. Para obtener más información sobre cómo tooinstall estas actualizaciones, consulte [instalar la actualización 4](storsimple-install-update-4.md) en el dispositivo StorSimple.

## <a name="virtual-device-updates-in-update-4"></a>Actualizaciones de dispositivos virtuales en Update 4

Esta actualización no puede ser aplicada toohello dispositivo de StorSimple en la nube (también conocido como Hola dispositivo virtual). Nuevos dispositivos virtuales necesitará toobe creado. 

## <a name="next-step"></a>Paso siguiente

Obtenga información acerca de cómo demasiado[instalar la actualización 4](storsimple-install-update-4.md) en el dispositivo StorSimple.

