---
title: "aaaAzure las API de empresa de facturación: equilibrio y resumen | Documentos de Microsoft"
description: "Obtenga información acerca del uso de facturación de Azure y RateCard APIs, que son visiones tooprovide usado del consumo de recursos de Azure y tendencias."
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
ms.openlocfilehash: b031de2c347e5abeacd11743cc96024434518918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a><span data-ttu-id="27389-103">API de informes para clientes de Enterprise: saldos y resumen</span><span class="sxs-lookup"><span data-stu-id="27389-103">Reporting APIs for Enterprise customers - Balance and Summary</span></span>

<span data-ttu-id="27389-104">Hola saldo y API de resumen le ofrece un resumen de información sobre saldos, nuevas adquisiciones, cargos de servicios de Azure Marketplace, ajustes y cargos por encima del límite mensual.</span><span class="sxs-lookup"><span data-stu-id="27389-104">hello Balance and Summary API offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments, and overage charges.</span></span>


##<a name="request"></a><span data-ttu-id="27389-105">Solicitud</span><span class="sxs-lookup"><span data-stu-id="27389-105">Request</span></span> 
<span data-ttu-id="27389-106">Se especifican las propiedades de encabezado comunes que necesitan toobe agrega [aquí](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="27389-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="27389-107">Si no se especifica un período de facturación, a continuación, datos de facturación actual de Hola período se devuelven.</span><span class="sxs-lookup"><span data-stu-id="27389-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span>

|<span data-ttu-id="27389-108">Método</span><span class="sxs-lookup"><span data-stu-id="27389-108">Method</span></span> | <span data-ttu-id="27389-109">URI de solicitud</span><span class="sxs-lookup"><span data-stu-id="27389-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="27389-110">GET</span><span class="sxs-lookup"><span data-stu-id="27389-110">GET</span></span>| <span data-ttu-id="27389-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="27389-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span></span>|
|<span data-ttu-id="27389-112">GET</span><span class="sxs-lookup"><span data-stu-id="27389-112">GET</span></span>| <span data-ttu-id="27389-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="27389-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span></span>|

> [!Note]
> <span data-ttu-id="27389-114">versión de vista previa de hello toouse de API, reemplace v2 con v1 en hello por encima de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="27389-114">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="27389-115">Response</span><span class="sxs-lookup"><span data-stu-id="27389-115">Response</span></span>

        {
            "id": "enrollments/100/billingperiods/201507/balancesummaries",
            "billingPeriodId": 201507,
            "currencyCode": "USD",
            "beginningBalance": 0,
            "endingBalance": 1.1,
            "newPurchases": 1,
            "adjustments": 1.1,
            "utilized": 1.1,
            "serviceOverage": 1,
            "chargesBilledSeparately": 1,
            "totalOverage": 1,
            "totalUsage": 1.1,
            "azureMarketplaceServiceCharges": 1,
            "newPurchasesDetails": [
                {
                "name": "",
                "value": 1
                }
            ],
            "adjustmentDetails": [
                {
                "name": "Promo Credit",
                "value": 1.1
                },
                {
                "name": "SIE Credit",
                "value": 1.0
                }
            ]
        }


<span data-ttu-id="27389-116">**Definiciones de propiedad de respuesta**</span><span class="sxs-lookup"><span data-stu-id="27389-116">**Response property definitions**</span></span>

|<span data-ttu-id="27389-117">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="27389-117">Property Name</span></span>| <span data-ttu-id="27389-118">Tipo</span><span class="sxs-lookup"><span data-stu-id="27389-118">Type</span></span>| <span data-ttu-id="27389-119">Descripción</span><span class="sxs-lookup"><span data-stu-id="27389-119">Description</span></span>
|-|-|-|
|<span data-ttu-id="27389-120">id</span><span class="sxs-lookup"><span data-stu-id="27389-120">id</span></span>|<span data-ttu-id="27389-121">cadena</span><span class="sxs-lookup"><span data-stu-id="27389-121">string</span></span>|<span data-ttu-id="27389-122">Hola Id. único para la inscripción y un período de facturación específico</span><span class="sxs-lookup"><span data-stu-id="27389-122">hello unique Id for a specific billing period and enrollment</span></span>|
|<span data-ttu-id="27389-123">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="27389-123">billingPeriodId</span></span>|<span data-ttu-id="27389-124">cadena</span><span class="sxs-lookup"><span data-stu-id="27389-124">string</span></span> |<span data-ttu-id="27389-125">Hola Id. del período de facturación</span><span class="sxs-lookup"><span data-stu-id="27389-125">hello billing period Id</span></span>|
|<span data-ttu-id="27389-126">currencyCode</span><span class="sxs-lookup"><span data-stu-id="27389-126">currencyCode</span></span>|<span data-ttu-id="27389-127">cadena</span><span class="sxs-lookup"><span data-stu-id="27389-127">string</span></span> |<span data-ttu-id="27389-128">código de divisa de Hola</span><span class="sxs-lookup"><span data-stu-id="27389-128">hello currency code</span></span>|
|<span data-ttu-id="27389-129">beginningBalance</span><span class="sxs-lookup"><span data-stu-id="27389-129">beginningBalance</span></span>|<span data-ttu-id="27389-130">Decimal</span><span class="sxs-lookup"><span data-stu-id="27389-130">decimal</span></span>| <span data-ttu-id="27389-131">saldo inicial de Hola Hola período de facturación</span><span class="sxs-lookup"><span data-stu-id="27389-131">hello beginning balance for hello billing period</span></span>|
|<span data-ttu-id="27389-132">endingBalance</span><span class="sxs-lookup"><span data-stu-id="27389-132">endingBalance</span></span>|<span data-ttu-id="27389-133">Decimal</span><span class="sxs-lookup"><span data-stu-id="27389-133">decimal</span></span>| <span data-ttu-id="27389-134">Hola saldo final de período de facturación de hello (para períodos abiertos se actualizarán cada día)</span><span class="sxs-lookup"><span data-stu-id="27389-134">hello ending balance for hello billing period (for open periods this will be updated daily)</span></span>|
|<span data-ttu-id="27389-135">newPurchases</span><span class="sxs-lookup"><span data-stu-id="27389-135">newPurchases</span></span>|<span data-ttu-id="27389-136">Decimal</span><span class="sxs-lookup"><span data-stu-id="27389-136">decimal</span></span>| <span data-ttu-id="27389-137">Cantidad total de nuevas compras</span><span class="sxs-lookup"><span data-stu-id="27389-137">Total new purchase amount</span></span>|
|<span data-ttu-id="27389-138">adjustments</span><span class="sxs-lookup"><span data-stu-id="27389-138">adjustments</span></span>|<span data-ttu-id="27389-139">Decimal</span><span class="sxs-lookup"><span data-stu-id="27389-139">decimal</span></span>| <span data-ttu-id="27389-140">Importe total de ajuste</span><span class="sxs-lookup"><span data-stu-id="27389-140">Total adjustment amount</span></span>|
|<span data-ttu-id="27389-141">utilized</span><span class="sxs-lookup"><span data-stu-id="27389-141">utilized</span></span>|<span data-ttu-id="27389-142">Decimal</span><span class="sxs-lookup"><span data-stu-id="27389-142">decimal</span></span>| <span data-ttu-id="27389-143">Uso total de compromiso</span><span class="sxs-lookup"><span data-stu-id="27389-143">Total Commitment usage</span></span>|
|<span data-ttu-id="27389-144">serviceOverage</span><span class="sxs-lookup"><span data-stu-id="27389-144">serviceOverage</span></span>|<span data-ttu-id="27389-145">Decimal</span><span class="sxs-lookup"><span data-stu-id="27389-145">decimal</span></span>| <span data-ttu-id="27389-146">Uso por encima del límite de servicios de Azure</span><span class="sxs-lookup"><span data-stu-id="27389-146">Overage for Azure services</span></span>|
|<span data-ttu-id="27389-147">chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="27389-147">chargesBilledSeparately</span></span>|<span data-ttu-id="27389-148">Decimal</span><span class="sxs-lookup"><span data-stu-id="27389-148">decimal</span></span>| <span data-ttu-id="27389-149">Gastos facturados por separado</span><span class="sxs-lookup"><span data-stu-id="27389-149">Charges Billed separately</span></span>|
|<span data-ttu-id="27389-150">totalOverage</span><span class="sxs-lookup"><span data-stu-id="27389-150">totalOverage</span></span>|<span data-ttu-id="27389-151">Decimal</span><span class="sxs-lookup"><span data-stu-id="27389-151">decimal</span></span>| <span data-ttu-id="27389-152">serviceOverage + chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="27389-152">serviceOverage + chargesBilledSeparately</span></span>|
|<span data-ttu-id="27389-153">totalUsage</span><span class="sxs-lookup"><span data-stu-id="27389-153">totalUsage</span></span>|<span data-ttu-id="27389-154">Decimal</span><span class="sxs-lookup"><span data-stu-id="27389-154">decimal</span></span>| <span data-ttu-id="27389-155">Compromiso de servicio de Azure + uso por encima del límite total</span><span class="sxs-lookup"><span data-stu-id="27389-155">Azure service commitment + total Overage</span></span>|
|<span data-ttu-id="27389-156">azureMarketplaceServiceCharges</span><span class="sxs-lookup"><span data-stu-id="27389-156">azureMarketplaceServiceCharges</span></span>|<span data-ttu-id="27389-157">Decimal</span><span class="sxs-lookup"><span data-stu-id="27389-157">decimal</span></span>| <span data-ttu-id="27389-158">Gastos totales de Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="27389-158">Total charges for Azure Marketplace</span></span>|
|<span data-ttu-id="27389-159">newPurchasesDetails</span><span class="sxs-lookup"><span data-stu-id="27389-159">newPurchasesDetails</span></span>|<span data-ttu-id="27389-160">Matriz de cadenas JSON de pares de nombre y valor</span><span class="sxs-lookup"><span data-stu-id="27389-160">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="27389-161">Lista de nuevas compras</span><span class="sxs-lookup"><span data-stu-id="27389-161">List of new purchases</span></span>|
|<span data-ttu-id="27389-162">adjustmentDetails</span><span class="sxs-lookup"><span data-stu-id="27389-162">adjustmentDetails</span></span>|<span data-ttu-id="27389-163">Matriz de cadenas JSON de pares de nombre y valor</span><span class="sxs-lookup"><span data-stu-id="27389-163">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="27389-164">Lista de ajustes (crédito promocional, crédito SIE, etc.)</span><span class="sxs-lookup"><span data-stu-id="27389-164">List of Adjustments (Promo credit, SIE credit etc.)</span></span> |


<br/>
## <a name="see-also"></a><span data-ttu-id="27389-165">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="27389-165">See also</span></span>

* [<span data-ttu-id="27389-166">API de períodos de facturación</span><span class="sxs-lookup"><span data-stu-id="27389-166">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="27389-167">API de detalles de uso</span><span class="sxs-lookup"><span data-stu-id="27389-167">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="27389-168">API de gastos en la tienda Marketplace</span><span class="sxs-lookup"><span data-stu-id="27389-168">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="27389-169">API de hoja de precios</span><span class="sxs-lookup"><span data-stu-id="27389-169">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)