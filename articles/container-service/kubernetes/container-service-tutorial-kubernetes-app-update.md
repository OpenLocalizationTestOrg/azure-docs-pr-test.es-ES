---
title: "tutorial de servicio de contenedor de aaaAzure - la aplicación de actualización | Documentos de Microsoft"
description: "Tutorial de Azure Container Service: actualización de una aplicación"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenedores, microservicios, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c467498bab7952926a18e45ffbb21051a98739d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="update-an-application-in-kubernetes"></a><span data-ttu-id="9b6fe-104">Actualización de una aplicación en Kubernetes</span><span class="sxs-lookup"><span data-stu-id="9b6fe-104">Update an application in Kubernetes</span></span>

<span data-ttu-id="9b6fe-105">Después de implementar una aplicación en Kubernetes, se puede actualizar mediante la especificación de una nueva imagen de contenedor o la versión de la imagen.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-105">After you deploy an application in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="9b6fe-106">Cuando se actualiza una aplicación, la implementación de actualización de hello preconfigurada para que solo una parte de la implementación de Hola se actualicen al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-106">When you update an application, hello update rollout is staged so that only a portion of hello deployment is concurrently updated.</span></span> <span data-ttu-id="9b6fe-107">Esta actualización por fases permite tookeep de aplicación Hola ejecutando durante la actualización de Hola y proporciona un mecanismo de reversión si se produce un error de implementación.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-107">This staged update enables hello application tookeep running during hello update, and provides a rollback mechanism if a deployment failure occurs.</span></span> 

<span data-ttu-id="9b6fe-108">En este tutorial, se actualiza la parte seis de siete, aplicación de Azure voto de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-108">In this tutorial, part six of seven, hello sample Azure Vote app is updated.</span></span> <span data-ttu-id="9b6fe-109">Las tareas que debe completar incluyen las siguientes:</span><span class="sxs-lookup"><span data-stu-id="9b6fe-109">Tasks that you complete include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9b6fe-110">Actualizar el código de aplicación front-end de Hola</span><span class="sxs-lookup"><span data-stu-id="9b6fe-110">Updating hello front-end application code</span></span>
> * <span data-ttu-id="9b6fe-111">Creación de una imagen de contenedor actualizado</span><span class="sxs-lookup"><span data-stu-id="9b6fe-111">Creating an updated container image</span></span>
> * <span data-ttu-id="9b6fe-112">Insertar tooAzure de imagen de contenedor de hello del registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="9b6fe-112">Pushing hello container image tooAzure Container Registry</span></span>
> * <span data-ttu-id="9b6fe-113">Implementación de imagen de contenedor se actualizaron Hola</span><span class="sxs-lookup"><span data-stu-id="9b6fe-113">Deploying hello updated container image</span></span>

<span data-ttu-id="9b6fe-114">En los tutoriales posteriores, Operations Management Suite es clúster de Kubernetes hello toomonitor configurado.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-114">In subsequent tutorials, Operations Management Suite is configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9b6fe-115">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="9b6fe-115">Before you begin</span></span>

<span data-ttu-id="9b6fe-116">En los tutoriales anteriores, una aplicación se empaqueta en una imagen de contenedor, imagen Hola cargó tooAzure del registro de contenedor y un clúster de Kubernetes creado.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-116">In previous tutorials, an application was packaged into a container image, hello image uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="9b6fe-117">a continuación, se ejecutó la aplicación de Hello en clúster de Kubernetes Hola.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-117">hello application was then run on hello Kubernetes cluster.</span></span> 

