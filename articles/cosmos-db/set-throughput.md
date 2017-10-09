---
title: rendimiento de aaaProvision de base de datos de Azure Cosmos | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooset había aprovisionado containsers, colecciones, gráficos y tablas de base de datos de Azure Cosmos para el rendimiento."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f98def7f-f012-4592-be03-f6fa185e1b1e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: mimig
ms.openlocfilehash: c143f4aace466b7109168a50e2eb80ddeca6400e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a><span data-ttu-id="353c2-103">Configuración del rendimiento para contenedores de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="353c2-103">Set throughput for Azure Cosmos DB containers</span></span>

<span data-ttu-id="353c2-104">Puede configurar rendimiento para los contenedores de la base de datos de Azure Cosmos Hola portal de Azure o mediante el uso de Hola SDK de cliente.</span><span class="sxs-lookup"><span data-stu-id="353c2-104">You can set throughput for your Azure Cosmos DB containers in hello Azure portal or by using hello client SDKs.</span></span> 

<span data-ttu-id="353c2-105">Hello en la tabla siguiente enumera rendimiento Hola disponible para los contenedores:</span><span class="sxs-lookup"><span data-stu-id="353c2-105">hello following table lists hello throughput available for containers:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="353c2-106"><strong>Contenedor de una única partición</strong></span><span class="sxs-lookup"><span data-stu-id="353c2-106"><strong>Single Partition Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="353c2-107"><strong>Contenedor con particiones</strong></span><span class="sxs-lookup"><span data-stu-id="353c2-107"><strong>Partitioned Container</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="353c2-108">Procesamiento mínimo</span><span class="sxs-lookup"><span data-stu-id="353c2-108">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="353c2-109">400 unidades de solicitud por segundo</span><span class="sxs-lookup"><span data-stu-id="353c2-109">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="353c2-110">2 500 unidades de solicitud por segundo</span><span class="sxs-lookup"><span data-stu-id="353c2-110">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="353c2-111">Procesamiento máximo</span><span class="sxs-lookup"><span data-stu-id="353c2-111">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="353c2-112">10 000 unidades de solicitud por segundo</span><span class="sxs-lookup"><span data-stu-id="353c2-112">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="353c2-113">Sin límite</span><span class="sxs-lookup"><span data-stu-id="353c2-113">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a><span data-ttu-id="353c2-114">rendimiento de hello tooset mediante el uso de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="353c2-114">tooset hello throughput by using hello Azure portal</span></span>

1. <span data-ttu-id="353c2-115">En una nueva ventana, abra hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="353c2-115">In a new window, open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="353c2-116">En la barra de la izquierda hello, haga clic en **base de datos de Azure Cosmos**, o haga clic en **más servicios** en la parte inferior de hello, a continuación, desplácese demasiado**bases de datos**y, a continuación, haga clic en **base de datos de Azure Cosmos**.</span><span class="sxs-lookup"><span data-stu-id="353c2-116">On hello left bar, click **Azure Cosmos DB**, or click **More Services** at hello bottom, then scroll too**Databases**, and then click **Azure Cosmos DB**.</span></span>
3. <span data-ttu-id="353c2-117">Seleccione la cuenta de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="353c2-117">Select your Cosmos DB account.</span></span>
4. <span data-ttu-id="353c2-118">En la ventana nueva hello, haga clic en **Explorador de datos (vista previa)** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="353c2-118">In hello new window, click **Data Explorer (Preview)** in hello navigation menu.</span></span>
5. <span data-ttu-id="353c2-119">En la ventana nueva Hola, expanda la base de datos y el contenedor y, a continuación, haga clic en **escala y configuración**.</span><span class="sxs-lookup"><span data-stu-id="353c2-119">In hello new window, expand your database and container and then click **Scale & Settings**.</span></span>
6. <span data-ttu-id="353c2-120">En la ventana nueva Hola escriba Hola nuevo valor de rendimiento en hello **rendimiento** cuadro y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="353c2-120">In hello new window, type hello new throughput value in hello **Throughput** box, and then click **Save**.</span></span>

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a><span data-ttu-id="353c2-121">rendimiento de hello tooset mediante el uso de hello API de documentos para .NET</span><span class="sxs-lookup"><span data-stu-id="353c2-121">tooset hello throughput by using hello DocumentDB API for .NET</span></span>

```C#
//Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput toohello new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a><span data-ttu-id="353c2-122">Preguntas más frecuentes sobre el rendimiento</span><span class="sxs-lookup"><span data-stu-id="353c2-122">Throughput FAQ</span></span>

<span data-ttu-id="353c2-123">**¿Puedo configurar a mi que no requiere herramientas de rendimiento de 400 RU/s?**</span><span class="sxs-lookup"><span data-stu-id="353c2-123">**Can I set my throughput tooless than 400 RU/s?**</span></span>

<span data-ttu-id="353c2-124">400 RU/s es el rendimiento mínimo de hello disponible en las recopilaciones de una sola partición de base de datos de Cosmos (2500 RU/s es hello mínima para las colecciones particionadas).</span><span class="sxs-lookup"><span data-stu-id="353c2-124">400 RU/s is hello minimum throughput available on Cosmos DB single partition collections (2500 RU/s is hello minimum for partitioned collections).</span></span> <span data-ttu-id="353c2-125">Solicitar unidades se establecen en intervalos de 100 RU/s, pero el rendimiento no se puede establecer too100 RU/s o cualquier valor menor que 400 RU/s..</span><span class="sxs-lookup"><span data-stu-id="353c2-125">Request units are set in 100 RU/s intervals, but throughput cannot be set too100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="353c2-126">Si está buscando un método rentable toodevelop y probar la base de datos de Cosmos, puede usar hello libre [emulador de base de datos de Azure Cosmos](local-emulator.md), que puede implementar localmente sin costo alguno.</span><span class="sxs-lookup"><span data-stu-id="353c2-126">If you're looking for a cost effective method toodevelop and test Cosmos DB, you can use hello free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span></span> 

<span data-ttu-id="353c2-127">**¿Cómo se configura througput con hello MongoDB API?**</span><span class="sxs-lookup"><span data-stu-id="353c2-127">**How do I set througput using hello MongoDB API?**</span></span>

<span data-ttu-id="353c2-128">No hay ningún rendimiento tooset de extensión de API de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="353c2-128">There's no MongoDB API extension tooset throughput.</span></span> <span data-ttu-id="353c2-129">Hello recomendación es toouse hello API de documentos, como se muestra en [tooset el rendimiento de hello mediante el uso de hello API de documentos para .NET](#set-throughput-sdk).</span><span class="sxs-lookup"><span data-stu-id="353c2-129">hello recommendation is toouse hello DocumentDB API, as shown in [tooset hello throughput by using hello DocumentDB API for .NET](#set-throughput-sdk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="353c2-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="353c2-130">Next steps</span></span>

<span data-ttu-id="353c2-131">toolearn más información sobre el aprovisionamiento y escala planeta continuo con la base de datos de Cosmos, consulte [particiones y escalado con la base de datos de Cosmos](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="353c2-131">toolearn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span></span>
