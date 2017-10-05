---
title: "Creación del registro de contenedores privado de Docker: CLI de Azure | Microsoft Docs"
description: "Introducción a la creación y la administración de registros de contenedor privados de Docker mediante la CLI de Azure 2.0"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2875f4089231ed12a0312b2c2e077938440365c6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-private-docker-container-registry-using-the-azure-cli-20"></a><span data-ttu-id="b2c34-103">Creación de un registro de contenedor privado de Docker con la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="b2c34-103">Create a private Docker container registry using the Azure CLI 2.0</span></span>
<span data-ttu-id="b2c34-104">Use los comandos de la [CLI de Azure 2.0](https://github.com/Azure/azure-cli) para crear un registro de contenedor y administrar su configuración desde un equipo Linux, Mac o Windows.</span><span class="sxs-lookup"><span data-stu-id="b2c34-104">Use commands in the [Azure CLI 2.0](https://github.com/Azure/azure-cli) to create a container registry and manage its settings from your Linux, Mac, or Windows computer.</span></span> <span data-ttu-id="b2c34-105">También puede crear y administrar registros de contenedor mediante [Azure Portal](container-registry-get-started-portal.md) o mediante programación con la [API de REST](https://go.microsoft.com/fwlink/p/?linkid=834376) de Container Registry.</span><span class="sxs-lookup"><span data-stu-id="b2c34-105">You can also create and manage container registries using the [Azure portal](container-registry-get-started-portal.md) or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="b2c34-106">Para más información sobre el entorno y los conceptos, consulte [la información general](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="b2c34-106">For background and concepts, see [the overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="b2c34-107">Para obtener ayuda sobre los comandos de la CLI de Container Registry (`az acr` comandos), pase el parámetro `-h` a cualquier comando.</span><span class="sxs-lookup"><span data-stu-id="b2c34-107">For help on Container Registry CLI commands (`az acr` commands), pass the `-h` parameter to any command.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b2c34-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b2c34-108">Prerequisites</span></span>
* <span data-ttu-id="b2c34-109">**CLI de Azure 2.0**: para instalar y empezar a trabajar con la CLI 2.0, consulte las [instrucciones de instalación](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b2c34-109">**Azure CLI 2.0**: To install and get started with the CLI 2.0, see the [installation instructions](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="b2c34-110">Inicie sesión en la suscripción de Azure mediante la ejecución de `az login`.</span><span class="sxs-lookup"><span data-stu-id="b2c34-110">Log in to your Azure subscription by running `az login`.</span></span> <span data-ttu-id="b2c34-111">Para más información, consulte la [introducción a la CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b2c34-111">For more information, see [Get started with the CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="b2c34-112">**Grupo de recursos**: cree un [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) antes de crear un registro de contenedor o utilice un grupo de recursos ya existente.</span><span class="sxs-lookup"><span data-stu-id="b2c34-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="b2c34-113">Asegúrese de que el grupo de recursos está en una ubicación donde el servicio Container Registry está [disponible](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="b2c34-113">Make sure the resource group is in a location where the Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="b2c34-114">Para crear un grupo de recursos con la CLI 2.0, consulte la [referencia de la CLI 2.0](/cli/azure/group).</span><span class="sxs-lookup"><span data-stu-id="b2c34-114">To create a resource group using the CLI 2.0, see [the CLI 2.0 reference](/cli/azure/group).</span></span>
* <span data-ttu-id="b2c34-115">**Cuenta de almacenamiento** (opcional): cree una [cuenta de almacenamiento](../storage/common/storage-introduction.md) estándar de Azure para realizar copias del registro de contenedor en la misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="b2c34-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) to back the container registry in the same location.</span></span> <span data-ttu-id="b2c34-116">Si no especifica una cuenta de almacenamiento al crear un registro con `az acr create`, el comando creará una automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b2c34-116">If you don't specify a storage account when creating a registry with `az acr create`, the command creates one for you.</span></span> <span data-ttu-id="b2c34-117">Para crear una cuenta de almacenamiento con la CLI 2.0, consulte la [referencia de la CLI 2.0](/cli/azure/storage/account).</span><span class="sxs-lookup"><span data-stu-id="b2c34-117">To create a storage account using the CLI 2.0, see [the CLI 2.0 reference](/cli/azure/storage/account).</span></span> <span data-ttu-id="b2c34-118">Premium Storage no se admite actualmente.</span><span class="sxs-lookup"><span data-stu-id="b2c34-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="b2c34-119">**Entidad de servicio** (opcional): cuando crea un registro con la CLI, el acceso a este no está configurado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b2c34-119">**Service principal** (optional): When you create a registry with the CLI, by default it is not set up for access.</span></span> <span data-ttu-id="b2c34-120">Según sus necesidades, puede asignar una entidad de servicio de Azure Active Directory existente a un registro (o crear y asignar una nueva), o habilitar la cuenta de usuario del administrador del registro.</span><span class="sxs-lookup"><span data-stu-id="b2c34-120">Depending on your needs, you can assign an existing Azure Active Directory service principal to a registry (or create and assign a new one), or enable the registry's admin user account.</span></span> <span data-ttu-id="b2c34-121">Consulte las secciones más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="b2c34-121">See the sections later in this article.</span></span> <span data-ttu-id="b2c34-122">Para más información acerca del acceso al registro, consulte [Authenticate with the container registry](container-registry-authentication.md) (Autenticación con el registro de contenedor).</span><span class="sxs-lookup"><span data-stu-id="b2c34-122">For more information about registry access, see [Authenticate with the container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="b2c34-123">Creación de un registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="b2c34-123">Create a container registry</span></span>
<span data-ttu-id="b2c34-124">Ejecute el comando `az acr create` para crear un registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="b2c34-124">Run the `az acr create` command to create a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="b2c34-125">Cuando cree un registro, especifique un nombre de dominio de nivel superior único global que contenga solo letras y números.</span><span class="sxs-lookup"><span data-stu-id="b2c34-125">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="b2c34-126">El nombre del registro en los ejemplos es `myRegistry1`, pero puede sustituirlo por un nombre único de su elección.</span><span class="sxs-lookup"><span data-stu-id="b2c34-126">The registry name in the examples is `myRegistry1`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="b2c34-127">El siguiente comando utiliza los parámetros mínimos necesarios para crear el registro de contenedor `myRegistry1` en el grupo de recursos `myResourceGroup` y en la SKU *Basic*:</span><span class="sxs-lookup"><span data-stu-id="b2c34-127">The following command uses the minimal parameters to create container registry `myRegistry1` in the resource group `myResourceGroup`, and using the *Basic* sku:</span></span>

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* <span data-ttu-id="b2c34-128">`--storage-account-name` es opcional.</span><span class="sxs-lookup"><span data-stu-id="b2c34-128">`--storage-account-name` is optional.</span></span> <span data-ttu-id="b2c34-129">Si no se especifica, se crea una cuenta de almacenamiento con un nombre formado por el nombre del registro y una marca de tiempo del grupo de recursos especificado.</span><span class="sxs-lookup"><span data-stu-id="b2c34-129">If not specified, a storage account is created with a name consisting of the registry name and a timestamp in the specified resource group.</span></span>

<span data-ttu-id="b2c34-130">Cuando se crea el registro, el resultado es similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="b2c34-130">When the registry is created, the output is similar to the following:</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


<span data-ttu-id="b2c34-131">Tenga en cuenta especialmente:</span><span class="sxs-lookup"><span data-stu-id="b2c34-131">Take special note:</span></span>

* <span data-ttu-id="b2c34-132">`id`: el identificador del registro en la suscripción, que necesitará si desea asignar una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="b2c34-132">`id` - Identifier for the registry in your subscription, which you need if you want to assign a service principal.</span></span>
* <span data-ttu-id="b2c34-133">`loginServer`: el nombre completo que especifique para [iniciar sesión en el registro](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b2c34-133">`loginServer` - The fully qualified name you specify to [log in to the registry](container-registry-authentication.md).</span></span> <span data-ttu-id="b2c34-134">En este ejemplo, el nombre es `myregistry1.exp.azurecr.io` (todo en minúsculas).</span><span class="sxs-lookup"><span data-stu-id="b2c34-134">In this example, the name is `myregistry1.exp.azurecr.io` (all lowercase).</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="b2c34-135">Asignación de una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="b2c34-135">Assign a service principal</span></span>
<span data-ttu-id="b2c34-136">Use los comandos de la CLI 2.0 para asignar una entidad de servicio de Azure Active Directory a un registro.</span><span class="sxs-lookup"><span data-stu-id="b2c34-136">Use CLI 2.0 commands to assign an Azure Active Directory service principal to a registry.</span></span> <span data-ttu-id="b2c34-137">A la entidad de servicio en estos ejemplos se le asigna el rol de propietario, pero puede asignar [otros roles](../active-directory/role-based-access-control-configure.md) si lo desea.</span><span class="sxs-lookup"><span data-stu-id="b2c34-137">The service principal in these examples is assigned the Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal-and-assign-access-to-the-registry"></a><span data-ttu-id="b2c34-138">Creación de una entidad de servicio y asignación de acceso al registro</span><span class="sxs-lookup"><span data-stu-id="b2c34-138">Create a service principal and assign access to the registry</span></span>
<span data-ttu-id="b2c34-139">En el siguiente comando, se le asigna a una nueva entidad de servicio un acceso de rol de propietario para el identificador del registro pasado con el parámetro `--scopes`.</span><span class="sxs-lookup"><span data-stu-id="b2c34-139">In the following command, a new service principal is assigned Owner role access to the registry identifier passed with the `--scopes` parameter.</span></span> <span data-ttu-id="b2c34-140">Especifique una contraseña segura con el parámetro `--password`.</span><span class="sxs-lookup"><span data-stu-id="b2c34-140">Specify a strong password with the `--password` parameter.</span></span>

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a><span data-ttu-id="b2c34-141">Asignación de una entidad de servicio existente</span><span class="sxs-lookup"><span data-stu-id="b2c34-141">Assign an existing service principal</span></span>
<span data-ttu-id="b2c34-142">Si ya tiene una entidad de servicio y desea asignar a esta un acceso de rol de propietario al registro, ejecute un comando similar al del ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="b2c34-142">If you already have a service principal and want to assign it Owner role access to the registry, run a command similar to the following example.</span></span> <span data-ttu-id="b2c34-143">Pase el identificador de la aplicación de la entidad de servicio mediante el parámetro `--assignee`:</span><span class="sxs-lookup"><span data-stu-id="b2c34-143">You pass the service principal app ID using the `--assignee` parameter:</span></span>

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a><span data-ttu-id="b2c34-144">Administración de las credenciales de administrador</span><span class="sxs-lookup"><span data-stu-id="b2c34-144">Manage admin credentials</span></span>
<span data-ttu-id="b2c34-145">Se crea automáticamente una cuenta de administrador para cada registro de contenedor, que estará deshabilitada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b2c34-145">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="b2c34-146">Los ejemplos siguientes muestran los comandos de la CLI `az acr` para administrar las credenciales de administrador del registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="b2c34-146">The following examples show `az acr` CLI commands to manage the admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="b2c34-147">Obtención de las credenciales de administrador</span><span class="sxs-lookup"><span data-stu-id="b2c34-147">Obtain admin user credentials</span></span>
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="b2c34-148">Habilitación del usuario de administrador para un registro existente</span><span class="sxs-lookup"><span data-stu-id="b2c34-148">Enable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="b2c34-149">Deshabilitación del usuario de administrador para un registro existente</span><span class="sxs-lookup"><span data-stu-id="b2c34-149">Disable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a><span data-ttu-id="b2c34-150">Lista de las imágenes y etiquetas</span><span class="sxs-lookup"><span data-stu-id="b2c34-150">List images and tags</span></span>
<span data-ttu-id="b2c34-151">Use los comandos de la CLI `az acr` para consultar las imágenes y etiquetas en un repositorio.</span><span class="sxs-lookup"><span data-stu-id="b2c34-151">Use the `az acr` CLI commands to query the images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="b2c34-152">Actualmente, Container Registry no admite el comando `docker search` para consultar las imágenes y etiquetas.</span><span class="sxs-lookup"><span data-stu-id="b2c34-152">Currently, Container Registry does not support the `docker search` command to query for images and tags.</span></span>


### <a name="list-repositories"></a><span data-ttu-id="b2c34-153">Lista de repositorios</span><span class="sxs-lookup"><span data-stu-id="b2c34-153">List repositories</span></span>
<span data-ttu-id="b2c34-154">En el ejemplo siguiente se enumeran los repositorios de un registro en formato JSON (notación de objetos JavaScript):</span><span class="sxs-lookup"><span data-stu-id="b2c34-154">The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="b2c34-155">Lista de etiquetas</span><span class="sxs-lookup"><span data-stu-id="b2c34-155">List tags</span></span>
<span data-ttu-id="b2c34-156">En el ejemplo siguiente se muestran las etiquetas del repositorio **samples/nginx**, en formato JSON:</span><span class="sxs-lookup"><span data-stu-id="b2c34-156">The following example lists the tags on the **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="b2c34-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b2c34-157">Next steps</span></span>
* [<span data-ttu-id="b2c34-158">Insertar la primera imagen mediante la CLI de Docker</span><span class="sxs-lookup"><span data-stu-id="b2c34-158">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
