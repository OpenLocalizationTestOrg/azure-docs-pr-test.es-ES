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
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a><span data-ttu-id="3ce69-104">Llamada a un webhook cuando se activan alertas del registro de actividades de Azure</span><span class="sxs-lookup"><span data-stu-id="3ce69-104">Call a webhook on Azure Activity Log alerts</span></span>
<span data-ttu-id="3ce69-105">Webhooks le permiten tooroute un Azure sistemas de notificación de tooother para acciones posteriores al procesamiento o personalizados de alerta.</span><span class="sxs-lookup"><span data-stu-id="3ce69-105">Webhooks allow you tooroute an Azure alert notification tooother systems for post-processing or custom actions.</span></span> <span data-ttu-id="3ce69-106">Puede usar un webhook en una alerta tooroute se tooservices que enviar SMS, registrar errores, notificar a un equipo a través de servicios de chat/mensajería o realizar cualquier número de otras acciones.</span><span class="sxs-lookup"><span data-stu-id="3ce69-106">You can use a webhook on an alert tooroute it tooservices that send SMS, log bugs, notify a team via chat/messaging services, or do any number of other actions.</span></span> <span data-ttu-id="3ce69-107">Este artículo describe cómo llama a tooset una toobe webhook cuando un se activa la alerta en el registro de actividad de Azure.</span><span class="sxs-lookup"><span data-stu-id="3ce69-107">This article describes how tooset a webhook toobe called when an Azure Activity Log alert fires.</span></span> <span data-ttu-id="3ce69-108">También muestra qué carga Hola Hola HTTP POST tooa webhook aspecto.</span><span class="sxs-lookup"><span data-stu-id="3ce69-108">It also shows what hello payload for hello HTTP POST tooa webhook looks like.</span></span> <span data-ttu-id="3ce69-109">Para obtener información sobre el programa de instalación de Hola y el esquema de una alerta de métrica de Azure, [vea esta página en su lugar](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="3ce69-109">For information on hello setup and schema for an Azure metric alert, [see this page instead](insights-webhooks-alerts.md).</span></span> <span data-ttu-id="3ce69-110">También puede configurar un correo electrónico de alerta toosend del registro de actividad cuando se activan.</span><span class="sxs-lookup"><span data-stu-id="3ce69-110">You can also set up an Activity Log alert toosend email when activated.</span></span>

> [!NOTE]
> <span data-ttu-id="3ce69-111">Esta característica está actualmente en versión preliminar y se quitará en algún momento futuro Hola.</span><span class="sxs-lookup"><span data-stu-id="3ce69-111">This feature is currently in preview and will be removed at some point in hello future.</span></span>
>
>

<span data-ttu-id="3ce69-112">Puede configurar una alerta de registro de actividad con hello [Cmdlets de PowerShell de Azure](insights-powershell-samples.md#create-metric-alerts), [multiplataforma CLI](insights-cli-samples.md#work-with-alerts), o [API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ce69-112">You can set up an Activity Log alert using hello [Azure PowerShell Cmdlets](insights-powershell-samples.md#create-metric-alerts), [Cross-Platform CLI](insights-cli-samples.md#work-with-alerts), or [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span></span> <span data-ttu-id="3ce69-113">Actualmente, no se puede establecer uno utilizando Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3ce69-113">Currently, you cannot set one up using hello Azure portal.</span></span>

## <a name="authenticating-hello-webhook"></a><span data-ttu-id="3ce69-114">Autenticar hello webhook</span><span class="sxs-lookup"><span data-stu-id="3ce69-114">Authenticating hello webhook</span></span>
<span data-ttu-id="3ce69-115">Hola webhook se puedan autenticar con cualquiera de estos métodos:</span><span class="sxs-lookup"><span data-stu-id="3ce69-115">hello webhook can authenticate using either of these methods:</span></span>

1. <span data-ttu-id="3ce69-116">**Autorización basada en token** -Hola webhook URI se guarda con un identificador de token, por ejemplo,`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span><span class="sxs-lookup"><span data-stu-id="3ce69-116">**Token-based authorization** - hello webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span></span>
2. <span data-ttu-id="3ce69-117">**Autorización básica** -Hola webhook URI se guarda con un nombre de usuario y una contraseña, por ejemplo,`https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span><span class="sxs-lookup"><span data-stu-id="3ce69-117">**Basic authorization** - hello webhook URI is saved with a username and password, for example, `https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span></span>

## <a name="payload-schema"></a><span data-ttu-id="3ce69-118">Esquema de carga</span><span class="sxs-lookup"><span data-stu-id="3ce69-118">Payload schema</span></span>
<span data-ttu-id="3ce69-119">Hola operación POST contiene Hola después carga JSON y el esquema para todas las alertas de registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="3ce69-119">hello POST operation contains hello following JSON payload and schema for all Activity Log-based alerts.</span></span> <span data-ttu-id="3ce69-120">Este esquema es similar toohello uno emplean alertas basadas en la métrica.</span><span class="sxs-lookup"><span data-stu-id="3ce69-120">This schema is similar toohello one used by metric-based alerts.</span></span>

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

| <span data-ttu-id="3ce69-121">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="3ce69-121">Element Name</span></span> | <span data-ttu-id="3ce69-122">Description</span><span class="sxs-lookup"><span data-stu-id="3ce69-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3ce69-123">status</span><span class="sxs-lookup"><span data-stu-id="3ce69-123">status</span></span> |<span data-ttu-id="3ce69-124">Usado para alertas de métrica.</span><span class="sxs-lookup"><span data-stu-id="3ce69-124">Used for metric alerts.</span></span> <span data-ttu-id="3ce69-125">Siempre se establece demasiado "activado" para las alertas de registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="3ce69-125">Always set too"activated" for Activity Log alerts.</span></span> |
| <span data-ttu-id="3ce69-126">contexto</span><span class="sxs-lookup"><span data-stu-id="3ce69-126">context</span></span> |<span data-ttu-id="3ce69-127">Contexto de evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="3ce69-127">Context of hello event.</span></span> |
| <span data-ttu-id="3ce69-128">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="3ce69-128">resourceProviderName</span></span> |<span data-ttu-id="3ce69-129">proveedor de recursos de Hola de hello afectado recursos.</span><span class="sxs-lookup"><span data-stu-id="3ce69-129">hello resource provider of hello impacted resource.</span></span> |
| <span data-ttu-id="3ce69-130">conditionType</span><span class="sxs-lookup"><span data-stu-id="3ce69-130">conditionType</span></span> |<span data-ttu-id="3ce69-131">Siempre "Event"</span><span class="sxs-lookup"><span data-stu-id="3ce69-131">Always "Event."</span></span> |
| <span data-ttu-id="3ce69-132">name</span><span class="sxs-lookup"><span data-stu-id="3ce69-132">name</span></span> |<span data-ttu-id="3ce69-133">Nombre de regla de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="3ce69-133">Name of hello alert rule.</span></span> |
| <span data-ttu-id="3ce69-134">id</span><span class="sxs-lookup"><span data-stu-id="3ce69-134">id</span></span> |<span data-ttu-id="3ce69-135">Id. de recurso de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="3ce69-135">Resource ID of hello alert.</span></span> |
| <span data-ttu-id="3ce69-136">description</span><span class="sxs-lookup"><span data-stu-id="3ce69-136">description</span></span> |<span data-ttu-id="3ce69-137">Descripción de la alerta como conjunto durante la creación de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="3ce69-137">Alert description as set during creation of hello alert.</span></span> |
| <span data-ttu-id="3ce69-138">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="3ce69-138">subscriptionId</span></span> |<span data-ttu-id="3ce69-139">Identificador de suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="3ce69-139">Azure Subscription ID.</span></span> |
| <span data-ttu-id="3ce69-140">timestamp</span><span class="sxs-lookup"><span data-stu-id="3ce69-140">timestamp</span></span> |<span data-ttu-id="3ce69-141">Hora a qué Hola se generó el evento por el servicio de Azure que procesa la solicitud de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="3ce69-141">Time at which hello event was generated by hello Azure service that processed hello request.</span></span> |
| <span data-ttu-id="3ce69-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="3ce69-142">resourceId</span></span> |<span data-ttu-id="3ce69-143">Id. de recurso de hello afectado recursos.</span><span class="sxs-lookup"><span data-stu-id="3ce69-143">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="3ce69-144">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="3ce69-144">resourceGroupName</span></span> |<span data-ttu-id="3ce69-145">Nombre de grupo de recursos de Hola Hola afectado recursos</span><span class="sxs-lookup"><span data-stu-id="3ce69-145">Name of hello resource group for hello impacted resource</span></span> |
| <span data-ttu-id="3ce69-146">propiedades</span><span class="sxs-lookup"><span data-stu-id="3ce69-146">properties</span></span> |<span data-ttu-id="3ce69-147">Conjunto de `<Key, Value>` pares (es decir, `Dictionary<String, String>`) que incluye detalles acerca del evento Hola.</span><span class="sxs-lookup"><span data-stu-id="3ce69-147">Set of `<Key, Value>` pairs (i.e. `Dictionary<String, String>`) that includes details about hello event.</span></span> |
| <span data-ttu-id="3ce69-148">event</span><span class="sxs-lookup"><span data-stu-id="3ce69-148">event</span></span> |<span data-ttu-id="3ce69-149">Elemento que contiene metadatos acerca del evento Hola.</span><span class="sxs-lookup"><span data-stu-id="3ce69-149">Element containing metadata about hello event.</span></span> |
| <span data-ttu-id="3ce69-150">authorization</span><span class="sxs-lookup"><span data-stu-id="3ce69-150">authorization</span></span> |<span data-ttu-id="3ce69-151">propiedades RBAC Hola de evento Hola.</span><span class="sxs-lookup"><span data-stu-id="3ce69-151">hello RBAC properties of hello event.</span></span> <span data-ttu-id="3ce69-152">Generalmente incluyen hello hello, "role" y "acción de" "ámbito".</span><span class="sxs-lookup"><span data-stu-id="3ce69-152">These usually include hello “action”, “role” and hello “scope.”</span></span> |
| <span data-ttu-id="3ce69-153">categoría</span><span class="sxs-lookup"><span data-stu-id="3ce69-153">category</span></span> |<span data-ttu-id="3ce69-154">Categoría de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3ce69-154">Category of hello event.</span></span> <span data-ttu-id="3ce69-155">Los valores admitidos son: Administrative, Alert, Security, ServiceHealth y Recommendation.</span><span class="sxs-lookup"><span data-stu-id="3ce69-155">Supported values include: Administrative, Alert, Security, ServiceHealth, Recommendation.</span></span> |
| <span data-ttu-id="3ce69-156">caller</span><span class="sxs-lookup"><span data-stu-id="3ce69-156">caller</span></span> |<span data-ttu-id="3ce69-157">Dirección de correo electrónico del usuario de Hola que realizó la operación de hello, notificación de UPN o notificación SPN según su disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="3ce69-157">Email address of hello user who performed hello operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="3ce69-158">Puede ser null para ciertas llamadas del sistema.</span><span class="sxs-lookup"><span data-stu-id="3ce69-158">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="3ce69-159">correlationId</span><span class="sxs-lookup"><span data-stu-id="3ce69-159">correlationId</span></span> |<span data-ttu-id="3ce69-160">Normalmente, un GUID en formato de cadena.</span><span class="sxs-lookup"><span data-stu-id="3ce69-160">Usually a GUID in string format.</span></span> <span data-ttu-id="3ce69-161">Eventos con correlationId pertenecen toohello misma acción mayor y normalmente comparten un correlationId.</span><span class="sxs-lookup"><span data-stu-id="3ce69-161">Events with correlationId belong toohello same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="3ce69-162">eventDescription</span><span class="sxs-lookup"><span data-stu-id="3ce69-162">eventDescription</span></span> |<span data-ttu-id="3ce69-163">Descripción de texto estático de evento Hola.</span><span class="sxs-lookup"><span data-stu-id="3ce69-163">Static text description of hello event.</span></span> |
| <span data-ttu-id="3ce69-164">eventDataId</span><span class="sxs-lookup"><span data-stu-id="3ce69-164">eventDataId</span></span> |<span data-ttu-id="3ce69-165">Identificador único para el evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="3ce69-165">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="3ce69-166">eventSource</span><span class="sxs-lookup"><span data-stu-id="3ce69-166">eventSource</span></span> |<span data-ttu-id="3ce69-167">Nombre de Hola servicio de Azure o la infraestructura de ese evento Hola generado.</span><span class="sxs-lookup"><span data-stu-id="3ce69-167">Name of hello Azure service or infrastructure that generated hello event.</span></span> |
| <span data-ttu-id="3ce69-168">httpRequest</span><span class="sxs-lookup"><span data-stu-id="3ce69-168">httpRequest</span></span> |<span data-ttu-id="3ce69-169">Normalmente incluye Estados valores de para saludo "clientRequestId", "clientIpAddress" y "method" (el método HTTP, por ejemplo, PUT).</span><span class="sxs-lookup"><span data-stu-id="3ce69-169">Usually includes hello “clientRequestId”, “clientIpAddress” and “method” (HTTP method e.g. PUT).</span></span> |
| <span data-ttu-id="3ce69-170">level</span><span class="sxs-lookup"><span data-stu-id="3ce69-170">level</span></span> |<span data-ttu-id="3ce69-171">Uno de hello siguientes valores: "Critical", "Error", "Warning", "Informational" y "Verbose".</span><span class="sxs-lookup"><span data-stu-id="3ce69-171">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose.”</span></span> |
| <span data-ttu-id="3ce69-172">operationId</span><span class="sxs-lookup"><span data-stu-id="3ce69-172">operationId</span></span> |<span data-ttu-id="3ce69-173">Normalmente un GUID que se comparten entre eventos de hello correspondiente toosingle operación.</span><span class="sxs-lookup"><span data-stu-id="3ce69-173">Usually a GUID shared among hello events corresponding toosingle operation.</span></span> |
| <span data-ttu-id="3ce69-174">operationName</span><span class="sxs-lookup"><span data-stu-id="3ce69-174">operationName</span></span> |<span data-ttu-id="3ce69-175">Nombre de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3ce69-175">Name of hello operation.</span></span> |
| <span data-ttu-id="3ce69-176">propiedades</span><span class="sxs-lookup"><span data-stu-id="3ce69-176">properties</span></span> |<span data-ttu-id="3ce69-177">Propiedades de evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="3ce69-177">Properties of hello event.</span></span> |
| <span data-ttu-id="3ce69-178">status</span><span class="sxs-lookup"><span data-stu-id="3ce69-178">status</span></span> |<span data-ttu-id="3ce69-179">String.</span><span class="sxs-lookup"><span data-stu-id="3ce69-179">String.</span></span> <span data-ttu-id="3ce69-180">Estado de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3ce69-180">Status of hello operation.</span></span> <span data-ttu-id="3ce69-181">Entre los valores habituales, se incluyen "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span><span class="sxs-lookup"><span data-stu-id="3ce69-181">Common values include: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span></span> |
| <span data-ttu-id="3ce69-182">subStatus</span><span class="sxs-lookup"><span data-stu-id="3ce69-182">subStatus</span></span> |<span data-ttu-id="3ce69-183">Normalmente incluye código de estado HTTP de Hola de llamada REST de hello correspondiente.</span><span class="sxs-lookup"><span data-stu-id="3ce69-183">Usually includes hello HTTP status code of hello corresponding REST call.</span></span> <span data-ttu-id="3ce69-184">También podría incluir otras cadenas que describen un subestado.</span><span class="sxs-lookup"><span data-stu-id="3ce69-184">It might also include other strings describing a substatus.</span></span> <span data-ttu-id="3ce69-185">Entre los valores de subestado habituales se incluyen OK (código de estado HTTP: 200), Created (código de estado HTTP: 201), Accepted (código de estado HTTP: 202), No Content (código de estado HTTP: 204), Bad Request (código de estado HTTP: 400), Not Found (código de estado HTTP: 404), Conflict (código de estado HTTP: 409), Internal Server Error (código de estado HTTP: 500), Service Unavailable (código de estado HTTP: 503) y Gateway Timeout (código de estado HTTP: 504)</span><span class="sxs-lookup"><span data-stu-id="3ce69-185">Common substatus values include: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3ce69-186">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3ce69-186">Next steps</span></span>
* [<span data-ttu-id="3ce69-187">Obtener más información sobre Hola registro de actividad</span><span class="sxs-lookup"><span data-stu-id="3ce69-187">Learn more about hello Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="3ce69-188">Ejecute scripts de Azure Automation (Runbooks) en alertas de Azure</span><span class="sxs-lookup"><span data-stu-id="3ce69-188">Execute Azure Automation scripts (Runbooks) on Azure alerts</span></span>](http://go.microsoft.com/fwlink/?LinkId=627081)
* <span data-ttu-id="3ce69-189">[Use la aplicación lógica toosend un SMS a través de Twilio de una alerta de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="3ce69-189">[Use Logic App toosend an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="3ce69-190">En este ejemplo es para las alertas métricas, pero podría ser modificado toowork con una alerta de registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="3ce69-190">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
* <span data-ttu-id="3ce69-191">[Usar la aplicación lógica toosend un mensaje desde una alerta Azure demora](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="3ce69-191">[Use Logic App toosend a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="3ce69-192">En este ejemplo es para las alertas métricas, pero podría ser modificado toowork con una alerta de registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="3ce69-192">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
* <span data-ttu-id="3ce69-193">[Usar la aplicación lógica toosend un tooan mensaje cola de Azure desde una alerta Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="3ce69-193">[Use Logic App toosend a message tooan Azure Queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="3ce69-194">En este ejemplo es para las alertas métricas, pero podría ser modificado toowork con una alerta de registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="3ce69-194">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
