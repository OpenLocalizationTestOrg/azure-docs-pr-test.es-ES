---
title: Comprender el esquema de webhook usado en las alertas del registro de actividad | Microsoft Docs
description: "Obtenga información acerca del esquema del archivo JSON que se publica en una dirección URL de webhook cuando se activa una alerta del registro de actividad."
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
ms.openlocfilehash: 75c71bcd16573d4f4dd3377c623aa9b414aa3906
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="03644-103">Webhooks para alertas del registro de actividad de Azure</span><span class="sxs-lookup"><span data-stu-id="03644-103">Webhooks for Azure activity log alerts</span></span>
<span data-ttu-id="03644-104">Como parte de la definición de un grupo de acciones, se pueden configurar puntos de conexión de webhook para recibir notificaciones de alertas del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="03644-104">As part of the definition of an action group, you can configure webhook endpoints to receive activity log alert notifications.</span></span> <span data-ttu-id="03644-105">Los webhooks permiten enrutar estas notificaciones a otros sistemas para su procesamiento posterior o acciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="03644-105">With webhooks, you can route these notifications to other systems for post-processing or custom actions.</span></span> <span data-ttu-id="03644-106">Este artículo muestra el aspecto de la carga útil para HTTP POST a un webhook.</span><span class="sxs-lookup"><span data-stu-id="03644-106">This article shows what the payload for the HTTP POST to a webhook looks like.</span></span>

