---
title: "notas de la versión de aaaStorSimple 8000 Series Update 2 | Documentos de Microsoft"
description: "Describe nuevas características de hello, problemas y soluciones alternativas de StorSimple 8000 Series Update 2."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: e2c8bffd-7fc5-4b77-b632-a4f59edacc3a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 36c75aad900c7b1286a924732967b8ee519a3d4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-2-release-notes"></a>Notas de la versión de la actualización 2 de la serie StorSimple 8000
## <a name="overview"></a>Información general
Hello siguientes notas de la versión describen características nuevas de hello e identifican problemas abiertos críticos de Hola de StorSimple 8000 Series Update 2. También contienen una lista de software de StorSimple de hello, controladores y actualizaciones de firmware de disco incluidas en esta versión. 

Actualización 2 puede ser dispositivo de StorSimple tooany aplicado ejecutando versión (GA) o actualización 0,1 a través de la actualización 1.2. versión del dispositivo Hola asociado con la actualización 2 es 6.3.9600.17673.

Revise información Hola contenida en la versión de Hola notas antes de implementar Hola actualización de la solución StorSimple.

> [!IMPORTANT]
> * Tarda aproximadamente 4-7 horas tooinstall esta actualización (incluidas las actualizaciones de Windows de hello). 
> * La actualización 2 tiene actualizaciones de software, controlador LSI y firmware de SSD.
> * Para cada versión nueva, quizás no pueda ver las actualizaciones inmediatamente porque se realiza una implementación por fases de actualizaciones de Hola. Espere unos días y luego busque actualizaciones de nuevo ya que estas estarán disponibles pronto.
> 
> 

## <a name="whats-new-in-update-2"></a>Novedades de la actualización 2
Actualización 2 introduce Hola siguientes nuevas funciones.

* **Anclado localmente volúmenes** : en las versiones anteriores de la serie StorSimple 8000 hello, bloques de datos eran toohello en capas en la nube basada en uso. Se ha producido ningún tooguarantee de manera que quedaría bloques en el equipo local. En Update 2, cuando se crea un volumen, puede designar un volumen como datos de ese volumen anclados localmente y principales no estará toohello en capas en la nube. Las instantáneas de volúmenes anclados localmente estarán copia toohello en la nube para copia de seguridad de modo que en la nube Hola puede usarse para fines de recuperación ante desastres y la movilidad de datos. Además, puede cambiar el tipo de volumen hello (es decir, convertir volúmenes de volúmenes en capas toolocally anclado y convert localmente anclado tootiered de volúmenes). 
* **Mejoras de dispositivo virtual StorSimple** : anteriormente, Hola serie StorSimple 8000 coloca el dispositivo virtual hello como una solución de desarrollo y pruebas o de recuperación ante desastres. Solo había un modelo de dispositivo virtual (modelo 1100). La actualización 2 presenta dos modelos de dispositivo virtual: 
  
  * 8010 (anteriormente llamado Hola 1100) – sin cambios; tiene una capacidad de 30 TB y usa el almacenamiento de Azure estándar.
  * 8020: tiene una capacidad de 64 TB y usa el almacenamiento premium de Azure para mejorar el rendimiento.
    
    Hay un solo VHD para ambos modelos de dispositivo virtual (8010/8020). Cuando se inicia por primera vez dispositivo virtual hello, detecta los parámetros de la plataforma de Hola y aplica la versión de Hola modelo correcto.
* **Mejoras de red** – Update 2 contiene Hola después mejoras de red:
  
  * Varias NIC pueden habilitarse para la nube de Hola para que la conmutación por error puede producirse si se produce un error en una NIC.
  * Mejoras de enrutamiento con métricas fijas para bloques habilitados para la nube.
  * Reintento en línea de recursos con errores antes de una conmutación por error.
  * Nuevas alertas para errores de servicio.
