---
title: "tutorial de distribución global de Cosmos DB aaaAzure de API de tabla | Documentos de Microsoft"
description: "Obtenga información acerca de cómo usar de distribución global de base de datos de Azure Cosmos toosetup Hola API de tabla."
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
ms.openlocfilehash: d2a995e09c37f9449856aef2ab707e95eb8a540c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-table-api"></a><span data-ttu-id="23410-104">Cómo usar de distribución global de base de datos de Azure Cosmos toosetup Hola API de tabla</span><span class="sxs-lookup"><span data-stu-id="23410-104">How toosetup Azure Cosmos DB global distribution using hello Table API</span></span>

<span data-ttu-id="23410-105">En este artículo, le mostramos cómo toouse Hola distribución global de base de datos de Azure Cosmos toosetup de portal de Azure y, a continuación, conectarse con hello API de tabla (vista previa).</span><span class="sxs-lookup"><span data-stu-id="23410-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello Table API (preview).</span></span>

<span data-ttu-id="23410-106">En este artículo se trata Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="23410-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="23410-107">Configure la distribución global con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="23410-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="23410-108">Configure la distribución global con hello [API de tabla](table-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="23410-108">Configure global distribution using hello [Table API](table-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-table-api"></a><span data-ttu-id="23410-109">Conexión tooa región preferida mediante Hola API de tabla</span><span class="sxs-lookup"><span data-stu-id="23410-109">Connecting tooa preferred region using hello Table API</span></span>

<span data-ttu-id="23410-110">En orden tootake aprovechar [distribución global](distribute-data-globally.md), pueden especificar las aplicaciones cliente hello ordenada la lista de preferencias de regiones toobe usa operaciones de documento tooperform.</span><span class="sxs-lookup"><span data-stu-id="23410-110">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="23410-111">Esto puede hacerse por establecer hello `TablePreferredLocations` valor de configuración en la configuración de aplicación hello para la vista previa de hello SDK de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="23410-111">This can be done by setting hello `TablePreferredLocations` configuration value in hello app config for hello preview Azure Storage SDK.</span></span> <span data-ttu-id="23410-112">En función de la configuración de cuenta de base de datos de Azure Cosmos hello, disponibilidad regional actual y ha especificado, la lista de preferencias Hola Hola mayoría extremo óptimo se elegirá por tooperform del SDK de almacenamiento de Azure de hello escribir y las operaciones de lectura.</span><span class="sxs-lookup"><span data-stu-id="23410-112">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello Azure Storage SDK tooperform write and read operations.</span></span>

<span data-ttu-id="23410-113">Hola `TablePreferredLocations` debe contener una lista separada por comas de ubicaciones (hospedaje múltiple) preferidos para las lecturas.</span><span class="sxs-lookup"><span data-stu-id="23410-113">hello `TablePreferredLocations` should contain a comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="23410-114">Cada instancia del cliente puede especificar un subconjunto de estas regiones en orden de hello preferido para las lecturas de latencia baja.</span><span class="sxs-lookup"><span data-stu-id="23410-114">Each client instance can specify a subset of these regions in hello preferred order for low latency reads.</span></span> <span data-ttu-id="23410-115">regiones de Hello deben denominarse mediante sus [nombres para mostrar](https://msdn.microsoft.com/library/azure/gg441293.aspx), por ejemplo, `West US`.</span><span class="sxs-lookup"><span data-stu-id="23410-115">hello regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span>

<span data-ttu-id="23410-116">Todas las lecturas se enviarán toohello primera región disponible en hello `TablePreferredLocations` lista.</span><span class="sxs-lookup"><span data-stu-id="23410-116">All reads will be sent toohello first available region in hello `TablePreferredLocations` list.</span></span> <span data-ttu-id="23410-117">Si se produce un error en la solicitud de Hola, cliente hello producirá un error hacia abajo de la región de hello lista toohello siguiente y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="23410-117">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span>

<span data-ttu-id="23410-118">Hola SDK sólo intentará tooread de regiones de hello especificado en `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="23410-118">hello SDK will only attempt tooread from hello regions specified in `TablePreferredLocations`.</span></span> <span data-ttu-id="23410-119">Por lo tanto, por ejemplo, si Hola cuenta de base de datos está disponible en tres regiones, pero solo para cliente hello especifica dos de Hola regiones de escritura para `TablePreferredLocations`, a continuación, no se enviará ningún lecturas fuera del área de escritura de hello, incluso en caso de hello de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="23410-119">So, for example, if hello Database Account is available in three regions, but hello client only specifies two of hello non-write regions for `TablePreferredLocations`, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="23410-120">Hola SDK enviará automáticamente todas las escrituras toohello actual escritura región.</span><span class="sxs-lookup"><span data-stu-id="23410-120">hello SDK will automatically send all writes toohello current write region.</span></span>

<span data-ttu-id="23410-121">Si hello `TablePreferredLocations` propiedad no está establecida, todas las solicitudes se servirá de región de escritura actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="23410-121">If hello `TablePreferredLocations` property is not set, all requests will be served from hello current write region.</span></span>

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

<span data-ttu-id="23410-122">De este modo finaliza este tutorial.</span><span class="sxs-lookup"><span data-stu-id="23410-122">That's it, that completes this tutorial.</span></span> <span data-ttu-id="23410-123">Obtener información sobre cómo toomanage Hola coherencia de la cuenta replicada a nivel mundial leyendo [niveles de coherencia en la base de datos de Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="23410-123">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="23410-124">Para más información sobre cómo funciona la replicación global de bases de datos en Azure Cosmos DB, consulte [Distribución global de datos con Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="23410-124">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="23410-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="23410-125">Next steps</span></span>

<span data-ttu-id="23410-126">En este tutorial, ha hecho siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="23410-126">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="23410-127">Configure la distribución global con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="23410-127">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="23410-128">Configure la distribución global con hello DocumentDB APIs</span><span class="sxs-lookup"><span data-stu-id="23410-128">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="23410-129">Ahora puede continuar toohello siguiente tutorial toolearn cómo toodevelop localmente mediante Hola emulador local de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="23410-129">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="23410-130">Desarrollar localmente con el emulador de Hola</span><span class="sxs-lookup"><span data-stu-id="23410-130">Develop locally with hello emulator</span></span>](local-emulator.md)
