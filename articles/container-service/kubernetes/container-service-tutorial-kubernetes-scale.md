---
title: "tutorial de servicio de contenedor de aaaAzure - aplicación de escala | Documentos de Microsoft"
description: "Tutorial de Azure Container Service: escalado de una aplicación"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Kubernetes, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 29571eef0fd91bd6b40f00d8c018539f320179bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a><span data-ttu-id="8f6bf-104">Escalado de pods de Kubernetes e infraestructura de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8f6bf-104">Scale Kubernetes pods and Kubernetes infrastructure</span></span>

<span data-ttu-id="8f6bf-105">Si ha seguido los tutoriales de hello, tienes un clúster de Kubernetes en funcionamiento en el servicio de contenedor de Azure y ha implementado la aplicación de Azure votos hello.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-105">If you've been following hello tutorials, you have a working Kubernetes cluster in Azure Container Service and you deployed hello Azure Voting app.</span></span> 

<span data-ttu-id="8f6bf-106">En este tutorial, parte cinco de siete, escalar horizontalmente pod hello en la aplicación hello y pruebe pod Autoescala.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-106">In this tutorial, part five of seven, you scale out hello pods in hello app and try pod autoscaling.</span></span> <span data-ttu-id="8f6bf-107">También aprenderá cómo número de hello tooscale de toochange de nodos de agente de máquina virtual de Azure Hola capacidad del clúster para hospedar las cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-107">You also learn how tooscale hello number of Azure VM agent nodes toochange hello cluster's capacity for hosting workloads.</span></span> <span data-ttu-id="8f6bf-108">Las tareas completadas incluyen:</span><span class="sxs-lookup"><span data-stu-id="8f6bf-108">Tasks completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8f6bf-109">Escalado manual de pods de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8f6bf-109">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="8f6bf-110">Configurar pod de escalado automático que se ejecuta el front-end de la aplicación de Hola</span><span class="sxs-lookup"><span data-stu-id="8f6bf-110">Configuring Autoscale pods running hello app front end</span></span>
> * <span data-ttu-id="8f6bf-111">Escalar los nodos de agente de Azure de hello Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8f6bf-111">Scale hello Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="8f6bf-112">En los tutoriales posteriores, se actualiza Hola aplicación voto de Azure y Operations Management Suite configurado el clúster de toomonitor hello Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-112">In subsequent tutorials, hello Azure Vote application is updated, and Operations Management Suite configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8f6bf-113">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="8f6bf-113">Before you begin</span></span>

