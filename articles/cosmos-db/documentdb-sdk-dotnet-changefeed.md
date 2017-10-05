---
title: Recursos y SDK para los procesadores de fuente de cambios .NET para Azure DocumentDB | Microsoft Docs
description: "Aprenda todo lo necesario sobre el SDK y la API para los procesadores de fuente de cambios como, por ejemplo, fechas de lanzamiento, fechas de retirada y cambios realizados de una versión a otra del SDK para los procesadores de fuente de cambios .NET de DocumentDB."
services: cosmos-db
documentationcenter: .net
author: ealsur
manager: kirillg
editor: mimig1
ms.assetid: f2dd9438-8879-4f74-bb6c-e1efc2cd0157
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/14/2017
ms.author: maquaran
ms.openlocfilehash: 40c796bc5af1220c46950a6fac062ffdd243e59f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="documentdb-net-change-feed-processor-sdk-download-and-release-notes"></a><span data-ttu-id="329ef-103">SDK para los procesadores de fuente de cambios .NET de DocumentDB: descarga y notas de la versión</span><span class="sxs-lookup"><span data-stu-id="329ef-103">DocumentDB .NET Change Feed Processor SDK: Download and release notes</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="329ef-104">.NET</span><span class="sxs-lookup"><span data-stu-id="329ef-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="329ef-105">Fuente de cambios de .NET</span><span class="sxs-lookup"><span data-stu-id="329ef-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="329ef-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="329ef-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="329ef-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="329ef-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="329ef-108">Java</span><span class="sxs-lookup"><span data-stu-id="329ef-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="329ef-109">Python</span><span class="sxs-lookup"><span data-stu-id="329ef-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="329ef-110">REST</span><span class="sxs-lookup"><span data-stu-id="329ef-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="329ef-111">Proveedor de recursos de REST</span><span class="sxs-lookup"><span data-stu-id="329ef-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="329ef-112">SQL</span><span class="sxs-lookup"><span data-stu-id="329ef-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="329ef-113">**Descarga del SDK**</span><span class="sxs-lookup"><span data-stu-id="329ef-113">**SDK download**</span></span></td><td>[<span data-ttu-id="329ef-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="329ef-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)</td></tr>

<tr><td><span data-ttu-id="329ef-115">**Documentación de la API**</span><span class="sxs-lookup"><span data-stu-id="329ef-115">**API documentation**</span></span></td><td>[<span data-ttu-id="329ef-116">Documentación de referencia de la API de biblioteca de procesadores de fuente de cambios</span><span class="sxs-lookup"><span data-stu-id="329ef-116">Change Feed Processor library API reference documentation</span></span>](/dotnet/api/microsoft.azure.documents.changefeedprocessor?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="329ef-117">**Introducción**</span><span class="sxs-lookup"><span data-stu-id="329ef-117">**Get started**</span></span></td><td>[<span data-ttu-id="329ef-118">Primeros pasos con el SDL para los procesadores de fuente de cambios .NET de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="329ef-118">Get started with the DocumentDB Change Feed Processor .NET SDK</span></span>](change-feed.md)</td></tr>

<tr><td><span data-ttu-id="329ef-119">**Plataforma admitida actualmente**</span><span class="sxs-lookup"><span data-stu-id="329ef-119">**Current supported framework**</span></span></td><td>[<span data-ttu-id="329ef-120">Microsoft .NET 4.5 Framework</span><span class="sxs-lookup"><span data-stu-id="329ef-120">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="329ef-121">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="329ef-121">Release notes</span></span>

### <a name="a-name110110"></a><span data-ttu-id="329ef-122"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="329ef-122"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="329ef-123">Agregue un método para obtener una estimación de trabajo restante que se va a procesar en la fuente de cambio.</span><span class="sxs-lookup"><span data-stu-id="329ef-123">Added a method to obtain an estimate of remaining work to be processed in the Change Feed.</span></span>
* <span data-ttu-id="329ef-124">Compatible con el [SDK para .NET de DocumentDB](documentdb-sdk-dotnet.md), versiones 1.13.2 y superiores.</span><span class="sxs-lookup"><span data-stu-id="329ef-124">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.13.2 and above.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="329ef-125"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="329ef-125"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="329ef-126">SDK de GA</span><span class="sxs-lookup"><span data-stu-id="329ef-126">GA SDK</span></span>
* <span data-ttu-id="329ef-127">Compatible con el [SDK para .NET de DocumentDB](documentdb-sdk-dotnet.md), versiones 1.14.1 e inferiores.</span><span class="sxs-lookup"><span data-stu-id="329ef-127">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.14.1 and below.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="329ef-128">Fechas de lanzamiento y de retirada</span><span class="sxs-lookup"><span data-stu-id="329ef-128">Release & Retirement dates</span></span>
<span data-ttu-id="329ef-129">Microsoft notificará la retirada de un SDK con al menos **12 meses** de antelación para facilitar la transición a una versión compatible o más reciente.</span><span class="sxs-lookup"><span data-stu-id="329ef-129">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="329ef-130">Solo se agregan nuevas características, funcionalidad y optimizaciones al SDK actual, por lo que se recomienda actualizar siempre a la última versión del SDK tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="329ef-130">New features and functionality and optimizations are only added to the current SDK, as such it is recommended that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="329ef-131">El servicio rechazará cualquier solicitud realizada a Cosmos DB mediante un SDK retirado.</span><span class="sxs-lookup"><span data-stu-id="329ef-131">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

<br/>

| <span data-ttu-id="329ef-132">Versión</span><span class="sxs-lookup"><span data-stu-id="329ef-132">Version</span></span> | <span data-ttu-id="329ef-133">Fecha de lanzamiento</span><span class="sxs-lookup"><span data-stu-id="329ef-133">Release Date</span></span> | <span data-ttu-id="329ef-134">Fecha de retirada</span><span class="sxs-lookup"><span data-stu-id="329ef-134">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="329ef-135">1.1.0</span><span class="sxs-lookup"><span data-stu-id="329ef-135">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="329ef-136">13 de agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="329ef-136">August 13, 2017</span></span> |--- |
| [<span data-ttu-id="329ef-137">1.0.0</span><span class="sxs-lookup"><span data-stu-id="329ef-137">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="329ef-138">7 de julio de 2017</span><span class="sxs-lookup"><span data-stu-id="329ef-138">July 07, 2017</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="329ef-139">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="329ef-139">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="329ef-140">Consulte también</span><span class="sxs-lookup"><span data-stu-id="329ef-140">See also</span></span>
<span data-ttu-id="329ef-141">Para más información sobre Cosmos DB, consulte la página del servicio [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="329ef-141">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

