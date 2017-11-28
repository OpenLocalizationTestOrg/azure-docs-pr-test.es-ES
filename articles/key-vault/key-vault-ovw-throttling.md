---
ms.assetid: 
title: "Guía de limitación de almacén de claves aaaAzure | Documentos de Microsoft"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: a75cf96bc6503e51f14378bee598bad57e85be82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="f9ced-102">Guía de las limitaciones de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="f9ced-102">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="f9ced-103">Limitación es un proceso inicia que limita el número de Hola de llamadas concurrentes toohello servicio de Azure tooprevent el uso excesivo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f9ced-103">Throttling is a process you initiate that limits hello number of concurrent calls toohello Azure service tooprevent overuse of resources.</span></span> <span data-ttu-id="f9ced-104">Almacén de claves de Azure (claves) es toohandle diseñado un gran volumen de solicitudes.</span><span class="sxs-lookup"><span data-stu-id="f9ced-104">Azure Key Vault (AKV) is designed toohandle a high volume of requests.</span></span> <span data-ttu-id="f9ced-105">Si se produce un número excesivo de solicitudes, la limitación de peticiones de su cliente le ayuda a mantener un rendimiento óptimo y la confiabilidad del programa Hola a servicio de claves.</span><span class="sxs-lookup"><span data-stu-id="f9ced-105">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of hello AKV service.</span></span>

<span data-ttu-id="f9ced-106">Límites de limitación varían según el escenario de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9ced-106">Throttling limits vary based on hello scenario.</span></span> <span data-ttu-id="f9ced-107">Por ejemplo, si está realizando un gran volumen de escrituras, posibilidad de hello para la limitación es mayor que si solo va a realizar lecturas.</span><span class="sxs-lookup"><span data-stu-id="f9ced-107">For example, if you are performing a large volume of writes, hello possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="f9ced-108">¿Cómo maneja Key Vaults sus límites?</span><span class="sxs-lookup"><span data-stu-id="f9ced-108">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="f9ced-109">Límites de servicio en el almacén de claves existen tooprevent el uso indebido de los recursos y garantizan la calidad de servicio para todos los clientes del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="f9ced-109">Service limits in Key Vault are there tooprevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="f9ced-110">Cuando se supera un umbral de servicio, Key Vault limita las solicitudes sucesivas de ese cliente durante un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="f9ced-110">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="f9ced-111">Cuando esto sucede, el almacén de claves devuelve código de estado HTTP 429 (demasiados muchas solicitudes), y Hola solicita producirá un error.</span><span class="sxs-lookup"><span data-stu-id="f9ced-111">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and hello requests fail.</span></span> <span data-ttu-id="f9ced-112">Además, no se pudo las solicitudes que devuelven un recuento 429 hacia límites Hola hace un seguimiento mediante el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="f9ced-112">Also, failed requests that return a 429 count towards hello throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="f9ced-113">Si tiene un caso empresarial válido para limitaciones superiores, póngase en contacto con nosotros.</span><span class="sxs-lookup"><span data-stu-id="f9ced-113">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-toothrottle-your-app-in-response-tooservice-limits"></a><span data-ttu-id="f9ced-114">¿Cómo toothrottle la aplicación en respuesta tooservice limita</span><span class="sxs-lookup"><span data-stu-id="f9ced-114">How toothrottle your app in response tooservice limits</span></span>

<span data-ttu-id="f9ced-115">Hello siguientes son **prácticas recomendadas** para la limitación de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="f9ced-115">hello following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="f9ced-116">Reducir el número de Hola de operaciones por solicitud.</span><span class="sxs-lookup"><span data-stu-id="f9ced-116">Reduce hello number of operations per request.</span></span>
- <span data-ttu-id="f9ced-117">Reduzca la frecuencia de Hola de solicitudes.</span><span class="sxs-lookup"><span data-stu-id="f9ced-117">Reduce hello frequency of requests.</span></span>
- <span data-ttu-id="f9ced-118">Evite los reintentos inmediatos.</span><span class="sxs-lookup"><span data-stu-id="f9ced-118">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="f9ced-119">Todas las solicitudes se acumulan en los límites de utilización.</span><span class="sxs-lookup"><span data-stu-id="f9ced-119">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="f9ced-120">Al implementar el control de errores de la aplicación, use Hola HTTP error código 429 toodetect Hola necesario para la limitación de cliente.</span><span class="sxs-lookup"><span data-stu-id="f9ced-120">When you implement your app's error handling, use hello HTTP error code 429 toodetect hello need for client-side throttling.</span></span> <span data-ttu-id="f9ced-121">Si la solicitud de hello vuelve a falla con un código de error HTTP 429, todavía se está produciendo un límite de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="f9ced-121">If hello request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="f9ced-122">Continuar toouse Hola recomienda método limitación del cliente, reintentar la solicitud de hello hasta que lo consiga.</span><span class="sxs-lookup"><span data-stu-id="f9ced-122">Continue toouse hello recommended client-side throttling method, retrying hello request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="f9ced-123">Método de limitación del cliente recomendado</span><span class="sxs-lookup"><span data-stu-id="f9ced-123">Recommended client-side throttling method</span></span>

<span data-ttu-id="f9ced-124">En el código de error HTTP 429, comience la limitación del cliente mediante un enfoque de retroceso exponencial:</span><span class="sxs-lookup"><span data-stu-id="f9ced-124">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="f9ced-125">Espere 1 segundo, reintente la solicitud</span><span class="sxs-lookup"><span data-stu-id="f9ced-125">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="f9ced-126">Si todavía está limitado, espere 2 segundos, reintente la solicitud</span><span class="sxs-lookup"><span data-stu-id="f9ced-126">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="f9ced-127">Si todavía está limitado, espere 4 segundos, reintente la solicitud</span><span class="sxs-lookup"><span data-stu-id="f9ced-127">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="f9ced-128">Si todavía está limitado, espere 8 segundos, reintente la solicitud</span><span class="sxs-lookup"><span data-stu-id="f9ced-128">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="f9ced-129">Si todavía está limitado, espere 16 segundos, reintente la solicitud</span><span class="sxs-lookup"><span data-stu-id="f9ced-129">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="f9ced-130">En este momento, se deben no está recibiendo los códigos de respuesta HTTP 429.</span><span class="sxs-lookup"><span data-stu-id="f9ced-130">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="f9ced-131">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="f9ced-131">See also</span></span>

<span data-ttu-id="f9ced-132">Para obtener una orientación más profunda de limitación en hello Microsoft Cloud, vea [limitación patrón](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span><span class="sxs-lookup"><span data-stu-id="f9ced-132">For a deeper orientation of throttling on hello Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

