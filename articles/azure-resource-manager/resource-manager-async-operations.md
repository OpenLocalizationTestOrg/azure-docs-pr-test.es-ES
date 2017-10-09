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
# <a name="track-asynchronous-azure-operations"></a><span data-ttu-id="94579-103">Seguimiento de las operaciones asincrónicas de Azure</span><span class="sxs-lookup"><span data-stu-id="94579-103">Track asynchronous Azure operations</span></span>
<span data-ttu-id="94579-104">Algunas operaciones de REST de Azure se ejecutan asincrónicamente porque no se puede completar la operación de hello rápidamente.</span><span class="sxs-lookup"><span data-stu-id="94579-104">Some Azure REST operations run asynchronously because hello operation cannot be completed quickly.</span></span> <span data-ttu-id="94579-105">Este tema describe cómo se devuelve el estado de Hola de tootrack de operaciones asincrónicas a través de los valores de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="94579-105">This topic describes how tootrack hello status of asynchronous operations through values returned in hello response.</span></span>  

## <a name="status-codes-for-asynchronous-operations"></a><span data-ttu-id="94579-106">Códigos de estado para las operaciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="94579-106">Status codes for asynchronous operations</span></span>
<span data-ttu-id="94579-107">Una operación asincrónica devuelve inicialmente un código de estado HTTP de alguno de estos tipos:</span><span class="sxs-lookup"><span data-stu-id="94579-107">An asynchronous operation initially returns an HTTP status code of either:</span></span>

* <span data-ttu-id="94579-108">201 (Created)</span><span class="sxs-lookup"><span data-stu-id="94579-108">201 (Created)</span></span>
* <span data-ttu-id="94579-109">202 (Accepted)</span><span class="sxs-lookup"><span data-stu-id="94579-109">202 (Accepted)</span></span> 

<span data-ttu-id="94579-110">Cuando se complete correctamente la operación de hello, devuelve:</span><span class="sxs-lookup"><span data-stu-id="94579-110">When hello operation successfully completes, it returns either:</span></span>

* <span data-ttu-id="94579-111">200 (OK)</span><span class="sxs-lookup"><span data-stu-id="94579-111">200 (OK)</span></span>
* <span data-ttu-id="94579-112">204 (No Content)</span><span class="sxs-lookup"><span data-stu-id="94579-112">204 (No Content)</span></span> 

<span data-ttu-id="94579-113">Consulte toohello [documentación de la API de REST](/rest/api/) toosee las respuestas de hello para la operación de Hola se esté ejecutando.</span><span class="sxs-lookup"><span data-stu-id="94579-113">Refer toohello [REST API documentation](/rest/api/) toosee hello responses for hello operation you are executing.</span></span> 

## <a name="monitor-status-of-operation"></a><span data-ttu-id="94579-114">Supervisión del estado de la operación</span><span class="sxs-lookup"><span data-stu-id="94579-114">Monitor status of operation</span></span>
<span data-ttu-id="94579-115">Hola asincrónica REST operaciones devuelto valores de encabezado, que se utiliza el estado de hello toodetermine de Hola operación.</span><span class="sxs-lookup"><span data-stu-id="94579-115">hello asynchronous REST operations return header values, which you use toodetermine hello status of hello operation.</span></span> <span data-ttu-id="94579-116">Potencialmente existen tooexamine de encabezado de tres valores:</span><span class="sxs-lookup"><span data-stu-id="94579-116">There are potentially three header values tooexamine:</span></span>

