---
title: "aaaStorSimple 8000 Update 0.1 notas de la versión | Documentos de Microsoft"
description: "Describe nuevas características de Hola y correcciones, incidencias abiertas y soluciones alternativas disponibles para hello octubre de 2014 (actualización 0,1) de lanzamiento de Microsoft Azure StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: fd35e3c3-4770-460c-999d-f72ab7053a20
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 684e31cb0b356ec59a9d6c245e5d2bc062cc4f0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-01-release-notes--october-2014"></a>Notas de la versión 0.1 de la actualización de la serie StorSimple 8000: octubre de 2014
## <a name="overview"></a>Información general
Hola siguientes notas de la versión identifica temas Hola críticos de StorSimple 8000 Series Update 0.1 publicada en octubre de 2014. También contienen una lista de software de StorSimple de Hola y actualizaciones de firmware incluidas en esta versión. Esto es Hola primera versión después de versión de la versión de StorSimple 8000 Series Hola se ponerse a disposición general en julio de 2014 y corresponde toosoftware versión 6.3.9600.17312.  

Se recomienda buscar y aplicar las actualizaciones disponibles inmediatamente después de instalar el dispositivo de Hola. También puede activar toodownload de actualizaciones automáticas e instalar actualizaciones de alta prioridad de Microsoft en cuanto se publican. Para obtener más información, vea cómo demasiado[actualizar el dispositivo de StorSimple](storsimple-update-device.md).  

Revise información Hola contenida en las notas de la versión de Hola antes de implementar las actualizaciones de hello de la solución StorSimple.  

> [!IMPORTANT]
> * Usar el servicio StorSimple Manager hello y no de Windows PowerShell para StorSimple tooinstall hello que las actualizaciones de octubre.  
> * Hola actualizaciones suelen tardar aproximadamente 3 toocomplete horas.  
> * Hello versión de octubre de StorSimple no contiene ningún dispositivo virtual de las actualizaciones toohello StorSimple. Puede aplicar las actualizaciones de Windows disponibles, incluidas las revisiones de seguridad, pero no verá un cambio en la versión del dispositivo virtual Hola.  
> 
> 

Asegúrese de Hola seguro después de los requisitos previos es cumpla tooupdating anterior en el dispositivo StorSimple.  

