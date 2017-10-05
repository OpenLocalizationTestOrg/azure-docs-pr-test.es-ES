---
title: Grupos de agentes de DC/OS para Azure Container Service | Microsoft Docs
description: "Funcionamiento de los grupos de agentes públicos y privados con un clúster de DC/OS de Azure Container Service."
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
ms.openlocfilehash: da4a196b1a73c78dfff7d8310edcc349b8d10665
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a><span data-ttu-id="92869-104">Grupos de agentes de DC/OS para Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="92869-104">DC/OS agent pools for Azure Container Service</span></span>
<span data-ttu-id="92869-105">Los clústeres de DC/OS en Azure Container Service contienen nodos de agente en dos grupos, uno público y otro privado.</span><span class="sxs-lookup"><span data-stu-id="92869-105">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span></span> <span data-ttu-id="92869-106">Una aplicación se puede implementar en cualquier grupo, lo que afecta a la accesibilidad entre las máquinas del servicio de contenedores.</span><span class="sxs-lookup"><span data-stu-id="92869-106">An application can be deployed to either pool, affecting accessibility between machines in your container service.</span></span> <span data-ttu-id="92869-107">Las máquinas pueden estar expuestas a Internet (públicas) o mantenerse internas (privadas).</span><span class="sxs-lookup"><span data-stu-id="92869-107">The machines can be exposed to the internet (public) or kept internal (private).</span></span> <span data-ttu-id="92869-108">En este artículo se ofrece una breve descripción de por qué hay grupos públicos y privados.</span><span class="sxs-lookup"><span data-stu-id="92869-108">This article gives a brief overview of why there are public and private pools.</span></span>


* <span data-ttu-id="92869-109">**Agentes privados**: los nodos de agentes privados se ejecutan mediante una red no enrutable.</span><span class="sxs-lookup"><span data-stu-id="92869-109">**Private agents**: Private agent nodes run through a non-routable network.</span></span> <span data-ttu-id="92869-110">Esta red solo es accesible desde la zona de administración o a través del enrutador de borde de la zona pública.</span><span class="sxs-lookup"><span data-stu-id="92869-110">This network is only accessible from the admin zone or through the public zone edge router.</span></span> <span data-ttu-id="92869-111">De forma predeterminada, DC/OS inicia aplicaciones en nodos de agente privado.</span><span class="sxs-lookup"><span data-stu-id="92869-111">By default, DC/OS launches apps on private agent nodes.</span></span> 

* <span data-ttu-id="92869-112">**Agentes públicos**: los nodos de agentes públicos ejecutan servicios y aplicaciones de DC/OS por medio de una red de acceso público.</span><span class="sxs-lookup"><span data-stu-id="92869-112">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span></span> 

<span data-ttu-id="92869-113">Para más información sobre la seguridad de red de DC/OS, consulte la [documentación de DC/OS](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span><span class="sxs-lookup"><span data-stu-id="92869-113">For more information about DC/OS network security, see the [DC/OS documentation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span></span>

## <a name="deploy-agent-pools"></a><span data-ttu-id="92869-114">Implementación de grupos de agentes</span><span class="sxs-lookup"><span data-stu-id="92869-114">Deploy agent pools</span></span>

<span data-ttu-id="92869-115">Los grupos de agentes de DC/OS de Azure Container Service se crean de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="92869-115">The DC/OS agent pools In Azure Container Service are created as follows:</span></span>

* <span data-ttu-id="92869-116">El **grupo privado** contiene el número de nodos de agente que especifica cuando [implementa el clúster de DC/OS](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="92869-116">The **private pool** contains the number of agent nodes that you specify when you [deploy the DC/OS cluster](container-service-deployment.md).</span></span> 

* <span data-ttu-id="92869-117">El **grupo público** contiene inicialmente un número predeterminado de nodos de agente.</span><span class="sxs-lookup"><span data-stu-id="92869-117">The **public pool** initially contains a predetermined number of agent nodes.</span></span> <span data-ttu-id="92869-118">Este grupo se agrega automáticamente cuando se aprovisiona el clúster de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="92869-118">This pool is added automatically when the DC/OS cluster is provisioned.</span></span>

<span data-ttu-id="92869-119">El grupo privado y el grupo público son conjuntos de escalado de máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="92869-119">The private pool and the public pool are Azure virtual machine scale sets.</span></span> <span data-ttu-id="92869-120">Puede cambiar el tamaño de estos grupos después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="92869-120">You can resize these pools after deployment.</span></span>

## <a name="use-agent-pools"></a><span data-ttu-id="92869-121">Uso de grupos de agentes</span><span class="sxs-lookup"><span data-stu-id="92869-121">Use agent pools</span></span>
<span data-ttu-id="92869-122">De forma predeterminada, **Marathon** implementa cualquier nueva aplicación en los nodos de agente *privado* .</span><span class="sxs-lookup"><span data-stu-id="92869-122">By default, **Marathon** deploys any new application to the *private* agent nodes.</span></span> <span data-ttu-id="92869-123">Tendrá que implementar explícitamente la aplicación en el nodo *público* durante la creación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="92869-123">You have to explicitly deploy the application to the *public* nodes during the creation of the application.</span></span> <span data-ttu-id="92869-124">Seleccione la pestaña **Opcional** y escriba **slave_public** en el valor **Accepted Resource Roles** (Roles de recursos aceptados).</span><span class="sxs-lookup"><span data-stu-id="92869-124">Select the **Optional** tab and enter **slave_public** for the **Accepted Resource Roles** value.</span></span> <span data-ttu-id="92869-125">Este proceso se describe [aquí](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) y en la documentación de [DC\OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/).</span><span class="sxs-lookup"><span data-stu-id="92869-125">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in the [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92869-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="92869-126">Next steps</span></span>
* <span data-ttu-id="92869-127">Lea sobre cómo [administrar los contenedores de DC/OS](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="92869-127">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

* <span data-ttu-id="92869-128">Aprenda a [abrir el firewall](container-service-enable-public-access.md) proporcionado por Azure para permitir acceso público al contenedor de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="92869-128">Learn how to [open the firewall](container-service-enable-public-access.md) provided by Azure to allow public access to your DC/OS containers.</span></span>

