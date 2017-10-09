---
title: "notas de la versión de aaaStorSimple 8000 Series Update 3 | Documentos de Microsoft"
description: "Describe nuevas características de hello, problemas y soluciones alternativas para StorSimple 8000 Series Update 3."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 2158aa7a-4ac3-42ba-8796-610d1adb984d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5bfcba61f7f210531437f650eafaad4dbd8c7c45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="update-3-release-notes-for-your-storsimple-8000-series-device"></a>Actualización de las notas de la versión Update 3 del dispositivo StorSimple serie 8000

## <a name="overview"></a>Información general
Hello siguientes notas de la versión describen características nuevas de hello e identifican problemas abiertos críticos de Hola de StorSimple 8000 Series Update 3. También contienen una lista de las actualizaciones de software de StorSimple Hola incluidos en esta versión. 

La actualización 3 puede ser dispositivo de StorSimple de tooany aplicado ejecutando la versión (GA) o actualización 0,1 a través de 2.2 de actualización. versión del dispositivo Hola asociado con Update 3 es 6.3.9600.17759.

Revise información Hola contenida en la versión de Hola notas antes de implementar Hola actualización de la solución StorSimple.

> [!IMPORTANT]
> * Update 3 incluye actualizaciones de software de dispositivo, controlador LSI y firmware, Storport y Spaceport. Tarda aproximadamente 1,5 a 2 horas tooinstall esta actualización. 
> * Para cada versión nueva, quizás no pueda ver las actualizaciones inmediatamente porque se realiza una implementación por fases de actualizaciones de Hola. Espere unos días y luego busque actualizaciones de nuevo ya que estas estarán disponibles pronto.
> 
> 

## <a name="whats-new-in-update-3"></a>Novedades de Update 3
Hello siguientes claves mejoras y correcciones de errores se realizaron en Update 3.

