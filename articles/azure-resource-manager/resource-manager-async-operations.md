---
title: "Operaciones asincrónicas de Azure | Microsoft Docs"
description: "Describe cómo realizar un seguimiento de las operaciones asincrónicas en Azure."
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
ms.openlocfilehash: 9fe3d98cd345aae45722295b6c1b7fc3e9036e95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="track-asynchronous-azure-operations"></a><span data-ttu-id="722c7-103">Seguimiento de las operaciones asincrónicas de Azure</span><span class="sxs-lookup"><span data-stu-id="722c7-103">Track asynchronous Azure operations</span></span>
<span data-ttu-id="722c7-104">Algunas operaciones de REST de Azure se ejecutan asincrónicamente porque la operación no se puede completar rápidamente.</span><span class="sxs-lookup"><span data-stu-id="722c7-104">Some Azure REST operations run asynchronously because the operation cannot be completed quickly.</span></span> <span data-ttu-id="722c7-105">En este tema se describe cómo realizar un seguimiento del estado de las operaciones asincrónicas a través de los valores devueltos en la respuesta.</span><span class="sxs-lookup"><span data-stu-id="722c7-105">This topic describes how to track the status of asynchronous operations through values returned in the response.</span></span>  

## <a name="status-codes-for-asynchronous-operations"></a><span data-ttu-id="722c7-106">Códigos de estado para las operaciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="722c7-106">Status codes for asynchronous operations</span></span>
<span data-ttu-id="722c7-107">Una operación asincrónica devuelve inicialmente un código de estado HTTP de alguno de estos tipos:</span><span class="sxs-lookup"><span data-stu-id="722c7-107">An asynchronous operation initially returns an HTTP status code of either:</span></span>

* <span data-ttu-id="722c7-108">201 (Created)</span><span class="sxs-lookup"><span data-stu-id="722c7-108">201 (Created)</span></span>
* <span data-ttu-id="722c7-109">202 (Accepted)</span><span class="sxs-lookup"><span data-stu-id="722c7-109">202 (Accepted)</span></span> 

<span data-ttu-id="722c7-110">Cuando la operación se completa correctamente, devuelve:</span><span class="sxs-lookup"><span data-stu-id="722c7-110">When the operation successfully completes, it returns either:</span></span>

* <span data-ttu-id="722c7-111">200 (OK)</span><span class="sxs-lookup"><span data-stu-id="722c7-111">200 (OK)</span></span>
* <span data-ttu-id="722c7-112">204 (No Content)</span><span class="sxs-lookup"><span data-stu-id="722c7-112">204 (No Content)</span></span> 

<span data-ttu-id="722c7-113">Consulte la [documentación de la API de REST](/rest/api/) para ver respuestas para la operación que está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="722c7-113">Refer to the [REST API documentation](/rest/api/) to see the responses for the operation you are executing.</span></span> 

## <a name="monitor-status-of-operation"></a><span data-ttu-id="722c7-114">Supervisión del estado de la operación</span><span class="sxs-lookup"><span data-stu-id="722c7-114">Monitor status of operation</span></span>
<span data-ttu-id="722c7-115">Las operaciones asincrónicas de REST devuelven valores de encabezado, que se utilizan para determinar el estado de la operación.</span><span class="sxs-lookup"><span data-stu-id="722c7-115">The asynchronous REST operations return header values, which you use to determine the status of the operation.</span></span> <span data-ttu-id="722c7-116">Hay potencialmente tres valores de encabezado para examinar:</span><span class="sxs-lookup"><span data-stu-id="722c7-116">There are potentially three header values to examine:</span></span>

