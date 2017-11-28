---
title: registro de contenedor de Docker privada de aaaCreate - CLI de Azure | Documentos de Microsoft
description: Empezar a crear y administrar registros de contenedor de Docker privados con hello 2.0 de CLI de Azure
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 2cadf42db0681a09c95486510f1e65c6f87c5280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-cli"></a><span data-ttu-id="49446-103">Crear un registro de contenedor administrado mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="49446-103">Create a managed container registry using hello Azure CLI</span></span>

<span data-ttu-id="49446-104">Azure Container Registry es un servicio de registro de contenedores de Docker administrado usado para almacenar imágenes de contenedor de Docker privadas.</span><span class="sxs-lookup"><span data-stu-id="49446-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="49446-105">Esta guía se detalla la creación de una instancia de registro de contenedor de Azure administrados mediante Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="49446-105">This guide details creating a managed Azure Container Registry instance using hello Azure CLI.</span></span>

<span data-ttu-id="49446-106">Azure Container Registry está en versión preliminar y no está disponible en todas las regiones.</span><span class="sxs-lookup"><span data-stu-id="49446-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="49446-107">Si elige tooinstall y usar hello CLI localmente, este tutorial rápido requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="49446-107">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="49446-108">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="49446-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="49446-109">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="49446-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="49446-110">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="49446-110">Create a resource group</span></span>

<span data-ttu-id="49446-111">Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="49446-111">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="49446-112">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="49446-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="49446-113">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *westcentralus* ubicación.</span><span class="sxs-lookup"><span data-stu-id="49446-113">hello following example creates a resource group named *myResourceGroup* in hello *westcentralus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a><span data-ttu-id="49446-114">Creación de un registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="49446-114">Create a container registry</span></span>

<span data-ttu-id="49446-115">Crear una instancia ACR mediante hello [crear acr az](/cli/azure/acr#create) comando.</span><span class="sxs-lookup"><span data-stu-id="49446-115">Create an ACR instance using hello [az acr create](/cli/azure/acr#create) command.</span></span>

> [!NOTE]
> <span data-ttu-id="49446-116">Cuando cree un registro, especifique un nombre de dominio de nivel superior único global que contenga solo letras y números.</span><span class="sxs-lookup"><span data-stu-id="49446-116">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span>

 <span data-ttu-id="49446-117">nombre del registro de Hello en el ejemplo de Hola *myContainerRegistry1*, sustituir un nombre único de su elección.</span><span class="sxs-lookup"><span data-stu-id="49446-117">hello registry name in hello example is *myContainerRegistry1*, substitute a unique name of your own.</span></span>

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

<span data-ttu-id="49446-118">Cuando se crea el registro de hello, salida de hello es siguiente de toohello similar:</span><span class="sxs-lookup"><span data-stu-id="49446-118">When hello registry is created, hello output is similar toohello following:</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-29T04:50:28.607134+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry1",
  "location": "westcentralus",
  "loginServer": "mycontainerregistry1.azurecr.io",
  "name": "myContainerRegistry1",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Managed_Standard",
    "tier": "Managed"
  },
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

## <a name="log-in-tooacr-instance"></a><span data-ttu-id="49446-119">Inicie sesión en la instancia de tooACR</span><span class="sxs-lookup"><span data-stu-id="49446-119">Log in tooACR instance</span></span>

<span data-ttu-id="49446-120">Antes de insertar y extraer imágenes de contenedor, primero debe iniciar sesión en la instancia ACR toohello.</span><span class="sxs-lookup"><span data-stu-id="49446-120">Before pushing and pulling container images, you must log in toohello ACR instance.</span></span> <span data-ttu-id="49446-121">toodo por lo tanto, usar hello [inicio de sesión de acr az](/cli/azure/acr#login) comando.</span><span class="sxs-lookup"><span data-stu-id="49446-121">toodo so, use hello [az acr login](/cli/azure/acr#login) command.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

<span data-ttu-id="49446-122">comando de Hello devuelve un mensaje de 'Inicio de sesión correcto' cuando se haya completado.</span><span class="sxs-lookup"><span data-stu-id="49446-122">hello command returns a 'Login Succeeded' message once completed.</span></span>

## <a name="use-azure-container-registry"></a><span data-ttu-id="49446-123">Uso de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="49446-123">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="49446-124">Lista de imágenes de contenedor</span><span class="sxs-lookup"><span data-stu-id="49446-124">List container images</span></span>

<span data-ttu-id="49446-125">Hola de uso `az acr` tooquery imágenes de Hola y etiquetas en un repositorio de los comandos de CLI.</span><span class="sxs-lookup"><span data-stu-id="49446-125">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="49446-126">Actualmente, el registro de contenedor no admite hello `docker search` tooquery de comando para imágenes y etiquetas.</span><span class="sxs-lookup"><span data-stu-id="49446-126">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="49446-127">Lista de repositorios</span><span class="sxs-lookup"><span data-stu-id="49446-127">List repositories</span></span>

<span data-ttu-id="49446-128">Hello en el ejemplo siguiente se enumera los repositorios de hello en un registro, en formato JSON (JavaScript Object Notation):</span><span class="sxs-lookup"><span data-stu-id="49446-128">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="49446-129">Lista de etiquetas</span><span class="sxs-lookup"><span data-stu-id="49446-129">List tags</span></span>

<span data-ttu-id="49446-130">Hello en el ejemplo siguiente se muestra etiquetas de hello en hello **ejemplos/nginx** repositorio, en formato JSON:</span><span class="sxs-lookup"><span data-stu-id="49446-130">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="49446-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="49446-131">Next steps</span></span>

<span data-ttu-id="49446-132">En este tutorial, ha creado una instancia administrada de registro de contenedor de Azure con hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="49446-132">In this quick start, you've created a managed Azure Container Registry instance using hello Azure CLI.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="49446-133">Insertar la primera imagen con hello CLI de Docker</span><span class="sxs-lookup"><span data-stu-id="49446-133">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
