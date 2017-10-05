---
title: Patrones y escenarios de Azure Service Fabric | Microsoft Docs
description: "Conozca los mejores procedimientos y los patrones probados y reutilizables para diseñar, desarrollar y utilizar microservicios en Service Fabric."
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
ms.openlocfilehash: fb2fa495758433e357722427b1c162420935955d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-patterns-and-scenarios"></a><span data-ttu-id="18095-103">Escenarios y patrones de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="18095-103">Service Fabric patterns and scenarios</span></span>
<span data-ttu-id="18095-104">Si está pensando en crear microservicios a gran escala mediante Azure Service Fabric, aprenda de la mano de los expertos que diseñaron y construyeron esta plataforma como servicio (PaaS).</span><span class="sxs-lookup"><span data-stu-id="18095-104">If you’re looking at building large-scale microservices using Azure Service Fabric, learn from the experts who designed and built this platform as a service (PaaS).</span></span> <span data-ttu-id="18095-105">Comience con la arquitectura adecuada y aprenda luego a optimizar los recursos de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="18095-105">Get started with proper architecture, and then learn how to optimize resources for your application.</span></span> <span data-ttu-id="18095-106">El curso de [patrones y procedimientos de Service Fabric](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) da respuesta a las preguntas más frecuentes que plantean los clientes del mundo real sobre los escenarios y las áreas de aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="18095-106">The [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) course answers the questions most often asked by real-world customers about Service Fabric scenarios and application areas.</span></span>
 
<span data-ttu-id="18095-107">Averigüe cómo diseñar, desarrollar y usar sus microservicios en Service Fabric mediante procedimientos recomendados y patrones probados y reutilizables.</span><span class="sxs-lookup"><span data-stu-id="18095-107">Find out how to design, develop, and operate your microservices on Service Fabric using best practices and proven, reusable patterns.</span></span> <span data-ttu-id="18095-108">Obtenga una introducción a Service Fabric y luego profundice en temas que abarcan la optimización y la seguridad del clúster, la migración de aplicaciones heredadas, IoT a escala, el hospedaje de motores de juegos, etc.</span><span class="sxs-lookup"><span data-stu-id="18095-108">Get an overview of Service Fabric and then dive deep into topics that cover cluster optimization and security, migrating legacy apps, IoT at scale, hosting game engines, and more.</span></span> <span data-ttu-id="18095-109">Examine la entrega continua de diversas cargas de trabajo y obtenga incluso detalles sobre la compatibilidad con Linux y los contenedores.</span><span class="sxs-lookup"><span data-stu-id="18095-109">Look at continuous delivery for various workloads, and even get the details on Linux support and containers.</span></span> 

## <a name="introduction"></a><span data-ttu-id="18095-110">Introducción</span><span class="sxs-lookup"><span data-stu-id="18095-110">Introduction</span></span>
<span data-ttu-id="18095-111">Examine los procedimientos recomendados y sepa cómo elegir plataforma como servicio (PaaS) sobre infraestructura cómo servicio (IaaS).</span><span class="sxs-lookup"><span data-stu-id="18095-111">Explore best practices, and learn about choosing platform as a service (PaaS) over infrastructure as a service (IaaS).</span></span> <span data-ttu-id="18095-112">Obtenga los detalles sobre los siguientes principios de diseño de aplicaciones probados.</span><span class="sxs-lookup"><span data-stu-id="18095-112">Get the details on following proven application design principles.</span></span>

<table><tr><th><span data-ttu-id="18095-113">Vídeo</span><span class="sxs-lookup"><span data-stu-id="18095-113">Video</span></span></th><th><span data-ttu-id="18095-114">Lote de PowerPoint</span><span class="sxs-lookup"><span data-stu-id="18095-114">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="./media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="18095-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introducción a Service Fabric</a></span><span class="sxs-lookup"><span data-stu-id="18095-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduction to Service Fabric</a></span></span></td></tr>
</table>

