---
title: aaaAdd un entorno de Azure Insights de serie de tiempo de evento origen tooyour | Documentos de Microsoft
description: "En este tutorial, se conectará un entorno de visión de la serie de tiempo de tooyour de origen de eventos"
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
ms.openlocfilehash: 817df5e81cb4dc3d7376914a4651aabebadbcc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a><span data-ttu-id="77e84-103">Crear un origen de eventos para el entorno de visión de la serie de tiempo mediante este portal como Hola</span><span class="sxs-lookup"><span data-stu-id="77e84-103">Create an event source for your Time Series Insights environment using hello Ibiza portal</span></span>

<span data-ttu-id="77e84-104">El origen de eventos de Time Series Insights se deriva de un agente de eventos, como Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="77e84-104">Time Series Insights Event Source is derived from an event broker, like Azure Event Hubs.</span></span> <span data-ttu-id="77e84-105">Visión de la serie de tiempo se conecta directamente orígenes tooEvent, ingesta de flujo de datos de hello sin necesidad de toowrite a los usuarios una sola línea de código.</span><span class="sxs-lookup"><span data-stu-id="77e84-105">Time Series Insights connects directly tooEvent Sources, ingesting hello data stream without requiring users toowrite a single line of code.</span></span> <span data-ttu-id="77e84-106">Actualmente, Time Series Insights es compatible tanto con Azure Event Hubs como con Azure IoT Hubs.</span><span class="sxs-lookup"><span data-stu-id="77e84-106">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs.</span></span> <span data-ttu-id="77e84-107">Hola futuras, se agregarán más orígenes de eventos.</span><span class="sxs-lookup"><span data-stu-id="77e84-107">In hello future, more Event Sources will be added.</span></span>

## <a name="steps-tooadd-an-event-source-tooyour-environment"></a><span data-ttu-id="77e84-108">Pasos tooadd un entorno de tooyour de origen de eventos</span><span class="sxs-lookup"><span data-stu-id="77e84-108">Steps tooadd an event source tooyour environment</span></span>

1.  <span data-ttu-id="77e84-109">Inicie sesión en toohello [este portal como](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="77e84-109">Sign in toohello [Ibiza portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="77e84-110">Haga clic en "Todos los recursos" en el menú izquierda Hola de este portal como Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="77e84-110">Click “All resources” in hello menu on hello left side of hello Ibiza portal.</span></span>
3.  <span data-ttu-id="77e84-111">Seleccione el entorno de Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="77e84-111">Select your Time Series Insights environment.</span></span>

  ![Crear origen de eventos de información de la serie de tiempo de Hola](media/add-event-source/getstarted-create-event-source-1.png)

4.  <span data-ttu-id="77e84-113">Seleccione "Orígenes de eventos", haga clic en "+Agregar".</span><span class="sxs-lookup"><span data-stu-id="77e84-113">Select “Event Sources”, click “+ Add.”</span></span>

  ![Crear origen de eventos de información de la serie de tiempo de hello - detalles](media/add-event-source/getstarted-create-event-source-2.png)

5.  <span data-ttu-id="77e84-115">Especifique el nombre de Hola Hola del origen de evento.</span><span class="sxs-lookup"><span data-stu-id="77e84-115">Specify hello name of hello event source.</span></span> <span data-ttu-id="77e84-116">Este nombre se asocia a todos los eventos procedentes de este origen de eventos y está disponible en el momento de la consulta.</span><span class="sxs-lookup"><span data-stu-id="77e84-116">This name is associated with all events coming from this event source and is available at query time.</span></span>
6.  <span data-ttu-id="77e84-117">Seleccione un concentrador de eventos de lista de Hola de recursos de concentrador de eventos de suscripción actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="77e84-117">Select an event hub from hello list of Event Hub resources in hello current subscription.</span></span> <span data-ttu-id="77e84-118">En caso contrario, elija la opción de importación "configuración del centro de eventos de proporcionar manualmente" toospecify un concentrador de eventos en otra suscripción.</span><span class="sxs-lookup"><span data-stu-id="77e84-118">Otherwise choose import option "Provide Event Hub settings manually” toospecify an event hub in another subscription.</span></span> <span data-ttu-id="77e84-119">Los eventos se deben publicar en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="77e84-119">Events must be published in JSON format.</span></span>
7.  <span data-ttu-id="77e84-120">Seleccione la directiva que tiene permiso en el concentrador de eventos de Hola de lectura.</span><span class="sxs-lookup"><span data-stu-id="77e84-120">Select policy that has read permission in hello event hub.</span></span>
8.  <span data-ttu-id="77e84-121">Especifique el grupo de consumidores del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="77e84-121">Specify event hub consumer group.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="77e84-122">Asegúrese de que el grupo de consumidores no es utilizado por ningún otro servicio (como un trabajo de Stream Analytics u otro entorno de Time Series Insights).</span><span class="sxs-lookup"><span data-stu-id="77e84-122">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="77e84-123">Si se usa el grupo de consumidores por otros servicios, lea la operación se ve afectada negativamente para este entorno y Hola otros servicios.</span><span class="sxs-lookup"><span data-stu-id="77e84-123">If consumer group is used by other services, read operation is negatively affected for this environment and hello other services.</span></span> <span data-ttu-id="77e84-124">Si usas "$Default" como grupo de consumidores de hello, puede provocar toopotential reutilización por otro lector.</span><span class="sxs-lookup"><span data-stu-id="77e84-124">If you are using “$Default” as hello consumer group, it could lead toopotential reuse by other readers.</span></span>

9.  <span data-ttu-id="77e84-125">Haga clic en "Crear".</span><span class="sxs-lookup"><span data-stu-id="77e84-125">Click “Create.”</span></span>

<span data-ttu-id="77e84-126">Después de la creación del origen de evento de hello, visión de la serie de tiempo se iniciará automáticamente la transmisión de datos en su entorno.</span><span class="sxs-lookup"><span data-stu-id="77e84-126">After creation of hello event source, Time Series Insights will automatically start streaming data into your environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77e84-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="77e84-127">Next steps</span></span>

* <span data-ttu-id="77e84-128">[Enviar eventos](time-series-insights-send-events.md) toohello origen del evento</span><span class="sxs-lookup"><span data-stu-id="77e84-128">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="77e84-129">Vea el entorno en el [portal de Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="77e84-129">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
