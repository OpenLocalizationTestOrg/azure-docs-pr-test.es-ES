---
title: "aaaConfigure webhooks en alertas de métrica de Azure | Documentos de Microsoft"
description: Redistribuir sistemas de alertas de Azure tooother distintas de Azure.
author: johnkemnetz
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 8b3ae540-1d19-4f3d-a635-376042f8a5bb
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: johnkem
ms.openlocfilehash: bc4153ccdcff41c5b9d3c081e59a1bf260d8a283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-webhook-on-an-azure-metric-alert"></a>Configuración de un webhook en una alerta de métrica de Azure
Webhooks le permiten tooroute un Azure sistemas de notificación de tooother para acciones posteriores al procesamiento o personalizados de alerta. Puede usar un webhook en una alerta tooroute se tooservices que enviar SMS, registrar errores, notificar a un equipo a través de servicios de chat/mensajería o realizar cualquier número de otras acciones. Este artículo se describe cómo tooset un webhook en una alerta de métrica de Azure y qué carga Hola Hola HTTP POST tooa webhook es similar. Para obtener información sobre el programa de instalación de Hola y el esquema de una alerta de registro de actividad de Azure (alerta de eventos), [vea esta página en su lugar](insights-auditlog-to-webhook-email.md).

Contenido de alerta de hello HTTP POST en formato JSON, alertas de Azure esquema define a continuación, tooa webhook URI que proporciona al crear la alerta de Hola. Este URI debe ser un punto de conexión HTTP o HTTPS válido. Azure envía una entrada por cada solicitud cuando se activa una alerta.

## <a name="configuring-webhooks-via-hello-portal"></a>Configuración de webhooks mediante el portal de Hola
Puede agregar o actualizar hello webhook URI en la pantalla de alertas de creación/actualización Hola Hola [portal](https://portal.azure.com/).

![Agregar una regla de alerta](./media/insights-webhooks-alerts/Alertwebhook.png)

También puede configurar un webhook de tooa toopost alerta URI mediante hello [Cmdlets de PowerShell de Azure](insights-powershell-samples.md#create-metric-alerts), [multiplataforma CLI](insights-cli-samples.md#work-with-alerts), o [API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/dn933805.aspx).

## <a name="authenticating-hello-webhook"></a>Autenticar hello webhook
Hola webhook se puedan autenticar con autorización basada en el símbolo (token). Hola webhook URI se guarda con un identificador de token, p. ej. `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`

## <a name="payload-schema"></a>Esquema de carga
Hola operación POST contiene Hola después carga JSON y el esquema para todas las alertas de métrica.

```JSON
{
"status": "Activated",
"context": {
            "timestamp": "2015-08-14T22:26:41.9975398Z",
            "id": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.insights/alertrules/ruleName1",
            "name": "ruleName1",
            "description": "some description",
            "conditionType": "Metric",
            "condition": {
                        "metricName": "Requests",
                        "metricUnit": "Count",
                        "metricValue": "10",
                        "threshold": "10",
                        "windowSize": "15",
                        "timeAggregation": "Average",
                        "operator": "GreaterThanOrEqual"
                },
            "subscriptionId": "s1",
            "resourceGroupName": "useast",                                
            "resourceName": "mysite1",
            "resourceType": "microsoft.foo/sites",
            "resourceId": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1",
            "resourceRegion": "centralus",
            "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1"
},
"properties": {
              "key1": "value1",
              "key2": "value2"
              }
}
```


| Campo | Obligatorio | Conjunto fijo de valores | Notas |
|:--- |:--- |:--- |:--- |
| status |Y |"Activado", "Resuelto" |Estado de alerta de hello en función de las condiciones de hello ha establecido. |
| contexto |Y | |contexto de alerta de Hola. |
| timestamp |Y | |hora de Hello en qué Hola se activó la alerta. |
| id |Y | |Cada regla de alerta tiene un id. único. |
| name |Y | |nombre de la alerta Hola. |
| description |Y | |Descripción de la alerta de Hola. |
| conditionType |Y |"Métrica", "Evento" |Se admiten dos tipos de alertas. Una basada en una condición de métrica y Hola otro basándose en un evento en el registro de actividad de Hola. Use este valor toocheck si alerta Hola se basa en la métrica o evento. |
| condition |Y | |Hola toocheck campos específicos para tomando como base conditionType Hola. |
| metricName |para alertas de métricas | |nombre de Hola de métrica de Hola que define qué regla Hola supervisa. |
| metricUnit |para alertas de métricas |"Bytes", "BytesPerSecond", "Count", "CountPerSecond", "Percent", "Seconds" |unidad de Hello permitido en la métrica de Hola. [Los valores permitidos aparecen aquí](https://msdn.microsoft.com/library/microsoft.azure.insights.models.unit.aspx). |
| metricValue |para alertas de métricas | |valor real de Hola de métrica de Hola que provocó la alerta Hola. |
| threshold |para alertas de métricas | |valor de umbral de Hello en qué Hola se activará la alerta. |
| windowSize |para alertas de métricas | |período de Hola de tiempo de actividad de alerta toomonitor utilizados en función de umbral de Hola. Debe estar comprendido entre 5 minutos y 1 día. Formato de duración ISO 8601. |
| timeAggregation |para alertas de métricas |"Average", "Last", "Maximum", "Minimum", "None", "Total" |¿Cómo se deben combinar datos de Hola que se recopilan con el tiempo. valor predeterminado de Hello es Media. [Los valores permitidos aparecen aquí](https://msdn.microsoft.com/library/microsoft.azure.insights.models.aggregationtype.aspx). |
| operator |para alertas de métricas | |Hola operador usado toocompare Hola actual datos métricos toohello umbral establecido. |
| subscriptionId |Y | |Identificador de suscripción de Azure |
| resourceGroupName |Y | |Nombre de grupo de recursos de Hola Hola afectado recursos. |
| resourceName |Y | |Nombre del recurso de hello afectado recursos. |
| resourceType |Y | |Tipo de recurso de hello afectado recursos. |
| resourceId |Y | |Id. de recurso de hello afectado recursos. |
| resourceRegion |Y | |Región o ubicación de hello afectado recursos. |
| portalLink |Y | |Página de resumen de vínculo directo toohello recursos portal. |
| propiedades |N |Opcional |Conjunto de `<Key, Value>` pares (es decir, `Dictionary<String, String>`) que incluye detalles acerca del evento Hola. campo de propiedades de Hello es opcional. En una interfaz de usuario o la lógica basada en la aplicación flujo de trabajo personalizado, los usuarios pueden especificar clave y valor que se pueden pasar a través de la carga de Hola. Hola forma alternativa toopass propiedades personalizadas toohello atrás webhook es a través de uri de webhook de hello propio (como parámetros de consulta) |

> [!NOTE]
> campo de propiedades de Hello solo puede establecerse utilizando hello [API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/dn933805.aspx).
>
>

## <a name="next-steps"></a>Pasos siguientes
* Obtener más información sobre alertas de Azure y webhook en vídeo de hello [integrar Azure Alerts con PagerDuty](http://go.microsoft.com/fwlink/?LinkId=627080)
* [Ejecute scripts de Azure Automation (Runbooks) en alertas de Azure](http://go.microsoft.com/fwlink/?LinkId=627081)
* [Use la aplicación lógica toosend un SMS a través de Twilio de una alerta de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
* [Use la aplicación lógica toosend un mensaje de demora de una alerta de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
* [Use la aplicación lógica toosend un tooan mensaje cola de Azure desde una alerta de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)
