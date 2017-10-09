---
title: "tutorial de servicio de contenedor de aaaAzure - implementar clústeres | Documentos de Microsoft"
description: "Tutorial de Azure Container Service: Implementación de clúster"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenedores, microservicios, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c4c8cc95c88d9c2077d0322f57e5d3159e2dd0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="ebda8-104">Implementación de un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="ebda8-104">Deploy a Kubernetes cluster in Azure Container Service</span></span>

<span data-ttu-id="ebda8-105">Kubernetes proporciona una plataforma distribuida para aplicaciones en contenedores.</span><span class="sxs-lookup"><span data-stu-id="ebda8-105">Kubernetes provides a distributed platform for containerized applications.</span></span> <span data-ttu-id="ebda8-106">Con Azure Container Service, el aprovisionamiento de un clúster de Kubernetes listo para producción se realiza de forma rápida y sencilla.</span><span class="sxs-lookup"><span data-stu-id="ebda8-106">With Azure Container Service, provisioning of a production ready Kubernetes cluster is simple and quick.</span></span> <span data-ttu-id="ebda8-107">En este tutorial, la tercera parte de siete, se implementa un clúster de Kubernetes de Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="ebda8-107">In this tutorial, part 3 of 7, an Azure Container Service Kubernetes cluster is deployed.</span></span> <span data-ttu-id="ebda8-108">Los pasos completados incluyen:</span><span class="sxs-lookup"><span data-stu-id="ebda8-108">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ebda8-109">Implementación de un clúster de ACS de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ebda8-109">Deploying a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="ebda8-110">Instalación de hello Kubernetes CLI (kubectl)</span><span class="sxs-lookup"><span data-stu-id="ebda8-110">Installation of hello Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="ebda8-111">Configuración de kubectl</span><span class="sxs-lookup"><span data-stu-id="ebda8-111">Configuration of kubectl</span></span>

<span data-ttu-id="ebda8-112">En los tutoriales posteriores, Hola voto de Azure es de aplicación implementado clúster toohello, escalada, actualiza y Operations Management Suite es clúster de Kubernetes hello toomonitor configurado.</span><span class="sxs-lookup"><span data-stu-id="ebda8-112">In subsequent tutorials, hello Azure Vote application is deployed toohello cluster, scaled, updated, and Operations Management Suite is configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ebda8-113">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="ebda8-113">Before you begin</span></span>

<span data-ttu-id="ebda8-114">En los tutoriales anteriores, una imagen de contenedor se ha creado y cargado tooan instancia de registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebda8-114">In previous tutorials, a container image was created and uploaded tooan Azure Container Registry instance.</span></span> <span data-ttu-id="ebda8-115">Si aún no ha hecho estos pasos y desearía toofollow a lo largo, devolver demasiado[Tutorial 1: crear imágenes del contenedor](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="ebda8-115">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span>

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="ebda8-116">Creación de un clúster de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ebda8-116">Create Kubernetes cluster</span></span>

<span data-ttu-id="ebda8-117">Hola [tutorial anterior](./container-service-tutorial-kubernetes-prepare-acr.md), un grupo de recursos denominado *myResourceGroup* se creó.</span><span class="sxs-lookup"><span data-stu-id="ebda8-117">In hello [previous tutorial](./container-service-tutorial-kubernetes-prepare-acr.md), a resource group named *myResourceGroup* was created.</span></span> <span data-ttu-id="ebda8-118">Si todavía no lo ha hecho, cree ahora este grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ebda8-118">If you have not done so, create this resource group now.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="ebda8-119">Crear un clúster de Kubernetes en el servicio de contenedor de Azure con hello [az acs crear](/cli/azure/acs#create) comando.</span><span class="sxs-lookup"><span data-stu-id="ebda8-119">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="ebda8-120">Hello en el ejemplo siguiente se crea un clúster denominado *myK8sCluster* con un Linux maestro de nodo y tres nodos de agente de Linux.</span><span class="sxs-lookup"><span data-stu-id="ebda8-120">hello following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

<span data-ttu-id="ebda8-121">Después de varios minutos, comando hello completa y, en formato json de devuelve información acerca de la implementación de hello ACS.</span><span class="sxs-lookup"><span data-stu-id="ebda8-121">After several minutes, hello command completes, and returns json formatted information about hello ACS deployment.</span></span>

