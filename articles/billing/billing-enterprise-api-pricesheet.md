---
title: "aaaAzure las API de empresa de facturación: PriceSheet | Documentos de Microsoft"
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
ms.openlocfilehash: 4cfe694c63fba266d117054b046d9caacb3b7197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a><span data-ttu-id="348f3-103">API de informes para clientes de Enterprise: hoja de precios</span><span class="sxs-lookup"><span data-stu-id="348f3-103">Reporting APIs for Enterprise customers - Price Sheet</span></span>

<span data-ttu-id="348f3-104">Hola API de la hoja de precios ofrece tasa aplicable de Hola de cada medidor para hello dada la inscripción y el período de facturación.</span><span class="sxs-lookup"><span data-stu-id="348f3-104">hello Price Sheet API provides hello applicable rate for each Meter for hello given Enrollment and Billing Period.</span></span>

##<a name="request"></a><span data-ttu-id="348f3-105">Solicitud</span><span class="sxs-lookup"><span data-stu-id="348f3-105">Request</span></span>
<span data-ttu-id="348f3-106">Se especifican las propiedades de encabezado comunes que necesitan toobe agrega [aquí](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="348f3-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="348f3-107">Si no se especifica un período de facturación, a continuación, datos de facturación actual de Hola período se devuelven.</span><span class="sxs-lookup"><span data-stu-id="348f3-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span>

|<span data-ttu-id="348f3-108">Método</span><span class="sxs-lookup"><span data-stu-id="348f3-108">Method</span></span> | <span data-ttu-id="348f3-109">URI de solicitud</span><span class="sxs-lookup"><span data-stu-id="348f3-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="348f3-110">GET</span><span class="sxs-lookup"><span data-stu-id="348f3-110">GET</span></span>|<span data-ttu-id="348f3-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="348f3-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span></span>|
|<span data-ttu-id="348f3-112">GET</span><span class="sxs-lookup"><span data-stu-id="348f3-112">GET</span></span>|<span data-ttu-id="348f3-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="348f3-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span></span>|

> [!Note]
> <span data-ttu-id="348f3-114">versión de vista previa de hello toouse de API, reemplace v2 con v1 en hello por encima de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="348f3-114">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="348f3-115">Response</span><span class="sxs-lookup"><span data-stu-id="348f3-115">Response</span></span>

    
        [
            {
                "id": "enrollments/57354989/billingperiods/201601/products/343/pricesheets",
                "billingPeriodId": "201704",
                "meterId": "dc210ecb-97e8-4522-8134-2385494233c0",
                "meterName": "A1 VM",
                "unitOfMeasure": "100 Hours",
                "includedQuantity": 0,
                "partNumber": "N7H-00015",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            {
                "id": "enrollments/57354989/billingperiods/201601/products/2884/pricesheets",
                "billingPeriodId": "201404",
                "meterId": "dc210ecb-97e8-4522-8134-5385494233c0",
                "meterName": "Locally Redundant Storage Premium Storage - Snapshots - AU East",
                "unitOfMeasure": "100 GB",
                "includedQuantity": 0,
                "partNumber": "N9H-00402",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            ...
        ]
    

> [!Note]
><span data-ttu-id="348f3-116">Si usas Hola API de vista previa, meterId campo no está disponible.</span><span class="sxs-lookup"><span data-stu-id="348f3-116">If you are using hello Preview API, meterId field is not available.</span></span>
>

<span data-ttu-id="348f3-117">**Definiciones de propiedad de respuesta**</span><span class="sxs-lookup"><span data-stu-id="348f3-117">**Response property definitions**</span></span>

|<span data-ttu-id="348f3-118">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="348f3-118">Property Name</span></span>| <span data-ttu-id="348f3-119">Tipo</span><span class="sxs-lookup"><span data-stu-id="348f3-119">Type</span></span>| <span data-ttu-id="348f3-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="348f3-120">Description</span></span>
|-|-|-|
|<span data-ttu-id="348f3-121">id</span><span class="sxs-lookup"><span data-stu-id="348f3-121">id</span></span>| <span data-ttu-id="348f3-122">cadena</span><span class="sxs-lookup"><span data-stu-id="348f3-122">string</span></span>| <span data-ttu-id="348f3-123">Hola identificador único que representa un elemento determinado de PriceSheet (metros por período de facturación)</span><span class="sxs-lookup"><span data-stu-id="348f3-123">hello unique Id that represents a particular PriceSheet item (meter by billing period)</span></span>|
|<span data-ttu-id="348f3-124">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="348f3-124">billingPeriodId</span></span>| <span data-ttu-id="348f3-125">cadena</span><span class="sxs-lookup"><span data-stu-id="348f3-125">string</span></span>| <span data-ttu-id="348f3-126">Hola identificador único que representa un período de facturación determinado</span><span class="sxs-lookup"><span data-stu-id="348f3-126">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="348f3-127">meterId</span><span class="sxs-lookup"><span data-stu-id="348f3-127">meterId</span></span>| <span data-ttu-id="348f3-128">cadena</span><span class="sxs-lookup"><span data-stu-id="348f3-128">string</span></span>| <span data-ttu-id="348f3-129">identificador de Hello para el medidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="348f3-129">hello identifier for hello meter.</span></span> <span data-ttu-id="348f3-130">Puede ser asignado toohello uso meterId.</span><span class="sxs-lookup"><span data-stu-id="348f3-130">It can be mapped toohello usage meterId.</span></span>|
|<span data-ttu-id="348f3-131">meterName</span><span class="sxs-lookup"><span data-stu-id="348f3-131">meterName</span></span>| <span data-ttu-id="348f3-132">cadena</span><span class="sxs-lookup"><span data-stu-id="348f3-132">string</span></span>| <span data-ttu-id="348f3-133">nombre de contador de Hola</span><span class="sxs-lookup"><span data-stu-id="348f3-133">hello meter name</span></span>|
|<span data-ttu-id="348f3-134">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="348f3-134">unitOfMeasure</span></span>| <span data-ttu-id="348f3-135">cadena</span><span class="sxs-lookup"><span data-stu-id="348f3-135">string</span></span>| <span data-ttu-id="348f3-136">Hola unidad de medida para medir el servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="348f3-136">hello Unit of Measure for measuring hello service</span></span>|
|<span data-ttu-id="348f3-137">includedQuantity</span><span class="sxs-lookup"><span data-stu-id="348f3-137">includedQuantity</span></span>| <span data-ttu-id="348f3-138">Decimal</span><span class="sxs-lookup"><span data-stu-id="348f3-138">decimal</span></span>| <span data-ttu-id="348f3-139">Cantidad que se incluye</span><span class="sxs-lookup"><span data-stu-id="348f3-139">Quantity that is included</span></span> |
|<span data-ttu-id="348f3-140">partNumber</span><span class="sxs-lookup"><span data-stu-id="348f3-140">partNumber</span></span>| <span data-ttu-id="348f3-141">cadena</span><span class="sxs-lookup"><span data-stu-id="348f3-141">string</span></span>| <span data-ttu-id="348f3-142">número de pieza de Hello asociada Hola medidor</span><span class="sxs-lookup"><span data-stu-id="348f3-142">hello part number associated with hello Meter</span></span>|
|<span data-ttu-id="348f3-143">unitPrice</span><span class="sxs-lookup"><span data-stu-id="348f3-143">unitPrice</span></span>| <span data-ttu-id="348f3-144">Decimal</span><span class="sxs-lookup"><span data-stu-id="348f3-144">decimal</span></span>| <span data-ttu-id="348f3-145">precio por unidad Hello para el medidor de Hola</span><span class="sxs-lookup"><span data-stu-id="348f3-145">hello unit price for hello meter</span></span>|
|<span data-ttu-id="348f3-146">currencyCode</span><span class="sxs-lookup"><span data-stu-id="348f3-146">currencyCode</span></span>| <span data-ttu-id="348f3-147">cadena</span><span class="sxs-lookup"><span data-stu-id="348f3-147">string</span></span>| <span data-ttu-id="348f3-148">código de moneda de Hola para unitPrice Hola</span><span class="sxs-lookup"><span data-stu-id="348f3-148">hello currency code for hello unitPrice</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="348f3-149">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="348f3-149">See also</span></span>

* [<span data-ttu-id="348f3-150">API de períodos de facturación</span><span class="sxs-lookup"><span data-stu-id="348f3-150">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="348f3-151">API de detalles de uso</span><span class="sxs-lookup"><span data-stu-id="348f3-151">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md)

* [<span data-ttu-id="348f3-152">API de saldo y resumen</span><span class="sxs-lookup"><span data-stu-id="348f3-152">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="348f3-153">API de gastos en la tienda Marketplace</span><span class="sxs-lookup"><span data-stu-id="348f3-153">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md)
