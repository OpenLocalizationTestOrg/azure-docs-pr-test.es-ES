---
title: Esquema de eventos de Azure Event Grid
description: Describe las propiedades que se proporcionan para los eventos con Azure Event Grid.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/15/2017
ms.author: babanisa
ms.openlocfilehash: 9e3c7b31ef23b29827d7184dc033227685ed92f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="event-grid-event-schema"></a><span data-ttu-id="65089-103">Esquema de eventos de Event Grid</span><span class="sxs-lookup"><span data-stu-id="65089-103">Event Grid event schema</span></span>

<span data-ttu-id="65089-104">En este artículo se proporcionan las propiedades y los esquemas de los eventos.</span><span class="sxs-lookup"><span data-stu-id="65089-104">This article provides the properties and schema for events.</span></span> <span data-ttu-id="65089-105">Los eventos constan de un conjunto de cinco propiedades de cadena y un objeto de **datos** obligatorios.</span><span class="sxs-lookup"><span data-stu-id="65089-105">Events consist of a set of five required string properties and a required **data** object.</span></span> <span data-ttu-id="65089-106">Las propiedades son comunes a todos los eventos de cualquier anunciante.</span><span class="sxs-lookup"><span data-stu-id="65089-106">The properties are common to all events from any publisher.</span></span> <span data-ttu-id="65089-107">El objeto de **datos** contiene propiedades específicas de cada anunciante.</span><span class="sxs-lookup"><span data-stu-id="65089-107">The **data** object contains properties that are specific to each publisher.</span></span> <span data-ttu-id="65089-108">Para los temas de sistema, estas propiedades son específicas del proveedor de recursos, como Storage o Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="65089-108">For system topics, these properties are specific to the resource provider, such as Storage or Event Hubs.</span></span>

<span data-ttu-id="65089-109">Los eventos se envían a Azure Event Grid en una matriz que puede contener varios objetos de evento.</span><span class="sxs-lookup"><span data-stu-id="65089-109">Events are sent to Azure Event Grid in an array, which can contain multiple event objects.</span></span> <span data-ttu-id="65089-110">Si hay un solo evento, la matriz tiene una longitud de 1.</span><span class="sxs-lookup"><span data-stu-id="65089-110">If there is only a single event, the array has a length of 1.</span></span> 
 
## <a name="event-properties"></a><span data-ttu-id="65089-111">Propiedades de evento</span><span class="sxs-lookup"><span data-stu-id="65089-111">Event properties</span></span>

<span data-ttu-id="65089-112">Todos los eventos contendrán los siguientes datos de nivel superior iguales.</span><span class="sxs-lookup"><span data-stu-id="65089-112">All events will contain the same following top level data.</span></span>

| <span data-ttu-id="65089-113">Propiedad</span><span class="sxs-lookup"><span data-stu-id="65089-113">Property</span></span> | <span data-ttu-id="65089-114">Escriba</span><span class="sxs-lookup"><span data-stu-id="65089-114">Type</span></span> | <span data-ttu-id="65089-115">Descripción</span><span class="sxs-lookup"><span data-stu-id="65089-115">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="65089-116">topic</span><span class="sxs-lookup"><span data-stu-id="65089-116">topic</span></span> | <span data-ttu-id="65089-117">cadena</span><span class="sxs-lookup"><span data-stu-id="65089-117">string</span></span> | <span data-ttu-id="65089-118">Ruta de acceso completa a los recursos del origen del evento.</span><span class="sxs-lookup"><span data-stu-id="65089-118">Full resource path to the event source.</span></span> <span data-ttu-id="65089-119">En este campo no se puede escribir.</span><span class="sxs-lookup"><span data-stu-id="65089-119">This field is not writeable.</span></span> |
| <span data-ttu-id="65089-120">subject</span><span class="sxs-lookup"><span data-stu-id="65089-120">subject</span></span> | <span data-ttu-id="65089-121">cadena</span><span class="sxs-lookup"><span data-stu-id="65089-121">string</span></span> | <span data-ttu-id="65089-122">Ruta al asunto del evento definida por el anunciante.</span><span class="sxs-lookup"><span data-stu-id="65089-122">Publisher defined path to the event subject.</span></span> |
| <span data-ttu-id="65089-123">eventType</span><span class="sxs-lookup"><span data-stu-id="65089-123">eventType</span></span> | <span data-ttu-id="65089-124">cadena</span><span class="sxs-lookup"><span data-stu-id="65089-124">string</span></span> | <span data-ttu-id="65089-125">Uno de los tipos de eventos registrados para este origen de eventos.</span><span class="sxs-lookup"><span data-stu-id="65089-125">One of the registered event types for this event source.</span></span> |
| <span data-ttu-id="65089-126">eventTime</span><span class="sxs-lookup"><span data-stu-id="65089-126">eventTime</span></span> | <span data-ttu-id="65089-127">cadena</span><span class="sxs-lookup"><span data-stu-id="65089-127">string</span></span> | <span data-ttu-id="65089-128">La hora de generación del evento en función de la hora UTC del proveedor.</span><span class="sxs-lookup"><span data-stu-id="65089-128">The time the event is generated based on the provider's UTC time.</span></span> |
| <span data-ttu-id="65089-129">id</span><span class="sxs-lookup"><span data-stu-id="65089-129">id</span></span> | <span data-ttu-id="65089-130">cadena</span><span class="sxs-lookup"><span data-stu-id="65089-130">string</span></span> | <span data-ttu-id="65089-131">Identificador único para el evento</span><span class="sxs-lookup"><span data-stu-id="65089-131">Unique identifier for the event.</span></span> |
| <span data-ttu-id="65089-132">data</span><span class="sxs-lookup"><span data-stu-id="65089-132">data</span></span> | <span data-ttu-id="65089-133">objeto</span><span class="sxs-lookup"><span data-stu-id="65089-133">object</span></span> | <span data-ttu-id="65089-134">Los datos del evento específicos del proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="65089-134">Event data specific to the resource provider.</span></span> |

