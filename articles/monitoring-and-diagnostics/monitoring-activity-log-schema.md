---
title: Esquema de eventos de registro de actividad de aaaAzure | Documentos de Microsoft
description: Comprender el esquema de eventos de Hola para los datos que se emiten en hello registro de actividad
author: johnkemnetz
manager: robb
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: johnkem
ms.openlocfilehash: dfece949a20a4d9b4e8a4d488c1c34842d87d586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-activity-log-event-schema"></a>Esquema de eventos del registro de actividad de Azure
Hola **Azure Activity Log** es un registro que proporciona una visión general de los eventos de nivel de suscripción que se han producido en Azure. Este artículo describe el esquema de eventos de Hola por categoría de datos.

## <a name="administrative"></a>Administrativo
Esta categoría contiene el registro de hello de todos los cree, las operaciones update, delete y acción se realizan a través del Administrador de recursos. Ejemplos de hello tipos de eventos que aparecen en esta categoría se incluyen "creación la máquina virtual" y "eliminación grupo de seguridad de red" cada acción realizada por un usuario o aplicación con el Administrador de recursos se modela como una operación en un tipo de recurso determinado. Si el tipo de operación de hello es escribir, eliminar o acción, registros de Hola de inicio de Hola y el éxito o por error de esa operación se registran en la categoría administrativa Hola. categoría administrativa de Hello también incluye cualquier control de acceso basado en toorole cambios en una suscripción.

### <a name="sample-event"></a>Evento de ejemplo
```json
{
  "authorization": {
    "action": "microsoft.support/supporttickets/write",
    "role": "Subscription Admin",
    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
  },
  "caller": "admin@contoso.com",
  "channels": "Operation",
  "claims": {
    "aud": "https://management.core.windows.net/",
    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
    "iat": "1421876371",
    "nbf": "1421876371",
    "exp": "1421880271",
    "ver": "1.0",
    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
    "puid": "20030000801A118C",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
    "name": "John Smith",
    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
    "appidacr": "2",
    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
    "http://schemas.microsoft.com/claims/authnclassreference": "1"
  },
  "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "description": "",
  "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
  "eventName": {
    "value": "EndRequest",
    "localizedValue": "End request"
  },
  "httpRequest": {
    "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
    "clientIpAddress": "192.168.35.115",
    "method": "PUT"
  },
  "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
  "level": "Informational",
  "resourceGroupName": "MSSupportGroup",
  "resourceProviderName": {
    "value": "microsoft.support",
    "localizedValue": "microsoft.support"
  },
  "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
  "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "operationName": {
    "value": "microsoft.support/supporttickets/write",
    "localizedValue": "microsoft.support/supporttickets/write"
  },
  "properties": {
    "statusCode": "Created"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": "Created",
    "localizedValue": "Created (HTTP Status Code: 201)"
  },
  "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
  "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
  "subscriptionId": "s1"
}
```

### <a name="property-descriptions"></a>Descripciones de propiedades
| Nombre del elemento | Description |
| --- | --- |
| authorization |BLOB de propiedades de evento de hello RBAC. Normalmente incluye propiedades de "acción", "role" y "ámbito" Hola. |
| caller |Dirección de correo electrónico del usuario de Hola que ha realizado la operación de hello, notificación de UPN o notificación SPN según su disponibilidad. |
| canales nueva |Uno de hello siguientes valores: "Admin", "Operación" |
| claims |token de JWT de Hello usa Active Directory tooauthenticate Hola usuario o aplicación tooperform esta operación en Administrador de recursos. |
| correlationId |Normalmente un GUID en formato de cadena de Hola. Los eventos que comparten un correlationId pertenecen toohello misma acción. |
| description |Descripción de texto estático de un evento. |
| eventDataId |Identificador único de un evento. |
| httpRequest |Hola BLOB que se describe a solicitud Http. Normalmente incluye Estados valores de para saludo "clientRequestId", "clientIpAddress" y "method" (método HTTP. Por ejemplo, PUT). |
| level |Nivel de evento de Hola. Uno de hello siguientes valores: "Critical", "Error", "Warning", "Informational" y "Verbose" |
| resourceGroupName |Nombre de grupo de recursos de Hola Hola afectado recursos. |
| resourceProviderName |Nombre de proveedor de recursos de Hola para hello afectado recursos |
| resourceId |Id. de recurso de hello afectado recursos. |
| operationId |Un GUID que se comparten entre los eventos de Hola que corresponden tooa única operación. |
| operationName |Nombre de operación de Hola. |
| propiedades |Conjunto de `<Key, Value>` pares (es decir, un diccionario) que se describen los detalles de Hola de evento Hola. |
| status |Cadena que describe el estado de Hola de operación de Hola. Algunos valores habituales son: Started, In Progress, Succeeded, Failed, Active y Resolved. |
| subStatus |Normalmente Hola código de estado HTTP de hello correspondiente llamada REST, pero también puede incluir otras cadenas que describen un subestado, por ejemplo, estos valores comunes: Aceptar (código de estado HTTP: 200), creado (código de estado HTTP: 201), aceptado (código de estado HTTP: 202), sin contenido (HTTP Código de estado: 204), solicitud incorrecta (código de estado HTTP: 400), pero no se encontraron (código de estado HTTP: 404), conflicto (código de estado HTTP: 409), Error interno del servidor (código de estado HTTP: 500), servicio no está disponible (código de estado HTTP: 503), el tiempo de espera de puerta de enlace (código de estado HTTP: 504). |
| eventTimestamp |Marca de tiempo cuando se generan eventos de Hola Hola Hola de procesamiento de servicio de Azure solicitar evento Hola correspondiente. |
| submissionTimestamp |Marca de tiempo al evento Hola empezó a estar disponible para las consultas. |
| subscriptionId |Identificador de la suscripción de Azure. |

