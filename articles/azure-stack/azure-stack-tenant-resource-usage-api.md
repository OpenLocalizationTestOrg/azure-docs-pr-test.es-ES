---
title: API de uso de recursos aaaTenant | Documentos de Microsoft
description: "Referencia de la API de uso de recursos, que recupera información de uso de Azure Stack."
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: b9d7c7ee-e906-4978-92a3-a2c52df16c36
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2016
ms.author: alfredop
ms.openlocfilehash: eb826aba87b3b5b79155d9003162f2b5e6871f82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tenant-resource-usage-api"></a><span data-ttu-id="e2470-103">API de uso de recursos de inquilino</span><span class="sxs-lookup"><span data-stu-id="e2470-103">Tenant Resource Usage API</span></span>
<span data-ttu-id="e2470-104">Un inquilino puede utilizar datos de uso de recursos del inquilino de hello API de inquilinos tooview Hola.</span><span class="sxs-lookup"><span data-stu-id="e2470-104">A tenant can use hello Tenant API tooview hello tenant’s own resource usage data.</span></span> <span data-ttu-id="e2470-105">Esta API es coherente con hello API de uso de Azure (actualmente en private preview).</span><span class="sxs-lookup"><span data-stu-id="e2470-105">This API is consistent with hello Azure Usage API (currently in private preview).</span></span>

<span data-ttu-id="e2470-106">Puede usar el cmdlet de Windows PowerShell de hello **UsageAggregates Get** tooget los datos de uso, como en Azure.</span><span class="sxs-lookup"><span data-stu-id="e2470-106">You can use hello Windows PowerShell cmdlet **Get-UsageAggregates** tooget usage data like in Azure.</span></span>

## <a name="api-call"></a><span data-ttu-id="e2470-107">Llamada a la API</span><span class="sxs-lookup"><span data-stu-id="e2470-107">API call</span></span>
### <a name="request"></a><span data-ttu-id="e2470-108">Solicitud</span><span class="sxs-lookup"><span data-stu-id="e2470-108">Request</span></span>
<span data-ttu-id="e2470-109">Hola solicitud obtiene detalles del consumo de hello había solicitado suscripciones y Hola solicita el período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="e2470-109">hello request gets consumption details for hello requested subscriptions and for hello requested time frame.</span></span> <span data-ttu-id="e2470-110">No hay ningún cuerpo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="e2470-110">There is no request body.</span></span>

| <span data-ttu-id="e2470-111">**Método**</span><span class="sxs-lookup"><span data-stu-id="e2470-111">**Method**</span></span> | <span data-ttu-id="e2470-112">**URI de solicitud**</span><span class="sxs-lookup"><span data-stu-id="e2470-112">**Request URI**</span></span> |
| --- | --- |
| <span data-ttu-id="e2470-113">GET</span><span class="sxs-lookup"><span data-stu-id="e2470-113">GET</span></span> |<span data-ttu-id="e2470-114">https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/usageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&api-version=2015-06-01-preview&continuationToken={token-value}</span><span class="sxs-lookup"><span data-stu-id="e2470-114">https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/usageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&api-version=2015-06-01-preview&continuationToken={token-value}</span></span> |

