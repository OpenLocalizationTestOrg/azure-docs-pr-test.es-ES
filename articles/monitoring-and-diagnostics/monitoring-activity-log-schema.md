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
# <a name="azure-activity-log-event-schema"></a><span data-ttu-id="557cc-103">Esquema de eventos del registro de actividad de Azure</span><span class="sxs-lookup"><span data-stu-id="557cc-103">Azure Activity Log event schema</span></span>
<span data-ttu-id="557cc-104">Hola **Azure Activity Log** es un registro que proporciona una visión general de los eventos de nivel de suscripción que se han producido en Azure.</span><span class="sxs-lookup"><span data-stu-id="557cc-104">hello **Azure Activity Log** is a log that provides insight into any subscription-level events that have occurred in Azure.</span></span> <span data-ttu-id="557cc-105">Este artículo describe el esquema de eventos de Hola por categoría de datos.</span><span class="sxs-lookup"><span data-stu-id="557cc-105">This article describes hello event schema per category of data.</span></span>

## <a name="administrative"></a><span data-ttu-id="557cc-106">Administrativo</span><span class="sxs-lookup"><span data-stu-id="557cc-106">Administrative</span></span>
<span data-ttu-id="557cc-107">Esta categoría contiene el registro de hello de todos los cree, las operaciones update, delete y acción se realizan a través del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="557cc-107">This category contains hello record of all create, update, delete, and action operations performed through Resource Manager.</span></span> <span data-ttu-id="557cc-108">Ejemplos de hello tipos de eventos que aparecen en esta categoría se incluyen "creación la máquina virtual" y "eliminación grupo de seguridad de red" cada acción realizada por un usuario o aplicación con el Administrador de recursos se modela como una operación en un tipo de recurso determinado.</span><span class="sxs-lookup"><span data-stu-id="557cc-108">Examples of hello types of events you would see in this category include "create virtual machine" and "delete network security group" Every action taken by a user or application using Resource Manager is modeled as an operation on a particular resource type.</span></span> <span data-ttu-id="557cc-109">Si el tipo de operación de hello es escribir, eliminar o acción, registros de Hola de inicio de Hola y el éxito o por error de esa operación se registran en la categoría administrativa Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-109">If hello operation type is Write, Delete, or Action, hello records of both hello start and success or fail of that operation are recorded in hello Administrative category.</span></span> <span data-ttu-id="557cc-110">categoría administrativa de Hello también incluye cualquier control de acceso basado en toorole cambios en una suscripción.</span><span class="sxs-lookup"><span data-stu-id="557cc-110">hello Administrative category also includes any changes toorole-based access control in a subscription.</span></span>

### <a name="sample-event"></a><span data-ttu-id="557cc-111">Evento de ejemplo</span><span class="sxs-lookup"><span data-stu-id="557cc-111">Sample event</span></span>
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

