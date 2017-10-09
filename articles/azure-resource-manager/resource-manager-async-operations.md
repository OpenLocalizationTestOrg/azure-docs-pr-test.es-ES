---
title: "operaciones asincrónicas aaaAzure | Documentos de Microsoft"
description: "Describe cómo tootrack operaciones asincrónicas en Azure."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: b81254196013adf87998eff11a50993efa52d40d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="track-asynchronous-azure-operations"></a>Seguimiento de las operaciones asincrónicas de Azure
Algunas operaciones de REST de Azure se ejecutan asincrónicamente porque no se puede completar la operación de hello rápidamente. Este tema describe cómo se devuelve el estado de Hola de tootrack de operaciones asincrónicas a través de los valores de respuesta de Hola.  

## <a name="status-codes-for-asynchronous-operations"></a>Códigos de estado para las operaciones asincrónicas
Una operación asincrónica devuelve inicialmente un código de estado HTTP de alguno de estos tipos:

* 201 (Created)
* 202 (Accepted) 

Cuando se complete correctamente la operación de hello, devuelve:

* 200 (OK)
* 204 (No Content) 

Consulte toohello [documentación de la API de REST](/rest/api/) toosee las respuestas de hello para la operación de Hola se esté ejecutando. 

## <a name="monitor-status-of-operation"></a>Supervisión del estado de la operación
Hola asincrónica REST operaciones devuelto valores de encabezado, que se utiliza el estado de hello toodetermine de Hola operación. Potencialmente existen tooexamine de encabezado de tres valores:

* `Azure-AsyncOperation`-Dirección URL para comprobar el estado actual de la operación de Hola Hola. Si la operación devuelve este valor, utilice siempre el estado de Hola de TI (en lugar de ubicación) tootrack de operación de Hola.
* `Location`: dirección URL para determinar cuándo se ha completado una operación. Use este valor sólo cuando no se devuelva Azure-AsyncOperation.
* `Retry-After`-Hola número de segundos toowait antes de comprobar el estado de saludo de la operación asincrónica de Hola.

Sin embargo, no todas las operaciones asincrónicas devuelven todos estos valores. Por ejemplo, puede necesitar valor del encabezado tooevaluate Hola AsyncOperation de Azure para una operación y el valor del encabezado de ubicación de Hola para otra operación. 

Recuperar valores de encabezado de hello como recuperaría cualquier valor de encabezado de una solicitud. Por ejemplo, en C#, recuperar el valor de encabezado de Hola desde una `HttpWebResponse` objeto denominado `response` con hello siguiente código:

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a>Solicitud y respuesta de Azure-AsyncOperation

estado de hello tooget de operación asincrónica de hello, enviar una dirección URL toohello GET en el valor del encabezado de AsyncOperation de Azure.

Hola cuerpo de respuesta de Hola de esta operación contiene información acerca de la operación de Hola. Hello en el ejemplo siguiente se muestra los valores posibles de hello procedentes de la operación de hello:

```json
{
    "id": "{resource path from GET operation}",
    "name": "{operation-id}", 
    "status" : "Succeeded | Failed | Canceled | {resource provider values}", 
    "startTime": "2017-01-06T20:56:36.002812+00:00",
    "endTime": "2017-01-06T20:56:56.002812+00:00",
    "percentComplete": {double between 0 and 100 },
    "properties": {
        /* Specific resource provider values for successful operations */
    },
    "error" : { 
        "code": "{error code}",  
        "message": "{error description}" 
    }
}
```

Solo se devuelve `status` para todas las respuestas. objeto de error de Hola se devuelve al estado de hello es error o cancelado. Todos los demás valores son opcionales; por lo tanto, respuesta de hello que recibirá puede ser diferente de ejemplo de Hola.

## <a name="provisioningstate-values"></a>Valores ProvisioningState

Las operaciones que crean, actualizan o eliminan (PUT, PATCH, DELETE) un recurso, normalmente devuelven un valor `provisioningState`. Cuando una operación ha finalizado, se devuelve uno de tres valores siguientes: 

* Correcto
* Con error
* Canceled

Todos los otros valores indican la operación de hello todavía se está ejecutando. proveedor de recursos de Hello puede devolver un valor personalizado que indica su estado. Por ejemplo, puede recibir **aceptado** cuando solicitud hello es recibido y en ejecución.

## <a name="example-requests-and-responses"></a>Solicitudes y respuestas de ejemplo

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a>Inicio de máquina virtual (202 con Azure-AsyncOperation)
Este ejemplo muestra cómo toodetermine Hola estado de **iniciar** operación para las máquinas virtuales. solicitud de saludo inicial está en hello siguiendo el formato:

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

Devuelve el código de estado 202. Entre los valores de encabezado de hello, verá:

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

estado de hello toocheck de operación asincrónica de hello, enviar otra solicitud toothat URL.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

cuerpo de respuesta de Hello contiene estado Hola de operación de hello:

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a>Implementación de recursos (201 con Azure-AsyncOperation)

Este ejemplo muestra cómo toodetermine Hola estado de **implementaciones** operación para la implementación de tooAzure de recursos. solicitud de saludo inicial está en hello siguiendo el formato:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

Devuelve el código de estado 201. Hola cuerpo de respuesta de hello incluye:

```json
"provisioningState":"Accepted",
```

Entre los valores de encabezado de hello, verá:

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

estado de hello toocheck de operación asincrónica de hello, enviar otra solicitud toothat URL.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

cuerpo de respuesta de Hello contiene estado Hola de operación de hello:

```json
{"status":"Running"}
```

Cuando haya finalizado la implementación de hello, respuesta de hello contiene:

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a>Creación de cuenta de almacenamiento (202 con Location y Retry-After)

Este ejemplo muestra cómo toodetermine Hola estado de hello **crear** operación las cuentas de almacenamiento. solicitud de saludo inicial está en hello siguiendo el formato:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

Y cuerpo de la solicitud de hello contiene las propiedades de cuenta de almacenamiento de hello:

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

Devuelve el código de estado 202. Entre los valores de encabezado de hello, vea Hola después de dos valores:

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

Después de esperar el número de segundos especifiquen en Retry-After, compruebe el estado de Hola de operación asincrónica de hello mediante el envío de otra dirección URL de toothat de solicitud.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

Si la solicitud de saludo se está ejecutando, recibirá un código de estado 202. Si ha completado la solicitud de hello, el recibir un código de estado 200 y cuerpo de Hola de respuesta de hello contiene propiedades de Hola de cuenta de almacenamiento de Hola que se ha creado.

## <a name="next-steps"></a>Pasos siguientes

* Para obtener documentación sobre cada operación de REST, consulte la [documentación de la API de REST](/rest/api/).
* Para obtener información acerca de cómo administrar los recursos a través de hello API de REST del Administrador de recursos, consulte [hello mediante API de REST del Administrador de recursos](resource-manager-rest-api.md).
* Para obtener información acerca de la implementación de plantillas a través de hello API de REST del Administrador de recursos, consulte [implementar los recursos con plantillas de administrador de recursos y API de REST del Administrador de recursos](resource-group-template-deploy-rest.md).
