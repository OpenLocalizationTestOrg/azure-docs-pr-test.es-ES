---
title: "esquema de eventos de cuadrícula de eventos de aaaAzure"
description: "Se describen las propiedades de Hola que se proporcionan para eventos con la cuadrícula de eventos de Azure."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/15/2017
ms.author: babanisa
ms.openlocfilehash: 37178a5650b93fd9072d9cff3333aae14b2a2ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-event-schema"></a><span data-ttu-id="2dab0-103">Esquema de eventos de Event Grid</span><span class="sxs-lookup"><span data-stu-id="2dab0-103">Event Grid event schema</span></span>

<span data-ttu-id="2dab0-104">Este artículo proporciona propiedades de Hola y el esquema de eventos.</span><span class="sxs-lookup"><span data-stu-id="2dab0-104">This article provides hello properties and schema for events.</span></span> <span data-ttu-id="2dab0-105">Los eventos constan de un conjunto de cinco propiedades de cadena y un objeto de **datos** obligatorios.</span><span class="sxs-lookup"><span data-stu-id="2dab0-105">Events consist of a set of five required string properties and a required **data** object.</span></span> <span data-ttu-id="2dab0-106">propiedades de Hello son eventos tooall comunes de los publicadores.</span><span class="sxs-lookup"><span data-stu-id="2dab0-106">hello properties are common tooall events from any publisher.</span></span> <span data-ttu-id="2dab0-107">Hola **datos** objeto contiene propiedades que son específicas tooeach publisher.</span><span class="sxs-lookup"><span data-stu-id="2dab0-107">hello **data** object contains properties that are specific tooeach publisher.</span></span> <span data-ttu-id="2dab0-108">Para consultar temas de sistema, estas propiedades son de proveedor de recursos toohello específicos, como almacenamiento o concentradores de eventos.</span><span class="sxs-lookup"><span data-stu-id="2dab0-108">For system topics, these properties are specific toohello resource provider, such as Storage or Event Hubs.</span></span>

<span data-ttu-id="2dab0-109">Se envían eventos tooAzure cuadrícula de eventos en una matriz, que puede contener varios objetos de evento.</span><span class="sxs-lookup"><span data-stu-id="2dab0-109">Events are sent tooAzure Event Grid in an array, which can contain multiple event objects.</span></span> <span data-ttu-id="2dab0-110">Si hay solo un único evento, la matriz de hello tiene una longitud de 1.</span><span class="sxs-lookup"><span data-stu-id="2dab0-110">If there is only a single event, hello array has a length of 1.</span></span> 
 
## <a name="event-properties"></a><span data-ttu-id="2dab0-111">Propiedades de evento</span><span class="sxs-lookup"><span data-stu-id="2dab0-111">Event properties</span></span>

<span data-ttu-id="2dab0-112">Todos los eventos contendrán Hola mismo después de datos de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="2dab0-112">All events will contain hello same following top level data.</span></span>

