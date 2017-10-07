---
title: "información general de instancias de contenedor aaaAzure | Documentos de Azure"
description: "Descripción de Azure Container Instances"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: c0662ede1260b15d9841bfc2c3c4cec4c30338d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances"></a><span data-ttu-id="14779-103">Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="14779-103">Azure Container Instances</span></span>

<span data-ttu-id="14779-104">Los contenedores están convirtiéndose en toopackage de manera Hola preferido, implementar y administrar aplicaciones en la nube.</span><span class="sxs-lookup"><span data-stu-id="14779-104">Containers are quickly becoming hello preferred way toopackage, deploy, and manage cloud applications.</span></span> <span data-ttu-id="14779-105">Instancias de contenedor de Azure ofrece hello más rápido y toorun de forma más sencilla un contenedor en Azure, sin necesidad de tooprovision todas las máquinas virtuales y sin necesidad de tooadopt un servicio de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="14779-105">Azure Container Instances offers hello fastest and simplest way toorun a container in Azure, without having tooprovision any virtual machines and without having tooadopt a higher-level service.</span></span> 

<span data-ttu-id="14779-106">Azure Container Instances es una excelente solución para cualquier escenario que pueda funcionar en contenedores aislados, incluidas las aplicaciones simples, la automatización de tareas y los trabajos de compilación.</span><span class="sxs-lookup"><span data-stu-id="14779-106">Azure Container Instances is a great solution for any scenario that can operate in isolated containers, including simple applications, task automation, and build jobs.</span></span> <span data-ttu-id="14779-107">Para escenarios donde necesita completos orquestación de contenedor, incluida la detección de servicios en varios contenedores, el escalado automático y las actualizaciones de aplicaciones coordinadas, se recomienda hello [servicio de contenedor de Azure](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="14779-107">For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

## <a name="fast-startup-times"></a><span data-ttu-id="14779-108">Tiempos de inicio rápido</span><span class="sxs-lookup"><span data-stu-id="14779-108">Fast startup times</span></span>

<span data-ttu-id="14779-109">Los contenedores ofrecen importantes ventajas de inicio sobre las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="14779-109">Containers offer significant startup benefits over virtual machines.</span></span> <span data-ttu-id="14779-110">Con instancias de contenedor de Azure, puede iniciar un contenedor de Azure en segundos sin Hola necesidad tooprovision y administrar las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="14779-110">With Azure Container Instances, you can start a container in Azure in seconds without hello need tooprovision and manage VMs.</span></span>

## <a name="hypervisor-level-security"></a><span data-ttu-id="14779-111">Seguridad de nivel de hipervisor</span><span class="sxs-lookup"><span data-stu-id="14779-111">Hypervisor-level security</span></span>

<span data-ttu-id="14779-112">Históricamente, los contenedores han ofrecido aislamiento a la dependencia entre aplicaciones y gobierno de recursos, pero no se han considerado suficientemente protegidos para el uso de varios inquilinos hostiles.</span><span class="sxs-lookup"><span data-stu-id="14779-112">Historically, containers have offered application dependency isolation and resource governance but have not been considered sufficiently hardened for hostile multi-tenant usage.</span></span> <span data-ttu-id="14779-113">Con Azure Container Instances, la aplicación está tan aislada en un contenedor como lo estaría en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="14779-113">With Azure Container Instances, your application is as isolated in a container as it would be in a VM.</span></span>

## <a name="custom-sizes"></a><span data-ttu-id="14779-114">Tamaños personalizados</span><span class="sxs-lookup"><span data-stu-id="14779-114">Custom sizes</span></span>

<span data-ttu-id="14779-115">Los contenedores son normalmente optimizado toorun solo una única aplicación, sino necesidades exactas de Hola de esas aplicaciones pueden diferir considerablemente.</span><span class="sxs-lookup"><span data-stu-id="14779-115">Containers are typically optimized toorun just a single application, but hello exact needs of those applications can differ greatly.</span></span> <span data-ttu-id="14779-116">Con Azure Container Instances, puede solicitar exactamente lo que necesita en relación a la memoria y núcleos de CPU.</span><span class="sxs-lookup"><span data-stu-id="14779-116">With Azure Container Instances, you can request exactly what you need in terms of CPU cores and memory.</span></span> <span data-ttu-id="14779-117">Se paga según lo que se solicita, facturado por hello segundo lugar, para que se pueden optimizar con precisión los gastos según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="14779-117">You pay based on what you request, billed by hello second, so you can finely optimize your spending based on your needs.</span></span>

## <a name="public-ip-connectivity"></a><span data-ttu-id="14779-118">Conectividad IP pública</span><span class="sxs-lookup"><span data-stu-id="14779-118">Public IP connectivity</span></span>

<span data-ttu-id="14779-119">Con instancias de contenedor de Azure, puede exponer los contenedores directamente toohello internet con una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="14779-119">With Azure Container Instances, you can expose your containers directly toohello internet with a public IP address.</span></span> <span data-ttu-id="14779-120">Hola futuras, se se expanda nuestra red capacidades tooinclude la integración con redes virtuales, carga equilibradores y otras partes principales de hello Azure infraestructura de red.</span><span class="sxs-lookup"><span data-stu-id="14779-120">In hello future, we will expand our networking capabilities tooinclude integration with virtual networks, load balancers, and other core parts of hello Azure networking infrastructure.</span></span>

## <a name="persistent-storage"></a><span data-ttu-id="14779-121">Almacenamiento persistente</span><span class="sxs-lookup"><span data-stu-id="14779-121">Persistent storage</span></span>

<span data-ttu-id="14779-122">tooretrieve y conservar el estado con instancias de contenedor de Azure, le ofrecemos recursos compartidos de archivos de montaje directo de Azure.</span><span class="sxs-lookup"><span data-stu-id="14779-122">tooretrieve and persist state with Azure Container Instances, we offer direct mounting of Azure files shares.</span></span>

## <a name="linux-and-windows-containers"></a><span data-ttu-id="14779-123">Contenedores de Linux y Windows</span><span class="sxs-lookup"><span data-stu-id="14779-123">Linux and Windows containers</span></span>

<span data-ttu-id="14779-124">Con instancias de contenedor de Azure, puede programar ambas ventanas y contenedores de Linux con Hola misma API.</span><span class="sxs-lookup"><span data-stu-id="14779-124">With Azure Container Instances, you can schedule both Windows and Linux containers with hello same API.</span></span> <span data-ttu-id="14779-125">Simplemente indican el tipo de sistema operativo base de Hola y todo lo demás es idéntica.</span><span class="sxs-lookup"><span data-stu-id="14779-125">Simply indicate hello base OS type and everything else is identical.</span></span>

## <a name="co-scheduled-groups"></a><span data-ttu-id="14779-126">Grupos con programación compartida</span><span class="sxs-lookup"><span data-stu-id="14779-126">Co-scheduled groups</span></span>

<span data-ttu-id="14779-127">Azure Container Instances admite la programación de grupos con varios contenedores que comparten una máquina host, la red local, el almacenamiento y el ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="14779-127">Azure Container Instances supports scheduling of multi-container groups that share a host machine, local network, storage, and lifecycle.</span></span> <span data-ttu-id="14779-128">Esto permite toocombine la aplicación principal con otras personas que actúa en una función auxiliar, como el registro.</span><span class="sxs-lookup"><span data-stu-id="14779-128">This enables you toocombine your main application with others acting in a supporting role, such as logging.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14779-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="14779-129">Next steps</span></span>

<span data-ttu-id="14779-130">Intente implementar un tooAzure de contenedor con un único comando con nuestro [Guía de inicio rápido](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="14779-130">Try deploying a container tooAzure with a single command using our [quickstart guide](container-instances-quickstart.md).</span></span>