## <a name="available-event-sources"></a><span data-ttu-id="65089-135">Orígenes de eventos disponibles</span><span class="sxs-lookup"><span data-stu-id="65089-135">Available event sources</span></span>

<span data-ttu-id="65089-136">Los siguientes orígenes de eventos publican eventos para el consumo a través de Event Grid:</span><span class="sxs-lookup"><span data-stu-id="65089-136">The following event sources publish events for consumption via Event Grid:</span></span>

* <span data-ttu-id="65089-137">Grupos de recursos (operaciones de administración)</span><span class="sxs-lookup"><span data-stu-id="65089-137">Resource Groups (management operations)</span></span>
* <span data-ttu-id="65089-138">Suscripciones de Azure (operaciones de administración)</span><span class="sxs-lookup"><span data-stu-id="65089-138">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="65089-139">Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="65089-139">Event Hubs</span></span>
* <span data-ttu-id="65089-140">Temas personalizados</span><span class="sxs-lookup"><span data-stu-id="65089-140">Custom Topics</span></span>

## <a name="azure-subscriptions"></a><span data-ttu-id="65089-141">Suscripciones de Azure</span><span class="sxs-lookup"><span data-stu-id="65089-141">Azure Subscriptions</span></span>

<span data-ttu-id="65089-142">Las suscripciones de Azure ahora pueden emitir eventos de administración de Azure Resource Manager, como cuando se crea una máquina virtual o se elimina una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="65089-142">Azure subscriptions can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="65089-143">Tipos de eventos disponibles</span><span class="sxs-lookup"><span data-stu-id="65089-143">Available event types</span></span>

- <span data-ttu-id="65089-144">**Microsoft.Resources.ResourceWriteSuccess**: se genera cuando se realiza una operación de creación o actualización de recursos correctamente.</span><span class="sxs-lookup"><span data-stu-id="65089-144">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="65089-145">**Microsoft.Resources.ResourceWriteFailure**: se genera cuando se produce un error en una operación de creación o actualización de recursos.</span><span class="sxs-lookup"><span data-stu-id="65089-145">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="65089-146">**Microsoft.Resources.ResourceWriteCancel**: se genera cuando se cancela una operación de creación o actualización de recursos.</span><span class="sxs-lookup"><span data-stu-id="65089-146">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="65089-147">**Microsoft.Resources.ResourceDeleteSuccess**: se genera cuando se elimina un recurso correctamente.</span><span class="sxs-lookup"><span data-stu-id="65089-147">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="65089-148">**Microsoft.Resources.ResourceDeleteFailure**: se genera cuando se produce un error al eliminar una operación de creación o actualización de recursos.</span><span class="sxs-lookup"><span data-stu-id="65089-148">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="65089-149">**Microsoft.Resources.ResourceDeleteCancel**: se genera cuando se cancela la eliminación de un recurso.</span><span class="sxs-lookup"><span data-stu-id="65089-149">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="65089-150">Esto sucede cuando se cancela la implementación de una plantilla.</span><span class="sxs-lookup"><span data-stu-id="65089-150">This happens when template deployment is cancelled.</span></span>

### <a name="example-event-schema"></a><span data-ttu-id="65089-151">Esquema de evento de ejemplo</span><span class="sxs-lookup"><span data-stu-id="65089-151">Example event schema</span></span>

