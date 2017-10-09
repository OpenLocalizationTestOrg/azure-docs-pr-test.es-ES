---
title: esquema de webhook de hello aaaUnderstand utilizado en las alertas de registro de actividad | Documentos de Microsoft
description: "Obtenga información acerca del esquema de Hola de hello JSON que se registra la dirección URL del webhook tooa cuando se activa una alerta de registro de actividad."
author: johnkemnetz
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
ms.author: johnkem
ms.openlocfilehash: 75562e0589222d3e392ea73eacfd7414a422d115
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a>Webhooks para alertas del registro de actividad de Azure
Como parte de la definición de Hola de un grupo de acciones, puede configurar notificaciones de alerta de webhook extremos tooreceive actividad registro. Con webhooks, es posible distribuir estos sistemas de tooother notificaciones para las acciones posteriores al procesamiento o personalizados. Este artículo muestra qué carga Hola Hola HTTP POST tooa webhook aspecto.

Para obtener más información sobre las alertas de registro de actividad, vea cómo demasiado[crear alertas de registro de actividad de Azure](monitoring-activity-log-alerts.md).

Para obtener información sobre grupos de acciones, vea cómo demasiado[crear grupos de acciones](monitoring-action-groups.md).

## <a name="authenticate-hello-webhook"></a>Autenticar hello webhook
Hola webhook puede utilizar opcionalmente la autorización basada en el símbolo (token) para la autenticación. Hola webhook URI se guarda con un identificador de token, por ejemplo, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.

## <a name="payload-schema"></a>Esquema de carga
carga JSON de Hello contenido en hello operación POST difiere según el en el campo de data.context.activityLog.eventSource de carga de Hola.

###<a name="common"></a>Común
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "channels": "Operation",
                "correlationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "eventSource": "Administrative",
                "eventTimestamp": "2017-03-29T15:43:08.0019532+00:00",
                "eventDataId": "8195a56a-85de-4663-943e-1a2bf401ad94",
                "level": "Informational",
                "operationName": "Microsoft.Insights/actionGroups/write",
                "operationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "status": "Started",
                "subStatus": "",
                "subscriptionId": "52c65f65-0518-4d37-9719-7dbbfc68c57a",
                "submissionTimestamp": "2017-03-29T15:43:20.3863637+00:00",
                ...
            }
        },
        "properties": {}
    }
}
```
###<a name="administrative"></a>Administrativo
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "authorization": {
                    "action": "Microsoft.Insights/actionGroups/write",
                    "scope": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions"
                },
                "claims": "{...}",
                "caller": "me@contoso.com",
                "description": "",
                "httpRequest": "{...}",
                "resourceId": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions",
                "resourceGroupName": "CONTOSO-TEST",
                "resourceProviderName": "Microsoft.Insights",
                "resourceType": "Microsoft.Insights/actionGroups"
            }
        },
        "properties": {}
    }
}

```
###<a name="servicehealth"></a>ServiceHealth
```json
{
    "schemaId": "unknown",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "properties": {
                    "title": "...",
                    "service": "...",
                    "region": "...",
                    "communication": "...",
                    "incidentType": "Incident",
                    "trackingId": "...",
                    "groupId": "...",
                    "impactStartTime": "3/29/2017 3:43:21 PM",
                    "impactMitigationTime": "3/29/2017 3:43:21 PM",
                    "eventCreationTime": "3/29/2017 3:43:21 PM",
                    "impactedServices": "[{...}]",
                    "defaultLanguageTitle": "...",
                    "defaultLanguageContent": "...",
                    "stage": "Active",
                    "communicationId": "...",
                    "version": "0.1"
                }
            }
        },
        "properties": {}
    }
}
```

Para obtener detalles del esquema específico sobre alertas del registro de actividad de notificaciones de mantenimiento del servicio, consulte [Notificaciones de mantenimiento del servicio](monitoring-service-notifications.md).

Para obtener información de esquema específico en todas las otras alertas de registro de actividad, consulte [información general sobre el registro de actividad de Azure de hello](monitoring-overview-activity-logs.md).

