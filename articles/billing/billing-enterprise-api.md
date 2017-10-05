---
title: "API de facturación de Azure Enterprise | Microsoft Docs"
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
ms.openlocfilehash: e3a5f9bcd6b54a51c29df649f1ae8ac185b153a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a><span data-ttu-id="ad585-103">Información general de API de informes para clientes de Enterprise</span><span class="sxs-lookup"><span data-stu-id="ad585-103">Overview of Reporting APIs for Enterprise customers</span></span>
<span data-ttu-id="ad585-104">Las API de informes permiten a los clientes de Azure Enterprise extraer datos de facturación y consumo mediante programación en las herramientas de análisis de datos preferidas.</span><span class="sxs-lookup"><span data-stu-id="ad585-104">The Reporting APIs enable Enterprise Azure customers to programmatically pull consumption and billing data into preferred data analysis tools.</span></span> 

## <a name="enabling-data-access-to-the-api"></a><span data-ttu-id="ad585-105">Habilitación del acceso de datos a la API</span><span class="sxs-lookup"><span data-stu-id="ad585-105">Enabling data access to the API</span></span>
* <span data-ttu-id="ad585-106">**Generar o recuperar la clave de API**: inicie sesión en el portal de Enterprise y siga el tutorial en la sección de API de informes de la ayuda.</span><span class="sxs-lookup"><span data-stu-id="ad585-106">**Generate or retrieve the API key** - Log in to the Enterprise portal and follow the tutorial under Help - Reporting APIs.</span></span> <span data-ttu-id="ad585-107">La primera sección de este artículo de ayuda explica cómo generar o recuperar la clave de API para la inscripción especificada.</span><span class="sxs-lookup"><span data-stu-id="ad585-107">The first section under this help article explains how to generate or retrieve the API key for the specified enrollment.</span></span>
* <span data-ttu-id="ad585-108">**Pasar claves en la API**: la clave de API tiene que pasarse para cada llamada para la autenticación y autorización.</span><span class="sxs-lookup"><span data-stu-id="ad585-108">**Passing keys in the API** - The API key needs to be passed for each call for Authentication and Authorization.</span></span> <span data-ttu-id="ad585-109">La siguiente propiedad tiene que ser los encabezados HTTP.</span><span class="sxs-lookup"><span data-stu-id="ad585-109">The following property needs to be to the HTTP headers</span></span>

|<span data-ttu-id="ad585-110">Clave de encabezado de solicitud</span><span class="sxs-lookup"><span data-stu-id="ad585-110">Request Header Key</span></span> | <span data-ttu-id="ad585-111">Valor</span><span class="sxs-lookup"><span data-stu-id="ad585-111">Value</span></span>|
|-|-|
|<span data-ttu-id="ad585-112">Autorización</span><span class="sxs-lookup"><span data-stu-id="ad585-112">Authorization</span></span>| <span data-ttu-id="ad585-113">Especifique el valor con este formato: **bearer {API_KEY}**</span><span class="sxs-lookup"><span data-stu-id="ad585-113">Specify the value in this format: **bearer {API_KEY}**</span></span> <br/> <span data-ttu-id="ad585-114">Ejemplo: bearer eyr....09</span><span class="sxs-lookup"><span data-stu-id="ad585-114">Example: bearer eyr....09</span></span>|

