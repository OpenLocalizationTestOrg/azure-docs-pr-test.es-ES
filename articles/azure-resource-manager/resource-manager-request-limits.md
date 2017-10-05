---
title: "Límites de solicitudes de Azure Resource Manager| Microsoft Docs"
description: "En este artículo se describe cómo usar la limitación con las solicitudes de Azure Resource Manager cuando se han alcanzado los límites de suscripción."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: 6d7eeaf460674c3ab98425a5412ffa465b9ffd1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="f2c9b-103">Limitación de solicitudes de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f2c9b-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="f2c9b-104">Para cada suscripción e inquilino, los límites de Resource Manager leen 15 000 solicitudes y escriben 1200 cada hora.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-104">For each subscription and tenant, Resource Manager limits read requests to 15,000 per hour and write requests to 1,200 per hour.</span></span> <span data-ttu-id="f2c9b-105">Estos límites se aplican a cada instancia de Azure Resource Manage. Hay varias instancias en cada región de Azure y Azure Resource Manager se implementa en todas las regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-105">These limits apply to each Azure Resource Manager instance; there are multiple instances in every Azure region, and Azure Resource Manager is deployed to all Azure regions.</span></span>  <span data-ttu-id="f2c9b-106">Por lo tanto, en la práctica, los límites son eficazmente mucho mayores que los mencionados anteriormente, ya que las solicitudes del usuario se ofrecen normalmente mediante muchas instancias diferentes.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-106">So, in practice, limits are effectively much higher than those listed above, as user requests are generally serviced by many different instances.</span></span>

<span data-ttu-id="f2c9b-107">Si la aplicación o el script alcanza estos límites, debe limitar las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-107">If your application or script reaches these limits, you need to throttle your requests.</span></span> <span data-ttu-id="f2c9b-108">En este tema se muestra cómo determinar las solicitudes restantes que quedan antes de alcanzar el límite y cómo responder cuando se ha alcanzado dicho límite.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-108">This topic shows you how to determine the remaining requests you have before reaching the limit, and how to respond when you have reached the limit.</span></span>

<span data-ttu-id="f2c9b-109">Cuando se alcanza este límite, recibirá el código de estado HTTP **429 Demasiadas solicitudes**.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-109">When you reach the limit, you receive the HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="f2c9b-110">El número de solicitudes se limita a su suscripción o inquilino.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-110">The number of requests is scoped to either your subscription or your tenant.</span></span> <span data-ttu-id="f2c9b-111">Si tiene varias aplicaciones simultáneas realizando solicitudes en su suscripción, estas se agregan conjuntamente para determinar el número de solicitudes restantes.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-111">If you have multiple, concurrent applications making requests in your subscription, the requests from those applications are added together to determine the number of remaining requests.</span></span>

<span data-ttu-id="f2c9b-112">Las solicitudes del ámbito de la suscripción son aquellas en las que se pasan el identificador de suscripción, por ejemplo, al recuperar el recurso de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-112">Subscription scoped requests are ones the involve passing your subscription id, such as retrieving the resource groups in your subscription.</span></span> <span data-ttu-id="f2c9b-113">Las solicitudes del ámbito del inquilino no incluyen el identificador de suscripción, por ejemplo, al recuperar ubicaciones válidas de Azure.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-113">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="f2c9b-114">Solicitudes restantes</span><span class="sxs-lookup"><span data-stu-id="f2c9b-114">Remaining requests</span></span>
<span data-ttu-id="f2c9b-115">Puede determinar el número de solicitudes restantes examinando los encabezados de respuesta.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-115">You can determine the number of remaining requests by examining response headers.</span></span> <span data-ttu-id="f2c9b-116">Cada solicitud incluye valores para el número de las demás solicitudes de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-116">Each request includes values for the number of remaining read and write requests.</span></span> <span data-ttu-id="f2c9b-117">En la tabla siguiente se describen los encabezados de respuesta que puede examinar para esos valores:</span><span class="sxs-lookup"><span data-stu-id="f2c9b-117">The following table describes the response headers you can examine for those values:</span></span>

