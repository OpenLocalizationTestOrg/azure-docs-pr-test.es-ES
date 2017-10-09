---
title: "notas de la versión 1.2 de la actualización de serie 8000 aaaStorSimple | Documentos de Microsoft"
description: "Describe nuevas características de hello, problemas y soluciones alternativas para StorSimple 8000 Series Update 1.2."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6c9aae87-6f77-44b8-b7fa-ebbdc9d8517c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7f564b794573fc3302ab15732e8dd85632ab9243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="update-12-release-notes-for-your-storsimple-8000-series-device"></a>Actualización de las notas de la versión Update 1.2 del dispositivo StorSimple serie 8000

## <a name="overview"></a>Información general
Hello siguientes notas de la versión describen características nuevas de hello e identifican problemas abiertos críticos de hello StorSimple 8000 Series Update 1.2. También contienen una lista de software de StorSimple de hello, controladores y actualizaciones de firmware de disco incluidas en esta versión. 

Actualización 1.2 puede ser dispositivo de StorSimple tooany aplicado ejecutan versión (GA), actualización 0,1, actualización 0,2 o software Update 0.3. La actualización 1.2 no está disponible si el dispositivo ejecuta la actualización 1 o la actualización 1.1. Si su dispositivo ejecuta la versión (GA), inicie [póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md) tooassist que con la instalación de esta actualización.

Hola la siguiente tabla enumera Hola software versiones del dispositivo correspondiente tooUpdates 1, 1.1 y 1.2.

| Si ejecuta la actualización... | esta es su versión de software de dispositivo. |
| --- | --- |
| Actualización 1.2 |6.3.9600.17584 |
| Actualización 1.1 |6.3.9600.17521 |
| Actualización 1.0 |6.3.9600.17491 |

Revise información Hola contenida en la versión de Hola notas antes de implementar Hola actualización de la solución StorSimple. Para obtener más información, vea cómo demasiado[instalar actualización 1.2 en el dispositivo StorSimple](storsimple-install-update-1.md). 

> [!IMPORTANT]
> * Tarda aproximadamente entre 5 y 10 horas tooinstall esta actualización (incluidas las actualizaciones de Windows hello). 
> * La actualización 1.2 tiene actualizaciones de software, controlador LSI y firmware de disco. tooinstall, siga las instrucciones de hello en [instalar actualización 1.2 en el dispositivo StorSimple](storsimple-install-update-1.md).
> * Para cada versión nueva, quizás no pueda ver las actualizaciones inmediatamente porque se realiza una implementación por fases de actualizaciones de Hola. Busque actualizaciones de nuevo en unos días ya que estas estarán disponible pronto.
> 
> 

## <a name="whats-new-in-update-12"></a>Novedades de la actualización 1.2
Estas características se han publicado en primer lugar con Update 1 que se realizó tooa disponible limitado de conjunto de usuarios. Con la versión 1.2 de actualización de Hola, la mayoría de los usuarios de StorSimple de hello vería Hola siguientes mejoras y nuevas características:

