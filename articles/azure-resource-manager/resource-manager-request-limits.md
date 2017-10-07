---
title: "límites de solicitudes del Administrador de recursos aaaAzure | Documentos de Microsoft"
description: "Describe cómo las solicitudes toouse limitación con el Administrador de recursos de Azure cuando se han alcanzado los límites de suscripción."
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
ms.openlocfilehash: ea274f3145af36aac753730e1f280d8a8b59c3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="54379-103">Limitación de solicitudes de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="54379-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="54379-104">Para cada suscripción y el inquilino, límites de administrador de recursos leen las solicitudes too15, 000 por hora y escribir solicitudes too1, 200 por hora.</span><span class="sxs-lookup"><span data-stu-id="54379-104">For each subscription and tenant, Resource Manager limits read requests too15,000 per hour and write requests too1,200 per hour.</span></span> <span data-ttu-id="54379-105">Estos límites aplican tooeach instancia de Azure Resource Manager; Hay varias instancias de cada región de Azure y Azure Resource Manager está implementado tooall Azure regiones.</span><span class="sxs-lookup"><span data-stu-id="54379-105">These limits apply tooeach Azure Resource Manager instance; there are multiple instances in every Azure region, and Azure Resource Manager is deployed tooall Azure regions.</span></span>  <span data-ttu-id="54379-106">Por lo tanto, en la práctica, los límites son eficazmente mucho mayores que los mencionados anteriormente, ya que las solicitudes del usuario se ofrecen normalmente mediante muchas instancias diferentes.</span><span class="sxs-lookup"><span data-stu-id="54379-106">So, in practice, limits are effectively much higher than those listed above, as user requests are generally serviced by many different instances.</span></span>

<span data-ttu-id="54379-107">Si la aplicación o el script alcanza estos límites, debe toothrottle las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="54379-107">If your application or script reaches these limits, you need toothrottle your requests.</span></span> <span data-ttu-id="54379-108">Este tema muestra cómo hello toodetermine restante solicita tiene antes de llegar al límite de Hola y cómo toorespond cuando se ha alcanzado el límite de Hola.</span><span class="sxs-lookup"><span data-stu-id="54379-108">This topic shows you how toodetermine hello remaining requests you have before reaching hello limit, and how toorespond when you have reached hello limit.</span></span>

<span data-ttu-id="54379-109">Cuando alcance el límite de hello, recibirá un código de estado HTTP de hello **429 demasiadas solicitudes**.</span><span class="sxs-lookup"><span data-stu-id="54379-109">When you reach hello limit, you receive hello HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="54379-110">número de solicitudes de Hola es tooeither con ámbito de su suscripción o el inquilino.</span><span class="sxs-lookup"><span data-stu-id="54379-110">hello number of requests is scoped tooeither your subscription or your tenant.</span></span> <span data-ttu-id="54379-111">Si tiene varias, aplicaciones simultáneas realizar solicitudes en su suscripción, las solicitudes de Hola de esas aplicaciones se suman toodetermine número de Hola de las solicitudes restantes.</span><span class="sxs-lookup"><span data-stu-id="54379-111">If you have multiple, concurrent applications making requests in your subscription, hello requests from those applications are added together toodetermine hello number of remaining requests.</span></span>

<span data-ttu-id="54379-112">Las solicitudes de suscripción ámbito son los Hola implican pasar el identificador de suscripción, como la recuperación de grupos de recursos de hello en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="54379-112">Subscription scoped requests are ones hello involve passing your subscription id, such as retrieving hello resource groups in your subscription.</span></span> <span data-ttu-id="54379-113">Las solicitudes del ámbito del inquilino no incluyen el identificador de suscripción, por ejemplo, al recuperar ubicaciones válidas de Azure.</span><span class="sxs-lookup"><span data-stu-id="54379-113">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="54379-114">Solicitudes restantes</span><span class="sxs-lookup"><span data-stu-id="54379-114">Remaining requests</span></span>
<span data-ttu-id="54379-115">Puede determinar el número de Hola de las solicitudes restantes examinando los encabezados de respuesta.</span><span class="sxs-lookup"><span data-stu-id="54379-115">You can determine hello number of remaining requests by examining response headers.</span></span> <span data-ttu-id="54379-116">Cada solicitud incluye valores de número de Hola de restante solicitudes de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="54379-116">Each request includes values for hello number of remaining read and write requests.</span></span> <span data-ttu-id="54379-117">Hello tabla siguiente describen los encabezados de respuesta de hello que puede examinar para esos valores:</span><span class="sxs-lookup"><span data-stu-id="54379-117">hello following table describes hello response headers you can examine for those values:</span></span>

