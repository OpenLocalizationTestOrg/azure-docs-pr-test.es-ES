---
title: "aaaQuickstart - clúster Kubernetes de Azure para Linux | Documentos de Microsoft"
description: "Aprender rápidamente toocreate un clúster Kubernetes para contenedores de Linux en el servicio de contenedor de Azure con hello CLI de Azure."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 8b0d7a803148c1cbf329f4b76f2e99b4b7e14983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-linux-containers"></a><span data-ttu-id="9ecbe-103">Implementación de un clúster de Kubernetes para los contenedores de Linux</span><span class="sxs-lookup"><span data-stu-id="9ecbe-103">Deploy Kubernetes cluster for Linux containers</span></span>

<span data-ttu-id="9ecbe-104">En esta guía de inicio rápido, un clúster de Kubernetes se implementa mediante Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-104">In this quick start, a Kubernetes cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="9ecbe-105">Una aplicación de contenedor múltiples que consta de front-end web y una instancia de Redis es, a continuación, implementar y ejecutar en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="9ecbe-106">Una vez completado, la aplicación hello es accesible a través de internet de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-106">Once completed, hello application is accessible over hello internet.</span></span> 

<span data-ttu-id="9ecbe-107">aplicación de ejemplo de Hola usado en este documento está escrita en Python.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-107">hello example application used in this document is written in Python.</span></span> <span data-ttu-id="9ecbe-108">conceptos de Hola y pasos que se detallan a continuación pueden ser utilizado toodeploy cualquier contenedor de la imagen en un clúster de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-108">hello concepts and steps detailed here can be used toodeploy any container image into a Kubernetes cluster.</span></span> <span data-ttu-id="9ecbe-109">Hello código, Dockerfile y el proyecto de toothis relacionados de archivos de manifiesto de Kubernetes creada previamente están disponibles en [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span><span class="sxs-lookup"><span data-stu-id="9ecbe-109">hello code, Dockerfile, and pre-created Kubernetes manifest files related toothis project are available on [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span></span>

![Imagen de la exploración tooAzure voto](media/container-service-kubernetes-walkthrough/azure-vote.png)

<span data-ttu-id="9ecbe-111">Este inicio rápido asume un conocimiento básico de conceptos de Kubernetes, para obtener información detallada en Kubernetes vea hello [Kubernetes documentación]( https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="9ecbe-111">This quick start assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see hello [Kubernetes documentation]( https://kubernetes.io/docs/home/).</span></span>

<span data-ttu-id="9ecbe-112">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9ecbe-113">Si elige tooinstall y usar hello CLI localmente, este tutorial rápido requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-113">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9ecbe-114">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9ecbe-115">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9ecbe-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="9ecbe-116">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9ecbe-116">Create a resource group</span></span>

<span data-ttu-id="9ecbe-117">Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-117">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="9ecbe-118">Un grupo de recursos de Azure es un grupo lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-118">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="9ecbe-119">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *westeurope* ubicación.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-119">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="9ecbe-120">Salida:</span><span class="sxs-lookup"><span data-stu-id="9ecbe-120">Output:</span></span>

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westeurope",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="9ecbe-121">Creación de un clúster de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="9ecbe-121">Create Kubernetes cluster</span></span>

<span data-ttu-id="9ecbe-122">Crear un clúster de Kubernetes en el servicio de contenedor de Azure con hello [az acs crear](/cli/azure/acs#create) comando.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-122">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> <span data-ttu-id="9ecbe-123">Hello en el ejemplo siguiente se crea un clúster denominado *myK8sCluster* con un Linux maestro de nodo y tres nodos de agente de Linux.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-123">hello following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8sCluster --generate-ssh-keys 
```

<span data-ttu-id="9ecbe-124">Tras varios minutos, comando hello completa y devuelve información de formato json sobre clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-124">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span> 

## <a name="connect-toohello-cluster"></a><span data-ttu-id="9ecbe-125">Conectar el clúster toohello</span><span class="sxs-lookup"><span data-stu-id="9ecbe-125">Connect toohello cluster</span></span>

<span data-ttu-id="9ecbe-126">usar un clúster de Kubernetes toomanage [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), cliente de línea de comandos de Kubernetes Hola.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-126">toomanage a Kubernetes cluster, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="9ecbe-127">Si usa Azure CloudShell, kubectl ya está instalado.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-127">If you're using Azure CloudShell, kubectl is already installed.</span></span> <span data-ttu-id="9ecbe-128">Si desea que tooinstall localmente, puede usar hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) comando.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-128">If you want tooinstall it locally, you can use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="9ecbe-129">tooconfigure kubectl tooconnect tooyour Kubernetes clúster, ejecute hello [az kubernetes get-credenciales de acs](/cli/azure/acs/kubernetes#get-credentials) comando.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-129">tooconfigure kubectl tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="9ecbe-130">Este paso descarga las credenciales y configura hello Kubernetes CLI toouse ellos.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-130">This step downloads credentials and configures hello Kubernetes CLI toouse them.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="9ecbe-131">clúster de tooyour conexión tooverify hello, use hello [kubectl obtener](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando tooreturn una lista de nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-131">tooverify hello connection tooyour cluster, use hello [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command tooreturn a list of hello cluster nodes.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="9ecbe-132">Salida:</span><span class="sxs-lookup"><span data-stu-id="9ecbe-132">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-14ad53a1-0    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-1    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-2    Ready                      10m       v1.6.6
k8s-master-14ad53a1-0   Ready,SchedulingDisabled   10m       v1.6.6
```

## <a name="run-hello-application"></a><span data-ttu-id="9ecbe-133">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="9ecbe-133">Run hello application</span></span>

<span data-ttu-id="9ecbe-134">Un archivo de manifiesto de Kubernetes define un estado deseado para el clúster de hello, incluidos lo que deben estar en ejecución imágenes del contenedor.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-134">A Kubernetes manifest file defines a desired state for hello cluster, including what container images should be running.</span></span> <span data-ttu-id="9ecbe-135">En este ejemplo, un manifiesto es toocreate usado todos los objetos necesarios toorun Hola aplicación voto de Azure.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-135">For this example, a manifest is used toocreate all objects needed toorun hello Azure Vote application.</span></span> 

<span data-ttu-id="9ecbe-136">Cree un archivo denominado `azure-vote.yml` y copie en él Hola siguientes YAML.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-136">Create a file named `azure-vote.yml` and copy into it hello following YAML.</span></span> <span data-ttu-id="9ecbe-137">Si está trabajando en Azure Cloud Shell, este archivo se puede crear mediante vi o Nano, como si trabajara en un sistema físico o virtual.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-137">If you are working in Azure Cloud Shell, this file can be created using vi or Nano as if working on a virtual or physical system.</span></span>

```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-back
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-back
    spec:
      containers:
      - name: azure-vote-back
        image: redis
        ports:
        - containerPort: 6379
          name: redis
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-back
spec:
  ports:
  - port: 6379
  selector:
    app: azure-vote-back
---
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-front
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-front
    spec:
      containers:
      - name: azure-vote-front
        image: microsoft/azure-vote-front:redis-v1
        ports:
        - containerPort: 80
        env:
        - name: REDIS
          value: "azure-vote-back"
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
```

<span data-ttu-id="9ecbe-138">Hola de uso [kubectl crear](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) aplicación hello de toorun de comandos.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-138">Use hello [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command toorun hello application.</span></span>

```azurecli-interactive
kubectl create -f azure-vote.yml
```

<span data-ttu-id="9ecbe-139">Salida:</span><span class="sxs-lookup"><span data-stu-id="9ecbe-139">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-hello-application"></a><span data-ttu-id="9ecbe-140">Probar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="9ecbe-140">Test hello application</span></span>

<span data-ttu-id="9ecbe-141">Cuando se ejecuta la aplicación hello, un [Kubernetes servicio](https://kubernetes.io/docs/concepts/services-networking/service/) se crea que expone Hola aplicación front-end toohello internet.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-141">As hello application is run, a [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created that exposes hello application front end toohello internet.</span></span> <span data-ttu-id="9ecbe-142">Este proceso puede tardar unos toocomplete minutos.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-142">This process can take a few minutes toocomplete.</span></span> 

<span data-ttu-id="9ecbe-143">curso toomonitor, use hello [kubectl obtener servicio](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando con hello `--watch` argumento.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-143">toomonitor progress, use hello [kubectl get service](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command with hello `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="9ecbe-144">Hola inicialmente **IP externas** para hello *azure front-voto* servicio aparece como *pendiente*.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-144">Initially hello **EXTERNAL-IP** for hello *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="9ecbe-145">Una vez que la dirección de hello externo IP ha cambiado desde *pendiente* tooan *dirección IP*, use `CTRL-C` proceso de inspección de toostop hello kubectl.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-145">Once hello EXTERNAL-IP address has changed from *pending* tooan *IP address*, use `CTRL-C` toostop hello kubectl watch process.</span></span> 
  
```bash
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

<span data-ttu-id="9ecbe-146">Ahora puede examinar Hola de toohello externo IP dirección toosee voto de aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-146">You can now browse toohello external IP address toosee hello Azure Vote App.</span></span>

![Imagen de la exploración tooAzure voto](media/container-service-kubernetes-walkthrough/azure-vote.png)  

## <a name="delete-cluster"></a><span data-ttu-id="9ecbe-148">Eliminación de clúster</span><span class="sxs-lookup"><span data-stu-id="9ecbe-148">Delete cluster</span></span>
<span data-ttu-id="9ecbe-149">Cuando ya no se necesita el clúster hello, puede usar hello [eliminación del grupo az](/cli/azure/group#delete) comandos tooremove grupo de recursos de hello, servicio de contenedor y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-149">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="9ecbe-150">Obtener el código de hello</span><span class="sxs-lookup"><span data-stu-id="9ecbe-150">Get hello code</span></span>

<span data-ttu-id="9ecbe-151">En esta guía de inicio rápido, imágenes del contenedor creada previamente han sido toocreate usa una implementación de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-151">In this quick start, pre-created container images have been used toocreate a Kubernetes deployment.</span></span> <span data-ttu-id="9ecbe-152">Hola relacionadas con código de aplicación, Dockerfile, y archivo de manifiesto de Kubernetes están disponibles en GitHub.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-152">hello related application code, Dockerfile, and Kubernetes manifest file are available on GitHub.</span></span>

[<span data-ttu-id="9ecbe-153">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="9ecbe-153">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="9ecbe-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9ecbe-154">Next steps</span></span>

<span data-ttu-id="9ecbe-155">En esta guía de inicio rápido, implementar un clúster de Kubernetes e implementa una aplicación de contenedor de varios tooit.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-155">In this quick start, you deployed a Kubernetes cluster and deployed a multi-container application tooit.</span></span> 

<span data-ttu-id="9ecbe-156">toolearn más información sobre el servicio de contenedor de Azure y recorrido a través de un ejemplo de código completo toodeployment, continuar con tutorial de clúster de toohello Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="9ecbe-156">toolearn more about Azure Container Service, and walk through a complete code toodeployment example, continue toohello Kubernetes cluster tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9ecbe-157">Administración de un clúster de ACS Kubernetes</span><span class="sxs-lookup"><span data-stu-id="9ecbe-157">Manage an ACS Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-prepare-app.md)