<span data-ttu-id="9b6fe-118">Si no se han completado estos pasos y desea toofollow a lo largo, devolver demasiado[Tutorial 1: crear imágenes del contenedor](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="9b6fe-118">If you haven't completed these steps, and want toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-application"></a><span data-ttu-id="9b6fe-119">Actualización de una aplicación</span><span class="sxs-lookup"><span data-stu-id="9b6fe-119">Update application</span></span>

<span data-ttu-id="9b6fe-120">pasos de hello toocomplete en este tutorial, debe clonar una copia del programa Hola a aplicaciones de Azure voto.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-120">toocomplete hello steps in this tutorial, you must have cloned a copy of hello Azure Vote application.</span></span> <span data-ttu-id="9b6fe-121">Si es necesario, cree esta copia clonada con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="9b6fe-121">If necessary, create this cloned copy with hello following command:</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="9b6fe-122">Abra hello `config_file.cfg` archivo con cualquier editor de texto o código.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-122">Open hello `config_file.cfg` file with any code or text editor.</span></span> <span data-ttu-id="9b6fe-123">Puede encontrar este archivo en hello siguiendo el directorio del repositorio de hello clonado.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-123">You can find this file under hello following directory of hello cloned repo.</span></span>

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="9b6fe-124">Cambiar los valores de hello de `VOTE1VALUE` y `VOTE2VALUE`y, a continuación, guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-124">Change hello values for `VOTE1VALUE` and `VOTE2VALUE`, and then save hello file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="9b6fe-125">Use [crear docker](https://docs.docker.com/compose/) toore-crear imagen de front-end de Hola y aplicación hello ejecución actualizado.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-125">Use [docker-compose](https://docs.docker.com/compose/) toore-create hello front-end image and run hello updated application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a><span data-ttu-id="9b6fe-126">Prueba local de la aplicación</span><span class="sxs-lookup"><span data-stu-id="9b6fe-126">Test application locally</span></span>

<span data-ttu-id="9b6fe-127">Examinar demasiado`http://localhost:8080` toosee Hola aplicación actualizada.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-127">Browse too`http://localhost:8080` toosee hello updated application.</span></span>

![Imagen del clúster de Kubernetes en Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a><span data-ttu-id="9b6fe-129">Etiquetado e inserción de imágenes</span><span class="sxs-lookup"><span data-stu-id="9b6fe-129">Tag and push images</span></span>

<span data-ttu-id="9b6fe-130">Hola etiqueta *azure front-voto* imagen con hello loginServer de registro de contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-130">Tag hello *azure-vote-front* image with hello loginServer of hello container registry.</span></span>

<span data-ttu-id="9b6fe-131">Si usas registro de contenedor de Azure, obtener el nombre del servidor de inicio de sesión de hello con hello [lista de acr az](/cli/azure/acr#list) comando.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-131">If you're using Azure Container Registry, get hello login server name with hello [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="9b6fe-132">Use [etiqueta docker](https://docs.docker.com/engine/reference/commandline/tag/) imagen de hello tootag.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-132">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) tootag hello image.</span></span> <span data-ttu-id="9b6fe-133">Reemplace `<acrLoginServer>` por el nombre del servidor de inicio de sesión de Azure Container Registry o por el nombre de host de registro público.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-133">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="9b6fe-134">Use [inserción de docker](https://docs.docker.com/engine/reference/commandline/push/) registro tooyour de tooupload Hola imágenes.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-134">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) tooupload hello image tooyour registry.</span></span> <span data-ttu-id="9b6fe-135">Reemplace `<acrLoginServer>` por el nombre del servidor de inicio de sesión de Azure Container Registry o por el nombre de host de registro público.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-135">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a><span data-ttu-id="9b6fe-136">Implementación de una aplicación actualizada</span><span class="sxs-lookup"><span data-stu-id="9b6fe-136">Deploy update application</span></span>

<span data-ttu-id="9b6fe-137">tooensure tiempo de actividad máxima, deben ejecutar varias instancias de pod de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-137">tooensure maximum uptime, multiple instances of hello application pod must be running.</span></span> <span data-ttu-id="9b6fe-138">Compruebe esta configuración con hello [kubectl obtener pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-138">Verify this configuration with hello [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```bash
kubectl get pod
```

<span data-ttu-id="9b6fe-139">Salida:</span><span class="sxs-lookup"><span data-stu-id="9b6fe-139">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="9b6fe-140">Si no dispone de varios pod ejecuta hello azure front-voto imagen, escalar hello *azure front-voto* implementación.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-140">If you don't have multiple pods running hello azure-vote-front image, scale hello *azure-vote-front* deployment.</span></span>


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="9b6fe-141">aplicación de hello tooupdate, use hello [kubectl conjunto](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) comando.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-141">tooupdate hello application, use hello [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) command.</span></span> <span data-ttu-id="9b6fe-142">Actualización `<acrLoginServer>` con el nombre de host o servidor de inicio de sesión de Hola de seguridad del registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-142">Update `<acrLoginServer>` with hello login server or host name of your container registry.</span></span>

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="9b6fe-143">implementación de hello toomonitor, use hello [kubectl obtener pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-143">toomonitor hello deployment, use hello [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span> <span data-ttu-id="9b6fe-144">Tal y como se implementa la aplicación hello actualizado, se terminan y se vuelve a crear con la nueva imagen de contenedor Hola su pod.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-144">As hello updated application is deployed, your pods are terminated and re-created with hello new container image.</span></span>

```azurecli-interactive
kubectl get pod
```

<span data-ttu-id="9b6fe-145">Salida:</span><span class="sxs-lookup"><span data-stu-id="9b6fe-145">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a><span data-ttu-id="9b6fe-146">Prueba de la aplicación actualizada</span><span class="sxs-lookup"><span data-stu-id="9b6fe-146">Test updated application</span></span>

<span data-ttu-id="9b6fe-147">Obtener dirección IP externa de Hola de hello *azure front-voto* servicio.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-147">Get hello external IP address of hello *azure-vote-front* service.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front
```

<span data-ttu-id="9b6fe-148">Examinar toohello IP dirección toosee Hola aplicación actualizada.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-148">Browse toohello IP address toosee hello updated application.</span></span>

![Imagen del clúster de Kubernetes en Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="9b6fe-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9b6fe-150">Next steps</span></span>

<span data-ttu-id="9b6fe-151">En este tutorial, una aplicación actualizada e implantado este clúster de Kubernetes tooa de actualización.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-151">In this tutorial, you updated an application and rolled out this update tooa Kubernetes cluster.</span></span> <span data-ttu-id="9b6fe-152">se completaron Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="9b6fe-152">hello following tasks were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9b6fe-153">Código de la aplicación front-end de hello actualizada</span><span class="sxs-lookup"><span data-stu-id="9b6fe-153">Updated hello front-end application code</span></span>
> * <span data-ttu-id="9b6fe-154">Creó la imagen de contenedor actualizado</span><span class="sxs-lookup"><span data-stu-id="9b6fe-154">Created an updated container image</span></span>
> * <span data-ttu-id="9b6fe-155">Insertar tooAzure de imagen de contenedor de hello del registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="9b6fe-155">Pushed hello container image tooAzure Container Registry</span></span>
> * <span data-ttu-id="9b6fe-156">Aplicación hello implementado actualizado</span><span class="sxs-lookup"><span data-stu-id="9b6fe-156">Deployed hello updated application</span></span>

<span data-ttu-id="9b6fe-157">Avanzar toohello toolearn de tutorial siguiente acerca de cómo toomonitor Kubernetes con Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="9b6fe-157">Advance toohello next tutorial toolearn about how toomonitor Kubernetes with Operations Management Suite.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9b6fe-158">Supervisión de Kubernetes con OMS</span><span class="sxs-lookup"><span data-stu-id="9b6fe-158">Monitor Kubernetes with OMS</span></span>](./container-service-tutorial-kubernetes-monitor.md)