---
title: "Supervisión de un clúster de Azure DC/OS - Dynatrace | Microsoft Docs"
description: "Supervisión de un clúster de Azure Container Service DC/OS con Dynatrace. Implemente Dynatrace OneAgent mediante el panel DC/OS."
services: container-service
documentationcenter: 
author: MartinGoodwell
manager: 
editor: 
tags: acs, azure-container-service
keywords: Contenedores, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 6fa23728680779e33eda7bb9aa8a01b9cad9a82b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a><span data-ttu-id="988ed-105">Supervisión de un clúster DC/OS de Azure Container Service con Dynatrace SaaS/Managed</span><span class="sxs-lookup"><span data-stu-id="988ed-105">Monitor an Azure Container Service DC/OS cluster with Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="988ed-106">En este artículo, le mostramos cómo implementar [Dynatrace](https://www.dynatrace.com/) OneAgent para supervisar todos los nodos de agente en el clúster de Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="988ed-106">In this article, we show you how to deploy the [Dynatrace](https://www.dynatrace.com/) OneAgent to monitor all the agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="988ed-107">Necesita una cuenta con Dynatrace SaaS/Managed para esta configuración.</span><span class="sxs-lookup"><span data-stu-id="988ed-107">You need an account with Dynatrace SaaS/Managed for this configuration.</span></span> 

## <a name="dynatrace-saasmanaged"></a><span data-ttu-id="988ed-108">Dynatrace SaaS/Managed</span><span class="sxs-lookup"><span data-stu-id="988ed-108">Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="988ed-109">Dynatrace es una solución de supervisión nativa en la nube para entornos de clúster y contenedor muy dinámicos.</span><span class="sxs-lookup"><span data-stu-id="988ed-109">Dynatrace is a cloud-native monitoring solution for highly dynamic container and cluster environments.</span></span> <span data-ttu-id="988ed-110">Permite optimizar mejor las implementaciones de contenedor y las asignaciones de memoria mediante el uso de datos de uso en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="988ed-110">It allows you to better optimize your container deployments and memory allocations by using real-time usage data.</span></span> <span data-ttu-id="988ed-111">Permite indicar automáticamente los problemas de infraestructura y aplicación proporcionando una línea de base automatizada, la correlación de problemas y la detección de la causa raíz.</span><span class="sxs-lookup"><span data-stu-id="988ed-111">It is capable of automatically pinpointing application and infrastructure issues by providing automated baselining, problem correlation, and root-cause detection.</span></span>

<span data-ttu-id="988ed-112">La figura siguiente muestra la interfaz de usuario de Dynatrace:</span><span class="sxs-lookup"><span data-stu-id="988ed-112">The following figure shows the Dynatrace UI:</span></span>

![Interfaz de usuario de Dynatrace](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a><span data-ttu-id="988ed-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="988ed-114">Prerequisites</span></span> 
<span data-ttu-id="988ed-115">[Implemente](container-service-deployment.md) y [conecte](./../container-service-connect.md) un clúster configurado por Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="988ed-115">[Deploy](container-service-deployment.md) and [connect](./../container-service-connect.md) to a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="988ed-116">Explore la [interfaz de usuario de Marathon](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="988ed-116">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="988ed-117">Vaya a [https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) para configurar una cuenta de Dynatrace SaaS.</span><span class="sxs-lookup"><span data-stu-id="988ed-117">Go to [https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) to set up a Dynatrace SaaS account.</span></span>  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a><span data-ttu-id="988ed-118">Configuración de una implementación de Dynatrace con Marathon</span><span class="sxs-lookup"><span data-stu-id="988ed-118">Configure a Dynatrace deployment with Marathon</span></span>
<span data-ttu-id="988ed-119">Estos pasos muestran cómo configurar e implementar aplicaciones de Dynatrace en su clúster con Marathon.</span><span class="sxs-lookup"><span data-stu-id="988ed-119">These steps show you how to configure and deploy Dynatrace applications to your cluster with Marathon.</span></span>

1. <span data-ttu-id="988ed-120">Acceda a la interfaz de usuario de DC/OS mediante [http://localhost:80/](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="988ed-120">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="988ed-121">Una vez en la interfaz de usuario de DC/OS, navegue hasta la pestaña **Universe** (Universo) y, a continuación, busque **Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="988ed-121">Once in the DC/OS UI, navigate to the **Universe** tab and then search for **Dynatrace**.</span></span>

    ![Dynatrace en Universe (Universo) en DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. <span data-ttu-id="988ed-123">Para completar la configuración, necesita una cuenta de Dynatrace SaaS o una cuenta de evaluación gratuita.</span><span class="sxs-lookup"><span data-stu-id="988ed-123">To complete the configuration, you need a Dynatrace SaaS account or a free trial account.</span></span> <span data-ttu-id="988ed-124">Una vez que haya iniciado sesión en el panel de Dynatrace, seleccione **Implementar Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="988ed-124">Once you log into the Dynatrace dashboard, select **Deploy Dynatrace**.</span></span>

    ![Integración de PaaS de configuración de Dynatrace](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. <span data-ttu-id="988ed-126">En la página, seleccione **Configurar integración de PaaS**.</span><span class="sxs-lookup"><span data-stu-id="988ed-126">On the page, select **Set up PaaS integration**.</span></span> 

    ![Token de la API de Dynatrace](./media/container-service-monitoring-dynatrace/api-token.png) 

4. <span data-ttu-id="988ed-128">Escriba el token de la API en la configuración de Dynatrace OneAgent dentro de Universe (Universo) en DC/OS.</span><span class="sxs-lookup"><span data-stu-id="988ed-128">Enter your API token into the Dynatrace OneAgent configuration within the DC/OS Universe.</span></span> 

    ![Configuración de Dynatrace OneAgent en Universe (Universo) en DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. <span data-ttu-id="988ed-130">Establezca las instancias en el número de nodos que vaya a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="988ed-130">Set the instances to the number of nodes you intend to run.</span></span> <span data-ttu-id="988ed-131">Establecer un número mayor también funciona, pero DC/OS seguirá intentando buscar nuevas instancias hasta que realmente se alcance ese número.</span><span class="sxs-lookup"><span data-stu-id="988ed-131">Setting a higher number also works, but DC/OS will keep trying to find new instances until that number is actually reached.</span></span> <span data-ttu-id="988ed-132">Si lo prefiere, también puede establecerlo en un valor como 1000000.</span><span class="sxs-lookup"><span data-stu-id="988ed-132">If you prefer, you can also set this to a value like 1000000.</span></span> <span data-ttu-id="988ed-133">En este caso, cada vez que se agregue un nuevo nodo al clúster, Dynatrace implementará automáticamente un agente en ese nodo nuevo, a costa de que DC/OS intente constantemente implementar instancias adicionales.</span><span class="sxs-lookup"><span data-stu-id="988ed-133">In this case, whenever a new node is added to the cluster, Dynatrace automatically deploys an agent to that new node, at the price of DC/OS constantly trying to deploy further instances.</span></span>

    ![Configuración de Dynatrace en instancias de Universe en DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a><span data-ttu-id="988ed-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="988ed-135">Next steps</span></span>

<span data-ttu-id="988ed-136">Una vez haya instalado el paquete, desplácese hacia el panel de Dynatrace.</span><span class="sxs-lookup"><span data-stu-id="988ed-136">Once you've installed the package, navigate back to the Dynatrace dashboard.</span></span> <span data-ttu-id="988ed-137">Puede explorar distintas métricas de uso de los contenedores en el clúster.</span><span class="sxs-lookup"><span data-stu-id="988ed-137">You can explore the different usage metrics for the containers within your cluster.</span></span> 