## <a name="service-health"></a>Estado del servicio
Esta categoría contiene el registro de hello de los incidentes de mantenimiento de servicio que se han producido en Azure. Un ejemplo de Hola tipo de evento que aparecen en esta categoría es "SQL Azure en este de EE. está experimentando tiempos de inactividad". Eventos de estado de servicio vienen en cinco variedades: acción requerida, recuperación asistida, incidente, mantenimiento, información o seguridad y sólo aparece si tiene un recurso de suscripción de Hola que podría verse afectada por los eventos de Hola.

### <a name="sample-event"></a>Evento de ejemplo
```json
{
  "channels": "Admin",
  "correlationId": "c550176b-8f52-4380-bdc5-36c1b59d3a44",
  "description": "Active: Network Infrastructure - UK South",
  "eventDataId": "c5bc4514-6642-2be3-453e-c6a67841b073",
  "eventName": {
      "value": null
  },
  "category": {
      "value": "ServiceHealth",
      "localizedValue": "Service Health"
  },
  "eventTimestamp": "2017-07-20T23:30:14.8022297Z",
  "id": "/subscriptions/mySubscriptionID/events/c5bc4514-6642-2be3-453e-c6a67841b073/ticks/636361902148022297",
  "level": "Warning",
  "operationName": {
      "value": "Microsoft.ServiceHealth/incident/action",
      "localizedValue": "Microsoft.ServiceHealth/incident/action"
  },
  "resourceProviderName": {
      "value": null
  },
  "resourceType": {
      "value": null,
      "localizedValue": ""
  },
  "resourceId": "/subscriptions/mySubscriptionID",
  "status": {
      "value": "Active",
      "localizedValue": "Active"
  },
  "subStatus": {
      "value": null
  },
  "submissionTimestamp": "2017-07-20T23:30:34.7431946Z",
  "subscriptionId": "mySubscriptionID",
  "properties": {
    "title": "Network Infrastructure - UK South",
    "service": "Service Fabric",
    "region": "UK South",
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a>Descripciones de propiedades
Nombre del elemento | Descripción
-------- | -----------
canales nueva | Es uno de hello siguientes valores: "Admin", "Operación"
correlationId | Suele ser un GUID en formato de cadena de Hola. Eventos que pertenecen toohello normalmente comparten la misma acción Hola mismo correlationId.
description | Descripción del evento de Hola.
eventDataId | Hola identificador único de un evento.
eventName | título de Hola de evento Hola.
level | Nivel de evento de Hola. Uno de hello siguientes valores: "Critical", "Error", "Warning", "Informational" y "Verbose"
resourceProviderName | Nombre de proveedor de recursos de Hola para hello afectado recursos. Si es desconocido, será null.
resourceType| tipo Hello del recurso de hello afectado recursos. Si es desconocido, será null.
subStatus | Normalmente es null para los eventos del estado del servicio.
eventTimestamp | Marca de tiempo cuando el evento del registro de hello se generó y envía toohello registro de actividad.
submissionTimestamp |   Marca de tiempo al evento de hello empezó a estar disponible en el registro de actividad de Hola.
subscriptionId | Hola suscripción de Azure en el que este evento se registra.
status | Cadena que describe el estado de Hola de operación de Hola. Algunos valores comunes: Activo y Resuelto.
operationName | Nombre de operación de Hola. Normalmente es Microsoft.ServiceHealth/incident/action.
categoría | "ServiceHealth"
resourceId | Id. de recurso de hello afectado el recurso, si se conoce. En caso contrario, se proporciona el identificador de suscripción.
Properties.title | título de Hello localizada para esta comunicación. Idioma predeterminado de hello es inglés.
Properties.communication | Hola localizado detalles de comunicación de hello con formato HTML. Idioma predeterminado de hello es inglés.
Properties.incidentType | Valores posibles: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security
Properties.trackingId | Identifica el incidente de hello que está asociado a este evento. Utilice este incidente de toocorrelate Hola eventos tooan relacionados.
Properties.impactedServices | Un escape blob JSON que describe los servicios de Hola y regiones que se ven afectadas por incidente Hola. Una lista de servicios, cada uno de los cuales tiene un valor ServiceName y una lista de ImpactedRegions, cada una de los cuales tiene un valor RegionName.
Properties.defaultLanguageTitle | comunicación de saludo en inglés
Properties.defaultLanguageContent | comunicación de saludo en inglés como marcado html o texto sin formato
Properties.stage | Valores posibles de AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security: Active y Resolved. En el caso de Maintenance son: Active, Planned, InProgress, Canceled, Rescheduled, Resolved y Complete
Properties.communicationId | comunicación de Hello este evento está asociado.

## <a name="alert"></a>Alerta
Esta categoría contiene el registro de hello de todas las activaciones de alertas de Azure. Un ejemplo de Hola tipo de evento que aparecen en esta categoría es "% de CPU en myVM ha sido por encima del 80 para hello últimos 5 minutos". Varios sistemas de Azure tienen un concepto de alerta: puede definir una regla de algún tipo y recibir una notificación cuando las condiciones coincidan con esa regla. Cada vez que un tipo de alerta de Azure compatible "se activa,' o hello las condiciones son toogenerate cumpla una notificación, un registro de la activación de hello también se inserta toothis categoría de hello registro de actividad.

### <a name="sample-event"></a>Evento de ejemplo

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in hello last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
  "eventDataId": "149d4baf-53dc-4cf4-9e29-17de37405cd9",
  "eventName": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "category": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle/events/149d4baf-53dc-4cf4-9e29-17de37405cd9/ticks/636362258535221920",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "Microsoft.ClassicCompute",
    "localizedValue": "Microsoft.ClassicCompute"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle",
  "resourceType": {
    "value": "Microsoft.ClassicCompute/domainNames/slots/roles",
    "localizedValue": "Microsoft.ClassicCompute/domainNames/slots/roles"
  },
  "operationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "operationName": {
    "value": "Microsoft.Insights/AlertRules/Resolved/Action",
    "localizedValue": "Microsoft.Insights/AlertRules/Resolved/Action"
  },
  "properties": {
    "RuleUri": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert",
    "RuleName": "myalert",
    "RuleDescription": "",
    "Threshold": "100000",
    "WindowSizeInMinutes": "5",
    "Aggregation": "Average",
    "Operator": "LessThan",
    "MetricName": "Disk read",
    "MetricUnit": "Count"
  },
  "status": {
    "value": "Resolved",
    "localizedValue": "Resolved"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T09:24:13.522192Z",
  "submissionTimestamp": "2017-07-21T09:24:15.6578651Z",
  "subscriptionId": "mySubscriptionID"
}
```

