---
title: "tutorial de distribución global de Cosmos DB aaaAzure de API de MongoDB | Documentos de Microsoft"
description: "Obtenga información acerca de cómo usar de distribución global de base de datos de Azure Cosmos toosetup Hola API de MongoDB."
services: cosmos-db
keywords: "distribución global, MongoDB"
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 0fc2d670bb4e21ac5f813f9586b407ba06ccf354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-mongodb-api"></a><span data-ttu-id="be253-104">Cómo usar de distribución global de base de datos de Azure Cosmos toosetup Hola API de MongoDB</span><span class="sxs-lookup"><span data-stu-id="be253-104">How toosetup Azure Cosmos DB global distribution using hello MongoDB API</span></span>

<span data-ttu-id="be253-105">En este artículo, le mostramos cómo toouse Hola toosetup portal Azure distribución global de base de datos de Azure Cosmos y, a continuación, conectarse mediante la API de MongoDB Hola.</span><span class="sxs-lookup"><span data-stu-id="be253-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello MongoDB API.</span></span>

<span data-ttu-id="be253-106">En este artículo se trata Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="be253-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="be253-107">Configure la distribución global con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="be253-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="be253-108">Configure la distribución global con hello [API de MongoDB](mongodb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="be253-108">Configure global distribution using hello [MongoDB API](mongodb-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-hello-mongodb-api"></a><span data-ttu-id="be253-109">Comprobar la configuración regional mediante la API de MongoDB Hola</span><span class="sxs-lookup"><span data-stu-id="be253-109">Verifying your regional setup using hello MongoDB API</span></span>
<span data-ttu-id="be253-110">la manera más sencilla de Hola de doble comprobando su configuración global dentro de la API de MongoDB es hello toorun *isMaster()* comando de Shell de Mongo Hola.</span><span class="sxs-lookup"><span data-stu-id="be253-110">hello simplest way of double checking your global configuration within API for MongoDB is toorun hello *isMaster()* command from hello Mongo Shell.</span></span>

<span data-ttu-id="be253-111">Desde el Shell de Mongo:</span><span class="sxs-lookup"><span data-stu-id="be253-111">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="be253-112">Resultados de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="be253-112">Example results:</span></span>

   ```JSON
      {
         "_t": "IsMasterResponse",
         "ok": 1,
         "ismaster": true,
         "maxMessageSizeBytes": 4194304,
         "maxWriteBatchSize": 1000,
         "minWireVersion": 0,
         "maxWireVersion": 2,
         "tags": {
            "region": "South India"
         },
         "hosts": [
            "vishi-api-for-mongodb-southcentralus.documents.azure.com:10255",
            "vishi-api-for-mongodb-westeurope.documents.azure.com:10255",
            "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
         ],
         "setName": "globaldb",
         "setVersion": 1,
         "primary": "vishi-api-for-mongodb-southindia.documents.azure.com:10255",
         "me": "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
      }
   ```

## <a name="connecting-tooa-preferred-region-using-hello-mongodb-api"></a><span data-ttu-id="be253-113">Conexión tooa región preferida mediante Hola API de MongoDB</span><span class="sxs-lookup"><span data-stu-id="be253-113">Connecting tooa preferred region using hello MongoDB API</span></span>

<span data-ttu-id="be253-114">Hola MongoDB API permite toospecify preferencias de lectura de la colección para una base de datos distribuido globalmente.</span><span class="sxs-lookup"><span data-stu-id="be253-114">hello MongoDB API enables you toospecify your collection's read preference for a globally distributed database.</span></span> <span data-ttu-id="be253-115">Para ambos bajo Lecturas de latencia y alta disponibilidad global, se recomienda establecer preferencias de lectura de la colección demasiado*más cercano*.</span><span class="sxs-lookup"><span data-stu-id="be253-115">For both low latency reads and global high availability, we recommend setting your collection's read preference too*nearest*.</span></span> <span data-ttu-id="be253-116">Una preferencia de lectura de *más cercano* es tooread configurado de la región más cercana de Hola.</span><span class="sxs-lookup"><span data-stu-id="be253-116">A read preference of *nearest* is configured tooread from hello closest region.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

<span data-ttu-id="be253-117">Para las aplicaciones con un elemento principal de lectura/escritura región y una región secundaria para la recuperación ante desastres (DR) escenarios, se recomienda establecer preferencias de lectura de la colección demasiado*secundaria preferido*.</span><span class="sxs-lookup"><span data-stu-id="be253-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference too*secondary preferred*.</span></span> <span data-ttu-id="be253-118">Una preferencia de lectura de *secundaria preferido* resulta tooread configurado de la región secundaria Hola región principal de hello no está disponible.</span><span class="sxs-lookup"><span data-stu-id="be253-118">A read preference of *secondary preferred* is configured tooread from hello secondary region when hello primary region is unavailable.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

<span data-ttu-id="be253-119">Por último, si como toomanually especificaría las regiones de lectura.</span><span class="sxs-lookup"><span data-stu-id="be253-119">Lastly, if you would like toomanually specify your read regions.</span></span> <span data-ttu-id="be253-120">Para establecer la región de hello etiqueta dentro de sus preferencias de lectura.</span><span class="sxs-lookup"><span data-stu-id="be253-120">You can set hello region Tag within your read preference.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

<span data-ttu-id="be253-121">De este modo finaliza este tutorial.</span><span class="sxs-lookup"><span data-stu-id="be253-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="be253-122">Obtener información sobre cómo toomanage Hola coherencia de la cuenta replicada a nivel mundial leyendo [niveles de coherencia en la base de datos de Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="be253-122">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="be253-123">Para más información sobre cómo funciona la replicación global de bases de datos en Azure Cosmos DB, consulte [Distribución global de datos con Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="be253-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="be253-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="be253-124">Next steps</span></span>

<span data-ttu-id="be253-125">En este tutorial, ha hecho siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="be253-125">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="be253-126">Configure la distribución global con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="be253-126">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="be253-127">Configure la distribución global con hello DocumentDB APIs</span><span class="sxs-lookup"><span data-stu-id="be253-127">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="be253-128">Ahora puede continuar toohello siguiente tutorial toolearn cómo toodevelop localmente mediante Hola emulador local de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="be253-128">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="be253-129">Desarrollar localmente con el emulador de Hola</span><span class="sxs-lookup"><span data-stu-id="be253-129">Develop locally with hello emulator</span></span>](local-emulator.md)
