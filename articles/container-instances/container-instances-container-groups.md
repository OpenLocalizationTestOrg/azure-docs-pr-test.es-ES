---
title: aaaAzure grupos del contenedor de instancias de contenedor
description: "Descripción del funcionamiento de los Grupos de contenedores en Azure Container Instances"
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
ms.date: 08/08/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2b0e784609979045c8f77d7b6d0987ec3fee714c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="container-groups-in-azure-container-instances"></a><span data-ttu-id="cbf41-103">Grupos de contenedores en Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="cbf41-103">Container Groups in Azure Container Instances</span></span>

<span data-ttu-id="cbf41-104">recurso de nivel superior de Hello en instancias de contenedor de Azure es un grupo contenedor.</span><span class="sxs-lookup"><span data-stu-id="cbf41-104">hello top-level resource in Azure Container Instances is a container group.</span></span> <span data-ttu-id="cbf41-105">Este artículo describe qué son los grupos de contenedores y qué tipos de escenarios permiten.</span><span class="sxs-lookup"><span data-stu-id="cbf41-105">This article describes what container groups are and what types of scenarios they enable.</span></span>

## <a name="how-a-container-group-works"></a><span data-ttu-id="cbf41-106">Cómo funciona un grupo de contenedores</span><span class="sxs-lookup"><span data-stu-id="cbf41-106">How a container group works</span></span>