## <a name="consumption-apis"></a><span data-ttu-id="ad585-115">API de consumo</span><span class="sxs-lookup"><span data-stu-id="ad585-115">Consumption APIs</span></span>
<span data-ttu-id="ad585-116">Hay disponible un punto de conexión de Swagger [aquí](https://consumption.azure.com/swagger/ui/index) para la API descrita a continuación que debe habilitar una introspección sencilla de la API y la capacidad de generar SDK de cliente con [AutoRest](https://github.com/Azure/AutoRest) o [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span><span class="sxs-lookup"><span data-stu-id="ad585-116">A Swagger endpoint is available [here](https://consumption.azure.com/swagger/ui/index) for the APIs described below which should enable easy introspection of the API and the ability to generate client SDKs using [AutoRest](https://github.com/Azure/AutoRest) or [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span></span> <span data-ttu-id="ad585-117">Los datos a partir del 1 de mayo de 2014 están disponibles a través de esta API.</span><span class="sxs-lookup"><span data-stu-id="ad585-117">Data beginning May 1, 2014 is available through this API.</span></span> 

* <span data-ttu-id="ad585-118">**Saldos y resumen**: la [API de saldos y resumen](billing-enterprise-api-balance-summary.md) ofrece un resumen mensual de información sobre saldos, nuevas compras, gastos de servicios en Azure Marketplace, ajustes y gastos de uso por encima del límite.</span><span class="sxs-lookup"><span data-stu-id="ad585-118">**Balance and Summary** - The [Balance and Summary API](billing-enterprise-api-balance-summary.md) offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments and overage charges.</span></span>

* <span data-ttu-id="ad585-119">**Detalles de uso**: la [API de detalles de uso](billing-enterprise-api-usage-detail.md) ofrece un desglose diario de cantidades consumidas y gastos estimados por una inscripción.</span><span class="sxs-lookup"><span data-stu-id="ad585-119">**Usage Details** - The [Usage Detail API](billing-enterprise-api-usage-detail.md) offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="ad585-120">El resultado también incluye información sobre instancias, medidores y departamentos.</span><span class="sxs-lookup"><span data-stu-id="ad585-120">The result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="ad585-121">La API se puede consultar por período de facturación o por una fecha de inicio y finalización especificada.</span><span class="sxs-lookup"><span data-stu-id="ad585-121">The API can be queried by Billing period or by a specified start and end date.</span></span> 

* <span data-ttu-id="ad585-122">**Gasto en la tienda Marketplace**: la [API de gastos en la tienda Marketplace](billing-enterprise-api-marketplace-storecharge.md) devuelve el desglose de los gastos de Marketplace basado en el uso por día para el período de facturación o las fechas de inicio y finalización especificadas (no se incluyen las cuotas de una vez).</span><span class="sxs-lookup"><span data-stu-id="ad585-122">**Marketplace Store Charge** - The [Marketplace Store Charge API](billing-enterprise-api-marketplace-storecharge.md) returns the usage-based marketplace charges breakdown by day for the specified Billing Period or start and end dates (one time fees are not included).</span></span>

* <span data-ttu-id="ad585-123">**Hoja de precios**: la [API de hoja de precios](billing-enterprise-api-pricesheet.md) proporciona el tipo aplicable de cada medidor para la inscripción y el período de facturación determinados.</span><span class="sxs-lookup"><span data-stu-id="ad585-123">**Price Sheet** - The [Price Sheet API](billing-enterprise-api-pricesheet.md) provides the applicable rate for each Meter for the given Enrollment and Billing Period.</span></span> 

## <a name="helper-apis"></a><span data-ttu-id="ad585-124">API de ayuda</span><span class="sxs-lookup"><span data-stu-id="ad585-124">Helper APIs</span></span>
 <span data-ttu-id="ad585-125">**Enumerar períodos de facturación**: la [API de períodos de facturación](billing-enterprise-api-billing-periods.md) devuelve una lista de períodos de facturación que tienen datos de consumo para la inscripción especificada en orden cronológico inverso.</span><span class="sxs-lookup"><span data-stu-id="ad585-125">**List Billing Periods** - The [Billing Periods API](billing-enterprise-api-billing-periods.md) returns a list of billing periods that have consumption data for the specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="ad585-126">Cada período contiene una propiedad que señala a la ruta de la API para los cuatro conjuntos de datos: BalanceSummary, UsageDetails, Marketplace Charges y Price Sheet.</span><span class="sxs-lookup"><span data-stu-id="ad585-126">Each Period contains a property pointing to the API route for the four sets of data - BalanceSummary, UsageDetails, Marketplace Charges, and Price Sheet.</span></span>


## <a name="api-response-codes"></a><span data-ttu-id="ad585-127">Códigos de respuesta de la API</span><span class="sxs-lookup"><span data-stu-id="ad585-127">API Response Codes</span></span>  
|<span data-ttu-id="ad585-128">Código de estado de respuesta</span><span class="sxs-lookup"><span data-stu-id="ad585-128">Response Status Code</span></span>|<span data-ttu-id="ad585-129">Message</span><span class="sxs-lookup"><span data-stu-id="ad585-129">Message</span></span>|<span data-ttu-id="ad585-130">Descripción</span><span class="sxs-lookup"><span data-stu-id="ad585-130">Description</span></span>|
|-|-|-|
|<span data-ttu-id="ad585-131">200</span><span class="sxs-lookup"><span data-stu-id="ad585-131">200</span></span>| <span data-ttu-id="ad585-132">OK</span><span class="sxs-lookup"><span data-stu-id="ad585-132">OK</span></span>|<span data-ttu-id="ad585-133">Sin errores</span><span class="sxs-lookup"><span data-stu-id="ad585-133">No error</span></span>|
|<span data-ttu-id="ad585-134">401</span><span class="sxs-lookup"><span data-stu-id="ad585-134">401</span></span>| <span data-ttu-id="ad585-135">No autorizado</span><span class="sxs-lookup"><span data-stu-id="ad585-135">Unauthorized</span></span>| <span data-ttu-id="ad585-136">Clave de API no encontrada, no válida, expirada, etc.</span><span class="sxs-lookup"><span data-stu-id="ad585-136">API Key not found, Invalid, Expired etc.</span></span>|
|<span data-ttu-id="ad585-137">404</span><span class="sxs-lookup"><span data-stu-id="ad585-137">404</span></span>| <span data-ttu-id="ad585-138">No disponible</span><span class="sxs-lookup"><span data-stu-id="ad585-138">Unavailable</span></span>| <span data-ttu-id="ad585-139">Punto de conexión de informe no encontrado</span><span class="sxs-lookup"><span data-stu-id="ad585-139">Report endpoint not found</span></span>|
|<span data-ttu-id="ad585-140">400</span><span class="sxs-lookup"><span data-stu-id="ad585-140">400</span></span>| <span data-ttu-id="ad585-141">Bad Request</span><span class="sxs-lookup"><span data-stu-id="ad585-141">Bad Request</span></span>| <span data-ttu-id="ad585-142">Parámetros no válidos: intervalos de fechas, números EA, etc.</span><span class="sxs-lookup"><span data-stu-id="ad585-142">Invalid params – Date ranges, EA numbers etc.</span></span>|
|<span data-ttu-id="ad585-143">500</span><span class="sxs-lookup"><span data-stu-id="ad585-143">500</span></span>| <span data-ttu-id="ad585-144">Error de servidor</span><span class="sxs-lookup"><span data-stu-id="ad585-144">Server Error</span></span>| <span data-ttu-id="ad585-145">Error inesperado al procesar la solicitud</span><span class="sxs-lookup"><span data-stu-id="ad585-145">Unexoected error processing request</span></span>| 









