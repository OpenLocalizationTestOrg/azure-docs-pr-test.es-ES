---
title: "notas de la versión de lanzamiento de aaaStorSimple 8000 | Documentos de Microsoft"
description: "Describe nuevas características de hello, incidencias abiertas y soluciones alternativas disponibles para hello julio de 2014 versión de StorSimple de Microsoft Azure."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 12f1796e-37c3-42b4-b997-a84fc1950c20
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: 74863a3e2811dc7be5e6f482a5be4bbc37e3cd71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-release-version-release-notes---july-2014"></a>Notas de la versión de StorSimple 8000 Series - julio de 2014
## <a name="overview"></a>Información general
notas de la versión de Hola seguimiento identifican Hola temas críticos por hello StorSimple 8000 Series versión de disponibilidad general (GA) de julio de 2014 de Microsoft Azure StorSimple. Esta versión corresponde toosoftware versión 6.3.9600.17215.  

A menos que se especifique lo contrario, estas notas de la versión tooall modelos de dispositivo de StorSimple de Hola se aplican. notas de la versión de Hola se actualizan continuamente; Cuando se detectan problemas críticos que requieren una solución, se agregan. Antes de implementar la solución de StorSimple de Microsoft Azure, considere la posibilidad de hello siguiente información.  

## <a name="known-issues-in-this-release"></a>Problemas conocidos en esta versión
Hello en la tabla siguiente proporciona un resumen de los problemas conocidos de esta versión.  

| No. | Característica | Problema | Comentarios/solución alternativa | Se aplica a dispositivos toophysical | Se aplica a dispositivos toovirtual |
| --- | --- | --- | --- | --- | --- |
| 1 |Restablecimiento de fábrica |En algunos casos, cuando se realiza un restablecimiento de fábrica, Hola dispositivo StorSimple puede bloquearse y mostrar este mensaje: **toofactory restablecimiento está en curso (fase 8)**. Esto sucede si presiona CTRL + C mientras Hola cmdlet está en curso. |No presione CTRL+C después de iniciar un restablecimiento de fábrica. Si ya está en este estado, póngase en contacto con el soporte técnico de Microsoft para conocer los pasos siguientes. |Sí |No |
| 2 |Cuórum de disco |En raras ocasiones, si la mayoría de Hola de discos del alojamiento EBOD Hola de un dispositivo 8600 se desconecta y no hay quórum de disco, a continuación, grupo de almacenamiento de hello estarán sin conexión. Incluso si se vuelven a conectar discos Hola permanecerá sin conexión. |Necesitará tooreboot dispositivo de Hola. Si persiste el problema de hello, póngase en contacto con Microsoft Support para los pasos siguientes. |Sí |No |
| 3 |Errores de instantánea en la nube |En raras ocasiones, puede producir un error de una instantánea en la nube con error de hello **ha alcanzado el límite de copia de seguridad de máximo**. Esto ocurre si excede 255 clones en línea en hello mismo dispositivo, de hello mismo volumen original que se ha eliminado. | |Sí |Sí |
| 4 |Identificador de controlador incorrecto |Cuando se realiza un reemplazo de controlador, el controlador 0 puede aparecer como controlador 1. Durante el reemplazo de controlador, cuando se carga la imagen de Hola desde el nodo del mismo nivel de hello, identificador de la controladora de hello puede mostrarse inicialmente como Id.. del controlador de hello del mismo nivel En raras ocasiones, este comportamiento también puede aparecer después del reinicio del sistema. |No se requiere ninguna acción del usuario. Esta situación se solucionará automáticamente una vez completada la sustitución del controlador Hola. |Sí |No |
| 5 |Gráficos de supervisión de dispositivos |En el servicio StorSimple Manager hello, gráficos de supervisión de dispositivos de hello no funcionan cuando básica o la autenticación NTLM está habilitada en la configuración de servidor proxy de hello de dispositivo de Hola. |Modificar configuración de proxy web de Hola para dispositivo Hola registrado con el servicio StorSimple Manager para que la autenticación se establece tooNONE. toodo, Hola Hola ejecución Windows PowerShell para el cmdlet Set-HcsWebProxy de StorSimple. |Sí |Sí |
| 6 |Cuentas de almacenamiento |Usar cuenta de almacenamiento de hello almacenamiento servicio toodelete hello es un escenario no compatible. Esto daría lugar situación tooa en el que no se puede recuperar datos de usuario. | |Sí |Sí |
| 7 |Conmutación por recuperación |No se admite una conmutación por recuperación durante las 24 horas siguientes a la recuperación ante desastres (DR). | |Sí |No |
| 8 |Conmutación por error del dispositivo |Varias conmutaciones por error de un contenedor de volumen de hello no se admite los mismos dispositivos de destino de toodifferent de dispositivo de origen. Conmutación por error de una única cola de dispositivos toomultiple dispositivos hará que los contenedores de volúmenes de hello en hello primero conmutado por dispositivo pierda la propiedad de los datos. Después de este tipo una conmutación por error, estos contenedores de volumen aparecerán o se comportan de forma diferente cuando se visualizan en hello portal de Azure clásico. | |Sí |No |
| 9 |Instalación |Durante el adaptador de StorSimple para la instalación de SharePoint, debe tooprovide una dirección IP de dispositivo para hello install toofinish correctamente. | |Sí |No |
| 10 |Interfaces de red |Interfaces de red DATA 2 y DATA 3 se cambiaron en el software de Hola. |Póngase en contacto con Microsoft Support si necesita tooconfigure estas interfaces. |Sí |No |

