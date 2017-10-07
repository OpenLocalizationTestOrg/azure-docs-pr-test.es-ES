---
title: comportamiento de alertas de aaaSMS en grupos de acciones | Documentos de Microsoft
description: Formato de mensaje SMS y responde tooSMS mensajes toounsubscribe, suscribirse o solicitar ayuda.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 3cd09b1903e3472f6402f62b74409d97e7e7ea97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a>Comportamiento de las alertas por SMS en los grupos de acciones
## <a name="overview"></a>Información general ##
Grupos de acciones le permiten tooconfigure una lista de destinatarios. A continuación, se pueden aprovechar estos grupos al definir las alertas del registro de actividad; asegurarse de que se notifique un grupo de acción determinado cuando se desencadene la alerta del registro de actividad de Hola. Uno de hello admiten mecanismos de alerta es SMS; las alertas de Hello admiten la comunicación bidireccional. Un usuario puede responder tooan alerta:

- **Cancelar la suscripción a alertas:** un usuario puede cancelar la suscripción a todas las alertas por SMS para todos los grupos de acciones o para un grupo de acciones singular.  
- **Suscribirse tooalerts:** un usuario puede volver a suscribirse tooall alertas SMS para todos los grupos de acciones o un grupo de acción singular.  
- **Solicitar ayuda:** puede pedir un usuario para obtener más información sobre Hola SMS. Estarán artículo toothis redirigida

Este artículo explica el comportamiento de Hola de alertas SMS de Hola y Hola usuario de Hola de acciones de respuesta puede tomar en función de configuración regional de saludo del usuario de hello:

## <a name="usacanada-sms-behavior"></a>Comportamiento de SMS en Estados Unidos y Canadá
### <a name="receiving-an-sms-alert"></a>Recepción de una alerta por SMS
Un receptor de SMS, que se configura como parte de un grupo de acciones, recibirá un SMS cuando se desencadene una alerta. Hola SMS transmitirá Hola siguiente información:
* Nombre corto de grupo de acciones de hello esta alerta se envió a
- Título de alerta de Hola

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a>Cancelación de la suscripción a alertas por SMS para un grupo de acciones
Un usuario puede cancelar la suscripción de SMS para las alertas para el grupo de acciones de una forma responde toohello 20873 con las palabras clave de hello: "Deshabilitar &lt;Shortname del grupo de acción&gt;".

Ejemplo: Un usuario que quieran toounsubscribe de alertas para un grupo de acciones con hello shortname "Azure", enviaría un toohello SMS 20873 que dice "Deshabilitar Azure"

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a>Cancelación de la suscripción a alertas por SMS para todos los grupos de acciones
Un usuario puede cancelar la suscripción a todas las alertas SMS para todos los grupos de acciones por responde toohello 20873 con cualquiera de hello siguientes palabras clave:
* STOP

Ejemplo: Un usuario que quieran toounsubscribe de todas las alertas SMS para todos los grupos de acciones, enviaría un toohello SMS 20873 que dice "Detener"

>[!NOTE]
>Si un usuario ha cancelado la suscripción a alertas SMS, pero, a continuación, se agrega el nuevo grupo de acciones tooa; SE recibir avisos SMS para ese grupo de acción nueva, pero permanecen sin suscripciones de todos los grupos de acción anterior.
>
>

### <a name="resubscribing-toosms-alerts-for-one-action-group"></a>Resubscribing tooSMS alertas para un grupo de acciones
Un usuario puede volver a suscribirse tooSMS para las alertas para el grupo de una acción por responde toohello 20873 con las palabras clave de hello: "Habilitar &lt;Shortname del grupo de acción&gt;".

Ejemplo: Un usuario que quieran tooresubscribe tooalerts para un grupo de acciones con hello shortname "Azure", enviaría un toohello SMS 20873 que dice "Habilitar Azure"

### <a name="resubscribing-toosms-alerts-for-all-action-groups"></a>Resubscribing tooSMS alertas para todos los grupos de acciones
Un usuario puede volver a suscribirse tooall SMS para las alertas para todos los grupos de acciones por responde toohello 20873 con cualquiera de hello siguientes palabras clave:

* START

Ejemplo: Un usuario que quieran toounsubscribe de todas las alertas SMS para todos los grupos de acciones, enviaría un toohello SMS 20873 que dice "START"

### <a name="requesting-help-via-sms"></a>Solicitud de ayuda a través de SMS
Un usuario puede solicitar para obtener más información acerca de hello SMS que han recibido por responde toohello 20873 con cualquiera de hello siguientes palabras clave:
* HELP

Usuario toohello con un artículo de toothis de vínculo se enviará una respuesta.

## <a name="next-steps"></a>Pasos siguientes
Obtener un [información general de alertas de registro de actividad](monitoring-overview-alerts.md) y obtenga información acerca de cómo tooget una alerta  
Más información sobre la [limitación de la tasa de SMS](monitoring-alerts-rate-limiting.md)  
Más información sobre los [grupos de acciones](monitoring-action-groups.md)