| <span data-ttu-id="f2c9b-118">Encabezado de respuesta</span><span class="sxs-lookup"><span data-stu-id="f2c9b-118">Response header</span></span> | <span data-ttu-id="f2c9b-119">Descripción</span><span class="sxs-lookup"><span data-stu-id="f2c9b-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f2c9b-120">x-ms-ratelimit-Remaining-Subscription-Reads</span><span class="sxs-lookup"><span data-stu-id="f2c9b-120">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="f2c9b-121">Lecturas restantes del ámbito de la suscripción</span><span class="sxs-lookup"><span data-stu-id="f2c9b-121">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="f2c9b-122">x-ms-ratelimit-Remaining-Subscription-Writes</span><span class="sxs-lookup"><span data-stu-id="f2c9b-122">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="f2c9b-123">Escrituras restantes del ámbito de la suscripción</span><span class="sxs-lookup"><span data-stu-id="f2c9b-123">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="f2c9b-124">x-ms-ratelimit-Remaining-tenant-Reads</span><span class="sxs-lookup"><span data-stu-id="f2c9b-124">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="f2c9b-125">Lecturas restantes del ámbito del inquilino</span><span class="sxs-lookup"><span data-stu-id="f2c9b-125">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="f2c9b-126">x-ms-ratelimit-Remaining-tenant-Writes</span><span class="sxs-lookup"><span data-stu-id="f2c9b-126">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="f2c9b-127">Escrituras restantes del ámbito del inquilino</span><span class="sxs-lookup"><span data-stu-id="f2c9b-127">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="f2c9b-128">x-ms-ratelimit-Remaining-Subscription-Resource-Requests</span><span class="sxs-lookup"><span data-stu-id="f2c9b-128">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="f2c9b-129">Solicitudes de tipos de recursos restantes del ámbito de la suscripción</span><span class="sxs-lookup"><span data-stu-id="f2c9b-129">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="f2c9b-130">Este valor de encabezado solo se devuelve si un servicio ha invalidado el límite predeterminado.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-130">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="f2c9b-131">Resource Manager agrega este valor en lugar de las lecturas o escrituras de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-131">Resource Manager adds this value instead of the subscription reads or writes.</span></span> |
| <span data-ttu-id="f2c9b-132">x-ms-ratelimit-Remaining-Subscription-Resource-Entities-Read</span><span class="sxs-lookup"><span data-stu-id="f2c9b-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="f2c9b-133">Solicitudes de colección de tipos de recursos restantes del ámbito de la suscripción</span><span class="sxs-lookup"><span data-stu-id="f2c9b-133">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="f2c9b-134">Este valor de encabezado solo se devuelve si un servicio ha invalidado el límite predeterminado.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-134">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="f2c9b-135">Este valor proporciona el número de solicitudes de colección restantes (recursos de lista).</span><span class="sxs-lookup"><span data-stu-id="f2c9b-135">This value provides the number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="f2c9b-136">x-ms-ratelimit-Remaining-tenant-Resource-Requests</span><span class="sxs-lookup"><span data-stu-id="f2c9b-136">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="f2c9b-137">Solicitudes de tipos de recurso restantes del ámbito del inquilino</span><span class="sxs-lookup"><span data-stu-id="f2c9b-137">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="f2c9b-138">Este encabezado solo se agrega para las solicitudes en el nivel del inquilino, y solo si un servicio ha invalidado el límite predeterminado.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-138">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> <span data-ttu-id="f2c9b-139">Resource Manager agrega este valor en lugar de las lecturas o escrituras del inquilino.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-139">Resource Manager adds this value instead of the tenant reads or writes.</span></span> |
| <span data-ttu-id="f2c9b-140">x-ms-ratelimit-Remaining-tenant-Resource-Entities-Read</span><span class="sxs-lookup"><span data-stu-id="f2c9b-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="f2c9b-141">Solicitudes de colección de tipos de recursos restantes del ámbito del inquilino</span><span class="sxs-lookup"><span data-stu-id="f2c9b-141">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="f2c9b-142">Este encabezado solo se agrega para las solicitudes en el nivel del inquilino, y solo si un servicio ha invalidado el límite predeterminado.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-142">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> |

## <a name="retrieving-the-header-values"></a><span data-ttu-id="f2c9b-143">Recuperación de los valores de encabezado</span><span class="sxs-lookup"><span data-stu-id="f2c9b-143">Retrieving the header values</span></span>
<span data-ttu-id="f2c9b-144">El proceso de recuperación de estos valores de encabezado del código o el script es igual que el de cualquier valor de encabezado.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-144">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="f2c9b-145">Por ejemplo, en **C#**, recupere el valor del encabezado de un objeto **HttpWebResponse** denominado "**response**"con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="f2c9b-145">For example, in **C#**, you retrieve the header value from an **HttpWebResponse** object named **response** with the following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="f2c9b-146">En **PowerShell**, recupere el valor del encabezado de una operación Invoke-WebRequest.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-146">In **PowerShell**, you retrieve the header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="f2c9b-147">O bien, si quiere ver las solicitudes restantes de depuración, puede proporcionar el parámetro **-Debug** en el cmdlet **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-147">Or, if want to see the remaining requests for debugging, you can provide the **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="f2c9b-148">Que devuelve muchos valores, incluido el siguiente valor de respuesta:</span><span class="sxs-lookup"><span data-stu-id="f2c9b-148">Which returns many values, including the following response value:</span></span>

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

<span data-ttu-id="f2c9b-149">En la **CLI de Azure**, recupere el valor del encabezado mediante la opción más detallada.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-149">In **Azure CLI**, you retrieve the header value by using the more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="f2c9b-150">Que devuelve muchos valores, incluido el siguiente objeto:</span><span class="sxs-lookup"><span data-stu-id="f2c9b-150">Which returns many values, including the following object:</span></span>

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="f2c9b-151">Espera antes de enviar la solicitud siguiente</span><span class="sxs-lookup"><span data-stu-id="f2c9b-151">Waiting before sending next request</span></span>
<span data-ttu-id="f2c9b-152">Cuando alcance el límite de solicitudes, Azure Resource Manager devuelve el código de estado HTTP **429** y un valor **Retry-After** del encabezado.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-152">When you reach the request limit, Resource Manager returns the **429** HTTP status code and a **Retry-After** value in the header.</span></span> <span data-ttu-id="f2c9b-153">El valor **Retry-After** valor especifica el número de segundos que debe esperar (o estar en estado de suspensión) la aplicación antes de enviar la solicitud siguiente.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-153">The **Retry-After** value specifies the number of seconds your application should wait (or sleep) before sending the next request.</span></span> <span data-ttu-id="f2c9b-154">Si envía una solicitud antes de que haya transcurrido el valor de reintento, no se procesa la solicitud y se devuelve un nuevo valor de reintento.</span><span class="sxs-lookup"><span data-stu-id="f2c9b-154">If you send a request before the retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2c9b-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f2c9b-155">Next steps</span></span>

* <span data-ttu-id="f2c9b-156">Para más información acerca de límites y cuotas, consulte [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="f2c9b-156">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="f2c9b-157">Para obtener información sobre el control de solicitudes asincrónicas de REST, vea [Seguimiento de las operaciones asincrónicas de Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="f2c9b-157">To learn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