* <span data-ttu-id="94579-117">`Azure-AsyncOperation`-Dirección URL para comprobar el estado actual de la operación de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="94579-117">`Azure-AsyncOperation` - URL for checking hello ongoing status of hello operation.</span></span> <span data-ttu-id="94579-118">Si la operación devuelve este valor, utilice siempre el estado de Hola de TI (en lugar de ubicación) tootrack de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="94579-118">If your operation returns this value, always use it (instead of Location) tootrack hello status of hello operation.</span></span>
* <span data-ttu-id="94579-119">`Location`: dirección URL para determinar cuándo se ha completado una operación.</span><span class="sxs-lookup"><span data-stu-id="94579-119">`Location` - URL for determining when an operation has completed.</span></span> <span data-ttu-id="94579-120">Use este valor sólo cuando no se devuelva Azure-AsyncOperation.</span><span class="sxs-lookup"><span data-stu-id="94579-120">Use this value only when Azure-AsyncOperation is not returned.</span></span>
* <span data-ttu-id="94579-121">`Retry-After`-Hola número de segundos toowait antes de comprobar el estado de saludo de la operación asincrónica de Hola.</span><span class="sxs-lookup"><span data-stu-id="94579-121">`Retry-After` - hello number of seconds toowait before checking hello status of hello asynchronous operation.</span></span>

<span data-ttu-id="94579-122">Sin embargo, no todas las operaciones asincrónicas devuelven todos estos valores.</span><span class="sxs-lookup"><span data-stu-id="94579-122">However, not every asynchronous operation returns all these values.</span></span> <span data-ttu-id="94579-123">Por ejemplo, puede necesitar valor del encabezado tooevaluate Hola AsyncOperation de Azure para una operación y el valor del encabezado de ubicación de Hola para otra operación.</span><span class="sxs-lookup"><span data-stu-id="94579-123">For example, you may need tooevaluate hello Azure-AsyncOperation header value for one operation, and hello Location header value for another operation.</span></span> 

<span data-ttu-id="94579-124">Recuperar valores de encabezado de hello como recuperaría cualquier valor de encabezado de una solicitud.</span><span class="sxs-lookup"><span data-stu-id="94579-124">You retrieve hello header values as you would retrieve any header value for a request.</span></span> <span data-ttu-id="94579-125">Por ejemplo, en C#, recuperar el valor de encabezado de Hola desde una `HttpWebResponse` objeto denominado `response` con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="94579-125">For example, in C#, you retrieve hello header value from an `HttpWebResponse` object named `response` with hello following code:</span></span>

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a><span data-ttu-id="94579-126">Solicitud y respuesta de Azure-AsyncOperation</span><span class="sxs-lookup"><span data-stu-id="94579-126">Azure-AsyncOperation request and response</span></span>

<span data-ttu-id="94579-127">estado de hello tooget de operación asincrónica de hello, enviar una dirección URL toohello GET en el valor del encabezado de AsyncOperation de Azure.</span><span class="sxs-lookup"><span data-stu-id="94579-127">tooget hello status of hello asynchronous operation, send a GET request toohello URL in Azure-AsyncOperation header value.</span></span>

<span data-ttu-id="94579-128">Hola cuerpo de respuesta de Hola de esta operación contiene información acerca de la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="94579-128">hello body of hello response from this operation contains information about hello operation.</span></span> <span data-ttu-id="94579-129">Hello en el ejemplo siguiente se muestra los valores posibles de hello procedentes de la operación de hello:</span><span class="sxs-lookup"><span data-stu-id="94579-129">hello following example shows hello possible values returned from hello operation:</span></span>

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

<span data-ttu-id="94579-130">Solo se devuelve `status` para todas las respuestas.</span><span class="sxs-lookup"><span data-stu-id="94579-130">Only `status` is returned for all responses.</span></span> <span data-ttu-id="94579-131">objeto de error de Hola se devuelve al estado de hello es error o cancelado.</span><span class="sxs-lookup"><span data-stu-id="94579-131">hello error object is returned when hello status is Failed or Canceled.</span></span> <span data-ttu-id="94579-132">Todos los demás valores son opcionales; por lo tanto, respuesta de hello que recibirá puede ser diferente de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="94579-132">All other values are optional; therefore, hello response you receive may look different than hello example.</span></span>

## <a name="provisioningstate-values"></a><span data-ttu-id="94579-133">Valores ProvisioningState</span><span class="sxs-lookup"><span data-stu-id="94579-133">provisioningState values</span></span>

