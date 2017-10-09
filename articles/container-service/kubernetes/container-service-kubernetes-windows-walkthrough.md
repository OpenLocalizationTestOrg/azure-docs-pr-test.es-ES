---
title: "aaaQuickstart - clúster Kubernetes de Azure para Windows | Documentos de Microsoft"
description: "Aprender rápidamente toocreate un clúster Kubernetes para contenedores de Windows en el servicio de contenedor de Azure con hello CLI de Azure."
documentationcenter: 
author: dlepow
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
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a><span data-ttu-id="8f903-103">Implementación de un clúster de Kubernetes para los contenedores de Windows</span><span class="sxs-lookup"><span data-stu-id="8f903-103">Deploy Kubernetes cluster for Windows containers</span></span>

<span data-ttu-id="8f903-104">Hola CLI de Azure es toocreate usado y administrar recursos de Azure desde la línea de comandos de Hola o en scripts.</span><span class="sxs-lookup"><span data-stu-id="8f903-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="8f903-105">Esta guía se detalla con hello Azure CLI toodeploy una [Kubernetes](https://kubernetes.io/docs/home/) de clúster en [servicio de contenedor de Azure](../container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="8f903-105">This guide details using hello Azure CLI toodeploy a [Kubernetes](https://kubernetes.io/docs/home/) cluster in [Azure Container Service](../container-service-intro.md).</span></span> <span data-ttu-id="8f903-106">Una vez que se implementa el clúster de hello, conectar tooit con hello Kubernetes `kubectl` herramienta de línea de comandos y, implementar el primer contenedor de Windows.</span><span class="sxs-lookup"><span data-stu-id="8f903-106">Once hello cluster is deployed, you connect tooit with hello Kubernetes `kubectl` command-line tool, and you deploy your first Windows container.</span></span>

<span data-ttu-id="8f903-107">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="8f903-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8f903-108">Si elige tooinstall y usar hello CLI localmente, este tutorial rápido requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="8f903-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="8f903-109">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f903-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8f903-110">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8f903-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

> [!NOTE]
> <span data-ttu-id="8f903-111">La compatibilidad para contenedores de Windows en Kubernetes en Azure Container Service está en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="8f903-111">Support for Windows containers on Kubernetes in Azure Container Service is in preview.</span></span> 
>

## <a name="create-a-resource-group"></a><span data-ttu-id="8f903-112">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8f903-112">Create a resource group</span></span>

