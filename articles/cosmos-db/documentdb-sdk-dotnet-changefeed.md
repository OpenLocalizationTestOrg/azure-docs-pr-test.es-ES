---
title: aaaAzure documentos .NET Cambiar fuente procesador SDK & recursos | Documentos de Microsoft
description: "Infórmese acerca de hello SDK como fechas de inicio, fechas de retirada y los cambios realizados entre cada versión de Hola documentos .NET Cambiar fuente procesador SDK y API de procesador de cambio de fuente."
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
ms.openlocfilehash: 7c001cc77f41c01445fb53328e9d99fd3d312c58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="documentdb-net-change-feed-processor-sdk-download-and-release-notes"></a><span data-ttu-id="eb053-103">SDK para los procesadores de fuente de cambios .NET de DocumentDB: descarga y notas de la versión</span><span class="sxs-lookup"><span data-stu-id="eb053-103">DocumentDB .NET Change Feed Processor SDK: Download and release notes</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eb053-104">.NET</span><span class="sxs-lookup"><span data-stu-id="eb053-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="eb053-105">Fuente de cambios de .NET</span><span class="sxs-lookup"><span data-stu-id="eb053-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="eb053-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="eb053-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="eb053-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="eb053-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="eb053-108">Java</span><span class="sxs-lookup"><span data-stu-id="eb053-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="eb053-109">Python</span><span class="sxs-lookup"><span data-stu-id="eb053-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="eb053-110">REST</span><span class="sxs-lookup"><span data-stu-id="eb053-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="eb053-111">Proveedor de recursos de REST</span><span class="sxs-lookup"><span data-stu-id="eb053-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="eb053-112">SQL</span><span class="sxs-lookup"><span data-stu-id="eb053-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="eb053-113">**Descarga del SDK**</span><span class="sxs-lookup"><span data-stu-id="eb053-113">**SDK download**</span></span></td><td>[<span data-ttu-id="eb053-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="eb053-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)</td></tr>

<tr><td><span data-ttu-id="eb053-115">**Documentación de la API**</span><span class="sxs-lookup"><span data-stu-id="eb053-115">**API documentation**</span></span></td><td>[<span data-ttu-id="eb053-116">Documentación de referencia de la API de biblioteca de procesadores de fuente de cambios</span><span class="sxs-lookup"><span data-stu-id="eb053-116">Change Feed Processor library API reference documentation</span></span>](/dotnet/api/microsoft.azure.documents.changefeedprocessor?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="eb053-117">**Introducción**</span><span class="sxs-lookup"><span data-stu-id="eb053-117">**Get started**</span></span></td><td>[<span data-ttu-id="eb053-118">Empezar a trabajar con documentos Cambiar fuente procesador .NET SDK Hola</span><span class="sxs-lookup"><span data-stu-id="eb053-118">Get started with hello DocumentDB Change Feed Processor .NET SDK</span></span>](change-feed.md)</td></tr>

<tr><td><span data-ttu-id="eb053-119">**Plataforma admitida actualmente**</span><span class="sxs-lookup"><span data-stu-id="eb053-119">**Current supported framework**</span></span></td><td>[<span data-ttu-id="eb053-120">Microsoft .NET 4.5 Framework</span><span class="sxs-lookup"><span data-stu-id="eb053-120">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="eb053-121">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="eb053-121">Release notes</span></span>

### <a name="a-name110110"></a><span data-ttu-id="eb053-122"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="eb053-122"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="eb053-123">Agrega un tooobtain una estimación de restantes toobe de trabajo procesado en hello fuente de cambio de método.</span><span class="sxs-lookup"><span data-stu-id="eb053-123">Added a method tooobtain an estimate of remaining work toobe processed in hello Change Feed.</span></span>
* <span data-ttu-id="eb053-124">Compatible con el [SDK para .NET de DocumentDB](documentdb-sdk-dotnet.md), versiones 1.13.2 y superiores.</span><span class="sxs-lookup"><span data-stu-id="eb053-124">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.13.2 and above.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="eb053-125"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="eb053-125"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="eb053-126">SDK de GA</span><span class="sxs-lookup"><span data-stu-id="eb053-126">GA SDK</span></span>
* <span data-ttu-id="eb053-127">Compatible con el [SDK para .NET de DocumentDB](documentdb-sdk-dotnet.md), versiones 1.14.1 e inferiores.</span><span class="sxs-lookup"><span data-stu-id="eb053-127">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.14.1 and below.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="eb053-128">Fechas de lanzamiento y de retirada</span><span class="sxs-lookup"><span data-stu-id="eb053-128">Release & Retirement dates</span></span>
<span data-ttu-id="eb053-129">Microsoft proporcionará la notificación al menos **12 meses** antes de retirar un SDK en la versión de más reciente admitida de orden toosmooth Hola transición tooa.</span><span class="sxs-lookup"><span data-stu-id="eb053-129">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="eb053-130">Nuevas características y funcionalidad y las optimizaciones se agregan solo toohello actual SDK, como por ejemplo, se recomienda que se realice siempre la actualización toohello última versión del SDK tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="eb053-130">New features and functionality and optimizations are only added toohello current SDK, as such it is recommended that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="eb053-131">Servicio de hello rechazará cualquier base de datos con un SDK retirado tooCosmos de solicitud.</span><span class="sxs-lookup"><span data-stu-id="eb053-131">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="eb053-132">Versión</span><span class="sxs-lookup"><span data-stu-id="eb053-132">Version</span></span> | <span data-ttu-id="eb053-133">Fecha de lanzamiento</span><span class="sxs-lookup"><span data-stu-id="eb053-133">Release Date</span></span> | <span data-ttu-id="eb053-134">Fecha de retirada</span><span class="sxs-lookup"><span data-stu-id="eb053-134">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="eb053-135">1.1.0</span><span class="sxs-lookup"><span data-stu-id="eb053-135">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="eb053-136">13 de agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="eb053-136">August 13, 2017</span></span> |--- |
| [<span data-ttu-id="eb053-137">1.0.0</span><span class="sxs-lookup"><span data-stu-id="eb053-137">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="eb053-138">7 de julio de 2017</span><span class="sxs-lookup"><span data-stu-id="eb053-138">July 07, 2017</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="eb053-139">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="eb053-139">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="eb053-140">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="eb053-140">See also</span></span>
<span data-ttu-id="eb053-141">toolearn más información acerca de la base de datos de Cosmos, consulte [base de datos de Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página de servicio.</span><span class="sxs-lookup"><span data-stu-id="eb053-141">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

