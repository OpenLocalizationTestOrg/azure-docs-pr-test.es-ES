---
title: aaaCall un webhook en alertas de registro de actividad de Azure | Documentos de Microsoft
description: "Enrutar servicios de tooother de eventos de registro de actividad para las acciones personalizadas. Por ejemplo, envíe SMS, registre errores o notifique a un equipo a través del servicio de chat o mensajería."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 64d333d1-7f37-4a00-9d16-dda6e69a113b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: johnkem
ms.openlocfilehash: 9017ff3e5165857ec7084a8f07f4123552e55f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a>Llamada a un webhook cuando se activan alertas del registro de actividades de Azure
Webhooks le permiten tooroute un Azure sistemas de notificación de tooother para acciones posteriores al procesamiento o personalizados de alerta. Puede usar un webhook en una alerta tooroute se tooservices que enviar SMS, registrar errores, notificar a un equipo a través de servicios de chat/mensajería o realizar cualquier número de otras acciones. Este artículo describe cómo llama a tooset una toobe webhook cuando un se activa la alerta en el registro de actividad de Azure. También muestra qué carga Hola Hola HTTP POST tooa webhook aspecto. Para obtener información sobre el programa de instalación de Hola y el esquema de una alerta de métrica de Azure, [vea esta página en su lugar](insights-webhooks-alerts.md). También puede configurar un correo electrónico de alerta toosend del registro de actividad cuando se activan.

> [!NOTE]
> Esta característica está actualmente en versión preliminar y se quitará en algún momento futuro Hola.
>
>