<span data-ttu-id="8f903-113">Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="8f903-113">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="8f903-114">Un grupo de recursos de Azure es un grupo lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f903-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="8f903-115">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación.</span><span class="sxs-lookup"><span data-stu-id="8f903-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="8f903-116">Creación de un clúster de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8f903-116">Create Kubernetes cluster</span></span>
<span data-ttu-id="8f903-117">Crear un clúster de Kubernetes en el servicio de contenedor de Azure con hello [az acs crear](/cli/azure/acs#create) comando.</span><span class="sxs-lookup"><span data-stu-id="8f903-117">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="8f903-118">Hello en el ejemplo siguiente se crea un clúster denominado *myK8sCluster* con un Linux maestro de nodo y dos nodos de agente de Windows.</span><span class="sxs-lookup"><span data-stu-id="8f903-118">hello following example creates a cluster named *myK8sCluster* with one Linux master node and two Windows agent nodes.</span></span> <span data-ttu-id="8f903-119">Este ejemplo crea SSH maestros de claves necesario tooconnect toohello Linux.</span><span class="sxs-lookup"><span data-stu-id="8f903-119">This example creates SSH keys needed tooconnect toohello Linux master.</span></span> <span data-ttu-id="8f903-120">Este ejemplo se utiliza *azureuser* para un nombre de usuario administrativo y *myPassword12* como contraseña de hello en nodos de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="8f903-120">This example uses *azureuser* for an administrative user name and *myPassword12* as hello password on hello Windows nodes.</span></span> <span data-ttu-id="8f903-121">Actualice estos entorno de valores toosomething tooyour adecuado.</span><span class="sxs-lookup"><span data-stu-id="8f903-121">Update these values toosomething appropriate tooyour environment.</span></span> 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

<span data-ttu-id="8f903-122">Después de varios minutos, comando hello completa y muestra información acerca de la implementación.</span><span class="sxs-lookup"><span data-stu-id="8f903-122">After several minutes, hello command completes, and shows you information about your deployment.</span></span>

## <a name="install-kubectl"></a><span data-ttu-id="8f903-123">Instalación de kubectl</span><span class="sxs-lookup"><span data-stu-id="8f903-123">Install kubectl</span></span>

<span data-ttu-id="8f903-124">tooconnect toohello Kubernetes de clúster desde el equipo cliente, use [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/), cliente de línea de comandos de Kubernetes Hola.</span><span class="sxs-lookup"><span data-stu-id="8f903-124">tooconnect toohello Kubernetes cluster from your client computer, use [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="8f903-125">Si usa Azure CloudShell, `kubectl` ya está instalado.</span><span class="sxs-lookup"><span data-stu-id="8f903-125">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="8f903-126">Si desea que tooinstall localmente, puede usar hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) comando.</span><span class="sxs-lookup"><span data-stu-id="8f903-126">If you want tooinstall it locally, you can use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="8f903-127">Hola después de la instalación de CLI de Azure en el ejemplo se `kubectl` tooyour sistema.</span><span class="sxs-lookup"><span data-stu-id="8f903-127">hello following Azure CLI example installs `kubectl` tooyour system.</span></span> <span data-ttu-id="8f903-128">En Windows, ejecute este comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="8f903-128">On Windows, run this command as an administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a><span data-ttu-id="8f903-129">Conexión con kubectl</span><span class="sxs-lookup"><span data-stu-id="8f903-129">Connect with kubectl</span></span>

<span data-ttu-id="8f903-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes clúster, ejecute hello [az kubernetes get-credenciales de acs](/cli/azure/acs/kubernetes#get-credentials) comando.</span><span class="sxs-lookup"><span data-stu-id="8f903-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="8f903-131">Hello en el ejemplo siguiente se descarga configuración de clúster de hello para el clúster de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="8f903-131">hello following example downloads hello cluster configuration for your Kubernetes cluster.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="8f903-132">clúster de tooyour de tooverify Hola conexión desde el equipo, ejecute:</span><span class="sxs-lookup"><span data-stu-id="8f903-132">tooverify hello connection tooyour cluster from your machine, try running:</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="8f903-133">`kubectl`Enumera los nodos de patrón y el agente de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f903-133">`kubectl` lists hello master and agent nodes.</span></span>

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a><span data-ttu-id="8f903-134">Implementación de un contenedor de Windows IIS</span><span class="sxs-lookup"><span data-stu-id="8f903-134">Deploy a Windows IIS container</span></span>

<span data-ttu-id="8f903-135">Puede ejecutar un contenedor de Docker dentro de un *pod* de Kubernetes que contiene uno o varios contenedores.</span><span class="sxs-lookup"><span data-stu-id="8f903-135">You can run a Docker container inside a Kubernetes *pod*, which contains one or more containers.</span></span> 

<span data-ttu-id="8f903-136">Este ejemplo básico se usa un toospecify de archivo JSON un contenedor de servicios de Microsoft Internet Information Server (IIS) y, a continuación, crea pod hello mediante hello `kubctl apply` comando.</span><span class="sxs-lookup"><span data-stu-id="8f903-136">This basic example uses a JSON file toospecify a Microsoft Internet Information Server (IIS) container, and then creates hello pod using hello `kubctl apply` command.</span></span> 

<span data-ttu-id="8f903-137">Cree un archivo local denominado `iis.json` y Hola copia siguiendo el texto.</span><span class="sxs-lookup"><span data-stu-id="8f903-137">Create a local file named `iis.json` and copy hello following text.</span></span> <span data-ttu-id="8f903-138">Este archivo indica Kubernetes toorun IIS en Windows Server 2016 Nano Server, con una imagen de contenedor público de [Docker Hub](https://hub.docker.com/r/nanoserver/iis/).</span><span class="sxs-lookup"><span data-stu-id="8f903-138">This file tells Kubernetes toorun IIS on Windows Server 2016 Nano Server, using a public container image from [Docker Hub](https://hub.docker.com/r/nanoserver/iis/).</span></span> <span data-ttu-id="8f903-139">contenedor de Hello usa el puerto 80, pero inicialmente solo es accesible dentro de la red de clústeres de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f903-139">hello container uses port 80, but initially is only accessible within hello cluster network.</span></span>

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

<span data-ttu-id="8f903-140">pod de hello toostart, tipo:</span><span class="sxs-lookup"><span data-stu-id="8f903-140">toostart hello pod, type:</span></span>
  
```azurecli-interactive
kubectl apply -f iis.json
```  

<span data-ttu-id="8f903-141">implementación de hello tootrack, tipo:</span><span class="sxs-lookup"><span data-stu-id="8f903-141">tootrack hello deployment, type:</span></span>
  
```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="8f903-142">Mientras se está implementando pod hello, estado de hello es `ContainerCreating`.</span><span class="sxs-lookup"><span data-stu-id="8f903-142">While hello pod is deploying, hello status is `ContainerCreating`.</span></span> <span data-ttu-id="8f903-143">Puede tardar unos minutos para hello de hello contenedor tooenter `Running` estado.</span><span class="sxs-lookup"><span data-stu-id="8f903-143">It can take a few minutes for hello container tooenter hello `Running` state.</span></span>

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="8f903-144">Hola de vista Página de bienvenida de IIS</span><span class="sxs-lookup"><span data-stu-id="8f903-144">View hello IIS welcome page</span></span>

<span data-ttu-id="8f903-145">tooexpose hello world de toohello de pod con una dirección IP pública, Hola de tipo siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8f903-145">tooexpose hello pod toohello world with a public IP address, type hello following command:</span></span>

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

<span data-ttu-id="8f903-146">Con este comando, Kubernetes crea un servicio y un [regla del equilibrador de carga de Azure](container-service-kubernetes-load-balancing.md) con una dirección IP pública para el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f903-146">With this command, Kubernetes creates a service and an [Azure load balancer rule](container-service-kubernetes-load-balancing.md) with a public IP address for hello service.</span></span> 

<span data-ttu-id="8f903-147">Ejecute hello siguiendo el estado del comando toosee Hola del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f903-147">Run hello following command toosee hello status of hello service.</span></span>

```azurecli-interactive
kubectl get svc
```

<span data-ttu-id="8f903-148">Dirección IP de hello aparece inicialmente como `pending`.</span><span class="sxs-lookup"><span data-stu-id="8f903-148">Initially hello IP address appears as `pending`.</span></span> <span data-ttu-id="8f903-149">Después de unos minutos, Hola dirección IP externa de hello `iis` pod está establecido:</span><span class="sxs-lookup"><span data-stu-id="8f903-149">After a few minutes, hello external IP address of hello `iis` pod is set:</span></span>
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

<span data-ttu-id="8f903-150">Puede usar un explorador web de la página de bienvenida de IIS de elección toosee Hola predeterminado en la dirección IP externa de hello:</span><span class="sxs-lookup"><span data-stu-id="8f903-150">You can use a web browser of your choice toosee hello default IIS welcome page at hello external IP address:</span></span>

![Imagen de la exploración tooIIS](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a><span data-ttu-id="8f903-152">Eliminación de clúster</span><span class="sxs-lookup"><span data-stu-id="8f903-152">Delete cluster</span></span>
<span data-ttu-id="8f903-153">Cuando ya no se necesita el clúster hello, puede usar hello [eliminación del grupo az](/cli/azure/group#delete) comandos tooremove grupo de recursos de hello, servicio de contenedor y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="8f903-153">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a><span data-ttu-id="8f903-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8f903-154">Next steps</span></span>

<span data-ttu-id="8f903-155">En esta guía de inicio rápido, ha implementado un clúster de Kubernetes, conectado con `kubectl` y un pod con un contenedor IIS.</span><span class="sxs-lookup"><span data-stu-id="8f903-155">In this quick start, you deployed a Kubernetes cluster, connected with `kubectl`, and deployed a pod with an IIS container.</span></span> <span data-ttu-id="8f903-156">toolearn más información sobre el servicio de contenedor de Azure, continuar toohello Kubernetes tutorial.</span><span class="sxs-lookup"><span data-stu-id="8f903-156">toolearn more about Azure Container Service, continue toohello Kubernetes tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8f903-157">Administración de un clúster de ACS Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8f903-157">Manage an ACS Kubernetes cluster</span></span>](container-service-tutorial-kubernetes-prepare-app.md)
