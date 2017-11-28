---
title: Llamada a un webhook cuando se activan alertas del registro de actividades de Azure | Microsoft Docs
description: "Enrute los eventos de registro de actividades a otros servicios para acciones personalizadas. Por ejemplo, envíe SMS, registre errores o notifique a un equipo a través del servicio de chat o mensajería."
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
ms.openlocfilehash: 341ab32ad0ec691285fbf1537ee298ab30156a5d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a><span data-ttu-id="b5a44-104">Llamada a un webhook cuando se activan alertas del registro de actividades de Azure</span><span class="sxs-lookup"><span data-stu-id="b5a44-104">Call a webhook on Azure Activity Log alerts</span></span>
<span data-ttu-id="b5a44-105">Los webhooks permiten enrutar una notificación de alerta de Azure a otros sistemas para su procesamiento posterior o acciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="b5a44-105">Webhooks allow you to route an Azure alert notification to other systems for post-processing or custom actions.</span></span> <span data-ttu-id="b5a44-106">Puede usar un webhook en una alerta para enrutarla a servicios que envían SMS, registran errores, notifican a un equipo mediante servicios de chat y mensajería o llevan a cabo otras acciones diversas.</span><span class="sxs-lookup"><span data-stu-id="b5a44-106">You can use a webhook on an alert to route it to services that send SMS, log bugs, notify a team via chat/messaging services, or do any number of other actions.</span></span> <span data-ttu-id="b5a44-107">En este artículo se describe cómo establecer un webhook al que llamar cuando se activa una alerta del registro de actividades de Azure.</span><span class="sxs-lookup"><span data-stu-id="b5a44-107">This article describes how to set a webhook to be called when an Azure Activity Log alert fires.</span></span> <span data-ttu-id="b5a44-108">También muestra el aspecto de la carga útil para HTTP POST a un webhook.</span><span class="sxs-lookup"><span data-stu-id="b5a44-108">It also shows what the payload for the HTTP POST to a webhook looks like.</span></span> <span data-ttu-id="b5a44-109">Para información sobre la configuración y el esquema de una alerta de métrica de Azure, [consulte esta página en su lugar](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="b5a44-109">For information on the setup and schema for an Azure metric alert, [see this page instead](insights-webhooks-alerts.md).</span></span> <span data-ttu-id="b5a44-110">También puede configurar una alerta de registro de actividad para enviar correo electrónico cuando se active.</span><span class="sxs-lookup"><span data-stu-id="b5a44-110">You can also set up an Activity Log alert to send email when activated.</span></span>

> [!NOTE]
> <span data-ttu-id="b5a44-111">Esta característica está actualmente en versión preliminar y se quitará en algún momento en el futuro.</span><span class="sxs-lookup"><span data-stu-id="b5a44-111">This feature is currently in preview and will be removed at some point in the future.</span></span>
>
>

<span data-ttu-id="b5a44-112">Puede configurar una alerta de registro de actividad mediante los [cmdlets de Azure PowerShell](insights-powershell-samples.md#create-metric-alerts), la [CLI multiplataforma](insights-cli-samples.md#work-with-alerts) o la [API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5a44-112">You can set up an Activity Log alert using the [Azure PowerShell Cmdlets](insights-powershell-samples.md#create-metric-alerts), [Cross-Platform CLI](insights-cli-samples.md#work-with-alerts), or [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span></span> <span data-ttu-id="b5a44-113">Actualmente, no se puede configurar una mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b5a44-113">Currently, you cannot set one up using the Azure portal.</span></span>

## <a name="authenticating-the-webhook"></a><span data-ttu-id="b5a44-114">Autenticación del webhook</span><span class="sxs-lookup"><span data-stu-id="b5a44-114">Authenticating the webhook</span></span>
<span data-ttu-id="b5a44-115">El webhook se puede autenticar con uno de estos métodos:</span><span class="sxs-lookup"><span data-stu-id="b5a44-115">The webhook can authenticate using either of these methods:</span></span>

1. <span data-ttu-id="b5a44-116">**Autorización basada en token**: el identificador URI de webhook se guarda con un identificador de token, por ejemplo, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span><span class="sxs-lookup"><span data-stu-id="b5a44-116">**Token-based authorization** - The webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span></span>
2. <span data-ttu-id="b5a44-117">**Autorización básica**: el identificador URI de webhook se guarda con un nombre de usuario y una contraseña, por ejemplo, `https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span><span class="sxs-lookup"><span data-stu-id="b5a44-117">**Basic authorization** - The webhook URI is saved with a username and password, for example, `https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span></span>

## <a name="payload-schema"></a><span data-ttu-id="b5a44-118">Esquema de carga</span><span class="sxs-lookup"><span data-stu-id="b5a44-118">Payload schema</span></span>
<span data-ttu-id="b5a44-119">La operación POST contiene el siguiente esquema y carga útil de JSON para todas las alertas basadas en el registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="b5a44-119">The POST operation contains the following JSON payload and schema for all Activity Log-based alerts.</span></span> <span data-ttu-id="b5a44-120">Este esquema es similar al usado por las alertas basadas en métrica.</span><span class="sxs-lookup"><span data-stu-id="b5a44-120">This schema is similar to the one used by metric-based alerts.</span></span>

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

| <span data-ttu-id="b5a44-121">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="b5a44-121">Element Name</span></span> | <span data-ttu-id="b5a44-122">Description</span><span class="sxs-lookup"><span data-stu-id="b5a44-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b5a44-123">status</span><span class="sxs-lookup"><span data-stu-id="b5a44-123">status</span></span> |<span data-ttu-id="b5a44-124">Usado para alertas de métrica.</span><span class="sxs-lookup"><span data-stu-id="b5a44-124">Used for metric alerts.</span></span> <span data-ttu-id="b5a44-125">Siempre se establece en "activated" para las alertas de registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="b5a44-125">Always set to "activated" for Activity Log alerts.</span></span> |
| <span data-ttu-id="b5a44-126">contexto</span><span class="sxs-lookup"><span data-stu-id="b5a44-126">context</span></span> |<span data-ttu-id="b5a44-127">Contexto del evento</span><span class="sxs-lookup"><span data-stu-id="b5a44-127">Context of the event.</span></span> |
| <span data-ttu-id="b5a44-128">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="b5a44-128">resourceProviderName</span></span> |<span data-ttu-id="b5a44-129">Proveedor de recursos del recurso afectado</span><span class="sxs-lookup"><span data-stu-id="b5a44-129">The resource provider of the impacted resource.</span></span> |
| <span data-ttu-id="b5a44-130">conditionType</span><span class="sxs-lookup"><span data-stu-id="b5a44-130">conditionType</span></span> |<span data-ttu-id="b5a44-131">Siempre "Event"</span><span class="sxs-lookup"><span data-stu-id="b5a44-131">Always "Event."</span></span> |
| <span data-ttu-id="b5a44-132">name</span><span class="sxs-lookup"><span data-stu-id="b5a44-132">name</span></span> |<span data-ttu-id="b5a44-133">Nombre de la regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="b5a44-133">Name of the alert rule.</span></span> |
| <span data-ttu-id="b5a44-134">id</span><span class="sxs-lookup"><span data-stu-id="b5a44-134">id</span></span> |<span data-ttu-id="b5a44-135">Identificador de recurso de la alerta</span><span class="sxs-lookup"><span data-stu-id="b5a44-135">Resource ID of the alert.</span></span> |
| <span data-ttu-id="b5a44-136">Description</span><span class="sxs-lookup"><span data-stu-id="b5a44-136">description</span></span> |<span data-ttu-id="b5a44-137">Descripción de la alerta como se estableció al crearla</span><span class="sxs-lookup"><span data-stu-id="b5a44-137">Alert description as set during creation of the alert.</span></span> |
| <span data-ttu-id="b5a44-138">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="b5a44-138">subscriptionId</span></span> |<span data-ttu-id="b5a44-139">Identificador de suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="b5a44-139">Azure Subscription ID.</span></span> |
| <span data-ttu-id="b5a44-140">timestamp</span><span class="sxs-lookup"><span data-stu-id="b5a44-140">timestamp</span></span> |<span data-ttu-id="b5a44-141">Cuándo generó el evento el servicio de Azure que procesó la solicitud</span><span class="sxs-lookup"><span data-stu-id="b5a44-141">Time at which the event was generated by the Azure service that processed the request.</span></span> |
| <span data-ttu-id="b5a44-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="b5a44-142">resourceId</span></span> |<span data-ttu-id="b5a44-143">Identificador de recurso del recurso afectado.</span><span class="sxs-lookup"><span data-stu-id="b5a44-143">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="b5a44-144">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="b5a44-144">resourceGroupName</span></span> |<span data-ttu-id="b5a44-145">Nombre del grupo de recursos del recurso afectado</span><span class="sxs-lookup"><span data-stu-id="b5a44-145">Name of the resource group for the impacted resource</span></span> |
| <span data-ttu-id="b5a44-146">propiedades</span><span class="sxs-lookup"><span data-stu-id="b5a44-146">properties</span></span> |<span data-ttu-id="b5a44-147">Conjunto de pares `<Key, Value>` (es decir, `Dictionary<String, String>`) que incluye detalles sobre el evento</span><span class="sxs-lookup"><span data-stu-id="b5a44-147">Set of `<Key, Value>` pairs (i.e. `Dictionary<String, String>`) that includes details about the event.</span></span> |
| <span data-ttu-id="b5a44-148">event</span><span class="sxs-lookup"><span data-stu-id="b5a44-148">event</span></span> |<span data-ttu-id="b5a44-149">Elemento que contiene metadatos sobre el evento</span><span class="sxs-lookup"><span data-stu-id="b5a44-149">Element containing metadata about the event.</span></span> |
| <span data-ttu-id="b5a44-150">authorization</span><span class="sxs-lookup"><span data-stu-id="b5a44-150">authorization</span></span> |<span data-ttu-id="b5a44-151">Propiedades RBAC del evento.</span><span class="sxs-lookup"><span data-stu-id="b5a44-151">The RBAC properties of the event.</span></span> <span data-ttu-id="b5a44-152">Normalmente incluyen "action", "role" y "scope".</span><span class="sxs-lookup"><span data-stu-id="b5a44-152">These usually include the “action”, “role” and the “scope.”</span></span> |
| <span data-ttu-id="b5a44-153">categoría</span><span class="sxs-lookup"><span data-stu-id="b5a44-153">category</span></span> |<span data-ttu-id="b5a44-154">Categoría del evento.</span><span class="sxs-lookup"><span data-stu-id="b5a44-154">Category of the event.</span></span> <span data-ttu-id="b5a44-155">Los valores admitidos son: Administrative, Alert, Security, ServiceHealth y Recommendation.</span><span class="sxs-lookup"><span data-stu-id="b5a44-155">Supported values include: Administrative, Alert, Security, ServiceHealth, Recommendation.</span></span> |
| <span data-ttu-id="b5a44-156">caller</span><span class="sxs-lookup"><span data-stu-id="b5a44-156">caller</span></span> |<span data-ttu-id="b5a44-157">Dirección de correo electrónico del usuario que realizó la operación, la notificación de UPN o la notificación de SPN basada en la disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="b5a44-157">Email address of the user who performed the operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="b5a44-158">Puede ser null para ciertas llamadas del sistema.</span><span class="sxs-lookup"><span data-stu-id="b5a44-158">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="b5a44-159">correlationId</span><span class="sxs-lookup"><span data-stu-id="b5a44-159">correlationId</span></span> |<span data-ttu-id="b5a44-160">Normalmente, un GUID en formato de cadena.</span><span class="sxs-lookup"><span data-stu-id="b5a44-160">Usually a GUID in string format.</span></span> <span data-ttu-id="b5a44-161">Los eventos con correlationId pertenecen a la misma acción de mayor tamaño y suelen compartir un campo correlationId.</span><span class="sxs-lookup"><span data-stu-id="b5a44-161">Events with correlationId belong to the same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="b5a44-162">eventDescription</span><span class="sxs-lookup"><span data-stu-id="b5a44-162">eventDescription</span></span> |<span data-ttu-id="b5a44-163">Descripción de texto estático del evento</span><span class="sxs-lookup"><span data-stu-id="b5a44-163">Static text description of the event.</span></span> |
| <span data-ttu-id="b5a44-164">eventDataId</span><span class="sxs-lookup"><span data-stu-id="b5a44-164">eventDataId</span></span> |<span data-ttu-id="b5a44-165">Identificador único para el evento</span><span class="sxs-lookup"><span data-stu-id="b5a44-165">Unique identifier for the event.</span></span> |
| <span data-ttu-id="b5a44-166">eventSource</span><span class="sxs-lookup"><span data-stu-id="b5a44-166">eventSource</span></span> |<span data-ttu-id="b5a44-167">Nombre de la infraestructura o el servicio de Azure que generó el evento</span><span class="sxs-lookup"><span data-stu-id="b5a44-167">Name of the Azure service or infrastructure that generated the event.</span></span> |
| <span data-ttu-id="b5a44-168">httpRequest</span><span class="sxs-lookup"><span data-stu-id="b5a44-168">httpRequest</span></span> |<span data-ttu-id="b5a44-169">Normalmente incluye "clientRequestId", "clientIpAddress" y "method" (el método HTTP, por ejemplo, PUT).</span><span class="sxs-lookup"><span data-stu-id="b5a44-169">Usually includes the “clientRequestId”, “clientIpAddress” and “method” (HTTP method e.g. PUT).</span></span> |
| <span data-ttu-id="b5a44-170">level</span><span class="sxs-lookup"><span data-stu-id="b5a44-170">level</span></span> |<span data-ttu-id="b5a44-171">Uno de los siguientes valores: "Critical", "Error", "Warning", "Informational" y "Verbose"</span><span class="sxs-lookup"><span data-stu-id="b5a44-171">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose.”</span></span> |
| <span data-ttu-id="b5a44-172">operationId</span><span class="sxs-lookup"><span data-stu-id="b5a44-172">operationId</span></span> |<span data-ttu-id="b5a44-173">Por lo general, un GUID compartido entre los eventos correspondientes a una sola operación</span><span class="sxs-lookup"><span data-stu-id="b5a44-173">Usually a GUID shared among the events corresponding to single operation.</span></span> |
| <span data-ttu-id="b5a44-174">operationName</span><span class="sxs-lookup"><span data-stu-id="b5a44-174">operationName</span></span> |<span data-ttu-id="b5a44-175">Nombre de la operación.</span><span class="sxs-lookup"><span data-stu-id="b5a44-175">Name of the operation.</span></span> |
| <span data-ttu-id="b5a44-176">propiedades</span><span class="sxs-lookup"><span data-stu-id="b5a44-176">properties</span></span> |<span data-ttu-id="b5a44-177">Propiedades del evento.</span><span class="sxs-lookup"><span data-stu-id="b5a44-177">Properties of the event.</span></span> |
| <span data-ttu-id="b5a44-178">status</span><span class="sxs-lookup"><span data-stu-id="b5a44-178">status</span></span> |<span data-ttu-id="b5a44-179">String.</span><span class="sxs-lookup"><span data-stu-id="b5a44-179">String.</span></span> <span data-ttu-id="b5a44-180">Estado de la operación.</span><span class="sxs-lookup"><span data-stu-id="b5a44-180">Status of the operation.</span></span> <span data-ttu-id="b5a44-181">Entre los valores habituales, se incluyen "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span><span class="sxs-lookup"><span data-stu-id="b5a44-181">Common values include: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span></span> |
| <span data-ttu-id="b5a44-182">subStatus</span><span class="sxs-lookup"><span data-stu-id="b5a44-182">subStatus</span></span> |<span data-ttu-id="b5a44-183">Normalmente, incluye el código de estado HTTP de la llamada de REST correspondiente.</span><span class="sxs-lookup"><span data-stu-id="b5a44-183">Usually includes the HTTP status code of the corresponding REST call.</span></span> <span data-ttu-id="b5a44-184">También podría incluir otras cadenas que describen un subestado.</span><span class="sxs-lookup"><span data-stu-id="b5a44-184">It might also include other strings describing a substatus.</span></span> <span data-ttu-id="b5a44-185">Entre los valores de subestado habituales se incluyen OK (código de estado HTTP: 200), Created (código de estado HTTP: 201), Accepted (código de estado HTTP: 202), No Content (código de estado HTTP: 204), Bad Request (código de estado HTTP: 400), Not Found (código de estado HTTP: 404), Conflict (código de estado HTTP: 409), Internal Server Error (código de estado HTTP: 500), Service Unavailable (código de estado HTTP: 503) y Gateway Timeout (código de estado HTTP: 504)</span><span class="sxs-lookup"><span data-stu-id="b5a44-185">Common substatus values include: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b5a44-186">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b5a44-186">Next steps</span></span>
* [<span data-ttu-id="b5a44-187">Más información sobre el registro de actividad</span><span class="sxs-lookup"><span data-stu-id="b5a44-187">Learn more about the Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="b5a44-188">Ejecute scripts de Azure Automation (Runbooks) en alertas de Azure</span><span class="sxs-lookup"><span data-stu-id="b5a44-188">Execute Azure Automation scripts (Runbooks) on Azure alerts</span></span>](http://go.microsoft.com/fwlink/?LinkId=627081)
* <span data-ttu-id="b5a44-189">[Use una aplicación lógica para enviar un SMS a través de Twilio desde una alerta de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="b5a44-189">[Use Logic App to send an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="b5a44-190">Este ejemplo es para alertas de métrica, pero podría modificarse para funcionar con una alerta de registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="b5a44-190">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
* <span data-ttu-id="b5a44-191">[Use una aplicación lógica para enviar un mensaje de Slack desde una alerta de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="b5a44-191">[Use Logic App to send a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="b5a44-192">Este ejemplo es para alertas de métrica, pero podría modificarse para funcionar con una alerta de registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="b5a44-192">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
* <span data-ttu-id="b5a44-193">[Use una aplicación lógica para enviar un mensaje a una cola de Azure desde una alerta de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="b5a44-193">[Use Logic App to send a message to an Azure Queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="b5a44-194">Este ejemplo es para alertas de métrica, pero podría modificarse para funcionar con una alerta de registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="b5a44-194">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