## <a name="cluster-planning-and-management"></a><span data-ttu-id="18095-116">Planeamiento y administración de clústeres</span><span class="sxs-lookup"><span data-stu-id="18095-116">Cluster planning and management</span></span>
<span data-ttu-id="18095-117">Aprenda sobre el planeamiento de la capacidad, la optimización del clúster y la seguridad del clúster en Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="18095-117">Learn about capacity planning, cluster optimization, and cluster security, in this look at Azure Service Fabric.</span></span>

<table><tr><th><span data-ttu-id="18095-118">Vídeo</span><span class="sxs-lookup"><span data-stu-id="18095-118">Video</span></span></th><th><span data-ttu-id="18095-119">Lote de PowerPoint</span><span class="sxs-lookup"><span data-stu-id="18095-119">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="./media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <span data-ttu-id="18095-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Planeamiento y administración de clústeres</a></span><span class="sxs-lookup"><span data-stu-id="18095-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Cluster Planning and Management</a></span></span></td></tr>
</table>

## <a name="hyper-scale-web"></a><span data-ttu-id="18095-121">Web a hiperescala</span><span class="sxs-lookup"><span data-stu-id="18095-121">Hyper-scale web</span></span>
<span data-ttu-id="18095-122">Repase conceptos en torno a web a hiperescala, como disponibilidad y confiabilidad, hiperescala y administración de estado.</span><span class="sxs-lookup"><span data-stu-id="18095-122">Review concepts around hyper-scale web, including availability and reliability, hyper-scale, and state management.</span></span>

<table><tr><th><span data-ttu-id="18095-123">Vídeo</span><span class="sxs-lookup"><span data-stu-id="18095-123">Video</span></span></th><th><span data-ttu-id="18095-124">Lote de PowerPoint</span><span class="sxs-lookup"><span data-stu-id="18095-124">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="./media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="18095-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Web a hiperescala</a></span><span class="sxs-lookup"><span data-stu-id="18095-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Hyper-scale web</a></span></span></td></tr>
</table>

## <a name="iot"></a><span data-ttu-id="18095-126">IoT</span><span class="sxs-lookup"><span data-stu-id="18095-126">IoT</span></span>
<span data-ttu-id="18095-127">Explore la Internet de las cosas (IoT) en el contexto de Azure Service Fabric, como la canalización de Azure IoT, el servicio multiinquilino e IoT a escala.</span><span class="sxs-lookup"><span data-stu-id="18095-127">Explore the Internet of Things (IoT) in the context of Azure Service Fabric, including the Azure IoT pipeline, multi-tenancy, and IoT at scale.</span></span>

<table><tr><th><span data-ttu-id="18095-128">Vídeo</span><span class="sxs-lookup"><span data-stu-id="18095-128">Video</span></span></th><th><span data-ttu-id="18095-129">Lote de PowerPoint</span><span class="sxs-lookup"><span data-stu-id="18095-129">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="./media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="18095-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span><span class="sxs-lookup"><span data-stu-id="18095-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span></span></td></tr>
</table>

## <a name="gaming"></a><span data-ttu-id="18095-131">Juegos</span><span class="sxs-lookup"><span data-stu-id="18095-131">Gaming</span></span>
<span data-ttu-id="18095-132">Examine juegos basados en turnos, juegos interactivos y hospedaje de motores de juegos existentes.</span><span class="sxs-lookup"><span data-stu-id="18095-132">Look at turn-based games, interactive games, and hosting existing game engines.</span></span>

<table><tr><th><span data-ttu-id="18095-133">Vídeo</span><span class="sxs-lookup"><span data-stu-id="18095-133">Video</span></span></th><th><span data-ttu-id="18095-134">Lote de PowerPoint</span><span class="sxs-lookup"><span data-stu-id="18095-134">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="./media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="18095-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Juegos</a></span><span class="sxs-lookup"><span data-stu-id="18095-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gaming</a></span></span></td></tr>
</table>

