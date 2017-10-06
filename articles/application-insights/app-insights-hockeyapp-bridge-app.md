---
title: aaaExploring HockeyApp datos en Azure Application Insights | Documentos de Microsoft
description: "Analice el uso y el rendimiento de la aplicación de Azure con Application Insights."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 97783cc6-67d6-465f-9926-cb9821f4176e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: bwren
ms.openlocfilehash: ed7cf99b48f5ec78d6b401bb954cfcd014b9d1f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a><span data-ttu-id="64216-103">Exploración de datos de HockeyApp en Application Insights</span><span class="sxs-lookup"><span data-stu-id="64216-103">Exploring HockeyApp data in Application Insights</span></span>
<span data-ttu-id="64216-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) recomienda Hola plataforma para la supervisión de aplicaciones de escritorio y móviles en vivo.</span><span class="sxs-lookup"><span data-stu-id="64216-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) is hello recommended platform for monitoring live desktop and mobile apps.</span></span> <span data-ttu-id="64216-105">De HockeyApp, puede enviar personalizado y realice un seguimiento telemetría toomonitor uso y ayudar a un diagnóstico más detallado (en los datos de bloqueo de suma toogetting).</span><span class="sxs-lookup"><span data-stu-id="64216-105">From HockeyApp, you can send custom and trace telemetry toomonitor usage and assist in diagnosis (in addition toogetting crash data).</span></span> <span data-ttu-id="64216-106">Puede consultar esta secuencia de telemetría con hello eficaz [análisis](app-insights-analytics.md) característica de [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="64216-106">This stream of telemetry can be queried using hello powerful [Analytics](app-insights-analytics.md) feature of [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="64216-107">Además, puede [exportar Hola personalizado y telemetría de seguimiento](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="64216-107">In addition, you can [export hello custom and trace telemetry](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="64216-108">tooenable estas características, configurar un puente que retransmite HockeyApp datos personalizados tooApplication visión.</span><span class="sxs-lookup"><span data-stu-id="64216-108">tooenable these features, you set up a bridge that relays HockeyApp custom data tooApplication Insights.</span></span>

## <a name="hello-hockeyapp-bridge-app"></a><span data-ttu-id="64216-109">aplicación de puente de HockeyApp Hello</span><span class="sxs-lookup"><span data-stu-id="64216-109">hello HockeyApp Bridge app</span></span>
<span data-ttu-id="64216-110">Hola HockeyApp puente aplicación es Hola principal característica que permite tooaccess la telemetría de seguimiento en Application Insights a través de hello análisis y HockeyApp personalizado y las características de exportación continua.</span><span class="sxs-lookup"><span data-stu-id="64216-110">hello HockeyApp Bridge App is hello core feature that enables you tooaccess your HockeyApp custom and trace telemetry in Application Insights through hello Analytics and Continuous Export features.</span></span> <span data-ttu-id="64216-111">Custom y seguimiento de los eventos recopilados por HockeyApp después de la creación de hello de hello HockeyApp puente aplicación será accesibles desde estas características.</span><span class="sxs-lookup"><span data-stu-id="64216-111">Custom and trace events collected by HockeyApp after hello creation of hello HockeyApp Bridge App will be accessible from these features.</span></span> <span data-ttu-id="64216-112">Veamos cómo tooset una de estas aplicaciones de puente.</span><span class="sxs-lookup"><span data-stu-id="64216-112">Let’s see how tooset up one of these Bridge Apps.</span></span>

<span data-ttu-id="64216-113">En HockeyApp, abra Configuración de cuenta, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens)(Tokens de API).</span><span class="sxs-lookup"><span data-stu-id="64216-113">In HockeyApp, open Account Settings, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens).</span></span> <span data-ttu-id="64216-114">Cree un token o use uno existente.</span><span class="sxs-lookup"><span data-stu-id="64216-114">Either create a new token or reuse an existing one.</span></span> <span data-ttu-id="64216-115">se requieren permisos mínimo de Hello son "solo lectura".</span><span class="sxs-lookup"><span data-stu-id="64216-115">hello minimum rights required are "read only".</span></span> <span data-ttu-id="64216-116">Realizar una copia de hello API símbolo (token).</span><span class="sxs-lookup"><span data-stu-id="64216-116">Take a copy of hello API token.</span></span>

![Obtener un token de API de HockeyApp](./media/app-insights-hockeyapp-bridge-app/01.png)

<span data-ttu-id="64216-118">Portal de Microsoft Azure Hola abierto y [crear un recurso de Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="64216-118">Open hello Microsoft Azure portal and [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="64216-119">Establecer tipo de aplicación demasiado "Aplicación de puente de HockeyApp":</span><span class="sxs-lookup"><span data-stu-id="64216-119">Set Application Type too“HockeyApp bridge application”:</span></span>

![Nuevo recurso de Application Insights](./media/app-insights-hockeyapp-bridge-app/02.png)

<span data-ttu-id="64216-121">No es necesario tooset un nombre: Esto se establecerá automáticamente de nombre de HockeyApp Hola.</span><span class="sxs-lookup"><span data-stu-id="64216-121">You don't need tooset a name - this will automatically be set from hello HockeyApp name.</span></span>

<span data-ttu-id="64216-122">Hola HockeyApp puente campos aparecen.</span><span class="sxs-lookup"><span data-stu-id="64216-122">hello HockeyApp bridge fields appear.</span></span> 

![Especifique los campos de puente](./media/app-insights-hockeyapp-bridge-app/03.png)

<span data-ttu-id="64216-124">Escriba hello HockeyApp token que se ha indicado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="64216-124">Enter hello HockeyApp token you noted earlier.</span></span> <span data-ttu-id="64216-125">Esta acción rellena el menú de lista desplegable de "HockeyApp aplicación" hello con todas las aplicaciones de HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="64216-125">This action populates hello “HockeyApp Application” dropdown menu with all your HockeyApp applications.</span></span> <span data-ttu-id="64216-126">Seleccione Hola uno desea toouse y el resto de hello completa de campos de Hola.</span><span class="sxs-lookup"><span data-stu-id="64216-126">Select hello one you want toouse, and complete hello remainder of hello fields.</span></span> 

<span data-ttu-id="64216-127">Abra el nuevo recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="64216-127">Open hello new resource.</span></span> 

<span data-ttu-id="64216-128">Tenga en cuenta que los datos de hello tardan un tiempo toostart que fluyen.</span><span class="sxs-lookup"><span data-stu-id="64216-128">Note that hello data takes a while toostart flowing.</span></span>

![Recurso de Application Insights en espera de datos](./media/app-insights-hockeyapp-bridge-app/04.png)

<span data-ttu-id="64216-130">¡Ya está!</span><span class="sxs-lookup"><span data-stu-id="64216-130">That’s it!</span></span> <span data-ttu-id="64216-131">Custom y seguimiento de los datos recopilados en la aplicación instrumentada HockeyApp a partir de este punto están ahora también tooyou disponible en hello análisis y exportar continua características de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="64216-131">Custom and trace data collected in your HockeyApp-instrumented app from this point forward is now also available tooyou in hello Analytics and Continuous Export features of Application Insights.</span></span>

<span data-ttu-id="64216-132">Revisemos brevemente cada uno de estos tooyou ahora disponible de características.</span><span class="sxs-lookup"><span data-stu-id="64216-132">Let’s briefly review each of these features now available tooyou.</span></span>

## <a name="analytics"></a><span data-ttu-id="64216-133">Análisis</span><span class="sxs-lookup"><span data-stu-id="64216-133">Analytics</span></span>
<span data-ttu-id="64216-134">Análisis es una herramienta eficaz para realizar consultas de los datos, lo que le toodiagnose de ad hoc y analizar la telemetría y descubra rápidamente los patrones y las causas raíz.</span><span class="sxs-lookup"><span data-stu-id="64216-134">Analytics is a powerful tool for ad-hoc querying of your data, allowing you toodiagnose and analyze your telemetry and quickly discover root causes and patterns.</span></span>

![Análisis](./media/app-insights-hockeyapp-bridge-app/05.png)

* [<span data-ttu-id="64216-136">Aprenda más acerca de Analytics</span><span class="sxs-lookup"><span data-stu-id="64216-136">Learn more about Analytics</span></span>](app-insights-analytics-tour.md)

## <a name="continuous-export"></a><span data-ttu-id="64216-137">Exportación continua</span><span class="sxs-lookup"><span data-stu-id="64216-137">Continuous export</span></span>
<span data-ttu-id="64216-138">Exportación continua permite tooexport los datos en un contenedor de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="64216-138">Continuous Export allows you tooexport your data into an Azure Blob Storage container.</span></span> <span data-ttu-id="64216-139">Esto es muy útil si necesita tookeep los datos durante más tiempo que el período de retención de hello ofrece actualmente de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="64216-139">This is very useful if you need tookeep your data for longer than hello retention period currently offered by Application Insights.</span></span> <span data-ttu-id="64216-140">Puede mantener los datos de hello en almacenamiento de blobs, procesarlo en una base de datos de SQL o la solución de almacenamiento de datos preferidos.</span><span class="sxs-lookup"><span data-stu-id="64216-140">You can keep hello data in blob storage, process it into a SQL Database, or your preferred data warehousing solution.</span></span>

[<span data-ttu-id="64216-141">Aprenda más acerca de la exportación continua</span><span class="sxs-lookup"><span data-stu-id="64216-141">Learn more about Continuous Export</span></span>](app-insights-export-telemetry.md)

## <a name="next-steps"></a><span data-ttu-id="64216-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="64216-142">Next steps</span></span>
* [<span data-ttu-id="64216-143">Aplicar datos de análisis de tooyour</span><span class="sxs-lookup"><span data-stu-id="64216-143">Apply Analytics tooyour data</span></span>](app-insights-analytics-tour.md)