* **Automatizar los cambios de recuperación de espacio** : a partir de Update 3, algoritmos de recuperación de espacio de hello ejecutan en el controlador en espera de hello del sistema Hola resultante en una ejecución más rápida. Para obtener más información sobre puertos hello toowork necesaria con la recuperación de espacio, consulte toohello [StorSimple requisitos de red](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
* **Mejoras de rendimiento** – actualización 3 ha mejorado el rendimiento de lectura y escritura toohello en la nube.
* **Mejoras relacionadas con la migración** : en esta versión, varias correcciones de errores y mejoras realizadas para la característica de migración de Hola desde dispositivos de la serie 5000 o 7000 serie dispositivos too8000. Para obtener más información sobre cómo toouse Hola característica de migración, vaya demasiado[migración de dispositivo de la serie 5000 o 7000 serie dispositivo too8000](https://gallery.technet.microsoft.com/Azure-StorSimple-50007000-c1a0460b). 
* **Supervisión de correcciones relacionadas** : en esta versión, errores relacionados con gráficos toomonitoring, el panel de servicio y el panel del dispositivo se corrigieron.

## <a name="issues-fixed-in-update-3"></a>Problemas corregidos en Update 3
Hola las tablas siguientes proporciona un resumen de los problemas que se corrigieron en Update 3.    

| No | Característica | Problema | Se aplica a dispositivos toophysical | Se aplica a dispositivos toovirtual |
| --- | --- | --- | --- | --- |
| 1 |Migración de datos en el lado host |Hola versión anterior, Hola aparato de nube de StorSimple estaba trabajando sin conexión durante una migración de datos en el host. Este problema está corregido en esta versión. |No |Sí |
| 2 |Volúmenes anclados localmente |En la versión anterior de hello, hubo problemas relacionados tooI/O errores, errores de conversión de volumen y ruta de datos para volúmenes anclados localmente. Estos problemas eran la causa raíz y se han solucionado en esta versión. |Sí |No |
| 3 |Supervisión |Hay varios problemas relacionados tooreporting unidades y supervisión, así como gráficos de panel de dispositivos donde se muestra información incorrecta para localmente anclar volúmenes. Estos problemas se han corregido en esta versión. |Sí |No |
| 4 |E/S de escrituras pesadas |Al usar StorSimple para cargas de trabajo que implican escrituras pesadas, usuario Hola llevarían a cabo en un error poco frecuente donde se se mueven los espacio de trabajo de hello en nube Hola. Este error se ha corregido en esta versión. |Sí |Sí |
| 5 |Backup |En algunos casos poco frecuentes, en versiones anteriores de Hola de software, cuando el usuario realiza una copia de seguridad de un clon remoto, ejecutaría en errores en la nube y Hola operación sufriría un error. En esta versión, se soluciona el problema de Hola y Hola operación se completa correctamente. |Sí |Sí |
| 6 |Directiva de copia de seguridad |En algunos casos poco frecuentes, Hola las versiones anteriores del software, se produjo un error relacionado con la eliminación de toohello de directiva de copia de seguridad. Este problema está corregido en esta versión. |Sí |Sí |

## <a name="known-issues-in-update-3"></a>Problemas conocidos de Update 3
Hello en la tabla siguiente proporciona un resumen de los problemas conocidos de esta versión.

| No. | Característica | Problema | Comentarios / solución alternativa | Se aplica a dispositivos toophysical | Se aplica a dispositivos toovirtual |
| --- | --- | --- | --- | --- | --- |
| 1 |Cuórum de disco |En raras ocasiones, si la mayoría de Hola de discos del alojamiento EBOD Hola de un dispositivo 8600 se desconecta y no hay quórum de disco, a continuación, grupo de almacenamiento de Hola se desconectará. Incluso si se vuelven a conectar discos Hola permanecerá sin conexión. |Necesitará tooreboot dispositivo de Hola. Si persiste el problema de hello, póngase en contacto con Microsoft Support para los pasos siguientes. |Sí |No |
| 2 |Identificador de controlador incorrecto |Cuando se realiza un reemplazo de controlador, el controlador 0 puede aparecer como controlador 1. Durante el reemplazo de controlador, cuando se carga la imagen de Hola desde el nodo del mismo nivel de hello, identificador de la controladora de hello puede mostrarse inicialmente como Id.. del controlador de hello del mismo nivel En raras ocasiones, este comportamiento también puede aparecer después del reinicio del sistema. |No se requiere ninguna acción del usuario. Esta situación se solucionará automáticamente una vez completada la sustitución del controlador Hola. |Sí |No |
| 3 |Cuentas de almacenamiento |Usar cuenta de almacenamiento de hello almacenamiento servicio toodelete hello es un escenario no compatible. Esto daría lugar situación tooa en el que no se puede recuperar datos de usuario. | |Sí |Sí |
| 4 |Conmutación por error del dispositivo |Varias conmutaciones por error de un contenedor de volumen de hello no se admite los mismos dispositivos de destino de toodifferent de dispositivo de origen. Conmutación por error de una única cola de dispositivos toomultiple dispositivos hará que los contenedores de volúmenes de hello en hello primero conmutado por dispositivo pierda la propiedad de los datos. Después de este tipo una conmutación por error, estos contenedores de volumen aparecerán o se comportan de forma diferente cuando se visualizan en hello portal de Azure clásico. | |Sí |No |
| 5 |Instalación |Durante el adaptador de StorSimple para la instalación de SharePoint, debe tooprovide una dirección IP de dispositivo en orden para hello install toofinish correctamente. | |Sí |No |
| 6 |Proxy web |Si la configuración del proxy web tiene HTTPS como Hola especifica protocolo, afectará a la comunicación de servicio de dispositivos y dispositivos de Hola se desconectará. Paquetes de compatibilidad también se generarán en el proceso de hello, que consumen muchos recursos en el dispositivo. |Asegúrese de que Hola URL de proxy web tenga HTTP como Hola protocolo especificado. Para obtener más información, consulte demasiado[configurar el proxy web para el dispositivo](storsimple-configure-web-proxy.md). |Sí |No |
| 7 |Proxy web |Si configura y habilitar el proxy web en un dispositivo registrado, deberá controlador activo de toorestart hello en el dispositivo. | |Sí |No |
| 8 |Latencia alta de la nube y alta carga de trabajo de E/S |Cuando el dispositivo de StorSimple encuentra una combinación de latencias de nube muy altas (orden de segundos) y la carga de trabajo de E/S alta, volúmenes del dispositivo Hola pasan a un estado degradado y Hola operaciones de E/s se puede producir un error "el dispositivo no está listo". |Se necesitan controladores de dispositivo de toomanually reinicio Hola o realizar una toorecover de conmutación por error de dispositivo de esta situación. |Sí |No |
| 9 |Azure PowerShell |Cuando usas hello StorSimple cmdlet **Get AzureStorSimpleStorageAccountCredential &#124; Select-Object - primero 1 - espera** tooselect Hola primer objeto para que pueda crear un nuevo **VolumeContainer** objeto Hola cmdlet devuelve todos los objetos de Hola. |Ajustar Hola cmdlet entre paréntesis, como se indica a continuación: **(Get-Azure-StorSimpleStorageAccountCredential) &#124; Select-Object - primero 1 - espera** |Sí |Sí |
| 10 |Migración |Cuando se pasan varios contenedores de volúmenes para la migración, es preciso solo para el primer contenedor de volumen Hola Hola ETA para copia de seguridad más reciente. Además, migración paralela se iniciará después de hello 4 primeras copias de seguridad en el primer contenedor de volumen Hola se migran. |Se recomienda migrar los contenedores de volúmenes de uno en uno. |Sí |No |
| 11 |Migración |Después de la restauración de hello, volúmenes no se agregan toohello copia de seguridad Hola o directiva de grupo de disco virtual. |Necesitará tooadd estos directiva de copia de seguridad de volúmenes tooa en las copias de seguridad toocreate de orden. |Sí |Sí |
| 12 |Migración |Una vez completada la migración de hello, no debe tener acceso dispositivo de la serie 5000 o 7000 Hola Hola migra contenedores de datos. |Se recomienda que elimine Hola migrar contenedores de datos una vez Hola migración completa y confirmada. |Sí |No |
| 13 |Clonación y recuperación ante desastres |Un dispositivo de StorSimple con Update 1 no puede clonar ni realizar dispositivo de tooa de recuperación ante desastres con 1 de anteriores a la actualización software. |Necesitará tooupdate Hola destino dispositivo tooUpdate 1 tooallow estas operaciones |Sí |Sí |
| 14 |Migración |En los dispositivos de las series 5000-7000, se puede producir un error en la copia de seguridad de la configuración para la migración cuando haya grupos de volúmenes sin volúmenes asociados. |Elimine todos los grupos de volúmenes vacíos Hola con ningún volúmenes asociados y, a continuación, vuelva a intentar la copia de seguridad de configuración de Hola. |Sí |No |
| 15 |Cmdlets de Azure PowerShell y volúmenes anclados localmente |No se puede crear un volumen anclado localmente mediante los cmdlets de Azure PowerShell. (Se puede almacenar en capas cualquier volumen creado con Azure PowerShell). |Utilice siempre volúmenes de hello StorSimple Manager servicio tooconfigure anclado localmente. |Sí |No |
| 16 |Espacio disponible para los volúmenes anclados localmente |Si elimina un volumen anclado localmente, puede que Hola espacio disponible para nuevos volúmenes no se actualiza inmediatamente. las actualizaciones del servicio de administrador de StorSimple de Hola Hola espacio local disponible aproximadamente cada hora. |Espere una hora antes de probar el nuevo volumen de toocreate Hola. |Sí |No |
| 17 |Volúmenes anclados localmente |El trabajo de restauración expone la copia de seguridad de instantánea temporal de Hola Hola catálogo de copia de seguridad, pero solo durante Hola de trabajo de restauración de Hola. Además, expone un grupo de discos virtuales con prefijo **tmpCollection** en hello **directivas de copia de seguridad** página, pero solo dure Hola Hola el trabajo de restauración. |Este comportamiento puede producirse si el trabajo de restauración ha anclado solo localmente volúmenes o una mezcla de volúmenes nivelados y anclados localmente. Si el trabajo de restauración de hello incluye solo los volúmenes en capas, este comportamiento no se producirá. No se requiere ninguna intervención del usuario. |Sí |No |
| 18 |Volúmenes anclados localmente |Si se cancela un trabajo de restauración y se produce una conmutación por error de controlador inmediatamente después, se mostrará el trabajo de restauración de hello **error** en lugar de **Canceled**. Si se produce un error en un trabajo de restauración y se produce una conmutación por error de controlador inmediatamente después, se mostrará el trabajo de restauración de hello **Canceled** en lugar de **error**. |Este comportamiento puede producirse si el trabajo de restauración ha anclado solo localmente volúmenes o una mezcla de volúmenes nivelados y anclados localmente. Si el trabajo de restauración de hello incluye solo los volúmenes en capas, este comportamiento no se producirá. No se requiere ninguna intervención del usuario. |Sí |No |
| 19 |Volúmenes anclados localmente |Si se cancela un trabajo de restauración o si se produce un error en una restauración y, a continuación, se produce una conmutación por error de controlador, aparece un trabajo de restauración adicionales en hello **trabajos** página. |Este comportamiento puede producirse si el trabajo de restauración ha anclado solo localmente volúmenes o una mezcla de volúmenes nivelados y anclados localmente. Si el trabajo de restauración de hello incluye solo los volúmenes en capas, este comportamiento no se producirá. No se requiere ninguna intervención del usuario. |Sí |No |
| 20 | |Volúmenes anclados localmente |Si trata de un volumen en capas (creado y clonado con actualización 1.2 o anterior) de tooconvert tooa localmente había anclado volumen y el dispositivo se está quedando sin espacio o una interrupción en la nube, y hello clone(s) puede estar dañada. |Este problema solo se produce con los volúmenes que se crearon y clonaron con software anterior a la actualización 2.1. Este debería ser un escenario poco frecuente. | | |
| 21 |Conversión de volumen |No se actualizan Hola ACR tooa adjunto volumen mientras se realiza una conversión de un volumen (en capas toolocally anclado o viceversa). Actualizar Hola ACR podría provocar daños en los datos. |Si es necesario, actualice la conversión del volumen de hello ACR toohello anterior y no realizar ninguna ACR actualizaciones mientras se realiza la conversión de Hola. | | |
| 22 |Actualizaciones |Al aplicar la actualización 3, Hola **mantenimiento** página en hello Azure will portal clásico siguiente Hola de presentación de mensajes relacionado tooUpdate 2: "StorSimple 8000 series Update 2 incluye la capacidad de Hola para recopilar tooproactively de Microsoft registrar información del dispositivo cuando se detecten posibles problemas". Esto puede resultar confuso tal y como indica que ese dispositivo Hola está siendo actualizada tooUpdate 2. Una vez dispositivo hello succeesfully actualiza tooUpdate 3, este mensaje desaparece. |Este comportamiento se solucionará en futuras versiones. |yes |No |

## <a name="controller-and-firmware-updates-in-update-3"></a>Actualizaciones de firmware y de controlador en Update 3
Esta versión tiene actualizaciones de firmware y controlador LSI. Para obtener más información sobre cómo ver tooinstall Hola LSI actualizaciones de controladores y firmware, [instalar Update 3](storsimple-install-update-3.md) en el dispositivo StorSimple.

## <a name="virtual-device-updates-in-update-3"></a>Actualizaciones de dispositivo virtual en Update 3
Esta actualización no puede ser aplicada toohello dispositivo de StorSimple en la nube (también conocido como Hola dispositivo virtual). Nuevos dispositivos virtuales necesitará toobe creado. 

## <a name="next-step"></a>Paso siguiente
Obtenga información acerca de cómo demasiado[instalar Update 3](storsimple-install-update-3.md) en el dispositivo StorSimple.