* <span data-ttu-id="722c7-117">`Azure-AsyncOperation`: dirección URL para comprobar el estado actual de la operación.</span><span class="sxs-lookup"><span data-stu-id="722c7-117">`Azure-AsyncOperation` - URL for checking the ongoing status of the operation.</span></span> <span data-ttu-id="722c7-118">Si la operación devuelve este valor, utilícelo siempre (en lugar de Location) para realizar un seguimiento del estado de la operación.</span><span class="sxs-lookup"><span data-stu-id="722c7-118">If your operation returns this value, always use it (instead of Location) to track the status of the operation.</span></span>
* <span data-ttu-id="722c7-119">`Location`: dirección URL para determinar cuándo se ha completado una operación.</span><span class="sxs-lookup"><span data-stu-id="722c7-119">`Location` - URL for determining when an operation has completed.</span></span> <span data-ttu-id="722c7-120">Use este valor sólo cuando no se devuelva Azure-AsyncOperation.</span><span class="sxs-lookup"><span data-stu-id="722c7-120">Use this value only when Azure-AsyncOperation is not returned.</span></span>
* <span data-ttu-id="722c7-121">`Retry-After`: el número de segundos que deben transcurrir antes de comprobar el estado de la operación asincrónica.</span><span class="sxs-lookup"><span data-stu-id="722c7-121">`Retry-After` - The number of seconds to wait before checking the status of the asynchronous operation.</span></span>

<span data-ttu-id="722c7-122">Sin embargo, no todas las operaciones asincrónicas devuelven todos estos valores.</span><span class="sxs-lookup"><span data-stu-id="722c7-122">However, not every asynchronous operation returns all these values.</span></span> <span data-ttu-id="722c7-123">Por ejemplo, debe evaluar el valor del encabezado Azure-AsyncOperation para una operación y el valor del encabezado Location para otra operación.</span><span class="sxs-lookup"><span data-stu-id="722c7-123">For example, you may need to evaluate the Azure-AsyncOperation header value for one operation, and the Location header value for another operation.</span></span> 

<span data-ttu-id="722c7-124">Puede recuperar los valores de encabezado como recuperaría cualquier valor de encabezado de una solicitud.</span><span class="sxs-lookup"><span data-stu-id="722c7-124">You retrieve the header values as you would retrieve any header value for a request.</span></span> <span data-ttu-id="722c7-125">Por ejemplo, en C#, recupere el valor del encabezado de un objeto `HttpWebResponse` denominado `response` con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="722c7-125">For example, in C#, you retrieve the header value from an `HttpWebResponse` object named `response` with the following code:</span></span>

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a><span data-ttu-id="722c7-126">Solicitud y respuesta de Azure-AsyncOperation</span><span class="sxs-lookup"><span data-stu-id="722c7-126">Azure-AsyncOperation request and response</span></span>

<span data-ttu-id="722c7-127">Para obtener el estado de la operación asincrónica, envíe una solicitud GET a la dirección URL en el valor del encabezado Azure-AsyncOperation.</span><span class="sxs-lookup"><span data-stu-id="722c7-127">To get the status of the asynchronous operation, send a GET request to the URL in Azure-AsyncOperation header value.</span></span>

<span data-ttu-id="722c7-128">El cuerpo de la respuesta de esta operación contiene información sobre la operación.</span><span class="sxs-lookup"><span data-stu-id="722c7-128">The body of the response from this operation contains information about the operation.</span></span> <span data-ttu-id="722c7-129">El ejemplo siguiente muestra los posibles valores devueltos por la operación:</span><span class="sxs-lookup"><span data-stu-id="722c7-129">The following example shows the possible values returned from the operation:</span></span>

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

<span data-ttu-id="722c7-130">Solo se devuelve `status` para todas las respuestas.</span><span class="sxs-lookup"><span data-stu-id="722c7-130">Only `status` is returned for all responses.</span></span> <span data-ttu-id="722c7-131">El objeto de error se devuelve cuando el estado es Failed o Canceled.</span><span class="sxs-lookup"><span data-stu-id="722c7-131">The error object is returned when the status is Failed or Canceled.</span></span> <span data-ttu-id="722c7-132">Todos los demás valores son opcionales; por lo tanto, la respuesta que reciba puede ser diferente del ejemplo.</span><span class="sxs-lookup"><span data-stu-id="722c7-132">All other values are optional; therefore, the response you receive may look different than the example.</span></span>