### <a name="property-descriptions"></a><span data-ttu-id="557cc-112">Descripciones de propiedades</span><span class="sxs-lookup"><span data-stu-id="557cc-112">Property descriptions</span></span>
| <span data-ttu-id="557cc-113">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="557cc-113">Element Name</span></span> | <span data-ttu-id="557cc-114">Description</span><span class="sxs-lookup"><span data-stu-id="557cc-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="557cc-115">authorization</span><span class="sxs-lookup"><span data-stu-id="557cc-115">authorization</span></span> |<span data-ttu-id="557cc-116">BLOB de propiedades de evento de hello RBAC.</span><span class="sxs-lookup"><span data-stu-id="557cc-116">Blob of RBAC properties of hello event.</span></span> <span data-ttu-id="557cc-117">Normalmente incluye propiedades de "acción", "role" y "ámbito" Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-117">Usually includes hello “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="557cc-118">caller</span><span class="sxs-lookup"><span data-stu-id="557cc-118">caller</span></span> |<span data-ttu-id="557cc-119">Dirección de correo electrónico del usuario de Hola que ha realizado la operación de hello, notificación de UPN o notificación SPN según su disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="557cc-119">Email address of hello user who has performed hello operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="557cc-120">canales nueva</span><span class="sxs-lookup"><span data-stu-id="557cc-120">channels</span></span> |<span data-ttu-id="557cc-121">Uno de hello siguientes valores: "Admin", "Operación"</span><span class="sxs-lookup"><span data-stu-id="557cc-121">One of hello following values: “Admin”, “Operation”</span></span> |
| <span data-ttu-id="557cc-122">claims</span><span class="sxs-lookup"><span data-stu-id="557cc-122">claims</span></span> |<span data-ttu-id="557cc-123">token de JWT de Hello usa Active Directory tooauthenticate Hola usuario o aplicación tooperform esta operación en Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="557cc-123">hello JWT token used by Active Directory tooauthenticate hello user or application tooperform this operation in resource manager.</span></span> |
| <span data-ttu-id="557cc-124">correlationId</span><span class="sxs-lookup"><span data-stu-id="557cc-124">correlationId</span></span> |<span data-ttu-id="557cc-125">Normalmente un GUID en formato de cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-125">Usually a GUID in hello string format.</span></span> <span data-ttu-id="557cc-126">Los eventos que comparten un correlationId pertenecen toohello misma acción.</span><span class="sxs-lookup"><span data-stu-id="557cc-126">Events that share a correlationId belong toohello same uber action.</span></span> |
| <span data-ttu-id="557cc-127">description</span><span class="sxs-lookup"><span data-stu-id="557cc-127">description</span></span> |<span data-ttu-id="557cc-128">Descripción de texto estático de un evento.</span><span class="sxs-lookup"><span data-stu-id="557cc-128">Static text description of an event.</span></span> |
| <span data-ttu-id="557cc-129">eventDataId</span><span class="sxs-lookup"><span data-stu-id="557cc-129">eventDataId</span></span> |<span data-ttu-id="557cc-130">Identificador único de un evento.</span><span class="sxs-lookup"><span data-stu-id="557cc-130">Unique identifier of an event.</span></span> |
| <span data-ttu-id="557cc-131">httpRequest</span><span class="sxs-lookup"><span data-stu-id="557cc-131">httpRequest</span></span> |<span data-ttu-id="557cc-132">Hola BLOB que se describe a solicitud Http.</span><span class="sxs-lookup"><span data-stu-id="557cc-132">Blob describing hello Http Request.</span></span> <span data-ttu-id="557cc-133">Normalmente incluye Estados valores de para saludo "clientRequestId", "clientIpAddress" y "method" (método HTTP.</span><span class="sxs-lookup"><span data-stu-id="557cc-133">Usually includes hello “clientRequestId”, “clientIpAddress” and “method” (HTTP method.</span></span> <span data-ttu-id="557cc-134">Por ejemplo, PUT).</span><span class="sxs-lookup"><span data-stu-id="557cc-134">For example, PUT).</span></span> |
| <span data-ttu-id="557cc-135">level</span><span class="sxs-lookup"><span data-stu-id="557cc-135">level</span></span> |<span data-ttu-id="557cc-136">Nivel de evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-136">Level of hello event.</span></span> <span data-ttu-id="557cc-137">Uno de hello siguientes valores: "Critical", "Error", "Warning", "Informational" y "Verbose"</span><span class="sxs-lookup"><span data-stu-id="557cc-137">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="557cc-138">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="557cc-138">resourceGroupName</span></span> |<span data-ttu-id="557cc-139">Nombre de grupo de recursos de Hola Hola afectado recursos.</span><span class="sxs-lookup"><span data-stu-id="557cc-139">Name of hello resource group for hello impacted resource.</span></span> |
| <span data-ttu-id="557cc-140">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="557cc-140">resourceProviderName</span></span> |<span data-ttu-id="557cc-141">Nombre de proveedor de recursos de Hola para hello afectado recursos</span><span class="sxs-lookup"><span data-stu-id="557cc-141">Name of hello resource provider for hello impacted resource</span></span> |
| <span data-ttu-id="557cc-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="557cc-142">resourceId</span></span> |<span data-ttu-id="557cc-143">Id. de recurso de hello afectado recursos.</span><span class="sxs-lookup"><span data-stu-id="557cc-143">Resource id of hello impacted resource.</span></span> |
| <span data-ttu-id="557cc-144">operationId</span><span class="sxs-lookup"><span data-stu-id="557cc-144">operationId</span></span> |<span data-ttu-id="557cc-145">Un GUID que se comparten entre los eventos de Hola que corresponden tooa única operación.</span><span class="sxs-lookup"><span data-stu-id="557cc-145">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="557cc-146">operationName</span><span class="sxs-lookup"><span data-stu-id="557cc-146">operationName</span></span> |<span data-ttu-id="557cc-147">Nombre de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-147">Name of hello operation.</span></span> |
| <span data-ttu-id="557cc-148">propiedades</span><span class="sxs-lookup"><span data-stu-id="557cc-148">properties</span></span> |<span data-ttu-id="557cc-149">Conjunto de `<Key, Value>` pares (es decir, un diccionario) que se describen los detalles de Hola de evento Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-149">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="557cc-150">status</span><span class="sxs-lookup"><span data-stu-id="557cc-150">status</span></span> |<span data-ttu-id="557cc-151">Cadena que describe el estado de Hola de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-151">String describing hello status of hello operation.</span></span> <span data-ttu-id="557cc-152">Algunos valores habituales son: Started, In Progress, Succeeded, Failed, Active y Resolved.</span><span class="sxs-lookup"><span data-stu-id="557cc-152">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="557cc-153">subStatus</span><span class="sxs-lookup"><span data-stu-id="557cc-153">subStatus</span></span> |<span data-ttu-id="557cc-154">Normalmente Hola código de estado HTTP de hello correspondiente llamada REST, pero también puede incluir otras cadenas que describen un subestado, por ejemplo, estos valores comunes: Aceptar (código de estado HTTP: 200), creado (código de estado HTTP: 201), aceptado (código de estado HTTP: 202), sin contenido (HTTP Código de estado: 204), solicitud incorrecta (código de estado HTTP: 400), pero no se encontraron (código de estado HTTP: 404), conflicto (código de estado HTTP: 409), Error interno del servidor (código de estado HTTP: 500), servicio no está disponible (código de estado HTTP: 503), el tiempo de espera de puerta de enlace (código de estado HTTP: 504).</span><span class="sxs-lookup"><span data-stu-id="557cc-154">Usually hello HTTP status code of hello corresponding REST call, but can also include other strings describing a substatus, such as these common values: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504).</span></span> |
| <span data-ttu-id="557cc-155">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="557cc-155">eventTimestamp</span></span> |<span data-ttu-id="557cc-156">Marca de tiempo cuando se generan eventos de Hola Hola Hola de procesamiento de servicio de Azure solicitar evento Hola correspondiente.</span><span class="sxs-lookup"><span data-stu-id="557cc-156">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="557cc-157">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="557cc-157">submissionTimestamp</span></span> |<span data-ttu-id="557cc-158">Marca de tiempo al evento Hola empezó a estar disponible para las consultas.</span><span class="sxs-lookup"><span data-stu-id="557cc-158">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="557cc-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="557cc-159">subscriptionId</span></span> |<span data-ttu-id="557cc-160">Identificador de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="557cc-160">Azure Subscription Id.</span></span> |

## <a name="service-health"></a><span data-ttu-id="557cc-161">Estado del servicio</span><span class="sxs-lookup"><span data-stu-id="557cc-161">Service health</span></span>
<span data-ttu-id="557cc-162">Esta categoría contiene el registro de hello de los incidentes de mantenimiento de servicio que se han producido en Azure.</span><span class="sxs-lookup"><span data-stu-id="557cc-162">This category contains hello record of any service health incidents that have occurred in Azure.</span></span> <span data-ttu-id="557cc-163">Un ejemplo de Hola tipo de evento que aparecen en esta categoría es "SQL Azure en este de EE. está experimentando tiempos de inactividad".</span><span class="sxs-lookup"><span data-stu-id="557cc-163">An example of hello type of event you would see in this category is "SQL Azure in East US is experiencing downtime."</span></span> <span data-ttu-id="557cc-164">Eventos de estado de servicio vienen en cinco variedades: acción requerida, recuperación asistida, incidente, mantenimiento, información o seguridad y sólo aparece si tiene un recurso de suscripción de Hola que podría verse afectada por los eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-164">Service health events come in five varieties: Action Required, Assisted Recovery, Incident, Maintenance, Information, or Security, and only appear if you have a resource in hello subscription that would be impacted by hello event.</span></span>

### <a name="sample-event"></a><span data-ttu-id="557cc-165">Evento de ejemplo</span><span class="sxs-lookup"><span data-stu-id="557cc-165">Sample event</span></span>
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

