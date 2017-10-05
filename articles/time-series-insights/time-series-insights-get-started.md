---
title: "Creación de un entorno de Azure Time Series Insights | Microsoft Docs"
description: "En este tutorial, aprenderá a crear un entorno de Time Series Insights, conectarse a un origen de eventos y estar listo para analizar los datos del evento en minutos."
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: eb710795916a2d7beea75a6408a0982fb4dc8750
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-new-time-series-insights-environment-in-the-azure-portal"></a><span data-ttu-id="664c0-103">Creación de un nuevo entorno de Time Series Insights en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="664c0-103">Create a new Time Series Insights environment in the Azure portal</span></span>

<span data-ttu-id="664c0-104">Un entorno de Time Series Insights es un recurso de Azure con funcionalidades de incorporación y almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="664c0-104">Time Series Insights environment is an Azure resource with ingress and storage capacity.</span></span> <span data-ttu-id="664c0-105">Los clientes aprovisionan los entornos mediante Azure Portal con la capacidad necesaria.</span><span class="sxs-lookup"><span data-stu-id="664c0-105">Customers provision environments via the Azure portal with the required capacity.</span></span>

## <a name="steps-to-create-the-environment"></a><span data-ttu-id="664c0-106">Pasos para crear el entorno</span><span class="sxs-lookup"><span data-stu-id="664c0-106">Steps to create the environment</span></span>

<span data-ttu-id="664c0-107">Siga estos pasos para crear el entorno:</span><span class="sxs-lookup"><span data-stu-id="664c0-107">Follow these steps to create your environment:</span></span>

1.  <span data-ttu-id="664c0-108">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="664c0-108">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="664c0-109">Haga clic en el signo más ("+") en la esquina superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="664c0-109">Click the plus sign (“+”) in the top left corner.</span></span>
3.  <span data-ttu-id="664c0-110">Busque "Time Series Insights" en el cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="664c0-110">Search for “Time Series Insights” in the search box.</span></span>

  ![Creación del entorno de Time Series Insights](media/get-started/getstarted-create-environment1.png)

4.  <span data-ttu-id="664c0-112">Seleccione "Time Series Insights" y haga clic en "Crear".</span><span class="sxs-lookup"><span data-stu-id="664c0-112">Select “Time Series Insights”, click “Create”.</span></span>

  ![Creación del grupo de recursos de Time Series Insights](media/get-started/getstarted-create-environment2.png)

5.  <span data-ttu-id="664c0-114">Especifique el nombre del entorno.</span><span class="sxs-lookup"><span data-stu-id="664c0-114">Specify environment name.</span></span> <span data-ttu-id="664c0-115">Este nombre representará al entorno en el [explorador de Time Series Insights](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="664c0-115">This name will represent the environment in [time series explorer](https://insights.timeseries.azure.com).</span></span>
6.  <span data-ttu-id="664c0-116">Seleccione una suscripción.</span><span class="sxs-lookup"><span data-stu-id="664c0-116">Select a subscription.</span></span> <span data-ttu-id="664c0-117">Elija una que contenga el origen de eventos.</span><span class="sxs-lookup"><span data-stu-id="664c0-117">Choose one that contains your event source.</span></span> <span data-ttu-id="664c0-118">Time Series Insights puede detectar automáticamente los recursos de Azure IoT Hub y Event Hubs existentes en la misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="664c0-118">Time Series Insights can auto-detect Azure IoT Hub and Event Hub resources existing in the same subscription.</span></span>
7.  <span data-ttu-id="664c0-119">Seleccione o cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="664c0-119">Select or create a resource group.</span></span> <span data-ttu-id="664c0-120">Un grupo de recursos es una colección de recursos de Azure que se usan juntos.</span><span class="sxs-lookup"><span data-stu-id="664c0-120">A resource group is a collection of Azure resources used together.</span></span>
8.  <span data-ttu-id="664c0-121">Selección de una ubicación de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="664c0-121">Select a hosting location.</span></span> <span data-ttu-id="664c0-122">Para evitar mover datos entre centros de datos, elija la ubicación que contiene el origen de eventos.</span><span class="sxs-lookup"><span data-stu-id="664c0-122">To avoid moving data across data centers, choose location that contains your event source.</span></span>
9.  <span data-ttu-id="664c0-123">Seleccione un plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="664c0-123">Select a pricing tier.</span></span>
10. <span data-ttu-id="664c0-124">Seleccione la capacidad.</span><span class="sxs-lookup"><span data-stu-id="664c0-124">Select capacity.</span></span> <span data-ttu-id="664c0-125">Puede cambiar la capacidad de un entorno después de su creación.</span><span class="sxs-lookup"><span data-stu-id="664c0-125">You can change capacity of an environment after creation.</span></span>
11. <span data-ttu-id="664c0-126">Cree el entorno.</span><span class="sxs-lookup"><span data-stu-id="664c0-126">Create your environment.</span></span> <span data-ttu-id="664c0-127">También puede anclar el entorno en el panel para facilitar el acceso siempre que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="664c0-127">You can also pin your environment to the dashboard for easy access whenever you sign in.</span></span>

  ![Anclaje de Time Series Insights al panel](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a><span data-ttu-id="664c0-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="664c0-129">Next steps</span></span>

* <span data-ttu-id="664c0-130">[Definición de las directivas de acceso de datos](time-series-insights-data-access.md) para tener acceso al entorno en el [portal de Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="664c0-130">[Define data access policies](time-series-insights-data-access.md) to access your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
* [<span data-ttu-id="664c0-131">Creación de un origen de eventos</span><span class="sxs-lookup"><span data-stu-id="664c0-131">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="664c0-132">[Envío de eventos](time-series-insights-send-events.md) al origen de eventos</span><span class="sxs-lookup"><span data-stu-id="664c0-132">[Send events](time-series-insights-send-events.md) to the event source</span></span>
