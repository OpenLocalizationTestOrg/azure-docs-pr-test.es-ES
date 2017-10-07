---
title: "notas de la versión de 0,5 de aaaStorSimple actualización de matriz Virtual | Documentos de Microsoft"
description: "Abrir crítico se describen problemas y soluciones para la ejecución de StorSimple Virtual Array Hola actualizan 0,5."
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
ms.date: 05/08/2017
ms.author: alkohli
ms.openlocfilehash: a249e2e8f0105dcf6cc02d3136dfa3e37ea615d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-05-release-notes"></a>Notas de la versión de StorSimple Virtual Array Update 0.5

## <a name="overview"></a>Información general

Hola notas de la versión siguiente identifican problemas abiertos críticos de Hola y Hola problemas resueltos para las actualizaciones de Microsoft Azure StorSimple Virtual Array.

notas de la versión de Hola se actualizan continuamente, y cuando se detectan problemas críticos que requieren una solución, se agregan. Antes de implementar la matriz Virtual de StorSimple, consulte atentamente información de hello contenida en las notas de la versión de Hola.

Actualización 0,5 corresponde versión del software toohello **10.0.10290.0**.

> [!NOTE]
> Las actualizaciones causan interrupciones y reinician el dispositivo. Si E/S están en curso, dispositivo Hola incurre en tiempo de inactividad. Para obtener instrucciones detalladas sobre cómo tooapply Hola actualización, vaya demasiado[instale la actualización 0,5](storsimple-virtual-array-install-update-05.md).


## <a name="whats-new-in-hello-update-05"></a>Novedades de hello actualización 0,5
Update 0.5 es principalmente una compilación de corrección de errores. las principales mejoras de Hola y correcciones de errores son los siguientes:

- **Mejoras en la resistencia de la copia de seguridad** -esta versión tiene revisiones que mejoran la resistencia de copia de seguridad de Hola. Hola versiones anteriores, las copias de seguridad se han reintentado solo para ciertas excepciones. Esta versión reintenta todas las excepciones de copia de seguridad de Hola y Hola de hace copias de seguridad más resistentes.

- **Las actualizaciones para la supervisión de la utilización de almacenamiento** -a partir de 30 de junio de 2017, Hola almacenamiento la supervisión del uso de la serie de dispositivos virtuales de StorSimple que se va a retirar. Esto aplica toohello gráficos en todas las matrices virtual Hola ejecuta Update 0,4 o inferior de supervisión. Esta actualización incluye cambios de hello necesarios para toocontinue Hola uso de uso de almacenamiento de supervisión en hello portal de Azure. Instale esta actualización crítica antes del 30 de junio de 2017 toocontinue mediante la característica de supervisión de Hola.


## <a name="issues-fixed-in-hello-update-05"></a>Problemas corregidos en hello actualización 0,5

Hello tabla siguiente proporciona un resumen de problemas corregidos en esta versión.

| No. | Característica | Problema |
| --- | --- | --- |
| 1 |Resistencia de copia de seguridad| Hola versiones anteriores, las copias de seguridad se han reintentado solo para ciertas excepciones. Esta versión contiene una copias de seguridad de corrección toomake más resistente reintentando todas las excepciones de copia de seguridad de Hola.|
| 2 |Supervisión| supervisión del uso de almacenamiento de Hello para la serie de dispositivos virtuales StorSimple quedará en desuso a partir del 30 de junio de 2017. Esta acción afecta Hola gráficos en servicio de administrador de dispositivos de StorSimple de hello en ejecución en arreglos de discos virtuales de StorSimple de supervisión (modelo de 1200). Esta versión tiene las actualizaciones que permiten el uso de hello usuario toocontinue Hola de supervisión de uso de almacenamiento de arreglos de discos virtuales de hello más allá del 30 de junio de 2017.|
| 3 |Servidor de archivos| Hola versiones anteriores, un usuario pudieron copiar erróneamente matriz virtual toohello de archivos cifrados. Esta versión contiene una corrección que no permitiría la operación de copia de la matriz de toovirtual archivos cifrados. Si el dispositivo tiene existente toohello anteriores de los archivos cifrados de actualización, las copias de seguridad continuará toofail hasta que se eliminan todos los archivos de hello cifrado del sistema de Hola. |


## <a name="known-issues-in-hello-update-05"></a>Problemas conocidos de actualización 0,5 Hola

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

## <a name="next-step"></a>Paso siguiente
[Instalación de Update 0.5](storsimple-virtual-array-install-update-05.md) en StorSimple Virtual Array

## <a name="references"></a>Referencias
¿Busca una nota de la versión anterior? Vaya a:

* [Notas de la versión de StorSimple Virtual Array Update 0.4](storsimple-virtual-array-update-04-release-notes.md)
* [Notas de la versión de StorSimple Virtual Array Update 0.3](storsimple-ova-update-03-release-notes.md)
* [Notas de la versión de la matriz virtual de StorSimple Update 0.1 y 0.2](storsimple-ova-update-01-release-notes.md)
* [Notas de la versión de disponibilidad general de la matriz Virtual de StorSimple](storsimple-ova-pp-release-notes.md)

