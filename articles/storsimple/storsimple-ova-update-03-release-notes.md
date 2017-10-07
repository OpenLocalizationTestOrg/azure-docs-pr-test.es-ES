---
title: "notas de la versión de las actualizaciones de matriz Virtual aaaStorSimple | Documentos de Microsoft"
description: "Abrir crítico se describen problemas y soluciones para la ejecución de StorSimple Virtual Array Hola actualización 0.3."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: b197651a-3c40-4185-b23d-4c8f22cfa8f4
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/15/2016
ms.author: alkohli
ms.openlocfilehash: 305e6419b248fde134abae65f3d2c241d72ffa18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-03-release-notes"></a>Notas de la versión de Update 0.3 de la matriz virtual de StorSimple
## <a name="overview"></a>Información general
Hola notas de la versión siguiente identifican problemas abiertos críticos de Hola y Hola problemas resueltos para las actualizaciones de Microsoft Azure StorSimple Virtual Array.

notas de la versión de Hola se actualizan continuamente, y cuando se detectan problemas críticos que requieren una solución, se agregan. Antes de implementar la matriz Virtual de StorSimple, consulte atentamente información de hello contenida en las notas de la versión de Hola.

Actualización 0.3 corresponde versión del software toohello **10.0.10288.0**.

> [!NOTE]
> Las actualizaciones causan interrupciones y reinician el dispositivo. Si E/S están en curso, dispositivo Hola incurre en tiempo de inactividad.
> 
> 

## <a name="whats-new-in-hello-update-03"></a>Novedades de hello Update 0.3
Update 0.3 es principalmente una compilación de corrección de errores. En esta versión, se han abordado varios errores que provocan errores de copia de seguridad en la versión anterior de Hola.

## <a name="issues-fixed-in-hello-update-03"></a>Problemas corregidos en hello Update 0.3
Hello tabla siguiente proporciona un resumen de problemas corregidos en esta versión.

| No. | Característica | Problema |
| --- | --- | --- |
| 1 |Copias de seguridad |Se encontró un problema en hello versión anterior, donde las copias de seguridad de hello produciría un error toocomplete para un recurso compartido de archivos. Si se produce este problema, producirá un trabajo de copia de seguridad de Hola y se genera una alerta crítica en hello StorSimple Manager toonotify Hola usuario. Este problema no afecta a los datos de hello en recursos compartidos de Hola o tener acceso a datos toohello. causa Hola se identificó y corrigió en esta versión. <br></br> corrección de Hello no aplica con carácter retroactivo tooshares que ya están experimentando este problema. Los clientes que están viendo este problema deben primero aplique la actualización 0.3, a continuación, póngase en contacto con Microsoft Support tooperform un problema de hello toofix copia de seguridad completa del sistema. En lugar de ponerse en contacto con Microsoft Support, los clientes también pueden restaurar desde una copia de seguridad correcto para recursos compartidos de hello afectado tooa nuevo recurso compartido. |
| 2 |iSCSI |Se encontró un problema en hello versión anterior, donde los volúmenes de hello desaparecerá cuando se copia el volumen de datos tooa en hello StorSimple Virtual Array. Este problema se ha corregido en esta versión. <br></br> correcciones de Hello surten efecto solo en recién creado volúmenes. correcciones de Hello no aplican con carácter retroactivo toovolumes que ya están experimentando este problema. Se recomienda a los clientes en línea los volúmenes de hello afectado toobring a través de Hola portal de Azure clásico, realizan una copia de seguridad para estos volúmenes y, a continuación, restauración estos volúmenes toonew de volúmenes. |

## <a name="known-issues-in-hello-update-03"></a>Problemas conocidos de actualización 0.3 Hola
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
| **8.** |Capacidad de recursos compartidos usada |Es posible que vea Compartir consumo cuando no hay ningún dato en el recurso compartido de Hola. Esto es porque la capacidad de hello utilizado para los recursos compartidos incluye metadatos. | |
| **9.** |Recuperación ante desastres |Solo puede realizar la recuperación de desastres de Hola de un toohello de servidor de archivos mismo dominio que la del dispositivo de origen Hola. Dispositivo de destino de tooa de recuperación de desastres en otro dominio no se admite en esta versión. |Esto se implementará en una versión posterior. |
| **10.** |Azure PowerShell |dispositivos virtuales de StorSimple de Hello no pueden administrarse a través de hello Azure PowerShell en esta versión. |Toda la administración de dispositivos virtuales Hola Hola debe realizarse a través de hello portal de Azure clásico y la interfaz de usuario de web local Hola. |
| **11.** |Cambio de contraseña |consola del dispositivo de matriz virtual Hola solo acepta datos proporcionados en el formato de teclado en-US. | |
| **12.** |CHAP |Las credenciales CHAP no se pueden quitar una vez creadas. Además, si modifica las credenciales CHAP hello, volúmenes tootake hello es necesario y, a continuación, colocarlos en línea para cambiar tootake efecto de Hola. |Este problema se corregirá en una versión posterior. |
| **13.** |Servidor iSCSI |Hola 'Usado el almacenamiento' muestra para un volumen de iSCSI puede ser diferente en el servicio StorSimple Manager hello y host de iSCSI de Hola. |host de iSCSI de Hello tiene vista de sistema de archivos de Hola.<br></br>dispositivo de Hello ve bloques Hola asignados al volumen de hello estaba al tamaño máximo de Hola. |
| **14.** |Servidor de archivos |Si un archivo en una carpeta tiene un flujo de datos alternativo (ADS) asociados a él, Hola anuncios no se copia o restaura a través de la recuperación ante desastres, clonación y recuperación de nivel de elemento. | |

## <a name="next-step"></a>Paso siguiente
[Instale la actualización 0.3](storsimple-ova-install-update-01.md) en la matriz virtual de StorSimple.

## <a name="references"></a>Referencias
¿Busca una nota de la versión anterior? Vaya a: 

* [Notas de la versión de la matriz virtual de StorSimple Update 0.1 y 0.2](storsimple-ova-update-01-release-notes.md)
* [Notas de la versión de disponibilidad general de la matriz Virtual de StorSimple](storsimple-ova-pp-release-notes.md)

