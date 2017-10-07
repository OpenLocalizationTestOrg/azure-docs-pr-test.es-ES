---
title: "aaaCreate un entorno de visión de serie de tiempo de Azure | Documentos de Microsoft"
description: "En este tutorial, obtendrá información sobre cómo toocreate entorno de la serie de tiempo, lo conecte el origen del evento tooan y está listo tooanalyze los datos del evento en minutos."
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
ms.openlocfilehash: 7120fc9a6e4d4a4972f8cb37e4d9945cfb746fd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-time-series-insights-environment-in-hello-azure-portal"></a><span data-ttu-id="ef6b7-103">Crear un nuevo entorno de visión de la serie de tiempo en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ef6b7-103">Create a new Time Series Insights environment in hello Azure portal</span></span>

<span data-ttu-id="ef6b7-104">Un entorno de Time Series Insights es un recurso de Azure con funcionalidades de incorporación y almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ef6b7-104">Time Series Insights environment is an Azure resource with ingress and storage capacity.</span></span> <span data-ttu-id="ef6b7-105">Los clientes proporcionar entornos a través de hello portal de Azure con capacidad de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="ef6b7-105">Customers provision environments via hello Azure portal with hello required capacity.</span></span>

## <a name="steps-toocreate-hello-environment"></a><span data-ttu-id="ef6b7-106">Entorno de hello toocreate de pasos</span><span class="sxs-lookup"><span data-stu-id="ef6b7-106">Steps toocreate hello environment</span></span>

<span data-ttu-id="ef6b7-107">Siga estos pasos toocreate su entorno:</span><span class="sxs-lookup"><span data-stu-id="ef6b7-107">Follow these steps toocreate your environment:</span></span>

1.  <span data-ttu-id="ef6b7-108">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ef6b7-108">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="ef6b7-109">Haga clic en hello más el signo ("+") en hello esquina superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="ef6b7-109">Click hello plus sign (“+”) in hello top left corner.</span></span>
3.  <span data-ttu-id="ef6b7-110">Busque "Información de Series de tiempo" en el cuadro de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef6b7-110">Search for “Time Series Insights” in hello search box.</span></span>

  ![Crear entorno de visión de la serie de tiempo de Hola](media/get-started/getstarted-create-environment1.png)

4.  <span data-ttu-id="ef6b7-112">Seleccione "Time Series Insights" y haga clic en "Crear".</span><span class="sxs-lookup"><span data-stu-id="ef6b7-112">Select “Time Series Insights”, click “Create”.</span></span>

  ![Crear grupo de recursos de información de la serie de tiempo de Hola](media/get-started/getstarted-create-environment2.png)

5.  <span data-ttu-id="ef6b7-114">Especifique el nombre del entorno.</span><span class="sxs-lookup"><span data-stu-id="ef6b7-114">Specify environment name.</span></span> <span data-ttu-id="ef6b7-115">Este nombre representa el entorno de hello en [explorer de la serie de tiempo](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ef6b7-115">This name will represent hello environment in [time series explorer](https://insights.timeseries.azure.com).</span></span>
6.  <span data-ttu-id="ef6b7-116">Seleccione una suscripción.</span><span class="sxs-lookup"><span data-stu-id="ef6b7-116">Select a subscription.</span></span> <span data-ttu-id="ef6b7-117">Elija una que contenga el origen de eventos.</span><span class="sxs-lookup"><span data-stu-id="ef6b7-117">Choose one that contains your event source.</span></span> <span data-ttu-id="ef6b7-118">Visión de la serie de tiempo puede detectar automáticamente centro de IoT de Azure y recursos de concentrador de eventos existentes en Hola misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="ef6b7-118">Time Series Insights can auto-detect Azure IoT Hub and Event Hub resources existing in hello same subscription.</span></span>
7.  <span data-ttu-id="ef6b7-119">Seleccione o cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ef6b7-119">Select or create a resource group.</span></span> <span data-ttu-id="ef6b7-120">Un grupo de recursos es una colección de recursos de Azure que se usan juntos.</span><span class="sxs-lookup"><span data-stu-id="ef6b7-120">A resource group is a collection of Azure resources used together.</span></span>
8.  <span data-ttu-id="ef6b7-121">Selección de una ubicación de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="ef6b7-121">Select a hosting location.</span></span> <span data-ttu-id="ef6b7-122">centros de tooavoid mover datos a través de los datos, elija la ubicación que contiene el origen del evento.</span><span class="sxs-lookup"><span data-stu-id="ef6b7-122">tooavoid moving data across data centers, choose location that contains your event source.</span></span>
9.  <span data-ttu-id="ef6b7-123">Seleccione un plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="ef6b7-123">Select a pricing tier.</span></span>
10. <span data-ttu-id="ef6b7-124">Seleccione la capacidad.</span><span class="sxs-lookup"><span data-stu-id="ef6b7-124">Select capacity.</span></span> <span data-ttu-id="ef6b7-125">Puede cambiar la capacidad de un entorno después de su creación.</span><span class="sxs-lookup"><span data-stu-id="ef6b7-125">You can change capacity of an environment after creation.</span></span>
11. <span data-ttu-id="ef6b7-126">Cree el entorno.</span><span class="sxs-lookup"><span data-stu-id="ef6b7-126">Create your environment.</span></span> <span data-ttu-id="ef6b7-127">También puede anclar el panel de toohello de entorno para facilitar el acceso siempre que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="ef6b7-127">You can also pin your environment toohello dashboard for easy access whenever you sign in.</span></span>

  ![Crear toodashboard de pin de hello visión de la serie de tiempo](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a><span data-ttu-id="ef6b7-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ef6b7-129">Next steps</span></span>

* <span data-ttu-id="ef6b7-130">[Definir directivas de acceso de datos](time-series-insights-data-access.md) tooaccess su entorno en [Portal de visión de Series de tiempo](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="ef6b7-130">[Define data access policies](time-series-insights-data-access.md) tooaccess your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
* [<span data-ttu-id="ef6b7-131">Creación de un origen de eventos</span><span class="sxs-lookup"><span data-stu-id="ef6b7-131">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="ef6b7-132">[Enviar eventos](time-series-insights-send-events.md) toohello origen del evento</span><span class="sxs-lookup"><span data-stu-id="ef6b7-132">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
