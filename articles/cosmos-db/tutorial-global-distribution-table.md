---
title: "Tutorial de distribución global de Azure Cosmos DB para Table API | Microsoft Docs"
description: "Obtenga información sobre cómo configurar la distribución global de Azure Cosmos DB con Table API."
services: cosmos-db
keywords: "distribución global, Table"
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
ms.openlocfilehash: 63c9e530a4982e2e6e478fea56e015fc77851e1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-table-api"></a><span data-ttu-id="12f8e-104">Configuración de la distribución global de Azure Cosmos DB con Table API</span><span class="sxs-lookup"><span data-stu-id="12f8e-104">How to setup Azure Cosmos DB global distribution using the Table API</span></span>

<span data-ttu-id="12f8e-105">En este artículo se muestra cómo usar Azure Portal para configurar la distribución global de Azure Cosmos DB y luego conectarse con Table API (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="12f8e-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the Table API (preview).</span></span>

<span data-ttu-id="12f8e-106">En este artículo se tratan las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="12f8e-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="12f8e-107">Configuración de la distribución global con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="12f8e-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="12f8e-108">Configuración de la distribución global con [Table API](table-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="12f8e-108">Configure global distribution using the [Table API](table-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-table-api"></a><span data-ttu-id="12f8e-109">Conexión a una región de preferencia con Table API</span><span class="sxs-lookup"><span data-stu-id="12f8e-109">Connecting to a preferred region using the Table API</span></span>

<span data-ttu-id="12f8e-110">Para aprovechar las ventajas de la [distribución global](distribute-data-globally.md), las aplicaciones cliente pueden especificar la lista del orden de preferencia de regiones que se usará para llevar a cabo operaciones de documentos.</span><span class="sxs-lookup"><span data-stu-id="12f8e-110">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="12f8e-111">Esto puede hacerse estableciendo el valor de configuración `TablePreferredLocations` en la configuración de aplicación para el SDK de versión preliminar de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="12f8e-111">This can be done by setting the `TablePreferredLocations` configuration value in the app config for the preview Azure Storage SDK.</span></span> <span data-ttu-id="12f8e-112">Según la configuración de la cuenta de Azure Cosmos DB, la disponibilidad regional actual y la lista de preferencias especificada, el SDK de Azure Storage elegirá el punto de conexión óptimo para realizar las operaciones de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="12f8e-112">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the Azure Storage SDK to perform write and read operations.</span></span>

<span data-ttu-id="12f8e-113">`TablePreferredLocations` debe contener una lista separada por comas de las ubicaciones preferidas (hospedaje múltiple) para las lecturas.</span><span class="sxs-lookup"><span data-stu-id="12f8e-113">The `TablePreferredLocations` should contain a comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="12f8e-114">Cada instancia de cliente puede especificar un subconjunto de estas regiones en el orden de preferencia para las lecturas de latencia baja.</span><span class="sxs-lookup"><span data-stu-id="12f8e-114">Each client instance can specify a subset of these regions in the preferred order for low latency reads.</span></span> <span data-ttu-id="12f8e-115">Estas regiones se deben denominar según sus [nombres para mostrar](https://msdn.microsoft.com/library/azure/gg441293.aspx), por ejemplo, `West US`.</span><span class="sxs-lookup"><span data-stu-id="12f8e-115">The regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span>

<span data-ttu-id="12f8e-116">Todas las lecturas se enviarán a la primera región disponible en la lista `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="12f8e-116">All reads will be sent to the first available region in the `TablePreferredLocations` list.</span></span> <span data-ttu-id="12f8e-117">Si se produce un error en la solicitud, el cliente pasará a la siguiente región de la lista y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="12f8e-117">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="12f8e-118">El SDK solo intentará leer en las regiones especificadas en `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="12f8e-118">The SDK will only attempt to read from the regions specified in `TablePreferredLocations`.</span></span> <span data-ttu-id="12f8e-119">Así que, por ejemplo, si la cuenta de base de datos está disponible en tres regiones, pero el cliente solo especifica dos de las regiones de no escritura para `TablePreferredLocations`, no se atenderá ninguna lectura desde la región de escritura, incluso en caso de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="12f8e-119">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for `TablePreferredLocations`, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="12f8e-120">El SDK enviará automáticamente todas las escrituras a la región de escritura actual.</span><span class="sxs-lookup"><span data-stu-id="12f8e-120">The SDK will automatically send all writes to the current write region.</span></span>

<span data-ttu-id="12f8e-121">Si la propiedad `TablePreferredLocations` no está establecida, atenderá todas las solicitudes procedentes de la región de escritura actual.</span><span class="sxs-lookup"><span data-stu-id="12f8e-121">If the `TablePreferredLocations` property is not set, all requests will be served from the current write region.</span></span>

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

<span data-ttu-id="12f8e-122">De este modo finaliza este tutorial.</span><span class="sxs-lookup"><span data-stu-id="12f8e-122">That's it, that completes this tutorial.</span></span> <span data-ttu-id="12f8e-123">Para información sobre cómo administrar la coherencia de la cuenta replicada globalmente, lea [Niveles de coherencia en Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="12f8e-123">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="12f8e-124">Para más información sobre cómo funciona la replicación global de bases de datos en Azure Cosmos DB, consulte [Distribución global de datos con Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="12f8e-124">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="12f8e-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="12f8e-125">Next steps</span></span>

<span data-ttu-id="12f8e-126">En este tutorial, ha hecho lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="12f8e-126">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="12f8e-127">Configuración de la distribución global con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="12f8e-127">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="12f8e-128">Configuración de la distribución global con las API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="12f8e-128">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="12f8e-129">Ahora puede continuar en el tutorial siguiente para aprender a desarrollar localmente con el emulador local de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="12f8e-129">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="12f8e-130">Desarrollo local con el emulador</span><span class="sxs-lookup"><span data-stu-id="12f8e-130">Develop locally with the emulator</span></span>](local-emulator.md)