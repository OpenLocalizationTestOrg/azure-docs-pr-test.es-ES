---
title: "notas de la versión de aaaStorSimple 8000 Series Update 2.2 | Documentos de Microsoft"
description: "Describe nuevas características de hello, problemas y soluciones alternativas para StorSimple 8000 Series Update 2.2."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5cf03ea8-2a0f-4552-b6dc-7ea517783d7b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/18/2016
ms.author: alkohli
ms.openlocfilehash: a2902126f4011fa9ade64f63a8abdec095874fb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-22-release-notes"></a>Notas de la versión de la serie StorSimple 8000 Update 2.2
## <a name="overview"></a>Información general
Hello siguientes notas de la versión describen características nuevas de hello e identifican problemas abiertos críticos de Hola para StorSimple 8000 Series Update 2.2. También contienen una lista de las actualizaciones de software de StorSimple Hola incluidos en esta versión. 

Actualización 2.2 puede ser dispositivo de StorSimple tooany aplicado ejecutar versión (GA) o actualización 0,1 mediante Update 2.1. versión del dispositivo Hola asociado a la 2.2 de actualización es 6.3.9600.17708.

Revise información Hola contenida en la versión de Hola notas antes de implementar Hola actualización de la solución StorSimple.

> [!IMPORTANT]
> * Update 2.2 incluye únicamente actualizaciones del software. Tarda aproximadamente 1,5 a 2 horas tooinstall esta actualización. 
> * Si ejecuta Update 2.1, recomendamos que aplique Update 2.2 tan pronto como sea posible.
> * Para cada versión nueva, quizás no pueda ver las actualizaciones inmediatamente porque se realiza una implementación por fases de actualizaciones de Hola. Espere unos días y luego busque actualizaciones de nuevo ya que estas estarán disponibles pronto.
> 
> 

## <a name="whats-new-in-update-22"></a>Novedades de Update 2.2
Hello siguientes claves se han realizado mejoras en 2.2 de actualización.

* **Automatizar la optimización de recuperación de espacio** : cuando se eliminan los datos en volúmenes con aprovisionamiento fino, los bloques de almacenamiento sin usar hello deben toobe reclame. Esta versión tiene el proceso de recuperación de espacio de hello mejorada de nube Hola resultante en hello sin usar se están convirtiendo con mayor rapidez como comparados toohello versiones anteriores disponibles del espacio.
* **Mejoras de rendimiento de la instantánea** – actualización 2.2 tiene Hola mejorada tiempo tooprocess una instantánea en la nube en ciertos escenarios donde se utilizan grandes volúmenes y no hay renovación de datos mínimo toono. Un escenario que se beneficiaría de esta mejora sería volúmenes de almacenamiento de Hola.
* **Protección del paquete de soporte de recopilación** : se han realizado mejoras en forma de hello paquete de soporte de Hola se recopilan y se cargan en esta versión. 
* **Mejoras de la confiabilidad de Update** : esta versión contiene correcciones de errores que conllevan una mayor confiabilidad de Update.

## <a name="issues-fixed-in-update-22"></a>Problemas corregidos en Update 2.2
Hola las tablas siguientes proporciona un resumen de los problemas que se corrigieron en actualizaciones 2.2 y 2.1.    

| No | Característica | Problema | Se aplica a dispositivos toophysical | Se aplica a dispositivos toovirtual |
| --- | --- | --- | --- | --- |
| 1 |Rendimiento del host |Hola anteriormente de la versión, los problemas de rendimiento del lado del host se observaron durante la creación de hello de un volumen anclado localmente y durante la conversión de Hola de localmente un tooa de volumen en capas anclado el volumen. En esta versión, por tanto, lo que produce una mejora del rendimiento de host de Hola durante los procedimientos de creación y la conversión del volumen Hola haya solucionado estos problemas. |Sí |No |
| 2 |Volúmenes anclados localmente |En raras ocasiones, sistema de hello podría bloquearse al crear un volumen anclado localmente. Este error se ha corregido en esta versión. |Sí |No |
| 3 |Organización en niveles |Se produjeron bloqueos esporádicos cuando Hola metadatos para niveles de hello aparatos de nube de StorSimple (8010 y 8020) demasiado hello en la nube. Este problema está corregido en esta versión. |No |Sí |
| 4 |Creación de instantáneas |Se han producido problemas relacionados toohello creación de instantáneas incrementales en escenarios con grandes volúmenes y la renovación de datos mínimo toono. Estos problemas se han corregido en esta versión. |Sí |Sí |
| 5 |Autenticación de Openstack |Cuando se usa Openstack como proveedor de servicios de nube de hello, usuario Hola llevarían a cabo en una autenticación de toohello relacionados errores poco frecuentes en analizador JSON de hello dio como resultado un bloqueo. Este error se ha corregido en esta versión. |Sí |No |
| 6 |Copia del lado del host |En versiones anteriores del software, un error poco frecuente relacionadas con el control de tiempo de toohello ODX se vio cuando se copian datos de Hola de volumen de un volumen tooanother. Eso resultaría en una conmutación por error de controlador y sistema de hello potencialmente podría entrar en modo de recuperación. Este error se ha corregido en esta versión. |yes |No |
| 7 |Instrumental de administración de Windows (WMI) |En versiones anteriores de Hola de software, había varias instancias del error de proxy web con la excepción de Hola "<ManagementException> error del proveedor de carga". Este error fue fuga de memoria WMI tooa con atributos y se ha corregido. |Sí |No |
| 8 |Actualizar |En algunos casos poco frecuentes, en las versiones anteriores del software, Hola usuario Hola recibió un "CisPowershellHcsscripterror" al tratar de tooscan o instalar actualizaciones. Este problema está corregido en esta versión. |Sí |Sí |
| 9 |Paquete de soporte |En esta versión, se han realizado mejoras toohello forma paquete de soporte de Hola se recopilan y se cargan. |Sí |Sí |

## <a name="known-issues-in-update-22"></a>Problemas conocidos de Update 2.2
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

## <a name="controller-and-firmware-updates-in-update-22"></a>Actualizaciones de firmware y de controlador en Update 2.2
Esta versión incluye únicamente actualizaciones del software. Sin embargo, si está actualizando desde una tooUpdate anteriores de versión 2, necesitará tooinstall controlador Storport, Spaceport y (en algunos casos) las actualizaciones de firmware en el dispositivo de disco.

Para obtener más información sobre cómo ver controlador de hello tooinstall, Storport, Spaceport y actualizaciones de firmware de disco, [instalar actualización 2.2](storsimple-install-update-21.md) en el dispositivo StorSimple.

## <a name="virtual-device-updates-in-update-22"></a>Actualizaciones de dispositivo virtual en Update 2.2
Esta actualización no puede ser el dispositivo virtual toohello aplicada. Nuevos dispositivos virtuales necesitará toobe creado. 

## <a name="next-step"></a>Paso siguiente
Obtenga información acerca de cómo demasiado[instalar actualización 2.2](storsimple-install-update-21.md) en el dispositivo StorSimple.