<span data-ttu-id="cbf41-107">Un grupo de contenedor es una colección de contenedores que se programan en hello mismo host de máquina y compartir un ciclo de vida, la red local y volúmenes de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="cbf41-107">A container group is a collection of containers that get scheduled on hello same host machine and share a lifecycle, local network, and storage volumes.</span></span> <span data-ttu-id="cbf41-108">Es similar concepto toohello de un *pod* en [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) y [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span><span class="sxs-lookup"><span data-stu-id="cbf41-108">It is similar toohello concept of a *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) and [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span></span>

<span data-ttu-id="cbf41-109">Hello siguiente diagrama muestra un ejemplo de un grupo contenedor que incluye varios contenedores.</span><span class="sxs-lookup"><span data-stu-id="cbf41-109">hello following diagram shows an example of a container group that includes multiple containers.</span></span>

![Ejemplo de grupo de contenedores][container-groups-example]

<span data-ttu-id="cbf41-111">Observe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cbf41-111">Note that:</span></span>

- <span data-ttu-id="cbf41-112">grupo de Hola se programa en una máquina de host único.</span><span class="sxs-lookup"><span data-stu-id="cbf41-112">hello group is scheduled on a single host machine.</span></span>
- <span data-ttu-id="cbf41-113">grupo de Hello expone una única dirección IP pública, con un puerto expuesto.</span><span class="sxs-lookup"><span data-stu-id="cbf41-113">hello group exposes a single public IP address, with one exposed port.</span></span>
- <span data-ttu-id="cbf41-114">grupo de Hola se compone de dos contenedores.</span><span class="sxs-lookup"><span data-stu-id="cbf41-114">hello group is made up of two containers.</span></span> <span data-ttu-id="cbf41-115">Un contenedor de escucha en el puerto 80, mientras Hola otro escucha en el puerto 5000.</span><span class="sxs-lookup"><span data-stu-id="cbf41-115">One container listens on port 80, while hello other listens on port 5000.</span></span>
- <span data-ttu-id="cbf41-116">grupo de Hello incluye dos recursos compartidos de archivos de Azure como montajes de volumen, y cada contenedor monta uno de los recursos compartidos de hello localmente.</span><span class="sxs-lookup"><span data-stu-id="cbf41-116">hello group includes two Azure file shares as volume mounts, and each container mounts one of hello shares locally.</span></span>

### <a name="networking"></a><span data-ttu-id="cbf41-117">Redes</span><span class="sxs-lookup"><span data-stu-id="cbf41-117">Networking</span></span>

<span data-ttu-id="cbf41-118">Los grupos de contenedores comparten una dirección IP y un espacio de nombres de puerto en esa dirección IP.</span><span class="sxs-lookup"><span data-stu-id="cbf41-118">Container groups share an IP address and a port namespace on that IP address.</span></span> <span data-ttu-id="cbf41-119">tooenable los clientes externos tooreach un contenedor en el grupo de hello, debe exponer el puerto de hello en dirección IP de Hola y de contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbf41-119">tooenable external clients tooreach a container within hello group, you must expose hello port on hello IP address and from hello container.</span></span> <span data-ttu-id="cbf41-120">Dado que los contenedores dentro de grupo de hello comparten un espacio de nombres de puerto, no se admite la asignación de puertos.</span><span class="sxs-lookup"><span data-stu-id="cbf41-120">Because containers within hello group share a port namespace, port mapping is not supported.</span></span> <span data-ttu-id="cbf41-121">Contenedores dentro de un grupo pueden llegar a entre sí a través de localhost en hello puertos que han expuesto, incluso si estos puertos no se exponen externamente en dirección IP del grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbf41-121">Containers within a group can reach each other via localhost on hello ports that they have exposed, even if those ports are not exposed externally on hello group's IP address.</span></span>

### <a name="storage"></a><span data-ttu-id="cbf41-122">Storage</span><span class="sxs-lookup"><span data-stu-id="cbf41-122">Storage</span></span>

<span data-ttu-id="cbf41-123">Puede especificar volúmenes externos toomount dentro de un grupo contenedor.</span><span class="sxs-lookup"><span data-stu-id="cbf41-123">You can specify external volumes toomount within a container group.</span></span> <span data-ttu-id="cbf41-124">Puede asignar los volúmenes en rutas de acceso específicas dentro de los contenedores individuales de hello en un grupo.</span><span class="sxs-lookup"><span data-stu-id="cbf41-124">You can map those volumes into specific paths within hello individual containers in a group.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="cbf41-125">Escenarios comunes</span><span class="sxs-lookup"><span data-stu-id="cbf41-125">Common scenarios</span></span>

<span data-ttu-id="cbf41-126">Grupos del contenedor múltiples son útiles en casos donde probablemente prefiera toodivide una sola tarea funcional en un pequeño número de imágenes de contenedor, que se pueden entregar mediante los distintos equipos y tienen requisitos de recursos independiente.</span><span class="sxs-lookup"><span data-stu-id="cbf41-126">Multi-container groups are useful in cases where you want toodivide up a single functional task into a small number of container images, which can be delivered by different teams and have separate resource requirements.</span></span> <span data-ttu-id="cbf41-127">Ejemplos posibles de uso serían:</span><span class="sxs-lookup"><span data-stu-id="cbf41-127">Example usage could include:</span></span>

- <span data-ttu-id="cbf41-128">Un contenedor de aplicación y un contenedor de registro.</span><span class="sxs-lookup"><span data-stu-id="cbf41-128">An application container and a logging container.</span></span> <span data-ttu-id="cbf41-129">contenedor de registro de Hello recopila registros de Hola y resultados de las métricas por aplicación principal hello y los escribe almacenamiento toolong término.</span><span class="sxs-lookup"><span data-stu-id="cbf41-129">hello logging container collects hello logs and metrics output by hello main application and writes them toolong-term storage.</span></span>
- <span data-ttu-id="cbf41-130">Una aplicación y un contenedor de supervisión.</span><span class="sxs-lookup"><span data-stu-id="cbf41-130">An application and a monitoring container.</span></span> <span data-ttu-id="cbf41-131">Hola supervisión periódica del contenedor hace un tooensure de aplicación de toohello de solicitud que se está ejecutando y responder correctamente y genera una alerta si no lo está.</span><span class="sxs-lookup"><span data-stu-id="cbf41-131">hello monitoring container periodically makes a request toohello application tooensure that it's running and responding correctly and raises an alert if it's not.</span></span>
- <span data-ttu-id="cbf41-132">Un contenedor para una aplicación web y un contenedor de extraer contenido más reciente de Hola de control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="cbf41-132">A container serving a web application and a container pulling hello latest content from source control.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbf41-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cbf41-133">Next steps</span></span>

<span data-ttu-id="cbf41-134">Obtenga información acerca de cómo demasiado[implementar un grupo contenedor múltiples](container-instances-multi-container-group.md) con una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cbf41-134">Learn how too[deploy a multi-container group](container-instances-multi-container-group.md) with an Azure Resource Manager template.</span></span>

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png