| <span data-ttu-id="54379-118">Encabezado de respuesta</span><span class="sxs-lookup"><span data-stu-id="54379-118">Response header</span></span> | <span data-ttu-id="54379-119">Descripción</span><span class="sxs-lookup"><span data-stu-id="54379-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="54379-120">x-ms-ratelimit-Remaining-Subscription-Reads</span><span class="sxs-lookup"><span data-stu-id="54379-120">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="54379-121">Lecturas restantes del ámbito de la suscripción</span><span class="sxs-lookup"><span data-stu-id="54379-121">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="54379-122">x-ms-ratelimit-Remaining-Subscription-Writes</span><span class="sxs-lookup"><span data-stu-id="54379-122">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="54379-123">Escrituras restantes del ámbito de la suscripción</span><span class="sxs-lookup"><span data-stu-id="54379-123">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="54379-124">x-ms-ratelimit-Remaining-tenant-Reads</span><span class="sxs-lookup"><span data-stu-id="54379-124">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="54379-125">Lecturas restantes del ámbito del inquilino</span><span class="sxs-lookup"><span data-stu-id="54379-125">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="54379-126">x-ms-ratelimit-Remaining-tenant-Writes</span><span class="sxs-lookup"><span data-stu-id="54379-126">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="54379-127">Escrituras restantes del ámbito del inquilino</span><span class="sxs-lookup"><span data-stu-id="54379-127">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="54379-128">x-ms-ratelimit-Remaining-Subscription-Resource-Requests</span><span class="sxs-lookup"><span data-stu-id="54379-128">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="54379-129">Solicitudes de tipos de recursos restantes del ámbito de la suscripción</span><span class="sxs-lookup"><span data-stu-id="54379-129">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="54379-130">Este valor de encabezado solo se devuelve si un servicio ha invalidado el límite predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="54379-130">This header value is only returned if a service has overridden hello default limit.</span></span> <span data-ttu-id="54379-131">El Administrador de recursos se agrega este valor en lugar de hello suscripción lecturas o escrituras.</span><span class="sxs-lookup"><span data-stu-id="54379-131">Resource Manager adds this value instead of hello subscription reads or writes.</span></span> |
| <span data-ttu-id="54379-132">x-ms-ratelimit-Remaining-Subscription-Resource-Entities-Read</span><span class="sxs-lookup"><span data-stu-id="54379-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="54379-133">Solicitudes de colección de tipos de recursos restantes del ámbito de la suscripción</span><span class="sxs-lookup"><span data-stu-id="54379-133">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="54379-134">Este valor de encabezado solo se devuelve si un servicio ha invalidado el límite predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="54379-134">This header value is only returned if a service has overridden hello default limit.</span></span> <span data-ttu-id="54379-135">Este valor proporciona número Hola de solicitudes de colección restantes (recursos de lista).</span><span class="sxs-lookup"><span data-stu-id="54379-135">This value provides hello number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="54379-136">x-ms-ratelimit-Remaining-tenant-Resource-Requests</span><span class="sxs-lookup"><span data-stu-id="54379-136">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="54379-137">Solicitudes de tipos de recurso restantes del ámbito del inquilino</span><span class="sxs-lookup"><span data-stu-id="54379-137">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="54379-138">Solo se agrega este encabezado para las solicitudes en el nivel del inquilino, y solo si un servicio ha invalidado el límite predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="54379-138">This header is only added for requests at tenant level, and only if a service has overridden hello default limit.</span></span> <span data-ttu-id="54379-139">El Administrador de recursos se agrega este valor en lugar de hello inquilino lecturas o escrituras.</span><span class="sxs-lookup"><span data-stu-id="54379-139">Resource Manager adds this value instead of hello tenant reads or writes.</span></span> |
| <span data-ttu-id="54379-140">x-ms-ratelimit-Remaining-tenant-Resource-Entities-Read</span><span class="sxs-lookup"><span data-stu-id="54379-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="54379-141">Solicitudes de colección de tipos de recursos restantes del ámbito del inquilino</span><span class="sxs-lookup"><span data-stu-id="54379-141">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="54379-142">Solo se agrega este encabezado para las solicitudes en el nivel del inquilino, y solo si un servicio ha invalidado el límite predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="54379-142">This header is only added for requests at tenant level, and only if a service has overridden hello default limit.</span></span> |

