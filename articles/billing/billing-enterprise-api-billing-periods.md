---
title: "API de facturación de Azure Enterprise - Períodos de facturació| Microsoft Docs"
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
ms.openlocfilehash: c6880b79189e0683387a7aafbd6fa4805b3b42ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a><span data-ttu-id="fddef-103">API de informes para clientes de Enterprise: períodos de facturación</span><span class="sxs-lookup"><span data-stu-id="fddef-103">Reporting APIs for Enterprise customers - Billing Periods</span></span>

<span data-ttu-id="fddef-104">La API de períodos de facturación devuelve una lista de períodos de facturación que tienen datos de consumo para la inscripción especificada en orden cronológico inverso.</span><span class="sxs-lookup"><span data-stu-id="fddef-104">The Billing Periods API returns a list of billing periods that have consumption data for the specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="fddef-105">Cada período contiene una propiedad que señala a la ruta de la API para los cuatro conjuntos de datos: BalanceSummary, UsageDetails, Marketplace Charges y PriceSheet.</span><span class="sxs-lookup"><span data-stu-id="fddef-105">Each Period contains a property pointing to the API route for the four sets of data - BalanceSummary, UsageDetails, Marktplace Charges, and PriceSheet.</span></span> <span data-ttu-id="fddef-106">Si el período no tiene datos, la propiedad correspondiente es null.</span><span class="sxs-lookup"><span data-stu-id="fddef-106">If the period does not have data, the corresponding property is null.</span></span> 


