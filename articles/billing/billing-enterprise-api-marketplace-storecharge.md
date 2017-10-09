---
title: "aaaAzure las API de empresa de facturación: cargos de Marketplace | Documentos de Microsoft"
description: "Obtenga información acerca de hello las API de generación de informes que permiten a los datos de consumo de Azure Enterprise los clientes toopull mediante programación."
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
ms.openlocfilehash: cdf2836b52df06a4bf5ed71a476fe33662c5363c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a><span data-ttu-id="63d51-103">API de informes para clientes de Enterprise: gastos de la tienda Marketplace</span><span class="sxs-lookup"><span data-stu-id="63d51-103">Reporting APIs for Enterprise customers - Marketplace Store Charge</span></span>

<span data-ttu-id="63d51-104">Hola Marketplace almacén cargo API devuelve Hola marketplace basada en uso cargos desglose por día de hello especifica período de facturación o fechas de inicio y finalización (no se incluyen las cuotas de una vez).</span><span class="sxs-lookup"><span data-stu-id="63d51-104">hello Marketplace Store Charge API returns hello usage-based marketplace charges breakdown by day for hello specified Billing Period or start and end dates (one time fees are not included).</span></span>

##<a name="request"></a><span data-ttu-id="63d51-105">Solicitud</span><span class="sxs-lookup"><span data-stu-id="63d51-105">Request</span></span> 
<span data-ttu-id="63d51-106">Se especifican las propiedades de encabezado comunes que necesitan toobe agrega [aquí](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="63d51-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="63d51-107">Si no se especifica un período de facturación, a continuación, datos de facturación actual de Hola período se devuelven.</span><span class="sxs-lookup"><span data-stu-id="63d51-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span> <span data-ttu-id="63d51-108">Intervalos de tiempo personalizado se pueden especificar con inicio de Hola y finalización los parámetros de fecha que se encuentran en tiempo de hello máximo admitida Hola formato aaaa-MM-dd, duración es de 36 meses.</span><span class="sxs-lookup"><span data-stu-id="63d51-108">Custom time ranges can be specified with hello start and end date parameters that are in hello format yyyy-MM-dd, hello maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="63d51-109">Método</span><span class="sxs-lookup"><span data-stu-id="63d51-109">Method</span></span> | <span data-ttu-id="63d51-110">URI de solicitud</span><span class="sxs-lookup"><span data-stu-id="63d51-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="63d51-111">GET</span><span class="sxs-lookup"><span data-stu-id="63d51-111">GET</span></span>|<span data-ttu-id="63d51-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="63d51-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span></span>|
|<span data-ttu-id="63d51-113">GET</span><span class="sxs-lookup"><span data-stu-id="63d51-113">GET</span></span>|<span data-ttu-id="63d51-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="63d51-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span></span>|
|<span data-ttu-id="63d51-115">GET</span><span class="sxs-lookup"><span data-stu-id="63d51-115">GET</span></span>|<span data-ttu-id="63d51-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span><span class="sxs-lookup"><span data-stu-id="63d51-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="63d51-117">versión de vista previa de hello toouse de API, reemplace v2 con v1 en hello por encima de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="63d51-117">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="63d51-118">Response</span><span class="sxs-lookup"><span data-stu-id="63d51-118">Response</span></span>
 
    
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
    

<span data-ttu-id="63d51-119">**Definiciones de propiedad de respuesta**</span><span class="sxs-lookup"><span data-stu-id="63d51-119">**Response property definitions**</span></span>

|<span data-ttu-id="63d51-120">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="63d51-120">Property Name</span></span>| <span data-ttu-id="63d51-121">Tipo</span><span class="sxs-lookup"><span data-stu-id="63d51-121">Type</span></span>| <span data-ttu-id="63d51-122">Descripción</span><span class="sxs-lookup"><span data-stu-id="63d51-122">Description</span></span>
|-|-|-|
|<span data-ttu-id="63d51-123">id</span><span class="sxs-lookup"><span data-stu-id="63d51-123">id</span></span>|<span data-ttu-id="63d51-124">cadena</span><span class="sxs-lookup"><span data-stu-id="63d51-124">string</span></span>|<span data-ttu-id="63d51-125">Identificador único para el artículo de costo de hello marketplace</span><span class="sxs-lookup"><span data-stu-id="63d51-125">Unique Id for hello marketplace charge item</span></span>|
|<span data-ttu-id="63d51-126">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="63d51-126">subscriptionGuid</span></span>|<span data-ttu-id="63d51-127">Guid</span><span class="sxs-lookup"><span data-stu-id="63d51-127">Guid</span></span>|<span data-ttu-id="63d51-128">Hola Guid de la suscripción</span><span class="sxs-lookup"><span data-stu-id="63d51-128">hello Subscription Guid</span></span>|
|<span data-ttu-id="63d51-129">subscriptionName</span><span class="sxs-lookup"><span data-stu-id="63d51-129">subscriptionName</span></span>|<span data-ttu-id="63d51-130">cadena</span><span class="sxs-lookup"><span data-stu-id="63d51-130">string</span></span>|<span data-ttu-id="63d51-131">Hola, nombre de la suscripción</span><span class="sxs-lookup"><span data-stu-id="63d51-131">hello Subscription Name</span></span>|
|<span data-ttu-id="63d51-132">meterId</span><span class="sxs-lookup"><span data-stu-id="63d51-132">meterId</span></span>|<span data-ttu-id="63d51-133">cadena</span><span class="sxs-lookup"><span data-stu-id="63d51-133">string</span></span>|<span data-ttu-id="63d51-134">Id. de hello genera medidor</span><span class="sxs-lookup"><span data-stu-id="63d51-134">Id for hello emitted Meter</span></span>|
|<span data-ttu-id="63d51-135">usageStartDate</span><span class="sxs-lookup"><span data-stu-id="63d51-135">usageStartDate</span></span>|<span data-ttu-id="63d51-136">DateTime</span><span class="sxs-lookup"><span data-stu-id="63d51-136">DateTime</span></span>|<span data-ttu-id="63d51-137">Hora de inicio de registro de uso de Hola</span><span class="sxs-lookup"><span data-stu-id="63d51-137">Start time for hello usage record</span></span>|
|<span data-ttu-id="63d51-138">usageEndDate</span><span class="sxs-lookup"><span data-stu-id="63d51-138">usageEndDate</span></span>|<span data-ttu-id="63d51-139">DateTime</span><span class="sxs-lookup"><span data-stu-id="63d51-139">DateTime</span></span>|<span data-ttu-id="63d51-140">Hora de finalización de registro de uso de Hola</span><span class="sxs-lookup"><span data-stu-id="63d51-140">End time for hello usage record</span></span>|
|<span data-ttu-id="63d51-141">offerName</span><span class="sxs-lookup"><span data-stu-id="63d51-141">offerName</span></span>|<span data-ttu-id="63d51-142">cadena</span><span class="sxs-lookup"><span data-stu-id="63d51-142">string</span></span>|<span data-ttu-id="63d51-143">nombre de la oferta de Hola</span><span class="sxs-lookup"><span data-stu-id="63d51-143">hello Offer name</span></span>|
|<span data-ttu-id="63d51-144">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="63d51-144">resourceGroup</span></span>|<span data-ttu-id="63d51-145">cadena</span><span class="sxs-lookup"><span data-stu-id="63d51-145">string</span></span>|<span data-ttu-id="63d51-146">recursos de Hello grupo</span><span class="sxs-lookup"><span data-stu-id="63d51-146">hello resource Group</span></span>|
|<span data-ttu-id="63d51-147">instanceId</span><span class="sxs-lookup"><span data-stu-id="63d51-147">instanceId</span></span>|<span data-ttu-id="63d51-148">cadena</span><span class="sxs-lookup"><span data-stu-id="63d51-148">string</span></span>|<span data-ttu-id="63d51-149">Identificador de instancia</span><span class="sxs-lookup"><span data-stu-id="63d51-149">Instance Id</span></span>|
|<span data-ttu-id="63d51-150">additionalInfo</span><span class="sxs-lookup"><span data-stu-id="63d51-150">additionalInfo</span></span>|<span data-ttu-id="63d51-151">string</span><span class="sxs-lookup"><span data-stu-id="63d51-151">string</span></span>|<span data-ttu-id="63d51-152">Cadena JSON de información adicional</span><span class="sxs-lookup"><span data-stu-id="63d51-152">Additional info JSON string</span></span>|
|<span data-ttu-id="63d51-153">etiquetas</span><span class="sxs-lookup"><span data-stu-id="63d51-153">tags</span></span>|<span data-ttu-id="63d51-154">cadena</span><span class="sxs-lookup"><span data-stu-id="63d51-154">string</span></span>|<span data-ttu-id="63d51-155">Cadena JSON de etiqueta</span><span class="sxs-lookup"><span data-stu-id="63d51-155">Tag JSON string</span></span>|
|<span data-ttu-id="63d51-156">orderNumber</span><span class="sxs-lookup"><span data-stu-id="63d51-156">orderNumber</span></span>|<span data-ttu-id="63d51-157">cadena</span><span class="sxs-lookup"><span data-stu-id="63d51-157">string</span></span>|<span data-ttu-id="63d51-158">número de pedido de Hola</span><span class="sxs-lookup"><span data-stu-id="63d51-158">hello order number</span></span>|
|<span data-ttu-id="63d51-159">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="63d51-159">unitOfMeasure</span></span>|<span data-ttu-id="63d51-160">cadena</span><span class="sxs-lookup"><span data-stu-id="63d51-160">string</span></span>|<span data-ttu-id="63d51-161">Unidad de medida para el medidor de Hola</span><span class="sxs-lookup"><span data-stu-id="63d51-161">Unit of measure for hello meter</span></span>|
|<span data-ttu-id="63d51-162">costCenter</span><span class="sxs-lookup"><span data-stu-id="63d51-162">costCenter</span></span>|<span data-ttu-id="63d51-163">cadena</span><span class="sxs-lookup"><span data-stu-id="63d51-163">string</span></span>|<span data-ttu-id="63d51-164">Centro de costo de Hola</span><span class="sxs-lookup"><span data-stu-id="63d51-164">hello cost center</span></span>|
|<span data-ttu-id="63d51-165">accountId</span><span class="sxs-lookup"><span data-stu-id="63d51-165">accountId</span></span>|<span data-ttu-id="63d51-166">int</span><span class="sxs-lookup"><span data-stu-id="63d51-166">int</span></span>|<span data-ttu-id="63d51-167">Id. de cuenta de Hello</span><span class="sxs-lookup"><span data-stu-id="63d51-167">hello account Id</span></span>|
|<span data-ttu-id="63d51-168">accountName</span><span class="sxs-lookup"><span data-stu-id="63d51-168">accountName</span></span>|<span data-ttu-id="63d51-169">cadena</span><span class="sxs-lookup"><span data-stu-id="63d51-169">string</span></span> |<span data-ttu-id="63d51-170">Nombre de la cuenta de Hello</span><span class="sxs-lookup"><span data-stu-id="63d51-170">hello Account Name</span></span>|
|<span data-ttu-id="63d51-171">accountOwnerId</span><span class="sxs-lookup"><span data-stu-id="63d51-171">accountOwnerId</span></span>|<span data-ttu-id="63d51-172">cadena</span><span class="sxs-lookup"><span data-stu-id="63d51-172">string</span></span>|<span data-ttu-id="63d51-173">Hola Id. de propietario de cuenta</span><span class="sxs-lookup"><span data-stu-id="63d51-173">hello Account Owner Id</span></span>|
|<span data-ttu-id="63d51-174">departmentId</span><span class="sxs-lookup"><span data-stu-id="63d51-174">departmentId</span></span>|<span data-ttu-id="63d51-175">int</span><span class="sxs-lookup"><span data-stu-id="63d51-175">int</span></span>|<span data-ttu-id="63d51-176">departamento de Hello Id.</span><span class="sxs-lookup"><span data-stu-id="63d51-176">hello department Id</span></span>|
|<span data-ttu-id="63d51-177">departmentName</span><span class="sxs-lookup"><span data-stu-id="63d51-177">departmentName</span></span>|<span data-ttu-id="63d51-178">cadena</span><span class="sxs-lookup"><span data-stu-id="63d51-178">string</span></span>|<span data-ttu-id="63d51-179">nombre del departamento de Hola</span><span class="sxs-lookup"><span data-stu-id="63d51-179">hello department name</span></span>|
|<span data-ttu-id="63d51-180">publisherName</span><span class="sxs-lookup"><span data-stu-id="63d51-180">publisherName</span></span>|<span data-ttu-id="63d51-181">cadena</span><span class="sxs-lookup"><span data-stu-id="63d51-181">string</span></span>|<span data-ttu-id="63d51-182">nombre del publicador Hola</span><span class="sxs-lookup"><span data-stu-id="63d51-182">hello publisher name</span></span>|
|<span data-ttu-id="63d51-183">planName</span><span class="sxs-lookup"><span data-stu-id="63d51-183">planName</span></span>|<span data-ttu-id="63d51-184">cadena</span><span class="sxs-lookup"><span data-stu-id="63d51-184">string</span></span>|<span data-ttu-id="63d51-185">nombre del Plan de Hola</span><span class="sxs-lookup"><span data-stu-id="63d51-185">hello Plan name</span></span>|
|<span data-ttu-id="63d51-186">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="63d51-186">consumedQuantity</span></span>|<span data-ttu-id="63d51-187">Decimal</span><span class="sxs-lookup"><span data-stu-id="63d51-187">decimal</span></span>|<span data-ttu-id="63d51-188">Cantidad consumida durante este período</span><span class="sxs-lookup"><span data-stu-id="63d51-188">Consumed Quantity during this time period</span></span>|
|<span data-ttu-id="63d51-189">resourceRate</span><span class="sxs-lookup"><span data-stu-id="63d51-189">resourceRate</span></span>|<span data-ttu-id="63d51-190">Decimal</span><span class="sxs-lookup"><span data-stu-id="63d51-190">decimal</span></span>|<span data-ttu-id="63d51-191">Precio por unidad de medidor Hola</span><span class="sxs-lookup"><span data-stu-id="63d51-191">Unit price for hello meter</span></span>|
|<span data-ttu-id="63d51-192">extendedCost</span><span class="sxs-lookup"><span data-stu-id="63d51-192">extendedCost</span></span>|<span data-ttu-id="63d51-193">Decimal</span><span class="sxs-lookup"><span data-stu-id="63d51-193">decimal</span></span>|<span data-ttu-id="63d51-194">Gasto estimado según la cantidad consumida y el costo total</span><span class="sxs-lookup"><span data-stu-id="63d51-194">Estimated charge based on Consumed Quantity and Extended cost</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="63d51-195">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="63d51-195">See also</span></span>

* [<span data-ttu-id="63d51-196">API de períodos de facturación</span><span class="sxs-lookup"><span data-stu-id="63d51-196">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="63d51-197">API de detalles de uso</span><span class="sxs-lookup"><span data-stu-id="63d51-197">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="63d51-198">API de saldo y resumen</span><span class="sxs-lookup"><span data-stu-id="63d51-198">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="63d51-199">API de hoja de precios</span><span class="sxs-lookup"><span data-stu-id="63d51-199">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)