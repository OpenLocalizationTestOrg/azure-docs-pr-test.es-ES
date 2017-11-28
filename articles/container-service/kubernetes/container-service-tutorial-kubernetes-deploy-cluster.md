---
title: "Tutorial de Azure Container Service: Implementación de clúster | Microsoft Docs"
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
ms.openlocfilehash: 472697c1f0c18859087d7b448e1786d85c27aca0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="2cdb1-104">Implementación de un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="2cdb1-104">Deploy a Kubernetes cluster in Azure Container Service</span></span>

<span data-ttu-id="2cdb1-105">Kubernetes proporciona una plataforma distribuida para aplicaciones en contenedores.</span><span class="sxs-lookup"><span data-stu-id="2cdb1-105">Kubernetes provides a distributed platform for containerized applications.</span></span> <span data-ttu-id="2cdb1-106">Con Azure Container Service, el aprovisionamiento de un clúster de Kubernetes listo para producción se realiza de forma rápida y sencilla.</span><span class="sxs-lookup"><span data-stu-id="2cdb1-106">With Azure Container Service, provisioning of a production ready Kubernetes cluster is simple and quick.</span></span> <span data-ttu-id="2cdb1-107">En este tutorial, la tercera parte de siete, se implementa un clúster de Kubernetes de Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="2cdb1-107">In this tutorial, part 3 of 7, an Azure Container Service Kubernetes cluster is deployed.</span></span> <span data-ttu-id="2cdb1-108">Los pasos completados incluyen:</span><span class="sxs-lookup"><span data-stu-id="2cdb1-108">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2cdb1-109">Implementación de un clúster de ACS de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="2cdb1-109">Deploying a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="2cdb1-110">Instalación de la CLI de Kubernetes (kubectl)</span><span class="sxs-lookup"><span data-stu-id="2cdb1-110">Installation of the Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="2cdb1-111">Configuración de kubectl</span><span class="sxs-lookup"><span data-stu-id="2cdb1-111">Configuration of kubectl</span></span>

<span data-ttu-id="2cdb1-112">En tutoriales posteriores, la aplicación Azure Vote se implementa en el clúster, se escala y se actualiza, y Operations Management Suite se configura para supervisar el clúster de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="2cdb1-112">In subsequent tutorials, the Azure Vote application is deployed to the cluster, scaled, updated, and Operations Management Suite is configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2cdb1-113">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="2cdb1-113">Before you begin</span></span>

<span data-ttu-id="2cdb1-114">En los tutoriales anteriores, se creó una imagen de contenedor y se actualizó en una instancia de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="2cdb1-114">In previous tutorials, a container image was created and uploaded to an Azure Container Registry instance.</span></span> <span data-ttu-id="2cdb1-115">Si no ha realizado estos pasos, pero desea continuar, vuelva al tutorial [Create container images to be used with Azure Container Service](./container-service-tutorial-kubernetes-prepare-app.md) (Creación de las imágenes de contenedor que se usan con Azure Container Service).</span><span class="sxs-lookup"><span data-stu-id="2cdb1-115">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span>

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="2cdb1-116">Creación de un clúster de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="2cdb1-116">Create Kubernetes cluster</span></span>

<span data-ttu-id="2cdb1-117">En el [tutorial anterior](./container-service-tutorial-kubernetes-prepare-acr.md), se creó un grupo de recursos denominado *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="2cdb1-117">In the [previous tutorial](./container-service-tutorial-kubernetes-prepare-acr.md), a resource group named *myResourceGroup* was created.</span></span> <span data-ttu-id="2cdb1-118">Si todavía no lo ha hecho, cree ahora este grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2cdb1-118">If you have not done so, create this resource group now.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="2cdb1-119">Cree un clúster de Kubernetes en Azure Container Service con el comando [az acs create](/cli/azure/acs#create).</span><span class="sxs-lookup"><span data-stu-id="2cdb1-119">Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="2cdb1-120">En el ejemplo siguiente, se crea un clúster denominado *myK8sCluster* con un nodo maestro de Linux y tres nodos de agente de Linux.</span><span class="sxs-lookup"><span data-stu-id="2cdb1-120">The following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

<span data-ttu-id="2cdb1-121">Después de varios minutos, el comando se completa y devuelve información en formato json sobre la implementación de ACS.</span><span class="sxs-lookup"><span data-stu-id="2cdb1-121">After several minutes, the command completes, and returns json formatted information about the ACS deployment.</span></span>