### <a name="property-descriptions"></a><span data-ttu-id="557cc-166">Descripciones de propiedades</span><span class="sxs-lookup"><span data-stu-id="557cc-166">Property descriptions</span></span>
<span data-ttu-id="557cc-167">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="557cc-167">Element Name</span></span> | <span data-ttu-id="557cc-168">Descripción</span><span class="sxs-lookup"><span data-stu-id="557cc-168">Description</span></span>
-------- | -----------
<span data-ttu-id="557cc-169">canales nueva</span><span class="sxs-lookup"><span data-stu-id="557cc-169">channels</span></span> | <span data-ttu-id="557cc-170">Es uno de hello siguientes valores: "Admin", "Operación"</span><span class="sxs-lookup"><span data-stu-id="557cc-170">Is one of hello following values: “Admin”, “Operation”</span></span>
<span data-ttu-id="557cc-171">correlationId</span><span class="sxs-lookup"><span data-stu-id="557cc-171">correlationId</span></span> | <span data-ttu-id="557cc-172">Suele ser un GUID en formato de cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-172">Is usually a GUID in hello string format.</span></span> <span data-ttu-id="557cc-173">Eventos que pertenecen toohello normalmente comparten la misma acción Hola mismo correlationId.</span><span class="sxs-lookup"><span data-stu-id="557cc-173">Events with that belong toohello same uber action usually share hello same correlationId.</span></span>
<span data-ttu-id="557cc-174">description</span><span class="sxs-lookup"><span data-stu-id="557cc-174">description</span></span> | <span data-ttu-id="557cc-175">Descripción del evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-175">Description of hello event.</span></span>
<span data-ttu-id="557cc-176">eventDataId</span><span class="sxs-lookup"><span data-stu-id="557cc-176">eventDataId</span></span> | <span data-ttu-id="557cc-177">Hola identificador único de un evento.</span><span class="sxs-lookup"><span data-stu-id="557cc-177">hello unique identifier of an event.</span></span>
<span data-ttu-id="557cc-178">eventName</span><span class="sxs-lookup"><span data-stu-id="557cc-178">eventName</span></span> | <span data-ttu-id="557cc-179">título de Hola de evento Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-179">hello title of hello event.</span></span>
<span data-ttu-id="557cc-180">level</span><span class="sxs-lookup"><span data-stu-id="557cc-180">level</span></span> | <span data-ttu-id="557cc-181">Nivel de evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-181">Level of hello event.</span></span> <span data-ttu-id="557cc-182">Uno de hello siguientes valores: "Critical", "Error", "Warning", "Informational" y "Verbose"</span><span class="sxs-lookup"><span data-stu-id="557cc-182">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span>
<span data-ttu-id="557cc-183">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="557cc-183">resourceProviderName</span></span> | <span data-ttu-id="557cc-184">Nombre de proveedor de recursos de Hola para hello afectado recursos.</span><span class="sxs-lookup"><span data-stu-id="557cc-184">Name of hello resource provider for hello impacted resource.</span></span> <span data-ttu-id="557cc-185">Si es desconocido, será null.</span><span class="sxs-lookup"><span data-stu-id="557cc-185">If not known, this will be null.</span></span>
<span data-ttu-id="557cc-186">resourceType</span><span class="sxs-lookup"><span data-stu-id="557cc-186">resourceType</span></span>| <span data-ttu-id="557cc-187">tipo Hello del recurso de hello afectado recursos.</span><span class="sxs-lookup"><span data-stu-id="557cc-187">hello type of resource of hello impacted resource.</span></span> <span data-ttu-id="557cc-188">Si es desconocido, será null.</span><span class="sxs-lookup"><span data-stu-id="557cc-188">If not known, this will be null.</span></span>
<span data-ttu-id="557cc-189">subStatus</span><span class="sxs-lookup"><span data-stu-id="557cc-189">subStatus</span></span> | <span data-ttu-id="557cc-190">Normalmente es null para los eventos del estado del servicio.</span><span class="sxs-lookup"><span data-stu-id="557cc-190">Usually null for Service Health events.</span></span>
<span data-ttu-id="557cc-191">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="557cc-191">eventTimestamp</span></span> | <span data-ttu-id="557cc-192">Marca de tiempo cuando el evento del registro de hello se generó y envía toohello registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="557cc-192">Timestamp when hello log event was generated and submitted toohello Activity Log.</span></span>
<span data-ttu-id="557cc-193">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="557cc-193">submissionTimestamp</span></span> |   <span data-ttu-id="557cc-194">Marca de tiempo al evento de hello empezó a estar disponible en el registro de actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-194">Timestamp when hello event became available in hello Activity Log.</span></span>
<span data-ttu-id="557cc-195">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="557cc-195">subscriptionId</span></span> | <span data-ttu-id="557cc-196">Hola suscripción de Azure en el que este evento se registra.</span><span class="sxs-lookup"><span data-stu-id="557cc-196">hello Azure subscription in which this event was logged.</span></span>
<span data-ttu-id="557cc-197">status</span><span class="sxs-lookup"><span data-stu-id="557cc-197">status</span></span> | <span data-ttu-id="557cc-198">Cadena que describe el estado de Hola de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-198">String describing hello status of hello operation.</span></span> <span data-ttu-id="557cc-199">Algunos valores comunes: Activo y Resuelto.</span><span class="sxs-lookup"><span data-stu-id="557cc-199">Some common values are: Active, Resolved.</span></span>
<span data-ttu-id="557cc-200">operationName</span><span class="sxs-lookup"><span data-stu-id="557cc-200">operationName</span></span> | <span data-ttu-id="557cc-201">Nombre de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-201">Name of hello operation.</span></span> <span data-ttu-id="557cc-202">Normalmente es Microsoft.ServiceHealth/incident/action.</span><span class="sxs-lookup"><span data-stu-id="557cc-202">Usually Microsoft.ServiceHealth/incident/action.</span></span>
<span data-ttu-id="557cc-203">categoría</span><span class="sxs-lookup"><span data-stu-id="557cc-203">category</span></span> | <span data-ttu-id="557cc-204">"ServiceHealth"</span><span class="sxs-lookup"><span data-stu-id="557cc-204">"ServiceHealth"</span></span>
<span data-ttu-id="557cc-205">resourceId</span><span class="sxs-lookup"><span data-stu-id="557cc-205">resourceId</span></span> | <span data-ttu-id="557cc-206">Id. de recurso de hello afectado el recurso, si se conoce.</span><span class="sxs-lookup"><span data-stu-id="557cc-206">Resource id of hello impacted resource, if known.</span></span> <span data-ttu-id="557cc-207">En caso contrario, se proporciona el identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="557cc-207">Subscription ID is provided otherwise.</span></span>
<span data-ttu-id="557cc-208">Properties.title</span><span class="sxs-lookup"><span data-stu-id="557cc-208">Properties.title</span></span> | <span data-ttu-id="557cc-209">título de Hello localizada para esta comunicación.</span><span class="sxs-lookup"><span data-stu-id="557cc-209">hello localized title for this communication.</span></span> <span data-ttu-id="557cc-210">Idioma predeterminado de hello es inglés.</span><span class="sxs-lookup"><span data-stu-id="557cc-210">English is hello default language.</span></span>
<span data-ttu-id="557cc-211">Properties.communication</span><span class="sxs-lookup"><span data-stu-id="557cc-211">Properties.communication</span></span> | <span data-ttu-id="557cc-212">Hola localizado detalles de comunicación de hello con formato HTML.</span><span class="sxs-lookup"><span data-stu-id="557cc-212">hello localized details of hello communication with HTML markup.</span></span> <span data-ttu-id="557cc-213">Idioma predeterminado de hello es inglés.</span><span class="sxs-lookup"><span data-stu-id="557cc-213">English is hello default.</span></span>
<span data-ttu-id="557cc-214">Properties.incidentType</span><span class="sxs-lookup"><span data-stu-id="557cc-214">Properties.incidentType</span></span> | <span data-ttu-id="557cc-215">Valores posibles: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span><span class="sxs-lookup"><span data-stu-id="557cc-215">Possible values: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span></span>
<span data-ttu-id="557cc-216">Properties.trackingId</span><span class="sxs-lookup"><span data-stu-id="557cc-216">Properties.trackingId</span></span> | <span data-ttu-id="557cc-217">Identifica el incidente de hello que está asociado a este evento.</span><span class="sxs-lookup"><span data-stu-id="557cc-217">Identifies hello incident this event is associated with.</span></span> <span data-ttu-id="557cc-218">Utilice este incidente de toocorrelate Hola eventos tooan relacionados.</span><span class="sxs-lookup"><span data-stu-id="557cc-218">Use this toocorrelate hello events related tooan incident.</span></span>
<span data-ttu-id="557cc-219">Properties.impactedServices</span><span class="sxs-lookup"><span data-stu-id="557cc-219">Properties.impactedServices</span></span> | <span data-ttu-id="557cc-220">Un escape blob JSON que describe los servicios de Hola y regiones que se ven afectadas por incidente Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-220">An escaped JSON blob which describes hello services and regions that are impacted by hello incident.</span></span> <span data-ttu-id="557cc-221">Una lista de servicios, cada uno de los cuales tiene un valor ServiceName y una lista de ImpactedRegions, cada una de los cuales tiene un valor RegionName.</span><span class="sxs-lookup"><span data-stu-id="557cc-221">A list of Services, each of which has a ServiceName and a list of ImpactedRegions, each of which has a RegionName.</span></span>
<span data-ttu-id="557cc-222">Properties.defaultLanguageTitle</span><span class="sxs-lookup"><span data-stu-id="557cc-222">Properties.defaultLanguageTitle</span></span> | <span data-ttu-id="557cc-223">comunicación de saludo en inglés</span><span class="sxs-lookup"><span data-stu-id="557cc-223">hello communication in English</span></span>
<span data-ttu-id="557cc-224">Properties.defaultLanguageContent</span><span class="sxs-lookup"><span data-stu-id="557cc-224">Properties.defaultLanguageContent</span></span> | <span data-ttu-id="557cc-225">comunicación de saludo en inglés como marcado html o texto sin formato</span><span class="sxs-lookup"><span data-stu-id="557cc-225">hello communication in English as either html markup or plain text</span></span>
<span data-ttu-id="557cc-226">Properties.stage</span><span class="sxs-lookup"><span data-stu-id="557cc-226">Properties.stage</span></span> | <span data-ttu-id="557cc-227">Valores posibles de AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security: Active y Resolved.</span><span class="sxs-lookup"><span data-stu-id="557cc-227">Possible values for AssistedRecovery, ActionRequired, Information, Incident, Security: are Active, Resolved.</span></span> <span data-ttu-id="557cc-228">En el caso de Maintenance son: Active, Planned, InProgress, Canceled, Rescheduled, Resolved y Complete</span><span class="sxs-lookup"><span data-stu-id="557cc-228">For Maintenance they are: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span></span>
<span data-ttu-id="557cc-229">Properties.communicationId</span><span class="sxs-lookup"><span data-stu-id="557cc-229">Properties.communicationId</span></span> | <span data-ttu-id="557cc-230">comunicación de Hello este evento está asociado.</span><span class="sxs-lookup"><span data-stu-id="557cc-230">hello communication this event is associated.</span></span>

