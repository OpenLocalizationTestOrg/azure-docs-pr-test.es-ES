---
title: aaaWhat son las notificaciones de estado de servicio | Documentos de Microsoft
description: Las notificaciones de estado de servicio permiten que publicar mensajes de estado del servicio de tooview por Microsoft Azure.
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
ms.openlocfilehash: 6f2fe72154c3e80d85062655c49dd1799b718e3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-health-notifications"></a>Notificaciones de estado del servicio
## <a name="overview"></a>Información general

Este artículo muestra cómo usar las notificaciones de estado de servicio de tooview Hola portal de Azure.

Las notificaciones de estado de servicio permiten tooview servicio mantenimiento mensajes publicados por Hola, equipo de Azure que puede afectar a los recursos de hello en su suscripción. Estas notificaciones son una subclase de la actividad de registro de sucesos y también pueden encontrarse en la hoja de registro de actividad de Hola. Las notificaciones de estado de servicio pueden ser informativo o procesables dependiendo de la clase hello.

Hay cinco clases de las notificaciones de estado del servicio:  

- **Acción requerida:** de tiempo tootime podemos observamos algo inusual suceder en tu cuenta. Podemos necesitar toowork con tooremedy esto. Le enviaremos una notificación ya sea que detalla las acciones de hello deberá tootake o con información detallada sobre cómo ingeniería toocontact Azure o admite.  
- **Recuperación asistida:** se ha producido un evento y los ingenieros han confirmado que todavía le afecta. Ingeniería deberá toowork con usted directamente toobring su toorestoration de servicios.  
- **Incidente:** un servicio de evento que afecta actualmente está afectando a uno o más de los recursos de hello en su suscripción.  
- **Mantenimiento:** se trata de una notificación que le informa de una actividad de mantenimiento planeado que puedan afectar a uno o varios de los recursos de hello en su suscripción.  
- **Información:** de tiempo tootime podremos enviarle notificaciones que un tooyou comunicar sobre posibles optimizaciones que puede ayudar a mejora la utilización de recursos.  
- **Seguridad:** información urgente relacionada con la seguridad de las soluciones que se ejecutan en Azure.

Cada notificación de estado de servicio transmitirá detalles en los recursos de tooyour de hello ámbito e impacto. Dichos datos incluyen:

Nombre de propiedad | Descripción
-------- | -----------
canales nueva | Es uno de hello siguientes valores: "Admin", "Operación"
correlationId | Suele ser un GUID en formato de cadena de Hola. Eventos que pertenecen toohello normalmente comparten la misma acción Hola mismo correlationId.
eventDataId | Es el identificador único de Hola de un evento
eventName | Es título Hola de evento Hola
level | Nivel de evento de Hola. Uno de hello siguientes valores: "Critical", "Error", "Warning", "Informational" y "Verbose"
resourceProviderName | Nombre de proveedor de recursos de Hola para hello afectado recursos
resourceType| tipo Hello del recurso de hello afectado recursos
subStatus | Normalmente Hola código de estado HTTP de hello correspondiente llamada REST, pero también puede incluir otras cadenas que describen un subestado, por ejemplo, estos valores comunes: Aceptar (código de estado HTTP: 200), creado (código de estado HTTP: 201), aceptado (código de estado HTTP: 202), sin contenido (HTTP Código de estado: 204), solicitud incorrecta (código de estado HTTP: 400), pero no se encontraron (código de estado HTTP: 404), conflicto (código de estado HTTP: 409), Error interno del servidor (código de estado HTTP: 500), servicio no está disponible (código de estado HTTP: 503), el tiempo de espera de puerta de enlace (código de estado HTTP: 504).
eventTimestamp | Marca de tiempo cuando se generan eventos de Hola Hola Hola de procesamiento de servicio de Azure solicitar evento Hola correspondiente.
submissionTimestamp |   Marca de tiempo al evento Hola empezó a estar disponible para las consultas.
subscriptionId | Hello en el que se registra este evento de suscripción de Azure
status | Cadena que describe el estado de Hola de operación de Hola. Algunos valores habituales son: Started, In Progress, Succeeded, Failed, Active y Resolved.
operationName | Nombre de operación de Hola.
categoría | "ServiceHealth"
resourceId | Id. de recurso de hello afectado recursos.
Properties.title | título de Hello localizada para esta comunicación. Idioma predeterminado de hello es inglés.
Properties.communication | Hola localizado detalles de comunicación de hello con formato HTML. Idioma predeterminado de hello es inglés.
Properties.incidentType | Valores posibles: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security
Properties.trackingId | Identifica el incidente de hello que está asociado a este evento. Utilice este incidente de toocorrelate Hola eventos tooan relacionados.
Properties.impactedServices | Un escape blob JSON que describe los servicios de Hola y regiones que se ven afectadas por incidente Hola. Una lista de servicios, cada uno de los cuales tiene un valor ServiceName y una lista de ImpactedRegions, cada una de los cuales tiene un valor RegionName.
Properties.defaultLanguageTitle | comunicación de saludo en inglés
Properties.defaultLanguageContent | comunicación de saludo en inglés como marcado html o texto sin formato
Properties.stage | Valores posibles de AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security: Active y Resolved. En el caso de Maintenance son: Active, Planned, InProgress, Canceled, Rescheduled, Resolved y Complete
Properties.communicationId | comunicación de Hello este evento está asociado.


## <a name="viewing-your-service-health-notifications-in-hello-azure-portal"></a>Ver las notificaciones de estado de servicio en hello portal de Azure
1.  Hola [portal](https://portal.azure.com), navegue toohello **Monitor** servicio

    ![Supervisión](./media/monitoring-service-notifications/home-monitor.png)
2.  Haga clic en hello **Monitor** opción tooopen una hoja de Monitor de Hola. En esta hoja se encuentran toda la configuración de supervisión y los datos en una sola vista consolidada. Abre por primera vez toohello **registro de actividad** sección.

3.  Ahora, haga clic en la sección **Notificaciones del servicio**

    ![Supervisión](./media/monitoring-service-notifications/service-health-summary.png)
4.  Haga clic en cualquiera de hello partidas tooview más detalles

5. Haga clic en hello **+ Agregar alerta de registro de actividad** operación tooreceive notificaciones tooensure se le notifica para las notificaciones de servicio futuras de este tipo. más información sobre la configuración de alertas en las notificaciones del servicio toolearn [haga clic aquí](monitoring-activity-log-alerts-on-service-notifications.md)

## <a name="next-steps"></a>Pasos siguientes:
Reciba [notificaciones de alertas cada vez que se publique una notificación de estado del servicio](monitoring-activity-log-alerts-on-service-notifications.md)  
Más información sobre las [alertas del registro de actividad](monitoring-activity-log-alerts.md)
