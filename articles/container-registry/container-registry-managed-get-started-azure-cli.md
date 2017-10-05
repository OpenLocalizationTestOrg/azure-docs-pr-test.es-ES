---
title: "Creación del registro de contenedores privado de Docker: CLI de Azure | Microsoft Docs"
description: "Introducción a la creación y la administración de registros de contenedor privados de Docker mediante la CLI de Azure 2.0"
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
ms.openlocfilehash: c7cdb1b13bf32388d18c2a25af28337a81861c1e
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-managed-container-registry-using-the-azure-cli"></a><span data-ttu-id="3caae-103">Creación de un registro de contenedores administrado mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="3caae-103">Create a managed container registry using the Azure CLI</span></span>

<span data-ttu-id="3caae-104">Azure Container Registry es un servicio de registro de contenedores de Docker administrado usado para almacenar imágenes de contenedor de Docker privadas.</span><span class="sxs-lookup"><span data-stu-id="3caae-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="3caae-105">Esta guía detalla la creación de una instancia administrada de Azure Container Registry mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="3caae-105">This guide details creating a managed Azure Container Registry instance using the Azure CLI.</span></span>

<span data-ttu-id="3caae-106">Azure Container Registry está en versión preliminar y no está disponible en todas las regiones.</span><span class="sxs-lookup"><span data-stu-id="3caae-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3caae-107">Si decide instalar y usar la CLI localmente, para esta guía de inicio rápido es preciso que ejecute la CLI de Azure versión 2.0.4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="3caae-107">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="3caae-108">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="3caae-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="3caae-109">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3caae-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="3caae-110">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="3caae-110">Create a resource group</span></span>

<span data-ttu-id="3caae-111">Cree un grupo de recursos con el comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="3caae-111">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="3caae-112">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="3caae-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="3caae-113">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroup* en la ubicación *westcentralus*.</span><span class="sxs-lookup"><span data-stu-id="3caae-113">The following example creates a resource group named *myResourceGroup* in the *westcentralus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a><span data-ttu-id="3caae-114">Creación de un registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="3caae-114">Create a container registry</span></span>

<span data-ttu-id="3caae-115">Creación de una instancia de ACR mediante el comando [az acr create](/cli/azure/acr#create).</span><span class="sxs-lookup"><span data-stu-id="3caae-115">Create an ACR instance using the [az acr create](/cli/azure/acr#create) command.</span></span>

> [!NOTE]
> <span data-ttu-id="3caae-116">Cuando cree un registro, especifique un nombre de dominio de nivel superior único global que contenga solo letras y números.</span><span class="sxs-lookup"><span data-stu-id="3caae-116">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span>

 <span data-ttu-id="3caae-117">El nombre del registro en el ejemplo es *myContainerRegistry1*, sustitúyalo por un nombre único de su elección.</span><span class="sxs-lookup"><span data-stu-id="3caae-117">The registry name in the example is *myContainerRegistry1*, substitute a unique name of your own.</span></span>

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

<span data-ttu-id="3caae-118">Cuando se crea el registro, el resultado es similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="3caae-118">When the registry is created, the output is similar to the following:</span></span>

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

## <a name="log-in-to-acr-instance"></a><span data-ttu-id="3caae-119">Inicio de sesión en la instancia de ACR</span><span class="sxs-lookup"><span data-stu-id="3caae-119">Log in to ACR instance</span></span>

<span data-ttu-id="3caae-120">Antes de insertar y extraer imágenes de contenedor, debe iniciar sesión en la instancia de ACR.</span><span class="sxs-lookup"><span data-stu-id="3caae-120">Before pushing and pulling container images, you must log in to the ACR instance.</span></span> <span data-ttu-id="3caae-121">Para ello, utilice el comando [az acr login](/cli/azure/acr#login).</span><span class="sxs-lookup"><span data-stu-id="3caae-121">To do so, use the [az acr login](/cli/azure/acr#login) command.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

<span data-ttu-id="3caae-122">Al finalizar, el comando devuelve un mensaje que indica que el inicio de sesión se ha realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="3caae-122">The command returns a 'Login Succeeded' message once completed.</span></span>

## <a name="use-azure-container-registry"></a><span data-ttu-id="3caae-123">Uso de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="3caae-123">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="3caae-124">Lista de imágenes de contenedor</span><span class="sxs-lookup"><span data-stu-id="3caae-124">List container images</span></span>

<span data-ttu-id="3caae-125">Use los comandos de la CLI `az acr` para consultar las imágenes y etiquetas en un repositorio.</span><span class="sxs-lookup"><span data-stu-id="3caae-125">Use the `az acr` CLI commands to query the images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="3caae-126">Actualmente, Container Registry no admite el comando `docker search` para consultar las imágenes y etiquetas.</span><span class="sxs-lookup"><span data-stu-id="3caae-126">Currently, Container Registry does not support the `docker search` command to query for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="3caae-127">Lista de repositorios</span><span class="sxs-lookup"><span data-stu-id="3caae-127">List repositories</span></span>

<span data-ttu-id="3caae-128">En el ejemplo siguiente se enumeran los repositorios de un registro en formato JSON (notación de objetos JavaScript):</span><span class="sxs-lookup"><span data-stu-id="3caae-128">The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="3caae-129">Lista de etiquetas</span><span class="sxs-lookup"><span data-stu-id="3caae-129">List tags</span></span>

<span data-ttu-id="3caae-130">En el ejemplo siguiente se muestran las etiquetas del repositorio **samples/nginx**, en formato JSON:</span><span class="sxs-lookup"><span data-stu-id="3caae-130">The following example lists the tags on the **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="3caae-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3caae-131">Next steps</span></span>

<span data-ttu-id="3caae-132">En esta guía se ha creado una instancia administrada de Azure Container Registry mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="3caae-132">In this quick start, you've created a managed Azure Container Registry instance using the Azure CLI.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3caae-133">Insertar la primera imagen mediante la CLI de Docker</span><span class="sxs-lookup"><span data-stu-id="3caae-133">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
