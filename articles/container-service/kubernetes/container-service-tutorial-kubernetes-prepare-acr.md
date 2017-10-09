---
title: tutorial de servicio de contenedor de aaaAzure - preparar ACR | Documentos de Microsoft
description: "Tutorial de Azure Container Service tutorial: preparación de ACR"
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
ms.openlocfilehash: 3980e5ce4eb9836f83c761a2f76c944bb3f13060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="cece0-104">Implementación y uso de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="cece0-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="cece0-105">Azure Container Registry (ACR) es un registro privado basado en Azure para imágenes de contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="cece0-105">Azure Container Registry (ACR) is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="cece0-106">Este tutorial, la segunda parte de siete, explica paso a paso de implementación de una instancia de registro de contenedor de Azure e insertar un tooit de imagen de contenedor.</span><span class="sxs-lookup"><span data-stu-id="cece0-106">This tutorial, part two of seven, walks through deploying an Azure Container Registry instance, and pushing a container image tooit.</span></span> <span data-ttu-id="cece0-107">Los pasos completados incluyen:</span><span class="sxs-lookup"><span data-stu-id="cece0-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cece0-108">Implementación de una instancia de Azure Container Registry (ACR)</span><span class="sxs-lookup"><span data-stu-id="cece0-108">Deploying an Azure Container Registry (ACR) instance</span></span>
> * <span data-ttu-id="cece0-109">Etiquetado de una imagen de contenedor para ACR</span><span class="sxs-lookup"><span data-stu-id="cece0-109">Tagging a container image for ACR</span></span>
> * <span data-ttu-id="cece0-110">Cargando Hola imagen tooACR</span><span class="sxs-lookup"><span data-stu-id="cece0-110">Uploading hello image tooACR</span></span>

<span data-ttu-id="cece0-111">En posteriores tutoriales, esta instancia de ACR se integra con un clúster de Kubernetes en Azure Container Service, para la ejecución segura de imágenes de contenedor.</span><span class="sxs-lookup"><span data-stu-id="cece0-111">In subsequent tutorials, this ACR instance is integrated with an Azure Container Service Kubernetes cluster, for securely running container images.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="cece0-112">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="cece0-112">Before you begin</span></span>

