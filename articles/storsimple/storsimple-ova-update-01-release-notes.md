---
title: "notas de la versión de las actualizaciones de matriz Virtual aaaStorSimple | Documentos de Microsoft"
description: "Describe temas críticos y las soluciones de hello StorSimple Virtual Array ejecutar Update 0,2 y 0,1."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3993864d-2ddd-4302-a2f1-8d737fba6eab
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2016
ms.author: alkohli
ms.openlocfilehash: dfd38890feeb667c95134f2adbb35ce2df165620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-02-and-01-release-notes"></a>Notas de la versión de la matriz virtual de StorSimple Update 0.2 y 0.1
## <a name="overview"></a>Información general
Hola notas de la versión siguiente identifican problemas abiertos críticos de Hola y Hola problemas resueltos para las actualizaciones de Microsoft Azure StorSimple Virtual Array. (Microsoft Azure StorSimple Virtual Array es también conocida como dispositivo virtual local StorSimple de Hola o dispositivo virtual StorSimple de hello). 

notas de la versión de Hola se actualizan continuamente, y cuando se detectan problemas críticos que requieren una solución, se agregan. Antes de implementar el dispositivo virtual StorSimple, revise cuidadosamente información de hello contenida en las notas de la versión de Hola.

Actualización 0,2 corresponde versión del software toohello **10.0.10280.0**; Actualización 0,1 es versión **10.0.10279.0**. Hola secciones siguientes muestran los cambios de Hola para cada actualización. 

> [!NOTE]
> Las actualizaciones causan interrupciones y reiniciarán el dispositivo. Si E/S están en curso, el dispositivo de hello incurrirá en tiempo de inactividad.
> 
> 

## <a name="issues-fixed-in-hello-update-02"></a>Problemas corregidos en hello Update 0.2
Actualización 0,2 incluye todos los cambios de actualización 0,1 suma toohello corrección descrito en hello en la tabla siguiente:

| Característica | Problema |
| --- | --- |
| Actualizaciones |En la última versión de hello, las actualizaciones no detectan automáticamente en hello portal de Azure clásico, por lo que tenía toouse Hola actualizaciones de tooinstall de interfaz de usuario Web locales. Este problema está corregido en esta versión. Después de instalar la actualización 0,2, puede instalar las actualizaciones futuras mediante Hola portal de Azure clásico. |

## <a name="whats-new-in-hello-update-01"></a>Novedades de hello actualización 0,1
Actualización 0,1 contiene siguiente Hola mejoras y correcciones de errores. 

* **Resistencia mejorada para las interrupciones en la nube**: esta versión tiene varias correcciones de errores sobre recuperación ante desastres, copia de seguridad, restauración y niveles en caso de hello de una interrupción de conectividad en la nube. 
* **Mejorar el rendimiento de la restauración**: esta versión tiene correcciones de errores que ha significativamente reducir la cantidad de tiempo de finalización de Hola Hola de trabajos de restauración.
* **Automatizar la optimización de recuperación de espacio**: cuando se eliminan los datos en volúmenes con aprovisionamiento fino, hello bloques de almacenamiento sin usar necesitan toobe reclame. Esta versión tiene el proceso de recuperación de espacio de hello mejorada de nube Hola resultante en hello sin usar se están convirtiendo con mayor rapidez como comparados toohello versiones anteriores disponibles del espacio.
* **Nuevas imágenes de disco virtual**: nuevo VHD y VHDX, VMDK ahora están disponibles a través de hello portal de Azure clásico. Puede descargar estos dispositivos de actualización 0,1 imágenes tooprovision nueva.
* **Mejorar la exactitud de Hola de estado de los trabajos en el portal de Hola**: versión anterior del software, estado de trabajo informes en el portal de Hola Hola no era granular. Este problema se ha corregido en esta versión.
* **Experiencia de unión de dominio**: correcciones de errores relacionados con la unión toodomain y cambiar el nombre de dispositivo de Hola.

## <a name="issues-fixed-in-hello-update-01"></a>Problemas corregidos en hello actualización 0,1
Hello tabla siguiente proporciona un resumen de problemas corregidos en esta versión.

| No. | Característica | Problema |
| --- | --- | --- |
| 1 |VMDK |En algunas versiones de VMware, el disco del sistema operativo de Hola se considerada como dispersas causan las alertas e interrumpir las operaciones normales. Esto se ha corregido en esta versión. |
| 2 |Servidor iSCSI |En la última versión de hello, usuario Hola era toospecify requiere una puerta de enlace para cada interfaz de red habilitado del dispositivo virtual StorSimple. Este comportamiento ha cambiado en esta versión para que el usuario hello tiene tooconfigure al menos una puerta de enlace para todas las interfaces de red de hello habilitado. |
| 3 |Paquete de soporte |En Hola versión anterior del software, admite la recopilación del paquete no se pudo al tamaño de paquete de hello eran mayor que 1 GB. Este problema está corregido en esta versión. |
| 4 |Acceso a la nube |En la última versión de hello, si hello StorSimple Virtual Array no tiene conectividad de red y se reinicia, hello interfaz de usuario local tendría problemas de conectividad. Este problema se ha corregido en esta versión. |
| 5 |Gráficos de supervisión |En la versión anterior de hello, tras una conmutación por error de dispositivo, gráficos de utilización de capacidad de nube de hello muestran valores incorrectos en hello portal de Azure clásico. Esto se fija en la versión actual de Hola. |