<span data-ttu-id="94579-134">Las operaciones que crean, actualizan o eliminan (PUT, PATCH, DELETE) un recurso, normalmente devuelven un valor `provisioningState`.</span><span class="sxs-lookup"><span data-stu-id="94579-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span></span> <span data-ttu-id="94579-135">Cuando una operación ha finalizado, se devuelve uno de tres valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="94579-135">When an operation has completed, one of following three values is returned:</span></span> 

* <span data-ttu-id="94579-136">Correcto</span><span class="sxs-lookup"><span data-stu-id="94579-136">Succeeded</span></span>
* <span data-ttu-id="94579-137">Con error</span><span class="sxs-lookup"><span data-stu-id="94579-137">Failed</span></span>
* <span data-ttu-id="94579-138">Canceled</span><span class="sxs-lookup"><span data-stu-id="94579-138">Canceled</span></span>

<span data-ttu-id="94579-139">Todos los otros valores indican la operación de hello todavía se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="94579-139">All other values indicate hello operation is still running.</span></span> <span data-ttu-id="94579-140">proveedor de recursos de Hello puede devolver un valor personalizado que indica su estado.</span><span class="sxs-lookup"><span data-stu-id="94579-140">hello resource provider can return a customized value that indicates its state.</span></span> <span data-ttu-id="94579-141">Por ejemplo, puede recibir **aceptado** cuando solicitud hello es recibido y en ejecución.</span><span class="sxs-lookup"><span data-stu-id="94579-141">For example, you may receive **Accepted** when hello request is received and running.</span></span>

