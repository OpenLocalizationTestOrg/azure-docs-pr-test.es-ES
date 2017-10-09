---
title: "aaaStorSimple 8000 Update 0.3 notas de la versión | Documentos de Microsoft"
description: "Describe nuevas características de Hola y correcciones, incidencias abiertas y soluciones alternativas disponibles para hello febrero de 2015 (actualización 0.3) de lanzamiento de Microsoft Azure StorSimple."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: b01bfd04-f9f8-45f4-ade8-95ac2b979e6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: 53638f9d286b2085c6b45f9e3fae75c34fc73e7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-03-release-notes---february-2015"></a>Notas de la versión 0.3 de la actualización de la serie StorSimple 8000 - febrero de 2015
## <a name="overview"></a>Información general
Hola siguientes notas de la versión identifica temas Hola críticos de StorSimple 8000 Series Update 0.3 publicada en febrero de 2015. También contienen una lista de software de StorSimple de Hola y actualizaciones de firmware incluidas en esta versión. Esta es la versión terceros de hello después de versión de la versión de StorSimple 8000 Series Hola se ponerse a disposición general en julio de 2014.

Esta actualización no cambia la versión de software de dispositivo de Hola de actualización de enero de Hola. Continúa toobe versión 6.3.9600.17312. Puede confirmar actualización Hola se ha instalado mediante la comprobación de hello **de la última actualización** fecha. Si la fecha de hello es 2/10/2015 o posterior, actualización de Hola se ha instalado correctamente.  

Se recomienda buscar y aplicar las actualizaciones disponibles inmediatamente después de instalar el dispositivo StorSimple. También puede activar toodownload de actualizaciones automáticas e instalar actualizaciones de alta prioridad de Microsoft en cuanto se publican. Para obtener más información, consulte [Actualizar dispositivo StorSimple](storsimple-update-device.md).  

Revise información Hola contenida en la versión de Hola notas antes de implementar Hola actualización de la solución StorSimple.  

> [!IMPORTANT]
> * Usar el servicio StorSimple Manager hello y no de Windows PowerShell para la actualización de febrero de StorSimple tooinstall Hola.   
> * Tarda aproximadamente un tooinstall hora esta actualización. Sin embargo, si va a instalar actualizaciones acumulativas, proceso de hello puede tardar unos 3 toocomplete horas.  
> * Hello versión de febrero de StorSimple no contiene ningún dispositivo virtual de las actualizaciones toohello StorSimple. Puede aplicar cualquier dispositivo virtual de Windows actualizaciones toohello disponible, incluso de seguridad recientes correcciones, pero no verá un cambio en la versión del dispositivo virtual Hola.  
> 
> 

Asegúrese de que ese Hola siguientes requisitos previos está tooupdating anterior cumpla el dispositivo StorSimple.  