## <a name="alert"></a><span data-ttu-id="557cc-231">Alerta</span><span class="sxs-lookup"><span data-stu-id="557cc-231">Alert</span></span>
<span data-ttu-id="557cc-232">Esta categoría contiene el registro de hello de todas las activaciones de alertas de Azure.</span><span class="sxs-lookup"><span data-stu-id="557cc-232">This category contains hello record of all activations of Azure alerts.</span></span> <span data-ttu-id="557cc-233">Un ejemplo de Hola tipo de evento que aparecen en esta categoría es "% de CPU en myVM ha sido por encima del 80 para hello últimos 5 minutos".</span><span class="sxs-lookup"><span data-stu-id="557cc-233">An example of hello type of event you would see in this category is "CPU % on myVM has been over 80 for hello past 5 minutes."</span></span> <span data-ttu-id="557cc-234">Varios sistemas de Azure tienen un concepto de alerta: puede definir una regla de algún tipo y recibir una notificación cuando las condiciones coincidan con esa regla.</span><span class="sxs-lookup"><span data-stu-id="557cc-234">A variety of Azure systems have an alerting concept -- you can define a rule of some sort and receive a notification when conditions match that rule.</span></span> <span data-ttu-id="557cc-235">Cada vez que un tipo de alerta de Azure compatible "se activa,' o hello las condiciones son toogenerate cumpla una notificación, un registro de la activación de hello también se inserta toothis categoría de hello registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="557cc-235">Each time a supported Azure alert type 'activates,' or hello conditions are met toogenerate a notification, a record of hello activation is also pushed toothis category of hello Activity Log.</span></span>

