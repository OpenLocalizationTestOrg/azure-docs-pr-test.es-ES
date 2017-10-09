---
title: "aaaStorSimple 8000 Update 0.2 notas de la versión | Documentos de Microsoft"
description: "Describe nuevas características de Hola y correcciones, incidencias abiertas y soluciones alternativas disponibles para Hola de enero de 2015 (actualización 0,2) de lanzamiento de Microsoft Azure StorSimple."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d9684ae3-b38f-4678-9d70-e5dbc6b03350
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/16/2016
ms.author: v-sharos
ms.openlocfilehash: 1cee795df0b53d9b9276bc33074cf1a7aa188835
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-02-release-notes---january-2015"></a>Notas de la versión 0.2 de la actualización de la serie StorSimple 8000 - enero de 2015
## <a name="overview"></a>Información general
Hello notas de la versión siguiente identifican Hola temas críticos por hello versión de enero de 2015 de Microsoft Azure StorSimple. También contienen una lista de software de StorSimple de Hola y actualizaciones de firmware incluidas en esta versión. Esto es Hola segunda versión después de versión de la versión de StorSimple 8000 Series Hola se ponerse a disposición general en julio de 2014.

Esta actualización no cambia la versión de software de dispositivo físico de Hola de actualización de octubre de Hola. Continúa toobe versión 6.3.9600.17312. imagen de Hello utilizado por la imagen del dispositivo virtual Hola ha cambiado en esta versión. Por lo tanto, todos los Hola nuevos dispositivos virtuales creados después del 1/20/2015 mostrará versión hello 6.3.9600.17361.  

Revise Hola siguiendo la información contenida en las notas de la versión de actualización de enero de 2015 Hola Hola.

> [!IMPORTANT]
> * Esta actualización no está disponible a través de Windows Update y no se puede instalar como otras actualizaciones. El dispositivo no recibirá esta actualización incluso si ha aplicado las actualizaciones de hello mediante el uso de hello portal de Azure clásico. Esta actualización aplicará solo los dispositivos toovirtual creados después del 20 de enero de 2015. 
> * Hello enero versión de StorSimple no contiene ningún dispositivo físico de las actualizaciones toohello StorSimple. Puede aplicar cualquier dispositivo virtual de Windows actualizaciones toohello disponible, incluso de seguridad recientes correcciones, pero no verá un cambio en la versión para el dispositivo físico StorSimple Hola.
> 
> 