* Asegúrese de que ambos controladores de dispositivo se están ejecutando antes de buscar actualizaciones. Si no se está ejecutando cualquier controlador, se producirá un error de análisis de Hola. tooverify que son controladores de hello en un estado correcto, navegue demasiado**estado del Hardware** en hello **mantenimiento** página. Si algún componente **Requiere atención**, póngase en contacto con el soporte técnico de Microsoft antes de continuar.
* Asegúrese de que direcciones IP fijas de los controladores 0 y 1 son enrutable y pueden conectarse toohello Internet ya que se utilizan para dar servicio a dispositivos de hello actualizaciones toohello. Puede usar hello [cmdlet Test-Connection](https://technet.microsoft.com/library/hh849808.aspx) tooping una dirección conocida fuera de la red de hello, por ejemplo, outlook.com, tooverify que Hola controlador tiene conectividad toohello fuera de la red.
* Asegúrese de que los puertos 80 y 443 están disponibles en el dispositivo StorSimple para la comunicación saliente. Para obtener más información, vea hello [requisitos de red para el dispositivo StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
* Si la versión del software de dispositivo de hello es anterior a 6.3.9600.17312 (actualización de octubre de 2014), deshabilitar puertos Data 2 y Data 3 de hello, si está habilitada, antes de iniciar la actualización de Hola. Dejando los puertos están habilitados cuando se aplica la actualización de Hola Hola Data 2 o 3 de datos puede provocar la toogo del controlador de dispositivo en modo de recuperación. Tenga en cuenta que al deshabilitar las interfaces de red de hello, todos los volúmenes de hello asociado se desconectarán y Hola i/OS se interrumpirán durante Hola de actualización de Hola.  

## <a name="whats-new-in-hello-february-release"></a>Novedades de la versión de febrero de Hola
Esta actualización contiene una corrección para el problema de restablecimiento de fábrica de Hola que se ha producido en los dispositivos que se han actualizado desde la versión de Hola GA toohello versión de octubre de 2014. Para obtener más información, consulte [Problemas corregidos en esta versión](#issues-fixed-in-the-february-release).   

Esta actualización no contiene características o funcionalidades nuevas.  

## <a name="issues-fixed-in-hello-february-release"></a>Problemas corregidos en la versión de febrero de Hola
Hello siguiente tabla describe problema Hola que se corrigió en esta actualización.  

| No. | Característica | Problema | Se aplica a dispositivos toophysical | Se aplica a dispositivos toovirtual |
| --- | --- | --- | --- | --- |
| 1 |Restablecimiento de fábrica |Intente tooperform una restablecimiento de fábrica en un dispositivo que tenía originalmente Hola GA (versión 6.3.9600.17215) de la versión instalada pero se ha actualizado toohello versión de octubre (versión 6.3.9600.17312). se produce un error de restablecimiento de fábrica de Hola y dispositivo Hola se vuelve inestable. |Sí |No |

## <a name="known-issues-in-hello-february-release"></a>Problemas conocidos de la versión de febrero de Hola
Hello en la tabla siguiente proporciona un resumen de los problemas conocidos de esta versión.

| No. | Característica | Problema | Comentarios/solución alternativa | Se aplica a dispositivos toophysical | Se aplica a dispositivos toovirtual |
| --- | --- | --- | --- | --- | --- |
| 1 |Restablecimiento de fábrica |En algunos casos, cuando se realiza un restablecimiento de fábrica, Hola dispositivo StorSimple puede bloquearse y mostrar este mensaje: **toofactory restablecimiento está en curso (fase 8)**. Esto sucede si presiona CTRL + C mientras Hola cmdlet está en curso. |No presione CTRL+C después de iniciar un restablecimiento de fábrica. Si ya está en este estado, póngase en contacto con el soporte técnico de Microsoft para conocer los pasos siguientes. |Sí |No |
| 2 |Cuórum de disco |En raras ocasiones, si la mayoría de Hola de discos del alojamiento EBOD Hola de un 8600device se desconecta y no hay quórum de disco, a continuación, grupo de almacenamiento de hello estarán sin conexión. Incluso si se vuelven a conectar discos Hola permanecerá sin conexión. |Necesitará tooreboot dispositivo de Hola. Si persiste el problema de hello, póngase en contacto con Microsoft Support para los pasos siguientes. |Sí |No |
| 3 |Errores de instantánea en la nube |En raras ocasiones, puede producir un error de una instantánea en la nube con error de hello **ha alcanzado el límite de copia de seguridad de máximo**. Esto ocurre si excede 255 clones en línea en hello mismo dispositivo, de hello mismo volumen original que se ha eliminado. | |Sí |Sí |
| 4 |Identificador de controlador incorrecto |Cuando se realiza un reemplazo de controlador, el controlador 0 puede aparecer como controlador 1. Durante el reemplazo de controlador, cuando se carga la imagen de Hola desde el nodo del mismo nivel de hello, identificador de la controladora de hello puede mostrarse inicialmente como Id.. del controlador de hello del mismo nivel En raras ocasiones, este comportamiento también puede aparecer después del reinicio del sistema. |No se requiere ninguna acción del usuario. Esta situación se solucionará automáticamente una vez completada la sustitución del controlador Hola. |Sí |No |
| 5 |Gráficos de supervisión de dispositivos |En el servicio StorSimple Manager hello, gráficos de supervisión de dispositivos de hello no funcionan cuando básica o la autenticación NTLM está habilitada en la configuración de servidor proxy de hello de dispositivo de Hola. |Modificar configuración de proxy web de Hola para dispositivo Hola registrado con el servicio StorSimple Manager para que la autenticación se establece tooNONE. toodo, Hola Hola ejecución Windows PowerShell para el cmdlet Set-HcsWebProxy de StorSimple. |Sí |Sí |
| 6 |Cuentas de almacenamiento |Usar cuenta de almacenamiento de hello almacenamiento servicio toodelete hello es un escenario no compatible. Esto daría lugar situación tooa en el que no se puede recuperar datos de usuario. | |Sí |Sí |
| 7 |Conmutación por error del dispositivo |Varias conmutaciones por error de un contenedor de volumen de hello no se admite los mismos dispositivos de destino de toodifferent de dispositivo de origen.    Conmutación por error de una única cola de dispositivos toomultiple dispositivos hará que los contenedores de volúmenes de hello en hello primero conmutado por dispositivo pierda la propiedad de los datos. Después de este tipo una conmutación por error, estos contenedores de volumen aparecerán o se comportan de forma diferente cuando se visualizan en hello portal de Azure clásico. | |Sí |No |
| 8 |Instalación |Durante el adaptador de StorSimple para la instalación de SharePoint, debe tooprovide una dirección IP de dispositivo en orden para hello install toofinish correctamente. | |Sí |No |
| 9 |Proxy web |Si la configuración del proxy web tiene HTTPS como Hola especifica protocolo, afectará a la comunicación de servicio de dispositivos y dispositivos de Hola se desconectará. Paquetes de compatibilidad también se generarán en el proceso de hello, que consumen muchos recursos en el dispositivo. |Asegúrese de que Hola URL de proxy web tenga HTTP como Hola protocolo especificado. Para obtener más información acerca de cómo demasiado[configurar el proxy web para el dispositivo](storsimple-configure-web-proxy.md). |Sí |No |
| 10 |Proxy web |Si configura y habilitar el proxy web en un dispositivo registrado, deberá controlador activo de toorestart hello en el dispositivo. | |Sí |No |
| 11 |Latencia alta de la nube y alta carga de trabajo de E/S |Cuando el dispositivo de StorSimple encuentra una combinación de latencias de nube muy altas (orden de segundos) y la carga de trabajo de E/S alta, volúmenes del dispositivo Hola pasan a un estado degradado y Hola operaciones de E/s se puede producir un error "el dispositivo no está listo". |Se necesitan controladores de dispositivo de toomanually reinicio Hola o realizar una toorecover de conmutación por error de dispositivo de esta situación. |Sí |No |

## <a name="physical-device-updates-in-hello-february-release"></a>Actualizaciones de dispositivo físico en la versión de febrero de Hola
Este generador de Hola de correcciones de actualización restablece el problema que se ha producido en los dispositivos que se han actualizado desde la versión de Hola GA toohello versión de octubre de 2014. No contiene ningún otro dispositivo de StorSimple de toohello de actualizaciones.  

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-february-release"></a>Conectado en serie SCSI (SAS) controlador y actualizaciones de firmware en versión de febrero de Hola
Esta versión no contiene ningún controlador de actualizaciones toohello conectado en serie SCSI (SAS) o el firmware de Hola. actualización del controlador Hola estaba en hello octubre, versión 2014.  

## <a name="virtual-device-updates-in-hello-february-release"></a>Actualizaciones de dispositivo virtual en la versión de febrero de Hola
Esta versión no contiene ninguna actualización para dispositivo virtual Hola. Aplicar esta actualización no cambiará la versión de software de Hola de un dispositivo virtual.

