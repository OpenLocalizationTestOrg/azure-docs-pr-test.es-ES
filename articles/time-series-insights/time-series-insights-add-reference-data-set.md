---
title: "entorno de visión de serie de tiempo de Azure de tooyour del conjunto de datos de referencia de aaaAdd | Documentos de Microsoft"
description: "En este tutorial, agregará un entorno de visión de la serie de tiempo de tooyour de conjunto de datos de referencia"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 05e626ed81a22f2a8710b23a931ccd17c0f38ca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a><span data-ttu-id="19438-103">Crear un conjunto de datos de referencia para su entorno de visión de la serie de tiempo mediante este portal como Hola</span><span class="sxs-lookup"><span data-stu-id="19438-103">Create a reference data set for your Time Series Insights environment using hello Ibiza portal</span></span>

<span data-ttu-id="19438-104">Un conjunto de datos de referencia es una colección de elementos que se han aumentado con eventos de Hola desde el origen del evento.</span><span class="sxs-lookup"><span data-stu-id="19438-104">A Reference Data Set is a collection of items that are augmented with hello events from your event source.</span></span> <span data-ttu-id="19438-105">El motor de entrada de Time Series Insights une a un evento del origen de eventos con un elemento en el conjunto de datos de referencia.</span><span class="sxs-lookup"><span data-stu-id="19438-105">Time Series Insights ingress engine joins an event from your event source with an item in your reference data set.</span></span> <span data-ttu-id="19438-106">A partir de ese momento, este evento aumentado está disponible para consultas.</span><span class="sxs-lookup"><span data-stu-id="19438-106">This augmented event is then available for query.</span></span> <span data-ttu-id="19438-107">Esta combinación se basa en claves de hello definidas en el conjunto de datos de referencia.</span><span class="sxs-lookup"><span data-stu-id="19438-107">This join is based on hello keys defined in your reference data set.</span></span>

## <a name="steps-tooadd-a-reference-data-set-tooyour-environment"></a><span data-ttu-id="19438-108">Pasos tooadd un entorno de tooyour del conjunto de datos de referencia</span><span class="sxs-lookup"><span data-stu-id="19438-108">Steps tooadd a reference data set tooyour environment</span></span>

1. <span data-ttu-id="19438-109">Inicie sesión en toohello [este portal como](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="19438-109">Sign in toohello [Ibiza portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="19438-110">Haga clic en "Todos los recursos" en el menú izquierda Hola de este portal como Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="19438-110">Click “All resources” in hello menu on hello left side of hello Ibiza portal.</span></span>
3. <span data-ttu-id="19438-111">Seleccione el entorno de Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="19438-111">Select your Time Series Insights environment.</span></span>

    ![Crear conjunto de datos de referencia de hello visión de la serie de tiempo](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. <span data-ttu-id="19438-113">Seleccione "Conjuntos de datos de referencia" y haga clic en "+ Agregar".</span><span class="sxs-lookup"><span data-stu-id="19438-113">Select “Reference Data Sets”, click “+ Add.”</span></span>

    ![Crear conjunto de datos de referencia de visión de la serie de tiempo hello - detalles](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. <span data-ttu-id="19438-115">Especifique el nombre de Hola Hola referencia del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="19438-115">Specify hello name of hello reference data set.</span></span>
6. <span data-ttu-id="19438-116">Especifique el nombre de clave de Hola y su tipo.</span><span class="sxs-lookup"><span data-stu-id="19438-116">Specify hello key name and its type.</span></span> <span data-ttu-id="19438-117">Este nombre y el tipo es propiedad correcto de Hola de toopick usado del evento de hello en el origen del evento.</span><span class="sxs-lookup"><span data-stu-id="19438-117">This name and type is used toopick hello correct property from hello event in your event source.</span></span> <span data-ttu-id="19438-118">Por ejemplo, si proporciona el nombre de clave como "DeviceId" y el tipo como "String", a continuación, Hola visión de serie de tiempo de motor de entrada busca una propiedad con nombre hello "DeviceId" de tipo "String" en el evento de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="19438-118">For instance, if you provide key name as “DeviceId” and type as “String”, then hello Time Series Insights ingress engine looks for a property with hello name “DeviceId” of type “String” in hello incoming event.</span></span> <span data-ttu-id="19438-119">Puede proporcionar más de un toojoin clave con eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="19438-119">You can provide more than one key toojoin with hello event.</span></span> <span data-ttu-id="19438-120">coincidencia de nombre de propiedad de Hello distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="19438-120">hello property name match is case-sensitive.</span></span>

     ![Crear conjunto de datos de referencia de visión de la serie de tiempo hello - detalles](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. <span data-ttu-id="19438-122">Haga clic en "Crear".</span><span class="sxs-lookup"><span data-stu-id="19438-122">Click “Create.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="19438-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="19438-123">Next steps</span></span>

* <span data-ttu-id="19438-124">[Administración de datos de referencia](time-series-insights-manage-reference-data-csharp.md) mediante programación.</span><span class="sxs-lookup"><span data-stu-id="19438-124">[Manage reference data](time-series-insights-manage-reference-data-csharp.md) programmatically.</span></span>
* <span data-ttu-id="19438-125">Para la referencia de API completa de hello, consulte [API de datos de referencia](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) documento.</span><span class="sxs-lookup"><span data-stu-id="19438-125">For hello complete API reference, see [Reference Data API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) document.</span></span>
