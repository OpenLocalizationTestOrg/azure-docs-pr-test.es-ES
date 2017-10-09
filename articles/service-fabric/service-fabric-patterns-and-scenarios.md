---
title: aaaAzure Service Fabric patrones y escenarios | Documentos de Microsoft
description: "Obtenga información acerca de los procedimientos recomendados y demostrar toodesign patrones reutilizable, desarrollar y utilizar su microservicios en Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: d5aa75ff-98b9-4573-a2e5-7f5ab288157a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 3811420eb53d9a49e490dd2e2e5319d8dea5629c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-patterns-and-scenarios"></a><span data-ttu-id="d9064-103">Escenarios y patrones de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d9064-103">Service Fabric patterns and scenarios</span></span>
<span data-ttu-id="d9064-104">Si está pensando en generar microservicios a gran escala mediante Azure Service Fabric, obtenga información acerca de los expertos de Hola que diseñados y creados de esta plataforma como servicio (PaaS).</span><span class="sxs-lookup"><span data-stu-id="d9064-104">If you’re looking at building large-scale microservices using Azure Service Fabric, learn from hello experts who designed and built this platform as a service (PaaS).</span></span> <span data-ttu-id="d9064-105">Introducción a la arquitectura correcta y, a continuación, obtenga información acerca de cómo toooptimize recursos de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="d9064-105">Get started with proper architecture, and then learn how toooptimize resources for your application.</span></span> <span data-ttu-id="d9064-106">Hola [Service Fabric patrones y prácticas](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) curso responde Hola preguntas con mayor frecuencia por los clientes reales sobre escenarios de Service Fabric y áreas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d9064-106">hello [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) course answers hello questions most often asked by real-world customers about Service Fabric scenarios and application areas.</span></span>
 
<span data-ttu-id="d9064-107">Averigüe cómo toodesign, desarrollar y utilizar su microservicios en el tejido de servicio con las prácticas recomendadas y patrones probados y reutilizables.</span><span class="sxs-lookup"><span data-stu-id="d9064-107">Find out how toodesign, develop, and operate your microservices on Service Fabric using best practices and proven, reusable patterns.</span></span> <span data-ttu-id="d9064-108">Obtenga una introducción a Service Fabric y luego profundice en temas que abarcan la optimización y la seguridad del clúster, la migración de aplicaciones heredadas, IoT a escala, el hospedaje de motores de juegos, etc.</span><span class="sxs-lookup"><span data-stu-id="d9064-108">Get an overview of Service Fabric and then dive deep into topics that cover cluster optimization and security, migrating legacy apps, IoT at scale, hosting game engines, and more.</span></span> <span data-ttu-id="d9064-109">Examine la entrega continua para diversas cargas de trabajo y obtener detalles de hello en compatibilidad con Linux y contenedores.</span><span class="sxs-lookup"><span data-stu-id="d9064-109">Look at continuous delivery for various workloads, and even get hello details on Linux support and containers.</span></span> 

## <a name="introduction"></a><span data-ttu-id="d9064-110">Introducción</span><span class="sxs-lookup"><span data-stu-id="d9064-110">Introduction</span></span>
<span data-ttu-id="d9064-111">Examine los procedimientos recomendados y sepa cómo elegir plataforma como servicio (PaaS) sobre infraestructura cómo servicio (IaaS).</span><span class="sxs-lookup"><span data-stu-id="d9064-111">Explore best practices, and learn about choosing platform as a service (PaaS) over infrastructure as a service (IaaS).</span></span> <span data-ttu-id="d9064-112">Obtener detalles de hello en los siguientes principios de diseño de la aplicación probada.</span><span class="sxs-lookup"><span data-stu-id="d9064-112">Get hello details on following proven application design principles.</span></span>

<table><tr><th><span data-ttu-id="d9064-113">Vídeo</span><span class="sxs-lookup"><span data-stu-id="d9064-113">Video</span></span></th><th><span data-ttu-id="d9064-114">Lote de PowerPoint</span><span class="sxs-lookup"><span data-stu-id="d9064-114">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="./media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="d9064-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introducción tooService tejido</a></span><span class="sxs-lookup"><span data-stu-id="d9064-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduction tooService Fabric</a></span></span></td></tr>
</table>

