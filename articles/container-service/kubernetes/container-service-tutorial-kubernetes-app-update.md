---
title: "Tutorial de Azure Container Service: actualización de una aplicación | Microsoft Docs"
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
ms.openlocfilehash: db580da3e2d70892bc37305394df5be609ebb8a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="update-an-application-in-kubernetes"></a><span data-ttu-id="d36e0-104">Actualización de una aplicación en Kubernetes</span><span class="sxs-lookup"><span data-stu-id="d36e0-104">Update an application in Kubernetes</span></span>

<span data-ttu-id="d36e0-105">Después de implementar una aplicación en Kubernetes, se puede actualizar mediante la especificación de una nueva imagen de contenedor o la versión de la imagen.</span><span class="sxs-lookup"><span data-stu-id="d36e0-105">After you deploy an application in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="d36e0-106">Cuando se actualiza una aplicación, el lanzamiento de la actualización se preconfigura para que solo una parte de la implementación se actualice simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="d36e0-106">When you update an application, the update rollout is staged so that only a portion of the deployment is concurrently updated.</span></span> <span data-ttu-id="d36e0-107">Esta actualización preconfigurada permite que la aplicación siga ejecutándose durante la actualización y proporciona un mecanismo de reversión si se produce un error de implementación.</span><span class="sxs-lookup"><span data-stu-id="d36e0-107">This staged update enables the application to keep running during the update, and provides a rollback mechanism if a deployment failure occurs.</span></span> 

<span data-ttu-id="d36e0-108">En este tutorial, la sección seis de siete, se actualiza la aplicación de ejemplo de Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="d36e0-108">In this tutorial, part six of seven, the sample Azure Vote app is updated.</span></span> <span data-ttu-id="d36e0-109">Las tareas que debe completar incluyen las siguientes:</span><span class="sxs-lookup"><span data-stu-id="d36e0-109">Tasks that you complete include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d36e0-110">Actualización del código de aplicación front-end</span><span class="sxs-lookup"><span data-stu-id="d36e0-110">Updating the front-end application code</span></span>
> * <span data-ttu-id="d36e0-111">Creación de una imagen de contenedor actualizado</span><span class="sxs-lookup"><span data-stu-id="d36e0-111">Creating an updated container image</span></span>
> * <span data-ttu-id="d36e0-112">Inserción de una imagen de contenedor en Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="d36e0-112">Pushing the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="d36e0-113">Implementación de una imagen de contenedor actualizado</span><span class="sxs-lookup"><span data-stu-id="d36e0-113">Deploying the updated container image</span></span>

<span data-ttu-id="d36e0-114">En tutoriales posteriores, se configura Operations Management Suite para supervisar el clúster de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="d36e0-114">In subsequent tutorials, Operations Management Suite is configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d36e0-115">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="d36e0-115">Before you begin</span></span>

<span data-ttu-id="d36e0-116">En tutoriales anteriores se ha empaquetado una aplicación en una imagen de contenedor, se ha cargado la imagen en Azure Container Registry y se ha creado un clúster de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="d36e0-116">In previous tutorials, an application was packaged into a container image, the image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="d36e0-117">La aplicación se ejecutó después en el clúster de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="d36e0-117">The application was then run on the Kubernetes cluster.</span></span> 

