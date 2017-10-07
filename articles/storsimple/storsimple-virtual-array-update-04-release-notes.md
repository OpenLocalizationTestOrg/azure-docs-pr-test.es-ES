---
title: "notas de la versión 0,4 de aaaStorSimple actualización de matriz Virtual | Documentos de Microsoft"
description: "Abrir crítico se describen problemas y soluciones para la ejecución de StorSimple Virtual Array Hola actualizan 0.4."
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
ms.date: 04/05/2017
ms.author: alkohli
ms.openlocfilehash: 1fd174ff483f4f7b1b4a7853c9d9573d1e948cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-04-release-notes"></a>Notas de la versión de Update 0.4 de la matriz virtual de StorSimple

## <a name="overview"></a>Información general

Hola notas de la versión siguiente identifican problemas abiertos críticos de Hola y Hola problemas resueltos para las actualizaciones de Microsoft Azure StorSimple Virtual Array.

notas de la versión de Hola se actualizan continuamente, y cuando se detectan problemas críticos que requieren una solución, se agregan. Antes de implementar la matriz Virtual de StorSimple, consulte atentamente información de hello contenida en las notas de la versión de Hola.

Actualización 0,4 corresponde versión del software toohello **10.0.10289.0**.

> [!NOTE]
> Las actualizaciones causan interrupciones y reinician el dispositivo. Si E/S están en curso, dispositivo Hola incurre en tiempo de inactividad.


## <a name="whats-new-in-hello-update-04"></a>Novedades de hello actualización 0,4
Update 0.4 es principalmente una compilación de corrección de errores, junto con algunas mejoras. En esta versión, se han abordado varios errores que provocan errores de copia de seguridad en la versión anterior de Hola. las principales mejoras de Hola y correcciones de errores son los siguientes:

- **Mejoras de rendimiento de copia de seguridad** -esta versión ha realizado varias mejoras claves rendimiento de copia de seguridad de tooimprove Hola. Como resultado, las copias de seguridad de Hola que incluyen a un gran número de archivos ven una reducción significativa del toocomplete de tiempo de hello, para las copias de seguridad completas e incrementales.

- **Mejorar el rendimiento de la restauración** -esta versión contiene mejoras que mejoran significativamente el rendimiento de la restauración de hello cuando se usa el gran número de archivos. Si utiliza 2-4 millones de archivos, le recomendamos que aprovisionar una matriz virtual con mejoras de hello toosee de 16 GB de RAM. Al usar menos de 2 millones de archivos, requisitos mínimos de hello para la máquina virtual de Hola continúa toobe 8 GB de RAM.

- **Paquete de mejoras tooSupport** -Hola mejoras estadísticas Hola de disco, CPU, memoria, red y en la nube en el paquete de soporte de Hola y mejorar el proceso de Hola de diagnosticar y depurar los problemas del dispositivo de inicio de sesión.

- **Límite localmente anclado iSCSI volúmenes too200 GB** -para volúmenes anclados localmente, es recomendable que limite el volumen de iSCSI de 200 GB tooa en la matriz Virtual de StorSimple. reserva local de Hola para volúmenes en capas continúa toobe 10% de hello aprovisionar el tamaño del volumen pero está limitado a 200 GB. 

- **Correcciones de errores relacionados con la copia de seguridad** -en versiones anteriores del software, había toobackups relacionados problemas que podrían causar errores de copia de seguridad. En esta versión se han solucionado estos errores.


## <a name="issues-fixed-in-hello-update-04"></a>Problemas corregidos en hello actualización 0,4

Hello tabla siguiente proporciona un resumen de problemas corregidos en esta versión.

| No. | Característica | Problema |
| --- | --- | --- |
| 1 |Rendimiento de copia de seguridad|Hola, las versiones anteriores, las copias de seguridad de hello relacionadas con gran número de archivos tardaría una toocomplete mucho tiempo (en orden de Hola de días). En esta versión, Hola completa y copias de seguridad incrementales ver una reducción significativa del Hola tiempo toocompletion. |
| 2 |Paquete de soporte|Disco, CPU, memoria, red y estadísticas en la nube ahora se registran en los registros de soporte técnico de toohello creación de paquetes de soporte técnico de hello muy eficaces para solucionar los problemas del dispositivo.|
| 3 |Backup |En versiones anteriores, las copias de seguridad de larga ejecución podría producir una crisis de espacio en el dispositivo de Hola que provocan errores de copia de seguridad. Este error se trata en esta versión al permitir que las copias de seguridad ya no más de 5 tooqueue al mismo tiempo.|
| 4 |iSCSI | En versiones anteriores, reserva local de Hola para volúmenes anclados localmente o en niveles era el 10% del tamaño del volumen Hola aprovisionado. En esta versión, reserva local de Hola para todos los volúmenes iSCSI (local anclada o niveles) es % too10 limitado con un máximo de hasta 200 GB (para volúmenes en capas superiores a 2 TB), por tanto, liberar más espacio en disco local de Hola. Se recomienda que los volúmenes de hello anclado localmente en esta versión sea limitado too200 GB.|


## <a name="known-issues-in-hello-update-04"></a>Problemas conocidos de actualización 0,4 Hola

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
| **15.** |Servidor de archivos |No se admiten los vínculos simbólicos. | |
| **16.** |Servidor de archivos |Archivos protegidos por Windows cifrado de sistema de archivos (EFS) cuando copió o almacenan en hello resultados del servidor de archivos de StorSimple Virtual Array en una configuración no admitida.  | |

## <a name="next-step"></a>Paso siguiente
[Instale Update 0.4](storsimple-virtual-array-install-update-04.md) en StorSimple Virtual Array.

## <a name="references"></a>Referencias
¿Busca una nota de la versión anterior? Vaya a: 

* [Notas de la versión de StorSimple Virtual Array Update 0.3](storsimple-ova-update-03-release-notes.md)
* [Notas de la versión de la matriz virtual de StorSimple Update 0.1 y 0.2](storsimple-ova-update-01-release-notes.md)
* [Notas de la versión de disponibilidad general de la matriz Virtual de StorSimple](storsimple-ova-pp-release-notes.md)