| <span data-ttu-id="2dab0-113">Propiedad</span><span class="sxs-lookup"><span data-stu-id="2dab0-113">Property</span></span> | <span data-ttu-id="2dab0-114">Escriba</span><span class="sxs-lookup"><span data-stu-id="2dab0-114">Type</span></span> | <span data-ttu-id="2dab0-115">Descripción</span><span class="sxs-lookup"><span data-stu-id="2dab0-115">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="2dab0-116">topic</span><span class="sxs-lookup"><span data-stu-id="2dab0-116">topic</span></span> | <span data-ttu-id="2dab0-117">cadena</span><span class="sxs-lookup"><span data-stu-id="2dab0-117">string</span></span> | <span data-ttu-id="2dab0-118">Origen de eventos de toohello de ruta de acceso completa a recursos.</span><span class="sxs-lookup"><span data-stu-id="2dab0-118">Full resource path toohello event source.</span></span> <span data-ttu-id="2dab0-119">En este campo no se puede escribir.</span><span class="sxs-lookup"><span data-stu-id="2dab0-119">This field is not writeable.</span></span> |
| <span data-ttu-id="2dab0-120">subject</span><span class="sxs-lookup"><span data-stu-id="2dab0-120">subject</span></span> | <span data-ttu-id="2dab0-121">cadena</span><span class="sxs-lookup"><span data-stu-id="2dab0-121">string</span></span> | <span data-ttu-id="2dab0-122">Asunto de eventos de toohello de ruta de acceso definida de publicador.</span><span class="sxs-lookup"><span data-stu-id="2dab0-122">Publisher defined path toohello event subject.</span></span> |
| <span data-ttu-id="2dab0-123">eventType</span><span class="sxs-lookup"><span data-stu-id="2dab0-123">eventType</span></span> | <span data-ttu-id="2dab0-124">cadena</span><span class="sxs-lookup"><span data-stu-id="2dab0-124">string</span></span> | <span data-ttu-id="2dab0-125">Uno de hello registra tipos de eventos para este origen de eventos.</span><span class="sxs-lookup"><span data-stu-id="2dab0-125">One of hello registered event types for this event source.</span></span> |
| <span data-ttu-id="2dab0-126">eventTime</span><span class="sxs-lookup"><span data-stu-id="2dab0-126">eventTime</span></span> | <span data-ttu-id="2dab0-127">cadena</span><span class="sxs-lookup"><span data-stu-id="2dab0-127">string</span></span> | <span data-ttu-id="2dab0-128">evento de Hola Hola tiempo se genera en función del tiempo de UTC del proveedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="2dab0-128">hello time hello event is generated based on hello provider's UTC time.</span></span> |
| <span data-ttu-id="2dab0-129">id</span><span class="sxs-lookup"><span data-stu-id="2dab0-129">id</span></span> | <span data-ttu-id="2dab0-130">cadena</span><span class="sxs-lookup"><span data-stu-id="2dab0-130">string</span></span> | <span data-ttu-id="2dab0-131">Identificador único para el evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="2dab0-131">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="2dab0-132">data</span><span class="sxs-lookup"><span data-stu-id="2dab0-132">data</span></span> | <span data-ttu-id="2dab0-133">objeto</span><span class="sxs-lookup"><span data-stu-id="2dab0-133">object</span></span> | <span data-ttu-id="2dab0-134">Proveedor de recursos de toohello específico de datos de evento.</span><span class="sxs-lookup"><span data-stu-id="2dab0-134">Event data specific toohello resource provider.</span></span> |

## <a name="available-event-sources"></a><span data-ttu-id="2dab0-135">Orígenes de eventos disponibles</span><span class="sxs-lookup"><span data-stu-id="2dab0-135">Available event sources</span></span>

<span data-ttu-id="2dab0-136">Hola siguientes orígenes de eventos publica eventos para su uso a través de la cuadrícula de eventos:</span><span class="sxs-lookup"><span data-stu-id="2dab0-136">hello following event sources publish events for consumption via Event Grid:</span></span>

* <span data-ttu-id="2dab0-137">Grupos de recursos (operaciones de administración)</span><span class="sxs-lookup"><span data-stu-id="2dab0-137">Resource Groups (management operations)</span></span>
* <span data-ttu-id="2dab0-138">Suscripciones de Azure (operaciones de administración)</span><span class="sxs-lookup"><span data-stu-id="2dab0-138">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="2dab0-139">Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="2dab0-139">Event Hubs</span></span>
* <span data-ttu-id="2dab0-140">Temas personalizados</span><span class="sxs-lookup"><span data-stu-id="2dab0-140">Custom Topics</span></span>

## <a name="azure-subscriptions"></a><span data-ttu-id="2dab0-141">Suscripciones de Azure</span><span class="sxs-lookup"><span data-stu-id="2dab0-141">Azure Subscriptions</span></span>

<span data-ttu-id="2dab0-142">Las suscripciones de Azure ahora pueden emitir eventos de administración de Azure Resource Manager, como cuando se crea una máquina virtual o se elimina una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2dab0-142">Azure subscriptions can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="2dab0-143">Tipos de eventos disponibles</span><span class="sxs-lookup"><span data-stu-id="2dab0-143">Available event types</span></span>