### <a name="property-descriptions"></a>Descripciones de propiedades
| Nombre del elemento | Descripción |
| --- | --- |
| caller | Siempre es Microsoft.Insights/alertRules. |
| canales nueva | Siempre es "Admin, Operation". |
| claims | Blob JSON con el tipo SPN (nombre principal de servicio), o recurso hello, del motor de alertas de Hola. |
| correlationId | Un GUID en formato de cadena de Hola. |
| description |Descripción de texto estático de evento de alerta de Hola. |
| eventDataId |Identificador único del evento de alerta de Hola. |
| level |Nivel de evento de Hola. Uno de hello siguientes valores: "Critical", "Error", "Warning", "Informational" y "Verbose" |
| resourceGroupName |Nombre de grupo de recursos de Hola Hola afectada recursos si se trata de una alerta de métrica. Para otros tipos de alerta, trata el nombre de Hola Hola del grupo de recursos que contiene la alerta de hello propio. |
| resourceProviderName |Nombre de proveedor de recursos de Hola para hello afectado recursos si se trata de una alerta de métrica. Para otros tipos de alerta, trata Hola nombre de proveedor de recursos de Hola Hola propia lista de alertas. |
| resourceId | Nombre de Id. de recurso de Hola para hello afectado recursos si se trata de una alerta de métrica. Para otros tipos de alerta, se trata de hello Id. de recurso de recurso alerta hello en Sí. |
| operationId |Un GUID que se comparten entre los eventos de Hola que corresponden tooa única operación. |
| operationName |Nombre de operación de Hola. |
| propiedades |Conjunto de `<Key, Value>` pares (es decir, un diccionario) que se describen los detalles de Hola de evento Hola. |
| status |Cadena que describe el estado de Hola de operación de Hola. Algunos valores habituales son: Started, In Progress, Succeeded, Failed, Active y Resolved. |
| subStatus | Normalmente es null para las alertas. |
| eventTimestamp |Marca de tiempo cuando se generan eventos de Hola Hola Hola de procesamiento de servicio de Azure solicitar evento Hola correspondiente. |
| submissionTimestamp |Marca de tiempo al evento Hola empezó a estar disponible para las consultas. |
| subscriptionId |Identificador de la suscripción de Azure. |