### <a name="sample-event"></a><span data-ttu-id="557cc-236">Evento de ejemplo</span><span class="sxs-lookup"><span data-stu-id="557cc-236">Sample event</span></span>

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

### <a name="property-descriptions"></a><span data-ttu-id="557cc-237">Descripciones de propiedades</span><span class="sxs-lookup"><span data-stu-id="557cc-237">Property descriptions</span></span>
| <span data-ttu-id="557cc-238">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="557cc-238">Element Name</span></span> | <span data-ttu-id="557cc-239">Descripción</span><span class="sxs-lookup"><span data-stu-id="557cc-239">Description</span></span> |
| --- | --- |
| <span data-ttu-id="557cc-240">caller</span><span class="sxs-lookup"><span data-stu-id="557cc-240">caller</span></span> | <span data-ttu-id="557cc-241">Siempre es Microsoft.Insights/alertRules.</span><span class="sxs-lookup"><span data-stu-id="557cc-241">Always Microsoft.Insights/alertRules</span></span> |
| <span data-ttu-id="557cc-242">canales nueva</span><span class="sxs-lookup"><span data-stu-id="557cc-242">channels</span></span> | <span data-ttu-id="557cc-243">Siempre es "Admin, Operation".</span><span class="sxs-lookup"><span data-stu-id="557cc-243">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="557cc-244">claims</span><span class="sxs-lookup"><span data-stu-id="557cc-244">claims</span></span> | <span data-ttu-id="557cc-245">Blob JSON con el tipo SPN (nombre principal de servicio), o recurso hello, del motor de alertas de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-245">JSON blob with hello SPN (service principal name), or resource type, of hello alert engine.</span></span> |
| <span data-ttu-id="557cc-246">correlationId</span><span class="sxs-lookup"><span data-stu-id="557cc-246">correlationId</span></span> | <span data-ttu-id="557cc-247">Un GUID en formato de cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-247">A GUID in hello string format.</span></span> |
| <span data-ttu-id="557cc-248">description</span><span class="sxs-lookup"><span data-stu-id="557cc-248">description</span></span> |<span data-ttu-id="557cc-249">Descripción de texto estático de evento de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-249">Static text description of hello alert event.</span></span> |
| <span data-ttu-id="557cc-250">eventDataId</span><span class="sxs-lookup"><span data-stu-id="557cc-250">eventDataId</span></span> |<span data-ttu-id="557cc-251">Identificador único del evento de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-251">Unique identifier of hello alert event.</span></span> |
| <span data-ttu-id="557cc-252">level</span><span class="sxs-lookup"><span data-stu-id="557cc-252">level</span></span> |<span data-ttu-id="557cc-253">Nivel de evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-253">Level of hello event.</span></span> <span data-ttu-id="557cc-254">Uno de hello siguientes valores: "Critical", "Error", "Warning", "Informational" y "Verbose"</span><span class="sxs-lookup"><span data-stu-id="557cc-254">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="557cc-255">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="557cc-255">resourceGroupName</span></span> |<span data-ttu-id="557cc-256">Nombre de grupo de recursos de Hola Hola afectada recursos si se trata de una alerta de métrica.</span><span class="sxs-lookup"><span data-stu-id="557cc-256">Name of hello resource group for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="557cc-257">Para otros tipos de alerta, trata el nombre de Hola Hola del grupo de recursos que contiene la alerta de hello propio.</span><span class="sxs-lookup"><span data-stu-id="557cc-257">For other alert types, this is hello name of hello resource group that contains hello alert itself.</span></span> |
| <span data-ttu-id="557cc-258">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="557cc-258">resourceProviderName</span></span> |<span data-ttu-id="557cc-259">Nombre de proveedor de recursos de Hola para hello afectado recursos si se trata de una alerta de métrica.</span><span class="sxs-lookup"><span data-stu-id="557cc-259">Name of hello resource provider for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="557cc-260">Para otros tipos de alerta, trata Hola nombre de proveedor de recursos de Hola Hola propia lista de alertas.</span><span class="sxs-lookup"><span data-stu-id="557cc-260">For other alert types, this is hello name of hello resource provider for hello alert itself.</span></span> |
| <span data-ttu-id="557cc-261">resourceId</span><span class="sxs-lookup"><span data-stu-id="557cc-261">resourceId</span></span> | <span data-ttu-id="557cc-262">Nombre de Id. de recurso de Hola para hello afectado recursos si se trata de una alerta de métrica.</span><span class="sxs-lookup"><span data-stu-id="557cc-262">Name of hello resource ID for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="557cc-263">Para otros tipos de alerta, se trata de hello Id. de recurso de recurso alerta hello en Sí.</span><span class="sxs-lookup"><span data-stu-id="557cc-263">For other alert types, this is hello resource ID of hello alert resource itself.</span></span> |
| <span data-ttu-id="557cc-264">operationId</span><span class="sxs-lookup"><span data-stu-id="557cc-264">operationId</span></span> |<span data-ttu-id="557cc-265">Un GUID que se comparten entre los eventos de Hola que corresponden tooa única operación.</span><span class="sxs-lookup"><span data-stu-id="557cc-265">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="557cc-266">operationName</span><span class="sxs-lookup"><span data-stu-id="557cc-266">operationName</span></span> |<span data-ttu-id="557cc-267">Nombre de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-267">Name of hello operation.</span></span> |
| <span data-ttu-id="557cc-268">propiedades</span><span class="sxs-lookup"><span data-stu-id="557cc-268">properties</span></span> |<span data-ttu-id="557cc-269">Conjunto de `<Key, Value>` pares (es decir, un diccionario) que se describen los detalles de Hola de evento Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-269">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="557cc-270">status</span><span class="sxs-lookup"><span data-stu-id="557cc-270">status</span></span> |<span data-ttu-id="557cc-271">Cadena que describe el estado de Hola de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-271">String describing hello status of hello operation.</span></span> <span data-ttu-id="557cc-272">Algunos valores habituales son: Started, In Progress, Succeeded, Failed, Active y Resolved.</span><span class="sxs-lookup"><span data-stu-id="557cc-272">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="557cc-273">subStatus</span><span class="sxs-lookup"><span data-stu-id="557cc-273">subStatus</span></span> | <span data-ttu-id="557cc-274">Normalmente es null para las alertas.</span><span class="sxs-lookup"><span data-stu-id="557cc-274">Usually null for alerts.</span></span> |
| <span data-ttu-id="557cc-275">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="557cc-275">eventTimestamp</span></span> |<span data-ttu-id="557cc-276">Marca de tiempo cuando se generan eventos de Hola Hola Hola de procesamiento de servicio de Azure solicitar evento Hola correspondiente.</span><span class="sxs-lookup"><span data-stu-id="557cc-276">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="557cc-277">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="557cc-277">submissionTimestamp</span></span> |<span data-ttu-id="557cc-278">Marca de tiempo al evento Hola empezó a estar disponible para las consultas.</span><span class="sxs-lookup"><span data-stu-id="557cc-278">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="557cc-279">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="557cc-279">subscriptionId</span></span> |<span data-ttu-id="557cc-280">Identificador de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="557cc-280">Azure Subscription Id.</span></span> |