## <a name="retrieving-hello-header-values"></a><span data-ttu-id="54379-143">Recuperar valores de encabezado de Hola</span><span class="sxs-lookup"><span data-stu-id="54379-143">Retrieving hello header values</span></span>
<span data-ttu-id="54379-144">El proceso de recuperación de estos valores de encabezado del código o el script es igual que el de cualquier valor de encabezado.</span><span class="sxs-lookup"><span data-stu-id="54379-144">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="54379-145">Por ejemplo, en **C#**, recuperar el valor del encabezado Hola desde una **HttpWebResponse** objeto denominado **respuesta** con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="54379-145">For example, in **C#**, you retrieve hello header value from an **HttpWebResponse** object named **response** with hello following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="54379-146">En **PowerShell**, recuperar el valor del encabezado de Hola de una operación de Invoke-WebRequest.</span><span class="sxs-lookup"><span data-stu-id="54379-146">In **PowerShell**, you retrieve hello header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="54379-147">O bien, si desea toosee Hola restantes solicitudes para la depuración, puede proporcionar hello **-depurar** parámetro en su **PowerShell** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="54379-147">Or, if want toosee hello remaining requests for debugging, you can provide hello **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="54379-148">Que devuelve varios valores, incluidos Hola siguiente valor de respuesta:</span><span class="sxs-lookup"><span data-stu-id="54379-148">Which returns many values, including hello following response value:</span></span>

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

<span data-ttu-id="54379-149">En **Azure CLI**, recuperar el valor del encabezado de hello mediante Hola opción más detallado.</span><span class="sxs-lookup"><span data-stu-id="54379-149">In **Azure CLI**, you retrieve hello header value by using hello more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="54379-150">Que devuelve muchos valores, incluidos Hola después de objeto:</span><span class="sxs-lookup"><span data-stu-id="54379-150">Which returns many values, including hello following object:</span></span>

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

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="54379-151">Espera antes de enviar la solicitud siguiente</span><span class="sxs-lookup"><span data-stu-id="54379-151">Waiting before sending next request</span></span>
<span data-ttu-id="54379-152">Cuando alcance el límite de solicitudes de Hola, Administrador de recursos devuelve hello **429** código de estado HTTP y un **Retry-After** valor de encabezado de Hola.</span><span class="sxs-lookup"><span data-stu-id="54379-152">When you reach hello request limit, Resource Manager returns hello **429** HTTP status code and a **Retry-After** value in hello header.</span></span> <span data-ttu-id="54379-153">Hola **Retry-After** valor especifica el número de Hola de segundos que debe esperar la aplicación (o suspensión) antes de enviar la solicitud siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="54379-153">hello **Retry-After** value specifies hello number of seconds your application should wait (or sleep) before sending hello next request.</span></span> <span data-ttu-id="54379-154">Si se envía una solicitud antes de que haya transcurrido el valor de reintento de hello, no se procesa la solicitud y se devuelve un nuevo valor de reintento.</span><span class="sxs-lookup"><span data-stu-id="54379-154">If you send a request before hello retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54379-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="54379-155">Next steps</span></span>

* <span data-ttu-id="54379-156">Para más información acerca de límites y cuotas, consulte [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="54379-156">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="54379-157">toolearn sobre el control de solicitudes asincrónicas de REST, consulte [realizar un seguimiento de las operaciones asincrónicas de Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="54379-157">toolearn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