<span data-ttu-id="d36e0-118">Si no ha finalizado estos pasos y desea continuar, vuelva al [Tutorial 1: Creación de las imágenes de contenedor](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="d36e0-118">If you haven't completed these steps, and want to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-application"></a><span data-ttu-id="d36e0-119">Actualización de una aplicación</span><span class="sxs-lookup"><span data-stu-id="d36e0-119">Update application</span></span>

<span data-ttu-id="d36e0-120">Para completar los pasos de este tutorial, debe clonar una copia de la aplicación Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="d36e0-120">To complete the steps in this tutorial, you must have cloned a copy of the Azure Vote application.</span></span> <span data-ttu-id="d36e0-121">Si es necesario, cree esta copia clonada con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="d36e0-121">If necessary, create this cloned copy with the following command:</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="d36e0-122">Abra el archivo `config_file.cfg` con cualquier editor de texto o código.</span><span class="sxs-lookup"><span data-stu-id="d36e0-122">Open the `config_file.cfg` file with any code or text editor.</span></span> <span data-ttu-id="d36e0-123">Puede encontrar este archivo en el siguiente directorio del repositorio clonado.</span><span class="sxs-lookup"><span data-stu-id="d36e0-123">You can find this file under the following directory of the cloned repo.</span></span>

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="d36e0-124">Cambie los valores de `VOTE1VALUE` y `VOTE2VALUE` y, después, guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="d36e0-124">Change the values for `VOTE1VALUE` and `VOTE2VALUE`, and then save the file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="d36e0-125">Use [docker-compose](https://docs.docker.com/compose/) para volver a crear la imagen de front-end y ejecutar la aplicación actualizada.</span><span class="sxs-lookup"><span data-stu-id="d36e0-125">Use [docker-compose](https://docs.docker.com/compose/) to re-create the front-end image and run the updated application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a><span data-ttu-id="d36e0-126">Prueba local de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d36e0-126">Test application locally</span></span>

<span data-ttu-id="d36e0-127">Navegue hasta `http://localhost:8080` para ver la aplicación actualizada.</span><span class="sxs-lookup"><span data-stu-id="d36e0-127">Browse to `http://localhost:8080` to see the updated application.</span></span>

![Imagen del clúster de Kubernetes en Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a><span data-ttu-id="d36e0-129">Etiquetado e inserción de imágenes</span><span class="sxs-lookup"><span data-stu-id="d36e0-129">Tag and push images</span></span>

<span data-ttu-id="d36e0-130">Etiquete la imagen *azure-vote-front* con el loginServer del registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="d36e0-130">Tag the *azure-vote-front* image with the loginServer of the container registry.</span></span>

<span data-ttu-id="d36e0-131">Si usa Azure Container Registry, obtenga el nombre del servidor de inicio de sesión con el comando [az acr list](/cli/azure/acr#list).</span><span class="sxs-lookup"><span data-stu-id="d36e0-131">If you're using Azure Container Registry, get the login server name with the [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="d36e0-132">Use la [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) para etiquetar la imagen.</span><span class="sxs-lookup"><span data-stu-id="d36e0-132">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) to tag the image.</span></span> <span data-ttu-id="d36e0-133">Reemplace `<acrLoginServer>` por el nombre del servidor de inicio de sesión de Azure Container Registry o por el nombre de host de registro público.</span><span class="sxs-lookup"><span data-stu-id="d36e0-133">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="d36e0-134">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) para cargar la imagen en el registro.</span><span class="sxs-lookup"><span data-stu-id="d36e0-134">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) to upload the image to your registry.</span></span> <span data-ttu-id="d36e0-135">Reemplace `<acrLoginServer>` por el nombre del servidor de inicio de sesión de Azure Container Registry o por el nombre de host de registro público.</span><span class="sxs-lookup"><span data-stu-id="d36e0-135">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a><span data-ttu-id="d36e0-136">Implementación de una aplicación actualizada</span><span class="sxs-lookup"><span data-stu-id="d36e0-136">Deploy update application</span></span>

<span data-ttu-id="d36e0-137">Para garantizar el tiempo máximo de actividad, se deben ejecutar varias instancias de pod de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d36e0-137">To ensure maximum uptime, multiple instances of the application pod must be running.</span></span> <span data-ttu-id="d36e0-138">Compruebe esta configuración con el comando [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get).</span><span class="sxs-lookup"><span data-stu-id="d36e0-138">Verify this configuration with the [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```bash
kubectl get pod
```

<span data-ttu-id="d36e0-139">Salida:</span><span class="sxs-lookup"><span data-stu-id="d36e0-139">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="d36e0-140">Si no tiene varios pods ejecutando la imagen de azure-vote-front, escale la implementación de *azure-vote-front*.</span><span class="sxs-lookup"><span data-stu-id="d36e0-140">If you don't have multiple pods running the azure-vote-front image, scale the *azure-vote-front* deployment.</span></span>


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="d36e0-141">Use el comando [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) para actualizar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d36e0-141">To update the application, use the [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) command.</span></span> <span data-ttu-id="d36e0-142">Actualice `<acrLoginServer>` con el nombre de host o servidor de inicio de sesión del registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="d36e0-142">Update `<acrLoginServer>` with the login server or host name of your container registry.</span></span>

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="d36e0-143">Para supervisar la implementación, use el comando [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get).</span><span class="sxs-lookup"><span data-stu-id="d36e0-143">To monitor the deployment, use the [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span> <span data-ttu-id="d36e0-144">A medida que se implementa la aplicación actualizada, sus pods se terminan y se vuelven a crear con la nueva imagen de contenedor.</span><span class="sxs-lookup"><span data-stu-id="d36e0-144">As the updated application is deployed, your pods are terminated and re-created with the new container image.</span></span>

```azurecli-interactive
kubectl get pod
```

<span data-ttu-id="d36e0-145">Salida:</span><span class="sxs-lookup"><span data-stu-id="d36e0-145">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a><span data-ttu-id="d36e0-146">Prueba de la aplicación actualizada</span><span class="sxs-lookup"><span data-stu-id="d36e0-146">Test updated application</span></span>

<span data-ttu-id="d36e0-147">Obtenga la dirección IP externa del servicio *azure -vote-front*.</span><span class="sxs-lookup"><span data-stu-id="d36e0-147">Get the external IP address of the *azure-vote-front* service.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front
```

<span data-ttu-id="d36e0-148">Navegue hasta la dirección IP para ver la aplicación actualizada.</span><span class="sxs-lookup"><span data-stu-id="d36e0-148">Browse to the IP address to see the updated application.</span></span>

![Imagen del clúster de Kubernetes en Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="d36e0-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d36e0-150">Next steps</span></span>

<span data-ttu-id="d36e0-151">En este tutorial, actualiza una aplicación y se implanta esta actualización en un clúster de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="d36e0-151">In this tutorial, you updated an application and rolled out this update to a Kubernetes cluster.</span></span> <span data-ttu-id="d36e0-152">Se completaron las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="d36e0-152">The following tasks were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d36e0-153">Actualizó el código de aplicación de front-end</span><span class="sxs-lookup"><span data-stu-id="d36e0-153">Updated the front-end application code</span></span>
> * <span data-ttu-id="d36e0-154">Creó la imagen de contenedor actualizado</span><span class="sxs-lookup"><span data-stu-id="d36e0-154">Created an updated container image</span></span>
> * <span data-ttu-id="d36e0-155">Insertó una imagen de contenedor en Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="d36e0-155">Pushed the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="d36e0-156">Implemento la aplicación actualizada</span><span class="sxs-lookup"><span data-stu-id="d36e0-156">Deployed the updated application</span></span>

<span data-ttu-id="d36e0-157">Avance al siguiente tutorial para obtener información sobre cómo supervisar Kubernetes con Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="d36e0-157">Advance to the next tutorial to learn about how to monitor Kubernetes with Operations Management Suite.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d36e0-158">Supervisión de Kubernetes con OMS</span><span class="sxs-lookup"><span data-stu-id="d36e0-158">Monitor Kubernetes with OMS</span></span>](./container-service-tutorial-kubernetes-monitor.md)