---
title: registro de contenedor de Docker privada de aaaCreate - CLI de Azure | Documentos de Microsoft
description: Empezar a crear y administrar registros de contenedor de Docker privados con hello 2.0 de CLI de Azure
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
ms.openlocfilehash: f0d876a70b71a5e1bd564fbc9198f693dfe8a347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-cli-20"></a><span data-ttu-id="6ef19-103">Crear un registro de contenedor de Docker privado mediante Hola 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="6ef19-103">Create a private Docker container registry using hello Azure CLI 2.0</span></span>
<span data-ttu-id="6ef19-104">Usar comandos en hello [CLI de Azure 2.0](https://github.com/Azure/azure-cli) toocreate un registro de contenedor y administrar su configuración desde un equipo Linux, Mac o Windows.</span><span class="sxs-lookup"><span data-stu-id="6ef19-104">Use commands in hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate a container registry and manage its settings from your Linux, Mac, or Windows computer.</span></span> <span data-ttu-id="6ef19-105">También puede crear y administrar registros de contenedor con hello [portal de Azure](container-registry-get-started-portal.md) o mediante programación con registro de contenedor de hello [API de REST](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="6ef19-105">You can also create and manage container registries using hello [Azure portal](container-registry-get-started-portal.md) or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="6ef19-106">En el fondo y conceptos, vea [Hola información general](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="6ef19-106">For background and concepts, see [hello overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="6ef19-107">Para obtener ayuda sobre los comandos de CLI de contenedor del registro (`az acr` comandos), pasar hello `-h` comando tooany de parámetro.</span><span class="sxs-lookup"><span data-stu-id="6ef19-107">For help on Container Registry CLI commands (`az acr` commands), pass hello `-h` parameter tooany command.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="6ef19-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6ef19-108">Prerequisites</span></span>
* <span data-ttu-id="6ef19-109">**Azure 2.0 CLI**: tooinstall y empezar a trabajar con hello 2.0 de CLI, consulte hello [las instrucciones de instalación](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6ef19-109">**Azure CLI 2.0**: tooinstall and get started with hello CLI 2.0, see hello [installation instructions](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="6ef19-110">Inicie sesión en tooyour suscripción de Azure ejecutando `az login`.</span><span class="sxs-lookup"><span data-stu-id="6ef19-110">Log in tooyour Azure subscription by running `az login`.</span></span> <span data-ttu-id="6ef19-111">Para obtener más información, consulte [empezar a trabajar con hello CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6ef19-111">For more information, see [Get started with hello CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="6ef19-112">**Grupo de recursos**: cree un [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) antes de crear un registro de contenedor o utilice un grupo de recursos ya existente.</span><span class="sxs-lookup"><span data-stu-id="6ef19-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="6ef19-113">Asegúrese de que el grupo de recursos de hello está en una ubicación donde hello servicio de registro de contenedor es [disponibles](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="6ef19-113">Make sure hello resource group is in a location where hello Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="6ef19-114">toocreate un grupo de recursos con Hola 2.0 de CLI, consulte [Hola referencia CLI 2.0](/cli/azure/group).</span><span class="sxs-lookup"><span data-stu-id="6ef19-114">toocreate a resource group using hello CLI 2.0, see [hello CLI 2.0 reference](/cli/azure/group).</span></span>
* <span data-ttu-id="6ef19-115">**Cuenta de almacenamiento** (opcional): crear un estándar Azure [cuenta de almacenamiento](../storage/common/storage-introduction.md) tooback registro de contenedor de Hola Hola misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="6ef19-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) tooback hello container registry in hello same location.</span></span> <span data-ttu-id="6ef19-116">Si no especifica una cuenta de almacenamiento al crear un registro con `az acr create`, comando hello crea uno automáticamente.</span><span class="sxs-lookup"><span data-stu-id="6ef19-116">If you don't specify a storage account when creating a registry with `az acr create`, hello command creates one for you.</span></span> <span data-ttu-id="6ef19-117">toocreate cuenta de almacenamiento mediante Hola 2.0 de CLI, consulte [Hola referencia CLI 2.0](/cli/azure/storage/account).</span><span class="sxs-lookup"><span data-stu-id="6ef19-117">toocreate a storage account using hello CLI 2.0, see [hello CLI 2.0 reference](/cli/azure/storage/account).</span></span> <span data-ttu-id="6ef19-118">Premium Storage no se admite actualmente.</span><span class="sxs-lookup"><span data-stu-id="6ef19-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="6ef19-119">**Entidad de servicio** (opcional): cuando se crea un registro con hello CLI, de forma predeterminada no está configurado para el acceso.</span><span class="sxs-lookup"><span data-stu-id="6ef19-119">**Service principal** (optional): When you create a registry with hello CLI, by default it is not set up for access.</span></span> <span data-ttu-id="6ef19-120">Según sus necesidades, puede asignar un registro de tooa principal de servicio de Azure Active Directory existente (o crear y asignar una nueva), o habilitar la cuenta de usuario de administrador del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="6ef19-120">Depending on your needs, you can assign an existing Azure Active Directory service principal tooa registry (or create and assign a new one), or enable hello registry's admin user account.</span></span> <span data-ttu-id="6ef19-121">Vea las secciones de hello más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="6ef19-121">See hello sections later in this article.</span></span> <span data-ttu-id="6ef19-122">Para obtener más información acerca del acceso del registro, consulte [autenticar con registro de contenedor de hello](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="6ef19-122">For more information about registry access, see [Authenticate with hello container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="6ef19-123">Creación de un registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="6ef19-123">Create a container registry</span></span>
<span data-ttu-id="6ef19-124">Ejecute hello `az acr create` comando toocreate un registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="6ef19-124">Run hello `az acr create` command toocreate a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="6ef19-125">Cuando cree un registro, especifique un nombre de dominio de nivel superior único global que contenga solo letras y números.</span><span class="sxs-lookup"><span data-stu-id="6ef19-125">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="6ef19-126">nombre del registro de Hello en los ejemplos de hello `myRegistry1`, pero sustituir un nombre único de su elección.</span><span class="sxs-lookup"><span data-stu-id="6ef19-126">hello registry name in hello examples is `myRegistry1`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="6ef19-127">Hola el siguiente comando utiliza Hola del registro de contenedor de parámetros mínimos toocreate `myRegistry1` en grupo de recursos de hello `myResourceGroup`y el uso de hello *básica* sku:</span><span class="sxs-lookup"><span data-stu-id="6ef19-127">hello following command uses hello minimal parameters toocreate container registry `myRegistry1` in hello resource group `myResourceGroup`, and using hello *Basic* sku:</span></span>

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* <span data-ttu-id="6ef19-128">`--storage-account-name` es opcional.</span><span class="sxs-lookup"><span data-stu-id="6ef19-128">`--storage-account-name` is optional.</span></span> <span data-ttu-id="6ef19-129">Si no se especifica, se crea una cuenta de almacenamiento con un nombre que consta del nombre del registro de hello y una marca de tiempo en hello especifica el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6ef19-129">If not specified, a storage account is created with a name consisting of hello registry name and a timestamp in hello specified resource group.</span></span>

<span data-ttu-id="6ef19-130">Cuando se crea el registro de hello, salida de hello es siguiente de toohello similar:</span><span class="sxs-lookup"><span data-stu-id="6ef19-130">When hello registry is created, hello output is similar toohello following:</span></span>

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


<span data-ttu-id="6ef19-131">Tenga en cuenta especialmente:</span><span class="sxs-lookup"><span data-stu-id="6ef19-131">Take special note:</span></span>

* <span data-ttu-id="6ef19-132">`id`-Identificador de registro de hello en su suscripción, que es necesario si desea tooassign una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="6ef19-132">`id` - Identifier for hello registry in your subscription, which you need if you want tooassign a service principal.</span></span>
* <span data-ttu-id="6ef19-133">`loginServer`-nombre completo de Hola que especifique demasiado[inicie sesión en el registro de toohello](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="6ef19-133">`loginServer` - hello fully qualified name you specify too[log in toohello registry](container-registry-authentication.md).</span></span> <span data-ttu-id="6ef19-134">En este ejemplo, se denomina hello `myregistry1.exp.azurecr.io` (en minúsculas).</span><span class="sxs-lookup"><span data-stu-id="6ef19-134">In this example, hello name is `myregistry1.exp.azurecr.io` (all lowercase).</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="6ef19-135">Asignación de una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="6ef19-135">Assign a service principal</span></span>
<span data-ttu-id="6ef19-136">Usar comandos de CLI 2.0 tooassign un registro de tooa principal de servicio de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6ef19-136">Use CLI 2.0 commands tooassign an Azure Active Directory service principal tooa registry.</span></span> <span data-ttu-id="6ef19-137">Hello entidad de servicio en estos ejemplos se asigna el rol de propietario de hello, pero puede asignar [otros roles](../active-directory/role-based-access-control-configure.md) si desea.</span><span class="sxs-lookup"><span data-stu-id="6ef19-137">hello service principal in these examples is assigned hello Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal-and-assign-access-toohello-registry"></a><span data-ttu-id="6ef19-138">Crear a una entidad de servicio y asignar del registro de acceso toohello</span><span class="sxs-lookup"><span data-stu-id="6ef19-138">Create a service principal and assign access toohello registry</span></span>
<span data-ttu-id="6ef19-139">En el siguiente comando de hello, una nueva entidad de servicio se asigna identificador Propietario rol acceso toohello del registro se ha superado con hello `--scopes` parámetro.</span><span class="sxs-lookup"><span data-stu-id="6ef19-139">In hello following command, a new service principal is assigned Owner role access toohello registry identifier passed with hello `--scopes` parameter.</span></span> <span data-ttu-id="6ef19-140">Especifique una contraseña segura con hello `--password` parámetro.</span><span class="sxs-lookup"><span data-stu-id="6ef19-140">Specify a strong password with hello `--password` parameter.</span></span>

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a><span data-ttu-id="6ef19-141">Asignación de una entidad de servicio existente</span><span class="sxs-lookup"><span data-stu-id="6ef19-141">Assign an existing service principal</span></span>
<span data-ttu-id="6ef19-142">Si ya tiene una entidad de servicio y desea tooassign el registro de toohello de propietario rol acceso, que se ejecute un toohello similar de comando siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="6ef19-142">If you already have a service principal and want tooassign it Owner role access toohello registry, run a command similar toohello following example.</span></span> <span data-ttu-id="6ef19-143">Pasar el identificador de la aplicación principal de servicio hello mediante hello `--assignee` parámetro:</span><span class="sxs-lookup"><span data-stu-id="6ef19-143">You pass hello service principal app ID using hello `--assignee` parameter:</span></span>

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a><span data-ttu-id="6ef19-144">Administración de las credenciales de administrador</span><span class="sxs-lookup"><span data-stu-id="6ef19-144">Manage admin credentials</span></span>
<span data-ttu-id="6ef19-145">Se crea automáticamente una cuenta de administrador para cada registro de contenedor, que estará deshabilitada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6ef19-145">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="6ef19-146">Hola siguientes ejemplos se muestra `az acr` toomanage credenciales de administrador de hello para el registro de contenedor de comandos de CLI.</span><span class="sxs-lookup"><span data-stu-id="6ef19-146">hello following examples show `az acr` CLI commands toomanage hello admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="6ef19-147">Obtención de las credenciales de administrador</span><span class="sxs-lookup"><span data-stu-id="6ef19-147">Obtain admin user credentials</span></span>
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="6ef19-148">Habilitación del usuario de administrador para un registro existente</span><span class="sxs-lookup"><span data-stu-id="6ef19-148">Enable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="6ef19-149">Deshabilitación del usuario de administrador para un registro existente</span><span class="sxs-lookup"><span data-stu-id="6ef19-149">Disable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a><span data-ttu-id="6ef19-150">Lista de las imágenes y etiquetas</span><span class="sxs-lookup"><span data-stu-id="6ef19-150">List images and tags</span></span>
<span data-ttu-id="6ef19-151">Hola de uso `az acr` tooquery imágenes de Hola y etiquetas en un repositorio de los comandos de CLI.</span><span class="sxs-lookup"><span data-stu-id="6ef19-151">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="6ef19-152">Actualmente, el registro de contenedor no admite hello `docker search` tooquery de comando para imágenes y etiquetas.</span><span class="sxs-lookup"><span data-stu-id="6ef19-152">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>


### <a name="list-repositories"></a><span data-ttu-id="6ef19-153">Lista de repositorios</span><span class="sxs-lookup"><span data-stu-id="6ef19-153">List repositories</span></span>
<span data-ttu-id="6ef19-154">Hello en el ejemplo siguiente se enumera los repositorios de hello en un registro, en formato JSON (JavaScript Object Notation):</span><span class="sxs-lookup"><span data-stu-id="6ef19-154">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="6ef19-155">Lista de etiquetas</span><span class="sxs-lookup"><span data-stu-id="6ef19-155">List tags</span></span>
<span data-ttu-id="6ef19-156">Hello en el ejemplo siguiente se muestra etiquetas de hello en hello **ejemplos/nginx** repositorio, en formato JSON:</span><span class="sxs-lookup"><span data-stu-id="6ef19-156">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="6ef19-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6ef19-157">Next steps</span></span>
* [<span data-ttu-id="6ef19-158">Insertar la primera imagen con hello CLI de Docker</span><span class="sxs-lookup"><span data-stu-id="6ef19-158">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
