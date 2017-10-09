---
title: "Guía de directiva aaaSupportability y retirada de SO invitado de Azure | Documentos de Microsoft"
description: "Proporciona información sobre lo que Microsoft proporcionará soporte en lo relativo a toohello SO invitado de Azure usa servicios en la nube."
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 919dd781-4dc6-4e50-bda8-9632966c5458
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/26/2017
ms.author: raiye
ms.openlocfilehash: 6a86c42ac95d12bbf116d900b7afb26fc3fe34e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-guest-os-supportability-and-retirement-policy"></a>Directiva de compatibilidad y retirada del SO invitado de Azure
información de Hello en esta página está relacionada con toohello sistema operativo invitado Azure ([SO invitado](cloud-services-guestos-update-matrix.md)) para los roles de trabajador y web de servicios en la nube (PaaS). No se aplica tooVirtual máquinas (IaaS).

Microsoft tiene un informe publicado [directiva de soporte técnico para hello SO invitado](http://support.microsoft.com/gp/azure-cloud-lifecycle-faq). página de Hello que está leyendo ahora describe la forma de implementar la directiva de Hola.

Directiva de Hello es

1. Microsoft proporcionará soporte **Hola al menos dos últimas familias del SO invitado de hello**. Cuando se retira una familia, los clientes tienen 12 meses a partir de hello retirada oficial fecha tooupdate tooa más reciente compatible familia del SO invitado.
2. Microsoft proporcionará soporte **Hola al menos dos últimas versiones de familias del SO invitado Hola admitida**.
3. Microsoft proporcionará soporte **Hola al menos dos últimas versiones de hello Azure SDK**. Cuando hay una versión de SDK se retira de hello, los clientes dispondrán de 12 meses a partir de la versión más reciente del tooa de tooupdate de fecha de retirada oficial para Hola.

En ocasiones, es posible que se proporcione soporte técnico para más de dos familias o versiones. Información de soporte oficial de SO invitado aparecerá en hello [versiones del SO invitado de Azure y la matriz de compatibilidad de SDK](cloud-services-guestos-update-matrix.md).

## <a name="when-a-guest-os-family-or-version-is-retired"></a>Cuando se retira una familia o versión del SO invitado
Un sistema operativo invitado nuevo **familia** se introdujo en algún momento después de la versión de Hola de una nueva versión oficial del sistema operativo de Windows Server de Hola. Cada vez que se introduce una nueva familia de SO invitado, Microsoft retira familia del SO invitado más antigua Hola.

Sistema operativo invitado nuevo **versiones** plantean sobre cada actualizaciones más recientes de MSRC de mes tooincorporate Hola. Debido a actualizaciones mensuales periódicas hello, una versión de SO invitado es deshabilita normalmente 60 días después de su lanzamiento. Esta actividad mantiene al menos dos versiones del SO invitado para cada familia disponibles para su uso.

### <a name="process-during-a-guest-os-family-retirement"></a>Proceso durante la retirada de una familia del SO invitado
Una vez que se anuncia la retirada de hello, los clientes tienen un período de 12 meses "transición" antes de familia de hello anterior se retire oficialmente de servicio. Este período de transición se puede prolongar a discreción de Hola de Microsoft. Las actualizaciones se publicarán en hello [versiones del SO invitado de Azure y la matriz de compatibilidad de SDK](cloud-services-guestos-update-matrix.md).

Un proceso gradual de retirada comenzará seis (6) meses en el período de transición de Hola. Durante este tiempo:

1. Microsoft notificará a los clientes de retirada de Hola.
2. versión más reciente de Hola de hello Azure SDK no admitirá la familia del SO invitado Hola retirado.
3. Nuevas implementaciones ni reimplementaciones de los servicios en la nube no se permitirán en la familia de hello retirado

Microsoft seguirá toointroduce nueva versión del SO invitado incorpora actualizaciones MSRC más recientes de hello hasta el último día del período de transición de hello, conocido como "fecha de expiración" Hola Hola. En la fecha de expiración de hello, servicios de nube que sigan ejecutándose se no se admitan en hello SLA de Azure. Microsoft tiene Hola discreción tooforce actualizar, eliminar o detener dichos servicios después de esa fecha.

### <a name="process-during-a-guest-os-version-retirement"></a>Proceso durante la retirada de una versión del SO invitado
Si los clientes establecen su actualización tooautomatically de SO invitado, nunca tienen tooworry sobre cómo gestionar versiones del SO invitado. Siempre va a usar versión más reciente de SO invitado de Hola.

Se publican versiones del SO invitado cada mes. Debido a tasa de Hola de versiones periódicas, cada versión tiene una vida útil fija.

En el 60 días de duración de hello, es una versión "*deshabilitado*". "Deshabilitado" significa que la versión Hola se quita del portal de Hola. versión de Hola ya no se puede establecer desde el archivo de configuración de CSCFG Hola. Las implementaciones existentes sigan ejecutándose. Pero no se permitirán nuevas implementaciones ni tooexisting implementaciones de actualizaciones de código y la configuración.

Versión del SO invitado de Hola de algún tiempo después de convertirse en "deshabilitado", "*expira*" y cualquier instalación que se siga ejecutando esa versión se tendrá que actualizar y establecerse tooautomatically actualización Hola SO invitado en hello futuras. La expiración se produce en lotes para que hello período de tiempo de deshabilitación tooexpiration puede variar.

Estos períodos se pueden prolongar en transiciones de cliente de tooease de discreción de Microsoft. Los cambios se comunicarán en hello [versiones del SO invitado de Azure y la matriz de compatibilidad de SDK](cloud-services-guestos-update-matrix.md).

### <a name="notifications-during-retirement"></a>Notificaciones durante la retirada
* **Retirada de la familia** <br>Microsoft usará las entradas de los blogs y las notificaciones del portal. Los clientes que aún utilicen una familia del SO invitado retirada se notificará a través de los administradores de servicios de tooassigned de comunicación directa (correo electrónico, mensajes del portal, llamada de teléfono). Todos los cambios se publicarán toothis hello y página fuente RSS que aparece al principio de Hola de esta página.
* **Retirada de la versión** <br>Todos los cambios y las fechas de Hola que se produzcan se publicarán toothis hello y página fuente RSS que aparece al principio de Hola de esta página, incluida la versión, deshabilitado y la expiración. Los administradores de los servicios recibirán correos electrónicos si tienen implementaciones que se ejecutan en una versión o familia del SO invitado que se ha deshabilitado. tiempo de Hola de estos correos electrónicos puede variar. Suelen ser al menos un mes antes de la deshabilitación, aunque este tiempo no es un contrato de nivel de servicio oficial.

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes
**¿Cómo puedo mitigar los efectos de saludo de la migración?**

Se recomienda utilizar la familia del SO invitado más reciente para diseñar los servicios en la nube.

1. Empezar a planear su familia más reciente de tooa de migración de una fase temprana.
2. Configurar su servicio de nube que se ejecuta en la nueva familia de Hola de tootest de las implementaciones de prueba temporal.
3. Establecer la versión del SO invitado demasiado**automática** (osVersion = * en hello [.cscfg](cloud-services-model-and-package.md#cscfg) archivo) para las versiones de SO invitado de hello migración toonew se produce automáticamente.

**¿Qué ocurre si mi aplicación web requiere una integración más profunda con hello OS?**

Si la arquitectura de aplicación web depende de las características subyacentes del sistema operativo de hello, usar las capacidades de plataforma admitida como [las tareas de inicio](cloud-services-startup-tasks.md) u otros mecanismos de extensibilidad. Como alternativa, también puede usar [máquinas virtuales de Azure](https://azure.microsoft.com/documentation/scenarios/virtual-machines/) (IaaS – infraestructura como servicio), que es responsable de mantener Hola subyacente de sistema operativo.

## <a name="next-steps"></a>Pasos siguientes
Hola de revisión más reciente [versiones del SO invitado](cloud-services-guestos-update-matrix.md).
