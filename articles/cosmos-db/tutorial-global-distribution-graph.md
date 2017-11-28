---
title: "Tutorial de distribución global de Azure Cosmos DB para API Graph | Microsoft Docs"
description: "Obtenga información sobre cómo configurar la distribución global de Azure Cosmos DB con la API Graph."
services: cosmos-db
keywords: "distribución global, graph, gremlin"
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 3c8794fe33c2ff5aa79559ea2c323cf8d92b426a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-graph-api"></a><span data-ttu-id="00894-104">Configuración de la distribución global de Azure Cosmos DB con la API Graph</span><span class="sxs-lookup"><span data-stu-id="00894-104">How to setup Azure Cosmos DB global distribution using the Graph API</span></span>

<span data-ttu-id="00894-105">En este artículo se muestra cómo usar Azure Portal para configurar la distribución global de Azure Cosmos DB y luego conectarse con la API Graph (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="00894-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the Graph API (preview).</span></span>

<span data-ttu-id="00894-106">En este artículo se tratan las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="00894-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="00894-107">Configuración de la distribución global con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="00894-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="00894-108">Configuración de la distribución global con las [API Graph](graph-introduction.md) (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="00894-108">Configure global distribution using the [Graph APIs](graph-introduction.md) (preview)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-graph-api-using-the-net-sdk"></a><span data-ttu-id="00894-109">Conexión a una región de preferencia con la API Graph mediante el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="00894-109">Connecting to a preferred region using the Graph API using the .NET SDK</span></span>

<span data-ttu-id="00894-110">La API Graph se expone como una biblioteca de extensiones sobre el SDK de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="00894-110">The Graph API is exposed as an extension library on top of the DocumentDB SDK.</span></span>

<span data-ttu-id="00894-111">Para aprovechar las ventajas de la [distribución global](distribute-data-globally.md), las aplicaciones cliente pueden especificar la lista del orden de preferencia de regiones que se usará para llevar a cabo operaciones de documentos.</span><span class="sxs-lookup"><span data-stu-id="00894-111">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="00894-112">Esto puede hacerse estableciendo la directiva de conexión.</span><span class="sxs-lookup"><span data-stu-id="00894-112">This can be done by setting the connection policy.</span></span> <span data-ttu-id="00894-113">Según la configuración de la cuenta de Azure Cosmos DB, la disponibilidad regional actual y la lista de preferencias especificada, el SDK elegirá el punto de conexión óptimo para realizar las operaciones de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="00894-113">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the SDK to perform write and read operations.</span></span>

<span data-ttu-id="00894-114">Esta lista de preferencias se especifica cuando se inicializa una conexión mediante los SDK.</span><span class="sxs-lookup"><span data-stu-id="00894-114">This preference list is specified when initializing a connection using the SDKs.</span></span> <span data-ttu-id="00894-115">Los SDK aceptan un parámetro opcional "PreferredLocations", que es una lista ordenada de regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="00894-115">The SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

* <span data-ttu-id="00894-116">**Escrituras**: el SDK enviará automáticamente todas las escrituras a la región de escritura actual.</span><span class="sxs-lookup"><span data-stu-id="00894-116">**Writes**: The SDK will automatically send all writes to the current write region.</span></span>
* <span data-ttu-id="00894-117">**Lecturas**: todas las lecturas se enviarán a la primera región disponible en la lista de PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="00894-117">**Reads**: All reads will be sent to the first available region in the PreferredLocations list.</span></span> <span data-ttu-id="00894-118">Si se produce un error en la solicitud, el cliente pasará a la siguiente región de la lista y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="00894-118">If the request fails, the client will fail down the list to the next region, and so on.</span></span> <span data-ttu-id="00894-119">Los SDK solo intentarán leer en las regiones especificadas en PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="00894-119">The SDKs will only attempt to read from the regions specified in PreferredLocations.</span></span> <span data-ttu-id="00894-120">Así que, por ejemplo, si la cuenta de Cosmos DB está disponible en tres regiones, pero el cliente solo especifica dos de las regiones de no escritura para PreferredLocations, no se atenderá ninguna lectura desde la región de escritura, incluso en caso de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="00894-120">So, for example, if the Cosmos DB account is available in three regions, but the client only specifies two of the non-write regions for PreferredLocations, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="00894-121">La aplicación puede comprobar los puntos de conexión de escritura y lectura actuales elegidos por el SDK. Para ello, comprueba dos propiedades, WriteEndpoint y ReadEndpoint, disponibles en el SDK 1.8 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="00894-121">The application can verify the current write endpoint and read endpoint chosen by the SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span> <span data-ttu-id="00894-122">Si la propiedad PreferredLocations no está establecida, atenderá todas las solicitudes procedentes de la región de escritura actual.</span><span class="sxs-lookup"><span data-stu-id="00894-122">If the PreferredLocations property is not set, all requests will be served from the current write region.</span></span>

### <a name="using-the-sdk"></a><span data-ttu-id="00894-123">Uso del SDK</span><span class="sxs-lookup"><span data-stu-id="00894-123">Using the SDK</span></span>

<span data-ttu-id="00894-124">Por ejemplo, en el SDK de .NET, el parámetro `ConnectionPolicy` del constructor `DocumentClient` tiene una propiedad llamada `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="00894-124">For example, in the .NET SDK, the `ConnectionPolicy` parameter for the `DocumentClient` constructor has a property called `PreferredLocations`.</span></span> <span data-ttu-id="00894-125">Esta propiedad se puede establecer en una lista de nombres de regiones.</span><span class="sxs-lookup"><span data-stu-id="00894-125">This property can be set to a list of region names.</span></span> <span data-ttu-id="00894-126">Los nombres para mostrar de las [regiones de Azure][regions] se pueden especificar como parte de `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="00894-126">The display names for [Azure Regions][regions] can be specified as part of `PreferredLocations`.</span></span>

> [!NOTE]
> <span data-ttu-id="00894-127">Las direcciones URL de los puntos de conexión no deben considerarse constantes de larga duración.</span><span class="sxs-lookup"><span data-stu-id="00894-127">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="00894-128">El servicio puede actualizarlas en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="00894-128">The service may update these at any point.</span></span> <span data-ttu-id="00894-129">El SDK administra este cambio automáticamente.</span><span class="sxs-lookup"><span data-stu-id="00894-129">The SDK handles this change automatically.</span></span>
>
>

```cs
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;

ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect to Azure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

<span data-ttu-id="00894-130">De este modo finaliza este tutorial.</span><span class="sxs-lookup"><span data-stu-id="00894-130">That's it, that completes this tutorial.</span></span> <span data-ttu-id="00894-131">Para información sobre cómo administrar la coherencia de la cuenta replicada globalmente, lea [Niveles de coherencia en Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="00894-131">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="00894-132">Para más información sobre cómo funciona la replicación global de bases de datos en Azure Cosmos DB, consulte [Distribución global de datos con Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="00894-132">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="00894-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="00894-133">Next steps</span></span>

<span data-ttu-id="00894-134">En este tutorial, ha hecho lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="00894-134">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="00894-135">Configuración de la distribución global con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="00894-135">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="00894-136">Configuración de la distribución global con las API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="00894-136">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="00894-137">Ahora puede continuar en el tutorial siguiente para aprender a desarrollar localmente con el emulador local de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="00894-137">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="00894-138">Desarrollo local con el emulador</span><span class="sxs-lookup"><span data-stu-id="00894-138">Develop locally with the emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

