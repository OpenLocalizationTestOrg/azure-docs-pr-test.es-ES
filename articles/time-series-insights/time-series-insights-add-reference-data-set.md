---
title: "Incorporación de un conjunto de datos de referencia al entorno de Azure Time Series Insights | Microsoft Docs"
description: En este tutorial, se agrega un conjunto de datos de referencia al entorno de Time Series Insights
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
ms.openlocfilehash: 23444297b5231e6a026bcd9ce3ee9f943bf05867
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-the-ibiza-portal"></a><span data-ttu-id="bbf49-103">Creación de un conjunto de datos de referencia para el entorno de Time Series Insights mediante el portal Ibiza</span><span class="sxs-lookup"><span data-stu-id="bbf49-103">Create a reference data set for your Time Series Insights environment using the Ibiza portal</span></span>

<span data-ttu-id="bbf49-104">Un conjunto de datos de referencia es una colección de elementos que aumentan con los eventos de un origen de eventos.</span><span class="sxs-lookup"><span data-stu-id="bbf49-104">A Reference Data Set is a collection of items that are augmented with the events from your event source.</span></span> <span data-ttu-id="bbf49-105">El motor de entrada de Time Series Insights une a un evento del origen de eventos con un elemento en el conjunto de datos de referencia.</span><span class="sxs-lookup"><span data-stu-id="bbf49-105">Time Series Insights ingress engine joins an event from your event source with an item in your reference data set.</span></span> <span data-ttu-id="bbf49-106">A partir de ese momento, este evento aumentado está disponible para consultas.</span><span class="sxs-lookup"><span data-stu-id="bbf49-106">This augmented event is then available for query.</span></span> <span data-ttu-id="bbf49-107">Esta combinación se basa en las claves definidas en el conjunto de datos de referencia.</span><span class="sxs-lookup"><span data-stu-id="bbf49-107">This join is based on the keys defined in your reference data set.</span></span>

## <a name="steps-to-add-a-reference-data-set-to-your-environment"></a><span data-ttu-id="bbf49-108">Pasos para agregar un conjunto de datos de referencia a un entorno</span><span class="sxs-lookup"><span data-stu-id="bbf49-108">Steps to add a reference data set to your environment</span></span>

1. <span data-ttu-id="bbf49-109">Inicie sesión en el [portal Ibiza](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bbf49-109">Sign in to the [Ibiza portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="bbf49-110">Haga clic en "Todos los recursos" en el menú izquierdo del portal Ibiza.</span><span class="sxs-lookup"><span data-stu-id="bbf49-110">Click “All resources” in the menu on the left side of the Ibiza portal.</span></span>
3. <span data-ttu-id="bbf49-111">Seleccione el entorno de Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="bbf49-111">Select your Time Series Insights environment.</span></span>

    ![Crear el conjunto de datos de referencia de Time Series Insights](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. <span data-ttu-id="bbf49-113">Seleccione "Conjuntos de datos de referencia" y haga clic en "+ Agregar".</span><span class="sxs-lookup"><span data-stu-id="bbf49-113">Select “Reference Data Sets”, click “+ Add.”</span></span>

    ![Crear el conjunto de datos de referencia de Time Series Insights (detalles)](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. <span data-ttu-id="bbf49-115">Especifique el nombre del conjunto de datos de referencia.</span><span class="sxs-lookup"><span data-stu-id="bbf49-115">Specify the name of the reference data set.</span></span>
6. <span data-ttu-id="bbf49-116">Especifique tanto el nombre de la clave como su tipo.</span><span class="sxs-lookup"><span data-stu-id="bbf49-116">Specify the key name and its type.</span></span> <span data-ttu-id="bbf49-117">Dichos nombre y el tipo se utilizan para elegir la propiedad correcta en el evento del origen de eventos.</span><span class="sxs-lookup"><span data-stu-id="bbf49-117">This name and type is used to pick the correct property from the event in your event source.</span></span> <span data-ttu-id="bbf49-118">Por ejemplo, si especifica el nombre de clave "DeviceId" y el tipo "Cadena", el motor de entrada de Time Series Insights busca una propiedad llamada "DeviceId" del tipo "Cadena" en el evento de entrada.</span><span class="sxs-lookup"><span data-stu-id="bbf49-118">For instance, if you provide key name as “DeviceId” and type as “String”, then the Time Series Insights ingress engine looks for a property with the name “DeviceId” of type “String” in the incoming event.</span></span> <span data-ttu-id="bbf49-119">Puede proporcionar más de una clave para realizar la combinación con el evento.</span><span class="sxs-lookup"><span data-stu-id="bbf49-119">You can provide more than one key to join with the event.</span></span> <span data-ttu-id="bbf49-120">La coincidencia del nombre de la propiedad distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="bbf49-120">The property name match is case-sensitive.</span></span>

     ![Crear el conjunto de datos de referencia de Time Series Insights (detalles)](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. <span data-ttu-id="bbf49-122">Haga clic en "Crear".</span><span class="sxs-lookup"><span data-stu-id="bbf49-122">Click “Create.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbf49-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bbf49-123">Next steps</span></span>

* <span data-ttu-id="bbf49-124">[Administración de datos de referencia](time-series-insights-manage-reference-data-csharp.md) mediante programación.</span><span class="sxs-lookup"><span data-stu-id="bbf49-124">[Manage reference data](time-series-insights-manage-reference-data-csharp.md) programmatically.</span></span>
* <span data-ttu-id="bbf49-125">Para obtener una referencia completa a la API, consulte el documento [API de datos de referencia](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api).</span><span class="sxs-lookup"><span data-stu-id="bbf49-125">For the complete API reference, see [Reference Data API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) document.</span></span>