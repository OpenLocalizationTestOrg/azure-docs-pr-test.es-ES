---
title: "notas de la versión de 0,6 de aaaStorSimple actualización de matriz Virtual | Documentos de Microsoft"
description: "Abrir crítico se describen problemas y soluciones para la ejecución de StorSimple Virtual Array Hola actualizan 0,6."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/24/2017
ms.author: alkohli
ms.openlocfilehash: 7b573457dc07ce41e95d49d66ccc174045f31a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-06-release-notes"></a>Notas de la versión de StorSimple Virtual Array Update 0.6

## <a name="overview"></a>Información general

Hola notas de la versión siguiente identifican problemas abiertos críticos de Hola y Hola problemas resueltos para las actualizaciones de Microsoft Azure StorSimple Virtual Array.

notas de la versión de Hola se actualizan continuamente, y cuando se detectan problemas críticos que requieren una solución, se agregan. Antes de implementar la matriz Virtual de StorSimple, consulte atentamente información de hello contenida en las notas de la versión de Hola.

Actualización 0,6 corresponde versión del software toohello **10.0.10293.0**.

> [!IMPORTANT]
> - Las actualizaciones causan interrupciones y reinician el dispositivo. Si E/S están en curso, dispositivo Hola incurre en tiempo de inactividad. Para obtener instrucciones detalladas sobre cómo tooapply Hola actualización, vaya demasiado[instale la actualización 0,6](storsimple-virtual-array-install-update-06.md).
>
> - Recomendamos encarecidamente que instale Update 0.6 inmediatamente porque contiene correcciones de seguridad críticas.


## <a name="whats-new-in-hello-update-06"></a>Novedades de hello actualización 0,6
Update 0.6 es una actualización crítica y se debe implementar de forma inmediata. Esta actualización contiene Hola siguientes correcciones: 

