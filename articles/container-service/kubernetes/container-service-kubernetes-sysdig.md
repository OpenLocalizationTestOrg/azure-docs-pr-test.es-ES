---
title: "Supervisión de un clúster de Azure Kubernetes - Sysdig | Microsoft Docs"
description: "Supervisión de un clúster de Kubernetes en Azure Container Service utilizando Sysdig"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: afe22b84015526f901111238e36baaa94694ccbf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a><span data-ttu-id="8a089-103">Supervisión de un clúster de Kubernetes de Azure Container Service con Sysdig</span><span class="sxs-lookup"><span data-stu-id="8a089-103">Monitor an Azure Container Service Kubernetes cluster using Sysdig</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a089-104">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8a089-104">Prerequisites</span></span>
<span data-ttu-id="8a089-105">En este tutorial se da por supuesto que ha [creado un clúster de Kubernetes con Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="8a089-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="8a089-106">También se da por supuesto que tiene herramientas de kubectl y de la CLI de Azure instaladas.</span><span class="sxs-lookup"><span data-stu-id="8a089-106">It also assumes that you have the azure cli and kubectl tools installed.</span></span>

<span data-ttu-id="8a089-107">Puede probar si tiene la herramienta `az` instalada mediante la ejecución de:</span><span class="sxs-lookup"><span data-stu-id="8a089-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="8a089-108">Si no tiene la herramienta `az` instalada, se ofrecen instrucciones [aquí](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="8a089-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="8a089-109">Puede probar si tiene la herramienta `kubectl` instalada mediante la ejecución de:</span><span class="sxs-lookup"><span data-stu-id="8a089-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="8a089-110">Si no tiene la herramienta `kubectl` instalada, puede ejecutar:</span><span class="sxs-lookup"><span data-stu-id="8a089-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a><span data-ttu-id="8a089-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="8a089-111">Sysdig</span></span>
<span data-ttu-id="8a089-112">Sysdig una empresa de servicio de supervisión externa que puede supervisar los contenedores en un clúster de Kubernetes que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="8a089-112">Sysdig is an external monitoring as a service company which can monitor containers in your Kubernetes cluster running in Azure.</span></span> <span data-ttu-id="8a089-113">El uso de Sysdig requiere una cuenta de Sysdig activa.</span><span class="sxs-lookup"><span data-stu-id="8a089-113">Using Sysdig requires an active Sysdig account.</span></span>
<span data-ttu-id="8a089-114">Puede registrarse para obtener una cuenta en su [sitio](https://app.sysdigcloud.com).</span><span class="sxs-lookup"><span data-stu-id="8a089-114">You can sign up for an account on their [site](https://app.sysdigcloud.com).</span></span>

<span data-ttu-id="8a089-115">Una vez que haya iniciado sesión en el sitio web de la nube de Sysdig, haga clic en su nombre de usuario; debería aparecer en la página la clave de acceso (Access Key).</span><span class="sxs-lookup"><span data-stu-id="8a089-115">Once you're logged in to the Sysdig cloud website, click on your user name, and on the page you should see your "Access Key."</span></span> 

![Clave de API de Sysdig](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-the-sysdig-agents-to-kubernetes"></a><span data-ttu-id="8a089-117">Instalación de los agentes Sysdig en Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8a089-117">Installing the Sysdig agents to Kubernetes</span></span>
<span data-ttu-id="8a089-118">Para supervisar los contenedores, Sysdig ejecuta un proceso en cada equipo con un `DaemonSet` de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="8a089-118">To monitor your containers, Sysdig runs a process on each machine using a Kubernetes `DaemonSet`.</span></span>
<span data-ttu-id="8a089-119">DaemonSets son objetos de la API de Kubernetes que ejecutan una instancia única de un contenedor por máquina.</span><span class="sxs-lookup"><span data-stu-id="8a089-119">DaemonSets are Kubernetes API objects that run a single instance of a container per machine.</span></span>
<span data-ttu-id="8a089-120">Son perfectos para instalar herramientas como el agente de supervisión de Sysdig.</span><span class="sxs-lookup"><span data-stu-id="8a089-120">They're perfect for installing tools like the Sysdig's monitoring agent.</span></span>

<span data-ttu-id="8a089-121">Para instalar el daemonset Sysdig, primero debe descargar [la plantilla](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) desde sysdig.</span><span class="sxs-lookup"><span data-stu-id="8a089-121">To install the Sysdig daemonset, you should first download [the template](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) from sysdig.</span></span> <span data-ttu-id="8a089-122">Guarde el archivo como `sysdig-daemonset.yaml`.</span><span class="sxs-lookup"><span data-stu-id="8a089-122">Save that file as `sysdig-daemonset.yaml`.</span></span>

<span data-ttu-id="8a089-123">En Linux y OS X, puede ejecutar:</span><span class="sxs-lookup"><span data-stu-id="8a089-123">On Linux and OS X you can run:</span></span>

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

<span data-ttu-id="8a089-124">En PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8a089-124">In PowerShell:</span></span>

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

<span data-ttu-id="8a089-125">A continuación, modifique ese archivo para insertar la clave de acceso que obtuvo de la cuenta Sysdig.</span><span class="sxs-lookup"><span data-stu-id="8a089-125">Next edit that file to insert your Access Key, that you obtained from your Sysdig account.</span></span>

<span data-ttu-id="8a089-126">Por último, cree el DaemonSet:</span><span class="sxs-lookup"><span data-stu-id="8a089-126">Finally, create the DaemonSet:</span></span>

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a><span data-ttu-id="8a089-127">Visualización de la supervisión</span><span class="sxs-lookup"><span data-stu-id="8a089-127">View your monitoring</span></span>
<span data-ttu-id="8a089-128">Una vez instalados y en ejecución, los agentes deben bombear datos a Sysdig.</span><span class="sxs-lookup"><span data-stu-id="8a089-128">Once installed and running, the agents should pump data back to Sysdig.</span></span>  <span data-ttu-id="8a089-129">Vuelva al [panel de sysdig](https://app.sysdigcloud.com) y debería ver la información acerca de los contenedores.</span><span class="sxs-lookup"><span data-stu-id="8a089-129">Go back to the [sysdig dashboard](https://app.sysdigcloud.com) and you should see information about your containers.</span></span>

<span data-ttu-id="8a089-130">También puede instalara paneles específicos de Kubernetes a través del [nuevo Asistente de panel](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="8a089-130">You can also install Kubernetes-specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
