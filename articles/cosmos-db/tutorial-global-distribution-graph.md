---
title: "tutorial de distribución global de Cosmos DB aaaAzure para API Graph | Documentos de Microsoft"
description: "Obtenga información acerca de cómo usar de distribución global de base de datos de Azure Cosmos toosetup Hola API Graph."
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
ms.openlocfilehash: 1629a31e12a18079f63e07c4909862b36b5f4c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-graph-api"></a><span data-ttu-id="daf88-104">¿Cómo uso de distribución global de base de datos de Azure Cosmos toosetup Hola API Graph</span><span class="sxs-lookup"><span data-stu-id="daf88-104">How toosetup Azure Cosmos DB global distribution using hello Graph API</span></span>

<span data-ttu-id="daf88-105">En este artículo, le mostramos cómo toouse Hola distribución global de base de datos de Azure Cosmos toosetup de portal de Azure y, a continuación, conectarse con hello API Graph (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="daf88-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello Graph API (preview).</span></span>

<span data-ttu-id="daf88-106">En este artículo se trata Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="daf88-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="daf88-107">Configure la distribución global con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="daf88-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="daf88-108">Configure la distribución global con hello [API de gráfico](graph-introduction.md) (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="daf88-108">Configure global distribution using hello [Graph APIs](graph-introduction.md) (preview)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-graph-api-using-hello-net-sdk"></a><span data-ttu-id="daf88-109">Conexión tooa región preferida mediante la API de Graph hello mediante Hola SDK para .NET</span><span class="sxs-lookup"><span data-stu-id="daf88-109">Connecting tooa preferred region using hello Graph API using hello .NET SDK</span></span>

<span data-ttu-id="daf88-110">Hola API Graph se expone como una biblioteca de extensión en la parte superior hello DocumentDB SDK.</span><span class="sxs-lookup"><span data-stu-id="daf88-110">hello Graph API is exposed as an extension library on top of hello DocumentDB SDK.</span></span>

<span data-ttu-id="daf88-111">En orden tootake aprovechar [distribución global](distribute-data-globally.md), pueden especificar las aplicaciones cliente hello ordenada la lista de preferencias de regiones toobe usa operaciones de documento tooperform.</span><span class="sxs-lookup"><span data-stu-id="daf88-111">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="daf88-112">Esto puede hacerse mediante el establecimiento de directivas de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="daf88-112">This can be done by setting hello connection policy.</span></span> <span data-ttu-id="daf88-113">En función de la configuración de cuenta de base de datos de Azure Cosmos hello, disponibilidad regional actual y la lista de preferencias de hello especificado, Hola mayoría extremo óptimo se elegida por escritura de tooperform SDK de Hola y las operaciones de lectura.</span><span class="sxs-lookup"><span data-stu-id="daf88-113">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello SDK tooperform write and read operations.</span></span>

<span data-ttu-id="daf88-114">Esta lista de preferencias se especifica al inicializar una conexión mediante el SDK de Hola.</span><span class="sxs-lookup"><span data-stu-id="daf88-114">This preference list is specified when initializing a connection using hello SDKs.</span></span> <span data-ttu-id="daf88-115">Hola SDK aceptan un parámetro opcional "PreferredLocations" que es una lista ordenada de regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="daf88-115">hello SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

* <span data-ttu-id="daf88-116">**Escribe**: Hola SDK enviará automáticamente todas las escrituras toohello actual región de escritura.</span><span class="sxs-lookup"><span data-stu-id="daf88-116">**Writes**: hello SDK will automatically send all writes toohello current write region.</span></span>
* <span data-ttu-id="daf88-117">**Lee**: todas las lecturas se enviarán toohello primera región disponible en la lista de PreferredLocations Hola.</span><span class="sxs-lookup"><span data-stu-id="daf88-117">**Reads**: All reads will be sent toohello first available region in hello PreferredLocations list.</span></span> <span data-ttu-id="daf88-118">Si se produce un error en la solicitud de Hola, cliente hello producirá un error hacia abajo de la región de hello lista toohello siguiente y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="daf88-118">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span> <span data-ttu-id="daf88-119">Hola SDK sólo intentará tooread de regiones de hello especificado en PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="daf88-119">hello SDKs will only attempt tooread from hello regions specified in PreferredLocations.</span></span> <span data-ttu-id="daf88-120">Por lo tanto, por ejemplo, si Hola DB Cosmos cuenta está disponible en tres regiones, pero cliente hello especifica sólo dos de las regiones de escritura de Hola para PreferredLocations, a continuación, ningún lecturas se servirá fuera del área de escritura de hello, incluso en caso de hello de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="daf88-120">So, for example, if hello Cosmos DB account is available in three regions, but hello client only specifies two of hello non-write regions for PreferredLocations, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="daf88-121">aplicación Hello puede comprobar el extremo de escritura actual de Hola y leer extremo elegido por hello SDK comprobación dos propiedades, WriteEndpoint y ReadEndpoint, disponible en la versión SDK 1.8 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="daf88-121">hello application can verify hello current write endpoint and read endpoint chosen by hello SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span> <span data-ttu-id="daf88-122">Si no se establece la propiedad PreferredLocations hello, todas las solicitudes se servirá de región de escritura actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="daf88-122">If hello PreferredLocations property is not set, all requests will be served from hello current write region.</span></span>

### <a name="using-hello-sdk"></a><span data-ttu-id="daf88-123">Uso de hello SDK</span><span class="sxs-lookup"><span data-stu-id="daf88-123">Using hello SDK</span></span>

<span data-ttu-id="daf88-124">Por ejemplo, en hello .NET SDK, Hola `ConnectionPolicy` parámetro hello `DocumentClient` constructor tiene una propiedad denominada `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="daf88-124">For example, in hello .NET SDK, hello `ConnectionPolicy` parameter for hello `DocumentClient` constructor has a property called `PreferredLocations`.</span></span> <span data-ttu-id="daf88-125">Esta propiedad puede establecerse tooa lista de nombres de las regiones.</span><span class="sxs-lookup"><span data-stu-id="daf88-125">This property can be set tooa list of region names.</span></span> <span data-ttu-id="daf88-126">nombres para mostrar de Hello [regiones de Azure] [ regions] puede especificarse como parte de `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="daf88-126">hello display names for [Azure Regions][regions] can be specified as part of `PreferredLocations`.</span></span>

> [!NOTE]
> <span data-ttu-id="daf88-127">Hola las direcciones URL para los extremos de hello no deberían considerarse como constantes de larga duración.</span><span class="sxs-lookup"><span data-stu-id="daf88-127">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="daf88-128">servicio de Hello puede actualizarlos en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="daf88-128">hello service may update these at any point.</span></span> <span data-ttu-id="daf88-129">Hola SDK controla automáticamente este cambio.</span><span class="sxs-lookup"><span data-stu-id="daf88-129">hello SDK handles this change automatically.</span></span>
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

// connect tooAzure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

<span data-ttu-id="daf88-130">De este modo finaliza este tutorial.</span><span class="sxs-lookup"><span data-stu-id="daf88-130">That's it, that completes this tutorial.</span></span> <span data-ttu-id="daf88-131">Obtener información sobre cómo toomanage Hola coherencia de la cuenta replicada a nivel mundial leyendo [niveles de coherencia en la base de datos de Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="daf88-131">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="daf88-132">Para más información sobre cómo funciona la replicación global de bases de datos en Azure Cosmos DB, consulte [Distribución global de datos con Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="daf88-132">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="daf88-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="daf88-133">Next steps</span></span>

<span data-ttu-id="daf88-134">En este tutorial, ha hecho siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="daf88-134">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="daf88-135">Configure la distribución global con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="daf88-135">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="daf88-136">Configure la distribución global con hello DocumentDB APIs</span><span class="sxs-lookup"><span data-stu-id="daf88-136">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="daf88-137">Ahora puede continuar toohello siguiente tutorial toolearn cómo toodevelop localmente mediante Hola emulador local de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="daf88-137">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="daf88-138">Desarrollar localmente con el emulador de Hola</span><span class="sxs-lookup"><span data-stu-id="daf88-138">Develop locally with hello emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