<span data-ttu-id="03644-107">Para más información sobre las alertas del registro de actividad, consulte cómo [crear alertas del registro de actividad de Azure](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="03644-107">For more information on activity log alerts, see how to [create Azure activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="03644-108">Para obtener información sobre los grupos de acciones, consulte cómo [crear grupos de acciones](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="03644-108">For information on action groups, see how to [create action groups](monitoring-action-groups.md).</span></span>

## <a name="authenticate-the-webhook"></a><span data-ttu-id="03644-109">Autenticación del webhook</span><span class="sxs-lookup"><span data-stu-id="03644-109">Authenticate the webhook</span></span>
<span data-ttu-id="03644-110">El webhook puede usar opcionalmente autorización basada en token para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="03644-110">The webhook can optionally use token-based authorization for authentication.</span></span> <span data-ttu-id="03644-111">El identificador URI del webhook se guarda con un identificador de token, por ejemplo, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span><span class="sxs-lookup"><span data-stu-id="03644-111">The webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span></span>

## <a name="payload-schema"></a><span data-ttu-id="03644-112">Esquema de carga</span><span class="sxs-lookup"><span data-stu-id="03644-112">Payload schema</span></span>
<span data-ttu-id="03644-113">La carga útil JSON incluida en la operación POST difiere según el campo data.context.activityLog.eventSource de la carga útil.</span><span class="sxs-lookup"><span data-stu-id="03644-113">The JSON payload contained in the POST operation differs based on the payload's data.context.activityLog.eventSource field.</span></span>

###<a name="common"></a><span data-ttu-id="03644-114">Común</span><span class="sxs-lookup"><span data-stu-id="03644-114">Common</span></span>
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
###<a name="administrative"></a><span data-ttu-id="03644-115">Administrativo</span><span class="sxs-lookup"><span data-stu-id="03644-115">Administrative</span></span>
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
###<a name="servicehealth"></a><span data-ttu-id="03644-116">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="03644-116">ServiceHealth</span></span>
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

<span data-ttu-id="03644-117">Para obtener detalles del esquema específico sobre alertas del registro de actividad de notificaciones de mantenimiento del servicio, consulte [Notificaciones de mantenimiento del servicio](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="03644-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span></span>

<span data-ttu-id="03644-118">Para obtener información del esquema específico en todas las otras alertas del registro de actividad, consulte [Información general sobre el registro de actividad de Azure](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="03644-118">For specific schema details on all other activity log alerts, see [Overview of the Azure activity log](monitoring-overview-activity-logs.md).</span></span>

| <span data-ttu-id="03644-119">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="03644-119">Element name</span></span> | <span data-ttu-id="03644-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="03644-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="03644-121">status</span><span class="sxs-lookup"><span data-stu-id="03644-121">status</span></span> |<span data-ttu-id="03644-122">Usado para alertas de métrica.</span><span class="sxs-lookup"><span data-stu-id="03644-122">Used for metric alerts.</span></span> <span data-ttu-id="03644-123">Siempre se establece en "activated" para las alertas del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="03644-123">Always set to "activated" for activity log alerts.</span></span> |
| <span data-ttu-id="03644-124">contexto</span><span class="sxs-lookup"><span data-stu-id="03644-124">context</span></span> |<span data-ttu-id="03644-125">Contexto del evento</span><span class="sxs-lookup"><span data-stu-id="03644-125">Context of the event.</span></span> |
| <span data-ttu-id="03644-126">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="03644-126">resourceProviderName</span></span> |<span data-ttu-id="03644-127">Proveedor de recursos del recurso afectado</span><span class="sxs-lookup"><span data-stu-id="03644-127">The resource provider of the impacted resource.</span></span> |
| <span data-ttu-id="03644-128">conditionType</span><span class="sxs-lookup"><span data-stu-id="03644-128">conditionType</span></span> |<span data-ttu-id="03644-129">Siempre "Event"</span><span class="sxs-lookup"><span data-stu-id="03644-129">Always "Event."</span></span> |
| <span data-ttu-id="03644-130">name</span><span class="sxs-lookup"><span data-stu-id="03644-130">name</span></span> |<span data-ttu-id="03644-131">Nombre de la regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="03644-131">Name of the alert rule.</span></span> |
| <span data-ttu-id="03644-132">id</span><span class="sxs-lookup"><span data-stu-id="03644-132">id</span></span> |<span data-ttu-id="03644-133">Identificador de recurso de la alerta</span><span class="sxs-lookup"><span data-stu-id="03644-133">Resource ID of the alert.</span></span> |
| <span data-ttu-id="03644-134">description</span><span class="sxs-lookup"><span data-stu-id="03644-134">description</span></span> |<span data-ttu-id="03644-135">Descripción de la alerta establecida al crear la alerta.</span><span class="sxs-lookup"><span data-stu-id="03644-135">Alert description set when the alert is created.</span></span> |
| <span data-ttu-id="03644-136">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="03644-136">subscriptionId</span></span> |<span data-ttu-id="03644-137">Identificador de suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="03644-137">Azure subscription ID.</span></span> |
| <span data-ttu-id="03644-138">timestamp</span><span class="sxs-lookup"><span data-stu-id="03644-138">timestamp</span></span> |<span data-ttu-id="03644-139">Cuándo generó el evento el servicio de Azure que procesó la solicitud</span><span class="sxs-lookup"><span data-stu-id="03644-139">Time at which the event was generated by the Azure service that processed the request.</span></span> |
| <span data-ttu-id="03644-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="03644-140">resourceId</span></span> |<span data-ttu-id="03644-141">Identificador de recurso del recurso afectado.</span><span class="sxs-lookup"><span data-stu-id="03644-141">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="03644-142">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="03644-142">resourceGroupName</span></span> |<span data-ttu-id="03644-143">Nombre del grupo de recursos del recurso afectado.</span><span class="sxs-lookup"><span data-stu-id="03644-143">Name of the resource group for the impacted resource.</span></span> |
| <span data-ttu-id="03644-144">propiedades</span><span class="sxs-lookup"><span data-stu-id="03644-144">properties</span></span> |<span data-ttu-id="03644-145">Conjunto de pares `<Key, Value>` (es decir, `Dictionary<String, String>`) que incluye detalles sobre el evento.</span><span class="sxs-lookup"><span data-stu-id="03644-145">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about the event.</span></span> |
| <span data-ttu-id="03644-146">event</span><span class="sxs-lookup"><span data-stu-id="03644-146">event</span></span> |<span data-ttu-id="03644-147">Elemento que contiene metadatos sobre el evento.</span><span class="sxs-lookup"><span data-stu-id="03644-147">Element that contains metadata about the event.</span></span> |
| <span data-ttu-id="03644-148">authorization</span><span class="sxs-lookup"><span data-stu-id="03644-148">authorization</span></span> |<span data-ttu-id="03644-149">Las propiedades del Control de acceso basado en rol del evento.</span><span class="sxs-lookup"><span data-stu-id="03644-149">The Role-Based Access Control properties of the event.</span></span> <span data-ttu-id="03644-150">Estas propiedades normalmente incluyen la acción, el rol y el ámbito.</span><span class="sxs-lookup"><span data-stu-id="03644-150">These properties usually include the action, the role, and the scope.</span></span> |
| <span data-ttu-id="03644-151">categoría</span><span class="sxs-lookup"><span data-stu-id="03644-151">category</span></span> |<span data-ttu-id="03644-152">Categoría del evento.</span><span class="sxs-lookup"><span data-stu-id="03644-152">Category of the event.</span></span> <span data-ttu-id="03644-153">Los valores admitidos incluyen: Administrative, Alert, Security, ServiceHealth y Recommendation.</span><span class="sxs-lookup"><span data-stu-id="03644-153">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span></span> |
| <span data-ttu-id="03644-154">caller</span><span class="sxs-lookup"><span data-stu-id="03644-154">caller</span></span> |<span data-ttu-id="03644-155">Dirección de correo electrónico del usuario que realizó la operación, la notificación de UPN o la notificación de SPN basada en la disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="03644-155">Email address of the user who performed the operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="03644-156">Puede ser null para ciertas llamadas del sistema.</span><span class="sxs-lookup"><span data-stu-id="03644-156">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="03644-157">correlationId</span><span class="sxs-lookup"><span data-stu-id="03644-157">correlationId</span></span> |<span data-ttu-id="03644-158">Normalmente, un GUID en formato de cadena.</span><span class="sxs-lookup"><span data-stu-id="03644-158">Usually a GUID in string format.</span></span> <span data-ttu-id="03644-159">Los eventos con correlationId pertenecen a la misma acción de mayor tamaño y suelen compartir un campo correlationId.</span><span class="sxs-lookup"><span data-stu-id="03644-159">Events with correlationId belong to the same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="03644-160">eventDescription</span><span class="sxs-lookup"><span data-stu-id="03644-160">eventDescription</span></span> |<span data-ttu-id="03644-161">Descripción de texto estático del evento</span><span class="sxs-lookup"><span data-stu-id="03644-161">Static text description of the event.</span></span> |
| <span data-ttu-id="03644-162">eventDataId</span><span class="sxs-lookup"><span data-stu-id="03644-162">eventDataId</span></span> |<span data-ttu-id="03644-163">Identificador único para el evento</span><span class="sxs-lookup"><span data-stu-id="03644-163">Unique identifier for the event.</span></span> |
| <span data-ttu-id="03644-164">eventSource</span><span class="sxs-lookup"><span data-stu-id="03644-164">eventSource</span></span> |<span data-ttu-id="03644-165">Nombre de la infraestructura o el servicio de Azure que generó el evento</span><span class="sxs-lookup"><span data-stu-id="03644-165">Name of the Azure service or infrastructure that generated the event.</span></span> |
| <span data-ttu-id="03644-166">httpRequest</span><span class="sxs-lookup"><span data-stu-id="03644-166">httpRequest</span></span> |<span data-ttu-id="03644-167">La solicitud normalmente incluye clientRequestId, clientIpAddress y el método HTTP (por ejemplo, PUT).</span><span class="sxs-lookup"><span data-stu-id="03644-167">The request usually includes the clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span></span> |
| <span data-ttu-id="03644-168">level</span><span class="sxs-lookup"><span data-stu-id="03644-168">level</span></span> |<span data-ttu-id="03644-169">Uno de los siguientes valores: Critical, Error, Warning, Informational y Verbose.</span><span class="sxs-lookup"><span data-stu-id="03644-169">One of the following values: Critical, Error, Warning, Informational, and Verbose.</span></span> |
| <span data-ttu-id="03644-170">operationId</span><span class="sxs-lookup"><span data-stu-id="03644-170">operationId</span></span> |<span data-ttu-id="03644-171">Por lo general, un GUID compartido entre los eventos correspondientes a una sola operación</span><span class="sxs-lookup"><span data-stu-id="03644-171">Usually a GUID shared among the events corresponding to single operation.</span></span> |
| <span data-ttu-id="03644-172">operationName</span><span class="sxs-lookup"><span data-stu-id="03644-172">operationName</span></span> |<span data-ttu-id="03644-173">Nombre de la operación.</span><span class="sxs-lookup"><span data-stu-id="03644-173">Name of the operation.</span></span> |
| <span data-ttu-id="03644-174">propiedades</span><span class="sxs-lookup"><span data-stu-id="03644-174">properties</span></span> |<span data-ttu-id="03644-175">Propiedades del evento.</span><span class="sxs-lookup"><span data-stu-id="03644-175">Properties of the event.</span></span> |
| <span data-ttu-id="03644-176">status</span><span class="sxs-lookup"><span data-stu-id="03644-176">status</span></span> |<span data-ttu-id="03644-177">String.</span><span class="sxs-lookup"><span data-stu-id="03644-177">String.</span></span> <span data-ttu-id="03644-178">Estado de la operación.</span><span class="sxs-lookup"><span data-stu-id="03644-178">Status of the operation.</span></span> <span data-ttu-id="03644-179">Entre los valores habituales, se incluyen Started, In Progress, Succeeded, Failed, Active y Resolved.</span><span class="sxs-lookup"><span data-stu-id="03644-179">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span></span> |
| <span data-ttu-id="03644-180">subStatus</span><span class="sxs-lookup"><span data-stu-id="03644-180">subStatus</span></span> |<span data-ttu-id="03644-181">Normalmente, incluye el código de estado HTTP de la llamada de REST correspondiente.</span><span class="sxs-lookup"><span data-stu-id="03644-181">Usually includes the HTTP status code of the corresponding REST call.</span></span> <span data-ttu-id="03644-182">También podría incluir otras cadenas que describen un subestado.</span><span class="sxs-lookup"><span data-stu-id="03644-182">It might also include other strings that describe a substatus.</span></span> <span data-ttu-id="03644-183">Entre los valores de subestado habituales se incluyen OK (código de estado HTTP: 200), Created (código de estado HTTP: 201), Accepted (código de estado HTTP: 202), No Content (código de estado HTTP: 204), Bad Request (código de estado HTTP: 400), Not Found (código de estado HTTP: 404), Conflict (código de estado HTTP: 409), Internal Server Error (código de estado HTTP: 500), Service Unavailable (código de estado HTTP: 503) y Gateway Timeout (código de estado HTTP: 504).</span><span class="sxs-lookup"><span data-stu-id="03644-183">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="03644-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="03644-184">Next steps</span></span>
* <span data-ttu-id="03644-185">[Más información sobre el registro de actividad](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="03644-185">[Learn more about the activity log](monitoring-overview-activity-logs.md).</span></span>
* <span data-ttu-id="03644-186">[Ejecución de scripts de Azure Automation (runbooks) en alertas de Azure](http://go.microsoft.com/fwlink/?LinkId=627081).</span><span class="sxs-lookup"><span data-stu-id="03644-186">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span></span>
* <span data-ttu-id="03644-187">[Uso de una aplicación lógica para enviar un SMS a través de Twilio desde una alerta de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="03644-187">[Use a logic app to send an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="03644-188">Este ejemplo es para alertas de métrica, pero podría modificarse para funcionar con una alerta del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="03644-188">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
* <span data-ttu-id="03644-189">[Uso de una aplicación lógica para enviar un mensaje de Slack desde una alerta de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="03644-189">[Use a logic app to send a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="03644-190">Este ejemplo es para alertas de métrica, pero podría modificarse para funcionar con una alerta del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="03644-190">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
* <span data-ttu-id="03644-191">[Uso de una aplicación lógica para enviar un mensaje a una cola de Azure desde una alerta de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="03644-191">[Use a logic app to send a message to an Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="03644-192">Este ejemplo es para alertas de métrica, pero podría modificarse para funcionar con una alerta del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="03644-192">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