### <a name="properties-field-per-alert-type"></a>Campo Propiedades por tipo de alerta
campo de propiedades de Hello contendrá diferentes valores en función del origen de Hola de evento de alerta de Hola. Dos proveedores de eventos de alerta comunes son las alertas de registro de actividad y las alertas de métrica.

#### <a name="properties-for-activity-log-alerts"></a>Propiedades de las alertas del registro de actividad
| Nombre del elemento | Descripción |
| --- | --- |
| properties.subscriptionId | Hola Id. de suscripción de evento de registro de actividad de Hola que produjo este toobe de regla de alerta de registro de actividad activa. |
| properties.eventDataId | Hola datos Id. de evento del evento de registro de actividad de Hola que produjo este toobe de regla de alerta de registro de actividad activa. |
| properties.resourceGroup | grupo de recursos de Hola de evento de registro de actividad de Hola que produjo este toobe de regla de alerta de registro de actividad activa. |
| properties.resourceId | Identificador de recurso de Hola de evento de registro de actividad de Hola que produjo este toobe de regla de alerta de registro de actividad activa. |
| properties.eventTimestamp | Hola marca de tiempo de evento del evento de registro de actividad de Hola que produjo este toobe de regla de alerta de registro de actividad activa. |
| properties.operationName | nombre de la operación de Hola de evento de registro de actividad de Hola que produjo este toobe de regla de alerta de registro de actividad activa. |
| properties.status | estado de Hola de evento de registro de actividad de Hola que produjo este toobe de regla de alerta de registro de actividad activa.|

#### <a name="properties-for-metric-alerts"></a>Propiedades de las alertas de métrica
| Nombre del elemento | Descripción |
| --- | --- |
| properties.RuleUri | Id. de recurso de métrica regla de alerta Hola propio. |
| properties.RuleName | nombre de Hola de regla de alerta métrica Hola. |
| properties.RuleDescription | Descripción de Hola de regla de alerta de hello métrica (tal y como se define en la regla de alerta de hello). |
| properties.Threshold | valor de umbral de Hello use en la evaluación de Hola de regla de alerta métrica Hola. |
| properties.WindowSizeInMinutes | Use en la evaluación de Hola de regla de alerta métrica Hola el tamaño de la ventana de Hola. |
| properties.Aggregation | tipo de agregación de Hello definido en la regla de alerta métrica Hola. |
| properties.Operator | operador condicional de Hola usado en la evaluación de Hola de regla de alerta de métrica de Hola. |
| properties.MetricName | nombre de la métrica de Hola de métrica de hello utilizada en la evaluación de Hola de regla de alerta métrica Hola. |
| properties.MetricUnit | Hola métrica unidad métrica de hello utilizada en la evaluación de Hola de regla de alerta métrica Hola. |

