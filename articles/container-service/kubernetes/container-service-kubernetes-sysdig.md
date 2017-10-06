---
title: "clúster de Azure Kubernetes aaaMonitor - Sysdig | Documentos de Microsoft"
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
ms.openlocfilehash: a27813d01ee4624b9e993f6185169ad73aeec3a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a><span data-ttu-id="8c446-103">Supervisión de un clúster de Kubernetes de Azure Container Service con Sysdig</span><span class="sxs-lookup"><span data-stu-id="8c446-103">Monitor an Azure Container Service Kubernetes cluster using Sysdig</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c446-104">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8c446-104">Prerequisites</span></span>
<span data-ttu-id="8c446-105">En este tutorial se da por supuesto que ha [creado un clúster de Kubernetes con Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="8c446-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="8c446-106">También se da por supuesto que tiene hello azure cli y kubectl instaladas las herramientas.</span><span class="sxs-lookup"><span data-stu-id="8c446-106">It also assumes that you have hello azure cli and kubectl tools installed.</span></span>

<span data-ttu-id="8c446-107">Puede probar si tiene hello `az` instalada mediante la ejecución de la herramienta:</span><span class="sxs-lookup"><span data-stu-id="8c446-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="8c446-108">Si no tienes hello `az` herramienta instalada, se ofrecen instrucciones [aquí](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="8c446-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="8c446-109">Puede probar si tiene hello `kubectl` instalada mediante la ejecución de la herramienta:</span><span class="sxs-lookup"><span data-stu-id="8c446-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="8c446-110">Si no tiene la herramienta `kubectl` instalada, puede ejecutar:</span><span class="sxs-lookup"><span data-stu-id="8c446-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a><span data-ttu-id="8c446-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="8c446-111">Sysdig</span></span>
<span data-ttu-id="8c446-112">Sysdig una empresa de servicio de supervisión externa que puede supervisar los contenedores en un clúster de Kubernetes que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="8c446-112">Sysdig is an external monitoring as a service company which can monitor containers in your Kubernetes cluster running in Azure.</span></span> <span data-ttu-id="8c446-113">El uso de Sysdig requiere una cuenta de Sysdig activa.</span><span class="sxs-lookup"><span data-stu-id="8c446-113">Using Sysdig requires an active Sysdig account.</span></span>
<span data-ttu-id="8c446-114">Puede registrarse para obtener una cuenta en su [sitio](https://app.sysdigcloud.com).</span><span class="sxs-lookup"><span data-stu-id="8c446-114">You can sign up for an account on their [site](https://app.sysdigcloud.com).</span></span>

<span data-ttu-id="8c446-115">Una vez que ha iniciado sesión en el sitio Web de toohello Sysdig en la nube, haga clic en su nombre de usuario y, en la página de hello verá la "clave de acceso".</span><span class="sxs-lookup"><span data-stu-id="8c446-115">Once you're logged in toohello Sysdig cloud website, click on your user name, and on hello page you should see your "Access Key."</span></span> 

![Clave de API de Sysdig](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-hello-sysdig-agents-tookubernetes"></a><span data-ttu-id="8c446-117">Instalar agentes tooKubernetes de hello Sysdig</span><span class="sxs-lookup"><span data-stu-id="8c446-117">Installing hello Sysdig agents tooKubernetes</span></span>
<span data-ttu-id="8c446-118">los contenedores, Sysdig ejecuta un proceso en cada equipo utilizando un Kubernetes de toomonitor `DaemonSet`.</span><span class="sxs-lookup"><span data-stu-id="8c446-118">toomonitor your containers, Sysdig runs a process on each machine using a Kubernetes `DaemonSet`.</span></span>
<span data-ttu-id="8c446-119">DaemonSets son objetos de la API de Kubernetes que ejecutan una instancia única de un contenedor por máquina.</span><span class="sxs-lookup"><span data-stu-id="8c446-119">DaemonSets are Kubernetes API objects that run a single instance of a container per machine.</span></span>
<span data-ttu-id="8c446-120">Son perfectos para instalar herramientas como Hola a agente de supervisión de Sysdig.</span><span class="sxs-lookup"><span data-stu-id="8c446-120">They're perfect for installing tools like hello Sysdig's monitoring agent.</span></span>

<span data-ttu-id="8c446-121">tooinstall hello Sysdig daemonset, primero debe descargar [plantilla hello](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) desde sysdig.</span><span class="sxs-lookup"><span data-stu-id="8c446-121">tooinstall hello Sysdig daemonset, you should first download [hello template](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) from sysdig.</span></span> <span data-ttu-id="8c446-122">Guarde el archivo como `sysdig-daemonset.yaml`.</span><span class="sxs-lookup"><span data-stu-id="8c446-122">Save that file as `sysdig-daemonset.yaml`.</span></span>

<span data-ttu-id="8c446-123">En Linux y OS X, puede ejecutar:</span><span class="sxs-lookup"><span data-stu-id="8c446-123">On Linux and OS X you can run:</span></span>

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

<span data-ttu-id="8c446-124">En PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8c446-124">In PowerShell:</span></span>

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

<span data-ttu-id="8c446-125">A continuación editar ese archivo tooinsert su clave de acceso, que obtiene de la cuenta Sysdig.</span><span class="sxs-lookup"><span data-stu-id="8c446-125">Next edit that file tooinsert your Access Key, that you obtained from your Sysdig account.</span></span>

<span data-ttu-id="8c446-126">Por último, cree Hola DaemonSet:</span><span class="sxs-lookup"><span data-stu-id="8c446-126">Finally, create hello DaemonSet:</span></span>

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a><span data-ttu-id="8c446-127">Visualización de la supervisión</span><span class="sxs-lookup"><span data-stu-id="8c446-127">View your monitoring</span></span>
<span data-ttu-id="8c446-128">Una vez instalado y en ejecución, agentes de hello deben bombeo tooSysdig atrás de datos.</span><span class="sxs-lookup"><span data-stu-id="8c446-128">Once installed and running, hello agents should pump data back tooSysdig.</span></span>  <span data-ttu-id="8c446-129">Volver atrás toothe [sysdig panel](https://app.sysdigcloud.com) y debería ver la información acerca de los contenedores.</span><span class="sxs-lookup"><span data-stu-id="8c446-129">Go back toothe [sysdig dashboard](https://app.sysdigcloud.com) and you should see information about your containers.</span></span>

<span data-ttu-id="8c446-130">También puede instalara paneles específicos de Kubernetes a través del [nuevo Asistente de panel](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="8c446-130">You can also install Kubernetes-specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