## <a name="cluster-planning-and-management"></a><span data-ttu-id="d9064-116">Planeamiento y administración de clústeres</span><span class="sxs-lookup"><span data-stu-id="d9064-116">Cluster planning and management</span></span>
<span data-ttu-id="d9064-117">Aprenda sobre el planeamiento de la capacidad, la optimización del clúster y la seguridad del clúster en Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d9064-117">Learn about capacity planning, cluster optimization, and cluster security, in this look at Azure Service Fabric.</span></span>

<table><tr><th><span data-ttu-id="d9064-118">Vídeo</span><span class="sxs-lookup"><span data-stu-id="d9064-118">Video</span></span></th><th><span data-ttu-id="d9064-119">Lote de PowerPoint</span><span class="sxs-lookup"><span data-stu-id="d9064-119">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="./media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <span data-ttu-id="d9064-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Planeamiento y administración de clústeres</a></span><span class="sxs-lookup"><span data-stu-id="d9064-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Cluster Planning and Management</a></span></span></td></tr>
</table>

## <a name="hyper-scale-web"></a><span data-ttu-id="d9064-121">Web a hiperescala</span><span class="sxs-lookup"><span data-stu-id="d9064-121">Hyper-scale web</span></span>
<span data-ttu-id="d9064-122">Repase conceptos en torno a web a hiperescala, como disponibilidad y confiabilidad, hiperescala y administración de estado.</span><span class="sxs-lookup"><span data-stu-id="d9064-122">Review concepts around hyper-scale web, including availability and reliability, hyper-scale, and state management.</span></span>

<table><tr><th><span data-ttu-id="d9064-123">Vídeo</span><span class="sxs-lookup"><span data-stu-id="d9064-123">Video</span></span></th><th><span data-ttu-id="d9064-124">Lote de PowerPoint</span><span class="sxs-lookup"><span data-stu-id="d9064-124">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="./media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="d9064-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Web a hiperescala</a></span><span class="sxs-lookup"><span data-stu-id="d9064-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Hyper-scale web</a></span></span></td></tr>
</table>

## <a name="iot"></a><span data-ttu-id="d9064-126">IoT</span><span class="sxs-lookup"><span data-stu-id="d9064-126">IoT</span></span>
<span data-ttu-id="d9064-127">Explorar Internet de las cosas (IoT) hello en el contexto de Hola de Azure Service Fabric, como canalización de IoT de Azure de hello, multiempresa y IoT a escala.</span><span class="sxs-lookup"><span data-stu-id="d9064-127">Explore hello Internet of Things (IoT) in hello context of Azure Service Fabric, including hello Azure IoT pipeline, multi-tenancy, and IoT at scale.</span></span>

<table><tr><th><span data-ttu-id="d9064-128">Vídeo</span><span class="sxs-lookup"><span data-stu-id="d9064-128">Video</span></span></th><th><span data-ttu-id="d9064-129">Lote de PowerPoint</span><span class="sxs-lookup"><span data-stu-id="d9064-129">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="./media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="d9064-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span><span class="sxs-lookup"><span data-stu-id="d9064-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span></span></td></tr>
</table>

## <a name="gaming"></a><span data-ttu-id="d9064-131">Juegos</span><span class="sxs-lookup"><span data-stu-id="d9064-131">Gaming</span></span>
<span data-ttu-id="d9064-132">Examine juegos basados en turnos, juegos interactivos y hospedaje de motores de juegos existentes.</span><span class="sxs-lookup"><span data-stu-id="d9064-132">Look at turn-based games, interactive games, and hosting existing game engines.</span></span>

<table><tr><th><span data-ttu-id="d9064-133">Vídeo</span><span class="sxs-lookup"><span data-stu-id="d9064-133">Video</span></span></th><th><span data-ttu-id="d9064-134">Lote de PowerPoint</span><span class="sxs-lookup"><span data-stu-id="d9064-134">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="./media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="d9064-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Juegos</a></span><span class="sxs-lookup"><span data-stu-id="d9064-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gaming</a></span></span></td></tr>
</table>

