---
title: "aaaAzure facturación Enterprise API | Documentos de Microsoft"
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
ms.openlocfilehash: 017cecc57ad6bdeb402b5d9d57fc95df9b033a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a><span data-ttu-id="88119-103">Información general de API de informes para clientes de Enterprise</span><span class="sxs-lookup"><span data-stu-id="88119-103">Overview of Reporting APIs for Enterprise customers</span></span>
<span data-ttu-id="88119-104">Hello Reporting API permiten consumo de extracción de tooprogrammatically de los clientes de Enterprise Azure y datos de facturación en herramientas de análisis de datos preferido.</span><span class="sxs-lookup"><span data-stu-id="88119-104">hello Reporting APIs enable Enterprise Azure customers tooprogrammatically pull consumption and billing data into preferred data analysis tools.</span></span> 

## <a name="enabling-data-access-toohello-api"></a><span data-ttu-id="88119-105">Habilitar la API de toohello de acceso a datos</span><span class="sxs-lookup"><span data-stu-id="88119-105">Enabling data access toohello API</span></span>
* <span data-ttu-id="88119-106">**Generar o recuperar la clave de API de hello** - registro de toohello Enterprise portal y seguir Hola tutorial en la Ayuda: API de informes.</span><span class="sxs-lookup"><span data-stu-id="88119-106">**Generate or retrieve hello API key** - Log in toohello Enterprise portal and follow hello tutorial under Help - Reporting APIs.</span></span> <span data-ttu-id="88119-107">Hola primera sección en este artículo de ayuda explican cómo toogenerate o recuperar la clave de hello API para hello especifica inscripción.</span><span class="sxs-lookup"><span data-stu-id="88119-107">hello first section under this help article explains how toogenerate or retrieve hello API key for hello specified enrollment.</span></span>
* <span data-ttu-id="88119-108">**Pasando claves Hola API** -clave Hola API necesita toobe pasa para cada llamada de autenticación y autorización.</span><span class="sxs-lookup"><span data-stu-id="88119-108">**Passing keys in hello API** - hello API key needs toobe passed for each call for Authentication and Authorization.</span></span> <span data-ttu-id="88119-109">propiedad siguiente Hello debe toobe toohello HTTP encabezados</span><span class="sxs-lookup"><span data-stu-id="88119-109">hello following property needs toobe toohello HTTP headers</span></span>

|<span data-ttu-id="88119-110">Clave de encabezado de solicitud</span><span class="sxs-lookup"><span data-stu-id="88119-110">Request Header Key</span></span> | <span data-ttu-id="88119-111">Valor</span><span class="sxs-lookup"><span data-stu-id="88119-111">Value</span></span>|
|-|-|
|<span data-ttu-id="88119-112">Autorización</span><span class="sxs-lookup"><span data-stu-id="88119-112">Authorization</span></span>| <span data-ttu-id="88119-113">Especifique el valor de hello en este formato: **portador {API_KEY}**</span><span class="sxs-lookup"><span data-stu-id="88119-113">Specify hello value in this format: **bearer {API_KEY}**</span></span> <br/> <span data-ttu-id="88119-114">Ejemplo: bearer eyr....09</span><span class="sxs-lookup"><span data-stu-id="88119-114">Example: bearer eyr....09</span></span>|

