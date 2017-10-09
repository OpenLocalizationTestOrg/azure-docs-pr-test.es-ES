---
title: grupos de agente de aaaDC/OS para el servicio de contenedor de Azure | Documentos de Microsoft
description: "Cómo funcionan los grupos de hello agente públicas y privadas con un clúster de servicio de contenedor de Azure DC/OS"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenedores, microservicios, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: c7d3889db07cb9908e8b68b668bd8a14ef3c2552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a><span data-ttu-id="266d1-104">Grupos de agentes de DC/OS para Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="266d1-104">DC/OS agent pools for Azure Container Service</span></span>
<span data-ttu-id="266d1-105">Los clústeres de DC/OS en Azure Container Service contienen nodos de agente en dos grupos, uno público y otro privado.</span><span class="sxs-lookup"><span data-stu-id="266d1-105">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span></span> <span data-ttu-id="266d1-106">Se puede implementar una aplicación de grupo de tooeither, afectar a su accesibilidad entre máquinas en el servicio de contenedor.</span><span class="sxs-lookup"><span data-stu-id="266d1-106">An application can be deployed tooeither pool, affecting accessibility between machines in your container service.</span></span> <span data-ttu-id="266d1-107">Hello máquinas pueden estar expuesto toohello internet (público) o mantienen interno (privado).</span><span class="sxs-lookup"><span data-stu-id="266d1-107">hello machines can be exposed toohello internet (public) or kept internal (private).</span></span> <span data-ttu-id="266d1-108">En este artículo se ofrece una breve descripción de por qué hay grupos públicos y privados.</span><span class="sxs-lookup"><span data-stu-id="266d1-108">This article gives a brief overview of why there are public and private pools.</span></span>


* <span data-ttu-id="266d1-109">**Agentes privados**: los nodos de agentes privados se ejecutan mediante una red no enrutable.</span><span class="sxs-lookup"><span data-stu-id="266d1-109">**Private agents**: Private agent nodes run through a non-routable network.</span></span> <span data-ttu-id="266d1-110">Esta red solo es accesible desde la zona de administración de Hola o a través de enrutador perimetral de hello zona pública.</span><span class="sxs-lookup"><span data-stu-id="266d1-110">This network is only accessible from hello admin zone or through hello public zone edge router.</span></span> <span data-ttu-id="266d1-111">De forma predeterminada, DC/OS inicia aplicaciones en nodos de agente privado.</span><span class="sxs-lookup"><span data-stu-id="266d1-111">By default, DC/OS launches apps on private agent nodes.</span></span> 

* <span data-ttu-id="266d1-112">**Agentes públicos**: los nodos de agentes públicos ejecutan servicios y aplicaciones de DC/OS por medio de una red de acceso público.</span><span class="sxs-lookup"><span data-stu-id="266d1-112">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span></span> 

<span data-ttu-id="266d1-113">Para obtener más información acerca de la seguridad de red del controlador de dominio/OS, vea hello [documentación del controlador de dominio/OS](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span><span class="sxs-lookup"><span data-stu-id="266d1-113">For more information about DC/OS network security, see hello [DC/OS documentation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span></span>

## <a name="deploy-agent-pools"></a><span data-ttu-id="266d1-114">Implementación de grupos de agentes</span><span class="sxs-lookup"><span data-stu-id="266d1-114">Deploy agent pools</span></span>

<span data-ttu-id="266d1-115">Hola DC/OS agente grupos en el servicio de contenedor de Azure se crean como sigue:</span><span class="sxs-lookup"><span data-stu-id="266d1-115">hello DC/OS agent pools In Azure Container Service are created as follows:</span></span>

* <span data-ttu-id="266d1-116">Hola **grupo privada** contiene Hola número de nodos de agente que especifique cuándo se [implementar Hola DC/OS clúster](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="266d1-116">hello **private pool** contains hello number of agent nodes that you specify when you [deploy hello DC/OS cluster](container-service-deployment.md).</span></span> 

* <span data-ttu-id="266d1-117">Hola **grupo público** inicialmente contiene un número predeterminado de nodos de agente.</span><span class="sxs-lookup"><span data-stu-id="266d1-117">hello **public pool** initially contains a predetermined number of agent nodes.</span></span> <span data-ttu-id="266d1-118">Este grupo se agrega automáticamente cuando se aprovisionan clústeres de Hola DC/OS.</span><span class="sxs-lookup"><span data-stu-id="266d1-118">This pool is added automatically when hello DC/OS cluster is provisioned.</span></span>

<span data-ttu-id="266d1-119">Hola privada grupo y Hola públicos son conjuntos de escalas de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="266d1-119">hello private pool and hello public pool are Azure virtual machine scale sets.</span></span> <span data-ttu-id="266d1-120">Puede cambiar el tamaño de estos grupos después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="266d1-120">You can resize these pools after deployment.</span></span>

## <a name="use-agent-pools"></a><span data-ttu-id="266d1-121">Uso de grupos de agentes</span><span class="sxs-lookup"><span data-stu-id="266d1-121">Use agent pools</span></span>
<span data-ttu-id="266d1-122">De forma predeterminada, **maratón** implementa cualquier toohello de aplicación nueva *privada* nodos de agente.</span><span class="sxs-lookup"><span data-stu-id="266d1-122">By default, **Marathon** deploys any new application toohello *private* agent nodes.</span></span> <span data-ttu-id="266d1-123">Tener tooexplicitly implementar Hola aplicación toohello *público* nodos durante la creación de hello de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="266d1-123">You have tooexplicitly deploy hello application toohello *public* nodes during hello creation of hello application.</span></span> <span data-ttu-id="266d1-124">Seleccione hello **opcional** pestaña y escriba **slave_public** para hello **aceptado recursos Roles** valor.</span><span class="sxs-lookup"><span data-stu-id="266d1-124">Select hello **Optional** tab and enter **slave_public** for hello **Accepted Resource Roles** value.</span></span> <span data-ttu-id="266d1-125">Este proceso está documentado [aquí](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) y Hola [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentación.</span><span class="sxs-lookup"><span data-stu-id="266d1-125">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="266d1-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="266d1-126">Next steps</span></span>
* <span data-ttu-id="266d1-127">Lea sobre cómo [administrar los contenedores de DC/OS](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="266d1-127">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

* <span data-ttu-id="266d1-128">Obtenga información acerca de cómo demasiado[abrir firewall de hello](container-service-enable-public-access.md) ofrecen los contenedores de DC/OS tooyour de Azure tooallow acceso público.</span><span class="sxs-lookup"><span data-stu-id="266d1-128">Learn how too[open hello firewall](container-service-enable-public-access.md) provided by Azure tooallow public access tooyour DC/OS containers.</span></span>

