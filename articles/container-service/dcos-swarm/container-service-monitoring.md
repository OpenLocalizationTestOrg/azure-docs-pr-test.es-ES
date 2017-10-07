---
title: "clúster de Azure DC/OS aaaMonitor - Datadog | Documentos de Microsoft"
description: "Supervise un clúster del servicio de contenedores de Azure con Datadog. Usar Hola DC/OS web UI toodeploy hello Datadog agentes tooyour clúster."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenedores, DC/OS, Docker Swarm, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 10268c04b5c2ef393429e706ed4a467fff80f718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a><span data-ttu-id="07a70-105">Supervisión de un clúster de DC/OS de Azure Container Service con Datadog</span><span class="sxs-lookup"><span data-stu-id="07a70-105">Monitor an Azure Container Service DC/OS cluster with Datadog</span></span>
<span data-ttu-id="07a70-106">En este artículo se implementará nodos de agente de Datadog agentes tooall hello en el clúster de servicio de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="07a70-106">In this article we will deploy Datadog agents tooall hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="07a70-107">Necesita una cuenta con Datadog para esta configuración.</span><span class="sxs-lookup"><span data-stu-id="07a70-107">You will need an account with Datadog for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="07a70-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="07a70-108">Prerequisites</span></span>
<span data-ttu-id="07a70-109">[Implemente](container-service-deployment.md) y [conecte](../container-service-connect.md) un clúster configurado por Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="07a70-109">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="07a70-110">Explorar hello [interfaz de usuario de maratón](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="07a70-110">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="07a70-111">Vaya demasiado[http://datadoghq.com](http://datadoghq.com) tooset una cuenta de Datadog.</span><span class="sxs-lookup"><span data-stu-id="07a70-111">Go too[http://datadoghq.com](http://datadoghq.com) tooset up a Datadog account.</span></span> 

## <a name="datadog"></a><span data-ttu-id="07a70-112">Datadog</span><span class="sxs-lookup"><span data-stu-id="07a70-112">Datadog</span></span>
<span data-ttu-id="07a70-113">Datadog es un servicio de supervisión que recopila datos de supervisión de los contenedores dentro del clúster del servicio de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="07a70-113">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="07a70-114">Datadog tiene un panel de integración de Docker donde puede ver las métricas específicas dentro de los contenedores.</span><span class="sxs-lookup"><span data-stu-id="07a70-114">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="07a70-115">Las métricas que se recopilan de los contenedores están organizadas por CPU, memoria, red y E/S.</span><span class="sxs-lookup"><span data-stu-id="07a70-115">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="07a70-116">Datadog divide las métricas en contenedores e imágenes.</span><span class="sxs-lookup"><span data-stu-id="07a70-116">Datadog splits metrics into containers and images.</span></span> <span data-ttu-id="07a70-117">Un ejemplo del programa Hola a qué interfaz de usuario parece para CPU uso esté por debajo.</span><span class="sxs-lookup"><span data-stu-id="07a70-117">An example of what hello UI looks like for CPU usage is below.</span></span>

![Interfaz de usuario de Datadog](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a><span data-ttu-id="07a70-119">Configuración de una implementación de Datadog con Marathon</span><span class="sxs-lookup"><span data-stu-id="07a70-119">Configure a Datadog deployment with Marathon</span></span>
<span data-ttu-id="07a70-120">Estos pasos le mostrarán cómo tooconfigure e implementar aplicaciones de Datadog tooyour clúster con maratón.</span><span class="sxs-lookup"><span data-stu-id="07a70-120">These steps will show you how tooconfigure and deploy Datadog applications tooyour cluster with Marathon.</span></span> 

<span data-ttu-id="07a70-121">Acceda a la interfaz de usuario de DC/OS mediante [http://localhost:80/](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="07a70-121">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="07a70-122">Una vez en hello navegar por la interfaz de usuario del controlador de dominio/OS toohello "Universo" que se encuentra en hello inferior izquierdo y, a continuación, busque "Datadog" y haga clic en "Instalar".</span><span class="sxs-lookup"><span data-stu-id="07a70-122">Once in hello DC/OS UI navigate toohello "Universe" which is on hello bottom left and then search for "Datadog" and click "Install."</span></span>

![Paquete de Datadog dentro de hello universo de DC/OS](./media/container-service-monitoring/datadog1.png)

<span data-ttu-id="07a70-124">Ahora toocomplete Hola configuración necesitará una cuenta de Datadog o una cuenta de prueba gratuita.</span><span class="sxs-lookup"><span data-stu-id="07a70-124">Now toocomplete hello configuration you will need a Datadog account or a free trial account.</span></span> <span data-ttu-id="07a70-125">Una vez que ha iniciado sesión en el sitio Web de Datadog toohello buscar toohello izquierda y vaya tooIntegrations ->, a continuación, [API](https://app.datadoghq.com/account/settings#api).</span><span class="sxs-lookup"><span data-stu-id="07a70-125">Once you're logged in toohello Datadog website look toohello left and go tooIntegrations -> then [APIs](https://app.datadoghq.com/account/settings#api).</span></span> 

![Clave de API de Datadog](./media/container-service-monitoring/datadog2.png)

<span data-ttu-id="07a70-127">A continuación, escriba la clave de API en configuración de Datadog de hello en hello universo de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="07a70-127">Next enter your API key into hello Datadog configuration within hello DC/OS Universe.</span></span> 

![Configuración de Datadog Hola universo de DC/OS](./media/container-service-monitoring/datadog3.png) 

<span data-ttu-id="07a70-129">Hola por encima de la configuración de instancias se establecen too10000000 por lo que cada vez que se agrega un nuevo nodo de clúster toohello Datadog implementará automáticamente un nodo de toothat de agente.</span><span class="sxs-lookup"><span data-stu-id="07a70-129">In hello above configuration instances are set too10000000 so whenever a new node is added toohello cluster Datadog will automatically deploy an agent toothat node.</span></span> <span data-ttu-id="07a70-130">Se trata de una solución provisional.</span><span class="sxs-lookup"><span data-stu-id="07a70-130">This is an interim solution.</span></span> <span data-ttu-id="07a70-131">Una vez haya instalado el paquete de hello debe navegar por el sitio Web de Datadog toohello atrás y busque "[paneles](https://app.datadoghq.com/dash/list)."</span><span class="sxs-lookup"><span data-stu-id="07a70-131">Once you've installed hello package you should navigate back toohello Datadog website and find "[Dashboards](https://app.datadoghq.com/dash/list)."</span></span> <span data-ttu-id="07a70-132">Desde allí, verá los paneles de integración y personalizados.</span><span class="sxs-lookup"><span data-stu-id="07a70-132">From there you will see Custom and Integration Dashboards.</span></span> <span data-ttu-id="07a70-133">Hola [panel Docker](https://app.datadoghq.com/screen/integration/docker) tendrá todas las métricas de contenedor de Hola que necesita para supervisar el clúster.</span><span class="sxs-lookup"><span data-stu-id="07a70-133">hello [Docker dashboard](https://app.datadoghq.com/screen/integration/docker) will have all hello container metrics you need for monitoring your cluster.</span></span> 

