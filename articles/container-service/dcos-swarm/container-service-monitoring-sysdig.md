---
title: "Supervisión de un clúster de Azure Container Service con Sysdig | Microsoft Docs"
description: "Supervise un clúster del servicio de contenedores de Azure con Sysdig."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenedores, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: e61001161e632a5d2e513107e30f1eaf06103989
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a><span data-ttu-id="1fbf9-104">Supervisión de un clúster del servicio de contenedores de Azure con Sysdig</span><span class="sxs-lookup"><span data-stu-id="1fbf9-104">Monitor an Azure Container Service cluster with Sysdig</span></span>
<span data-ttu-id="1fbf9-105">En este artículo, implementaremos agentes Sysdig en todos los nodos de agente del clúster del servicio de contenedores de Azure.</span><span class="sxs-lookup"><span data-stu-id="1fbf9-105">In this article, we will deploy Sysdig agents to all the agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="1fbf9-106">Necesita una cuenta con Sysdig para esta configuración.</span><span class="sxs-lookup"><span data-stu-id="1fbf9-106">You need an account with Sysdig for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1fbf9-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1fbf9-107">Prerequisites</span></span>
<span data-ttu-id="1fbf9-108">[Implemente](container-service-deployment.md) y [conecte](../container-service-connect.md) un clúster configurado por Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="1fbf9-108">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="1fbf9-109">Explore la [interfaz de usuario de Marathon](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="1fbf9-109">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="1fbf9-110">Vaya a [http://app.sysdigcloud.com](http://app.sysdigcloud.com) para configurar una cuenta en la nube de Sysdig.</span><span class="sxs-lookup"><span data-stu-id="1fbf9-110">Go to [http://app.sysdigcloud.com](http://app.sysdigcloud.com) to set up a Sysdig cloud account.</span></span> 

## <a name="sysdig"></a><span data-ttu-id="1fbf9-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="1fbf9-111">Sysdig</span></span>
<span data-ttu-id="1fbf9-112">Sysdig es un servicio de supervisión que le permite supervisar sus contenedores dentro del clúster.</span><span class="sxs-lookup"><span data-stu-id="1fbf9-112">Sysdig is a monitoring service that allows you to monitor your containers within your cluster.</span></span> <span data-ttu-id="1fbf9-113">Sysdig es conocido por servir para solucionar problemas, pero además incluye métricas de supervisión básicas para la CPU, la red, la memoria y la E/S.</span><span class="sxs-lookup"><span data-stu-id="1fbf9-113">Sysdig is known to help with troubleshooting but it also has your basic monitoring metrics for CPU, Networking, Memory, and I/O.</span></span> <span data-ttu-id="1fbf9-114">Con Sysdig resulta más fácil ver qué contenedores hacen más trabajo o esencialmente cuáles utilizan más memoria y CPU.</span><span class="sxs-lookup"><span data-stu-id="1fbf9-114">Sysdig makes it easy to see which containers are working the hardest or essentially using the most memory and CPU.</span></span> <span data-ttu-id="1fbf9-115">Esta vista se encuentra en la sección "Overview" (Información general), actualmente en versión beta.</span><span class="sxs-lookup"><span data-stu-id="1fbf9-115">This view is in the “Overview” section, which is currently in beta.</span></span> 

![Interfaz de usuario de Sysdig](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a><span data-ttu-id="1fbf9-117">Configuración de una implementación de Sysdig con Marathon</span><span class="sxs-lookup"><span data-stu-id="1fbf9-117">Configure a Sysdig deployment with Marathon</span></span>
<span data-ttu-id="1fbf9-118">Estos pasos muestran cómo configurar e implementar aplicaciones de Sysdig en su clúster con Marathon.</span><span class="sxs-lookup"><span data-stu-id="1fbf9-118">These steps will show you how to configure and deploy Sysdig applications to your cluster with Marathon.</span></span> 

<span data-ttu-id="1fbf9-119">Acceda a la interfaz de usuario de DC/OS mediante [http://localhost:80/](http://localhost:80/). Una vez en la interfaz de usuario de DC/OS, vaya a "Universe" (Universo) en la parte inferior izquierda y busque "Sysdig".</span><span class="sxs-lookup"><span data-stu-id="1fbf9-119">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in the DC/OS UI navigate to the "Universe", which is on the bottom left and then search for "Sysdig."</span></span>

![Sysdig en Universe en DC/OS](./media/container-service-monitoring-sysdig/sysdig1.png)

<span data-ttu-id="1fbf9-121">Ahora, para completar la configuración, necesita una cuenta en la nube de Sysdig o una cuenta de evaluación gratuita.</span><span class="sxs-lookup"><span data-stu-id="1fbf9-121">Now to complete the configuration you need a Sysdig cloud account or a free trial account.</span></span> <span data-ttu-id="1fbf9-122">Una vez que haya iniciado sesión en el sitio web de la nube de Sysdig, haga clic en su nombre de usuario; debería aparecer en la página la clave de acceso (Access Key).</span><span class="sxs-lookup"><span data-stu-id="1fbf9-122">Once you're logged in to the Sysdig cloud website, click on your user name, and on the page you should see your "Access Key."</span></span> 

![Clave de API de Sysdig](./media/container-service-monitoring-sysdig/sysdig2.png) 

<span data-ttu-id="1fbf9-124">Después, escriba la clave de acceso en la configuración de Sysdig dentro de Universe (Universo) en DC/OS.</span><span class="sxs-lookup"><span data-stu-id="1fbf9-124">Next enter your Access Key into the Sysdig configuration within the DC/OS Universe.</span></span> 

![Configuración de Sysdig en Universe en DC/OS](./media/container-service-monitoring-sysdig/sysdig3.png)

<span data-ttu-id="1fbf9-126">Ahora establezca las instancias en 10000000 para que, siempre que se agregue un nuevo nodo al clúster de Sysdig, se implemente automáticamente un agente en ese nodo nuevo.</span><span class="sxs-lookup"><span data-stu-id="1fbf9-126">Now set the instances to 10000000 so whenever a new node is added to the cluster Sysdig will automatically deploy an agent to that new node.</span></span> <span data-ttu-id="1fbf9-127">Se trata de una solución provisional para asegurarse de que Sysdig se implemente en todos los agentes nuevos dentro del clúster.</span><span class="sxs-lookup"><span data-stu-id="1fbf9-127">This is an interim solution to make sure Sysdig will deploy to all new agents within the cluster.</span></span> 

![Configuración de Sysdig en instancias de Universe en DC/OS](./media/container-service-monitoring-sysdig/sysdig4.png)

<span data-ttu-id="1fbf9-129">Una vez que haya instalado el paquete, vuelva a la interfaz de usuario de Sysdig y podrá explorar las diferentes métricas de uso para los contenedores dentro del clúster.</span><span class="sxs-lookup"><span data-stu-id="1fbf9-129">Once you've installed the package navigate back to the Sysdig UI and you'll be able to explore the different usage metrics for the containers within your cluster.</span></span> 

<span data-ttu-id="1fbf9-130">También puede paneles específicos de Mesos y Marathon a través del [nuevo Asistente de panel](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="1fbf9-130">You can also install Mesos and Marathon specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