* **Mejoras de la actualización** : en actualizar 1.2 y versiones anteriores, serie StorSimple 8000 Hola se actualizó a través de dos canales: actualización de Windows para Microsoft Update para los archivos binarios y firmware, agrupación en clústeres, iSCSI y así sucesivamente.
    La actualización 2 usa Microsoft Update para todos los paquetes de actualizaciones. Esto debería plazo que no requiere herramientas aplicación de revisiones o bien las conmutaciones por error. 
* **Las actualizaciones de firmware** : hello después de firmware se incluyen las actualizaciones:
  
  * LSI: versión del producto 2.00.72.10 lsi_sas2.sys
  * SSD solo (ninguna actualización de la unidad de disco duro): XMGG, XGEG, KZ50, F6C2 y VR08
* **Soporte proactivo** – Update 2 permite que Microsoft toopull información de diagnóstico adicional desde dispositivo Hola. Cuando el equipo de operaciones identifica los dispositivos que están experimentando problemas, estamos mejor equipada toocollect información de hello dispositivo y diagnosticar problemas. **Si se acepta la actualización 2, nos permitirá tooprovide esta compatibilidad automático**.    

## <a name="issues-fixed-in-update-2"></a>Problemas corregidos en la actualización 2
Hola las tablas siguientes proporciona un resumen de problemas que se corrigieron en 2 de las actualizaciones.    

| No. | Característica | Problema | Se aplica a dispositivos toophysical | Se aplica a dispositivos toovirtual |
| --- | --- | --- | --- | --- |
| 1 |Interfaces de red |Después de una actualización tooUpdate 1, Hola el servicio StorSimple Manager informó de puertos de Data2 y Data3 Hola un error en un controlador. Ahora se ha corregido. |Sí |No |
| 2 |Actualizaciones |Después de una actualización tooUpdate 1, alertas de alarma audible produjo en hello portal de Azure clásico en varios dispositivos. Ahora se ha corregido. |Sí |No |
| 3 |Autenticación de Openstack |Al utilizar Openstack como proveedor de servicios en la nube, podría recibir un error que indica que la cadena de autenticación de la nube es demasiado larga. Esto se ha solucionado. |Sí |No |

## <a name="known-issues-in-update-2"></a>Problemas conocidos de la actualización 2
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
| 20 | |Volúmenes anclados localmente |Si trata de un volumen en capas (creado y clonado con actualización 1.2 o anterior) de tooconvert tooa localmente había anclado volumen y el dispositivo se está quedando sin espacio o una interrupción en la nube, y hello clone(s) puede estar dañada. |Este problema solo se produce con los volúmenes que se crearon y clonaron con software anterior a la actualización 2. Este debería ser un escenario poco frecuente. | | |
| 21 |Conversión de volumen |No se actualizan Hola ACR tooa adjunto volumen mientras se realiza una conversión de un volumen (en capas toolocally anclado o viceversa). Actualizar Hola ACR podría provocar daños en los datos. |Si es necesario, actualice la conversión del volumen de hello ACR toohello anterior y no realizar ninguna ACR actualizaciones mientras se realiza la conversión de Hola. | | |

## <a name="controller-and-firmware-updates-in-update-2"></a>Actualizaciones del firmware y del controlador en la actualización 2
Esta versión actualiza el controlador de Hola y de firmware de disco de hello en el dispositivo.

* Para obtener más información acerca de firmware de LSI Hola actualización, consulte el artículo de Microsoft Knowledge base 3121900. 
* Para obtener más información acerca de firmware del disco Hola actualización, consulte el artículo de Microsoft Knowledge base 3121899.

## <a name="virtual-device-updates-in-update-2"></a>Actualizaciones del dispositivo virtual en la actualización 2
Esta actualización no puede ser el dispositivo virtual toohello aplicada. Nuevos dispositivos virtuales necesitará toobe creado. 

## <a name="next-step"></a>Paso siguiente
Obtenga información acerca de cómo demasiado[instale actualización 2](storsimple-install-update-2.md) en el dispositivo StorSimple.