##<a name="request"></a><span data-ttu-id="fddef-107">Solicitud</span><span class="sxs-lookup"><span data-stu-id="fddef-107">Request</span></span> 
<span data-ttu-id="fddef-108">Las propiedades de encabezado comunes que tienen que agregarse se especifican [aquí](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="fddef-108">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> 

|<span data-ttu-id="fddef-109">Método</span><span class="sxs-lookup"><span data-stu-id="fddef-109">Method</span></span> | <span data-ttu-id="fddef-110">URI de solicitud</span><span class="sxs-lookup"><span data-stu-id="fddef-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="fddef-111">GET</span><span class="sxs-lookup"><span data-stu-id="fddef-111">GET</span></span>| <span data-ttu-id="fddef-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span><span class="sxs-lookup"><span data-stu-id="fddef-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span></span>|

> [!Note]
> <span data-ttu-id="fddef-113">Para usar la versión preliminar de la API, reemplace v2 por v1 en la dirección URL anterior.</span><span class="sxs-lookup"><span data-stu-id="fddef-113">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="fddef-114">Respuesta</span><span class="sxs-lookup"><span data-stu-id="fddef-114">Response</span></span>
 
    
    
      [
            {
                "billingPeriodId": "201704",
                "billingStart": "2017-04-01T00:00:00Z",
                "billingEnd": "2017-04-30T11:59:59Z",
                "balanceSummary": "/v1/enrollments/100/billingperiods/201704/balancesummary",
                "usageDetails": "/v1/enrollments/100/billingperiods/201704/usagedetails",
                "marketplaceCharges": "/v1/enrollments/100/billingperiods/201704/marketplacecharges",
                "priceSheet": "/v1/enrollments/100/billingperiods/201704/pricesheet"
            },          
            ....
      ]
    

<span data-ttu-id="fddef-115">**Definiciones de propiedad de respuesta**</span><span class="sxs-lookup"><span data-stu-id="fddef-115">**Response property definitions**</span></span>

|<span data-ttu-id="fddef-116">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="fddef-116">Property Name</span></span>| <span data-ttu-id="fddef-117">Tipo</span><span class="sxs-lookup"><span data-stu-id="fddef-117">Type</span></span>| <span data-ttu-id="fddef-118">Descripción</span><span class="sxs-lookup"><span data-stu-id="fddef-118">Description</span></span>
|-|-|-|
|<span data-ttu-id="fddef-119">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="fddef-119">billingPeriodId</span></span>| <span data-ttu-id="fddef-120">cadena</span><span class="sxs-lookup"><span data-stu-id="fddef-120">string</span></span>| <span data-ttu-id="fddef-121">El identificador único que representa un período de facturación determinado</span><span class="sxs-lookup"><span data-stu-id="fddef-121">The unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="fddef-122">billingStart</span><span class="sxs-lookup"><span data-stu-id="fddef-122">billingStart</span></span>| <span data-ttu-id="fddef-123">datetime</span><span class="sxs-lookup"><span data-stu-id="fddef-123">datetime</span></span>| <span data-ttu-id="fddef-124">Cadena ISO 8601 que representa la fecha de inicio del período</span><span class="sxs-lookup"><span data-stu-id="fddef-124">ISO 8601 string representing the period start date</span></span>|
|<span data-ttu-id="fddef-125">billingEnd</span><span class="sxs-lookup"><span data-stu-id="fddef-125">billingEnd</span></span>| <span data-ttu-id="fddef-126">datetime</span><span class="sxs-lookup"><span data-stu-id="fddef-126">datetime</span></span>| <span data-ttu-id="fddef-127">Cadena ISO 8601 que representa la fecha de finalización del período</span><span class="sxs-lookup"><span data-stu-id="fddef-127">ISO 8601 string representing the period end date</span></span>|
|<span data-ttu-id="fddef-128">balanceSummary</span><span class="sxs-lookup"><span data-stu-id="fddef-128">balanceSummary</span></span>| <span data-ttu-id="fddef-129">cadena</span><span class="sxs-lookup"><span data-stu-id="fddef-129">string</span></span>| <span data-ttu-id="fddef-130">La ruta de acceso de la dirección URL que se enruta a los datos de resumen de saldos para este período</span><span class="sxs-lookup"><span data-stu-id="fddef-130">The URL path that routes to the Balance Summary data for this period</span></span>|
|<span data-ttu-id="fddef-131">usageDetails</span><span class="sxs-lookup"><span data-stu-id="fddef-131">usageDetails</span></span>| <span data-ttu-id="fddef-132">cadena</span><span class="sxs-lookup"><span data-stu-id="fddef-132">string</span></span>| <span data-ttu-id="fddef-133">La ruta de acceso de la dirección URL que se enruta a los datos de detalles de uso para este período</span><span class="sxs-lookup"><span data-stu-id="fddef-133">The URL path that routes to the Usage Details data for this period</span></span>|
|<span data-ttu-id="fddef-134">marketplaceCharges</span><span class="sxs-lookup"><span data-stu-id="fddef-134">marketplaceCharges</span></span>| <span data-ttu-id="fddef-135">cadena</span><span class="sxs-lookup"><span data-stu-id="fddef-135">string</span></span>| <span data-ttu-id="fddef-136">La ruta de acceso de la dirección URL que se enruta a los datos de gastos en Marketplace para este período</span><span class="sxs-lookup"><span data-stu-id="fddef-136">The URL path that routes to the Marketplace Charges data for this period</span></span>|
|<span data-ttu-id="fddef-137">priceSheet</span><span class="sxs-lookup"><span data-stu-id="fddef-137">priceSheet</span></span>| <span data-ttu-id="fddef-138">cadena</span><span class="sxs-lookup"><span data-stu-id="fddef-138">string</span></span>| <span data-ttu-id="fddef-139">La ruta de acceso de la dirección URL que se enruta a los datos de PriceSheet para este período</span><span class="sxs-lookup"><span data-stu-id="fddef-139">The URL path that routes to the PriceSheet data for this period</span></span>|

<br/>
## <a name="see-also"></a><span data-ttu-id="fddef-140">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="fddef-140">See also</span></span>

* [<span data-ttu-id="fddef-141">API de saldo y resumen</span><span class="sxs-lookup"><span data-stu-id="fddef-141">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="fddef-142">API de detalles de uso</span><span class="sxs-lookup"><span data-stu-id="fddef-142">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="fddef-143">API de gastos en la tienda Marketplace</span><span class="sxs-lookup"><span data-stu-id="fddef-143">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="fddef-144">API de hoja de precios</span><span class="sxs-lookup"><span data-stu-id="fddef-144">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)