## <a name="provisioningstate-values"></a><span data-ttu-id="722c7-133">Valores ProvisioningState</span><span class="sxs-lookup"><span data-stu-id="722c7-133">provisioningState values</span></span>

<span data-ttu-id="722c7-134">Las operaciones que crean, actualizan o eliminan (PUT, PATCH, DELETE) un recurso, normalmente devuelven un valor `provisioningState`.</span><span class="sxs-lookup"><span data-stu-id="722c7-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span></span> <span data-ttu-id="722c7-135">Cuando una operación ha finalizado, se devuelve uno de tres valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="722c7-135">When an operation has completed, one of following three values is returned:</span></span> 

* <span data-ttu-id="722c7-136">Correcto</span><span class="sxs-lookup"><span data-stu-id="722c7-136">Succeeded</span></span>
* <span data-ttu-id="722c7-137">Con error</span><span class="sxs-lookup"><span data-stu-id="722c7-137">Failed</span></span>
* <span data-ttu-id="722c7-138">Canceled</span><span class="sxs-lookup"><span data-stu-id="722c7-138">Canceled</span></span>

<span data-ttu-id="722c7-139">Todos los demás valores indican que la operación todavía se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="722c7-139">All other values indicate the operation is still running.</span></span> <span data-ttu-id="722c7-140">El proveedor de recursos puede devolver un valor personalizado que indica su estado.</span><span class="sxs-lookup"><span data-stu-id="722c7-140">The resource provider can return a customized value that indicates its state.</span></span> <span data-ttu-id="722c7-141">Por ejemplo, puede recibir **Accepted** cuando la solicitud se ha recibido y está en ejecución.</span><span class="sxs-lookup"><span data-stu-id="722c7-141">For example, you may receive **Accepted** when the request is received and running.</span></span>