Puede configurar una alerta de registro de actividad con hello [Cmdlets de PowerShell de Azure](insights-powershell-samples.md#create-metric-alerts), [multiplataforma CLI](insights-cli-samples.md#work-with-alerts), o [API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/dn933805.aspx). Actualmente, no se puede establecer uno utilizando Hola portal de Azure.

## <a name="authenticating-hello-webhook"></a>Autenticar hello webhook
Hola webhook se puedan autenticar con cualquiera de estos métodos:

1. **Autorización basada en token** -Hola webhook URI se guarda con un identificador de token, por ejemplo,`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`
2. **Autorización básica** -Hola webhook URI se guarda con un nombre de usuario y una contraseña, por ejemplo,`https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`

## <a name="payload-schema"></a>Esquema de carga
Hola operación POST contiene Hola después carga JSON y el esquema para todas las alertas de registro de actividad. Este esquema es similar toohello uno emplean alertas basadas en la métrica.

```
{
        "status": "Activated",
        "context": {
                "resourceProviderName": "Microsoft.Web",
                "event": {
                        "$type": "Microsoft.WindowsAzure.Management.Monitoring.Automation.Notifications.GenericNotifications.Datacontracts.InstanceEventContext, Microsoft.WindowsAzure.Management.Mon.Automation",
                        "authorization": {
                                "action": "Microsoft.Web/sites/start/action",
                                "scope": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest"
                        },
                        "eventDataId": "327caaca-08d7-41b1-86d8-27d0a7adb92d",
                        "category": "Administrative",
                        "caller": "myname@mycompany.com",
                        "httpRequest": {
                                "clientRequestId": "f58cead8-c9ed-43af-8710-55e64def208d",
                                "clientIpAddress": "104.43.166.155",
                                "method": "POST"
                        },
                        "status": "Succeeded",
                        "subStatus": "OK",
                        "level": "Informational",
                        "correlationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "eventDescription": "",
                        "operationName": "Microsoft.Web/sites/start/action",
                        "operationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "properties": {
                                "$type": "Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage",
                                "statusCode": "OK",
                                "serviceRequestId": "f7716681-496a-4f5c-8d14-d564bcf54714"
                        }
                },
                "timestamp": "Friday, March 11, 2016 9:13:23 PM",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/alertonevent2",
                "name": "alertonevent2",
                "description": "test alert on event start",
                "conditionType": "Event",
                "subscriptionId": "s1",
                "resourceId": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest",
                "resourceGroupName": "rg1"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```

| Nombre del elemento | Description |
| --- | --- |
| status |Usado para alertas de métrica. Siempre se establece demasiado "activado" para las alertas de registro de actividad. |
| contexto |Contexto de evento de Hola. |
| resourceProviderName |proveedor de recursos de Hola de hello afectado recursos. |
| conditionType |Siempre "Event" |
| name |Nombre de regla de alerta de Hola. |
| id |Id. de recurso de alerta de Hola. |
| description |Descripción de la alerta como conjunto durante la creación de alerta de Hola. |
| subscriptionId |Identificador de suscripción de Azure |
| timestamp |Hora a qué Hola se generó el evento por el servicio de Azure que procesa la solicitud de Hola Hola. |
| resourceId |Id. de recurso de hello afectado recursos. |
| resourceGroupName |Nombre de grupo de recursos de Hola Hola afectado recursos |
| propiedades |Conjunto de `<Key, Value>` pares (es decir, `Dictionary<String, String>`) que incluye detalles acerca del evento Hola. |
| event |Elemento que contiene metadatos acerca del evento Hola. |
| authorization |propiedades RBAC Hola de evento Hola. Generalmente incluyen hello hello, "role" y "acción de" "ámbito". |
| categoría |Categoría de eventos de Hola. Los valores admitidos son: Administrative, Alert, Security, ServiceHealth y Recommendation. |
| caller |Dirección de correo electrónico del usuario de Hola que realizó la operación de hello, notificación de UPN o notificación SPN según su disponibilidad. Puede ser null para ciertas llamadas del sistema. |
| correlationId |Normalmente, un GUID en formato de cadena. Eventos con correlationId pertenecen toohello misma acción mayor y normalmente comparten un correlationId. |
| eventDescription |Descripción de texto estático de evento Hola. |
| eventDataId |Identificador único para el evento de Hola. |
| eventSource |Nombre de Hola servicio de Azure o la infraestructura de ese evento Hola generado. |
| httpRequest |Normalmente incluye Estados valores de para saludo "clientRequestId", "clientIpAddress" y "method" (el método HTTP, por ejemplo, PUT). |
| level |Uno de hello siguientes valores: "Critical", "Error", "Warning", "Informational" y "Verbose". |
| operationId |Normalmente un GUID que se comparten entre eventos de hello correspondiente toosingle operación. |
| operationName |Nombre de operación de Hola. |
| propiedades |Propiedades de evento de Hola. |
| status |String. Estado de operación de Hola. Entre los valores habituales, se incluyen "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved". |
| subStatus |Normalmente incluye código de estado HTTP de Hola de llamada REST de hello correspondiente. También podría incluir otras cadenas que describen un subestado. Entre los valores de subestado habituales se incluyen OK (código de estado HTTP: 200), Created (código de estado HTTP: 201), Accepted (código de estado HTTP: 202), No Content (código de estado HTTP: 204), Bad Request (código de estado HTTP: 400), Not Found (código de estado HTTP: 404), Conflict (código de estado HTTP: 409), Internal Server Error (código de estado HTTP: 500), Service Unavailable (código de estado HTTP: 503) y Gateway Timeout (código de estado HTTP: 504) |

## <a name="next-steps"></a>Pasos siguientes
* [Obtener más información sobre Hola registro de actividad](monitoring-overview-activity-logs.md)
* [Ejecute scripts de Azure Automation (Runbooks) en alertas de Azure](http://go.microsoft.com/fwlink/?LinkId=627081)
* [Use la aplicación lógica toosend un SMS a través de Twilio de una alerta de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app). En este ejemplo es para las alertas métricas, pero podría ser modificado toowork con una alerta de registro de actividad.
* [Usar la aplicación lógica toosend un mensaje desde una alerta Azure demora](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app). En este ejemplo es para las alertas métricas, pero podría ser modificado toowork con una alerta de registro de actividad.
* [Usar la aplicación lógica toosend un tooan mensaje cola de Azure desde una alerta Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app). En este ejemplo es para las alertas métricas, pero podría ser modificado toowork con una alerta de registro de actividad.