## <a name="known-issues-in-hello-update-01"></a>Problemas conocidos de actualización 0,1 Hola
Hello tabla siguiente proporciona un resumen de los problemas conocidos de hello StorSimple Virtual Array e incluye problemas Hola se indica la versión de las versiones anteriores de Hola. **Hola se indica en esta versión de lanzamiento de los problemas marcados con un asterisco. Casi todos los problemas de hello en esta lista se realiza a través de versión de Hola GA de StorSimple Virtual Array.**

| No. | Característica | Problema | Soluciones alternativas o comentarios |
| --- | --- | --- | --- |
| **1.** |Actualizaciones |dispositivos virtuales Hola creados en la versión de vista previa de hello no pueden ser tooa actualizado que admite la versión de disponibilidad General. |Estos dispositivos virtuales deben conmutar por error para hello versión de disponibilidad General mediante un flujo de trabajo de recuperación ante desastres. |
| **2.** |Disco de datos aprovisionado |Una vez que ha aprovisionado un disco de datos de un determinado tamaño especificado y creado Hola correspondiente dispositivo StorSimple virtual, no debe aumentar o reducir el disco de datos de Hola. Por lo que intentar toodo se producirá una pérdida de todos los datos de hello en los niveles local hello de dispositivo de Hola. | |
| **3.** |Directiva de grupo |Cuando un dispositivo está unido a un dominio, aplicar una directiva de grupo puede afectar negativamente el funcionamiento de dispositivo de Hola. |Asegúrese de que la matriz virtual está en su propia unidad organizativa (OU) de Active Directory y ningún objeto de directiva de grupo (GPO) está tooit aplicada. |
| **4.** |Interfaz de usuario web local. |Si tiene las características de seguridad mejorada habilitadas en Internet Explorer (IE ESC), es posible que algunas páginas de la interfaz de usuario web local, tales como Solución de problemas o Mantenimiento, no funcionen correctamente. Asimismo, cabe la posibilidad de que los botones de estas páginas tampoco funcionen. |Desactive las características de seguridad mejorada de Internet Explorer. |
| **5.** |Interfaz de usuario web local. |En una máquina virtual de Hyper-V, Hola interfaces de red en la interfaz de usuario se muestran como interfaces de 10 GB/s de web de Hola. |Este comportamiento es un reflejo de Hyper-V. Hyper-V siempre muestra los adaptadores de red virtual a 10 Gbps. |
| **6.** |Volúmenes o recursos compartidos en niveles |No se admite para las aplicaciones que funcionan con hello StorSimple volúmenes en capas de bloqueo de intervalo de bytes. Si tiene habilitado un bloqueo de intervalo de bytes, la organización en niveles de StorSimple no funcionará. |Entre las medidas recomendadas se incluyen:  <br></br>Desactive el bloqueo del intervalo de bytes en la lógica de la aplicación.<br></br>Elegir datos tooput para esta aplicación en los volúmenes anclados localmente los volúmenes de tootiered diferencia.<br></br>*Advertencia*: si con localmente anclado volúmenes y está habilitado el bloqueo de intervalo de bytes, tenga en cuenta que el volumen de hello anclado localmente puede estar conectado incluso antes de completar la restauración de Hola. En esos casos, si una restauración está en curso, a continuación, se debe esperar a hello toocomplete de restauración. |
| **7.** |Recursos compartidos organizados en niveles |Si trabaja con archivos de gran tamaño, estos podrían ocasionar que la organización en niveles se desarrolle lentamente. |Cuando se trabaja con archivos grandes, se recomienda que ese archivo más grande de hello es menor que 3% del tamaño del recurso compartido de Hola. |
| **8.** |Capacidad de recursos compartidos usada |Es posible que vea Compartir consumo en ausencia de Hola de todos los datos en el recurso compartido de Hola. Esto es porque la capacidad de hello utilizado para los recursos compartidos incluye metadatos. | |
| **9.** |Recuperación ante desastres |Solo puede realizar la recuperación de desastres de Hola de un toohello de servidor de archivos mismo dominio que la del dispositivo de origen Hola. Dispositivo de destino de tooa de recuperación de desastres en otro dominio no se admite en esta versión. |Esta característica se implementará en una versión posterior. |
| **10.** |Azure PowerShell |dispositivos virtuales de StorSimple de Hello no pueden administrarse a través de hello Azure PowerShell en esta versión. |Toda la administración de dispositivos virtuales Hola Hola debe realizarse a través de hello portal de Azure clásico y la interfaz de usuario de web local Hola. |
| **11.** |Cambio de contraseña |consola del dispositivo de matriz virtual Hola solo acepta datos proporcionados en el formato de teclado en-US. | |
| **12.** |CHAP |Las credenciales CHAP no se pueden quitar una vez creadas. Además, si modifica las credenciales CHAP hello, deberá volúmenes tootake hello y, a continuación, colocarlos en línea para cambiar tootake efecto de Hola. |Esta situación se abordará en una versión posterior. |
| **13.** |Servidor iSCSI |Hola 'Usado el almacenamiento' muestra para un volumen de iSCSI puede ser diferente en el servicio StorSimple Manager hello y host de iSCSI de Hola. |host de iSCSI de Hello tiene vista de sistema de archivos de Hola.<br></br>dispositivo de Hello ve bloques Hola asignados al volumen de hello estaba al tamaño máximo de Hola. |
| **14.** |Servidor de archivos* |Si un archivo en una carpeta tiene un flujo de datos alternativo (ADS) asociados a él, Hola anuncios no se copia o restaura a través de la recuperación ante desastres, clonación y recuperación de nivel de elemento. | |

## <a name="next-step"></a>Paso siguiente
[Instale actualizaciones](storsimple-ova-install-update-01.md) en la matriz virtual de StorSimple.

