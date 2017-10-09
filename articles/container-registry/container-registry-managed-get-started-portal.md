---
title: registro Docker privada aaaCreate - portal de Azure | Documentos de Microsoft
description: Empezar a crear y administrar registros de contenedor de Docker privados con hello portal de Azure
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: cf3ce0dcf3036d0e9cd1eaf01721deccb00248d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-portal"></a><span data-ttu-id="19466-103">Crear un registro de contenedor administrado mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="19466-103">Create a managed container registry using hello Azure portal</span></span>

<span data-ttu-id="19466-104">Azure Container Registry es un servicio de registro de contenedores de Docker administrado usado para almacenar imágenes de contenedor de Docker privadas.</span><span class="sxs-lookup"><span data-stu-id="19466-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="19466-105">Esta guía se detalla la creación de una instancia de registro de contenedor de Azure administrados mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="19466-105">This guide details creating a managed Azure Container Registry instance using hello Azure portal.</span></span>

<span data-ttu-id="19466-106">Azure Container Registry está en versión preliminar y no está disponible en todas las regiones.</span><span class="sxs-lookup"><span data-stu-id="19466-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="19466-107">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="19466-107">Log in tooAzure</span></span>

<span data-ttu-id="19466-108">Inicie sesión en toohello portal de Azure en http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="19466-108">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="19466-109">Creación de un registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="19466-109">Create a container registry</span></span>

1. <span data-ttu-id="19466-110">Haga clic en hello **New** encontró el botón en la esquina izquierda superior de Hola de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="19466-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="19466-111">Busque en marketplace Hola para **registro de contenedor de Azure** y selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="19466-111">Search hello marketplace for **Azure container registry** and select it.</span></span>