### <a name="properties-field-per-alert-type"></a><span data-ttu-id="557cc-281">Campo Propiedades por tipo de alerta</span><span class="sxs-lookup"><span data-stu-id="557cc-281">Properties field per alert type</span></span>
<span data-ttu-id="557cc-282">campo de propiedades de Hello contendrá diferentes valores en función del origen de Hola de evento de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-282">hello properties field will contain different values depending on hello source of hello alert event.</span></span> <span data-ttu-id="557cc-283">Dos proveedores de eventos de alerta comunes son las alertas de registro de actividad y las alertas de métrica.</span><span class="sxs-lookup"><span data-stu-id="557cc-283">Two common alert event providers are Activity Log alerts and metric alerts.</span></span>

#### <a name="properties-for-activity-log-alerts"></a><span data-ttu-id="557cc-284">Propiedades de las alertas del registro de actividad</span><span class="sxs-lookup"><span data-stu-id="557cc-284">Properties for Activity Log alerts</span></span>
| <span data-ttu-id="557cc-285">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="557cc-285">Element Name</span></span> | <span data-ttu-id="557cc-286">Descripción</span><span class="sxs-lookup"><span data-stu-id="557cc-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="557cc-287">properties.subscriptionId</span><span class="sxs-lookup"><span data-stu-id="557cc-287">properties.subscriptionId</span></span> | <span data-ttu-id="557cc-288">Hola Id. de suscripción de evento de registro de actividad de Hola que produjo este toobe de regla de alerta de registro de actividad activa.</span><span class="sxs-lookup"><span data-stu-id="557cc-288">hello subscription ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="557cc-289">properties.eventDataId</span><span class="sxs-lookup"><span data-stu-id="557cc-289">properties.eventDataId</span></span> | <span data-ttu-id="557cc-290">Hola datos Id. de evento del evento de registro de actividad de Hola que produjo este toobe de regla de alerta de registro de actividad activa.</span><span class="sxs-lookup"><span data-stu-id="557cc-290">hello event data ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="557cc-291">properties.resourceGroup</span><span class="sxs-lookup"><span data-stu-id="557cc-291">properties.resourceGroup</span></span> | <span data-ttu-id="557cc-292">grupo de recursos de Hola de evento de registro de actividad de Hola que produjo este toobe de regla de alerta de registro de actividad activa.</span><span class="sxs-lookup"><span data-stu-id="557cc-292">hello resource group from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="557cc-293">properties.resourceId</span><span class="sxs-lookup"><span data-stu-id="557cc-293">properties.resourceId</span></span> | <span data-ttu-id="557cc-294">Identificador de recurso de Hola de evento de registro de actividad de Hola que produjo este toobe de regla de alerta de registro de actividad activa.</span><span class="sxs-lookup"><span data-stu-id="557cc-294">hello resource ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="557cc-295">properties.eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="557cc-295">properties.eventTimestamp</span></span> | <span data-ttu-id="557cc-296">Hola marca de tiempo de evento del evento de registro de actividad de Hola que produjo este toobe de regla de alerta de registro de actividad activa.</span><span class="sxs-lookup"><span data-stu-id="557cc-296">hello event timestamp of hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="557cc-297">properties.operationName</span><span class="sxs-lookup"><span data-stu-id="557cc-297">properties.operationName</span></span> | <span data-ttu-id="557cc-298">nombre de la operación de Hola de evento de registro de actividad de Hola que produjo este toobe de regla de alerta de registro de actividad activa.</span><span class="sxs-lookup"><span data-stu-id="557cc-298">hello operation name from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="557cc-299">properties.status</span><span class="sxs-lookup"><span data-stu-id="557cc-299">properties.status</span></span> | <span data-ttu-id="557cc-300">estado de Hola de evento de registro de actividad de Hola que produjo este toobe de regla de alerta de registro de actividad activa.</span><span class="sxs-lookup"><span data-stu-id="557cc-300">hello status from hello activity log event which caused this activity log alert rule toobe activated.</span></span>|