- <span data-ttu-id="2dab0-144">**Microsoft.Resources.ResourceWriteSuccess**: se genera cuando se realiza una operación de creación o actualización de recursos correctamente.</span><span class="sxs-lookup"><span data-stu-id="2dab0-144">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="2dab0-145">**Microsoft.Resources.ResourceWriteFailure**: se genera cuando se produce un error en una operación de creación o actualización de recursos.</span><span class="sxs-lookup"><span data-stu-id="2dab0-145">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="2dab0-146">**Microsoft.Resources.ResourceWriteCancel**: se genera cuando se cancela una operación de creación o actualización de recursos.</span><span class="sxs-lookup"><span data-stu-id="2dab0-146">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="2dab0-147">**Microsoft.Resources.ResourceDeleteSuccess**: se genera cuando se elimina un recurso correctamente.</span><span class="sxs-lookup"><span data-stu-id="2dab0-147">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="2dab0-148">**Microsoft.Resources.ResourceDeleteFailure**: se genera cuando se produce un error al eliminar una operación de creación o actualización de recursos.</span><span class="sxs-lookup"><span data-stu-id="2dab0-148">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="2dab0-149">**Microsoft.Resources.ResourceDeleteCancel**: se genera cuando se cancela la eliminación de un recurso.</span><span class="sxs-lookup"><span data-stu-id="2dab0-149">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="2dab0-150">Esto sucede cuando se cancela la implementación de una plantilla.</span><span class="sxs-lookup"><span data-stu-id="2dab0-150">This happens when template deployment is cancelled.</span></span>

### <a name="example-event-schema"></a><span data-ttu-id="2dab0-151">Esquema de evento de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2dab0-151">Example event schema</span></span>

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



## <a name="resource-groups"></a><span data-ttu-id="2dab0-152">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="2dab0-152">Resource Groups</span></span>

<span data-ttu-id="2dab0-153">Los grupos de recursos ahora pueden emitir eventos de administración de Azure Resource Manager, como cuando se crea una máquina virtual o se elimina una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2dab0-153">Resource Groups can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="2dab0-154">Tipos de eventos disponibles</span><span class="sxs-lookup"><span data-stu-id="2dab0-154">Available event types</span></span>

- <span data-ttu-id="2dab0-155">**Microsoft.Resources.ResourceWriteSuccess**: se genera cuando se realiza una operación de creación o actualización de recursos correctamente.</span><span class="sxs-lookup"><span data-stu-id="2dab0-155">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="2dab0-156">**Microsoft.Resources.ResourceWriteFailure**: se genera cuando se produce un error en una operación de creación o actualización de recursos.</span><span class="sxs-lookup"><span data-stu-id="2dab0-156">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="2dab0-157">**Microsoft.Resources.ResourceWriteCancel**: se genera cuando se cancela una operación de creación o actualización de recursos.</span><span class="sxs-lookup"><span data-stu-id="2dab0-157">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="2dab0-158">**Microsoft.Resources.ResourceDeleteSuccess**: se genera cuando se elimina un recurso correctamente.</span><span class="sxs-lookup"><span data-stu-id="2dab0-158">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="2dab0-159">**Microsoft.Resources.ResourceDeleteFailure**: se genera cuando se produce un error al eliminar una operación de creación o actualización de recursos.</span><span class="sxs-lookup"><span data-stu-id="2dab0-159">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="2dab0-160">**Microsoft.Resources.ResourceDeleteCancel**: se genera cuando se cancela la eliminación de un recurso.</span><span class="sxs-lookup"><span data-stu-id="2dab0-160">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="2dab0-161">Esto sucede cuando se cancela la implementación de una plantilla.</span><span class="sxs-lookup"><span data-stu-id="2dab0-161">This happens when template deployment is cancelled.</span></span>

### <a name="example-event"></a><span data-ttu-id="2dab0-162">Evento de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2dab0-162">Example event</span></span>

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



## <a name="event-hubs"></a><span data-ttu-id="2dab0-163">Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="2dab0-163">Event Hubs</span></span>

<span data-ttu-id="2dab0-164">Eventos de los centros de eventos están actualmente solo se genera cuando un archivo se envía automáticamente toostorage mediante la característica de captura de Hola.</span><span class="sxs-lookup"><span data-stu-id="2dab0-164">Event Hubs events are currently only emitted when a file is automatically sent toostorage using hello Capture feature.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="2dab0-165">Tipos de eventos disponibles</span><span class="sxs-lookup"><span data-stu-id="2dab0-165">Available event types</span></span>

- <span data-ttu-id="2dab0-166">**Microsoft.EventHub.CaptureFileCreated**: se genera cuando se crea un archivo de captura.</span><span class="sxs-lookup"><span data-stu-id="2dab0-166">**Microsoft.EventHub.CaptureFileCreated**: Raised when a capture file is created.</span></span>