* Asegúrese de que ambos controladores de dispositivo se están ejecutando antes de buscar actualizaciones. Si no se está ejecutando cualquier controlador, se producirá un error de análisis de Hola. tooverify que son controladores de hello en un estado correcto, navegue demasiado**estado del Hardware** en hello **mantenimiento** página. Si algún componente **Requiere atención**, póngase en contacto con el soporte técnico de Microsoft antes de continuar.  
* Asegúrese de que direcciones IP fijas de los controladores 0 y 1 son enrutables y pueden conectarse toohello Internet ya que se utilizan para dar servicio a dispositivos de hello actualizaciones toohello. Puede usar hello [cmdlet Test-Connection](https://technet.microsoft.com/library/hh849808.aspx) tooping una dirección conocida fuera de la red de hello, como outlook.com, tooverify que Hola controlador tiene conectividad toohello fuera de la red.  
* Asegúrese de que Hola requiere los puertos de salida están disponibles en el dispositivo de StorSimple para la comunicación saliente. Para obtener más información, vea hello [requisitos de red para el dispositivo StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).  
* Si la versión del software de dispositivo de hello es anterior a 6.3.9600.17312 (actualización de octubre de 2014), deshabilitar puertos Data 2 y Data 3 de hello, si está habilitada, antes de iniciar la actualización de Hola. Si deja Hola Data 2 o 3 datos puertos están habilitados cuando se aplica la actualización de hello, es posible que su toogo de controlador de dispositivo en modo de recuperación. Tenga en cuenta que al deshabilitar las interfaces de red de hello, todos los volúmenes de hello asociado se desconectarán y Hola E/S se interrumpirán durante Hola de actualización de Hola.  

## <a name="whats-new-in-hello-october-release"></a>Novedades de la versión de octubre de Hola
Esta actualización incluye Hola siguientes mejoras:

* Ahora puede usar toomanage de interfaz de usuario de servicio de StorSimple Manager Hola los controladores del dispositivo. administración de Hello acciones incluyen reiniciar, apagar, o activar un controlador. Para obtener más información, consulte demasiado[StorSimple administrar controladores de dispositivo](storsimple-manage-device-controller.md).  
* Puede programar la asignación de ancho de banda WAN según combinaciones tooday de la semana y hora del día. Esto le permite toomake un mejor uso del ancho de banda WAN durante las horas. Se admiten plantillas diferentes de ancho de banda para distintos contenedores de volúmenes. Para obtener más información, consulte demasiado[administrar sus plantillas de ancho de banda de StorSimple](storsimple-manage-bandwidth-templates.md).  
* Puede configurar notificaciones de correo electrónico tooproactively notificar a los administradores de Hola y a otros usuarios de los problemas existentes o futuros posiblemente. Para obtener más información, consulte demasiado[configurar opciones de alertas](storsimple-manage-alerts.md#configure-alert-settings).  

## <a name="issues-fixed-in-hello-october-release"></a>Problemas corregidos en la versión de octubre de Hola
Hello tabla siguiente proporciona un resumen de los problemas que se corrigieron en esta actualización.  

| No. | Característica | Problema | Se aplica a dispositivos toophysical | Se aplica a dispositivos toovirtual |
| --- | --- | --- | --- | --- |
| 1 |Interfaces de red |Hola anterior de la versión, interfaces de red de hello DATA 2 y DATA 3 se cambiaron en el software de Hola. Esto se corrigió en esta actualización. Por favor, borrar la configuración de Hola y deshabilite estas interfaces de red antes de instalar la actualización de Hola. Después de instalar la actualización de hello, tendrá tooreconfigure estas interfaces. |Sí |No |
| 2 |Paquete de soporte |En versión anterior de hello, si ha ejecutado Hola Windows PowerShell **Export-HcsSupportPackage** cmdlet tooretrieve Hola controlador de administración de placa base (BMC) inicia una sesión, la operación Hola Hola siguiente advertencia: "¡hello operación correcta en este controlador, pero no en el controlador del mismo nivel de hello debido toohello siguiente errores. Compruebe si el nivel de hello es correcto y si Hola actual nodo puede conectar toohello del mismo nivel." Este problema está corregido. |Sí |No |
| 3 |Conmutación por error del dispositivo |En la versión anterior de hello, hubo una posibilidad de incoherencia en los datos si un **detectar copia de seguridad** error del trabajo durante una conmutación por error de dispositivo. Este problema está corregido. |Sí |No |
| 4 |Conmutación por error del dispositivo |Hola anterior de la versión, después de una conmutación por error de dispositivo, las copias de seguridad estaban visibles, pero contenedor de volúmenes asociado hello no estaba presente en el dispositivo de destino de Hola. Este problema está corregido. |Sí |No |
| 5 |Conmutación por error del dispositivo |En la versión anterior de hello, hubo un error de enumeración de Hola de copias de seguridad en la nube durante la operación de restauración del registro de hello que podría dañar toodata incoherencia si había problemas de conectividad a en la nube. |Sí |No |
| 6 |Actualización de firmware |En la versión anterior de hello, hello trabajo de actualización de firmware de dispositivo no se pudo y muestra un error que afirmaba que Hola cmdlets no eran reconocibles, y esa actualización Hola error como resultado. controlador de Hello entraba en modo de recuperación. Este problema está corregido. |Sí |No |
| 7 |Instalación |Ahora se han corregido errores causados por dispositivo de hello no se digitalizaba correctamente durante la instalación. |Sí |No |
| 8 |Restablecimiento de fábrica |Ahora puede omitir comprobación de firmware de hello para el restablecimiento de fábrica. Se trata de un cambio de versión anterior de Hola. |Sí |No |
| 9 |Restablecimiento de fábrica |En la versión anterior de hello, cuando se ejecuta un cmdlet de restablecimiento de fábrica, comprobaciones de versión del firmware solo se realizaban para algunos componentes de hardware. Comprobaciones de firmware adicionales efectuadas con posterioridad Hola reiniciar por primera vez en el proceso de hello, lo que puede provocar toofail de restablecimiento de Hola. Esta revisión garantiza que todas las comprobaciones de firmware de Hola se realizan cuando se ejecuta el cmdlet de restablecimiento de fábrica de Hola y antes de hello primer sistema reiniciará. |Sí |No |
| 10 |Rotación de claves de cuentas de almacenamiento |Hola **Invoke-HcsmServiceDataEncryptionKeyChange** cmdlet usa claves de cuenta de almacenamiento de toorotate Hola ahora mensajes de Hola clave de cifrado de datos de usuario tooenter Hola servicio. Se trata de un cambio de versión anterior de hello en qué Hola clave de cifrado de datos de servicio se ha pasado como un parámetro en línea. |Sí |No |
| 11 |Conmutación por recuperación en 24 horas |Durante la recuperación ante desastres, limpieza de hello en dispositivo de origen de hello no produjera toofail de conmutación por recuperación correcta, con lo que ha provocado. Esto se corrigió en esta versión. |Sí |No |

## <a name="known-issues-in-hello-october-release"></a>Problemas conocidos de la versión de octubre de Hola
Hello en la tabla siguiente proporciona un resumen de los problemas conocidos de esta versión.

| No. | Característica | Problema | Comentarios/solución alternativa | Se aplica a dispositivos toophysical | Se aplica a dispositivos toovirtual |
| --- | --- | --- | --- | --- | --- |
| 1 |Restablecimiento de fábrica |En algunos casos, cuando se realiza un restablecimiento de fábrica, Hola dispositivo StorSimple puede bloquearse y mostrar este mensaje: **toofactory restablecimiento está en curso (fase 8)**. Esto sucede si presiona CTRL + C mientras Hola cmdlet está en curso. |No presione CTRL+C después de iniciar un restablecimiento de fábrica. Si ya está en este estado, póngase en contacto con el soporte técnico de Microsoft para conocer los pasos siguientes. |Sí |No |
| 2 |Restablecimiento de fábrica |Realizar el restablecimiento de fábrica no un dispositivo de StorSimple que se actualiza desde la versión de GA tooOctober 2014. |Esta operación solo funcionará si se instala una revisión. Póngase en contacto con Microsoft Support tooget la revisión necesaria. |Sí |No |
| 3 |Cuórum de disco |En raras ocasiones, si la mayoría de Hola de discos del alojamiento EBOD Hola de un dispositivo 8600 se desconecta y no hay quórum de disco, a continuación, grupo de almacenamiento de hello estarán sin conexión. Incluso si se vuelven a conectar discos Hola permanecerá sin conexión. |Necesitará tooreboot dispositivo de Hola. Si persiste el problema de hello, póngase en contacto con Microsoft Support para los pasos siguientes. |Sí |No |
| 4 |Errores de instantánea en la nube |En raras ocasiones, puede producir un error de una instantánea en la nube con error de hello **ha alcanzado el límite de copia de seguridad de máximo**. Esto ocurre si excede 255 clones en línea en hello mismo dispositivo, de hello mismo volumen original que se ha eliminado. | |Sí |Sí |
| 5 |Identificador de controlador incorrecto |Cuando se realiza un reemplazo de controlador, el controlador 0 puede aparecer como controlador 1. Durante el reemplazo de controlador, cuando se carga la imagen de Hola desde el nodo del mismo nivel de hello, identificador de la controladora de hello puede mostrarse inicialmente como Id.. del controlador de hello del mismo nivel En raras ocasiones, este comportamiento también puede aparecer después del reinicio del sistema. |No se requiere ninguna acción del usuario. Esta situación se solucionará automáticamente una vez completada la sustitución del controlador Hola. |Sí |No |
| 6 |Gráficos de supervisión de dispositivos |En el servicio StorSimple Manager hello, gráficos de supervisión de dispositivos de hello no funcionan cuando básica o la autenticación NTLM está habilitada en la configuración de servidor proxy de hello de dispositivo de Hola. |Modificar configuración de proxy web de Hola para dispositivo Hola registrado con el servicio StorSimple Manager para que la autenticación se establece tooNONE. toodo, Hola Hola ejecución Windows PowerShell para el cmdlet Set-HcsWebProxy de StorSimple. |Sí |Sí |
| 7 |Cuentas de almacenamiento |Usar cuenta de almacenamiento de hello almacenamiento servicio toodelete hello es un escenario no compatible. Esto daría lugar situación tooa en el que no se puede recuperar datos de usuario. | |Sí |Sí |
| 8 |Conmutación por error del dispositivo |Varias conmutaciones por error de un contenedor de volumen de hello no se admite los mismos dispositivos de destino de toodifferent de dispositivo de origen. |Conmutación por error de una única cola de dispositivos toomultiple dispositivos hará que los contenedores de volúmenes de hello en hello primero conmutado por dispositivo pierda la propiedad de los datos. Después de este tipo una conmutación por error, estos contenedores de volumen aparecerán o se comportan de forma diferente cuando se visualizan en hello portal de Azure clásico. |Sí |No |
| 9 |Instalación |Durante el adaptador de StorSimple para la instalación de SharePoint, debe tooprovide una dirección IP de dispositivo en orden para hello install toofinish correctamente. | |Sí |No |
| 10 |Proxy web |Si la configuración del proxy web tiene HTTPS como Hola especifica protocolo, afectará a la comunicación de servicio de dispositivos y dispositivos de Hola se desconectará. Paquetes de compatibilidad también se generarán en el proceso de hello, que consumen muchos recursos en el dispositivo. |Asegúrese de que Hola URL de proxy web tenga HTTP como Hola protocolo especificado. Para obtener más información acerca de cómo demasiado[configurar el proxy web para el dispositivo](storsimple-configure-web-proxy.md). |Sí |No |
| 11 |Proxy web |Si configura y habilitar el proxy web en un dispositivo registrado, deberá controlador activo de toorestart hello en el dispositivo. | |Sí |No |
| 12 |Latencia alta de la nube y alta carga de trabajo de E/S |Cuando el dispositivo de StorSimple encuentra una combinación de latencias de nube muy altas (orden de segundos) y la carga de trabajo de E/S alta, volúmenes del dispositivo Hola pasan a un estado degradado y Hola operaciones de E/s se puede producir un error "el dispositivo no está listo". |Se necesitan controladores de dispositivo de toomanually reinicio Hola o realizar una toorecover de conmutación por error de dispositivo de esta situación. |Sí |No |

## <a name="physical-device-updates-in-hello-october-release"></a>Actualizaciones de dispositivo físico en la versión de octubre de Hola
Cuando estas actualizaciones estén dispositivo físico tooa aplicado, versión de software de hello cambiará too6.3.9600.17312. A menos que se especifique lo contrario, estas notas de la versión tooall modelos de dispositivo de StorSimple de Hola se aplican. Para obtener más información sobre estas actualizaciones, consulte [Actualización de software del dispositivo físico de octubre de 2014 para el dispositivo de Microsoft Azure StorSimple](http://support.microsoft.com/kb/2986997).  

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-october-release"></a>Conectado en serie SCSI (SAS) controlador y actualizaciones de firmware en la versión de octubre de Hola
Esta versión actualiza el controlador de Hola y Hola firmware controlador SAS de hello de dispositivo físico. Para obtener más información acerca de la actualización del controlador SAS hello, consulte [actualización de octubre de 2014 para controladores SAS LSI del dispositivo de StorSimple de Microsoft Azure](http://support.microsoft.com/kb/2987020).   

Esta versión también aplica una actualización de firmware acumulativa que trata los problemas de confiabilidad con componentes de hardware de dispositivo de Hola. Para obtener más información acerca de la actualización de firmware de hello, consulte [actualización de firmware de octubre de 2014 para Microsoft Azure StorSimple Appliance](http://support.microsoft.com/kb/2987015).  

## <a name="virtual-device-updates-in-hello-october-release"></a>Actualizaciones de dispositivo virtual en la versión de octubre de Hola
Esta versión no contiene ninguna actualización para dispositivo virtual Hola. Aplicar esta actualización no cambiará la versión de software de Hola de un dispositivo virtual.