#### <a name="properties-for-metric-alerts"></a><span data-ttu-id="557cc-301">Propiedades de las alertas de métrica</span><span class="sxs-lookup"><span data-stu-id="557cc-301">Properties for metric alerts</span></span>
| <span data-ttu-id="557cc-302">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="557cc-302">Element Name</span></span> | <span data-ttu-id="557cc-303">Descripción</span><span class="sxs-lookup"><span data-stu-id="557cc-303">Description</span></span> |
| --- | --- |
| <span data-ttu-id="557cc-304">properties.RuleUri</span><span class="sxs-lookup"><span data-stu-id="557cc-304">properties.RuleUri</span></span> | <span data-ttu-id="557cc-305">Id. de recurso de métrica regla de alerta Hola propio.</span><span class="sxs-lookup"><span data-stu-id="557cc-305">Resource ID of hello metric alert rule itself.</span></span> |
| <span data-ttu-id="557cc-306">properties.RuleName</span><span class="sxs-lookup"><span data-stu-id="557cc-306">properties.RuleName</span></span> | <span data-ttu-id="557cc-307">nombre de Hola de regla de alerta métrica Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-307">hello name of hello metric alert rule.</span></span> |
| <span data-ttu-id="557cc-308">properties.RuleDescription</span><span class="sxs-lookup"><span data-stu-id="557cc-308">properties.RuleDescription</span></span> | <span data-ttu-id="557cc-309">Descripción de Hola de regla de alerta de hello métrica (tal y como se define en la regla de alerta de hello).</span><span class="sxs-lookup"><span data-stu-id="557cc-309">hello description of hello metric alert rule (as defined in hello alert rule).</span></span> |
| <span data-ttu-id="557cc-310">properties.Threshold</span><span class="sxs-lookup"><span data-stu-id="557cc-310">properties.Threshold</span></span> | <span data-ttu-id="557cc-311">valor de umbral de Hello use en la evaluación de Hola de regla de alerta métrica Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-311">hello threshold value used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="557cc-312">properties.WindowSizeInMinutes</span><span class="sxs-lookup"><span data-stu-id="557cc-312">properties.WindowSizeInMinutes</span></span> | <span data-ttu-id="557cc-313">Use en la evaluación de Hola de regla de alerta métrica Hola el tamaño de la ventana de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-313">hello window size used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="557cc-314">properties.Aggregation</span><span class="sxs-lookup"><span data-stu-id="557cc-314">properties.Aggregation</span></span> | <span data-ttu-id="557cc-315">tipo de agregación de Hello definido en la regla de alerta métrica Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-315">hello aggregation type defined in hello metric alert rule.</span></span> |
| <span data-ttu-id="557cc-316">properties.Operator</span><span class="sxs-lookup"><span data-stu-id="557cc-316">properties.Operator</span></span> | <span data-ttu-id="557cc-317">operador condicional de Hola usado en la evaluación de Hola de regla de alerta de métrica de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-317">hello conditional operator used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="557cc-318">properties.MetricName</span><span class="sxs-lookup"><span data-stu-id="557cc-318">properties.MetricName</span></span> | <span data-ttu-id="557cc-319">nombre de la métrica de Hola de métrica de hello utilizada en la evaluación de Hola de regla de alerta métrica Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-319">hello metric name of hello metric used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="557cc-320">properties.MetricUnit</span><span class="sxs-lookup"><span data-stu-id="557cc-320">properties.MetricUnit</span></span> | <span data-ttu-id="557cc-321">Hola métrica unidad métrica de hello utilizada en la evaluación de Hola de regla de alerta métrica Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-321">hello metric unit for hello metric used in hello evaluation of hello metric alert rule.</span></span> |

## <a name="autoscale"></a><span data-ttu-id="557cc-322">Autoscale</span><span class="sxs-lookup"><span data-stu-id="557cc-322">Autoscale</span></span>
<span data-ttu-id="557cc-323">Esta categoría contiene registro de hello de cualquier operación de toohello relacionados de eventos del motor de escalado automático de hello en función de cualquier configuración de escalado automático que ha definido en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="557cc-323">This category contains hello record of any events related toohello operation of hello autoscale engine based on any autoscale settings you have defined in your subscription.</span></span> <span data-ttu-id="557cc-324">Un ejemplo de Hola tipo de evento que aparecen en esta categoría es "Escalado automático ampliación vertical error en la acción".</span><span class="sxs-lookup"><span data-stu-id="557cc-324">An example of hello type of event you would see in this category is "Autoscale scale up action failed."</span></span> <span data-ttu-id="557cc-325">Usar el escalado automático, automáticamente puede escalar horizontalmente o escalar en hello número de instancias de un tipo de recurso compatible se basa en la hora del día y carga datos (métricas) con una configuración de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="557cc-325">Using autoscale, you can automatically scale out or scale in hello number of instances in a supported resource type based on time of day and/or load (metric) data using an autoscale setting.</span></span> <span data-ttu-id="557cc-326">Cuando se cumplen las condiciones de hello tooscale hacia arriba o hacia abajo, Hola inicio y se ha realizado correctamente o eventos de error se registrará en esta categoría.</span><span class="sxs-lookup"><span data-stu-id="557cc-326">When hello conditions are met tooscale up or down, hello start and succeeded or failed events will be recorded in this category.</span></span>

### <a name="sample-event"></a><span data-ttu-id="557cc-327">Evento de ejemplo</span><span class="sxs-lookup"><span data-stu-id="557cc-327">Sample event</span></span>
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

