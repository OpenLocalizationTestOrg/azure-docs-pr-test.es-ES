---
title: Aprovisionamiento del rendimiento de Azure Cosmos DB | Microsoft Docs
description: Aprenda a configurar el rendimiento aprovisionado para sus contenedores, colecciones, grafos y tablas de Azure Cosmos DB.
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
ms.openlocfilehash: d541bb19ba7e5ecb44c9fe91b1e232d4d9c2170e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a><span data-ttu-id="5018e-103">Configuración del rendimiento para contenedores de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5018e-103">Set throughput for Azure Cosmos DB containers</span></span>

<span data-ttu-id="5018e-104">Puede configurar el rendimiento de los contenedores de Azure Cosmos DB en Azure Portal o mediante los SDK del cliente.</span><span class="sxs-lookup"><span data-stu-id="5018e-104">You can set throughput for your Azure Cosmos DB containers in the Azure portal or by using the client SDKs.</span></span> 

<span data-ttu-id="5018e-105">En la tabla siguiente se enumeran los rendimientos disponibles para los contenedores:</span><span class="sxs-lookup"><span data-stu-id="5018e-105">The following table lists the throughput available for containers:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="5018e-106"><strong>Contenedor de una única partición</strong></span><span class="sxs-lookup"><span data-stu-id="5018e-106"><strong>Single Partition Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="5018e-107"><strong>Contenedor con particiones</strong></span><span class="sxs-lookup"><span data-stu-id="5018e-107"><strong>Partitioned Container</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="5018e-108">Procesamiento mínimo</span><span class="sxs-lookup"><span data-stu-id="5018e-108">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="5018e-109">400 unidades de solicitud por segundo</span><span class="sxs-lookup"><span data-stu-id="5018e-109">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="5018e-110">2 500 unidades de solicitud por segundo</span><span class="sxs-lookup"><span data-stu-id="5018e-110">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="5018e-111">Procesamiento máximo</span><span class="sxs-lookup"><span data-stu-id="5018e-111">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="5018e-112">10 000 unidades de solicitud por segundo</span><span class="sxs-lookup"><span data-stu-id="5018e-112">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="5018e-113">Sin límite</span><span class="sxs-lookup"><span data-stu-id="5018e-113">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

## <a name="to-set-the-throughput-by-using-the-azure-portal"></a><span data-ttu-id="5018e-114">Para establecer el rendimiento mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5018e-114">To set the throughput by using the Azure portal</span></span>

1. <span data-ttu-id="5018e-115">Abra [Azure Portal](https://portal.azure.com) en una nueva ventana.</span><span class="sxs-lookup"><span data-stu-id="5018e-115">In a new window, open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5018e-116">En la barra la izquierda, haga clic en **Azure Cosmos DB** o en **Más servicios**, en la parte inferior, desplácese a **Bases de datos** y, luego, haga clic en **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="5018e-116">On the left bar, click **Azure Cosmos DB**, or click **More Services** at the bottom, then scroll to **Databases**, and then click **Azure Cosmos DB**.</span></span>
3. <span data-ttu-id="5018e-117">Seleccione la cuenta de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5018e-117">Select your Cosmos DB account.</span></span>
4. <span data-ttu-id="5018e-118">En la nueva ventana, haga clic en **Explorador de datos (versión preliminar)** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="5018e-118">In the new window, click **Data Explorer (Preview)** in the navigation menu.</span></span>
5. <span data-ttu-id="5018e-119">En la nueva ventana, expanda la base de datos y el contenedor y, a continuación, haga clic en **Escala y configuración**.</span><span class="sxs-lookup"><span data-stu-id="5018e-119">In the new window, expand your database and container and then click **Scale & Settings**.</span></span>
6. <span data-ttu-id="5018e-120">En la nueva ventana, escriba el nuevo valor de rendimiento en el cuadro **Rendimiento** y luego haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="5018e-120">In the new window, type the new throughput value in the **Throughput** box, and then click **Save**.</span></span>

<a id="set-throughput-sdk"></a>

## <a name="to-set-the-throughput-by-using-the-documentdb-api-for-net"></a><span data-ttu-id="5018e-121">Configuración del rendimiento mediante la API de DocumentDB para .NET</span><span class="sxs-lookup"><span data-stu-id="5018e-121">To set the throughput by using the DocumentDB API for .NET</span></span>

```C#
//Fetch the resource to be updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to the new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a><span data-ttu-id="5018e-122">Preguntas más frecuentes sobre el rendimiento</span><span class="sxs-lookup"><span data-stu-id="5018e-122">Throughput FAQ</span></span>

<span data-ttu-id="5018e-123">**¿Se puede configurar el rendimiento a menos de 400 RU/s?**</span><span class="sxs-lookup"><span data-stu-id="5018e-123">**Can I set my throughput to less than 400 RU/s?**</span></span>

<span data-ttu-id="5018e-124">400 RU/s es el rendimiento mínimo disponible en las recopilaciones de una sola partición de Cosmos DB (2500 RU/s es el valor mínimo para las colecciones particionadas).</span><span class="sxs-lookup"><span data-stu-id="5018e-124">400 RU/s is the minimum throughput available on Cosmos DB single partition collections (2500 RU/s is the minimum for partitioned collections).</span></span> <span data-ttu-id="5018e-125">Las unidades de solicitud se establecen en intervalos de 100 RU/s pero el rendimiento no se puede establecer en 100 RU/s o en ningún valor inferior a 400 RU/s.</span><span class="sxs-lookup"><span data-stu-id="5018e-125">Request units are set in 100 RU/s intervals, but throughput cannot be set to 100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="5018e-126">Si está buscando un método rentable para desarrollar y probar Cosmos DB, puede usar gratuitamente el [Emulador de Azure Cosmos DB](local-emulator.md), que puede implementar localmente sin costo alguno.</span><span class="sxs-lookup"><span data-stu-id="5018e-126">If you're looking for a cost effective method to develop and test Cosmos DB, you can use the free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span></span> 

<span data-ttu-id="5018e-127">**¿Cómo se configura el rendimiento mediante la API de MongoDB?**</span><span class="sxs-lookup"><span data-stu-id="5018e-127">**How do I set througput using the MongoDB API?**</span></span>

<span data-ttu-id="5018e-128">No hay ninguna extensión de API de MongoDB para configurar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="5018e-128">There's no MongoDB API extension to set throughput.</span></span> <span data-ttu-id="5018e-129">La recomendación es utilizar la API de DocumentDB, como se muestra en [Configuración del rendimiento mediante la API de DocumentDB para .NET](#set-throughput-sdk).</span><span class="sxs-lookup"><span data-stu-id="5018e-129">The recommendation is to use the DocumentDB API, as shown in [To set the throughput by using the DocumentDB API for .NET](#set-throughput-sdk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5018e-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5018e-130">Next steps</span></span>

<span data-ttu-id="5018e-131">Para aprender más sobre el aprovisionamiento y cómo pasar a escala planetaria con Cosmos DB, consulte [Partición y escalado en Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="5018e-131">To learn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span></span>
