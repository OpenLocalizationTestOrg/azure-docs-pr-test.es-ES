---
title: 'tutorial de instancias de contenedor aaaAzure: preparar el registro de contenedor de Azure | Documentos de Microsoft'
description: "Tutorial de Azure Container Instances: preparación de Azure Container Registry"
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenedores, microservicios, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2525626125740c3c861fad36aad207d0b587ff54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="3bc1d-104">Implementación y uso de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="3bc1d-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="3bc1d-105">Esta es la segunda parte de un tutorial de tres partes.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-105">This is part two of a three-part tutorial.</span></span> <span data-ttu-id="3bc1d-106">Hola [paso anterior](./container-instances-tutorial-prepare-app.md), una imagen de contenedor se creó para una aplicación web simple escrita en [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="3bc1d-106">In hello [previous step](./container-instances-tutorial-prepare-app.md), a container image was created for a simple web application written in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="3bc1d-107">En este tutorial, esta imagen se inserta tooan del registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-107">In this tutorial, this image is pushed tooan Azure Container Registry.</span></span> <span data-ttu-id="3bc1d-108">Si no ha creado la imagen de contenedor de hello, devolver demasiado[Tutorial 1: crear la imagen de contenedor](./container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="3bc1d-108">If you have not created hello container image, return too[Tutorial 1 – Create container image](./container-instances-tutorial-prepare-app.md).</span></span> 

<span data-ttu-id="3bc1d-109">Hola del registro de contenedor de Azure es un registro basado en Azure, privado, para las imágenes de contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-109">hello Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="3bc1d-110">Este tutorial le guía a través de la implementación de una instancia de registro de contenedor de Azure e insertar un tooit de imagen de contenedor.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-110">This tutorial walks through deploying an Azure Container Registry instance, and pushing a container image tooit.</span></span> <span data-ttu-id="3bc1d-111">Los pasos completados incluyen:</span><span class="sxs-lookup"><span data-stu-id="3bc1d-111">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3bc1d-112">Implementación de una instancia de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="3bc1d-112">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="3bc1d-113">Etiquetado de una imagen de contenedor para Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="3bc1d-113">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="3bc1d-114">Cargar imagen tooAzure del registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="3bc1d-114">Uploading image tooAzure Container Registry</span></span>

<span data-ttu-id="3bc1d-115">En los tutoriales posteriores, implemente el contenedor de Hola desde su tooAzure registro privada instancias de contenedor.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-115">In subsequent tutorials, you deploy hello container from your private registry tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3bc1d-116">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="3bc1d-116">Before you begin</span></span>

<span data-ttu-id="3bc1d-117">Este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-117">This tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="3bc1d-118">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3bc1d-119">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3bc1d-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="3bc1d-120">Implementación de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="3bc1d-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="3bc1d-121">Para implementar Azure Container Registry, necesita tener antes un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="3bc1d-122">Un grupo de recursos de Azure es una colección lógica en la que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-122">An Azure resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="3bc1d-123">Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-123">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="3bc1d-124">En este ejemplo, un grupo de recursos denominado *myResourceGroup* se crea en hello *eastus* región.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-124">In this example, a resource group named *myResourceGroup* is created in hello *eastus* region.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="3bc1d-125">Crear un registro de contenedor de Azure con hello [crear acr az](/cli/azure/acr#create) comando.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-125">Create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="3bc1d-126">nombre de Hola de un registro de contenedor **deben ser únicos**.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-126">hello name of a Container Registry **must be unique**.</span></span> <span data-ttu-id="3bc1d-127">En el siguiente ejemplo de Hola, usamos nombre hello *mycontainerregistry082*.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-127">In hello following example, we use hello name *mycontainerregistry082*.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

<span data-ttu-id="3bc1d-128">A lo largo del resto de Hola de este tutorial, usamos `<acrname>` como un marcador de posición para el nombre del registro de hello contenedor que eligió.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-128">Throughout hello rest of this tutorial, we use `<acrname>` as a placeholder for hello container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="3bc1d-129">Inicio de sesión en Container Registry</span><span class="sxs-lookup"><span data-stu-id="3bc1d-129">Container registry login</span></span>

<span data-ttu-id="3bc1d-130">Debe iniciar sesión en la instancia ACR tooyour antes de insertar imágenes tooit.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-130">You must log in tooyour ACR instance before pushing images tooit.</span></span> <span data-ttu-id="3bc1d-131">Hola de uso [inicio de sesión de acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) operación de hello toocomplete de comandos.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-131">Use hello [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command toocomplete hello operation.</span></span> <span data-ttu-id="3bc1d-132">Necesita tooprovide Hola único nombre dado del registro de contenedor de toohello cuando se creó.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-132">You need tooprovide hello unique name given toohello container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="3bc1d-133">comando de Hello devuelve un mensaje de 'Inicio de sesión correcto' cuando se haya completado.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-133">hello command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-image"></a><span data-ttu-id="3bc1d-134">Etiquetado de la imagen de contenedor</span><span class="sxs-lookup"><span data-stu-id="3bc1d-134">Tag container image</span></span>

<span data-ttu-id="3bc1d-135">toodeploy una imagen de contenedor de un registro privada, imagen Hola necesita toobe etiquetado con hello `loginServer` nombre del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-135">toodeploy a container image from a private registry, hello image needs toobe tagged with hello `loginServer` name of hello registry.</span></span>

<span data-ttu-id="3bc1d-136">una lista de imágenes actuales, use hello toosee `docker images` comando.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-136">toosee a list of current images, use hello `docker images` command.</span></span>

```bash
docker images
```

<span data-ttu-id="3bc1d-137">Salida:</span><span class="sxs-lookup"><span data-stu-id="3bc1d-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

<span data-ttu-id="3bc1d-138">nombre de loginServer en hello tooget, ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-138">tooget hello loginServer name, run hello following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="3bc1d-139">Hola etiqueta *aplicación de tutorial de aci* imagen con hello loginServer de registro de contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-139">Tag hello *aci-tutorial-app* image with hello loginServer of hello container registry.</span></span> <span data-ttu-id="3bc1d-140">Además, agregue `:v1` toohello final del nombre de la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-140">Also, add `:v1` toohello end of hello image name.</span></span> <span data-ttu-id="3bc1d-141">Esta etiqueta indica el número de versión de imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-141">This tag indicates hello image version number.</span></span>

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

<span data-ttu-id="3bc1d-142">Una vez que estén etiquetadas, ejecutar `docker images` operación de hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-142">Once tagged, run `docker images` tooverify hello operation.</span></span>

```bash
docker images
```

<span data-ttu-id="3bc1d-143">Salida:</span><span class="sxs-lookup"><span data-stu-id="3bc1d-143">Output:</span></span>

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-tooazure-container-registry"></a><span data-ttu-id="3bc1d-144">Insertar imagen tooAzure del registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="3bc1d-144">Push image tooAzure Container Registry</span></span>

<span data-ttu-id="3bc1d-145">Insertar hello *aplicación de tutorial de aci* registro toohello de imágenes.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-145">Push hello *aci-tutorial-app* image toohello registry.</span></span>

<span data-ttu-id="3bc1d-146">Con el siguiente ejemplo de Hola, sustituya Hola contenedor del registro loginServer con loginServer Hola de su entorno.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-146">Using hello following example, replace hello container registry loginServer name with hello loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a><span data-ttu-id="3bc1d-147">Lista de imágenes en Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="3bc1d-147">List images in Azure Container Registry</span></span>

<span data-ttu-id="3bc1d-148">una lista de imágenes que se han insertado tooyour registro de contenedor de Azure, Hola usuario tooreturn [lista de repositorios de acr az](/cli/azure/acr/repository#list) comando.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-148">tooreturn a list of images that have been pushed tooyour Azure Container registry, user hello [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="3bc1d-149">Actualizar un comando hello con el nombre de registro del contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-149">Update hello command with hello container registry name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="3bc1d-150">Salida:</span><span class="sxs-lookup"><span data-stu-id="3bc1d-150">Output:</span></span>

```azurecli
Result
----------------
aci-tutorial-app
```

<span data-ttu-id="3bc1d-151">Y, a continuación, etiquetas de hello toosee para una imagen específica, use hello [az acr repositorio Mostrar etiquetas](/cli/azure/acr/repository#show-tags) comando.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-151">And then toosee hello tags for a specific image, use hello [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

<span data-ttu-id="3bc1d-152">Salida:</span><span class="sxs-lookup"><span data-stu-id="3bc1d-152">Output:</span></span>

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a><span data-ttu-id="3bc1d-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3bc1d-153">Next steps</span></span>

<span data-ttu-id="3bc1d-154">En este tutorial, un registro de contenedor de Azure se ha preparado para su uso con instancias de contenedor de Azure y se inserta la imagen de contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-154">In this tutorial, an Azure Container Registry was prepared for use with Azure Container Instances, and hello container image was pushed.</span></span> <span data-ttu-id="3bc1d-155">se completaron Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3bc1d-155">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3bc1d-156">Implementación de una instancia de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="3bc1d-156">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="3bc1d-157">Etiquetado de una imagen de contenedor para Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="3bc1d-157">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="3bc1d-158">Cargar imagen tooAzure del registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="3bc1d-158">Uploading image tooAzure Container Registry</span></span>

<span data-ttu-id="3bc1d-159">Avanzar toohello toolearn de tutorial siguiente acerca de la implementación Hola contenedor tooAzure mediante instancias de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="3bc1d-159">Advance toohello next tutorial toolearn about deploying hello container tooAzure using Azure Container Instances.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3bc1d-160">Implementar contenedores tooAzure instancias de contenedor</span><span class="sxs-lookup"><span data-stu-id="3bc1d-160">Deploy containers tooAzure Container Instances</span></span>](./container-instances-tutorial-deploy-app.md)