| Nombre del elemento | Descripción |
| --- | --- |
| status |Usado para alertas de métrica. Siempre se establece demasiado "activado" para las alertas de registro de actividad. |
| contexto |Contexto de evento de Hola. |
| resourceProviderName |proveedor de recursos de Hola de hello afectado recursos. |
| conditionType |Siempre "Event" |
| name |Nombre de regla de alerta de Hola. |
| id |Id. de recurso de alerta de Hola. |
| description |Descripción de la alerta establece cuando se crea la alerta de Hola. |
| subscriptionId |Identificador de suscripción de Azure |
| timestamp |Hora a qué Hola se generó el evento por el servicio de Azure que procesa la solicitud de Hola Hola. |
| resourceId |Id. de recurso de hello afectado recursos. |
| resourceGroupName |Nombre de grupo de recursos de Hola Hola afectado recursos. |
| propiedades |Conjunto de `<Key, Value>` pares (es decir, `Dictionary<String, String>`) que incluye detalles acerca del evento Hola. |
| event |Elemento que contiene metadatos acerca del evento Hola. |
| authorization |propiedades de Control de acceso basado en roles de Hola de evento de Hola. Normalmente, estas propiedades incluyen acción hello, rol Hola y Hola ámbito. |
| categoría |Categoría de eventos de Hola. Los valores admitidos incluyen: Administrative, Alert, Security, ServiceHealth y Recommendation. |
| caller |Dirección de correo electrónico del usuario de Hola que realizó la operación de hello, notificación de UPN o notificación SPN según su disponibilidad. Puede ser null para ciertas llamadas del sistema. |
| correlationId |Normalmente, un GUID en formato de cadena. Eventos con correlationId pertenecen toohello misma acción mayor y normalmente comparten un correlationId. |
| eventDescription |Descripción de texto estático de evento Hola. |
| eventDataId |Identificador único para el evento de Hola. |
| eventSource |Nombre de Hola servicio de Azure o la infraestructura de ese evento Hola generado. |
| httpRequest |Hello solicitud normalmente incluye hello clientRequestId, clientIpAddress y método HTTP (por ejemplo, PUT). |
| level |Uno de hello siguientes valores: crítico, Error, advertencia, informativo y detallado. |
| operationId |Normalmente un GUID que se comparten entre eventos de hello correspondiente toosingle operación. |
| operationName |Nombre de operación de Hola. |
| propiedades |Propiedades de evento de Hola. |
| status |String. Estado de operación de Hola. Entre los valores habituales, se incluyen Started, In Progress, Succeeded, Failed, Active y Resolved. |
| subStatus |Normalmente incluye código de estado HTTP de Hola de llamada REST de hello correspondiente. También podría incluir otras cadenas que describen un subestado. Entre los valores de subestado habituales se incluyen OK (código de estado HTTP: 200), Created (código de estado HTTP: 201), Accepted (código de estado HTTP: 202), No Content (código de estado HTTP: 204), Bad Request (código de estado HTTP: 400), Not Found (código de estado HTTP: 404), Conflict (código de estado HTTP: 409), Internal Server Error (código de estado HTTP: 500), Service Unavailable (código de estado HTTP: 503) y Gateway Timeout (código de estado HTTP: 504). |

## <a name="next-steps"></a>Pasos siguientes
* [Obtener más información sobre el registro de actividad de hello](monitoring-overview-activity-logs.md).
* [Ejecución de scripts de Azure Automation (runbooks) en alertas de Azure](http://go.microsoft.com/fwlink/?LinkId=627081).
* [Usar un toosend de aplicación lógica un SMS a través de Twilio de una alerta Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app). En este ejemplo es para alertas métricas, pero puede ser modificado toowork con una alerta de registro de actividad.
* [Usar un toosend de aplicación lógica un mensaje desde una alerta Azure demora](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app). En este ejemplo es para alertas métricas, pero puede ser modificado toowork con una alerta de registro de actividad.
* [Usar un toosend de aplicación lógica un tooan mensaje Azure cola desde una alerta Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app). En este ejemplo es para alertas métricas, pero puede ser modificado toowork con una alerta de registro de actividad.
