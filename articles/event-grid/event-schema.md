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
# <a name="event-grid-event-schema"></a>Esquema de eventos de Event Grid

Este artículo proporciona propiedades de Hola y el esquema de eventos. Los eventos constan de un conjunto de cinco propiedades de cadena y un objeto de **datos** obligatorios. propiedades de Hello son eventos tooall comunes de los publicadores. Hola **datos** objeto contiene propiedades que son específicas tooeach publisher. Para consultar temas de sistema, estas propiedades son de proveedor de recursos toohello específicos, como almacenamiento o concentradores de eventos.

Se envían eventos tooAzure cuadrícula de eventos en una matriz, que puede contener varios objetos de evento. Si hay solo un único evento, la matriz de hello tiene una longitud de 1. 
 
## <a name="event-properties"></a>Propiedades de evento

Todos los eventos contendrán Hola mismo después de datos de nivel superior.

| Propiedad | Escriba | Descripción |
| -------- | ---- | ----------- |
| topic | cadena | Origen de eventos de toohello de ruta de acceso completa a recursos. En este campo no se puede escribir. |
| subject | cadena | Asunto de eventos de toohello de ruta de acceso definida de publicador. |
| eventType | cadena | Uno de hello registra tipos de eventos para este origen de eventos. |
| eventTime | cadena | evento de Hola Hola tiempo se genera en función del tiempo de UTC del proveedor de Hola. |
| id | cadena | Identificador único para el evento de Hola. |
| data | objeto | Proveedor de recursos de toohello específico de datos de evento. |

## <a name="available-event-sources"></a>Orígenes de eventos disponibles

Hola siguientes orígenes de eventos publica eventos para su uso a través de la cuadrícula de eventos:

* Grupos de recursos (operaciones de administración)
* Suscripciones de Azure (operaciones de administración)
* Centros de eventos
* Temas personalizados

## <a name="azure-subscriptions"></a>Suscripciones de Azure

Las suscripciones de Azure ahora pueden emitir eventos de administración de Azure Resource Manager, como cuando se crea una máquina virtual o se elimina una cuenta de almacenamiento.

### <a name="available-event-types"></a>Tipos de eventos disponibles

- **Microsoft.Resources.ResourceWriteSuccess**: se genera cuando se realiza una operación de creación o actualización de recursos correctamente.  
- **Microsoft.Resources.ResourceWriteFailure**: se genera cuando se produce un error en una operación de creación o actualización de recursos.  
- **Microsoft.Resources.ResourceWriteCancel**: se genera cuando se cancela una operación de creación o actualización de recursos.  
- **Microsoft.Resources.ResourceDeleteSuccess**: se genera cuando se elimina un recurso correctamente.  
- **Microsoft.Resources.ResourceDeleteFailure**: se genera cuando se produce un error al eliminar una operación de creación o actualización de recursos.  
- **Microsoft.Resources.ResourceDeleteCancel**: se genera cuando se cancela la eliminación de un recurso. Esto sucede cuando se cancela la implementación de una plantilla.

### <a name="example-event-schema"></a>Esquema de evento de ejemplo

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



## <a name="resource-groups"></a>Grupos de recursos

Los grupos de recursos ahora pueden emitir eventos de administración de Azure Resource Manager, como cuando se crea una máquina virtual o se elimina una cuenta de almacenamiento.

### <a name="available-event-types"></a>Tipos de eventos disponibles

- **Microsoft.Resources.ResourceWriteSuccess**: se genera cuando se realiza una operación de creación o actualización de recursos correctamente.  
- **Microsoft.Resources.ResourceWriteFailure**: se genera cuando se produce un error en una operación de creación o actualización de recursos.  
- **Microsoft.Resources.ResourceWriteCancel**: se genera cuando se cancela una operación de creación o actualización de recursos.  
- **Microsoft.Resources.ResourceDeleteSuccess**: se genera cuando se elimina un recurso correctamente.  
- **Microsoft.Resources.ResourceDeleteFailure**: se genera cuando se produce un error al eliminar una operación de creación o actualización de recursos.  
- **Microsoft.Resources.ResourceDeleteCancel**: se genera cuando se cancela la eliminación de un recurso. Esto sucede cuando se cancela la implementación de una plantilla.

### <a name="example-event"></a>Evento de ejemplo

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



## <a name="event-hubs"></a>Centros de eventos

Eventos de los centros de eventos están actualmente solo se genera cuando un archivo se envía automáticamente toostorage mediante la característica de captura de Hola.

### <a name="available-event-types"></a>Tipos de eventos disponibles

- **Microsoft.EventHub.CaptureFileCreated**: se genera cuando se crea un archivo de captura.

### <a name="example-event"></a>Evento de ejemplo

Este evento de ejemplo muestra el esquema Hola de un evento de los centros de eventos que se produce cuando se captura almacena un archivo. 

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



## <a name="azure-blob-storage"></a>Almacenamiento de blobs de Azure

Azure Blob Storage en versión preliminar privada con inicio de sesión para la integración con Event Grid.

### <a name="available-event-types"></a>Tipos de eventos disponibles

- **Microsoft.Storage.BlobCreated**: se genera cuando se crea un blob.
- **Microsoft.Storage.BlobDeleted**: se genera cuando se elimina un blob.

### <a name="example-event"></a>Evento de ejemplo

Este evento de ejemplo muestra el esquema de Hola de un evento de almacenamiento que se desencadena cuando se crea un blob. 

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




## <a name="custom-topics"></a>Temas personalizados

carga de datos de Hola de sus eventos personalizados definido por el usuario y puede ser cualquier también un formato JSON. datos de nivel superior de Hello deben contener Hola mismo campos como eventos de recursos estándar definidos. Al publicar temas de eventos toocustom considere la posibilidad de modelado asunto Hola de su tooaid de eventos en el enrutamiento y el filtrado.

### <a name="example-event"></a>Evento de ejemplo

Hola de ejemplo siguiente muestra un evento para un tema personalizado:
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

## <a name="next-steps"></a>Pasos siguientes

* Para una cuadrícula de introducción tooEvent, consulte [¿qué es la cuadrícula de eventos?](overview.md)
* toolearn acerca de cómo crear una suscripción de la cuadrícula de eventos, vea [esquema de suscripción de cuadrícula de eventos](subscription-creation-schema.md).
