---
title: "aaaAzure Enterprise API de facturación - períodos de facturación | Documentos de Microsoft"
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
ms.openlocfilehash: d4e17f25b22729a7f213306fb019ee0dbeca87ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a><span data-ttu-id="d5924-103">API de informes para clientes de Enterprise: períodos de facturación</span><span class="sxs-lookup"><span data-stu-id="d5924-103">Reporting APIs for Enterprise customers - Billing Periods</span></span>

<span data-ttu-id="d5924-104">Hola API de períodos de facturación devuelve una lista de períodos que tienen datos de consumo para Hola de facturación especificado inscripción en orden cronológico inverso.</span><span class="sxs-lookup"><span data-stu-id="d5924-104">hello Billing Periods API returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="d5924-105">Cada período contiene una propiedad que señala la ruta de la API de toohello para cuatro conjuntos de datos - BalanceSummary, UsageDetails, Marktplace cargos y PriceSheet de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5924-105">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marktplace Charges, and PriceSheet.</span></span> <span data-ttu-id="d5924-106">Si el período de hello no tiene datos, propiedad correspondiente de hello es null.</span><span class="sxs-lookup"><span data-stu-id="d5924-106">If hello period does not have data, hello corresponding property is null.</span></span> 


##<a name="request"></a><span data-ttu-id="d5924-107">Solicitud</span><span class="sxs-lookup"><span data-stu-id="d5924-107">Request</span></span> 
<span data-ttu-id="d5924-108">Se especifican las propiedades de encabezado comunes que necesitan toobe agrega [aquí](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="d5924-108">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> 

|<span data-ttu-id="d5924-109">Método</span><span class="sxs-lookup"><span data-stu-id="d5924-109">Method</span></span> | <span data-ttu-id="d5924-110">URI de solicitud</span><span class="sxs-lookup"><span data-stu-id="d5924-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="d5924-111">GET</span><span class="sxs-lookup"><span data-stu-id="d5924-111">GET</span></span>| <span data-ttu-id="d5924-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span><span class="sxs-lookup"><span data-stu-id="d5924-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span></span>|

> [!Note]
> <span data-ttu-id="d5924-113">versión de vista previa de hello toouse de API, reemplace v2 con v1 en hello por encima de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="d5924-113">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="d5924-114">Response</span><span class="sxs-lookup"><span data-stu-id="d5924-114">Response</span></span>
 
    
    
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
    

<span data-ttu-id="d5924-115">**Definiciones de propiedad de respuesta**</span><span class="sxs-lookup"><span data-stu-id="d5924-115">**Response property definitions**</span></span>

|<span data-ttu-id="d5924-116">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="d5924-116">Property Name</span></span>| <span data-ttu-id="d5924-117">Tipo</span><span class="sxs-lookup"><span data-stu-id="d5924-117">Type</span></span>| <span data-ttu-id="d5924-118">Descripción</span><span class="sxs-lookup"><span data-stu-id="d5924-118">Description</span></span>
|-|-|-|
|<span data-ttu-id="d5924-119">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="d5924-119">billingPeriodId</span></span>| <span data-ttu-id="d5924-120">cadena</span><span class="sxs-lookup"><span data-stu-id="d5924-120">string</span></span>| <span data-ttu-id="d5924-121">Hola identificador único que representa un período de facturación determinado</span><span class="sxs-lookup"><span data-stu-id="d5924-121">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="d5924-122">billingStart</span><span class="sxs-lookup"><span data-stu-id="d5924-122">billingStart</span></span>| <span data-ttu-id="d5924-123">datetime</span><span class="sxs-lookup"><span data-stu-id="d5924-123">datetime</span></span>| <span data-ttu-id="d5924-124">Cadena de ISO 8601 que representa la fecha de inicio del periodo de Hola</span><span class="sxs-lookup"><span data-stu-id="d5924-124">ISO 8601 string representing hello period start date</span></span>|
|<span data-ttu-id="d5924-125">billingEnd</span><span class="sxs-lookup"><span data-stu-id="d5924-125">billingEnd</span></span>| <span data-ttu-id="d5924-126">datetime</span><span class="sxs-lookup"><span data-stu-id="d5924-126">datetime</span></span>| <span data-ttu-id="d5924-127">Cadena de ISO 8601 que representa la fecha de finalización del periodo de Hola</span><span class="sxs-lookup"><span data-stu-id="d5924-127">ISO 8601 string representing hello period end date</span></span>|
|<span data-ttu-id="d5924-128">balanceSummary</span><span class="sxs-lookup"><span data-stu-id="d5924-128">balanceSummary</span></span>| <span data-ttu-id="d5924-129">cadena</span><span class="sxs-lookup"><span data-stu-id="d5924-129">string</span></span>| <span data-ttu-id="d5924-130">la ruta de acceso de dirección URL de Hola que enruta los datos de resumen de Balance de toohello para este período</span><span class="sxs-lookup"><span data-stu-id="d5924-130">hello URL path that routes toohello Balance Summary data for this period</span></span>|
|<span data-ttu-id="d5924-131">usageDetails</span><span class="sxs-lookup"><span data-stu-id="d5924-131">usageDetails</span></span>| <span data-ttu-id="d5924-132">cadena</span><span class="sxs-lookup"><span data-stu-id="d5924-132">string</span></span>| <span data-ttu-id="d5924-133">la ruta de acceso de dirección URL de Hola que enruta los datos de detalles de uso de toohello para este período</span><span class="sxs-lookup"><span data-stu-id="d5924-133">hello URL path that routes toohello Usage Details data for this period</span></span>|
|<span data-ttu-id="d5924-134">marketplaceCharges</span><span class="sxs-lookup"><span data-stu-id="d5924-134">marketplaceCharges</span></span>| <span data-ttu-id="d5924-135">cadena</span><span class="sxs-lookup"><span data-stu-id="d5924-135">string</span></span>| <span data-ttu-id="d5924-136">la ruta de acceso de dirección URL de Hola que enruta los datos de cargos de Marketplace de toohello para este período</span><span class="sxs-lookup"><span data-stu-id="d5924-136">hello URL path that routes toohello Marketplace Charges data for this period</span></span>|
|<span data-ttu-id="d5924-137">priceSheet</span><span class="sxs-lookup"><span data-stu-id="d5924-137">priceSheet</span></span>| <span data-ttu-id="d5924-138">cadena</span><span class="sxs-lookup"><span data-stu-id="d5924-138">string</span></span>| <span data-ttu-id="d5924-139">la ruta de acceso de dirección URL de Hola que enruta toohello PriceSheet datos para este período</span><span class="sxs-lookup"><span data-stu-id="d5924-139">hello URL path that routes toohello PriceSheet data for this period</span></span>|

<br/>
## <a name="see-also"></a><span data-ttu-id="d5924-140">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="d5924-140">See also</span></span>

* [<span data-ttu-id="d5924-141">API de saldo y resumen</span><span class="sxs-lookup"><span data-stu-id="d5924-141">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="d5924-142">API de detalles de uso</span><span class="sxs-lookup"><span data-stu-id="d5924-142">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="d5924-143">API de gastos en la tienda Marketplace</span><span class="sxs-lookup"><span data-stu-id="d5924-143">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="d5924-144">API de hoja de precios</span><span class="sxs-lookup"><span data-stu-id="d5924-144">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)