<span data-ttu-id="8f6bf-114">En los tutoriales anteriores, una aplicación se empaqueta en una imagen de contenedor, esta imagen cargó tooAzure del registro de contenedor y un clúster de Kubernetes creado.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-114">In previous tutorials, an application was packaged into a container image, this image uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="8f6bf-115">a continuación, se ejecutó la aplicación de Hello en clúster de Kubernetes Hola.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-115">hello application was then run on hello Kubernetes cluster.</span></span> <span data-ttu-id="8f6bf-116">Si aún no ha hecho estos pasos y desearía toofollow a lo largo, devolver toohello [Tutorial 1: crear imágenes del contenedor](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="8f6bf-116">If you have not done these steps, and would like toofollow along, return toohello [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="8f6bf-117">Como mínimo, este tutorial requiere un clúster de Kubernetes con una aplicación en ejecución.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-117">At minimum, this tutorial requires a Kubernetes cluster with a running application.</span></span>

## <a name="manually-scale-pods"></a><span data-ttu-id="8f6bf-118">Escalado manual de pods</span><span class="sxs-lookup"><span data-stu-id="8f6bf-118">Manually scale pods</span></span>

<span data-ttu-id="8f6bf-119">Hasta ahora, hello Azure voto front-end y la instancia de Redis se han implementado, cada uno con una única réplica.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-119">Thus far, hello Azure Vote front-end and Redis instance have been deployed, each with a single replica.</span></span> <span data-ttu-id="8f6bf-120">tooverify, ejecute hello [kubectl obtener](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-120">tooverify, run hello [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="8f6bf-121">Salida:</span><span class="sxs-lookup"><span data-stu-id="8f6bf-121">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

<span data-ttu-id="8f6bf-122">Cambiar manualmente el número de Hola de pod Hola `azure-vote-front` implementación mediante hello [kubectl escala](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) comando.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-122">Manually change hello number of pods in hello `azure-vote-front` deployment using hello [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) command.</span></span> <span data-ttu-id="8f6bf-123">Este ejemplo aumenta Hola número too5.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-123">This example increases hello number too5.</span></span>

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

<span data-ttu-id="8f6bf-124">Ejecutar [kubectl obtener pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify que Kubernetes crea pod Hola.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-124">Run [kubectl get pods](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify that Kubernetes is creating hello pods.</span></span> <span data-ttu-id="8f6bf-125">Tras un minuto aproximadamente, ejecutan pod de hello adicionales:</span><span class="sxs-lookup"><span data-stu-id="8f6bf-125">After a minute or so, hello additional pods are running:</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="8f6bf-126">Salida:</span><span class="sxs-lookup"><span data-stu-id="8f6bf-126">Output:</span></span>

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a><span data-ttu-id="8f6bf-127">Escalado automático de pods</span><span class="sxs-lookup"><span data-stu-id="8f6bf-127">Autoscale pods</span></span>

<span data-ttu-id="8f6bf-128">Admite Kubernetes [pod horizontal Autoescala](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) número de hello tooadjust de pod en una implementación de la función de uso de CPU u otros selecciona métricas.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-128">Kubernetes supports [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust hello number of pods in a deployment depending on CPU utilization or other select metrics.</span></span> 

<span data-ttu-id="8f6bf-129">toouse hello autoscaler, debe tener su pod solicitudes de CPU y los límites definidos.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-129">toouse hello autoscaler, your pods must have CPU requests and limits defined.</span></span> <span data-ttu-id="8f6bf-130">Hola `azure-vote-front` implementación, Hola CPU de las solicitudes 0,25 contenedor front-end, con un límite de 0,5 CPU.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-130">In hello `azure-vote-front` deployment, hello front-end container requests 0.25 CPU, with a limit of 0.5 CPU.</span></span> <span data-ttu-id="8f6bf-131">configuración de Hello tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="8f6bf-131">hello settings look like:</span></span>

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

<span data-ttu-id="8f6bf-132">Hello en el ejemplo siguiente se usa hello [escalado automático de kubectl](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) comando tooautoscale número de Hola de pod Hola `azure-vote-front` implementación.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-132">hello following example uses hello [kubectl autoscale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) command tooautoscale hello number of pods in hello `azure-vote-front` deployment.</span></span> <span data-ttu-id="8f6bf-133">En este caso, si el uso de CPU supera el 50%, hello autoscaler aumenta Hola pod tooa como máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-133">Here, if CPU utilization exceeds 50%, hello autoscaler increases hello pods tooa maximum of 10.</span></span>


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

<span data-ttu-id="8f6bf-134">estado de hello toosee de hello autoscaler, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="8f6bf-134">toosee hello status of hello autoscaler, run hello following command:</span></span>

```azurecli-interactive
kubectl get hpa
```

<span data-ttu-id="8f6bf-135">Salida:</span><span class="sxs-lookup"><span data-stu-id="8f6bf-135">Output:</span></span>

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

<span data-ttu-id="8f6bf-136">Después de unos minutos, con una carga mínima en la aplicación de Azure voto hello, número de Hola de réplicas de pod disminuye automáticamente too3.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-136">After a few minutes, with minimal load on hello Azure Vote app, hello number of pod replicas decreases automatically too3.</span></span>

## <a name="scale-hello-agents"></a><span data-ttu-id="8f6bf-137">Agentes de Hola de escala</span><span class="sxs-lookup"><span data-stu-id="8f6bf-137">Scale hello agents</span></span>

<span data-ttu-id="8f6bf-138">Si ha creado su clúster de Kubernetes mediante comandos de manera predeterminada en el tutorial anterior hello, tiene tres nodos de agente.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-138">If you created your Kubernetes cluster using default commands in hello previous tutorial, it has three agent nodes.</span></span> <span data-ttu-id="8f6bf-139">Puede ajustar manualmente número Hola de agentes si tiene previsto más o menos cargas de trabajo de contenedor en el clúster.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-139">You can adjust hello number of agents manually if you plan more or fewer container workloads on your cluster.</span></span> <span data-ttu-id="8f6bf-140">Hola de uso [az acs escalar](/cli/azure/acs#scale) comando y especifique el número de Hola de agentes con hello `--new-agent-count` parámetro.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-140">Use hello [az acs scale](/cli/azure/acs#scale) command, and specify hello number of agents with hello `--new-agent-count` parameter.</span></span>

<span data-ttu-id="8f6bf-141">Hello en el ejemplo siguiente se aumenta número Hola de too4 de nodos de agente en clúster de hello Kubernetes denominado *myK8sCluster*.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-141">hello following example increases hello number of agent nodes too4 in hello Kubernetes cluster named *myK8sCluster*.</span></span> <span data-ttu-id="8f6bf-142">comando de Hello toma un par de minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-142">hello command takes a couple of minutes toocomplete.</span></span>

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

<span data-ttu-id="8f6bf-143">Hello salida del comando muestra hello número del agente de nodos de valor de Hola de `agentPoolProfiles:count`:</span><span class="sxs-lookup"><span data-stu-id="8f6bf-143">hello command output shows hello number of agent nodes in hello value of `agentPoolProfiles:count`:</span></span>

```azurecli
{
  "agentPoolProfiles": [
    {
      "count": 4,
      "dnsPrefix": "myK8SCluster-myK8SCluster-e44f25-k8s-agents",
      "fqdn": "",
      "name": "agentpools",
      "vmSize": "Standard_D2_v2"
    }
  ],
...

```

## <a name="next-steps"></a><span data-ttu-id="8f6bf-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8f6bf-144">Next steps</span></span>

<span data-ttu-id="8f6bf-145">En este tutorial, se han usado distintas características de escalado en el clúster de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-145">In this tutorial, you used different scaling features in your Kubernetes cluster.</span></span> <span data-ttu-id="8f6bf-146">Las tareas tratadas incluyen:</span><span class="sxs-lookup"><span data-stu-id="8f6bf-146">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8f6bf-147">Escalado manual de pods de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8f6bf-147">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="8f6bf-148">Configurar pod de escalado automático que se ejecuta el front-end de la aplicación de Hola</span><span class="sxs-lookup"><span data-stu-id="8f6bf-148">Configuring Autoscale pods running hello app front end</span></span>
> * <span data-ttu-id="8f6bf-149">Escalar los nodos de agente de Azure de hello Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8f6bf-149">Scale hello Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="8f6bf-150">Avanzar toohello toolearn de tutorial siguiente acerca de cómo actualizar la aplicación en Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="8f6bf-150">Advance toohello next tutorial toolearn about updating application in Kubernetes.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8f6bf-151">Actualización de una aplicación en Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8f6bf-151">Update an application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-app-update.md)