## <a name="whats-new-in-hello-january-release"></a>Novedades de la versión de enero de Hola
Esta actualización contiene una corrección volúmenes toohello quedarse sin conexión en el dispositivo virtual Hola relacionados. (Consulte [Problemas corregidos en esta versión](#issues-fixed-in-the-january-release)).  

actualización de Hello no contiene nuevas características o funcionalidad.  

## <a name="issues-fixed-in-hello-january-release"></a>Problemas corregidos en la versión de enero de Hola
Hello siguiente tabla describe problema Hola que se corrigió en esta actualización.

| No. | Característica | Problema | Se aplica a dispositivos toophysical | Se aplica a dispositivos toovirtual |
| --- | --- | --- | --- | --- |
| 1 |Volúmenes que se desconectan |Cuando las latencias de nube alta persisten durante varios minutos, volúmenes del dispositivo virtual StorSimple Hola se desconectan en hosts de Hola. Esta revisión aumenta el umbral de Hola para las latencias de nube, lo que minimiza las situaciones de Hola que provocarían hello toogo de volúmenes sin conexión en los hosts. |No |Sí |

## <a name="known-issues-in-hello-january-release"></a>Problemas conocidos de la versión de enero de Hola
Hello en la tabla siguiente proporciona un resumen de los problemas conocidos de esta versión.

| No. | Característica | Problema | Comentarios/solución alternativa | Se aplica a dispositivos toophysical | Se aplica a dispositivos toovirtual |
| --- | --- | --- | --- | --- | --- |
| 1 |Restablecimiento de fábrica |En algunos casos, cuando se realiza un restablecimiento de fábrica, Hola dispositivo StorSimple puede bloquearse y mostrar este mensaje: **toofactory restablecimiento está en curso (fase 8).** Esto sucede si presiona CTRL + C mientras Hola cmdlet está en curso. |No presione CTRL+C después de iniciar un restablecimiento de fábrica. Si ya está en este estado, póngase en contacto con el soporte técnico de Microsoft para conocer los pasos siguientes. |Sí |No |
| 2 |Cuórum de disco |En raras ocasiones, si la mayoría de Hola de discos del alojamiento EBOD Hola de un dispositivo 8600 se desconecta y no hay quórum de disco, a continuación, grupo de almacenamiento de hello estarán sin conexión. Incluso si se vuelven a conectar discos Hola permanecerá sin conexión. |Necesitará tooreboot dispositivo de Hola. Si persiste el problema de hello, póngase en contacto con Microsoft Support para los pasos siguientes. |Sí |No |
| 3 |Errores de instantánea en la nube |En raras ocasiones, puede producir un error de una instantánea en la nube con error de hello **ha alcanzado el límite de copia de seguridad de máximo**. Esto ocurre si excede 255 clones en línea en hello mismo dispositivo, de hello mismo volumen original que se ha eliminado. | |Sí |Sí |
| 4 |Identificador de controlador incorrecto |Cuando se realiza un reemplazo de controlador, el controlador 0 puede aparecer como controlador 1. Durante el reemplazo de controlador, cuando se carga la imagen de Hola desde el nodo del mismo nivel de hello, identificador de la controladora de hello puede mostrarse inicialmente como Id.. del controlador de hello del mismo nivel  En raras ocasiones, este comportamiento también puede aparecer después del reinicio del sistema. |No se requiere ninguna acción del usuario. Esta situación se solucionará automáticamente una vez completada la sustitución del controlador Hola. |Sí |No |
| 5 |Gráficos de supervisión de dispositivos |En el servicio StorSimple Manager hello, gráficos de supervisión de dispositivos de hello no funcionan cuando básica o la autenticación NTLM está habilitada en la configuración de servidor proxy de hello de dispositivo de Hola. |Modificar configuración de proxy web de Hola para dispositivo Hola registrado con el servicio StorSimple Manager para que la autenticación se establece tooNONE. toodo, Hola Hola ejecución Windows PowerShell para el cmdlet Set-HcsWebProxy de StorSimple. |Sí |Sí |
| 6 |Cuentas de almacenamiento |Usar cuenta de almacenamiento de hello almacenamiento servicio toodelete hello es un escenario no compatible. Esto daría lugar situación tooa en el que no se puede recuperar datos de usuario. | |Sí |Sí |
| 7 |Conmutación por error del dispositivo |Varias conmutaciones por error de un contenedor de volumen de hello no se admite los mismos dispositivos de destino de toodifferent de dispositivo de origen. |Conmutación por error de una única cola de dispositivos toomultiple dispositivos hará que los contenedores de volúmenes de hello en hello primero conmutado por dispositivo pierda la propiedad de los datos. Después de este tipo una conmutación por error, estos contenedores de volumen aparecerán o se comportan de forma diferente cuando se visualizan en hello portal de Azure clásico. |Sí |No |
| 8 |Instalación |Durante el adaptador de StorSimple para la instalación de SharePoint, debe tooprovide una dirección IP de dispositivo en orden para hello install toofinish correctamente. | |Sí |No |
| 9 |Proxy web |Si la configuración del proxy web tiene HTTPS como Hola especifica protocolo, afectará a la comunicación de servicio de dispositivos y dispositivos de Hola se desconectará. Paquetes de compatibilidad también se generarán en el proceso de hello, que consumen muchos recursos en el dispositivo. |Asegúrese de que Hola URL de proxy web tenga HTTP como Hola protocolo especificado. Obtener más información acerca de cómo demasiado[configurar el proxy web para el dispositivo](storsimple-configure-web-proxy.md). |Sí |No |
| 10 |Proxy web |Si configura y habilitar el proxy web en un dispositivo registrado, deberá controlador activo de toorestart hello en el dispositivo. | |Sí |No |
| 11 |Latencia alta de la nube y alta carga de trabajo de E/S |Cuando el dispositivo de StorSimple encuentra una combinación de latencias de nube muy altas (orden de segundos) y la carga de trabajo de E/S alta, volúmenes del dispositivo Hola pasan a un estado degradado y Hola operaciones de E/s se puede producir un error "el dispositivo no está listo". |Se necesitan controladores de dispositivo de toomanually reinicio Hola o realizar una toorecover de conmutación por error de dispositivo de esta situación. |Sí |No |

## <a name="physical-device-updates-in-hello-january-release"></a>Actualizaciones de dispositivo físico en el lanzamiento de enero de Hola
Esta actualización no contiene ningún otro dispositivo de StorSimple de toohello de cambios.

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-january-release"></a>Conectado en serie SCSI (SAS) controlador y actualizaciones de firmware en el lanzamiento de enero de Hola
Esta versión no contiene ningún controlador de actualizaciones toohello conectado en serie SCSI (SAS) o el firmware de Hola. actualización del controlador Hola estaba en hello octubre, versión 2014. 

## <a name="virtual-device-updates-in-hello-january-release"></a>Actualizaciones de dispositivo virtual en la versión de enero de Hola
Esta versión contiene una imagen actualizada para el dispositivo virtual Hola. Todos los dispositivos virtuales de hello creados después del 20 de enero de 2015 mostrará la versión de software de hello 6.3.9600.17361.