## <a name="continuous-delivery"></a><span data-ttu-id="18095-136">Entrega continua</span><span class="sxs-lookup"><span data-stu-id="18095-136">Continuous delivery</span></span>
<span data-ttu-id="18095-137">Explore conceptos, como integración continua/entrega continua con Visual Studio Team Services, compilación/empaquetado/publicación de flujos de trabajo, configuración en varios entornos y empaquetado/uso compartido de servicios.</span><span class="sxs-lookup"><span data-stu-id="18095-137">Explore concepts, including continuous integration/continuous delivery with Visual Studio Team Services, build/package/publish workflow, multi-environment setup, and service package/share.</span></span>

<table><tr><th><span data-ttu-id="18095-138">Vídeo</span><span class="sxs-lookup"><span data-stu-id="18095-138">Video</span></span></th><th><span data-ttu-id="18095-139">Lote de PowerPoint</span><span class="sxs-lookup"><span data-stu-id="18095-139">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="18095-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Entrega continua</a></span><span class="sxs-lookup"><span data-stu-id="18095-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Continuous delivery</a></span></span></td></tr>
</table>

## <a name="migration"></a><span data-ttu-id="18095-141">Migración</span><span class="sxs-lookup"><span data-stu-id="18095-141">Migration</span></span>
<span data-ttu-id="18095-142">Aprenda sobre la migración desde un servicio en la nube, además de la migración de aplicaciones heredadas.</span><span class="sxs-lookup"><span data-stu-id="18095-142">Learn about migrating from a cloud service, in addition to migration of legacy apps.</span></span>

<table><tr><th><span data-ttu-id="18095-143">Vídeo</span><span class="sxs-lookup"><span data-stu-id="18095-143">Video</span></span></th><th><span data-ttu-id="18095-144">Lote de PowerPoint</span><span class="sxs-lookup"><span data-stu-id="18095-144">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="./media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="18095-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migración</a></span><span class="sxs-lookup"><span data-stu-id="18095-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migration</a></span></span></td></tr>
</table>

## <a name="containers-and-linux-support"></a><span data-ttu-id="18095-146">Contenedores y compatibilidad con Linux</span><span class="sxs-lookup"><span data-stu-id="18095-146">Containers and Linux support</span></span>
<span data-ttu-id="18095-147">Conozca la respuesta a la pregunta: "¿Por qué contenedores?"</span><span class="sxs-lookup"><span data-stu-id="18095-147">Get the answer to the question, "Why containers?"</span></span> <span data-ttu-id="18095-148">Aprenda sobre la versión preliminar de contenedores de Windows, la compatibilidad con Linux y la organización de contenedores de Linux.</span><span class="sxs-lookup"><span data-stu-id="18095-148">Learn about the preview for Windows containers, Linux supports, and Linux containers orchestration.</span></span> <span data-ttu-id="18095-149">Además, descubra cómo migrar aplicaciones de .NET Core a Linux.</span><span class="sxs-lookup"><span data-stu-id="18095-149">Plus, find out how to migrate .NET Core apps to Linux.</span></span>

<table><tr><th><span data-ttu-id="18095-150">Vídeo</span><span class="sxs-lookup"><span data-stu-id="18095-150">Video</span></span></th><th><span data-ttu-id="18095-151">Lote de PowerPoint</span><span class="sxs-lookup"><span data-stu-id="18095-151">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="18095-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Contenedores y compatibilidad con Linux</a></span><span class="sxs-lookup"><span data-stu-id="18095-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Containers and Linux support</a></span></span></td></tr>
</table>

## <a name="next-steps"></a><span data-ttu-id="18095-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18095-153">Next steps</span></span>
<span data-ttu-id="18095-154">Ahora que ha aprendido sobre los patrones y escenarios de Service Fabric, lea más sobre cómo [crear y administrar clústeres](service-fabric-deploy-anywhere.md), [migrar aplicaciones de Cloud Services a Service Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [configurar la entrega continua](service-fabric-set-up-continuous-integration.md) e [implementar contenedores](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="18095-154">Now that you've learned about Service Fabric patterns and scenarios, read more about how to [create and manage clusters](service-fabric-deploy-anywhere.md), [migrate Cloud Services apps to Service Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [set up continuous delivery](service-fabric-set-up-continuous-integration.md), and [deploy containers](service-fabric-containers-overview.md).</span></span>