## <a name="install-the-kubectl-cli"></a><span data-ttu-id="2cdb1-122">Instalación de la CLI de kubectl</span><span class="sxs-lookup"><span data-stu-id="2cdb1-122">Install the kubectl CLI</span></span>

<span data-ttu-id="2cdb1-123">Para conectarse al clúster de Kubernetes desde el equipo cliente, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), el cliente de la línea de comandos de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="2cdb1-123">To connect to the Kubernetes cluster from your client computer, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span></span> 

<span data-ttu-id="2cdb1-124">Si usa Azure CloudShell, `kubectl` ya está instalado.</span><span class="sxs-lookup"><span data-stu-id="2cdb1-124">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="2cdb1-125">Si desea instalarlo de forma local, use el comando [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli).</span><span class="sxs-lookup"><span data-stu-id="2cdb1-125">If you want to install it locally, use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="2cdb1-126">Si está ejecutando en Linux o macOS, debe ejecutar con sudo.</span><span class="sxs-lookup"><span data-stu-id="2cdb1-126">If running in Linux or macOS, you may need to run with sudo.</span></span> <span data-ttu-id="2cdb1-127">En Windows, asegúrese de que el shell se ha ejecutado como administrador.</span><span class="sxs-lookup"><span data-stu-id="2cdb1-127">On Windows, ensure your shell has been run as administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli 
```

<span data-ttu-id="2cdb1-128">En Windows, la instalación predeterminada es *c:\program files (x86)\kubectl.exe*.</span><span class="sxs-lookup"><span data-stu-id="2cdb1-128">On Windows, the default installation is *c:\program files (x86)\kubectl.exe*.</span></span> <span data-ttu-id="2cdb1-129">Puede que deba agregar este archivo a la ruta de acceso de Windows.</span><span class="sxs-lookup"><span data-stu-id="2cdb1-129">You may need to add this file to the Windows path.</span></span> 

## <a name="connect-with-kubectl"></a><span data-ttu-id="2cdb1-130">Conexión con kubectl</span><span class="sxs-lookup"><span data-stu-id="2cdb1-130">Connect with kubectl</span></span>

<span data-ttu-id="2cdb1-131">Para configurar `kubectl` para conectarse al clúster de Kubernetes, ejecute el comando [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials).</span><span class="sxs-lookup"><span data-stu-id="2cdb1-131">To configure `kubectl` to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

<span data-ttu-id="2cdb1-132">Para comprobar la conexión al clúster, ejecute el comando [kubectl get nodes](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get).</span><span class="sxs-lookup"><span data-stu-id="2cdb1-132">To verify the connection to your cluster, run the [kubectl get nodes](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="2cdb1-133">Salida:</span><span class="sxs-lookup"><span data-stu-id="2cdb1-133">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

<span data-ttu-id="2cdb1-134">Al finalizar el tutorial, tendrá un clúster de ACS de Kubernetes preparado para cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2cdb1-134">At tutorial completion, you have an ACS Kubernetes cluster ready for workloads.</span></span> <span data-ttu-id="2cdb1-135">En los tutoriales posteriores, una aplicación de contenedores múltiples está implementada en este clúster, escalada horizontalmente, actualizada y supervisada.</span><span class="sxs-lookup"><span data-stu-id="2cdb1-135">In subsequent tutorials, a multi-container application is deployed to this cluster, scaled out, updated, and monitored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2cdb1-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2cdb1-136">Next steps</span></span>

<span data-ttu-id="2cdb1-137">En este tutorial, se implementó un clúster de Kubernetes de Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="2cdb1-137">In this tutorial, an Azure Container Service Kubernetes cluster was deployed.</span></span> <span data-ttu-id="2cdb1-138">Se han completado los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="2cdb1-138">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2cdb1-139">Implementación de un clúster de ACS de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="2cdb1-139">Deployed a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="2cdb1-140">Instalación de la CLI de Kubernetes (kubectl)</span><span class="sxs-lookup"><span data-stu-id="2cdb1-140">Installed the Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="2cdb1-141">Configuración de kubectl</span><span class="sxs-lookup"><span data-stu-id="2cdb1-141">Configured kubectl</span></span>

<span data-ttu-id="2cdb1-142">Avance al siguiente tutorial para aprender a ejecutar la aplicación en el clúster.</span><span class="sxs-lookup"><span data-stu-id="2cdb1-142">Advance to the next tutorial to learn about running application on the cluster.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2cdb1-143">Implementación de una aplicación en Kubernetes</span><span class="sxs-lookup"><span data-stu-id="2cdb1-143">Deploy application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-deploy-application.md)
