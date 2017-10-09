---
title: "clúster de aaaMonitor un Kubernetes de Azure con CoScale | Documentos de Microsoft"
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
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a><span data-ttu-id="e926d-103">Supervisión de un clúster de Kubernetes de Azure Container Service con CoScale</span><span class="sxs-lookup"><span data-stu-id="e926d-103">Monitor an Azure Container Service Kubernetes cluster with CoScale</span></span>

<span data-ttu-id="e926d-104">En este artículo, le mostraremos cómo hello toodeploy [CoScale](https://www.coscale.com/) toomonitor agente todos los nodos y contenedores en su Kubernetes de clúster en el servicio de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="e926d-104">In this article, we show you how toodeploy hello [CoScale](https://www.coscale.com/) agent toomonitor all nodes and containers in your Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="e926d-105">Para esta configuración se necesita una cuenta con CoScale.</span><span class="sxs-lookup"><span data-stu-id="e926d-105">You need an account with CoScale for this configuration.</span></span> 


## <a name="about-coscale"></a><span data-ttu-id="e926d-106">Acerca de CoScale</span><span class="sxs-lookup"><span data-stu-id="e926d-106">About CoScale</span></span> 

<span data-ttu-id="e926d-107">CoScale es una plataforma de supervisión que recopila métricas y eventos de todos los contenedores de varias plataformas de orquestación.</span><span class="sxs-lookup"><span data-stu-id="e926d-107">CoScale is a monitoring platform that gathers metrics and events from all containers in several orchestration platforms.</span></span> <span data-ttu-id="e926d-108">CoScale ofrece supervisión de toda la pila para los entornos de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e926d-108">CoScale offers full-stack monitoring for Kubernetes environments.</span></span> <span data-ttu-id="e926d-109">Proporciona visualizaciones y análisis para todas las capas de la pila de hello: Hola SO, Kubernetes, Docker y aplicaciones que se ejecutan dentro de los contenedores.</span><span class="sxs-lookup"><span data-stu-id="e926d-109">It provides visualizations and analytics for all layers in hello stack: hello OS, Kubernetes, Docker, and applications running inside your containers.</span></span> <span data-ttu-id="e926d-110">CoScale ofrece varios paneles de supervisión integrados y tiene operadores de tooallow de detección de anomalías integrados y rápida de problemas de infraestructura y las aplicaciones de toofind a los desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="e926d-110">CoScale offers several built-in monitoring dashboards, and it has built-in anomaly detection tooallow operators and developers toofind infrastructure and application issues fast.</span></span>

![Interfaz de usuario de CoScale](./media/container-service-kubernetes-coscale/coscale.png)

<span data-ttu-id="e926d-112">Como se muestra en este artículo, puede instalar a agentes en un toorun de clúster Kubernetes CoScale como una solución de SaaS.</span><span class="sxs-lookup"><span data-stu-id="e926d-112">As shown in this article, you can install agents on a Kubernetes cluster toorun CoScale as a SaaS solution.</span></span> <span data-ttu-id="e926d-113">Si desea que tookeep los datos locales, CoScale también está disponible para la instalación local.</span><span class="sxs-lookup"><span data-stu-id="e926d-113">If you want tookeep your data on-site, CoScale is also available for on-premises installation.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e926d-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e926d-114">Prerequisites</span></span>

<span data-ttu-id="e926d-115">Primero debe demasiado[crear una cuenta de CoScale](https://www.coscale.com/free-trial).</span><span class="sxs-lookup"><span data-stu-id="e926d-115">You first need too[create a CoScale account](https://www.coscale.com/free-trial).</span></span>

<span data-ttu-id="e926d-116">En este tutorial se da por supuesto que ha [creado un clúster de Kubernetes con Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="e926d-116">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="e926d-117">También se supone que dispone de hello `az` CLI de Azure y `kubectl` herramientas instaladas.</span><span class="sxs-lookup"><span data-stu-id="e926d-117">It also assumes that you have hello `az` Azure CLI and `kubectl` tools installed.</span></span>

<span data-ttu-id="e926d-118">Puede probar si tiene hello `az` instalada mediante la ejecución de la herramienta:</span><span class="sxs-lookup"><span data-stu-id="e926d-118">You can test if you have hello `az` tool installed by running:</span></span>

```azurecli
az --version
```

<span data-ttu-id="e926d-119">Si no tienes hello `az` herramienta instalada, se ofrecen instrucciones [aquí](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e926d-119">If you don't have hello `az` tool installed, there are instructions [here](/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="e926d-120">Puede probar si tiene hello `kubectl` instalada mediante la ejecución de la herramienta:</span><span class="sxs-lookup"><span data-stu-id="e926d-120">You can test if you have hello `kubectl` tool installed by running:</span></span>

```bash
kubectl version
```

<span data-ttu-id="e926d-121">Si no tiene la herramienta `kubectl` instalada, puede ejecutar:</span><span class="sxs-lookup"><span data-stu-id="e926d-121">If you don't have `kubectl` installed, you can run:</span></span>

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a><span data-ttu-id="e926d-122">Instalación de agente de hello CoScale con un DaemonSet</span><span class="sxs-lookup"><span data-stu-id="e926d-122">Installing hello CoScale agent with a DaemonSet</span></span>
<span data-ttu-id="e926d-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) están utilizando Kubernetes toorun una sola instancia de un contenedor en cada host de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e926d-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="e926d-124">Son perfectos para ejecutar agentes de supervisión como el agente de CoScale Hola.</span><span class="sxs-lookup"><span data-stu-id="e926d-124">They're perfect for running monitoring agents such as hello CoScale agent.</span></span>

<span data-ttu-id="e926d-125">Después de iniciar sesión en tooCoScale, vaya toohello [página agente](https://app.coscale.com/) agentes de CoScale tooinstall en su clúster mediante un DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="e926d-125">After you log in tooCoScale, go toohello [agent page](https://app.coscale.com/) tooinstall CoScale agents on your cluster using a DaemonSet.</span></span> <span data-ttu-id="e926d-126">Hola CoScale UI proporciona toocreate de pasos de configuración guiada un agente e iniciar la supervisión de su clúster Kubernetes completando.</span><span class="sxs-lookup"><span data-stu-id="e926d-126">hello CoScale UI provides guided configuration steps toocreate an agent and start monitoring your complete Kubernetes cluster.</span></span>

![Configuración del agente de CoScale](./media/container-service-kubernetes-coscale/installation.png)

<span data-ttu-id="e926d-128">toostart Hola agente Hola clúster, ejecute el comando de hello proporcionado:</span><span class="sxs-lookup"><span data-stu-id="e926d-128">toostart hello agent on hello cluster, run hello supplied command:</span></span>

![Iniciar el agente de hello CoScale](./media/container-service-kubernetes-coscale/agent_script.png)

<span data-ttu-id="e926d-130">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="e926d-130">That's it!</span></span> <span data-ttu-id="e926d-131">Una vez que los agentes de hello están activados y ejecutándose, debería ver datos en la consola de hello en unos minutos.</span><span class="sxs-lookup"><span data-stu-id="e926d-131">Once hello agents are up and running, you should see data in hello console in a few minutes.</span></span> <span data-ttu-id="e926d-132">Visite hello [página agente](https://app.coscale.com/) toosee un resumen del clúster, lleve a cabo los pasos de configuración adicional así como paneles como hello **Kubernetes información general del clúster**.</span><span class="sxs-lookup"><span data-stu-id="e926d-132">Visit hello [agent page](https://app.coscale.com/) toosee a summary of your cluster, perform additional configuration steps, and see dashboards such as hello **Kubernetes cluster overview**.</span></span>

![Información general del clúster de Kubernetes](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

<span data-ttu-id="e926d-134">agente de CoScale Hola se implementa automáticamente en nuevas máquinas en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e926d-134">hello CoScale agent is automatically deployed on new machines in hello cluster.</span></span> <span data-ttu-id="e926d-135">Hola las actualizaciones del agente automáticamente cuando se lance una nueva versión.</span><span class="sxs-lookup"><span data-stu-id="e926d-135">hello agent updates automatically when a new version is released.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e926d-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e926d-136">Next steps</span></span>

<span data-ttu-id="e926d-137">Vea hello [CoScale documentación](http://docs.coscale.com/) y [blog](https://www.coscale.com/blog) para obtener más información sobre CoScale soluciones de supervisión.</span><span class="sxs-lookup"><span data-stu-id="e926d-137">See hello [CoScale documentation](http://docs.coscale.com/) and [blog](https://www.coscale.com/blog) for more more information about CoScale monitoring solutions.</span></span> 