```json
[
    {
    "topic":"/subscriptions/{subscription-id}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="resource-groups"></a><span data-ttu-id="65089-152">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="65089-152">Resource Groups</span></span>

<span data-ttu-id="65089-153">Los grupos de recursos ahora pueden emitir eventos de administración de Azure Resource Manager, como cuando se crea una máquina virtual o se elimina una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="65089-153">Resource Groups can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="65089-154">Tipos de eventos disponibles</span><span class="sxs-lookup"><span data-stu-id="65089-154">Available event types</span></span>

- <span data-ttu-id="65089-155">**Microsoft.Resources.ResourceWriteSuccess**: se genera cuando se realiza una operación de creación o actualización de recursos correctamente.</span><span class="sxs-lookup"><span data-stu-id="65089-155">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="65089-156">**Microsoft.Resources.ResourceWriteFailure**: se genera cuando se produce un error en una operación de creación o actualización de recursos.</span><span class="sxs-lookup"><span data-stu-id="65089-156">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="65089-157">**Microsoft.Resources.ResourceWriteCancel**: se genera cuando se cancela una operación de creación o actualización de recursos.</span><span class="sxs-lookup"><span data-stu-id="65089-157">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="65089-158">**Microsoft.Resources.ResourceDeleteSuccess**: se genera cuando se elimina un recurso correctamente.</span><span class="sxs-lookup"><span data-stu-id="65089-158">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="65089-159">**Microsoft.Resources.ResourceDeleteFailure**: se genera cuando se produce un error al eliminar una operación de creación o actualización de recursos.</span><span class="sxs-lookup"><span data-stu-id="65089-159">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="65089-160">**Microsoft.Resources.ResourceDeleteCancel**: se genera cuando se cancela la eliminación de un recurso.</span><span class="sxs-lookup"><span data-stu-id="65089-160">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="65089-161">Esto sucede cuando se cancela la implementación de una plantilla.</span><span class="sxs-lookup"><span data-stu-id="65089-161">This happens when template deployment is cancelled.</span></span>

### <a name="example-event"></a><span data-ttu-id="65089-162">Evento de ejemplo</span><span class="sxs-lookup"><span data-stu-id="65089-162">Example event</span></span>

```json
[
    {
    "topic":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="event-hubs"></a><span data-ttu-id="65089-163">Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="65089-163">Event Hubs</span></span>

<span data-ttu-id="65089-164">A día de hoy, los eventos de Event Hubs solo se generan cuando se envía automáticamente un archivo al almacenamiento mediante la característica Captura.</span><span class="sxs-lookup"><span data-stu-id="65089-164">Event Hubs events are currently only emitted when a file is automatically sent to storage using the Capture feature.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="65089-165">Tipos de eventos disponibles</span><span class="sxs-lookup"><span data-stu-id="65089-165">Available event types</span></span>

- <span data-ttu-id="65089-166">**Microsoft.EventHub.CaptureFileCreated**: se genera cuando se crea un archivo de captura.</span><span class="sxs-lookup"><span data-stu-id="65089-166">**Microsoft.EventHub.CaptureFileCreated**: Raised when a capture file is created.</span></span>

### <a name="example-event"></a><span data-ttu-id="65089-167">Evento de ejemplo</span><span class="sxs-lookup"><span data-stu-id="65089-167">Example event</span></span>

<span data-ttu-id="65089-168">Este evento de ejemplo muestra el esquema de un evento de Event Hubs que se genera cuando Captura almacena un archivo.</span><span class="sxs-lookup"><span data-stu-id="65089-168">This sample event shows the schema of an Event Hubs event raised when Capture stores a file.</span></span> 

```json
[
    {
        "topic": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.EventHub/namespaces/{event-hubs-ns}",
        "subject": "eventhubs/eh1",
        "eventType": "Microsoft.EventHub.CaptureFileCreated",
        "eventTime": "2017-07-11T00:55:55.0120485Z",
        "id": "bd440490-a65e-4c97-8298-ef1eb325673c",
        "data": {
            "fileUrl": "https://gridtest1.blob.core.windows.net/acontainer/eventgridtest1/eh1/1/2017/07/11/00/54/54.avro",
            "fileType": "AzureBlockBlob",
            "partitionId": "1",
            "sizeInBytes": 0,
            "eventCount": 0,
            "firstSequenceNumber": -1,
            "lastSequenceNumber": -1,
            "firstEnqueueTime": "0001-01-01T00:00:00",
            "lastEnqueueTime": "0001-01-01T00:00:00"
        },
    }
]

```



## <a name="azure-blob-storage"></a><span data-ttu-id="65089-169">Almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="65089-169">Azure Blob Storage</span></span>

<span data-ttu-id="65089-170">Azure Blob Storage en versión preliminar privada con inicio de sesión para la integración con Event Grid.</span><span class="sxs-lookup"><span data-stu-id="65089-170">Azure Blob Storage in private preview with sign-up for integration with Event Grid.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="65089-171">Tipos de eventos disponibles</span><span class="sxs-lookup"><span data-stu-id="65089-171">Available event types</span></span>

- <span data-ttu-id="65089-172">**Microsoft.Storage.BlobCreated**: se genera cuando se crea un blob.</span><span class="sxs-lookup"><span data-stu-id="65089-172">**Microsoft.Storage.BlobCreated**: Raised when a blob is created.</span></span>
- <span data-ttu-id="65089-173">**Microsoft.Storage.BlobDeleted**: se genera cuando se elimina un blob.</span><span class="sxs-lookup"><span data-stu-id="65089-173">**Microsoft.Storage.BlobDeleted**: Raised when a blob is deleted.</span></span>

### <a name="example-event"></a><span data-ttu-id="65089-174">Evento de ejemplo</span><span class="sxs-lookup"><span data-stu-id="65089-174">Example event</span></span>

<span data-ttu-id="65089-175">Este evento de ejemplo muestra el esquema de un evento de almacenamiento que se genera cuando se crea un blob.</span><span class="sxs-lookup"><span data-stu-id="65089-175">This sample event shows the schema of a storage event raised when a blob is created.</span></span> 

```json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.Storage/storageAccounts/xstoretestaccount",
    "subject": "/blobServices/default/containers/oc2d2817345i200097container/blobs/oc2d2817345i20002296blob",
    "eventType": "Microsoft.Storage.BlobCreated",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "id": "831e1650-001e-001b-66ab-eeb76e069631",
    "data": {
      "api": "PutBlockList",
      "clientRequestId": "6d79dbfb-0e37-4fc4-981f-442c9ca65760",
      "requestId": "831e1650-001e-001b-66ab-eeb76e000000",
      "eTag": "0x8D4BCC2E4835CD0",
      "contentType": "application/octet-stream",
      "contentLength": 524288,
      "blobType": "BlockBlob",
      "url": "https://oc2d2817345i60006.blob.core.windows.net/oc2d2817345i200097container/oc2d2817345i20002296blob",
      "sequencer": "00000000000004420000000000028963",
      "storageDiagnostics": {
        "batchId": "b68529f3-68cd-4744-baa4-3c0498ec19f0"
      }
    }
  }
]
```




## <a name="custom-topics"></a><span data-ttu-id="65089-176">Temas personalizados</span><span class="sxs-lookup"><span data-stu-id="65089-176">Custom Topics</span></span>

<span data-ttu-id="65089-177">La carga de datos de los eventos personalizados la define el usuario y puede ser cualquier formato JSON correcto.</span><span class="sxs-lookup"><span data-stu-id="65089-177">The data payload of your custom events is defined by you and can be any well formated JSON.</span></span> <span data-ttu-id="65089-178">Los datos de nivel superior deben contener los mismos campos que los eventos estándar definidos por los recursos.</span><span class="sxs-lookup"><span data-stu-id="65089-178">The top level data should contain the same fields as standard resource defined events.</span></span> <span data-ttu-id="65089-179">Al publicar eventos de temas personalizados debe considerar modelar el asunto de los eventos como ayuda para el enrutamiento y el filtrado.</span><span class="sxs-lookup"><span data-stu-id="65089-179">When publishing events to custom topics you should consider modeling the subject of your events to aid in routing and filtering.</span></span>

### <a name="example-event"></a><span data-ttu-id="65089-180">Evento de ejemplo</span><span class="sxs-lookup"><span data-stu-id="65089-180">Example event</span></span>

<span data-ttu-id="65089-181">En el ejemplo siguiente se muestra un evento de tema personalizado:</span><span class="sxs-lookup"><span data-stu-id="65089-181">The following example shows an event for a custom topic:</span></span>
````json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.EventGrid/topics/myeventgridtopic",
    "subject": "/myapp/vehicles/motorcycles",    
    "id": "b68529f3-68cd-4744-baa4-3c0498ec19e2",
    "eventType": "recordInserted",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "data":{
      "make": "Ducati",
      "model": "Monster"
    }
  }
]

````

## <a name="next-steps"></a><span data-ttu-id="65089-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="65089-182">Next steps</span></span>

* <span data-ttu-id="65089-183">Para ver una introducción a Event Grid, consulte el artículo acerca de [qué es Event Grid](overview.md).</span><span class="sxs-lookup"><span data-stu-id="65089-183">For an introduction to Event Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="65089-184">Para información acerca de la creación de una suscripción de Event Grid, consulte [Event Grid subscription schema](subscription-creation-schema.md) (Esquema de suscripción de Event Grid).</span><span class="sxs-lookup"><span data-stu-id="65089-184">To learn about creating an Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