<span data-ttu-id="cece0-113">Hola [tutorial anterior](./container-service-tutorial-kubernetes-prepare-app.md), una imagen de contenedor se creó para una aplicación sencilla de votación de Azure.</span><span class="sxs-lookup"><span data-stu-id="cece0-113">In hello [previous tutorial](./container-service-tutorial-kubernetes-prepare-app.md), a container image was created for a simple Azure Voting application.</span></span> <span data-ttu-id="cece0-114">En este tutorial, esta imagen se inserta tooan del registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="cece0-114">In this tutorial, this image is pushed tooan Azure Container Registry.</span></span> <span data-ttu-id="cece0-115">Si no ha creado la imagen de aplicación de Azure votos hello, devolver demasiado[Tutorial 1: crear imágenes del contenedor](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="cece0-115">If you have not created hello Azure Voting app image, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> <span data-ttu-id="cece0-116">Como alternativa, los pasos de hello aquí detallan trabajar con cualquier imagen de contenedor.</span><span class="sxs-lookup"><span data-stu-id="cece0-116">Alternatively, hello steps detailed here work with any container image.</span></span>

<span data-ttu-id="cece0-117">Este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="cece0-117">This tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="cece0-118">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="cece0-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="cece0-119">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cece0-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="cece0-120">Implementación de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="cece0-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="cece0-121">Para implementar Azure Container Registry, necesita tener antes un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cece0-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="cece0-122">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="cece0-122">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="cece0-123">Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="cece0-123">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="cece0-124">En este ejemplo, un grupo de recursos denominado *myResourceGroup* se crea en hello *westeurope* región.</span><span class="sxs-lookup"><span data-stu-id="cece0-124">In this example, a resource group named *myResourceGroup* is created in hello *westeurope* region.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="cece0-125">Crear un registro de contenedor de Azure con hello [crear acr az](/cli/azure/acr#create) comando.</span><span class="sxs-lookup"><span data-stu-id="cece0-125">Create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="cece0-126">nombre de Hola de un registro de contenedor **deben ser únicos**.</span><span class="sxs-lookup"><span data-stu-id="cece0-126">hello name of a Container Registry **must be unique**.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

<span data-ttu-id="cece0-127">A lo largo del resto de Hola de este tutorial, usamos "acrname" como un marcador de posición para el nombre del registro de hello contenedor que eligió.</span><span class="sxs-lookup"><span data-stu-id="cece0-127">Throughout hello rest of this tutorial, we use "acrname" as a placeholder for hello container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="cece0-128">Inicio de sesión en Container Registry</span><span class="sxs-lookup"><span data-stu-id="cece0-128">Container registry login</span></span>

<span data-ttu-id="cece0-129">Debe iniciar sesión en la instancia ACR tooyour antes de insertar imágenes tooit.</span><span class="sxs-lookup"><span data-stu-id="cece0-129">You must log in tooyour ACR instance before pushing images tooit.</span></span> <span data-ttu-id="cece0-130">Hola de uso [inicio de sesión de acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) operación de hello toocomplete de comandos.</span><span class="sxs-lookup"><span data-stu-id="cece0-130">Use hello [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command toocomplete hello operation.</span></span> <span data-ttu-id="cece0-131">Necesita tooprovide Hola único nombre dado del registro de contenedor de toohello cuando se creó.</span><span class="sxs-lookup"><span data-stu-id="cece0-131">You need tooprovide hello unique name given toohello container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="cece0-132">comando de Hello devuelve un mensaje de 'Inicio de sesión correcto' cuando se haya completado.</span><span class="sxs-lookup"><span data-stu-id="cece0-132">hello command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-images"></a><span data-ttu-id="cece0-133">Etiquetado de imágenes de contenedor</span><span class="sxs-lookup"><span data-stu-id="cece0-133">Tag container images</span></span>

<span data-ttu-id="cece0-134">Cada imagen de contenedor debe toobe etiquetado con el nombre de hello loginServer del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="cece0-134">Each container image needs toobe tagged with hello loginServer name of hello registry.</span></span> <span data-ttu-id="cece0-135">Esta etiqueta se utiliza para el enrutamiento al activar el registro de imágenes de tooan de imágenes de contenedor.</span><span class="sxs-lookup"><span data-stu-id="cece0-135">This tag is used for routing when pushing container images tooan image registry.</span></span>

<span data-ttu-id="cece0-136">una lista de imágenes actuales, use hello toosee [imágenes de docker](https://docs.docker.com/engine/reference/commandline/images/) comando.</span><span class="sxs-lookup"><span data-stu-id="cece0-136">toosee a list of current images, use hello [docker images](https://docs.docker.com/engine/reference/commandline/images/) command.</span></span>

```bash
docker images
```

<span data-ttu-id="cece0-137">Salida:</span><span class="sxs-lookup"><span data-stu-id="cece0-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="cece0-138">nombre de loginServer en hello tooget, ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="cece0-138">tooget hello loginServer name, run hello following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="cece0-139">Ahora, Hola de etiqueta *azure front-voto* imagen con hello loginServer de registro de contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="cece0-139">Now, tag hello *azure-vote-front* image with hello loginServer of hello container registry.</span></span> <span data-ttu-id="cece0-140">Además, agregue `:redis-v1` toohello final del nombre de la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="cece0-140">Also, add `:redis-v1` toohello end of hello image name.</span></span> <span data-ttu-id="cece0-141">Esta etiqueta indica la versión de la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="cece0-141">This tag indicates hello image version.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="cece0-142">Una vez que estén etiquetadas, ejecute [imágenes de docker] operación de hello tooverify (https://docs.docker.com/engine/reference/commandline/images/).</span><span class="sxs-lookup"><span data-stu-id="cece0-142">Once tagged, run [docker images] (https://docs.docker.com/engine/reference/commandline/images/) tooverify hello operation.</span></span>

```bash
docker images
```

<span data-ttu-id="cece0-143">Salida:</span><span class="sxs-lookup"><span data-stu-id="cece0-143">Output:</span></span>

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-tooregistry"></a><span data-ttu-id="cece0-144">Insertar imágenes tooregistry</span><span class="sxs-lookup"><span data-stu-id="cece0-144">Push images tooregistry</span></span>

<span data-ttu-id="cece0-145">Insertar hello *azure front-voto* registro toohello de imágenes.</span><span class="sxs-lookup"><span data-stu-id="cece0-145">Push hello *azure-vote-front* image toohello registry.</span></span> 

<span data-ttu-id="cece0-146">Con el siguiente ejemplo de Hola, sustituya Hola ACR loginServer con loginServer Hola de su entorno.</span><span class="sxs-lookup"><span data-stu-id="cece0-146">Using hello following example, replace hello ACR loginServer name with hello loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="cece0-147">Esto tiene un par de minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="cece0-147">This takes a couple of minutes toocomplete.</span></span>

## <a name="list-images-in-registry"></a><span data-ttu-id="cece0-148">Lista de imágenes en el registro</span><span class="sxs-lookup"><span data-stu-id="cece0-148">List images in registry</span></span>

<span data-ttu-id="cece0-149">una lista de imágenes que se han insertado tooyour registro de contenedor de Azure, Hola usuario tooreturn [lista de repositorios de acr az](/cli/azure/acr/repository#list) comando.</span><span class="sxs-lookup"><span data-stu-id="cece0-149">tooreturn a list of images that have been pushed tooyour Azure Container registry, user hello [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="cece0-150">Actualizar un comando hello con nombre de instancia ACR Hola.</span><span class="sxs-lookup"><span data-stu-id="cece0-150">Update hello command with hello ACR instance name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="cece0-151">Salida:</span><span class="sxs-lookup"><span data-stu-id="cece0-151">Output:</span></span>

```azurecli
Result
----------------
azure-vote-front
```

<span data-ttu-id="cece0-152">Y, a continuación, etiquetas de hello toosee para una imagen específica, use hello [az acr repositorio Mostrar etiquetas](/cli/azure/acr/repository#show-tags) comando.</span><span class="sxs-lookup"><span data-stu-id="cece0-152">And then toosee hello tags for a specific image, use hello [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

<span data-ttu-id="cece0-153">Salida:</span><span class="sxs-lookup"><span data-stu-id="cece0-153">Output:</span></span>

```azurecli
Result
--------
redis-v1
```

<span data-ttu-id="cece0-154">Tutorial se complete, imagen de contenedor de Hola se ha almacenado en una instancia de registro de contenedor de Azure privada.</span><span class="sxs-lookup"><span data-stu-id="cece0-154">At tutorial completion, hello container image has been stored in a private Azure Container Registry instance.</span></span> <span data-ttu-id="cece0-155">Esta imagen se implementa de clúster ACR tooa Kubernetes en los tutoriales posteriores.</span><span class="sxs-lookup"><span data-stu-id="cece0-155">This image is deployed from ACR tooa Kubernetes cluster in subsequent tutorials.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cece0-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cece0-156">Next steps</span></span>

<span data-ttu-id="cece0-157">En este tutorial, se ha preparado una instancia de Azure Container Registry para su uso en un clúster de ACS Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="cece0-157">In this tutorial, an Azure Container Registry was prepared for use in an ACS Kubernetes cluster.</span></span> <span data-ttu-id="cece0-158">se completaron Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="cece0-158">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cece0-159">Implementación de una instancia de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="cece0-159">Deployed an Azure Container Registry instance</span></span>
> * <span data-ttu-id="cece0-160">Etiquetado de una imagen de contenedor para ACR</span><span class="sxs-lookup"><span data-stu-id="cece0-160">Tagged a container image for ACR</span></span>
> * <span data-ttu-id="cece0-161">Hola cargado imagen tooACR</span><span class="sxs-lookup"><span data-stu-id="cece0-161">Uploaded hello image tooACR</span></span>

<span data-ttu-id="cece0-162">Avanzar toohello toolearn de tutorial siguiente acerca de cómo implementar un clúster de Kubernetes en Azure.</span><span class="sxs-lookup"><span data-stu-id="cece0-162">Advance toohello next tutorial toolearn about deploying a Kubernetes cluster in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cece0-163">Implementación de un clúster de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cece0-163">Deploy Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-deploy-cluster.md)