## <a name="install-hello-kubectl-cli"></a><span data-ttu-id="ebda8-122">Instalar hello kubectl CLI</span><span class="sxs-lookup"><span data-stu-id="ebda8-122">Install hello kubectl CLI</span></span>

<span data-ttu-id="ebda8-123">tooconnect toohello Kubernetes de clúster desde el equipo cliente, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), cliente de línea de comandos de Kubernetes Hola.</span><span class="sxs-lookup"><span data-stu-id="ebda8-123">tooconnect toohello Kubernetes cluster from your client computer, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="ebda8-124">Si usa Azure CloudShell, `kubectl` ya está instalado.</span><span class="sxs-lookup"><span data-stu-id="ebda8-124">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="ebda8-125">Si desea que tooinstall forma local, use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) comando.</span><span class="sxs-lookup"><span data-stu-id="ebda8-125">If you want tooinstall it locally, use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="ebda8-126">Si está ejecutando en Linux o Mac OS, debe toorun con sudo.</span><span class="sxs-lookup"><span data-stu-id="ebda8-126">If running in Linux or macOS, you may need toorun with sudo.</span></span> <span data-ttu-id="ebda8-127">En Windows, asegúrese de que el shell se ha ejecutado como administrador.</span><span class="sxs-lookup"><span data-stu-id="ebda8-127">On Windows, ensure your shell has been run as administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli 
```

<span data-ttu-id="ebda8-128">En Windows, es la instalación predeterminada de hello *c:\program files (x86)\kubectl.exe*.</span><span class="sxs-lookup"><span data-stu-id="ebda8-128">On Windows, hello default installation is *c:\program files (x86)\kubectl.exe*.</span></span> <span data-ttu-id="ebda8-129">Puede que tenga tooadd esta ruta de acceso de archivo toohello Windows.</span><span class="sxs-lookup"><span data-stu-id="ebda8-129">You may need tooadd this file toohello Windows path.</span></span> 

## <a name="connect-with-kubectl"></a><span data-ttu-id="ebda8-130">Conexión con kubectl</span><span class="sxs-lookup"><span data-stu-id="ebda8-130">Connect with kubectl</span></span>

<span data-ttu-id="ebda8-131">tooconfigure `kubectl` tooconnect tooyour Kubernetes clúster, ejecute hello [az kubernetes get-credenciales de acs](/cli/azure/acs/kubernetes#get-credentials) comando.</span><span class="sxs-lookup"><span data-stu-id="ebda8-131">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

<span data-ttu-id="ebda8-132">clúster de tooyour de conexión de hello tooverify, ejecute hello [kubectl obtener nodos](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.</span><span class="sxs-lookup"><span data-stu-id="ebda8-132">tooverify hello connection tooyour cluster, run hello [kubectl get nodes](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="ebda8-133">Salida:</span><span class="sxs-lookup"><span data-stu-id="ebda8-133">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

<span data-ttu-id="ebda8-134">Al finalizar el tutorial, tendrá un clúster de ACS de Kubernetes preparado para cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ebda8-134">At tutorial completion, you have an ACS Kubernetes cluster ready for workloads.</span></span> <span data-ttu-id="ebda8-135">En los tutoriales posteriores, una aplicación de contenedor múltiples es clúster toothis implementado, escalar horizontalmente, actualizar y supervisar.</span><span class="sxs-lookup"><span data-stu-id="ebda8-135">In subsequent tutorials, a multi-container application is deployed toothis cluster, scaled out, updated, and monitored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebda8-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ebda8-136">Next steps</span></span>

<span data-ttu-id="ebda8-137">En este tutorial, se implementó un clúster de Kubernetes de Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="ebda8-137">In this tutorial, an Azure Container Service Kubernetes cluster was deployed.</span></span> <span data-ttu-id="ebda8-138">se completaron Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="ebda8-138">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ebda8-139">Implementación de un clúster de ACS de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ebda8-139">Deployed a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="ebda8-140">Hola instalado Kubernetes CLI (kubectl)</span><span class="sxs-lookup"><span data-stu-id="ebda8-140">Installed hello Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="ebda8-141">Configuración de kubectl</span><span class="sxs-lookup"><span data-stu-id="ebda8-141">Configured kubectl</span></span>

<span data-ttu-id="ebda8-142">Avanzar toohello toolearn de tutorial siguiente sobre cómo ejecutar la aplicación en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="ebda8-142">Advance toohello next tutorial toolearn about running application on hello cluster.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ebda8-143">Implementación de una aplicación en Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ebda8-143">Deploy application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-deploy-application.md)
