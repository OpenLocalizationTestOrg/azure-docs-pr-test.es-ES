---
title: "Tutorial de distribución global de Azure Cosmos DB para la API de MongoDB | Microsoft Docs"
description: "Obtenga información sobre cómo configurar la distribución global de Azure Cosmos DB con la API de MongoDB."
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
ms.openlocfilehash: a2747102f4d8cac412b67abc3fd07cfa3661bcee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-mongodb-api"></a><span data-ttu-id="d9934-104">Configuración de la distribución global de Azure Cosmos DB con la API de MongoDB</span><span class="sxs-lookup"><span data-stu-id="d9934-104">How to setup Azure Cosmos DB global distribution using the MongoDB API</span></span>

<span data-ttu-id="d9934-105">En este artículo se muestra cómo usar Azure Portal para configurar la distribución global de Azure Cosmos DB y luego conectarse con la API de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d9934-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the MongoDB API.</span></span>

<span data-ttu-id="d9934-106">En este artículo se tratan las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="d9934-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="d9934-107">Configuración de la distribución global con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d9934-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="d9934-108">Configuración de la distribución global con la [API de MongoDB](mongodb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="d9934-108">Configure global distribution using the [MongoDB API](mongodb-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-the-mongodb-api"></a><span data-ttu-id="d9934-109">Comprobación de la configuración regional con la API de MongoDB</span><span class="sxs-lookup"><span data-stu-id="d9934-109">Verifying your regional setup using the MongoDB API</span></span>
<span data-ttu-id="d9934-110">La manera más sencilla de comprobar la configuración global dentro de la API de MongoDB es ejecutar el comando *isMaster()* desde el Shell de Mongo.</span><span class="sxs-lookup"><span data-stu-id="d9934-110">The simplest way of double checking your global configuration within API for MongoDB is to run the *isMaster()* command from the Mongo Shell.</span></span>

<span data-ttu-id="d9934-111">Desde el Shell de Mongo:</span><span class="sxs-lookup"><span data-stu-id="d9934-111">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="d9934-112">Resultados de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d9934-112">Example results:</span></span>

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

## <a name="connecting-to-a-preferred-region-using-the-mongodb-api"></a><span data-ttu-id="d9934-113">Conexión a una región de preferencia con la API de MongoDB</span><span class="sxs-lookup"><span data-stu-id="d9934-113">Connecting to a preferred region using the MongoDB API</span></span>

<span data-ttu-id="d9934-114">La API de MongoDB permite especificar preferencias de lectura de la colección para una base de datos distribuida globalmente.</span><span class="sxs-lookup"><span data-stu-id="d9934-114">The MongoDB API enables you to specify your collection's read preference for a globally distributed database.</span></span> <span data-ttu-id="d9934-115">Para lecturas de poca latencia y alta disponibilidad global, se recomienda establecer las preferencias de lectura de la colección en *más cercano*.</span><span class="sxs-lookup"><span data-stu-id="d9934-115">For both low latency reads and global high availability, we recommend setting your collection's read preference to *nearest*.</span></span> <span data-ttu-id="d9934-116">Una preferencia de lectura de *más cercano* está configurada para leer desde la región más cercana.</span><span class="sxs-lookup"><span data-stu-id="d9934-116">A read preference of *nearest* is configured to read from the closest region.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

<span data-ttu-id="d9934-117">Para las aplicaciones con una región de lectura/escritura principal y una secundaria para escenarios de recuperación ante desastres, se recomienda establecer preferencias de lectura de la colección en *secundaria preferida*.</span><span class="sxs-lookup"><span data-stu-id="d9934-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference to *secondary preferred*.</span></span> <span data-ttu-id="d9934-118">Una preferencia de lectura de *secundaria preferida* está configurado para leer desde la región secundaria cuando la región principal no está disponible.</span><span class="sxs-lookup"><span data-stu-id="d9934-118">A read preference of *secondary preferred* is configured to read from the secondary region when the primary region is unavailable.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

<span data-ttu-id="d9934-119">Por último, si quiere hacerlo manualmente, especifique las áreas de lectura.</span><span class="sxs-lookup"><span data-stu-id="d9934-119">Lastly, if you would like to manually specify your read regions.</span></span> <span data-ttu-id="d9934-120">Puede establecer la etiqueta de región dentro de sus preferencias de lectura.</span><span class="sxs-lookup"><span data-stu-id="d9934-120">You can set the region Tag within your read preference.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

<span data-ttu-id="d9934-121">De este modo finaliza este tutorial.</span><span class="sxs-lookup"><span data-stu-id="d9934-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="d9934-122">Para información sobre cómo administrar la coherencia de la cuenta replicada globalmente, lea [Niveles de coherencia en Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="d9934-122">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="d9934-123">Para más información sobre cómo funciona la replicación global de bases de datos en Azure Cosmos DB, consulte [Distribución global de datos con Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="d9934-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9934-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d9934-124">Next steps</span></span>

<span data-ttu-id="d9934-125">En este tutorial, ha hecho lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d9934-125">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d9934-126">Configuración de la distribución global con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d9934-126">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="d9934-127">Configuración de la distribución global con las API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="d9934-127">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="d9934-128">Ahora puede continuar en el tutorial siguiente para aprender a desarrollar localmente con el emulador local de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d9934-128">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d9934-129">Desarrollo local con el emulador</span><span class="sxs-lookup"><span data-stu-id="d9934-129">Develop locally with the emulator</span></span>](local-emulator.md)