* **Migración desde dispositivos de la serie 5000-7000 serie too8000** : esta versión introduce una nueva característica de migración que permite hello StorSimple 5000-7000 serie dispositivo usuarios toomigrate su dispositivo físico de datos tooa StorSimple 8000 series o un dispositivo virtual. característica de migración de Hello tiene dos propuestas de valor de clave:                                                                  
  
  * **Continuidad del negocio**, habilitando la migración de datos existentes en los equipos de la serie de 5000-7000 serie aparatos too8000.
  * **Mejorar las ofertas de la característica de equipos de la serie 8000 de hello**, como eficaz administración centralizada de varios dispositivos a través del servicio StorSimple Manager, clase de hardware y de mejor forma actualizar firmware, aparatos virtuales, movilidad de datos y características en el futuro de Hola.
    
    Consulte toohello [Guía de migración](http://www.microsoft.com/download/details.aspx?id=47322) para obtener más información acerca de cómo toomigrate un dispositivo de la serie StorSimple 5000-7000 serie tooan 8000. 
* **Disponibilidad de hello Portal de administración pública de Azure** – StorSimple ahora está disponible en el portal de Azure Government Hola. Vea cómo demasiado[implementar un dispositivo de StorSimple en hello Portal de administración pública de Azure](storsimple-deployment-walkthrough-gov.md).
* **Compatibilidad con otros proveedores de servicios de nube** : hello admitidas otros proveedores de servicios de nube son S3 de Amazon, Amazon S3 con registros de recursos, HP y OpenStack (beta).
* **Actualizar toolatest las API de almacenamiento** : con esta versión, ha sido StorSimple servicio de almacenamiento de Azure más reciente de toohello las API que se actualiza. Dispositivos de la serie 8000 de StorSimple que se ejecutan versiones de software anterior a Update 1 (versión, 0.1, 0.2 y 0.3) usan versiones de hello API del servicio de almacenamiento de Azure anteriores a 17 de julio de 2009. Como se indica en hello actualiza [anuncio acerca de la eliminación de versiones del servicio de almacenamiento](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx), mediante el 1 de agosto de 2016, dejará de utilizarse estas API. Es necesario que aplique hello StorSimple 8000 Series Update 1 anterior tooAugust 1, 2016. Si no toodo por lo tanto, los dispositivos de StorSimple dejará de funcionar correctamente.
* **Soporte para el almacenamiento de redundancia de zona (ZRS)** : con hello toohello actualización última versión del programa Hola a las API de almacenamiento, serie StorSimple 8000 Hola admitirá almacenamiento redundancia de zona (ZRS) en suma tooLocally almacenamiento redundante (LRS) y con redundancia geográfica Almacenamiento (GRS). Consulte toothis [artículo sobre las opciones de redundancia de almacenamiento de Azure](../storage/common/storage-redundancy.md) para obtener detalles ZRS.
* **Mejorado la experiencia de implementación y actualización inicial** : en esta versión, Hola instalación y se han mejorado los procesos de actualización. instalación de Hola a través del Asistente para la instalación de hello es usuario de toohello de comentarios de tooprovide mejorada si opciones de configuración y el firewall de red Hola son incorrectas. Cmdlets de diagnóstico adicionales se han proporcionado toohelp, con la solución de problemas de red del dispositivo de Hola. Vea hello [artículo de la implementación de la solución de problemas](storsimple-troubleshoot-deployment.md) para obtener más información acerca de los cmdlets de diagnóstico nuevo Hola utilizados para solucionar problemas.

## <a name="issues-fixed-in-update-12"></a>Problemas corregidos en la actualización 1.2
Hello en la tabla siguiente proporciona un resumen de los problemas que se corrigieron en actualizaciones de 1, 1.1 y 1.2.    

| No. | Característica | Problema | Se ha corregido en la actualización | Se aplica a dispositivos toophysical | Se aplica a dispositivos toovirtual |
| --- | --- | --- | --- | --- | --- |
| 1 |Windows PowerShell para StorSimple |Cuando un usuario acceso remoto a él de dispositivo de StorSimple de hello mediante Windows PowerShell para StorSimple y, a continuación, inicia el Asistente para la instalación de hello, se produjo en cuanto Data 0 IP se ha especificado un bloqueo. El error se ha corregido en la actualización 1. |Actualización 1 |Sí |Sí |
| 2 |Restablecimiento de fábrica |En algunos casos, cuando se lleva a cabo un restablecimiento de fábrica, el dispositivo StorSimple Hola pasara a ser bloqueado y muestra este mensaje: **toofactory restablecimiento está en curso (fase 8)**. Esto ha sucedido si presiona CTRL + C mientras Hola cmdlet estaba en curso. El error se ha corregido. |Actualización 1 |Sí |No |
| 3 |Restablecimiento de fábrica |Después de restablecer una fábrica de controlador doble con error, se permiten tooproceed al registro de dispositivos. Esto provocó una configuración no compatible del sistema. En la actualización 1, se muestra un mensaje de error y el registro se bloquea en los dispositivos en que se haya producido algún error al realizar un restablecimiento de fábrica. |Actualización 1 |Sí |No |
| 4 |Restablecimiento de fábrica |En algunos casos, se han generado alertas de discrepancia que son falsos positivos. Dejarán de generarse alertas de falta de coincidencia incorrectas en los dispositivos con la actualización 1. |Actualización 1 |Sí |No |
| 5 |Restablecimiento de fábrica |Si se interrumpe un restablecimiento de fábrica toocompletion anterior, Hola a modo de recuperación del dispositivo especificado y no permitió tooaccess Windows PowerShell para StorSimple. El error se ha corregido. |Actualización 1 |Sí |No |
| 6 |Recuperación ante desastres |Se corrigió un error de recuperación ante desastres donde DR produciría un error durante la detección de Hola de copias de seguridad en el dispositivo de destino de Hola. |Actualización 1 |Sí |Sí |
| 7 |LED de supervisión |En algunos casos, el LED de supervisión en hello parte posterior del dispositivo no haya indicado estado correcto. se ha desactivado el LED azul Hola. Los LED de DATA 0 y DATA 1 parpadeaban aun cuando las interfaces no se habían configurado. una vez solucionado el problema de Hola y LED de supervisión ahora indican el estado correcto de Hola. |Actualización 1 |Sí |No |
| 8 |LED de supervisión |En algunos casos, después de aplicar la actualización 1, luz de hello azul en el controlador activo Hola desactivada, por lo que el controlador de disco duro tooidentify Hola activo. Este problema se ha corregido en esta versión de revisión. |Actualización 1.2 |Sí |No |
| 9 |Interfaces de red |En las versiones anteriores, los dispositivos de StorSimple configurados con una puerta de enlace no enrutable podían quedarse sin conexión. En esta versión, métrica de enrutamiento de Hola para Data 0 se ha realizado hello más baja; por lo tanto, aunque otras interfaces de red están habilitada para la nube, todo el tráfico de nube hello de dispositivo de Hola se enrutará a través de Data 0. |Actualización 1 |Sí |Sí |
| 10 |Copias de seguridad |Un error en Update 1 que provocaron toofail de copias de seguridad después de haber corregido 24 días revisión hello de la versión 1.1 de actualización. |Actualización 1.1 |Sí |Sí |
| 11 |Copias de seguridad |Un error en las versiones anteriores tuvo como resultado un rendimiento deficiente de las instantáneas en la nube con frecuencias de cambio bajas. Este error se ha corregido en esta versión de revisión. |Actualización 1.2 |Sí |Sí |
| 12 |Actualizaciones |Un error en la actualización 1 informó de un error de actualización y provocase hello toogo de controladores en modo de recuperación, se ha corregido en esta versión de revisión. |Actualización 1.2 |Sí |Sí |

## <a name="known-issues-in-update-12"></a>Problemas conocidos de la actualización 1.2
Hello en la tabla siguiente proporciona un resumen de los problemas conocidos de esta versión.

| No. | Característica | Problema | Comentarios/solución alternativa | Se aplica a dispositivos toophysical | Se aplica a dispositivos toovirtual |
| --- | --- | --- | --- | --- | --- |
| 1 |Cuórum de disco |En raras ocasiones, si la mayoría de Hola de discos del alojamiento EBOD Hola de un dispositivo 8600 se desconecta y no hay quórum de disco, a continuación, grupo de almacenamiento de hello estarán sin conexión. Incluso si se vuelven a conectar discos Hola permanecerá sin conexión. |Necesitará tooreboot dispositivo de Hola. Si persiste el problema de hello, póngase en contacto con Microsoft Support para los pasos siguientes. |Sí |No |
| 2 |Identificador de controlador incorrecto |Cuando se realiza un reemplazo de controlador, el controlador 0 puede aparecer como controlador 1. Durante el reemplazo de controlador, cuando se carga la imagen de Hola desde el nodo del mismo nivel de hello, identificador de la controladora de hello puede mostrarse inicialmente como Id.. del controlador de hello del mismo nivel En raras ocasiones, este comportamiento también puede aparecer después del reinicio del sistema. |No se requiere ninguna acción del usuario. Esta situación se solucionará automáticamente una vez completada la sustitución del controlador Hola. |Sí |No |
| 3 |Cuentas de almacenamiento |Usar cuenta de almacenamiento de hello almacenamiento servicio toodelete hello es un escenario no compatible. Esto daría lugar situación tooa en el que no se puede recuperar datos de usuario. |Sí |Sí | |
| 4 |Conmutación por error del dispositivo |Varias conmutaciones por error de un contenedor de volumen de hello no se admite los mismos dispositivos de destino de toodifferent de dispositivo de origen. Conmutación por error de dispositivo de los dispositivos de toomultiple de un único dispositivo inactivo hará que los contenedores de volúmenes de hello en hello primero conmutado por dispositivo pierda la propiedad de los datos. Después de este tipo una conmutación por error, estos contenedores de volumen aparecerán o se comportan de forma diferente cuando se visualizan en hello portal de Azure clásico. | |Sí |No |
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

## <a name="physical-device-updates-in-update-12"></a>Actualizaciones del dispositivo físico en la actualización 1.2
Si revisión actualización 1.2 es el dispositivo físico de tooa aplicado (ejecutando versiones anteriores tooUpdate 1), versión de software de hello cambiará too6.3.9600.17584.

## <a name="controller-and-firmware-updates-in-update-12"></a>Actualizaciones de firmware y de controlador en Update 1.2
Esta versión actualiza el controlador de Hola y de firmware de disco de hello en el dispositivo.

* Para obtener más información acerca de la actualización del controlador SAS hello, consulte [Update 1 para controladores SAS LSI en Microsoft Azure StorSimple Appliance](https://support.microsoft.com/kb/3043005). 
* Para obtener más información acerca de la actualización de firmware de disco de hello, consulte [firmware del disco Update 1 para Microsoft Azure StorSimple Appliance](https://support.microsoft.com/kb/3063416).

## <a name="virtual-device-updates-in-update-12"></a>Actualizaciones de dispositivo virtual en la actualización 1.2
Esta actualización no puede ser el dispositivo virtual toohello aplicada. Nuevos dispositivos virtuales necesitará toobe creado. 

## <a name="next-steps"></a>Pasos siguientes
* [Instalación de la actualización 1.2 en el dispositivo](storsimple-install-update-1.md).

