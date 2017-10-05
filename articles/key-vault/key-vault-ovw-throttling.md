---
ms.assetid: 
title: "Guía de las limitaciones de Azure Key Vault | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: fe700e22c5323c2a0bdc315e349cd119798bcf40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="d274c-102">Guía de las limitaciones de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="d274c-102">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="d274c-103">La limitación es un proceso que se inicia y que limita el número de llamadas simultáneas al servicio de Azure para evitar el uso excesivo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d274c-103">Throttling is a process you initiate that limits the number of concurrent calls to the Azure service to prevent overuse of resources.</span></span> <span data-ttu-id="d274c-104">Azure Key Vault se ha diseñado para controlar un volumen muy alto de solicitudes.</span><span class="sxs-lookup"><span data-stu-id="d274c-104">Azure Key Vault (AKV) is designed to handle a high volume of requests.</span></span> <span data-ttu-id="d274c-105">Si tiene lugar un número excesivo de solicitudes, la limitación de las solicitudes del cliente le ayuda a mantener un rendimiento óptimo y la confiabilidad del servicio Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d274c-105">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of the AKV service.</span></span>

<span data-ttu-id="d274c-106">Las limitaciones varían según el escenario.</span><span class="sxs-lookup"><span data-stu-id="d274c-106">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="d274c-107">Por ejemplo, si está realizando un gran volumen de escrituras, la posibilidad de limitación es mayor que si solo realiza lecturas.</span><span class="sxs-lookup"><span data-stu-id="d274c-107">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="d274c-108">¿Cómo maneja Key Vaults sus límites?</span><span class="sxs-lookup"><span data-stu-id="d274c-108">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="d274c-109">Los límites de servicio en Key Vault sirven para evitar el uso incorrecto de los recursos y garantizar la calidad de servicio para todos los clientes de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d274c-109">Service limits in Key Vault are there to prevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="d274c-110">Cuando se supera un umbral de servicio, Key Vault limita las solicitudes sucesivas de ese cliente durante un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="d274c-110">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="d274c-111">Cuando esto sucede, Key Vault devuelve el código de estado HTTP 429 (demasiadas solicitudes) y se producirá un error en las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="d274c-111">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and the requests fail.</span></span> <span data-ttu-id="d274c-112">Además, las solicitudes con error que devuelven un código 429 cuentan para la limitación cuyo seguimiento realiza Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d274c-112">Also, failed requests that return a 429 count towards the throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="d274c-113">Si tiene un caso empresarial válido para limitaciones superiores, póngase en contacto con nosotros.</span><span class="sxs-lookup"><span data-stu-id="d274c-113">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-to-throttle-your-app-in-response-to-service-limits"></a><span data-ttu-id="d274c-114">Limitación de la aplicación en respuesta a los límites de servicio</span><span class="sxs-lookup"><span data-stu-id="d274c-114">How to throttle your app in response to service limits</span></span>

<span data-ttu-id="d274c-115">A continuación se muestran los **procedimientos recomendados** para la limitación de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="d274c-115">The following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="d274c-116">Reduzca el número de operaciones por solicitud.</span><span class="sxs-lookup"><span data-stu-id="d274c-116">Reduce the number of operations per request.</span></span>
- <span data-ttu-id="d274c-117">Reduzca la frecuencia de las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="d274c-117">Reduce the frequency of requests.</span></span>
- <span data-ttu-id="d274c-118">Evite los reintentos inmediatos.</span><span class="sxs-lookup"><span data-stu-id="d274c-118">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="d274c-119">Todas las solicitudes se acumulan en los límites de utilización.</span><span class="sxs-lookup"><span data-stu-id="d274c-119">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="d274c-120">Al implementar el control de errores de la aplicación, utilice el código de error HTTP 429 para detectar la necesidad de limitación del cliente.</span><span class="sxs-lookup"><span data-stu-id="d274c-120">When you implement your app's error handling, use the HTTP error code 429 to detect the need for client-side throttling.</span></span> <span data-ttu-id="d274c-121">Si la solicitud vuelve a enviar un código de error HTTP 429, todavía se está produciendo un límite de servicio Azure.</span><span class="sxs-lookup"><span data-stu-id="d274c-121">If the request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="d274c-122">Continúe usando el método de limitación del cliente recomendado y vuelva a intentar la solicitud hasta que lo consiga.</span><span class="sxs-lookup"><span data-stu-id="d274c-122">Continue to use the recommended client-side throttling method, retrying the request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="d274c-123">Método de limitación del cliente recomendado</span><span class="sxs-lookup"><span data-stu-id="d274c-123">Recommended client-side throttling method</span></span>

<span data-ttu-id="d274c-124">En el código de error HTTP 429, comience la limitación del cliente mediante un enfoque de retroceso exponencial:</span><span class="sxs-lookup"><span data-stu-id="d274c-124">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="d274c-125">Espere 1 segundo, reintente la solicitud</span><span class="sxs-lookup"><span data-stu-id="d274c-125">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="d274c-126">Si todavía está limitado, espere 2 segundos, reintente la solicitud</span><span class="sxs-lookup"><span data-stu-id="d274c-126">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="d274c-127">Si todavía está limitado, espere 4 segundos, reintente la solicitud</span><span class="sxs-lookup"><span data-stu-id="d274c-127">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="d274c-128">Si todavía está limitado, espere 8 segundos, reintente la solicitud</span><span class="sxs-lookup"><span data-stu-id="d274c-128">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="d274c-129">Si todavía está limitado, espere 16 segundos, reintente la solicitud</span><span class="sxs-lookup"><span data-stu-id="d274c-129">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="d274c-130">En este momento, se deben no está recibiendo los códigos de respuesta HTTP 429.</span><span class="sxs-lookup"><span data-stu-id="d274c-130">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="d274c-131">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="d274c-131">See also</span></span>

<span data-ttu-id="d274c-132">Para obtener una orientación más profunda de la limitación en Microsoft Cloud, consulte [Patrón de limitación](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span><span class="sxs-lookup"><span data-stu-id="d274c-132">For a deeper orientation of throttling on the Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