### <a name="example-event"></a><span data-ttu-id="2dab0-167">Evento de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2dab0-167">Example event</span></span>

<span data-ttu-id="2dab0-168">Este evento de ejemplo muestra el esquema Hola de un evento de los centros de eventos que se produce cuando se captura almacena un archivo.</span><span class="sxs-lookup"><span data-stu-id="2dab0-168">This sample event shows hello schema of an Event Hubs event raised when Capture stores a file.</span></span> 

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



## <a name="azure-blob-storage"></a><span data-ttu-id="2dab0-169">Almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="2dab0-169">Azure Blob Storage</span></span>

<span data-ttu-id="2dab0-170">Azure Blob Storage en versión preliminar privada con inicio de sesión para la integración con Event Grid.</span><span class="sxs-lookup"><span data-stu-id="2dab0-170">Azure Blob Storage in private preview with sign-up for integration with Event Grid.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="2dab0-171">Tipos de eventos disponibles</span><span class="sxs-lookup"><span data-stu-id="2dab0-171">Available event types</span></span>

- <span data-ttu-id="2dab0-172">**Microsoft.Storage.BlobCreated**: se genera cuando se crea un blob.</span><span class="sxs-lookup"><span data-stu-id="2dab0-172">**Microsoft.Storage.BlobCreated**: Raised when a blob is created.</span></span>
- <span data-ttu-id="2dab0-173">**Microsoft.Storage.BlobDeleted**: se genera cuando se elimina un blob.</span><span class="sxs-lookup"><span data-stu-id="2dab0-173">**Microsoft.Storage.BlobDeleted**: Raised when a blob is deleted.</span></span>

### <a name="example-event"></a><span data-ttu-id="2dab0-174">Evento de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2dab0-174">Example event</span></span>

<span data-ttu-id="2dab0-175">Este evento de ejemplo muestra el esquema de Hola de un evento de almacenamiento que se desencadena cuando se crea un blob.</span><span class="sxs-lookup"><span data-stu-id="2dab0-175">This sample event shows hello schema of a storage event raised when a blob is created.</span></span> 

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




## <a name="custom-topics"></a><span data-ttu-id="2dab0-176">Temas personalizados</span><span class="sxs-lookup"><span data-stu-id="2dab0-176">Custom Topics</span></span>

<span data-ttu-id="2dab0-177">carga de datos de Hola de sus eventos personalizados definido por el usuario y puede ser cualquier también un formato JSON.</span><span class="sxs-lookup"><span data-stu-id="2dab0-177">hello data payload of your custom events is defined by you and can be any well formated JSON.</span></span> <span data-ttu-id="2dab0-178">datos de nivel superior de Hello deben contener Hola mismo campos como eventos de recursos estándar definidos.</span><span class="sxs-lookup"><span data-stu-id="2dab0-178">hello top level data should contain hello same fields as standard resource defined events.</span></span> <span data-ttu-id="2dab0-179">Al publicar temas de eventos toocustom considere la posibilidad de modelado asunto Hola de su tooaid de eventos en el enrutamiento y el filtrado.</span><span class="sxs-lookup"><span data-stu-id="2dab0-179">When publishing events toocustom topics you should consider modeling hello subject of your events tooaid in routing and filtering.</span></span>

### <a name="example-event"></a><span data-ttu-id="2dab0-180">Evento de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2dab0-180">Example event</span></span>

<span data-ttu-id="2dab0-181">Hola de ejemplo siguiente muestra un evento para un tema personalizado:</span><span class="sxs-lookup"><span data-stu-id="2dab0-181">hello following example shows an event for a custom topic:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="2dab0-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2dab0-182">Next steps</span></span>

* <span data-ttu-id="2dab0-183">Para una cuadrícula de introducción tooEvent, consulte [¿qué es la cuadrícula de eventos?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="2dab0-183">For an introduction tooEvent Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="2dab0-184">toolearn acerca de cómo crear una suscripción de la cuadrícula de eventos, vea [esquema de suscripción de cuadrícula de eventos](subscription-creation-schema.md).</span><span class="sxs-lookup"><span data-stu-id="2dab0-184">toolearn about creating an Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