## <a name="consumption-apis"></a><span data-ttu-id="88119-115">API de consumo</span><span class="sxs-lookup"><span data-stu-id="88119-115">Consumption APIs</span></span>
<span data-ttu-id="88119-116">Está disponible un extremo de Swagger [aquí](https://consumption.azure.com/swagger/ui/index) API de Hola se describen por debajo del cual debería habilitar introspección fácil de hello API y SDK de cliente de toogenerate de capacidad de hello utilizando [AutoRest](https://github.com/Azure/AutoRest) o [ Swagger CodeGen](http://swagger.io/swagger-codegen/).</span><span class="sxs-lookup"><span data-stu-id="88119-116">A Swagger endpoint is available [here](https://consumption.azure.com/swagger/ui/index) for hello APIs described below which should enable easy introspection of hello API and hello ability toogenerate client SDKs using [AutoRest](https://github.com/Azure/AutoRest) or [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span></span> <span data-ttu-id="88119-117">Los datos a partir del 1 de mayo de 2014 están disponibles a través de esta API.</span><span class="sxs-lookup"><span data-stu-id="88119-117">Data beginning May 1, 2014 is available through this API.</span></span> 

* <span data-ttu-id="88119-118">**Equilibrio y resumen** : hello [equilibrio y resumen API](billing-enterprise-api-balance-summary.md) ofrece un resumen de información sobre saldos, nuevas compras, cargos de servicios de Azure Marketplace, ajustes y cargos por encima del límite mensual.</span><span class="sxs-lookup"><span data-stu-id="88119-118">**Balance and Summary** - hello [Balance and Summary API](billing-enterprise-api-balance-summary.md) offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments and overage charges.</span></span>

* <span data-ttu-id="88119-119">**Obtener detalles de uso** : hello [API de detalle de uso](billing-enterprise-api-usage-detail.md) ofrece un desglose diario de cantidades consumidas y gastos estimados por una inscripción.</span><span class="sxs-lookup"><span data-stu-id="88119-119">**Usage Details** - hello [Usage Detail API](billing-enterprise-api-usage-detail.md) offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="88119-120">resultado de Hello también incluye información sobre instancias, medidores y departamentos.</span><span class="sxs-lookup"><span data-stu-id="88119-120">hello result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="88119-121">Hola API se puede consultar por período de facturación o por una apertura especificada y la fecha de finalización.</span><span class="sxs-lookup"><span data-stu-id="88119-121">hello API can be queried by Billing period or by a specified start and end date.</span></span> 

* <span data-ttu-id="88119-122">**Cargo de la tienda del Bazar** : hello [API cargo del almacén de Marketplace](billing-enterprise-api-marketplace-storecharge.md) devuelve desglose de cargos de marketplace basada en el uso de Hola por día para hello especifica el período de facturación o las fechas de inicio y finalización (no se incluyen las cuotas de una vez) .</span><span class="sxs-lookup"><span data-stu-id="88119-122">**Marketplace Store Charge** - hello [Marketplace Store Charge API](billing-enterprise-api-marketplace-storecharge.md) returns hello usage-based marketplace charges breakdown by day for hello specified Billing Period or start and end dates (one time fees are not included).</span></span>

* <span data-ttu-id="88119-123">**Hoja de precios** : hello [API de la hoja de precios](billing-enterprise-api-pricesheet.md) proporciona el tipo aplicable Hola de cada medidor para hello dada la inscripción y el período de facturación.</span><span class="sxs-lookup"><span data-stu-id="88119-123">**Price Sheet** - hello [Price Sheet API](billing-enterprise-api-pricesheet.md) provides hello applicable rate for each Meter for hello given Enrollment and Billing Period.</span></span> 

## <a name="helper-apis"></a><span data-ttu-id="88119-124">API de ayuda</span><span class="sxs-lookup"><span data-stu-id="88119-124">Helper APIs</span></span>
 <span data-ttu-id="88119-125">**Lista de períodos de facturación** : hello [API de períodos de facturación](billing-enterprise-api-billing-periods.md) devuelve una lista de puntos que tienen datos de consumo de hello especificada inscripción en orden cronológico inverso de facturación.</span><span class="sxs-lookup"><span data-stu-id="88119-125">**List Billing Periods** - hello [Billing Periods API](billing-enterprise-api-billing-periods.md) returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="88119-126">Cada período contiene una propiedad que señala la ruta de la API de toohello para cuatro conjuntos de datos - BalanceSummary, UsageDetails, cargos de Marketplace y hoja de precios de Hola.</span><span class="sxs-lookup"><span data-stu-id="88119-126">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marketplace Charges, and Price Sheet.</span></span>


## <a name="api-response-codes"></a><span data-ttu-id="88119-127">Códigos de respuesta de la API</span><span class="sxs-lookup"><span data-stu-id="88119-127">API Response Codes</span></span>  
|<span data-ttu-id="88119-128">Código de estado de respuesta</span><span class="sxs-lookup"><span data-stu-id="88119-128">Response Status Code</span></span>|<span data-ttu-id="88119-129">Message</span><span class="sxs-lookup"><span data-stu-id="88119-129">Message</span></span>|<span data-ttu-id="88119-130">Descripción</span><span class="sxs-lookup"><span data-stu-id="88119-130">Description</span></span>|
|-|-|-|
|<span data-ttu-id="88119-131">200</span><span class="sxs-lookup"><span data-stu-id="88119-131">200</span></span>| <span data-ttu-id="88119-132">OK</span><span class="sxs-lookup"><span data-stu-id="88119-132">OK</span></span>|<span data-ttu-id="88119-133">Sin errores</span><span class="sxs-lookup"><span data-stu-id="88119-133">No error</span></span>|
|<span data-ttu-id="88119-134">401</span><span class="sxs-lookup"><span data-stu-id="88119-134">401</span></span>| <span data-ttu-id="88119-135">No autorizado</span><span class="sxs-lookup"><span data-stu-id="88119-135">Unauthorized</span></span>| <span data-ttu-id="88119-136">Clave de API no encontrada, no válida, expirada, etc.</span><span class="sxs-lookup"><span data-stu-id="88119-136">API Key not found, Invalid, Expired etc.</span></span>|
|<span data-ttu-id="88119-137">404</span><span class="sxs-lookup"><span data-stu-id="88119-137">404</span></span>| <span data-ttu-id="88119-138">No disponible</span><span class="sxs-lookup"><span data-stu-id="88119-138">Unavailable</span></span>| <span data-ttu-id="88119-139">Punto de conexión de informe no encontrado</span><span class="sxs-lookup"><span data-stu-id="88119-139">Report endpoint not found</span></span>|
|<span data-ttu-id="88119-140">400</span><span class="sxs-lookup"><span data-stu-id="88119-140">400</span></span>| <span data-ttu-id="88119-141">Bad Request</span><span class="sxs-lookup"><span data-stu-id="88119-141">Bad Request</span></span>| <span data-ttu-id="88119-142">Parámetros no válidos: intervalos de fechas, números EA, etc.</span><span class="sxs-lookup"><span data-stu-id="88119-142">Invalid params – Date ranges, EA numbers etc.</span></span>|
|<span data-ttu-id="88119-143">500</span><span class="sxs-lookup"><span data-stu-id="88119-143">500</span></span>| <span data-ttu-id="88119-144">Error de servidor</span><span class="sxs-lookup"><span data-stu-id="88119-144">Server Error</span></span>| <span data-ttu-id="88119-145">Error inesperado al procesar la solicitud</span><span class="sxs-lookup"><span data-stu-id="88119-145">Unexoected error processing request</span></span>| 









