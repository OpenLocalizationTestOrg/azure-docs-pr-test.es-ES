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
# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="ca367-103">Webhooks para alertas del registro de actividad de Azure</span><span class="sxs-lookup"><span data-stu-id="ca367-103">Webhooks for Azure activity log alerts</span></span>
<span data-ttu-id="ca367-104">Como parte de la definición de Hola de un grupo de acciones, puede configurar notificaciones de alerta de webhook extremos tooreceive actividad registro.</span><span class="sxs-lookup"><span data-stu-id="ca367-104">As part of hello definition of an action group, you can configure webhook endpoints tooreceive activity log alert notifications.</span></span> <span data-ttu-id="ca367-105">Con webhooks, es posible distribuir estos sistemas de tooother notificaciones para las acciones posteriores al procesamiento o personalizados.</span><span class="sxs-lookup"><span data-stu-id="ca367-105">With webhooks, you can route these notifications tooother systems for post-processing or custom actions.</span></span> <span data-ttu-id="ca367-106">Este artículo muestra qué carga Hola Hola HTTP POST tooa webhook aspecto.</span><span class="sxs-lookup"><span data-stu-id="ca367-106">This article shows what hello payload for hello HTTP POST tooa webhook looks like.</span></span>

<span data-ttu-id="ca367-107">Para obtener más información sobre las alertas de registro de actividad, vea cómo demasiado[crear alertas de registro de actividad de Azure](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="ca367-107">For more information on activity log alerts, see how too[create Azure activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="ca367-108">Para obtener información sobre grupos de acciones, vea cómo demasiado[crear grupos de acciones](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="ca367-108">For information on action groups, see how too[create action groups](monitoring-action-groups.md).</span></span>

## <a name="authenticate-hello-webhook"></a><span data-ttu-id="ca367-109">Autenticar hello webhook</span><span class="sxs-lookup"><span data-stu-id="ca367-109">Authenticate hello webhook</span></span>
<span data-ttu-id="ca367-110">Hola webhook puede utilizar opcionalmente la autorización basada en el símbolo (token) para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="ca367-110">hello webhook can optionally use token-based authorization for authentication.</span></span> <span data-ttu-id="ca367-111">Hola webhook URI se guarda con un identificador de token, por ejemplo, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span><span class="sxs-lookup"><span data-stu-id="ca367-111">hello webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span></span>

## <a name="payload-schema"></a><span data-ttu-id="ca367-112">Esquema de carga</span><span class="sxs-lookup"><span data-stu-id="ca367-112">Payload schema</span></span>
<span data-ttu-id="ca367-113">carga JSON de Hello contenido en hello operación POST difiere según el en el campo de data.context.activityLog.eventSource de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca367-113">hello JSON payload contained in hello POST operation differs based on hello payload's data.context.activityLog.eventSource field.</span></span>

###<a name="common"></a><span data-ttu-id="ca367-114">Común</span><span class="sxs-lookup"><span data-stu-id="ca367-114">Common</span></span>
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
###<a name="administrative"></a><span data-ttu-id="ca367-115">Administrativo</span><span class="sxs-lookup"><span data-stu-id="ca367-115">Administrative</span></span>
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
###<a name="servicehealth"></a><span data-ttu-id="ca367-116">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="ca367-116">ServiceHealth</span></span>
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

<span data-ttu-id="ca367-117">Para obtener detalles del esquema específico sobre alertas del registro de actividad de notificaciones de mantenimiento del servicio, consulte [Notificaciones de mantenimiento del servicio](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="ca367-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span></span>

<span data-ttu-id="ca367-118">Para obtener información de esquema específico en todas las otras alertas de registro de actividad, consulte [información general sobre el registro de actividad de Azure de hello](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="ca367-118">For specific schema details on all other activity log alerts, see [Overview of hello Azure activity log](monitoring-overview-activity-logs.md).</span></span>

| <span data-ttu-id="ca367-119">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="ca367-119">Element name</span></span> | <span data-ttu-id="ca367-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="ca367-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ca367-121">status</span><span class="sxs-lookup"><span data-stu-id="ca367-121">status</span></span> |<span data-ttu-id="ca367-122">Usado para alertas de métrica.</span><span class="sxs-lookup"><span data-stu-id="ca367-122">Used for metric alerts.</span></span> <span data-ttu-id="ca367-123">Siempre se establece demasiado "activado" para las alertas de registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="ca367-123">Always set too"activated" for activity log alerts.</span></span> |
| <span data-ttu-id="ca367-124">contexto</span><span class="sxs-lookup"><span data-stu-id="ca367-124">context</span></span> |<span data-ttu-id="ca367-125">Contexto de evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca367-125">Context of hello event.</span></span> |
| <span data-ttu-id="ca367-126">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="ca367-126">resourceProviderName</span></span> |<span data-ttu-id="ca367-127">proveedor de recursos de Hola de hello afectado recursos.</span><span class="sxs-lookup"><span data-stu-id="ca367-127">hello resource provider of hello impacted resource.</span></span> |
| <span data-ttu-id="ca367-128">conditionType</span><span class="sxs-lookup"><span data-stu-id="ca367-128">conditionType</span></span> |<span data-ttu-id="ca367-129">Siempre "Event"</span><span class="sxs-lookup"><span data-stu-id="ca367-129">Always "Event."</span></span> |
| <span data-ttu-id="ca367-130">name</span><span class="sxs-lookup"><span data-stu-id="ca367-130">name</span></span> |<span data-ttu-id="ca367-131">Nombre de regla de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca367-131">Name of hello alert rule.</span></span> |
| <span data-ttu-id="ca367-132">id</span><span class="sxs-lookup"><span data-stu-id="ca367-132">id</span></span> |<span data-ttu-id="ca367-133">Id. de recurso de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca367-133">Resource ID of hello alert.</span></span> |
| <span data-ttu-id="ca367-134">description</span><span class="sxs-lookup"><span data-stu-id="ca367-134">description</span></span> |<span data-ttu-id="ca367-135">Descripción de la alerta establece cuando se crea la alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca367-135">Alert description set when hello alert is created.</span></span> |
| <span data-ttu-id="ca367-136">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="ca367-136">subscriptionId</span></span> |<span data-ttu-id="ca367-137">Identificador de suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="ca367-137">Azure subscription ID.</span></span> |
| <span data-ttu-id="ca367-138">timestamp</span><span class="sxs-lookup"><span data-stu-id="ca367-138">timestamp</span></span> |<span data-ttu-id="ca367-139">Hora a qué Hola se generó el evento por el servicio de Azure que procesa la solicitud de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="ca367-139">Time at which hello event was generated by hello Azure service that processed hello request.</span></span> |
| <span data-ttu-id="ca367-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="ca367-140">resourceId</span></span> |<span data-ttu-id="ca367-141">Id. de recurso de hello afectado recursos.</span><span class="sxs-lookup"><span data-stu-id="ca367-141">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="ca367-142">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="ca367-142">resourceGroupName</span></span> |<span data-ttu-id="ca367-143">Nombre de grupo de recursos de Hola Hola afectado recursos.</span><span class="sxs-lookup"><span data-stu-id="ca367-143">Name of hello resource group for hello impacted resource.</span></span> |
| <span data-ttu-id="ca367-144">propiedades</span><span class="sxs-lookup"><span data-stu-id="ca367-144">properties</span></span> |<span data-ttu-id="ca367-145">Conjunto de `<Key, Value>` pares (es decir, `Dictionary<String, String>`) que incluye detalles acerca del evento Hola.</span><span class="sxs-lookup"><span data-stu-id="ca367-145">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about hello event.</span></span> |
| <span data-ttu-id="ca367-146">event</span><span class="sxs-lookup"><span data-stu-id="ca367-146">event</span></span> |<span data-ttu-id="ca367-147">Elemento que contiene metadatos acerca del evento Hola.</span><span class="sxs-lookup"><span data-stu-id="ca367-147">Element that contains metadata about hello event.</span></span> |
| <span data-ttu-id="ca367-148">authorization</span><span class="sxs-lookup"><span data-stu-id="ca367-148">authorization</span></span> |<span data-ttu-id="ca367-149">propiedades de Control de acceso basado en roles de Hola de evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca367-149">hello Role-Based Access Control properties of hello event.</span></span> <span data-ttu-id="ca367-150">Normalmente, estas propiedades incluyen acción hello, rol Hola y Hola ámbito.</span><span class="sxs-lookup"><span data-stu-id="ca367-150">These properties usually include hello action, hello role, and hello scope.</span></span> |
| <span data-ttu-id="ca367-151">categoría</span><span class="sxs-lookup"><span data-stu-id="ca367-151">category</span></span> |<span data-ttu-id="ca367-152">Categoría de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca367-152">Category of hello event.</span></span> <span data-ttu-id="ca367-153">Los valores admitidos incluyen: Administrative, Alert, Security, ServiceHealth y Recommendation.</span><span class="sxs-lookup"><span data-stu-id="ca367-153">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span></span> |
| <span data-ttu-id="ca367-154">caller</span><span class="sxs-lookup"><span data-stu-id="ca367-154">caller</span></span> |<span data-ttu-id="ca367-155">Dirección de correo electrónico del usuario de Hola que realizó la operación de hello, notificación de UPN o notificación SPN según su disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="ca367-155">Email address of hello user who performed hello operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="ca367-156">Puede ser null para ciertas llamadas del sistema.</span><span class="sxs-lookup"><span data-stu-id="ca367-156">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="ca367-157">correlationId</span><span class="sxs-lookup"><span data-stu-id="ca367-157">correlationId</span></span> |<span data-ttu-id="ca367-158">Normalmente, un GUID en formato de cadena.</span><span class="sxs-lookup"><span data-stu-id="ca367-158">Usually a GUID in string format.</span></span> <span data-ttu-id="ca367-159">Eventos con correlationId pertenecen toohello misma acción mayor y normalmente comparten un correlationId.</span><span class="sxs-lookup"><span data-stu-id="ca367-159">Events with correlationId belong toohello same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="ca367-160">eventDescription</span><span class="sxs-lookup"><span data-stu-id="ca367-160">eventDescription</span></span> |<span data-ttu-id="ca367-161">Descripción de texto estático de evento Hola.</span><span class="sxs-lookup"><span data-stu-id="ca367-161">Static text description of hello event.</span></span> |
| <span data-ttu-id="ca367-162">eventDataId</span><span class="sxs-lookup"><span data-stu-id="ca367-162">eventDataId</span></span> |<span data-ttu-id="ca367-163">Identificador único para el evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca367-163">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="ca367-164">eventSource</span><span class="sxs-lookup"><span data-stu-id="ca367-164">eventSource</span></span> |<span data-ttu-id="ca367-165">Nombre de Hola servicio de Azure o la infraestructura de ese evento Hola generado.</span><span class="sxs-lookup"><span data-stu-id="ca367-165">Name of hello Azure service or infrastructure that generated hello event.</span></span> |
| <span data-ttu-id="ca367-166">httpRequest</span><span class="sxs-lookup"><span data-stu-id="ca367-166">httpRequest</span></span> |<span data-ttu-id="ca367-167">Hello solicitud normalmente incluye hello clientRequestId, clientIpAddress y método HTTP (por ejemplo, PUT).</span><span class="sxs-lookup"><span data-stu-id="ca367-167">hello request usually includes hello clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span></span> |
| <span data-ttu-id="ca367-168">level</span><span class="sxs-lookup"><span data-stu-id="ca367-168">level</span></span> |<span data-ttu-id="ca367-169">Uno de hello siguientes valores: crítico, Error, advertencia, informativo y detallado.</span><span class="sxs-lookup"><span data-stu-id="ca367-169">One of hello following values: Critical, Error, Warning, Informational, and Verbose.</span></span> |
| <span data-ttu-id="ca367-170">operationId</span><span class="sxs-lookup"><span data-stu-id="ca367-170">operationId</span></span> |<span data-ttu-id="ca367-171">Normalmente un GUID que se comparten entre eventos de hello correspondiente toosingle operación.</span><span class="sxs-lookup"><span data-stu-id="ca367-171">Usually a GUID shared among hello events corresponding toosingle operation.</span></span> |
| <span data-ttu-id="ca367-172">operationName</span><span class="sxs-lookup"><span data-stu-id="ca367-172">operationName</span></span> |<span data-ttu-id="ca367-173">Nombre de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca367-173">Name of hello operation.</span></span> |
| <span data-ttu-id="ca367-174">propiedades</span><span class="sxs-lookup"><span data-stu-id="ca367-174">properties</span></span> |<span data-ttu-id="ca367-175">Propiedades de evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca367-175">Properties of hello event.</span></span> |
| <span data-ttu-id="ca367-176">status</span><span class="sxs-lookup"><span data-stu-id="ca367-176">status</span></span> |<span data-ttu-id="ca367-177">String.</span><span class="sxs-lookup"><span data-stu-id="ca367-177">String.</span></span> <span data-ttu-id="ca367-178">Estado de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca367-178">Status of hello operation.</span></span> <span data-ttu-id="ca367-179">Entre los valores habituales, se incluyen Started, In Progress, Succeeded, Failed, Active y Resolved.</span><span class="sxs-lookup"><span data-stu-id="ca367-179">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span></span> |
| <span data-ttu-id="ca367-180">subStatus</span><span class="sxs-lookup"><span data-stu-id="ca367-180">subStatus</span></span> |<span data-ttu-id="ca367-181">Normalmente incluye código de estado HTTP de Hola de llamada REST de hello correspondiente.</span><span class="sxs-lookup"><span data-stu-id="ca367-181">Usually includes hello HTTP status code of hello corresponding REST call.</span></span> <span data-ttu-id="ca367-182">También podría incluir otras cadenas que describen un subestado.</span><span class="sxs-lookup"><span data-stu-id="ca367-182">It might also include other strings that describe a substatus.</span></span> <span data-ttu-id="ca367-183">Entre los valores de subestado habituales se incluyen OK (código de estado HTTP: 200), Created (código de estado HTTP: 201), Accepted (código de estado HTTP: 202), No Content (código de estado HTTP: 204), Bad Request (código de estado HTTP: 400), Not Found (código de estado HTTP: 404), Conflict (código de estado HTTP: 409), Internal Server Error (código de estado HTTP: 500), Service Unavailable (código de estado HTTP: 503) y Gateway Timeout (código de estado HTTP: 504).</span><span class="sxs-lookup"><span data-stu-id="ca367-183">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ca367-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ca367-184">Next steps</span></span>
* <span data-ttu-id="ca367-185">[Obtener más información sobre el registro de actividad de hello](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="ca367-185">[Learn more about hello activity log](monitoring-overview-activity-logs.md).</span></span>
* <span data-ttu-id="ca367-186">[Ejecución de scripts de Azure Automation (runbooks) en alertas de Azure](http://go.microsoft.com/fwlink/?LinkId=627081).</span><span class="sxs-lookup"><span data-stu-id="ca367-186">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span></span>
* <span data-ttu-id="ca367-187">[Usar un toosend de aplicación lógica un SMS a través de Twilio de una alerta Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="ca367-187">[Use a logic app toosend an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="ca367-188">En este ejemplo es para alertas métricas, pero puede ser modificado toowork con una alerta de registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="ca367-188">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
* <span data-ttu-id="ca367-189">[Usar un toosend de aplicación lógica un mensaje desde una alerta Azure demora](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="ca367-189">[Use a logic app toosend a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="ca367-190">En este ejemplo es para alertas métricas, pero puede ser modificado toowork con una alerta de registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="ca367-190">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
* <span data-ttu-id="ca367-191">[Usar un toosend de aplicación lógica un tooan mensaje Azure cola desde una alerta Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="ca367-191">[Use a logic app toosend a message tooan Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="ca367-192">En este ejemplo es para alertas métricas, pero puede ser modificado toowork con una alerta de registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="ca367-192">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