## <a name="example-requests-and-responses"></a><span data-ttu-id="94579-142">Solicitudes y respuestas de ejemplo</span><span class="sxs-lookup"><span data-stu-id="94579-142">Example requests and responses</span></span>

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a><span data-ttu-id="94579-143">Inicio de máquina virtual (202 con Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="94579-143">Start virtual machine (202 with Azure-AsyncOperation)</span></span>
<span data-ttu-id="94579-144">Este ejemplo muestra cómo toodetermine Hola estado de **iniciar** operación para las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="94579-144">This example shows how toodetermine hello status of **start** operation for virtual machines.</span></span> <span data-ttu-id="94579-145">solicitud de saludo inicial está en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="94579-145">hello initial request is in hello following format:</span></span>

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

<span data-ttu-id="94579-146">Devuelve el código de estado 202.</span><span class="sxs-lookup"><span data-stu-id="94579-146">It returns status code 202.</span></span> <span data-ttu-id="94579-147">Entre los valores de encabezado de hello, verá:</span><span class="sxs-lookup"><span data-stu-id="94579-147">Among hello header values, you see:</span></span>

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="94579-148">estado de hello toocheck de operación asincrónica de hello, enviar otra solicitud toothat URL.</span><span class="sxs-lookup"><span data-stu-id="94579-148">toocheck hello status of hello asynchronous operation, sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="94579-149">cuerpo de respuesta de Hello contiene estado Hola de operación de hello:</span><span class="sxs-lookup"><span data-stu-id="94579-149">hello response body contains hello status of hello operation:</span></span>

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a><span data-ttu-id="94579-150">Implementación de recursos (201 con Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="94579-150">Deploy resources (201 with Azure-AsyncOperation)</span></span>

<span data-ttu-id="94579-151">Este ejemplo muestra cómo toodetermine Hola estado de **implementaciones** operación para la implementación de tooAzure de recursos.</span><span class="sxs-lookup"><span data-stu-id="94579-151">This example shows how toodetermine hello status of **deployments** operation for deploying resources tooAzure.</span></span> <span data-ttu-id="94579-152">solicitud de saludo inicial está en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="94579-152">hello initial request is in hello following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

<span data-ttu-id="94579-153">Devuelve el código de estado 201.</span><span class="sxs-lookup"><span data-stu-id="94579-153">It returns status code 201.</span></span> <span data-ttu-id="94579-154">Hola cuerpo de respuesta de hello incluye:</span><span class="sxs-lookup"><span data-stu-id="94579-154">hello body of hello response includes:</span></span>

```json
"provisioningState":"Accepted",
```

<span data-ttu-id="94579-155">Entre los valores de encabezado de hello, verá:</span><span class="sxs-lookup"><span data-stu-id="94579-155">Among hello header values, you see:</span></span>

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="94579-156">estado de hello toocheck de operación asincrónica de hello, enviar otra solicitud toothat URL.</span><span class="sxs-lookup"><span data-stu-id="94579-156">toocheck hello status of hello asynchronous operation, sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="94579-157">cuerpo de respuesta de Hello contiene estado Hola de operación de hello:</span><span class="sxs-lookup"><span data-stu-id="94579-157">hello response body contains hello status of hello operation:</span></span>

```json
{"status":"Running"}
```

<span data-ttu-id="94579-158">Cuando haya finalizado la implementación de hello, respuesta de hello contiene:</span><span class="sxs-lookup"><span data-stu-id="94579-158">When hello deployment is finished, hello response contains:</span></span>

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a><span data-ttu-id="94579-159">Creación de cuenta de almacenamiento (202 con Location y Retry-After)</span><span class="sxs-lookup"><span data-stu-id="94579-159">Create storage account (202 with Location and Retry-After)</span></span>

<span data-ttu-id="94579-160">Este ejemplo muestra cómo toodetermine Hola estado de hello **crear** operación las cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="94579-160">This example shows how toodetermine hello status of hello **create** operation for storage accounts.</span></span> <span data-ttu-id="94579-161">solicitud de saludo inicial está en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="94579-161">hello initial request is in hello following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

<span data-ttu-id="94579-162">Y cuerpo de la solicitud de hello contiene las propiedades de cuenta de almacenamiento de hello:</span><span class="sxs-lookup"><span data-stu-id="94579-162">And hello request body contains properties for hello storage account:</span></span>

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

<span data-ttu-id="94579-163">Devuelve el código de estado 202.</span><span class="sxs-lookup"><span data-stu-id="94579-163">It returns status code 202.</span></span> <span data-ttu-id="94579-164">Entre los valores de encabezado de hello, vea Hola después de dos valores:</span><span class="sxs-lookup"><span data-stu-id="94579-164">Among hello header values, you see hello following two values:</span></span>

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

<span data-ttu-id="94579-165">Después de esperar el número de segundos especifiquen en Retry-After, compruebe el estado de Hola de operación asincrónica de hello mediante el envío de otra dirección URL de toothat de solicitud.</span><span class="sxs-lookup"><span data-stu-id="94579-165">After waiting for number of seconds specified in Retry-After, check hello status of hello asynchronous operation by sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

<span data-ttu-id="94579-166">Si la solicitud de saludo se está ejecutando, recibirá un código de estado 202.</span><span class="sxs-lookup"><span data-stu-id="94579-166">If hello request is still running, you receive a status code 202.</span></span> <span data-ttu-id="94579-167">Si ha completado la solicitud de hello, el recibir un código de estado 200 y cuerpo de Hola de respuesta de hello contiene propiedades de Hola de cuenta de almacenamiento de Hola que se ha creado.</span><span class="sxs-lookup"><span data-stu-id="94579-167">If hello request has completed, your receive a status code 200, and hello body of hello response contains hello properties of hello storage account that has been created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94579-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="94579-168">Next steps</span></span>

* <span data-ttu-id="94579-169">Para obtener documentación sobre cada operación de REST, consulte la [documentación de la API de REST](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="94579-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span></span>
* <span data-ttu-id="94579-170">Para obtener información acerca de cómo administrar los recursos a través de hello API de REST del Administrador de recursos, consulte [hello mediante API de REST del Administrador de recursos](resource-manager-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="94579-170">For information about managing resources through hello Resource Manager REST API, see [Using hello Resource Manager REST API](resource-manager-rest-api.md).</span></span>
* <span data-ttu-id="94579-171">Para obtener información acerca de la implementación de plantillas a través de hello API de REST del Administrador de recursos, consulte [implementar los recursos con plantillas de administrador de recursos y API de REST del Administrador de recursos](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="94579-171">for information about deploying templates through hello Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span></span>
