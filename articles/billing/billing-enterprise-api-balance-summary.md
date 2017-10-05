---
title: "API de facturación de Azure Enterprise - Saldos y resumen| Microsoft Docs"
description: "Obtenga información sobre las API de RateCard y de uso de facturación de Azure que se usan para proporcionar información sobre el consumo de recursos y tendencias de Azure."
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
ms.openlocfilehash: f6b149f0e656d2263705048aa5b644f5bb4a5712
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a><span data-ttu-id="f11b8-103">API de informes para clientes de Enterprise: saldos y resumen</span><span class="sxs-lookup"><span data-stu-id="f11b8-103">Reporting APIs for Enterprise customers - Balance and Summary</span></span>

<span data-ttu-id="f11b8-104">La API de saldos y resumen ofrece un resumen mensual de información sobre saldos, nuevas compras, gastos de servicios en Azure Marketplace, ajustes y gastos por de uso por encima del límite.</span><span class="sxs-lookup"><span data-stu-id="f11b8-104">The Balance and Summary API offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments, and overage charges.</span></span>


##<a name="request"></a><span data-ttu-id="f11b8-105">Solicitud</span><span class="sxs-lookup"><span data-stu-id="f11b8-105">Request</span></span> 
<span data-ttu-id="f11b8-106">Las propiedades de encabezado comunes que tienen que agregarse se especifican [aquí](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="f11b8-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="f11b8-107">Si no se especifica un período de facturación, se devuelven datos para el período de facturación actual.</span><span class="sxs-lookup"><span data-stu-id="f11b8-107">If a billing period is not specified, then data for the current billing period is returned.</span></span>

|<span data-ttu-id="f11b8-108">Método</span><span class="sxs-lookup"><span data-stu-id="f11b8-108">Method</span></span> | <span data-ttu-id="f11b8-109">URI de solicitud</span><span class="sxs-lookup"><span data-stu-id="f11b8-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="f11b8-110">GET</span><span class="sxs-lookup"><span data-stu-id="f11b8-110">GET</span></span>| <span data-ttu-id="f11b8-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="f11b8-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span></span>|
|<span data-ttu-id="f11b8-112">GET</span><span class="sxs-lookup"><span data-stu-id="f11b8-112">GET</span></span>| <span data-ttu-id="f11b8-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="f11b8-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span></span>|

> [!Note]
> <span data-ttu-id="f11b8-114">Para usar la versión preliminar de la API, reemplace v2 por v1 en la dirección URL anterior.</span><span class="sxs-lookup"><span data-stu-id="f11b8-114">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="f11b8-115">Respuesta</span><span class="sxs-lookup"><span data-stu-id="f11b8-115">Response</span></span>

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


<span data-ttu-id="f11b8-116">**Definiciones de propiedad de respuesta**</span><span class="sxs-lookup"><span data-stu-id="f11b8-116">**Response property definitions**</span></span>

|<span data-ttu-id="f11b8-117">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="f11b8-117">Property Name</span></span>| <span data-ttu-id="f11b8-118">Tipo</span><span class="sxs-lookup"><span data-stu-id="f11b8-118">Type</span></span>| <span data-ttu-id="f11b8-119">Descripción</span><span class="sxs-lookup"><span data-stu-id="f11b8-119">Description</span></span>
|-|-|-|
|<span data-ttu-id="f11b8-120">id</span><span class="sxs-lookup"><span data-stu-id="f11b8-120">id</span></span>|<span data-ttu-id="f11b8-121">cadena</span><span class="sxs-lookup"><span data-stu-id="f11b8-121">string</span></span>|<span data-ttu-id="f11b8-122">Identificador único para una inscripción y un período de facturación específicos</span><span class="sxs-lookup"><span data-stu-id="f11b8-122">The unique Id for a specific billing period and enrollment</span></span>|
|<span data-ttu-id="f11b8-123">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="f11b8-123">billingPeriodId</span></span>|<span data-ttu-id="f11b8-124">cadena</span><span class="sxs-lookup"><span data-stu-id="f11b8-124">string</span></span> |<span data-ttu-id="f11b8-125">Identificador de período de facturación</span><span class="sxs-lookup"><span data-stu-id="f11b8-125">The billing period Id</span></span>|
|<span data-ttu-id="f11b8-126">currencyCode</span><span class="sxs-lookup"><span data-stu-id="f11b8-126">currencyCode</span></span>|<span data-ttu-id="f11b8-127">cadena</span><span class="sxs-lookup"><span data-stu-id="f11b8-127">string</span></span> |<span data-ttu-id="f11b8-128">Código de divisa</span><span class="sxs-lookup"><span data-stu-id="f11b8-128">The currency code</span></span>|
|<span data-ttu-id="f11b8-129">beginningBalance</span><span class="sxs-lookup"><span data-stu-id="f11b8-129">beginningBalance</span></span>|<span data-ttu-id="f11b8-130">Decimal</span><span class="sxs-lookup"><span data-stu-id="f11b8-130">decimal</span></span>| <span data-ttu-id="f11b8-131">Saldo inicial del período de facturación</span><span class="sxs-lookup"><span data-stu-id="f11b8-131">The beginning balance for the billing period</span></span>|
|<span data-ttu-id="f11b8-132">endingBalance</span><span class="sxs-lookup"><span data-stu-id="f11b8-132">endingBalance</span></span>|<span data-ttu-id="f11b8-133">Decimal</span><span class="sxs-lookup"><span data-stu-id="f11b8-133">decimal</span></span>| <span data-ttu-id="f11b8-134">Saldo final del período de facturación (para períodos abiertos, se actualizará a diario)</span><span class="sxs-lookup"><span data-stu-id="f11b8-134">The ending balance for the billing period (for open periods this will be updated daily)</span></span>|
|<span data-ttu-id="f11b8-135">newPurchases</span><span class="sxs-lookup"><span data-stu-id="f11b8-135">newPurchases</span></span>|<span data-ttu-id="f11b8-136">Decimal</span><span class="sxs-lookup"><span data-stu-id="f11b8-136">decimal</span></span>| <span data-ttu-id="f11b8-137">Cantidad total de nuevas compras</span><span class="sxs-lookup"><span data-stu-id="f11b8-137">Total new purchase amount</span></span>|
|<span data-ttu-id="f11b8-138">adjustments</span><span class="sxs-lookup"><span data-stu-id="f11b8-138">adjustments</span></span>|<span data-ttu-id="f11b8-139">Decimal</span><span class="sxs-lookup"><span data-stu-id="f11b8-139">decimal</span></span>| <span data-ttu-id="f11b8-140">Importe total de ajuste</span><span class="sxs-lookup"><span data-stu-id="f11b8-140">Total adjustment amount</span></span>|
|<span data-ttu-id="f11b8-141">utilized</span><span class="sxs-lookup"><span data-stu-id="f11b8-141">utilized</span></span>|<span data-ttu-id="f11b8-142">Decimal</span><span class="sxs-lookup"><span data-stu-id="f11b8-142">decimal</span></span>| <span data-ttu-id="f11b8-143">Uso total de compromiso</span><span class="sxs-lookup"><span data-stu-id="f11b8-143">Total Commitment usage</span></span>|
|<span data-ttu-id="f11b8-144">serviceOverage</span><span class="sxs-lookup"><span data-stu-id="f11b8-144">serviceOverage</span></span>|<span data-ttu-id="f11b8-145">Decimal</span><span class="sxs-lookup"><span data-stu-id="f11b8-145">decimal</span></span>| <span data-ttu-id="f11b8-146">Uso por encima del límite de servicios de Azure</span><span class="sxs-lookup"><span data-stu-id="f11b8-146">Overage for Azure services</span></span>|
|<span data-ttu-id="f11b8-147">chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="f11b8-147">chargesBilledSeparately</span></span>|<span data-ttu-id="f11b8-148">Decimal</span><span class="sxs-lookup"><span data-stu-id="f11b8-148">decimal</span></span>| <span data-ttu-id="f11b8-149">Gastos facturados por separado</span><span class="sxs-lookup"><span data-stu-id="f11b8-149">Charges Billed separately</span></span>|
|<span data-ttu-id="f11b8-150">totalOverage</span><span class="sxs-lookup"><span data-stu-id="f11b8-150">totalOverage</span></span>|<span data-ttu-id="f11b8-151">Decimal</span><span class="sxs-lookup"><span data-stu-id="f11b8-151">decimal</span></span>| <span data-ttu-id="f11b8-152">serviceOverage + chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="f11b8-152">serviceOverage + chargesBilledSeparately</span></span>|
|<span data-ttu-id="f11b8-153">totalUsage</span><span class="sxs-lookup"><span data-stu-id="f11b8-153">totalUsage</span></span>|<span data-ttu-id="f11b8-154">Decimal</span><span class="sxs-lookup"><span data-stu-id="f11b8-154">decimal</span></span>| <span data-ttu-id="f11b8-155">Compromiso de servicio de Azure + uso por encima del límite total</span><span class="sxs-lookup"><span data-stu-id="f11b8-155">Azure service commitment + total Overage</span></span>|
|<span data-ttu-id="f11b8-156">azureMarketplaceServiceCharges</span><span class="sxs-lookup"><span data-stu-id="f11b8-156">azureMarketplaceServiceCharges</span></span>|<span data-ttu-id="f11b8-157">Decimal</span><span class="sxs-lookup"><span data-stu-id="f11b8-157">decimal</span></span>| <span data-ttu-id="f11b8-158">Gastos totales de Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="f11b8-158">Total charges for Azure Marketplace</span></span>|
|<span data-ttu-id="f11b8-159">newPurchasesDetails</span><span class="sxs-lookup"><span data-stu-id="f11b8-159">newPurchasesDetails</span></span>|<span data-ttu-id="f11b8-160">Matriz de cadenas JSON de pares de nombre y valor</span><span class="sxs-lookup"><span data-stu-id="f11b8-160">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="f11b8-161">Lista de nuevas compras</span><span class="sxs-lookup"><span data-stu-id="f11b8-161">List of new purchases</span></span>|
|<span data-ttu-id="f11b8-162">adjustmentDetails</span><span class="sxs-lookup"><span data-stu-id="f11b8-162">adjustmentDetails</span></span>|<span data-ttu-id="f11b8-163">Matriz de cadenas JSON de pares de nombre y valor</span><span class="sxs-lookup"><span data-stu-id="f11b8-163">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="f11b8-164">Lista de ajustes (crédito promocional, crédito SIE, etc.)</span><span class="sxs-lookup"><span data-stu-id="f11b8-164">List of Adjustments (Promo credit, SIE credit etc.)</span></span> |


<br/>
## <a name="see-also"></a><span data-ttu-id="f11b8-165">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="f11b8-165">See also</span></span>

* [<span data-ttu-id="f11b8-166">API de períodos de facturación</span><span class="sxs-lookup"><span data-stu-id="f11b8-166">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="f11b8-167">API de detalles de uso</span><span class="sxs-lookup"><span data-stu-id="f11b8-167">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="f11b8-168">API de gastos en la tienda Marketplace</span><span class="sxs-lookup"><span data-stu-id="f11b8-168">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="f11b8-169">API de hoja de precios</span><span class="sxs-lookup"><span data-stu-id="f11b8-169">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)