3. <span data-ttu-id="19466-112">Haga clic en **crear** que abrirá la hoja de creación de hello ACR.</span><span class="sxs-lookup"><span data-stu-id="19466-112">Click **Create** which will open hello ACR creation blade.</span></span>

    ![Configuración de Container Registry](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. <span data-ttu-id="19466-114">Hola **registro de contenedor de Azure** hoja, escriba Hola siguiente información.</span><span class="sxs-lookup"><span data-stu-id="19466-114">In hello **Azure Container Registry** blade, enter hello following information.</span></span> <span data-ttu-id="19466-115">Cuando haya terminado, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="19466-115">Click **Create** when you are done.</span></span>

    <span data-ttu-id="19466-116">a.</span><span class="sxs-lookup"><span data-stu-id="19466-116">a.</span></span> <span data-ttu-id="19466-117">**Nombre del registro**: un nombre de dominio de nivel superior único global para el registro específico.</span><span class="sxs-lookup"><span data-stu-id="19466-117">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="19466-118">En este ejemplo, es el nombre del registro de hello *myAzureContainerRegistry1*, pero sustituir un nombre único de su elección.</span><span class="sxs-lookup"><span data-stu-id="19466-118">In this example, hello registry name is *myAzureContainerRegistry1*, but substitute a unique name of your own.</span></span> <span data-ttu-id="19466-119">Hola nombre puede contener sólo letras y números.</span><span class="sxs-lookup"><span data-stu-id="19466-119">hello name can contain only letters and numbers.</span></span>

    <span data-ttu-id="19466-120">b.</span><span class="sxs-lookup"><span data-stu-id="19466-120">b.</span></span> <span data-ttu-id="19466-121">**Grupo de recursos**: seleccione una existente [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) o nombre de tipo hello para uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="19466-121">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span>

    <span data-ttu-id="19466-122">c.</span><span class="sxs-lookup"><span data-stu-id="19466-122">c.</span></span> <span data-ttu-id="19466-123">**Ubicación**: seleccione la ubicación de centro de datos Azure donde es el servicio de hello [disponibles](https://azure.microsoft.com/regions/services/), como **Ee.uu. Central sur**.</span><span class="sxs-lookup"><span data-stu-id="19466-123">**Location**: Select an Azure datacenter location where hello service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="19466-124">d.</span><span class="sxs-lookup"><span data-stu-id="19466-124">d.</span></span> <span data-ttu-id="19466-125">**El usuario administrador**: si lo desea, habilitar un registro de hello de tooaccess de usuario de administrador.</span><span class="sxs-lookup"><span data-stu-id="19466-125">**Admin user**: If you want, enable an admin user tooaccess hello registry.</span></span> <span data-ttu-id="19466-126">Puede cambiar esta configuración después de crear el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="19466-126">You can change this setting after creating hello registry.</span></span>

    <span data-ttu-id="19466-127">e.</span><span class="sxs-lookup"><span data-stu-id="19466-127">e.</span></span> <span data-ttu-id="19466-128">**Registro de uso administrado**: seleccione la opción Sí toohave ACR automáticamente administrar el almacenamiento de registro de hello, use webhooks y use autenticación de AAD.</span><span class="sxs-lookup"><span data-stu-id="19466-128">**Use managed registry**: Select yes toohave ACR automatically manage hello registry storage, use webhooks, and use AAD authentication.</span></span>

    <span data-ttu-id="19466-129">f.</span><span class="sxs-lookup"><span data-stu-id="19466-129">f.</span></span> <span data-ttu-id="19466-130">**Plan de tarifa**: seleccione un plan de tarifa, consulte precios de ACR para más información.</span><span class="sxs-lookup"><span data-stu-id="19466-130">**Pricing Tier**: Select a pricing tier, see here ACR pricing for more information.</span></span>

## <a name="log-in-tooacr-instance"></a><span data-ttu-id="19466-131">Inicie sesión en la instancia de tooACR</span><span class="sxs-lookup"><span data-stu-id="19466-131">Log in tooACR instance</span></span>

<span data-ttu-id="19466-132">Antes de insertar y extraer imágenes de contenedor, primero debe iniciar sesión en la instancia ACR toohello.</span><span class="sxs-lookup"><span data-stu-id="19466-132">Before pushing and pulling container images, you must log in toohello ACR instance.</span></span> 

<span data-ttu-id="19466-133">toodo por lo tanto, utilice Hola 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="19466-133">toodo so, use hello Azure CLI 2.0.</span></span> <span data-ttu-id="19466-134">En primer lugar, si es necesario, inicie sesión en Azure con hello [inicio de sesión de az](/cli/azure/#login) comando.</span><span class="sxs-lookup"><span data-stu-id="19466-134">First, if needed, log into Azure using hello [az login](/cli/azure/#login) command.</span></span> 

```azurecli
az login
```

<span data-ttu-id="19466-135">A continuación, usar hello [inicio de sesión de acr az](/cli/azure/acr#login) comando toolog en toohello del registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="19466-135">Next, use hello [az acr login](/cli/azure/acr#login) command toolog in toohello Azure Container Registry.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a><span data-ttu-id="19466-136">Uso de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="19466-136">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="19466-137">Lista de imágenes de contenedor</span><span class="sxs-lookup"><span data-stu-id="19466-137">List container images</span></span>

<span data-ttu-id="19466-138">Hola de uso `az acr` tooquery imágenes de Hola y etiquetas en un repositorio de los comandos de CLI.</span><span class="sxs-lookup"><span data-stu-id="19466-138">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="19466-139">Actualmente, el registro de contenedor no admite hello `docker search` tooquery de comando para imágenes y etiquetas.</span><span class="sxs-lookup"><span data-stu-id="19466-139">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="19466-140">Lista de repositorios</span><span class="sxs-lookup"><span data-stu-id="19466-140">List repositories</span></span>

<span data-ttu-id="19466-141">Hello en el ejemplo siguiente se enumera los repositorios de hello en un registro, en formato JSON (JavaScript Object Notation):</span><span class="sxs-lookup"><span data-stu-id="19466-141">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="19466-142">Lista de etiquetas</span><span class="sxs-lookup"><span data-stu-id="19466-142">List tags</span></span>

<span data-ttu-id="19466-143">Hello en el ejemplo siguiente se muestra etiquetas de hello en hello **ejemplos/nginx** repositorio, en formato JSON:</span><span class="sxs-lookup"><span data-stu-id="19466-143">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="19466-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="19466-144">Next steps</span></span>

<span data-ttu-id="19466-145">En este tutorial, ha creado una instancia administrada de registro de contenedor de Azure con hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="19466-145">In this quick start, you've created a managed Azure Container Registry instance using hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="19466-146">Insertar la primera imagen con hello CLI de Docker</span><span class="sxs-lookup"><span data-stu-id="19466-146">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