## <a name="autoscale"></a>Autoscale
Esta categoría contiene registro de hello de cualquier operación de toohello relacionados de eventos del motor de escalado automático de hello en función de cualquier configuración de escalado automático que ha definido en su suscripción. Un ejemplo de Hola tipo de evento que aparecen en esta categoría es "Escalado automático ampliación vertical error en la acción". Usar el escalado automático, automáticamente puede escalar horizontalmente o escalar en hello número de instancias de un tipo de recurso compatible se basa en la hora del día y carga datos (métricas) con una configuración de escalado automático. Cuando se cumplen las condiciones de hello tooscale hacia arriba o hacia abajo, Hola inicio y se ha realizado correctamente o eventos de error se registrará en esta categoría.

### <a name="sample-event"></a>Evento de ejemplo
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
  "eventDataId": "a5b92075-1de9-42f1-b52e-6f3e4945a7c7",
  "eventName": {
    "value": "AutoscaleAction",
    "localizedValue": "AutoscaleAction"
  },
  "category": {
    "value": "Autoscale",
    "localizedValue": "Autoscale"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup/events/a5b92075-1de9-42f1-b52e-6f3e4945a7c7/ticks/636361956518681572",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "microsoft.insights",
    "localizedValue": "microsoft.insights"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup",
  "resourceType": {
    "value": "microsoft.insights/autoscalesettings",
    "localizedValue": "microsoft.insights/autoscalesettings"
  },
  "operationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "operationName": {
    "value": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action",
    "localizedValue": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action"
  },
  "properties": {
    "Description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
    "ResourceName": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource",
    "OldInstancesCount": "3",
    "NewInstancesCount": "2",
    "LastScaleActionTime": "Fri, 21 Jul 2017 01:00:51 GMT"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T01:00:51.8681572Z",
  "submissionTimestamp": "2017-07-21T01:00:52.3008754Z",
  "subscriptionId": "mySubscriptionID"
}

```

### <a name="property-descriptions"></a>Descripciones de propiedades
| Nombre del elemento | Descripción |
| --- | --- |
| caller | Siempre es Microsoft.Insights/autoscaleSettings. |
| canales nueva | Siempre es "Admin, Operation". |
| claims | Blob JSON con hello tipo SPN (nombre principal de servicio), o el recurso, de motor de escalado automático de Hola. |
| correlationId | Un GUID en formato de cadena de Hola. |
| description |Descripción de texto estático de evento de escalado automático de Hola. |
| eventDataId |Identificador único del evento de escalado automático de Hola. |
| level |Nivel de evento de Hola. Uno de hello siguientes valores: "Critical", "Error", "Warning", "Informational" y "Verbose" |
| resourceGroupName |Nombre del grupo de recursos de Hola para configuración de escalado automático de Hola. |
| resourceProviderName |Nombre del proveedor de recursos de hello para la configuración de escalado automático de Hola. |
| resourceId |Id. de recurso de configuración de escalado automático de Hola. |
| operationId |Un GUID que se comparten entre los eventos de Hola que corresponden tooa única operación. |
| operationName |Nombre de operación de Hola. |
| propiedades |Conjunto de `<Key, Value>` pares (es decir, un diccionario) que se describen los detalles de Hola de evento Hola. |
| properties.Description | Descripción detallada de qué motor de escalado automático de hello hacía. |
| properties.ResourceName | Id. de recurso de hello afectado recursos (hello en qué Hola se estaba realizando la acción de escalado de recursos) |
| properties.OldInstancesCount | número de Hola de instancias antes de la acción de escalado automático de hello entra en vigor. |
| properties.NewInstancesCount | número de Hola de instancias después de la acción de escalado automático de hello entra en vigor. |
| properties.LastScaleActionTime | marca de tiempo de Hola de cuando se produjo la acción de escalado automático de Hola. |
| status |Cadena que describe el estado de Hola de operación de Hola. Algunos valores habituales son: Started, In Progress, Succeeded, Failed, Active y Resolved. |
| subStatus | Normalmente es null para el escalado automático. |
| eventTimestamp |Marca de tiempo cuando se generan eventos de Hola Hola Hola de procesamiento de servicio de Azure solicitar evento Hola correspondiente. |
| submissionTimestamp |Marca de tiempo al evento Hola empezó a estar disponible para las consultas. |
| subscriptionId |Identificador de la suscripción de Azure. |

## <a name="next-steps"></a>Pasos siguientes
* [Obtener más información sobre Hola registro de actividad (anteriormente registros de auditoría)](monitoring-overview-activity-logs.md)
* [Transmitir hello Azure Activity Log tooEvent centros](monitoring-stream-activity-logs-event-hubs.md)
