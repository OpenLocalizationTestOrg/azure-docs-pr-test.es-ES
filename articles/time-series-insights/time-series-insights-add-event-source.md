---
title: "Incorporación de un origen de eventos al entorno de Azure Time Series Insights | Microsoft Docs"
description: En este tutorial, se conecta un origen de eventos al entorno de Time Series Insights
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
ms.openlocfilehash: ffa2eaf3680e68ac14aabf49b6308caeb173fd43
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-the-ibiza-portal"></a><span data-ttu-id="ec23a-103">Creación de un origen de eventos para el entorno de Time Series Insights mediante el portal Ibiza</span><span class="sxs-lookup"><span data-stu-id="ec23a-103">Create an event source for your Time Series Insights environment using the Ibiza portal</span></span>

<span data-ttu-id="ec23a-104">El origen de eventos de Time Series Insights se deriva de un agente de eventos, como Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="ec23a-104">Time Series Insights Event Source is derived from an event broker, like Azure Event Hubs.</span></span> <span data-ttu-id="ec23a-105">Time Series Insights se conecta directamente a los orígenes de eventos e ingiere el flujo de datos sin necesidad de que los usuarios escriban una sola línea de código.</span><span class="sxs-lookup"><span data-stu-id="ec23a-105">Time Series Insights connects directly to Event Sources, ingesting the data stream without requiring users to write a single line of code.</span></span> <span data-ttu-id="ec23a-106">Actualmente, Time Series Insights es compatible tanto con Azure Event Hubs como con Azure IoT Hubs.</span><span class="sxs-lookup"><span data-stu-id="ec23a-106">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs.</span></span> <span data-ttu-id="ec23a-107">En el futuro, se agregarán más orígenes de eventos.</span><span class="sxs-lookup"><span data-stu-id="ec23a-107">In the future, more Event Sources will be added.</span></span>

## <a name="steps-to-add-an-event-source-to-your-environment"></a><span data-ttu-id="ec23a-108">Pasos para agregar un origen de eventos a su entorno</span><span class="sxs-lookup"><span data-stu-id="ec23a-108">Steps to add an event source to your environment</span></span>

1.  <span data-ttu-id="ec23a-109">Inicie sesión en el [portal Ibiza](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ec23a-109">Sign in to the [Ibiza portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="ec23a-110">Haga clic en "Todos los recursos" en el menú izquierdo del portal Ibiza.</span><span class="sxs-lookup"><span data-stu-id="ec23a-110">Click “All resources” in the menu on the left side of the Ibiza portal.</span></span>
3.  <span data-ttu-id="ec23a-111">Seleccione el entorno de Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="ec23a-111">Select your Time Series Insights environment.</span></span>

  ![Creación del origen de eventos de Time Series Insights](media/add-event-source/getstarted-create-event-source-1.png)

4.  <span data-ttu-id="ec23a-113">Seleccione "Orígenes de eventos", haga clic en "+Agregar".</span><span class="sxs-lookup"><span data-stu-id="ec23a-113">Select “Event Sources”, click “+ Add.”</span></span>

  ![Creación del origen de eventos de Time Series Insights: detalles](media/add-event-source/getstarted-create-event-source-2.png)

5.  <span data-ttu-id="ec23a-115">Especifique el nombre del origen de eventos.</span><span class="sxs-lookup"><span data-stu-id="ec23a-115">Specify the name of the event source.</span></span> <span data-ttu-id="ec23a-116">Este nombre se asocia a todos los eventos procedentes de este origen de eventos y está disponible en el momento de la consulta.</span><span class="sxs-lookup"><span data-stu-id="ec23a-116">This name is associated with all events coming from this event source and is available at query time.</span></span>
6.  <span data-ttu-id="ec23a-117">Seleccione un centro de eventos en la lista de recursos de Event Hub de la suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="ec23a-117">Select an event hub from the list of Event Hub resources in the current subscription.</span></span> <span data-ttu-id="ec23a-118">Otra opción es que elija la opción "Proporcionar configuración del centro de eventos de forma manual" para especificar un centro de eventos de otra suscripción.</span><span class="sxs-lookup"><span data-stu-id="ec23a-118">Otherwise choose import option "Provide Event Hub settings manually” to specify an event hub in another subscription.</span></span> <span data-ttu-id="ec23a-119">Los eventos se deben publicar en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="ec23a-119">Events must be published in JSON format.</span></span>
7.  <span data-ttu-id="ec23a-120">Seleccione una directiva con permiso de lectura en el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="ec23a-120">Select policy that has read permission in the event hub.</span></span>
8.  <span data-ttu-id="ec23a-121">Especifique el grupo de consumidores del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="ec23a-121">Specify event hub consumer group.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="ec23a-122">Asegúrese de que el grupo de consumidores no es utilizado por ningún otro servicio (como un trabajo de Stream Analytics u otro entorno de Time Series Insights).</span><span class="sxs-lookup"><span data-stu-id="ec23a-122">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="ec23a-123">Si otros servicios utilizan el grupo de consumidores, la operación de lectura se ve afectada negativamente en este entorno y en los otros servicios.</span><span class="sxs-lookup"><span data-stu-id="ec23a-123">If consumer group is used by other services, read operation is negatively affected for this environment and the other services.</span></span> <span data-ttu-id="ec23a-124">Utilizar “$Default” como grupo de consumidores podría provocar que otros lectores lo reutilicen.</span><span class="sxs-lookup"><span data-stu-id="ec23a-124">If you are using “$Default” as the consumer group, it could lead to potential reuse by other readers.</span></span>

9.  <span data-ttu-id="ec23a-125">Haga clic en "Crear".</span><span class="sxs-lookup"><span data-stu-id="ec23a-125">Click “Create.”</span></span>

<span data-ttu-id="ec23a-126">Tras la creación del origen de eventos, Time Series Insights iniciará automáticamente la transmisión de datos al entorno.</span><span class="sxs-lookup"><span data-stu-id="ec23a-126">After creation of the event source, Time Series Insights will automatically start streaming data into your environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec23a-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ec23a-127">Next steps</span></span>

* <span data-ttu-id="ec23a-128">[Envío de eventos](time-series-insights-send-events.md) al origen de eventos</span><span class="sxs-lookup"><span data-stu-id="ec23a-128">[Send events](time-series-insights-send-events.md) to the event source</span></span>
* <span data-ttu-id="ec23a-129">Vea el entorno en el [portal de Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="ec23a-129">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