## <a name="continuous-delivery"></a><span data-ttu-id="d9064-136">Entrega continua</span><span class="sxs-lookup"><span data-stu-id="d9064-136">Continuous delivery</span></span>
<span data-ttu-id="d9064-137">Explore conceptos, como integración continua/entrega continua con Visual Studio Team Services, compilación/empaquetado/publicación de flujos de trabajo, configuración en varios entornos y empaquetado/uso compartido de servicios.</span><span class="sxs-lookup"><span data-stu-id="d9064-137">Explore concepts, including continuous integration/continuous delivery with Visual Studio Team Services, build/package/publish workflow, multi-environment setup, and service package/share.</span></span>

<table><tr><th><span data-ttu-id="d9064-138">Vídeo</span><span class="sxs-lookup"><span data-stu-id="d9064-138">Video</span></span></th><th><span data-ttu-id="d9064-139">Lote de PowerPoint</span><span class="sxs-lookup"><span data-stu-id="d9064-139">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="d9064-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Entrega continua</a></span><span class="sxs-lookup"><span data-stu-id="d9064-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Continuous delivery</a></span></span></td></tr>
</table>

## <a name="migration"></a><span data-ttu-id="d9064-141">Migración</span><span class="sxs-lookup"><span data-stu-id="d9064-141">Migration</span></span>
<span data-ttu-id="d9064-142">Obtenga información sobre la migración desde un servicio en la nube, además toomigration de las aplicaciones heredadas.</span><span class="sxs-lookup"><span data-stu-id="d9064-142">Learn about migrating from a cloud service, in addition toomigration of legacy apps.</span></span>

<table><tr><th><span data-ttu-id="d9064-143">Vídeo</span><span class="sxs-lookup"><span data-stu-id="d9064-143">Video</span></span></th><th><span data-ttu-id="d9064-144">Lote de PowerPoint</span><span class="sxs-lookup"><span data-stu-id="d9064-144">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="./media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="d9064-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migración</a></span><span class="sxs-lookup"><span data-stu-id="d9064-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migration</a></span></span></td></tr>
</table>

## <a name="containers-and-linux-support"></a><span data-ttu-id="d9064-146">Contenedores y compatibilidad con Linux</span><span class="sxs-lookup"><span data-stu-id="d9064-146">Containers and Linux support</span></span>
<span data-ttu-id="d9064-147">Obtener la pregunta de toohello de respuesta de hello, "¿por qué contenedores?"</span><span class="sxs-lookup"><span data-stu-id="d9064-147">Get hello answer toohello question, "Why containers?"</span></span> <span data-ttu-id="d9064-148">Obtenga información acerca de la vista previa de Hola para contenedores de Windows, Linux admite y orquestación de contenedores de Linux.</span><span class="sxs-lookup"><span data-stu-id="d9064-148">Learn about hello preview for Windows containers, Linux supports, and Linux containers orchestration.</span></span> <span data-ttu-id="d9064-149">Además, averigüe cómo toomigrate .NET Core aplicaciones tooLinux.</span><span class="sxs-lookup"><span data-stu-id="d9064-149">Plus, find out how toomigrate .NET Core apps tooLinux.</span></span>

<table><tr><th><span data-ttu-id="d9064-150">Vídeo</span><span class="sxs-lookup"><span data-stu-id="d9064-150">Video</span></span></th><th><span data-ttu-id="d9064-151">Lote de PowerPoint</span><span class="sxs-lookup"><span data-stu-id="d9064-151">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="d9064-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Contenedores y compatibilidad con Linux</a></span><span class="sxs-lookup"><span data-stu-id="d9064-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Containers and Linux support</a></span></span></td></tr>
</table>

## <a name="next-steps"></a><span data-ttu-id="d9064-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d9064-153">Next steps</span></span>
<span data-ttu-id="d9064-154">Ahora que ha aprendido sobre escenarios y patrones de Service Fabric, obtenga más información sobre cómo demasiado[crear y administrar clústeres](service-fabric-deploy-anywhere.md), [migrar aplicaciones de servicios en la nube tooService tejido](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [configurar la entrega continua](service-fabric-set-up-continuous-integration.md), y [implementar contenedores](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d9064-154">Now that you've learned about Service Fabric patterns and scenarios, read more about how too[create and manage clusters](service-fabric-deploy-anywhere.md), [migrate Cloud Services apps tooService Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [set up continuous delivery](service-fabric-set-up-continuous-integration.md), and [deploy containers](service-fabric-containers-overview.md).</span></span>
