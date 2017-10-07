---
title: aaaTroubleshooting con seguimiento de eventos | Documentos de Microsoft
description: "problemas más comunes de Hello al implementar servicios en Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: f5adb7e15fa1e2c964bbbc5726246630c95e13f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a><span data-ttu-id="a3f9b-103">Solución de problemas comunes al implementar servicios en Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a3f9b-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span></span>
<span data-ttu-id="a3f9b-104">Si estás ejecutando los servicios en el equipo del desarrollador, resulta fácil toouse [herramientas de depuración de Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="a3f9b-104">When you're running services on your developer computer, it is easy toouse [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span> <span data-ttu-id="a3f9b-105">Para los clústeres remotos, [informes de mantenimiento](service-fabric-view-entities-aggregated-health.md) siempre son un buen lugar toostart.</span><span class="sxs-lookup"><span data-stu-id="a3f9b-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place toostart.</span></span> <span data-ttu-id="a3f9b-106">Hola tooaccess más fácil de formas son estos informes a través de PowerShell o [SFX](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="a3f9b-106">hello easiest ways tooaccess these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="a3f9b-107">En este artículo se da por supuesto que está depurando un clúster remoto y tener un conocimiento básico de cómo toouse cualquiera de estas herramientas.</span><span class="sxs-lookup"><span data-stu-id="a3f9b-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how toouse either of these tools.</span></span>

## <a name="application-crash"></a><span data-ttu-id="a3f9b-108">Bloqueo de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="a3f9b-108">Application crash</span></span>
<span data-ttu-id="a3f9b-109">Hola "partición está por debajo de recuento de instancia o la réplica de destino" informe es una buena indicación de que el servicio está bloqueado.</span><span class="sxs-lookup"><span data-stu-id="a3f9b-109">hello "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span></span> <span data-ttu-id="a3f9b-110">toofind out donde está bloqueando el servicio tarda un poco más investigación.</span><span class="sxs-lookup"><span data-stu-id="a3f9b-110">toofind out where your service is crashing takes a little more investigation.</span></span> <span data-ttu-id="a3f9b-111">Cuando el servicio se ejecuta a escala, su mejor amigo será un conjunto de seguimiento bien elaborados.</span><span class="sxs-lookup"><span data-stu-id="a3f9b-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span></span>  <span data-ttu-id="a3f9b-112">Le sugerimos que pruebe [diagnósticos de Azure](service-fabric-diagnostics-how-to-setup-wad.md) para recopilar esos seguimientos y con una solución como [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) para ver y buscar seguimientos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3f9b-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching hello traces.</span></span>

![Estado de las particiones SFX](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a><span data-ttu-id="a3f9b-114">Durante la inicialización del actor o del servicio</span><span class="sxs-lookup"><span data-stu-id="a3f9b-114">During service or actor initialization</span></span>
<span data-ttu-id="a3f9b-115">Cualquier excepción antes de inicializa el tipo de servicio de hello provocará Hola proceso toocrash.</span><span class="sxs-lookup"><span data-stu-id="a3f9b-115">Any exceptions before hello service type is initialized will cause hello process toocrash.</span></span> <span data-ttu-id="a3f9b-116">Para estos tipos de bloqueos, registro de eventos de aplicación Hola mostrará error Hola de su servicio.</span><span class="sxs-lookup"><span data-stu-id="a3f9b-116">For these types of crashes, hello application event log will show hello error from your service.</span></span>
<span data-ttu-id="a3f9b-117">Se trata de toosee las excepciones más comunes de hello antes de inicializa el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3f9b-117">These are hello most common exceptions toosee before hello service is initialized.</span></span>

<span data-ttu-id="a3f9b-118">***System.IO.FileNotFoundException***</span><span class="sxs-lookup"><span data-stu-id="a3f9b-118">***System.IO.FileNotFoundException***</span></span>

<span data-ttu-id="a3f9b-119">Este error suele ser debido a las dependencias de ensamblado de toomissing.</span><span class="sxs-lookup"><span data-stu-id="a3f9b-119">This error is often due toomissing assembly dependencies.</span></span> <span data-ttu-id="a3f9b-120">Compruebe la propiedad CopyLocal de hello en Visual Studio o la caché de ensamblados global de hello para el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3f9b-120">Check hello CopyLocal property in Visual Studio or hello global assembly cache for hello node.</span></span>

<span data-ttu-id="a3f9b-121">***System.Runtime.InteropServices.COMException*** *en System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*</span><span class="sxs-lookup"><span data-stu-id="a3f9b-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span></span>

 <span data-ttu-id="a3f9b-122">Esto indica que ese nombre de tipo de servicio registrado hello no coincide con el manifiesto del servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="a3f9b-122">This indicates that hello registered service type name does not match hello service manifest.</span></span>

<span data-ttu-id="a3f9b-123">[Diagnósticos de Azure](service-fabric-diagnostics-how-to-setup-wad.md) puede ser configurado tooupload Hola el registro de eventos de aplicación para todos los nodos automáticamente.</span><span class="sxs-lookup"><span data-stu-id="a3f9b-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured tooupload hello application event log for all your nodes automatically.</span></span>

### <a name="runasync-or-onactivateasync"></a><span data-ttu-id="a3f9b-124">RunAsync() o OnActivateAsync()</span><span class="sxs-lookup"><span data-stu-id="a3f9b-124">RunAsync() or OnActivateAsync()</span></span>
<span data-ttu-id="a3f9b-125">Si se produce un bloqueo de Hola durante la inicialización de Hola o la ejecución de su tipo de servicio registrado o un actor, excepción de hello detectará Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a3f9b-125">If hello crash happens during hello initialization or running of your registered service type or actor, hello exception will be caught by Azure Service Fabric.</span></span> <span data-ttu-id="a3f9b-126">Puede ver estas desde proveedores de hello EventSource detallados en la sección "Pasos siguientes" Hola.</span><span class="sxs-lookup"><span data-stu-id="a3f9b-126">You can view these from hello EventSource providers detailed in hello "Next steps" section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3f9b-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a3f9b-127">Next steps</span></span>
<span data-ttu-id="a3f9b-128">Más información sobre el diagnóstico existente ofrecido por Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="a3f9b-128">Learn more about existing diagnostics provided by Service Fabric:</span></span>

* [<span data-ttu-id="a3f9b-129">Diagnósticos de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="a3f9b-129">Reliable Actors diagnostics</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="a3f9b-130">Diagnóstico de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="a3f9b-130">Reliable Services diagnostics</span></span>](service-fabric-reliable-services-diagnostics.md)