### <a name="property-descriptions"></a><span data-ttu-id="557cc-328">Descripciones de propiedades</span><span class="sxs-lookup"><span data-stu-id="557cc-328">Property descriptions</span></span>
| <span data-ttu-id="557cc-329">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="557cc-329">Element Name</span></span> | <span data-ttu-id="557cc-330">Descripción</span><span class="sxs-lookup"><span data-stu-id="557cc-330">Description</span></span> |
| --- | --- |
| <span data-ttu-id="557cc-331">caller</span><span class="sxs-lookup"><span data-stu-id="557cc-331">caller</span></span> | <span data-ttu-id="557cc-332">Siempre es Microsoft.Insights/autoscaleSettings.</span><span class="sxs-lookup"><span data-stu-id="557cc-332">Always Microsoft.Insights/autoscaleSettings</span></span> |
| <span data-ttu-id="557cc-333">canales nueva</span><span class="sxs-lookup"><span data-stu-id="557cc-333">channels</span></span> | <span data-ttu-id="557cc-334">Siempre es "Admin, Operation".</span><span class="sxs-lookup"><span data-stu-id="557cc-334">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="557cc-335">claims</span><span class="sxs-lookup"><span data-stu-id="557cc-335">claims</span></span> | <span data-ttu-id="557cc-336">Blob JSON con hello tipo SPN (nombre principal de servicio), o el recurso, de motor de escalado automático de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-336">JSON blob with hello SPN (service principal name), or resource type, of hello autoscale engine.</span></span> |
| <span data-ttu-id="557cc-337">correlationId</span><span class="sxs-lookup"><span data-stu-id="557cc-337">correlationId</span></span> | <span data-ttu-id="557cc-338">Un GUID en formato de cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-338">A GUID in hello string format.</span></span> |
| <span data-ttu-id="557cc-339">description</span><span class="sxs-lookup"><span data-stu-id="557cc-339">description</span></span> |<span data-ttu-id="557cc-340">Descripción de texto estático de evento de escalado automático de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-340">Static text description of hello autoscale event.</span></span> |
| <span data-ttu-id="557cc-341">eventDataId</span><span class="sxs-lookup"><span data-stu-id="557cc-341">eventDataId</span></span> |<span data-ttu-id="557cc-342">Identificador único del evento de escalado automático de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-342">Unique identifier of hello autoscale event.</span></span> |
| <span data-ttu-id="557cc-343">level</span><span class="sxs-lookup"><span data-stu-id="557cc-343">level</span></span> |<span data-ttu-id="557cc-344">Nivel de evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-344">Level of hello event.</span></span> <span data-ttu-id="557cc-345">Uno de hello siguientes valores: "Critical", "Error", "Warning", "Informational" y "Verbose"</span><span class="sxs-lookup"><span data-stu-id="557cc-345">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="557cc-346">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="557cc-346">resourceGroupName</span></span> |<span data-ttu-id="557cc-347">Nombre del grupo de recursos de Hola para configuración de escalado automático de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-347">Name of hello resource group for hello autoscale setting.</span></span> |
| <span data-ttu-id="557cc-348">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="557cc-348">resourceProviderName</span></span> |<span data-ttu-id="557cc-349">Nombre del proveedor de recursos de hello para la configuración de escalado automático de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-349">Name of hello resource provider for hello autoscale setting.</span></span> |
| <span data-ttu-id="557cc-350">resourceId</span><span class="sxs-lookup"><span data-stu-id="557cc-350">resourceId</span></span> |<span data-ttu-id="557cc-351">Id. de recurso de configuración de escalado automático de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-351">Resource id of hello autoscale setting.</span></span> |
| <span data-ttu-id="557cc-352">operationId</span><span class="sxs-lookup"><span data-stu-id="557cc-352">operationId</span></span> |<span data-ttu-id="557cc-353">Un GUID que se comparten entre los eventos de Hola que corresponden tooa única operación.</span><span class="sxs-lookup"><span data-stu-id="557cc-353">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="557cc-354">operationName</span><span class="sxs-lookup"><span data-stu-id="557cc-354">operationName</span></span> |<span data-ttu-id="557cc-355">Nombre de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-355">Name of hello operation.</span></span> |
| <span data-ttu-id="557cc-356">propiedades</span><span class="sxs-lookup"><span data-stu-id="557cc-356">properties</span></span> |<span data-ttu-id="557cc-357">Conjunto de `<Key, Value>` pares (es decir, un diccionario) que se describen los detalles de Hola de evento Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-357">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="557cc-358">properties.Description</span><span class="sxs-lookup"><span data-stu-id="557cc-358">properties.Description</span></span> | <span data-ttu-id="557cc-359">Descripción detallada de qué motor de escalado automático de hello hacía.</span><span class="sxs-lookup"><span data-stu-id="557cc-359">Detailed description of what hello autoscale engine was doing.</span></span> |
| <span data-ttu-id="557cc-360">properties.ResourceName</span><span class="sxs-lookup"><span data-stu-id="557cc-360">properties.ResourceName</span></span> | <span data-ttu-id="557cc-361">Id. de recurso de hello afectado recursos (hello en qué Hola se estaba realizando la acción de escalado de recursos)</span><span class="sxs-lookup"><span data-stu-id="557cc-361">Resource ID of hello impacted resource (hello resource on which hello scale action was being performed)</span></span> |
| <span data-ttu-id="557cc-362">properties.OldInstancesCount</span><span class="sxs-lookup"><span data-stu-id="557cc-362">properties.OldInstancesCount</span></span> | <span data-ttu-id="557cc-363">número de Hola de instancias antes de la acción de escalado automático de hello entra en vigor.</span><span class="sxs-lookup"><span data-stu-id="557cc-363">hello number of instances before hello autoscale action took effect.</span></span> |
| <span data-ttu-id="557cc-364">properties.NewInstancesCount</span><span class="sxs-lookup"><span data-stu-id="557cc-364">properties.NewInstancesCount</span></span> | <span data-ttu-id="557cc-365">número de Hola de instancias después de la acción de escalado automático de hello entra en vigor.</span><span class="sxs-lookup"><span data-stu-id="557cc-365">hello number of instances after hello autoscale action took effect.</span></span> |
| <span data-ttu-id="557cc-366">properties.LastScaleActionTime</span><span class="sxs-lookup"><span data-stu-id="557cc-366">properties.LastScaleActionTime</span></span> | <span data-ttu-id="557cc-367">marca de tiempo de Hola de cuando se produjo la acción de escalado automático de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-367">hello timestamp of when hello autoscale action occurred.</span></span> |
| <span data-ttu-id="557cc-368">status</span><span class="sxs-lookup"><span data-stu-id="557cc-368">status</span></span> |<span data-ttu-id="557cc-369">Cadena que describe el estado de Hola de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="557cc-369">String describing hello status of hello operation.</span></span> <span data-ttu-id="557cc-370">Algunos valores habituales son: Started, In Progress, Succeeded, Failed, Active y Resolved.</span><span class="sxs-lookup"><span data-stu-id="557cc-370">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="557cc-371">subStatus</span><span class="sxs-lookup"><span data-stu-id="557cc-371">subStatus</span></span> | <span data-ttu-id="557cc-372">Normalmente es null para el escalado automático.</span><span class="sxs-lookup"><span data-stu-id="557cc-372">Usually null for autoscale.</span></span> |
| <span data-ttu-id="557cc-373">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="557cc-373">eventTimestamp</span></span> |<span data-ttu-id="557cc-374">Marca de tiempo cuando se generan eventos de Hola Hola Hola de procesamiento de servicio de Azure solicitar evento Hola correspondiente.</span><span class="sxs-lookup"><span data-stu-id="557cc-374">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="557cc-375">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="557cc-375">submissionTimestamp</span></span> |<span data-ttu-id="557cc-376">Marca de tiempo al evento Hola empezó a estar disponible para las consultas.</span><span class="sxs-lookup"><span data-stu-id="557cc-376">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="557cc-377">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="557cc-377">subscriptionId</span></span> |<span data-ttu-id="557cc-378">Identificador de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="557cc-378">Azure Subscription Id.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="557cc-379">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="557cc-379">Next steps</span></span>
* [<span data-ttu-id="557cc-380">Obtener más información sobre Hola registro de actividad (anteriormente registros de auditoría)</span><span class="sxs-lookup"><span data-stu-id="557cc-380">Learn more about hello Activity Log (formerly Audit Logs)</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="557cc-381">Transmitir hello Azure Activity Log tooEvent centros</span><span class="sxs-lookup"><span data-stu-id="557cc-381">Stream hello Azure Activity Log tooEvent Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
