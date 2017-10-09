---
title: "Instancias de contenedor de aaaAzure y orquestación de contenedor"
description: "Descripción de cómo Azure Container Instances interactúa con orquestadores de contenedores"
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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 69a39edc6f14d885c1ac300990ed1399002ccfee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a><span data-ttu-id="aa9e3-103">Azure Container Instances y orquestadores de contenedores</span><span class="sxs-lookup"><span data-stu-id="aa9e3-103">Azure Container Instances and container orchestrators</span></span>

<span data-ttu-id="aa9e3-104">Los contenedores, debido a su tamaño pequeño y a la orientación de aplicaciones, se adaptan perfectamente a entornos de entrega ágil y arquitecturas basadas en microservicios.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-104">Because of their small size and application orientation, containers are well suited for agile delivery environments and microservice-based architectures.</span></span> <span data-ttu-id="aa9e3-105">tarea de Hello de automatizar y administrar un gran número de contenedores y cómo interactúan se conoce como *orquestación*.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-105">hello task of automating and managing a large number of containers and how they interact is known as *orchestration*.</span></span> <span data-ttu-id="aa9e3-106">Orchestrators contenedor populares incluyen Kubernetes, DC/OS y Docker Swarm, todas ellas están disponibles en hello [servicio de contenedor de Azure](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="aa9e3-106">Popular container orchestrators include Kubernetes, DC/OS, and Docker Swarm, all of which are available in hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

<span data-ttu-id="aa9e3-107">Instancias de contenedor de Azure proporciona algunas hello básico de funcionalidades de plataformas de orquestación de programación, pero no se tratan los servicios de valor más alto de Hola que esas plataformas proporcionan y de hecho pueden ser complementarias con ellos.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-107">Azure Container Instances provides some of hello basic scheduling capabilities of orchestration platforms, but it does not cover hello higher-value services that those platforms provide and can in fact be complementary with them.</span></span> <span data-ttu-id="aa9e3-108">Este artículo describe el ámbito de Hola de lo que controla las instancias de contenedor de Azure y cuánto orchestrators contenedor podrían interactuar con él.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-108">This article describes hello scope of what Azure Container Instances handles and how full container orchestrators might interact with it.</span></span>

## <a name="traditional-orchestration"></a><span data-ttu-id="aa9e3-109">Orquestación tradicional</span><span class="sxs-lookup"><span data-stu-id="aa9e3-109">Traditional orchestration</span></span>

<span data-ttu-id="aa9e3-110">definición estándar de Hola de orquestación incluye Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="aa9e3-110">hello standard definition of orchestration includes hello following tasks:</span></span>

- <span data-ttu-id="aa9e3-111">**Programación**: debido a una imagen de contenedor y una solicitud de recursos, encontrar una máquina adecuada en qué contenedor de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-111">**Scheduling**: Given a container image and a resource request, find a suitable machine on which toorun hello container.</span></span>
- <span data-ttu-id="aa9e3-112">**Afinidad/antiafinidad**: especifique que un conjunto de contenedores se deben ejecutar de manera cercana entre sí (para mejorar el rendimiento) o con la distancia suficiente como para mejorar la disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-112">**Affinity/Anti-affinity**: Specify that a set of containers should run nearby each other (for performance) or sufficiently far apart (for availability).</span></span>
- <span data-ttu-id="aa9e3-113">**Seguimiento de estado**: inspeccione los contenedores por si existen errores y vuelva a programarlos.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-113">**Health monitoring**: Watch for container failures and automatically reschedule them.</span></span>
- <span data-ttu-id="aa9e3-114">**Conmutación por error**: realizar un seguimiento de lo que se ejecuta en cada equipo y volver a programar los contenedores de los nodos de toohealthy de equipos con errores.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-114">**Failover**: Keep track of what is running on each machine and reschedule containers from failed machines toohealthy nodes.</span></span>
- <span data-ttu-id="aa9e3-115">**Ajuste de escala**: agregar o quitar la petición de toomatch de instancias de contenedor, ya sea de forma manual o automática.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-115">**Scaling**: Add or remove container instances toomatch demand, either manually or automatically.</span></span>
- <span data-ttu-id="aa9e3-116">**Redes**: proporcione una red superpuesta para coordinar todas las toocommunicate de contenedores en varios equipos host.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-116">**Networking**: Provide an overlay network for coordinating containers toocommunicate across multiple host machines.</span></span>
- <span data-ttu-id="aa9e3-117">**Detección de servicios**: habilitar contenedores toolocate entre sí automáticamente incluso cuando pasan entre equipos host y cambiar las direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-117">**Service discovery**: Enable containers toolocate each other automatically even as they move between host machines and change IP addresses.</span></span>
- <span data-ttu-id="aa9e3-118">**Coordina las actualizaciones de aplicaciones**: administrar aplicación tooavoid las actualizaciones de contenedor de tiempo de inactividad y habilitar la reversión si algo va mal.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-118">**Coordinated application upgrades**: Manage container upgrades tooavoid application down time and enable rollback if something goes wrong.</span></span>

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a><span data-ttu-id="aa9e3-119">Orquestación con Azure Container Instances: un enfoque por niveles</span><span class="sxs-lookup"><span data-stu-id="aa9e3-119">Orchestration with Azure Container Instances: A layered approach</span></span>

<span data-ttu-id="aa9e3-120">Instancias de contenedor de Azure permite un tooorchestration enfoque por capas, que ofrece toda la programación de Hola y capacidades de administración necesario toorun un único contenedor, permitiendo orchestrator tareas de contenedor múltiples plataformas toomanage sobre él.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-120">Azure Container Instances enables a layered approach tooorchestration, providing all of hello scheduling and management capabilities required toorun a single container, while allowing orchestrator platforms toomanage multi-container tasks on top of it.</span></span>

<span data-ttu-id="aa9e3-121">Porque todos Hola infraestructura subyacente para instancias de contenedor está administrado por Azure, una plataforma de orchestrator no es necesario tooconcern con la búsqueda de una máquina de host correspondiente en qué toorun un único contenedor.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-121">Because all of hello underlying infrastructure for Container Instances is managed by Azure, an orchestrator platform does not need tooconcern itself with finding an appropriate host machine on which toorun a single container.</span></span> <span data-ttu-id="aa9e3-122">elasticidad de Hola de nube de hello garantiza que uno siempre esté disponible.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-122">hello elasticity of hello cloud ensures that one is always available.</span></span> <span data-ttu-id="aa9e3-123">En su lugar, orchestrator Hola puede centrarse en tareas de Hola que simplifican el desarrollo de Hola de contenedor varias arquitecturas, incluido el ajuste y coordina las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-123">Instead, hello orchestrator can focus on hello tasks that simplify hello development of multi-container architectures, including scaling and coordinated upgrades.</span></span>



## <a name="potential-scenarios"></a><span data-ttu-id="aa9e3-124">Escenarios potenciales</span><span class="sxs-lookup"><span data-stu-id="aa9e3-124">Potential scenarios</span></span>

<span data-ttu-id="aa9e3-125">Si bien la integración de los orquestadores con Azure Container Instances todavía es incipiente, podemos prever que surgirán algunos entornos distintos:</span><span class="sxs-lookup"><span data-stu-id="aa9e3-125">While orchestrator integration with Azure Container Instances is still nascent, we anticipate that a few different environments may emerge:</span></span>

### <a name="orchestration-of-container-instances-exclusively"></a><span data-ttu-id="aa9e3-126">Orquestación exclusiva de Container Instances</span><span class="sxs-lookup"><span data-stu-id="aa9e3-126">Orchestration of Container Instances exclusively</span></span>

<span data-ttu-id="aa9e3-127">Dado que se inician rápidamente y facturar por hello segundo, un entorno basado exclusivamente en instancias de contenedor de Azure ofrece inició tooget de manera más rápida de Hola y toodeal con cargas de trabajo muy variables.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-127">Because they start quickly and bill by hello second, an environment based exclusively on Azure Container Instances offers hello fastest way tooget started and toodeal with highly variable workloads.</span></span>

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a><span data-ttu-id="aa9e3-128">Combinación de Container Instances y contenedores en máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="aa9e3-128">Combination of Container Instances and Containers in Virtual Machines</span></span>

<span data-ttu-id="aa9e3-129">De ejecución prolongada, cargas de trabajo estables, orquestar contenedores en un clúster de máquinas virtuales dedicadas suele ser más económico que ejecuta Hola mismos contenedores con instancias de contenedor.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-129">For long-running, stable workloads, orchestrating containers in a cluster of dedicated virtual machines will typically be cheaper than running hello same containers with Container Instances.</span></span> <span data-ttu-id="aa9e3-130">Sin embargo, las instancias de contenedor ofrecen una excelente solución para rápidamente expandir y contraer los toodeal de capacidad total con picos inesperados o de corta duración en el uso.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-130">However, Container Instances offer a great solution for quickly expanding and contracting your overall capacity toodeal with unexpected or short-lived spikes in usage.</span></span> <span data-ttu-id="aa9e3-131">En lugar de escalado horizontal de número de Hola de máquinas virtuales en el clúster, a continuación, implementar contenedores adicionales en dichos equipos, Hola orchestrator puede simplemente programar contenedores adicionales de hello mediante instancias de contenedor y eliminarlos cuando están sin es necesario.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-131">Rather than scaling out hello number of virtual machines in your cluster, then deploying additional containers onto those machines, hello orchestrator can simply schedule hello additional containers using Container Instances and delete them when they're no longer needed.</span></span>

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a><span data-ttu-id="aa9e3-132">Implementación de ejemplo: conector de Azure Container Instances para Kubernetes</span><span class="sxs-lookup"><span data-stu-id="aa9e3-132">Sample implementation: Azure Container Instances Connector for Kubernetes</span></span>

<span data-ttu-id="aa9e3-133">toodemonstrate cómo pueden integrar las plataformas de orquestación de contenedor con instancias de contenedor de Azure, hemos hemos iniciado la creación una [conector de ejemplo para Kubernetes][aci-connector-k8s].</span><span class="sxs-lookup"><span data-stu-id="aa9e3-133">toodemonstrate how container orchestration platforms can integrate with Azure Container Instances, we have started building a [sample connector for Kubernetes][aci-connector-k8s].</span></span> 

<span data-ttu-id="aa9e3-134">Hola conector para Kubernetes imita hello [kubelet] [ kubelet-doc] mediante el registro como un nodo con una capacidad ilimitada y enviar la creación de hello de [pod] [ pod-doc] como grupos del contenedor en instancias de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-134">hello connector for Kubernetes mimics hello [kubelet][kubelet-doc] by registering as a node with unlimited capacity and dispatching hello creation of [pods][pod-doc] as container groups in Azure Container Instances.</span></span> 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

<span data-ttu-id="aa9e3-135">Pudieron crear conectores para otras orchestrators, del mismo modo integrado con alimentación de plataforma primitivas toocombine Hola de orchestrator Hola API con una velocidad de Hola y la simplicidad de la administración de contenedores en instancias de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-135">Connectors for other orchestrators could be built that similarly integrated with platform primitives toocombine hello power of hello orchestrator API with hello speed and simplicity of managing containers in Azure Container Instances.</span></span>

> [!WARNING]
> <span data-ttu-id="aa9e3-136">Hola conector ACI para Kubernetes es *experimental* y no debe usarse en producción.</span><span class="sxs-lookup"><span data-stu-id="aa9e3-136">hello ACI connector for Kubernetes is *experimental* and should not be used in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa9e3-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aa9e3-137">Next steps</span></span>

<span data-ttu-id="aa9e3-138">Crear el primer contenedor con instancias de contenedor de Azure mediante hello [Guía de inicio rápido](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="aa9e3-138">Create your first container with Azure Container Instances using hello [quick start guide](container-instances-quickstart.md).</span></span>

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/