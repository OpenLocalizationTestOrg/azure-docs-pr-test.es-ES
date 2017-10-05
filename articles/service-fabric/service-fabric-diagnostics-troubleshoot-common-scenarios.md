---
title: "Solución de problemas con el seguimiento de eventos | Microsoft Docs"
description: "Los problemas más habituales que aparecen al implementar servicios en Microsoft Azure Service Fabric."
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
ms.openlocfilehash: e60bd4b9291cb2fc748921e42f11f54bb545984f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a><span data-ttu-id="8049f-103">Solución de problemas comunes al implementar servicios en Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8049f-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span></span>
<span data-ttu-id="8049f-104">Al ejecutar servicios en su equipo de desarrollador, es fácil usar [herramientas de depuración de Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="8049f-104">When you're running services on your developer computer, it is easy to use [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span> <span data-ttu-id="8049f-105">Para clústeres remotos, los [informes de estado](service-fabric-view-entities-aggregated-health.md) resultan siempre un buen punto de partida.</span><span class="sxs-lookup"><span data-stu-id="8049f-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place to start.</span></span> <span data-ttu-id="8049f-106">La manera más sencilla de obtener acceso a estos informes es a través de PowerShell o [SFX](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="8049f-106">The easiest ways to access these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="8049f-107">En este artículo se supone que está depurando un clúster remoto y que tiene un conocimiento básico de cómo usar cualquiera de estas herramientas.</span><span class="sxs-lookup"><span data-stu-id="8049f-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how to use either of these tools.</span></span>

## <a name="application-crash"></a><span data-ttu-id="8049f-108">Bloqueo de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="8049f-108">Application crash</span></span>
<span data-ttu-id="8049f-109">El informe "La partición se encuentra por debajo del número de instancias o de réplicas de destino" es un buen indicio de que se bloquea el servicio.</span><span class="sxs-lookup"><span data-stu-id="8049f-109">The "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span></span> <span data-ttu-id="8049f-110">Para averiguar dónde se bloquea su servicio, será necesario investigar un poco más.</span><span class="sxs-lookup"><span data-stu-id="8049f-110">To find out where your service is crashing takes a little more investigation.</span></span> <span data-ttu-id="8049f-111">Cuando el servicio se ejecuta a escala, su mejor amigo será un conjunto de seguimiento bien elaborados.</span><span class="sxs-lookup"><span data-stu-id="8049f-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span></span>  <span data-ttu-id="8049f-112">Le recomendamos que pruebe [Diagnósticos de Azure](service-fabric-diagnostics-how-to-setup-wad.md) para recopilar esos seguimientos y usar una solución como [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) para ver y buscar los seguimientos.</span><span class="sxs-lookup"><span data-stu-id="8049f-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching the traces.</span></span>

![Estado de las particiones SFX](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a><span data-ttu-id="8049f-114">Durante la inicialización del actor o del servicio</span><span class="sxs-lookup"><span data-stu-id="8049f-114">During service or actor initialization</span></span>
<span data-ttu-id="8049f-115">Las excepciones antes de que se inicialice el tipo de servicio harán que se bloquee el proceso.</span><span class="sxs-lookup"><span data-stu-id="8049f-115">Any exceptions before the service type is initialized will cause the process to crash.</span></span> <span data-ttu-id="8049f-116">Para estos tipos de bloqueos, el registro de eventos de la aplicación mostrará el error desde el servicio.</span><span class="sxs-lookup"><span data-stu-id="8049f-116">For these types of crashes, the application event log will show the error from your service.</span></span>
<span data-ttu-id="8049f-117">Estas son las excepciones más comunes que se ven antes de que se inicialice el servicio.</span><span class="sxs-lookup"><span data-stu-id="8049f-117">These are the most common exceptions to see before the service is initialized.</span></span>

<span data-ttu-id="8049f-118">***System.IO.FileNotFoundException***</span><span class="sxs-lookup"><span data-stu-id="8049f-118">***System.IO.FileNotFoundException***</span></span>

<span data-ttu-id="8049f-119">Este error a menudo se debe a que faltan las dependencias de ensamblado.</span><span class="sxs-lookup"><span data-stu-id="8049f-119">This error is often due to missing assembly dependencies.</span></span> <span data-ttu-id="8049f-120">Compruebe la propiedad CopyLocal en Visual Studio o en la caché global de ensamblados para el nodo.</span><span class="sxs-lookup"><span data-stu-id="8049f-120">Check the CopyLocal property in Visual Studio or the global assembly cache for the node.</span></span>

<span data-ttu-id="8049f-121">***System.Runtime.InteropServices.COMException*** *en System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*</span><span class="sxs-lookup"><span data-stu-id="8049f-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span></span>

 <span data-ttu-id="8049f-122">Esto indica que el nombre del tipo de servicio registrado no coincide con el manifiesto de servicio.</span><span class="sxs-lookup"><span data-stu-id="8049f-122">This indicates that the registered service type name does not match the service manifest.</span></span>

<span data-ttu-id="8049f-123">[Diagnósticos de Azure](service-fabric-diagnostics-how-to-setup-wad.md) se puede configurar para cargar automáticamente el registro de eventos de la aplicación para todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="8049f-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured to upload the application event log for all your nodes automatically.</span></span>

### <a name="runasync-or-onactivateasync"></a><span data-ttu-id="8049f-124">RunAsync() o OnActivateAsync()</span><span class="sxs-lookup"><span data-stu-id="8049f-124">RunAsync() or OnActivateAsync()</span></span>
<span data-ttu-id="8049f-125">Si el bloqueo se produce durante la inicialización o al ejecutar su actor o tipo de servicio registrado, Azure Service Fabric detectará la excepción.</span><span class="sxs-lookup"><span data-stu-id="8049f-125">If the crash happens during the initialization or running of your registered service type or actor, the exception will be caught by Azure Service Fabric.</span></span> <span data-ttu-id="8049f-126">Puede verlos desde los proveedores de EventSource detallados en la sección "Pasos siguientes".</span><span class="sxs-lookup"><span data-stu-id="8049f-126">You can view these from the EventSource providers detailed in the "Next steps" section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8049f-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8049f-127">Next steps</span></span>
<span data-ttu-id="8049f-128">Más información sobre el diagnóstico existente ofrecido por Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="8049f-128">Learn more about existing diagnostics provided by Service Fabric:</span></span>

* [<span data-ttu-id="8049f-129">Diagnósticos de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="8049f-129">Reliable Actors diagnostics</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="8049f-130">Diagnóstico de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="8049f-130">Reliable Services diagnostics</span></span>](service-fabric-reliable-services-diagnostics.md)

