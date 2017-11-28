---
title: "Supervisión de un clúster de Azure Kubernetes con CoScale | Microsoft Docs"
description: "Supervisión de un clúster de Kubernetes en Azure Container Service mediante CoScale"
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f894191baced710fc0f5a8c8692df98033341a48
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a><span data-ttu-id="e5202-103">Supervisión de un clúster de Kubernetes de Azure Container Service con CoScale</span><span class="sxs-lookup"><span data-stu-id="e5202-103">Monitor an Azure Container Service Kubernetes cluster with CoScale</span></span>

<span data-ttu-id="e5202-104">En este artículo, le mostramos cómo implementar el agente de [CoScale](https://www.coscale.com/) para supervisar todos los nodos y contenedores un clúster de Kubernetes en Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="e5202-104">In this article, we show you how to deploy the [CoScale](https://www.coscale.com/) agent to monitor all nodes and containers in your Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="e5202-105">Para esta configuración se necesita una cuenta con CoScale.</span><span class="sxs-lookup"><span data-stu-id="e5202-105">You need an account with CoScale for this configuration.</span></span> 


## <a name="about-coscale"></a><span data-ttu-id="e5202-106">Acerca de CoScale</span><span class="sxs-lookup"><span data-stu-id="e5202-106">About CoScale</span></span> 

<span data-ttu-id="e5202-107">CoScale es una plataforma de supervisión que recopila métricas y eventos de todos los contenedores de varias plataformas de orquestación.</span><span class="sxs-lookup"><span data-stu-id="e5202-107">CoScale is a monitoring platform that gathers metrics and events from all containers in several orchestration platforms.</span></span> <span data-ttu-id="e5202-108">CoScale ofrece supervisión de toda la pila para los entornos de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e5202-108">CoScale offers full-stack monitoring for Kubernetes environments.</span></span> <span data-ttu-id="e5202-109">Proporciona visualizaciones y análisis a todas las capas de la pila: el sistema operativo, Kubernetes, Docker y aplicaciones que se ejecutan en los contenedores.</span><span class="sxs-lookup"><span data-stu-id="e5202-109">It provides visualizations and analytics for all layers in the stack: the OS, Kubernetes, Docker, and applications running inside your containers.</span></span> <span data-ttu-id="e5202-110">CoScale ofrece varios paneles de supervisión integrados y tiene la función de detección de anomalías integrada para permitir a los operadores y los desarrolladores encontrar rápidamente problemas en la infraestructura y las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e5202-110">CoScale offers several built-in monitoring dashboards, and it has built-in anomaly detection to allow operators and developers to find infrastructure and application issues fast.</span></span>

![Interfaz de usuario de CoScale](./media/container-service-kubernetes-coscale/coscale.png)

<span data-ttu-id="e5202-112">Como se muestra en este artículo, se pueden instalar agentes en un clúster de Kubernetes para ejecutar CoScale como solución de SaaS.</span><span class="sxs-lookup"><span data-stu-id="e5202-112">As shown in this article, you can install agents on a Kubernetes cluster to run CoScale as a SaaS solution.</span></span> <span data-ttu-id="e5202-113">Si desea conservar los datos en un entorno local, CoScale también estará disponible para su instalación local.</span><span class="sxs-lookup"><span data-stu-id="e5202-113">If you want to keep your data on-site, CoScale is also available for on-premises installation.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e5202-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e5202-114">Prerequisites</span></span>

<span data-ttu-id="e5202-115">En primer lugar, es preciso [crear una cuenta de CoScale](https://www.coscale.com/free-trial).</span><span class="sxs-lookup"><span data-stu-id="e5202-115">You first need to [create a CoScale account](https://www.coscale.com/free-trial).</span></span>

<span data-ttu-id="e5202-116">En este tutorial se da por supuesto que ha [creado un clúster de Kubernetes con Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="e5202-116">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="e5202-117">También se asume que tiene la CLI de Azure `az` y las herramientas de `kubectl` instaladas.</span><span class="sxs-lookup"><span data-stu-id="e5202-117">It also assumes that you have the `az` Azure CLI and `kubectl` tools installed.</span></span>

<span data-ttu-id="e5202-118">Puede probar si tiene la herramienta `az` instalada mediante la ejecución de:</span><span class="sxs-lookup"><span data-stu-id="e5202-118">You can test if you have the `az` tool installed by running:</span></span>

```azurecli
az --version
```

<span data-ttu-id="e5202-119">Si no tiene la herramienta `az` instalada, se ofrecen instrucciones [aquí](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e5202-119">If you don't have the `az` tool installed, there are instructions [here](/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="e5202-120">Puede probar si tiene la herramienta `kubectl` instalada mediante la ejecución de:</span><span class="sxs-lookup"><span data-stu-id="e5202-120">You can test if you have the `kubectl` tool installed by running:</span></span>

```bash
kubectl version
```

<span data-ttu-id="e5202-121">Si no tiene la herramienta `kubectl` instalada, puede ejecutar:</span><span class="sxs-lookup"><span data-stu-id="e5202-121">If you don't have `kubectl` installed, you can run:</span></span>

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-the-coscale-agent-with-a-daemonset"></a><span data-ttu-id="e5202-122">Instalación del agente de CoScale con un DaemonSet</span><span class="sxs-lookup"><span data-stu-id="e5202-122">Installing the CoScale agent with a DaemonSet</span></span>
<span data-ttu-id="e5202-123">Kubernetes utiliza los [DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) para ejecutar una única instancia de un contenedor en cada host del clúster.</span><span class="sxs-lookup"><span data-stu-id="e5202-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) are used by Kubernetes to run a single instance of a container on each host in the cluster.</span></span>
<span data-ttu-id="e5202-124">Son perfectos para ejecutar agentes de supervisión como el agente de CoScale.</span><span class="sxs-lookup"><span data-stu-id="e5202-124">They're perfect for running monitoring agents such as the CoScale agent.</span></span>

<span data-ttu-id="e5202-125">Después de iniciar sesión en CoScale, vaya a la [página de los agentes](https://app.coscale.com/) para instalar agentes de CoScale en su clúster mediante un DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="e5202-125">After you log in to CoScale, go to the [agent page](https://app.coscale.com/) to install CoScale agents on your cluster using a DaemonSet.</span></span> <span data-ttu-id="e5202-126">La interfaz de usuario de CoScale proporciona pasos de configuración guiada para crear a un agente y comenzar a supervisar todo el clúster de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e5202-126">The CoScale UI provides guided configuration steps to create an agent and start monitoring your complete Kubernetes cluster.</span></span>

![Configuración del agente de CoScale](./media/container-service-kubernetes-coscale/installation.png)

<span data-ttu-id="e5202-128">Para iniciar al agente en el clúster, ejecute el comando suministrado para tal fin:</span><span class="sxs-lookup"><span data-stu-id="e5202-128">To start the agent on the cluster, run the supplied command:</span></span>

![Inicie al agente de CoScale](./media/container-service-kubernetes-coscale/agent_script.png)

<span data-ttu-id="e5202-130">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="e5202-130">That's it!</span></span> <span data-ttu-id="e5202-131">Una vez que los agentes están en funcionamiento debería ver datos en la consola durante unos minutos.</span><span class="sxs-lookup"><span data-stu-id="e5202-131">Once the agents are up and running, you should see data in the console in a few minutes.</span></span> <span data-ttu-id="e5202-132">Visite la [página de los agentes](https://app.coscale.com/) para ver un resumen del clúster, realizar los pasos de configuración adicionales y ver los paneles, como la **información general del clúster de Kubernetes**.</span><span class="sxs-lookup"><span data-stu-id="e5202-132">Visit the [agent page](https://app.coscale.com/) to see a summary of your cluster, perform additional configuration steps, and see dashboards such as the **Kubernetes cluster overview**.</span></span>

![Información general del clúster de Kubernetes](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

<span data-ttu-id="e5202-134">El agente de CoScale se implementa automáticamente en las máquinas nuevas del clúster.</span><span class="sxs-lookup"><span data-stu-id="e5202-134">The CoScale agent is automatically deployed on new machines in the cluster.</span></span> <span data-ttu-id="e5202-135">El agente se actualiza automáticamente cuando se lanza una versión nueva.</span><span class="sxs-lookup"><span data-stu-id="e5202-135">The agent updates automatically when a new version is released.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e5202-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e5202-136">Next steps</span></span>

<span data-ttu-id="e5202-137">Consulte la [documentación de CoScale](http://docs.coscale.com/) y [blog](https://www.coscale.com/blog) para más información sobre las soluciones de supervisión de CoScale.</span><span class="sxs-lookup"><span data-stu-id="e5202-137">See the [CoScale documentation](http://docs.coscale.com/) and [blog](https://www.coscale.com/blog) for more more information about CoScale monitoring solutions.</span></span> 

