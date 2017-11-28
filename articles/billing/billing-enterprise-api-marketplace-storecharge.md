---
title: "API de facturación de Azure Enterprise: Gastos en Marketplace | Microsoft Docs"
description: "Obtenga información acerca de las API de informes que permiten a los clientes de Azure Enterprise extraer datos de consumo mediante programación."
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: 5539623f7ae35e14b6dafe6fdf9efe4bcaba4fd3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a><span data-ttu-id="b2176-103">API de informes para clientes de Enterprise: gastos de la tienda Marketplace</span><span class="sxs-lookup"><span data-stu-id="b2176-103">Reporting APIs for Enterprise customers - Marketplace Store Charge</span></span>

<span data-ttu-id="b2176-104">La API de gastos de la tienda Marketplace devuelve el desglose de los gastos de Marketplace basado en el uso por día para el período de facturación o las fechas de inicio y finalización especificadas (no se incluyen las cuotas de una vez).</span><span class="sxs-lookup"><span data-stu-id="b2176-104">The Marketplace Store Charge API returns the usage-based marketplace charges breakdown by day for the specified Billing Period or start and end dates (one time fees are not included).</span></span>

##<a name="request"></a><span data-ttu-id="b2176-105">Solicitud</span><span class="sxs-lookup"><span data-stu-id="b2176-105">Request</span></span> 
<span data-ttu-id="b2176-106">Las propiedades de encabezado comunes que tienen que agregarse se especifican [aquí](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="b2176-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="b2176-107">Si no se especifica un período de facturación, se devuelven datos para el período de facturación actual.</span><span class="sxs-lookup"><span data-stu-id="b2176-107">If a billing period is not specified, then data for the current billing period is returned.</span></span> <span data-ttu-id="b2176-108">Los intervalos de tiempo personalizados pueden especificarse con los parámetros de fecha de inicio y finalización que están en formato aaaa-MM-dd. El intervalo de tiempo máximo compatible es de 36 meses.</span><span class="sxs-lookup"><span data-stu-id="b2176-108">Custom time ranges can be specified with the start and end date parameters that are in the format yyyy-MM-dd, the maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="b2176-109">Método</span><span class="sxs-lookup"><span data-stu-id="b2176-109">Method</span></span> | <span data-ttu-id="b2176-110">URI de solicitud</span><span class="sxs-lookup"><span data-stu-id="b2176-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="b2176-111">GET</span><span class="sxs-lookup"><span data-stu-id="b2176-111">GET</span></span>|<span data-ttu-id="b2176-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="b2176-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span></span>|
|<span data-ttu-id="b2176-113">GET</span><span class="sxs-lookup"><span data-stu-id="b2176-113">GET</span></span>|<span data-ttu-id="b2176-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="b2176-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span></span>|
|<span data-ttu-id="b2176-115">GET</span><span class="sxs-lookup"><span data-stu-id="b2176-115">GET</span></span>|<span data-ttu-id="b2176-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span><span class="sxs-lookup"><span data-stu-id="b2176-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="b2176-117">Para usar la versión preliminar de la API, reemplace v2 por v1 en la dirección URL anterior.</span><span class="sxs-lookup"><span data-stu-id="b2176-117">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="b2176-118">Respuesta</span><span class="sxs-lookup"><span data-stu-id="b2176-118">Response</span></span>
 
    
        [
            {
                "id": "id",
                "subscriptionGuid": "00000000-0000-0000-0000-000000000000",
                "subscriptionName": "subName",
                "meterId": "2core",
                "usageStartDate": "2015-09-17T00:00:00Z",
                "usageEndDate": "2015-09-17T23:59:59Z",
                "offerName": "Virtual LoadMaster™ (VLM) for Azure",
                "resourceGroup": "Res group",
                "instanceId": "id",
                "additionalInfo": "{\"ImageType\":null,\"ServiceType\":\"Medium\"}",
                "tags": "",
                "orderNumber": "order",
                "unitOfMeasure": "",
                "costCenter": "100",
                "accountId": 100,
                "accountName": "Account Name",
                "accountOwnerId": "account@live.com",
                "departmentId": 101,
                "departmentName": "Department 1",
                "publisherName": "Publisher 1",
                "planName": "Plan name",
                "consumedQuantity": 1.15,
                "resourceRate": 0.1,
                "extendedCost": 1.11
            },
            ...
        ]
    

<span data-ttu-id="b2176-119">**Definiciones de propiedad de respuesta**</span><span class="sxs-lookup"><span data-stu-id="b2176-119">**Response property definitions**</span></span>

|<span data-ttu-id="b2176-120">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="b2176-120">Property Name</span></span>| <span data-ttu-id="b2176-121">Tipo</span><span class="sxs-lookup"><span data-stu-id="b2176-121">Type</span></span>| <span data-ttu-id="b2176-122">Descripción</span><span class="sxs-lookup"><span data-stu-id="b2176-122">Description</span></span>
|-|-|-|
|<span data-ttu-id="b2176-123">id</span><span class="sxs-lookup"><span data-stu-id="b2176-123">id</span></span>|<span data-ttu-id="b2176-124">cadena</span><span class="sxs-lookup"><span data-stu-id="b2176-124">string</span></span>|<span data-ttu-id="b2176-125">Identificador único para el elemento de gastos en Marketplace</span><span class="sxs-lookup"><span data-stu-id="b2176-125">Unique Id for the marketplace charge item</span></span>|
|<span data-ttu-id="b2176-126">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="b2176-126">subscriptionGuid</span></span>|<span data-ttu-id="b2176-127">Guid</span><span class="sxs-lookup"><span data-stu-id="b2176-127">Guid</span></span>|<span data-ttu-id="b2176-128">GUID de suscripción</span><span class="sxs-lookup"><span data-stu-id="b2176-128">The Subscription Guid</span></span>|
|<span data-ttu-id="b2176-129">subscriptionName</span><span class="sxs-lookup"><span data-stu-id="b2176-129">subscriptionName</span></span>|<span data-ttu-id="b2176-130">cadena</span><span class="sxs-lookup"><span data-stu-id="b2176-130">string</span></span>|<span data-ttu-id="b2176-131">Nombre de suscripción</span><span class="sxs-lookup"><span data-stu-id="b2176-131">The Subscription Name</span></span>|
|<span data-ttu-id="b2176-132">meterId</span><span class="sxs-lookup"><span data-stu-id="b2176-132">meterId</span></span>|<span data-ttu-id="b2176-133">cadena</span><span class="sxs-lookup"><span data-stu-id="b2176-133">string</span></span>|<span data-ttu-id="b2176-134">Identificador del medidor emitido</span><span class="sxs-lookup"><span data-stu-id="b2176-134">Id for the emitted Meter</span></span>|
|<span data-ttu-id="b2176-135">usageStartDate</span><span class="sxs-lookup"><span data-stu-id="b2176-135">usageStartDate</span></span>|<span data-ttu-id="b2176-136">DateTime</span><span class="sxs-lookup"><span data-stu-id="b2176-136">DateTime</span></span>|<span data-ttu-id="b2176-137">Hora de inicio del registro de uso</span><span class="sxs-lookup"><span data-stu-id="b2176-137">Start time for the usage record</span></span>|
|<span data-ttu-id="b2176-138">usageEndDate</span><span class="sxs-lookup"><span data-stu-id="b2176-138">usageEndDate</span></span>|<span data-ttu-id="b2176-139">DateTime</span><span class="sxs-lookup"><span data-stu-id="b2176-139">DateTime</span></span>|<span data-ttu-id="b2176-140">Hora de finalización del registro de uso</span><span class="sxs-lookup"><span data-stu-id="b2176-140">End time for the usage record</span></span>|
|<span data-ttu-id="b2176-141">offerName</span><span class="sxs-lookup"><span data-stu-id="b2176-141">offerName</span></span>|<span data-ttu-id="b2176-142">cadena</span><span class="sxs-lookup"><span data-stu-id="b2176-142">string</span></span>|<span data-ttu-id="b2176-143">Nombre de la oferta</span><span class="sxs-lookup"><span data-stu-id="b2176-143">The Offer name</span></span>|
|<span data-ttu-id="b2176-144">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="b2176-144">resourceGroup</span></span>|<span data-ttu-id="b2176-145">string</span><span class="sxs-lookup"><span data-stu-id="b2176-145">string</span></span>|<span data-ttu-id="b2176-146">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b2176-146">The resource Group</span></span>|
|<span data-ttu-id="b2176-147">instanceId</span><span class="sxs-lookup"><span data-stu-id="b2176-147">instanceId</span></span>|<span data-ttu-id="b2176-148">cadena</span><span class="sxs-lookup"><span data-stu-id="b2176-148">string</span></span>|<span data-ttu-id="b2176-149">Identificador de instancia</span><span class="sxs-lookup"><span data-stu-id="b2176-149">Instance Id</span></span>|
|<span data-ttu-id="b2176-150">additionalInfo</span><span class="sxs-lookup"><span data-stu-id="b2176-150">additionalInfo</span></span>|<span data-ttu-id="b2176-151">string</span><span class="sxs-lookup"><span data-stu-id="b2176-151">string</span></span>|<span data-ttu-id="b2176-152">Cadena JSON de información adicional</span><span class="sxs-lookup"><span data-stu-id="b2176-152">Additional info JSON string</span></span>|
|<span data-ttu-id="b2176-153">etiquetas</span><span class="sxs-lookup"><span data-stu-id="b2176-153">tags</span></span>|<span data-ttu-id="b2176-154">cadena</span><span class="sxs-lookup"><span data-stu-id="b2176-154">string</span></span>|<span data-ttu-id="b2176-155">Cadena JSON de etiqueta</span><span class="sxs-lookup"><span data-stu-id="b2176-155">Tag JSON string</span></span>|
|<span data-ttu-id="b2176-156">orderNumber</span><span class="sxs-lookup"><span data-stu-id="b2176-156">orderNumber</span></span>|<span data-ttu-id="b2176-157">string</span><span class="sxs-lookup"><span data-stu-id="b2176-157">string</span></span>|<span data-ttu-id="b2176-158">Número de pedido</span><span class="sxs-lookup"><span data-stu-id="b2176-158">The order number</span></span>|
|<span data-ttu-id="b2176-159">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="b2176-159">unitOfMeasure</span></span>|<span data-ttu-id="b2176-160">cadena</span><span class="sxs-lookup"><span data-stu-id="b2176-160">string</span></span>|<span data-ttu-id="b2176-161">Unidad de medida del medidor</span><span class="sxs-lookup"><span data-stu-id="b2176-161">Unit of measure for the meter</span></span>|
|<span data-ttu-id="b2176-162">costCenter</span><span class="sxs-lookup"><span data-stu-id="b2176-162">costCenter</span></span>|<span data-ttu-id="b2176-163">string</span><span class="sxs-lookup"><span data-stu-id="b2176-163">string</span></span>|<span data-ttu-id="b2176-164">Centro de coste</span><span class="sxs-lookup"><span data-stu-id="b2176-164">The cost center</span></span>|
|<span data-ttu-id="b2176-165">accountId</span><span class="sxs-lookup"><span data-stu-id="b2176-165">accountId</span></span>|<span data-ttu-id="b2176-166">int</span><span class="sxs-lookup"><span data-stu-id="b2176-166">int</span></span>|<span data-ttu-id="b2176-167">Identificador de cuenta</span><span class="sxs-lookup"><span data-stu-id="b2176-167">The account Id</span></span>|
|<span data-ttu-id="b2176-168">accountName</span><span class="sxs-lookup"><span data-stu-id="b2176-168">accountName</span></span>|<span data-ttu-id="b2176-169">cadena</span><span class="sxs-lookup"><span data-stu-id="b2176-169">string</span></span> |<span data-ttu-id="b2176-170">Nombre de cuenta</span><span class="sxs-lookup"><span data-stu-id="b2176-170">The Account Name</span></span>|
|<span data-ttu-id="b2176-171">accountOwnerId</span><span class="sxs-lookup"><span data-stu-id="b2176-171">accountOwnerId</span></span>|<span data-ttu-id="b2176-172">cadena</span><span class="sxs-lookup"><span data-stu-id="b2176-172">string</span></span>|<span data-ttu-id="b2176-173">Identificador de propietario de cuenta</span><span class="sxs-lookup"><span data-stu-id="b2176-173">The Account Owner Id</span></span>|
|<span data-ttu-id="b2176-174">departmentId</span><span class="sxs-lookup"><span data-stu-id="b2176-174">departmentId</span></span>|<span data-ttu-id="b2176-175">int</span><span class="sxs-lookup"><span data-stu-id="b2176-175">int</span></span>|<span data-ttu-id="b2176-176">Identificador de departamento</span><span class="sxs-lookup"><span data-stu-id="b2176-176">The department Id</span></span>|
|<span data-ttu-id="b2176-177">departmentName</span><span class="sxs-lookup"><span data-stu-id="b2176-177">departmentName</span></span>|<span data-ttu-id="b2176-178">cadena</span><span class="sxs-lookup"><span data-stu-id="b2176-178">string</span></span>|<span data-ttu-id="b2176-179">Nombre de departamento</span><span class="sxs-lookup"><span data-stu-id="b2176-179">The department name</span></span>|
|<span data-ttu-id="b2176-180">publisherName</span><span class="sxs-lookup"><span data-stu-id="b2176-180">publisherName</span></span>|<span data-ttu-id="b2176-181">cadena</span><span class="sxs-lookup"><span data-stu-id="b2176-181">string</span></span>|<span data-ttu-id="b2176-182">Nombre de publicador</span><span class="sxs-lookup"><span data-stu-id="b2176-182">The publisher name</span></span>|
|<span data-ttu-id="b2176-183">planName</span><span class="sxs-lookup"><span data-stu-id="b2176-183">planName</span></span>|<span data-ttu-id="b2176-184">cadena</span><span class="sxs-lookup"><span data-stu-id="b2176-184">string</span></span>|<span data-ttu-id="b2176-185">Nombre de plan</span><span class="sxs-lookup"><span data-stu-id="b2176-185">The Plan name</span></span>|
|<span data-ttu-id="b2176-186">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="b2176-186">consumedQuantity</span></span>|<span data-ttu-id="b2176-187">Decimal</span><span class="sxs-lookup"><span data-stu-id="b2176-187">decimal</span></span>|<span data-ttu-id="b2176-188">Cantidad consumida durante este período</span><span class="sxs-lookup"><span data-stu-id="b2176-188">Consumed Quantity during this time period</span></span>|
|<span data-ttu-id="b2176-189">resourceRate</span><span class="sxs-lookup"><span data-stu-id="b2176-189">resourceRate</span></span>|<span data-ttu-id="b2176-190">Decimal</span><span class="sxs-lookup"><span data-stu-id="b2176-190">decimal</span></span>|<span data-ttu-id="b2176-191">Precio por unidad del medidor</span><span class="sxs-lookup"><span data-stu-id="b2176-191">Unit price for the meter</span></span>|
|<span data-ttu-id="b2176-192">extendedCost</span><span class="sxs-lookup"><span data-stu-id="b2176-192">extendedCost</span></span>|<span data-ttu-id="b2176-193">Decimal</span><span class="sxs-lookup"><span data-stu-id="b2176-193">decimal</span></span>|<span data-ttu-id="b2176-194">Gasto estimado según la cantidad consumida y el costo total</span><span class="sxs-lookup"><span data-stu-id="b2176-194">Estimated charge based on Consumed Quantity and Extended cost</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="b2176-195">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="b2176-195">See also</span></span>

* [<span data-ttu-id="b2176-196">API de períodos de facturación</span><span class="sxs-lookup"><span data-stu-id="b2176-196">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="b2176-197">API de detalles de uso</span><span class="sxs-lookup"><span data-stu-id="b2176-197">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="b2176-198">API de saldo y resumen</span><span class="sxs-lookup"><span data-stu-id="b2176-198">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="b2176-199">API de hoja de precios</span><span class="sxs-lookup"><span data-stu-id="b2176-199">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)