### <a name="arguments"></a><span data-ttu-id="e2470-115">Argumentos</span><span class="sxs-lookup"><span data-stu-id="e2470-115">Arguments</span></span>
| <span data-ttu-id="e2470-116">**Argumento**</span><span class="sxs-lookup"><span data-stu-id="e2470-116">**Argument**</span></span> | <span data-ttu-id="e2470-117">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="e2470-117">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="e2470-118">*Armendpoint*</span><span class="sxs-lookup"><span data-stu-id="e2470-118">*Armendpoint*</span></span> |<span data-ttu-id="e2470-119">Punto de conexión de Azure Resource Manager del entorno de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="e2470-119">Azure Resource Manager endpoint of your Azure Stack environment.</span></span> <span data-ttu-id="e2470-120">Hola convención de pila de Azure es el nombre hello de Azure Resource Manager extremo está en formato de hello `https://management.{domain-name}`.</span><span class="sxs-lookup"><span data-stu-id="e2470-120">hello Azure Stack convention is that hello name of Azure Resource Manager endpoint is in hello format `https://management.{domain-name}`.</span></span> <span data-ttu-id="e2470-121">Por ejemplo, nombre de dominio es local.azurestack.external si hello, entonces es el punto de conexión de administrador de recursos de hello `https://management.local.azurestack.external`.</span><span class="sxs-lookup"><span data-stu-id="e2470-121">For example, if hello domain name is local.azurestack.external, then hello Resource Manager  endpoint is `https://management.local.azurestack.external`.</span></span> |
| <span data-ttu-id="e2470-122">*subId*</span><span class="sxs-lookup"><span data-stu-id="e2470-122">*subId*</span></span> |<span data-ttu-id="e2470-123">Identificador de suscripción del usuario de Hola que está realizando la llamada de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2470-123">Subscription ID of hello user who is making hello call.</span></span> <span data-ttu-id="e2470-124">Puede usar este tooquery única API para el uso de una sola suscripción.</span><span class="sxs-lookup"><span data-stu-id="e2470-124">You can use this API only tooquery for a single subscription’s usage.</span></span> <span data-ttu-id="e2470-125">Proveedores pueden usar el uso de la API de uso de recursos de proveedor tooquery Hola para todos los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="e2470-125">Providers can use hello Provider Resource Usage API tooquery usage for all tenants.</span></span> |
| <span data-ttu-id="e2470-126">*reportedStartTime*</span><span class="sxs-lookup"><span data-stu-id="e2470-126">*reportedStartTime*</span></span> |<span data-ttu-id="e2470-127">Hora de inicio de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2470-127">Start time of hello query.</span></span> <span data-ttu-id="e2470-128">Hola valor para *DateTime* debe estar en hora UTC y al principio de Hola de hora de hello, por ejemplo, 13:00.</span><span class="sxs-lookup"><span data-stu-id="e2470-128">hello value for *DateTime* should be in UTC and at hello beginning of hello hour, for example, 13:00.</span></span> <span data-ttu-id="e2470-129">Agregaciones diarias, establecer este medianoche tooUTC de valor.</span><span class="sxs-lookup"><span data-stu-id="e2470-129">For daily aggregation, set this value tooUTC midnight.</span></span> <span data-ttu-id="e2470-130">formato de Hello es *caracteres de escape* ISO 8601, por ejemplo, 2015-06-16T18% 3a53% 3a11% 2b00% 3a00Z, donde dos puntos se escapa demasiado % 3a y además se escapa demasiado % 2b para que esté URI descriptivo.</span><span class="sxs-lookup"><span data-stu-id="e2470-130">hello format is *escaped* ISO 8601, for example, 2015-06-16T18%3a53%3a11%2b00%3a00Z, where colon is escaped too%3a and plus is escaped too%2b so that it is URI friendly.</span></span> |
| <span data-ttu-id="e2470-131">*reportedEndTime*</span><span class="sxs-lookup"><span data-stu-id="e2470-131">*reportedEndTime*</span></span> |<span data-ttu-id="e2470-132">Hora de finalización de la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2470-132">End time of hello query.</span></span> <span data-ttu-id="e2470-133">Hola restricciones que se aplican demasiado*reportedStartTime* toothis argumento también se aplican.</span><span class="sxs-lookup"><span data-stu-id="e2470-133">hello constraints that apply too*reportedStartTime* also apply toothis argument.</span></span> <span data-ttu-id="e2470-134">Hola valor para *reportedEndTime* no puede estar en hello futuras.</span><span class="sxs-lookup"><span data-stu-id="e2470-134">hello value for *reportedEndTime* cannot be in hello future.</span></span> |
| <span data-ttu-id="e2470-135">*aggregationGranularity*</span><span class="sxs-lookup"><span data-stu-id="e2470-135">*aggregationGranularity*</span></span> |<span data-ttu-id="e2470-136">Parámetro opcional que tiene dos valores posibles discretos: días y horas.</span><span class="sxs-lookup"><span data-stu-id="e2470-136">Optional parameter that has two discrete potential values: daily and hourly.</span></span> <span data-ttu-id="e2470-137">Como sugieren los valores de hello, uno devuelve datos Hola granularidad diaria y Hola otro es una resolución por horas.</span><span class="sxs-lookup"><span data-stu-id="e2470-137">As hello values suggest, one returns hello data in daily granularity, and hello other is an hourly resolution.</span></span> <span data-ttu-id="e2470-138">opción diario de Hello es Hola predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e2470-138">hello daily option is hello default.</span></span> |
| <span data-ttu-id="e2470-139">*api-version*</span><span class="sxs-lookup"><span data-stu-id="e2470-139">*api-version*</span></span> |<span data-ttu-id="e2470-140">Versión del protocolo de hello es toomake usado esta solicitud.</span><span class="sxs-lookup"><span data-stu-id="e2470-140">Version of hello protocol that is used toomake this request.</span></span> <span data-ttu-id="e2470-141">Debe usar 2015-06-01-preview.</span><span class="sxs-lookup"><span data-stu-id="e2470-141">You must use 2015-06-01-preview.</span></span> |
| <span data-ttu-id="e2470-142">*continuationToken*</span><span class="sxs-lookup"><span data-stu-id="e2470-142">*continuationToken*</span></span> |<span data-ttu-id="e2470-143">Símbolo (token) recupera Hola última llamada toohello API de uso proveedor.</span><span class="sxs-lookup"><span data-stu-id="e2470-143">Token retrieved from hello last call toohello Usage API provider.</span></span> <span data-ttu-id="e2470-144">Este token es necesario cuando una respuesta es superior a 1.000 líneas y actúa como un marcador para el progreso.</span><span class="sxs-lookup"><span data-stu-id="e2470-144">This token is needed when a response is greater than 1,000 lines and it acts as a bookmark for progress.</span></span> <span data-ttu-id="e2470-145">Si no lo está, Hola principio de hello del día de Hola o de hora, en función de la granularidad de hello pasa se recuperan los datos.</span><span class="sxs-lookup"><span data-stu-id="e2470-145">If not present, hello data is retrieved from hello beginning of hello day or hour, based on hello granularity passed in.</span></span> |