## <a name="example-requests-and-responses"></a><span data-ttu-id="722c7-142">Solicitudes y respuestas de ejemplo</span><span class="sxs-lookup"><span data-stu-id="722c7-142">Example requests and responses</span></span>

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a><span data-ttu-id="722c7-143">Inicio de máquina virtual (202 con Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="722c7-143">Start virtual machine (202 with Azure-AsyncOperation)</span></span>
<span data-ttu-id="722c7-144">En este ejemplo se muestra cómo determinar el estado de la operación **start** para máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="722c7-144">This example shows how to determine the status of **start** operation for virtual machines.</span></span> <span data-ttu-id="722c7-145">La solicitud inicial está en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="722c7-145">The initial request is in the following format:</span></span>

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

<span data-ttu-id="722c7-146">Devuelve el código de estado 202.</span><span class="sxs-lookup"><span data-stu-id="722c7-146">It returns status code 202.</span></span> <span data-ttu-id="722c7-147">Entre los valores de encabezado, verá:</span><span class="sxs-lookup"><span data-stu-id="722c7-147">Among the header values, you see:</span></span>

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="722c7-148">Para comprobar el estado de la operación asincrónica, envíe otra solicitud a esa dirección URL.</span><span class="sxs-lookup"><span data-stu-id="722c7-148">To check the status of the asynchronous operation, sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="722c7-149">El cuerpo de respuesta contiene el estado de la operación:</span><span class="sxs-lookup"><span data-stu-id="722c7-149">The response body contains the status of the operation:</span></span>

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a><span data-ttu-id="722c7-150">Implementación de recursos (201 con Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="722c7-150">Deploy resources (201 with Azure-AsyncOperation)</span></span>

<span data-ttu-id="722c7-151">En este ejemplo se muestra cómo determinar el estado de la operación **deployments** para implementar recursos en Azure.</span><span class="sxs-lookup"><span data-stu-id="722c7-151">This example shows how to determine the status of **deployments** operation for deploying resources to Azure.</span></span> <span data-ttu-id="722c7-152">La solicitud inicial está en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="722c7-152">The initial request is in the following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

<span data-ttu-id="722c7-153">Devuelve el código de estado 201.</span><span class="sxs-lookup"><span data-stu-id="722c7-153">It returns status code 201.</span></span> <span data-ttu-id="722c7-154">El cuerpo de la respuesta incluye:</span><span class="sxs-lookup"><span data-stu-id="722c7-154">The body of the response includes:</span></span>

```json
"provisioningState":"Accepted",
```

<span data-ttu-id="722c7-155">Entre los valores de encabezado, verá:</span><span class="sxs-lookup"><span data-stu-id="722c7-155">Among the header values, you see:</span></span>

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="722c7-156">Para comprobar el estado de la operación asincrónica, envíe otra solicitud a esa dirección URL.</span><span class="sxs-lookup"><span data-stu-id="722c7-156">To check the status of the asynchronous operation, sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="722c7-157">El cuerpo de respuesta contiene el estado de la operación:</span><span class="sxs-lookup"><span data-stu-id="722c7-157">The response body contains the status of the operation:</span></span>

```json
{"status":"Running"}
```

<span data-ttu-id="722c7-158">Cuando haya finalizado la implementación, la respuesta contiene:</span><span class="sxs-lookup"><span data-stu-id="722c7-158">When the deployment is finished, the response contains:</span></span>

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a><span data-ttu-id="722c7-159">Creación de cuenta de almacenamiento (202 con Location y Retry-After)</span><span class="sxs-lookup"><span data-stu-id="722c7-159">Create storage account (202 with Location and Retry-After)</span></span>

<span data-ttu-id="722c7-160">Este ejemplo muestra cómo determinar el estado de la operación **create** para cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="722c7-160">This example shows how to determine the status of the **create** operation for storage accounts.</span></span> <span data-ttu-id="722c7-161">La solicitud inicial está en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="722c7-161">The initial request is in the following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

<span data-ttu-id="722c7-162">Y el cuerpo de solicitud contiene las propiedades de la cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="722c7-162">And the request body contains properties for the storage account:</span></span>

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

<span data-ttu-id="722c7-163">Devuelve el código de estado 202.</span><span class="sxs-lookup"><span data-stu-id="722c7-163">It returns status code 202.</span></span> <span data-ttu-id="722c7-164">Entre los valores de encabezado, vea los dos valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="722c7-164">Among the header values, you see the following two values:</span></span>

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

<span data-ttu-id="722c7-165">Después de esperar el número de segundos especificados en Retry-After, compruebe el estado de la operación asincrónica mediante el envío de otra solicitud a esa dirección URL.</span><span class="sxs-lookup"><span data-stu-id="722c7-165">After waiting for number of seconds specified in Retry-After, check the status of the asynchronous operation by sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

<span data-ttu-id="722c7-166">Si la solicitud aún se está ejecutando, recibe un código de estado 202.</span><span class="sxs-lookup"><span data-stu-id="722c7-166">If the request is still running, you receive a status code 202.</span></span> <span data-ttu-id="722c7-167">Si la solicitud se ha completado, recibe un código de estado 200 y el cuerpo de la respuesta contiene las propiedades de la cuenta de almacenamiento que se ha creado.</span><span class="sxs-lookup"><span data-stu-id="722c7-167">If the request has completed, your receive a status code 200, and the body of the response contains the properties of the storage account that has been created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="722c7-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="722c7-168">Next steps</span></span>

* <span data-ttu-id="722c7-169">Para obtener documentación sobre cada operación de REST, consulte la [documentación de la API de REST](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="722c7-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span></span>
* <span data-ttu-id="722c7-170">Para obtener información acerca de cómo administrar los recursos a través de la API de REST de Resource Manager, consulte [API de REST de Resource Manager](resource-manager-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="722c7-170">For information about managing resources through the Resource Manager REST API, see [Using the Resource Manager REST API](resource-manager-rest-api.md).</span></span>
* <span data-ttu-id="722c7-171">Para obtener información acerca de la implementación de plantillas a través de la API de REST de Resource Manager, consulte [Implementación de recursos con las plantillas de Resource Manager y la API de REST de Resource Manager](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="722c7-171">for information about deploying templates through the Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span></span>