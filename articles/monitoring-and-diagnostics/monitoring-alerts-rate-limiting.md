---
title: "limitar aaaRate de SMS, mensajes de correo electrónico y webhooks | Documentos de Microsoft"
description: "Entender cómo Azure limita el número de Hola de notificaciones de SMS, correo electrónico o webhook posibles de un grupo de acción."
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
ms.openlocfilehash: 1cd08a5b982c82bb02e0bf93451aa1fcd9bc34af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a>Limitación del número de mensajes SMS, correo electrónico y envíos webhook
Limitación de velocidad es una suspensión de las notificaciones que se produce cuando se envían notificaciones demasiados tooa dirección de correo electrónico o número de teléfono específico. La limitación del índice asegura que las alertas son fáciles de administrar y procesar.

reglas de Hola de SMS y correo electrónico no son Hola igual. umbral de límite de velocidad de Hello es:

 - **SMS**: 10 mensajes en una hora.
 - **Correo electrónico**: 100 mensajes en una hora.

## <a name="rate-limit-rules"></a>Reglas de limitación de número
- Un número de teléfono particular o correo electrónico es velocidad limitada cuando recibe los mensajes de más de umbral de Hola que permite.
- Un número de teléfono o correo electrónico puede formar parte de grupos de acciones de muchas suscripciones. La limitación de número se aplica en todas las suscripciones. Se aplica en cuanto se alcanza el umbral de hello, incluso si se envían los mensajes de varias suscripciones.  
- Cuando un número de teléfono o correo electrónico es tasa limitado, se envía una notificación de adicional toocommunicate Hola de limitación de velocidad. Hello notificación Estados cuando hello velocidad limitar expira.

## <a name="rate-limit-of-webhooks"></a>Limitación de número para los webhooks ##
Actualmente, no hay ninguna limitación en vigor para webhooks.

## <a name="next-steps"></a>Pasos siguientes ##
* Más información sobre el [comportamiento de las alertas por SMS](monitoring-sms-alert-behavior.md).
* Obtener un [información general de alertas de registro de actividad](monitoring-overview-alerts.md)y obtenga información acerca de cómo tooreceive alertas.  
* Obtenga información acerca de cómo demasiado[configurar alertas siempre que se registra una notificación de estado de servicio](monitoring-activity-log-alerts-on-service-notifications.md).