### <a name="response"></a><span data-ttu-id="e2470-146">Response</span><span class="sxs-lookup"><span data-stu-id="e2470-146">Response</span></span>
<span data-ttu-id="e2470-147">GET /subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&api-version=1.0</span><span class="sxs-lookup"><span data-stu-id="e2470-147">GET /subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&api-version=1.0</span></span>

<span data-ttu-id="e2470-148">{</span><span class="sxs-lookup"><span data-stu-id="e2470-148">{</span></span>

<span data-ttu-id="e2470-149">"value": \[</span><span class="sxs-lookup"><span data-stu-id="e2470-149">"value": \[</span></span>

<span data-ttu-id="e2470-150">{</span><span class="sxs-lookup"><span data-stu-id="e2470-150">{</span></span>

<span data-ttu-id="e2470-151">"id": "/subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregate/sub1-meterID1",</span><span class="sxs-lookup"><span data-stu-id="e2470-151">"id": "/subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregate/sub1-meterID1",</span></span>

<span data-ttu-id="e2470-152">"name": "sub1-meterID1",</span><span class="sxs-lookup"><span data-stu-id="e2470-152">"name": "sub1-meterID1",</span></span>

<span data-ttu-id="e2470-153">"type": "Microsoft.Commerce/UsageAggregate",</span><span class="sxs-lookup"><span data-stu-id="e2470-153">"type": "Microsoft.Commerce/UsageAggregate",</span></span>

<span data-ttu-id="e2470-154">"properties": {</span><span class="sxs-lookup"><span data-stu-id="e2470-154">"properties": {</span></span>

<span data-ttu-id="e2470-155">"subscriptionId":"sub1",</span><span class="sxs-lookup"><span data-stu-id="e2470-155">"subscriptionId":"sub1",</span></span>

<span data-ttu-id="e2470-156">"usageStartTime": "2015-03-03T00:00:00+00:00",</span><span class="sxs-lookup"><span data-stu-id="e2470-156">"usageStartTime": "2015-03-03T00:00:00+00:00",</span></span>

<span data-ttu-id="e2470-157">"usageEndTime": "2015-03-04T00:00:00+00:00",</span><span class="sxs-lookup"><span data-stu-id="e2470-157">"usageEndTime": "2015-03-04T00:00:00+00:00",</span></span>

<span data-ttu-id="e2470-158">"instanceData":"{\\"Microsoft.Resources\\":{\\"resourceUri\\":\\"resourceUri1\\",\\"location\\":\\"Alaska\\",\\"tags\\":null,\\"additionalInfo\\":null}}",</span><span class="sxs-lookup"><span data-stu-id="e2470-158">"instanceData":"{\\"Microsoft.Resources\\":{\\"resourceUri\\":\\"resourceUri1\\",\\"location\\":\\"Alaska\\",\\"tags\\":null,\\"additionalInfo\\":null}}",</span></span>

<span data-ttu-id="e2470-159">"quantity":2.4000000000,</span><span class="sxs-lookup"><span data-stu-id="e2470-159">"quantity":2.4000000000,</span></span>

<span data-ttu-id="e2470-160">"meterId":"meterID1"</span><span class="sxs-lookup"><span data-stu-id="e2470-160">"meterId":"meterID1"</span></span>

<span data-ttu-id="e2470-161">}</span><span class="sxs-lookup"><span data-stu-id="e2470-161">}</span></span>

<span data-ttu-id="e2470-162">},</span><span class="sxs-lookup"><span data-stu-id="e2470-162">},</span></span>

<span data-ttu-id="e2470-163">…</span><span class="sxs-lookup"><span data-stu-id="e2470-163">…</span></span>

### <a name="response-details"></a><span data-ttu-id="e2470-164">Detalles de la respuesta</span><span class="sxs-lookup"><span data-stu-id="e2470-164">Response details</span></span>
| <span data-ttu-id="e2470-165">**Argumento**</span><span class="sxs-lookup"><span data-stu-id="e2470-165">**Argument**</span></span> | <span data-ttu-id="e2470-166">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="e2470-166">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="e2470-167">*id*</span><span class="sxs-lookup"><span data-stu-id="e2470-167">*id*</span></span> |<span data-ttu-id="e2470-168">Identificador único del uso de hello agregado</span><span class="sxs-lookup"><span data-stu-id="e2470-168">Unique ID of hello usage aggregate</span></span> |
| <span data-ttu-id="e2470-169">*name*</span><span class="sxs-lookup"><span data-stu-id="e2470-169">*name*</span></span> |<span data-ttu-id="e2470-170">Nombre de agregado de uso de Hola</span><span class="sxs-lookup"><span data-stu-id="e2470-170">Name of hello usage aggregate</span></span> |
| <span data-ttu-id="e2470-171">*type*</span><span class="sxs-lookup"><span data-stu-id="e2470-171">*type*</span></span> |<span data-ttu-id="e2470-172">Definición de recursos</span><span class="sxs-lookup"><span data-stu-id="e2470-172">Resource definition</span></span> |
| <span data-ttu-id="e2470-173">*subscriptionId*</span><span class="sxs-lookup"><span data-stu-id="e2470-173">*subscriptionId*</span></span> |<span data-ttu-id="e2470-174">Identificador de la suscripción del programa Hola a usuario de Azure</span><span class="sxs-lookup"><span data-stu-id="e2470-174">Subscription identifier of hello Azure user</span></span> |
| <span data-ttu-id="e2470-175">*usageStartTime*</span><span class="sxs-lookup"><span data-stu-id="e2470-175">*usageStartTime*</span></span> |<span data-ttu-id="e2470-176">UTC hora de inicio de hello uso depósito toowhich pertenece este agregado de uso</span><span class="sxs-lookup"><span data-stu-id="e2470-176">UTC start time of hello usage bucket toowhich this usage aggregate belongs</span></span> |
| <span data-ttu-id="e2470-177">*usageEndTime*</span><span class="sxs-lookup"><span data-stu-id="e2470-177">*usageEndTime*</span></span> |<span data-ttu-id="e2470-178">Hora de hello uso depósito toowhich pertenece este agregado de uso de finalización UTC</span><span class="sxs-lookup"><span data-stu-id="e2470-178">UTC end time of hello usage bucket toowhich this usage aggregate belongs</span></span> |
| <span data-ttu-id="e2470-179">*instanceData*</span><span class="sxs-lookup"><span data-stu-id="e2470-179">*instanceData*</span></span> |<span data-ttu-id="e2470-180">Pares de clave y valor de los detalles de la instancia (con un formato nuevo):</span><span class="sxs-lookup"><span data-stu-id="e2470-180">Key-value pairs of instance details (in a new format):</span></span><br>  <span data-ttu-id="e2470-181">*resourceUri*: identificador de recurso completo, incluidos los grupos de recursos y el nombre de instancia</span><span class="sxs-lookup"><span data-stu-id="e2470-181">*resourceUri*: Fully qualified resource ID, including resource groups and instance name</span></span> <br>  <span data-ttu-id="e2470-182">*location*: región en la que se ejecutó este servicio</span><span class="sxs-lookup"><span data-stu-id="e2470-182">*location*: Region in which this service was run</span></span> <br>  <span data-ttu-id="e2470-183">*etiquetas*: especifica ese usuario Hola de las etiquetas del recurso</span><span class="sxs-lookup"><span data-stu-id="e2470-183">*tags*: Resource tags that hello user specifies</span></span> <br>  <span data-ttu-id="e2470-184">*additionalInfo*: más detalles sobre los recursos de hello consumido, por ejemplo, tipo de imagen o la versión de sistema operativo</span><span class="sxs-lookup"><span data-stu-id="e2470-184">*additionalInfo*: More details about hello resource that was consumed, for example, OS version or image type</span></span> |
| <span data-ttu-id="e2470-185">*quantity*</span><span class="sxs-lookup"><span data-stu-id="e2470-185">*quantity*</span></span> |<span data-ttu-id="e2470-186">Cantidad de consumo de recursos que se produjo en este período de tiempo</span><span class="sxs-lookup"><span data-stu-id="e2470-186">Amount of resource consumption that occurred in this time frame</span></span> |
| <span data-ttu-id="e2470-187">*meterId*</span><span class="sxs-lookup"><span data-stu-id="e2470-187">*meterId*</span></span> |<span data-ttu-id="e2470-188">Identificador único para el recurso de Hola que se consumió (también denominada *ResourceID*)</span><span class="sxs-lookup"><span data-stu-id="e2470-188">Unique ID for hello resource that was consumed (also called *ResourceID*)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e2470-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e2470-189">Next steps</span></span>
[<span data-ttu-id="e2470-190">API de uso de recursos de proveedor</span><span class="sxs-lookup"><span data-stu-id="e2470-190">Provider resource usage API</span></span>](azure-stack-provider-resource-api.md)

[<span data-ttu-id="e2470-191">Preguntas más frecuentes relacionadas con la utilización</span><span class="sxs-lookup"><span data-stu-id="e2470-191">Usage-related FAQ</span></span>](azure-stack-usage-related-faq.md)

