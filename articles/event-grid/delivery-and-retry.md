---
title: "reintento y la entrega de la cuadrícula de eventos de aaaAzure"
description: "Describe cómo Azure Event Grid entrega eventos y cómo administra los mensajes no entregados."
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: 874b3bf8892fbf803ef40f29d0ec10eb50150916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-message-delivery-and-retry"></a>Entrega y reintento de entrega de mensajes de Event Grid 

En este artículo se describe cómo Azure Event Grid administra los eventos cuando no se confirma la entrega.

Event Grid ofrece entrega duradera. Entrega cada mensaje por lo menos una vez en cada suscripción. Eventos se envían inmediatamente webhook toohello registrado de cada suscripción. Si un webhook no confirmar la recepción de un evento 60 segundos de entrega de hello primer intento, cuadrícula de eventos reintenta la entrega de eventos de Hola.

## <a name="message-delivery-status"></a>Estado de entrega de mensajes

Cuadrícula de eventos usa HTTP respuesta códigos tooacknowledge la recepción de eventos. 

### <a name="success-codes"></a>Códigos de éxito

Hello códigos de respuesta HTTP siguientes indican que un evento se ha entregado correctamente tooyour webhook. Event Grid considera la entrega finalizada.

- 200 OK
- 202 - Aceptado

### <a name="failure-codes"></a>Códigos de error

Hola siguientes códigos de respuesta HTTP indica que un intento de entrega de evento no se pudo. Cuadrícula de eventos intenta de nuevo evento de hello toosend. 

- 400 - Solicitud incorrecta
- 401 No autorizado
- 404 No encontrado
- 408 - Tiempo de espera de solicitud
- 414 - URI de solicitud demasiado largo
- Error de servidor interno 500
- Servicio no disponible 503
- Tiempo de espera de puerta de enlace 504

Cualquier otro código de respuesta o la falta de respuesta indica un error. Event Grid reintenta la entrega. 

## <a name="retry-intervals"></a>Intervalos de reintento

Event Grid usa una directiva de reintentos de retroceso exponencial para la entrega de eventos. Si el webhook no responde o devuelve un código de error, cuadrícula de eventos reintenta la entrega en hello siguiente programación:

1. 10 segundos
2. 30 segundos
3. 1 minuto
4. 5 minutos
5. 10 minutos
6. 30 minutos
7. 1 hora

Cuadrícula de eventos agrega un intervalos de reintento de selección aleatoria pequeño tooall.

## <a name="retry-duration"></a>Duración de reintentos

Durante la vista previa de hello, cuadrícula de eventos de Azure caduca todos los eventos que no se entregan dentro de dos horas. Antes de la disponibilidad General, este tiempo será mayor too24 horas. 

## <a name="next-steps"></a>Pasos siguientes

* Para una cuadrícula de introducción tooEvent, consulte [acerca de la cuadrícula de eventos](overview.md).
* tooquickly Introducción al uso de la cuadrícula de eventos, vea [ruta y crear eventos personalizados con la cuadrícula de eventos de Azure](custom-event-quickstart.md).