- **Revisiones de seguridad de Windows**: esta versión contiene **correcciones de seguridad críticas de Windows**. Revise Hola después de las actualizaciones de seguridad para obtener más información acerca de los problemas de seguridad de Hola y Hola correcciones asociadas:
    - [Actualización de calidad exclusiva de seguridad de diciembre de 2016 para Windows 8.1 y Windows Server 2012 R2](https://support.microsoft.com/help/3205400/december-2016-security-only-quality-update-for-windows-8.1-and-windows-server-2012-r2)
    - [Actualización de calidad exclusiva de seguridad de marzo de 2017 para Windows 8.1 y Windows Server 2012 R2](https://support.microsoft.com/help/4012213/march-2017-security-only-quality-update-for-windows-8-1-and-windows-server-2012-r23)
    - [9 de mayo de 2017: KB4019213 (actualización solo de seguridad)](https://support.microsoft.com/help/4019213/windows-8-update-kb4019213)

- **Restaurar corrección** -en versiones anteriores, se produjo un error que podría impedir la restauración de Hola de finalización. Este error se ha corregido en esta versión.


## <a name="issues-fixed-in-hello-update-06"></a>Problemas corregidos en hello actualización 0,6

Hello tabla siguiente proporciona un resumen de problemas corregidos en esta versión.

| No. | Característica | Problema |
| --- | --- | --- |
| 1 |Seguridad| Esta versión contiene actualizaciones críticas de seguridad de Windows. Se recomienda que instale esta actualización inmediatamente.|
| 2 |Restauración| Durante una restauración, se ha producido una condición de carrera que impedirían que el trabajo de restauración de Hola de finalización. corrección de errores de Hello corrige esta condición de carrera.|


## <a name="known-issues-in-hello-update-06"></a>Problemas conocidos de actualización 0,6 Hola

Hello tabla siguiente proporciona un resumen de los problemas conocidos de hello StorSimple Virtual Array e incluye problemas Hola se indica la versión de las versiones anteriores de Hola.

| No. | Característica | Problema | Soluciones alternativas o comentarios |
| --- | --- | --- | --- |
| **1.** |Actualizaciones |dispositivos virtuales Hola creados en la versión de vista previa de hello no pueden ser tooa actualizado que admite la versión de disponibilidad General. |Estos dispositivos virtuales deben conmutar por error para hello versión de disponibilidad General mediante un flujo de trabajo de recuperación ante desastres. |
| **2.** |Disco de datos aprovisionado |Una vez que ha aprovisionado un disco de datos de un determinado tamaño especificado y creado Hola correspondiente dispositivo StorSimple virtual, no debe aumentar o reducir el disco de datos de Hola. Se intentó una toodo da como resultado una pérdida de todos los datos de hello en los niveles local hello de dispositivo de Hola. | |
| **3.** |Directiva de grupo |Cuando un dispositivo está unido a un dominio, aplicar una directiva de grupo puede afectar negativamente el funcionamiento de dispositivo de Hola. |Asegúrese de que la matriz virtual está en su propia unidad organizativa (OU) de Active Directory y ningún objeto de directiva de grupo (GPO) está tooit aplicada. |
| **4.** |Interfaz de usuario web local. |Si tiene las características de seguridad mejorada habilitadas en Internet Explorer (IE ESC), es posible que algunas páginas de la interfaz de usuario web local, tales como Solución de problemas o Mantenimiento, no funcionen correctamente. Asimismo, cabe la posibilidad de que los botones de estas páginas tampoco funcionen. |Desactive las características de seguridad mejorada de Internet Explorer. |
| **5.** |Interfaz de usuario web local. |En una máquina virtual de Hyper-V, Hola interfaces de red en la interfaz de usuario se muestran como interfaces de 10 GB/s de web de Hola. |Este comportamiento es un reflejo de Hyper-V. Hyper-V siempre muestra los adaptadores de red virtual a 10 Gbps. |
| **6.** |Volúmenes o recursos compartidos en niveles |No se admite para las aplicaciones que funcionan con hello StorSimple volúmenes en capas de bloqueo de intervalo de bytes. Si tiene habilitado un bloqueo de intervalo de bytes, la organización en niveles de StorSimple no funciona. |Entre las medidas recomendadas se incluyen:  <br></br>Desactive el bloqueo del intervalo de bytes en la lógica de la aplicación.<br></br>Elegir datos tooput para esta aplicación en los volúmenes anclados localmente los volúmenes de tootiered diferencia.<br></br>*Advertencia*: al usar localmente anclado volúmenes y está habilitado el bloqueo de intervalo de bytes, volumen Hola anclado localmente puede estar conectado incluso antes de completar la restauración de Hola. En esos casos, si una restauración está en curso, a continuación, se debe esperar a hello toocomplete de restauración. |
| **7.** |Recursos compartidos organizados en niveles |Si trabaja con archivos de gran tamaño, estos podrían ocasionar que la organización en niveles se desarrolle lentamente. |Cuando se trabaja con archivos grandes, se recomienda que ese archivo más grande de hello es menor que 3% del tamaño del recurso compartido de Hola. |
| **8.** |Capacidad de recursos compartidos usada |Es posible que vea Compartir consumo cuando no hay ningún dato en el recurso compartido de Hola. Este consumo es porque la capacidad de hello utilizado para los recursos compartidos incluye los metadatos. | |
| **9.** |Recuperación ante desastres |Solo puede realizar la recuperación de desastres de Hola de un toohello de servidor de archivos mismo dominio que la del dispositivo de origen Hola. Dispositivo de destino de tooa de recuperación de desastres en otro dominio no se admite en esta versión. |Esto se implementará en una versión posterior. Para obtener más información, consulte demasiado[conmutación por error y recuperación ante desastres de la matriz Virtual de StorSimple](storsimple-virtual-array-failover-dr.md) |
| **10.** |Azure PowerShell |dispositivos virtuales de StorSimple de Hello no pueden administrarse a través de hello Azure PowerShell en esta versión. |Toda la administración de dispositivos virtuales Hola Hola debe realizarse a través de hello Azure hello y portal de IU web local. |
| **11.** |Cambio de contraseña |Hello consola del dispositivo virtual matriz solo acepta datos proporcionados en la norma en-formato de teclado. | |
| **12.** |CHAP |Las credenciales CHAP no se pueden quitar una vez creadas. Además, si modifica las credenciales CHAP hello, volúmenes tootake hello es necesario y, a continuación, colocarlos en línea para cambiar tootake efecto de Hola. |Este problema se corregirá en una versión posterior. |
| **13.** |Servidor iSCSI |Hola 'Usado el almacenamiento' muestra para un volumen de iSCSI puede ser diferente en el servicio de administrador de dispositivos de StorSimple de Hola y de host de iSCSI de Hola. |host de iSCSI de Hello tiene vista de sistema de archivos de Hola.<br></br>dispositivo de Hello ve bloques Hola asignados al volumen de hello estaba al tamaño máximo de Hola. |
| **14.** |Servidor de archivos |Si un archivo en una carpeta tiene un flujo de datos alternativo (ADS) asociados a él, Hola anuncios no se copia o restaura a través de la recuperación ante desastres, clonación y recuperación de nivel de elemento. | |
| **15.** |Servidor de archivos |No se admiten los vínculos simbólicos. | |
| **16.** |Servidor de archivos |Archivos protegidos por Windows cifrado de sistema de archivos (EFS) cuando copió o almacenan en hello resultados del servidor de archivos de StorSimple Virtual Array en una configuración no admitida.  | |
| **17.** |Actualizaciones |Si ve el Error de código: 2359302 (hex 0x240006) al intentar tooinstall una revisión a través de Hola interfaz de usuario local, a continuación, esto implica que revisión Hola ya está instalada en el dispositivo.   | |

## <a name="next-step"></a>Paso siguiente
[Instale Update 0.6](storsimple-virtual-array-install-update-06.md) en StorSimple Virtual Array.

## <a name="references"></a>Referencias
¿Busca una nota de la versión anterior? Vaya a:

* [Notas de la versión de StorSimple Virtual Array Update 0.5](storsimple-virtual-array-update-05-release-notes.md)
* [Notas de la versión de StorSimple Virtual Array Update 0.4](storsimple-virtual-array-update-04-release-notes.md)
* [Notas de la versión de StorSimple Virtual Array Update 0.3](storsimple-ova-update-03-release-notes.md)
* [Notas de la versión de la matriz virtual de StorSimple Update 0.1 y 0.2](storsimple-ova-update-01-release-notes.md)
* [Notas de la versión de disponibilidad general de la matriz Virtual de StorSimple](storsimple-ova-pp-release-notes.md)

