---
title: Repositorios de Azure Container Registry | Microsoft Docs
description: "Uso de los repositorios de Azure Container Registry para imágenes de Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: cristyg
ms.openlocfilehash: 1e5d5ea5b1ec121fe008abc48178b1d58f540ce1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-private-docker-container-registry-using-the-azure-powershell"></a><span data-ttu-id="bca3a-103">Creación de un registro de contenedor privado de Docker con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bca3a-103">Create a private Docker container registry using the Azure PowerShell</span></span>
<span data-ttu-id="bca3a-104">Use los comandos de la [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) para crear un registro de contenedor y administrar su configuración desde un equipo Windows.</span><span class="sxs-lookup"><span data-stu-id="bca3a-104">Use commands in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) to create a container registry and manage its settings from your Windows computer.</span></span> <span data-ttu-id="bca3a-105">También puede crear y administrar registros de contenedor mediante [Azure Portal](container-registry-get-started-portal.md), la [CLI de Azure](container-registry-get-started-azure-cli.md) o mediante programación con la [API de REST](https://go.microsoft.com/fwlink/p/?linkid=834376) de Container Registry.</span><span class="sxs-lookup"><span data-stu-id="bca3a-105">You can also create and manage container registries using the [Azure portal](container-registry-get-started-portal.md), the [Azure CLI](container-registry-get-started-azure-cli.md), or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="bca3a-106">Para más información sobre el entorno y los conceptos, consulte [la información general](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="bca3a-106">For background and concepts, see [the overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="bca3a-107">Para una lista de los cmdlets compatibles, consulte el artículo sobre los [Cmdlets de administración de Azure Container Registry](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span><span class="sxs-lookup"><span data-stu-id="bca3a-107">For a full list of supported cmdlets, see [Azure Container Registry Management Cmdlets](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="bca3a-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bca3a-108">Prerequisites</span></span>
* <span data-ttu-id="bca3a-109">**Azure PowerShell**: para instalar y empezar a trabajar con PowerShell, consulte las [instrucciones de instalación](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="bca3a-109">**Azure PowerShell**: To install and get started with Azure PowerShell, see the [installation instructions](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="bca3a-110">Inicie sesión en la suscripción de Azure mediante la ejecución de `Login-AzureRMAccount`.</span><span class="sxs-lookup"><span data-stu-id="bca3a-110">Log in to your Azure subscription by running `Login-AzureRMAccount`.</span></span> <span data-ttu-id="bca3a-111">Para más información, consulte el artículo de [introducción a Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span><span class="sxs-lookup"><span data-stu-id="bca3a-111">For more information, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span></span>
* <span data-ttu-id="bca3a-112">**Grupo de recursos**: cree un [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) antes de crear un registro de contenedor o utilice un grupo de recursos ya existente.</span><span class="sxs-lookup"><span data-stu-id="bca3a-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="bca3a-113">Asegúrese de que el grupo de recursos está en una ubicación donde el servicio Container Registry está [disponible](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="bca3a-113">Make sure the resource group is in a location where the Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="bca3a-114">Para crear un grupo de recursos mediante Azure PowerShell, consulte la [referencia de PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span><span class="sxs-lookup"><span data-stu-id="bca3a-114">To create a resource group using Azure PowerShell, see [the PowerShell reference](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span></span>
* <span data-ttu-id="bca3a-115">**Cuenta de almacenamiento** (opcional): cree una [cuenta de almacenamiento](../storage/common/storage-introduction.md) estándar de Azure para realizar copias del registro de contenedor en la misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="bca3a-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) to back the container registry in the same location.</span></span> <span data-ttu-id="bca3a-116">Si no especifica una cuenta de almacenamiento al crear un registro con `New-AzureRMContainerRegistry`, el comando creará una automáticamente.</span><span class="sxs-lookup"><span data-stu-id="bca3a-116">If you don't specify a storage account when creating a registry with `New-AzureRMContainerRegistry`, the command creates one for you.</span></span> <span data-ttu-id="bca3a-117">Para crear una cuenta de almacenamiento mediante PowerShell, consulte la [referencia de PowerShell](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span><span class="sxs-lookup"><span data-stu-id="bca3a-117">To create a storage account using PowerShell, see [the PowerShell reference](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span></span> <span data-ttu-id="bca3a-118">Premium Storage no se admite actualmente.</span><span class="sxs-lookup"><span data-stu-id="bca3a-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="bca3a-119">**Entidad de servicio** (opcional): cuando crea un registro con PowerShell, el acceso a este no está configurado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="bca3a-119">**Service principal** (optional): When you create a registry with PowerShell, by default it is not set up for access.</span></span> <span data-ttu-id="bca3a-120">Según sus necesidades, puede asignar una entidad de servicio de Azure Active Directory existente a un registro o crear y asignar una nueva.</span><span class="sxs-lookup"><span data-stu-id="bca3a-120">Depending on your needs, you can assign an existing Azure Active Directory service principal to a registry or create and assign a new one.</span></span> <span data-ttu-id="bca3a-121">Como alternativa, puede habilitar la cuenta de usuario de administrador del registro.</span><span class="sxs-lookup"><span data-stu-id="bca3a-121">Alternatively, you can enable the registry's admin user account.</span></span> <span data-ttu-id="bca3a-122">Consulte las secciones más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="bca3a-122">See the sections later in this article.</span></span> <span data-ttu-id="bca3a-123">Para más información acerca del acceso al registro, consulte [Authenticate with the container registry](container-registry-authentication.md) (Autenticación con el registro de contenedor).</span><span class="sxs-lookup"><span data-stu-id="bca3a-123">For more information about registry access, see [Authenticate with the container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="bca3a-124">Creación de un registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="bca3a-124">Create a container registry</span></span>
<span data-ttu-id="bca3a-125">Ejecute el comando `New-AzureRMContainerRegistry` para crear un registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="bca3a-125">Run the `New-AzureRMContainerRegistry` command to create a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="bca3a-126">Cuando cree un registro, especifique un nombre de dominio de nivel superior único global que contenga solo letras y números.</span><span class="sxs-lookup"><span data-stu-id="bca3a-126">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="bca3a-127">El nombre del registro en los ejemplos es `MyRegistry`, pero puede sustituirlo por un nombre único de su elección.</span><span class="sxs-lookup"><span data-stu-id="bca3a-127">The registry name in the examples is `MyRegistry`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="bca3a-128">El siguiente comando utiliza los parámetros mínimos necesarios para crear el registro de contenedor `MyRegistry` en el grupo de recursos `MyResourceGroup` en la ubicación centro-sur de EE. UU.:</span><span class="sxs-lookup"><span data-stu-id="bca3a-128">The following command uses the minimal parameters to create container registry `MyRegistry` in the resource group `MyResourceGroup` in the South Central US location:</span></span>

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* <span data-ttu-id="bca3a-129">`-StorageAccountName` es opcional.</span><span class="sxs-lookup"><span data-stu-id="bca3a-129">`-StorageAccountName` is optional.</span></span> <span data-ttu-id="bca3a-130">Si no se especifica, se crea una cuenta de almacenamiento con un nombre formado por el nombre del registro y una marca de tiempo del grupo de recursos especificado.</span><span class="sxs-lookup"><span data-stu-id="bca3a-130">If not specified, a storage account is created with a name consisting of the registry name and a timestamp in the specified resource group.</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="bca3a-131">Asignación de una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="bca3a-131">Assign a service principal</span></span>
<span data-ttu-id="bca3a-132">Use los comandos de PowerShell para asignar una [entidad de servicio](../azure-resource-manager/resource-group-authenticate-service-principal.md) de Azure Active Directory a un registro.</span><span class="sxs-lookup"><span data-stu-id="bca3a-132">Use PowerShell commands to assign an Azure Active Directory [service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) to a registry.</span></span> <span data-ttu-id="bca3a-133">A la entidad de servicio en estos ejemplos se le asigna el rol de propietario, pero puede asignar [otros roles](../active-directory/role-based-access-control-configure.md) si lo desea.</span><span class="sxs-lookup"><span data-stu-id="bca3a-133">The service principal in these examples is assigned the Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal"></a><span data-ttu-id="bca3a-134">Creación de una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="bca3a-134">Create a service principal</span></span>
<span data-ttu-id="bca3a-135">En el siguiente comando se crea una nueva entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="bca3a-135">In the following command, a new service principal is created.</span></span> <span data-ttu-id="bca3a-136">Especifique una contraseña segura con el parámetro `-Password`.</span><span class="sxs-lookup"><span data-stu-id="bca3a-136">Specify a strong password with the `-Password` parameter.</span></span>

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a><span data-ttu-id="bca3a-137">Asignación de una entidad de servicio nueva o existente</span><span class="sxs-lookup"><span data-stu-id="bca3a-137">Assign a new or existing service principal</span></span>
<span data-ttu-id="bca3a-138">A un registro puede asignar una entidad de servicio nueva o existente.</span><span class="sxs-lookup"><span data-stu-id="bca3a-138">You can assign a new or an existing service principal to a registry.</span></span> <span data-ttu-id="bca3a-139">Para asignarle acceso de rol de propietario al registro, ejecute un comando similar al del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="bca3a-139">To assign it Owner role access to the registry, run a command similar to the following example:</span></span>

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-to-the-registry-with-the-service-principal"></a><span data-ttu-id="bca3a-140">Inicie sesión en el registro con la entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="bca3a-140">Sign in to the registry with the service principal</span></span>
<span data-ttu-id="bca3a-141">Después de asignar la entidad de servicio al registro, puede iniciar sesión con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="bca3a-141">After assigning the service principal to the registry, you can sign in using the following command:</span></span>

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a><span data-ttu-id="bca3a-142">Administración de las credenciales de administrador</span><span class="sxs-lookup"><span data-stu-id="bca3a-142">Manage admin credentials</span></span>
<span data-ttu-id="bca3a-143">Se crea automáticamente una cuenta de administrador para cada registro de contenedor, que estará deshabilitada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="bca3a-143">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="bca3a-144">Los ejemplos siguientes muestran los comandos de PowerShell para administrar las credenciales de administrador del registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="bca3a-144">The following examples show PowerShell commands to manage the admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="bca3a-145">Obtención de las credenciales de administrador</span><span class="sxs-lookup"><span data-stu-id="bca3a-145">Obtain admin user credentials</span></span>
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="bca3a-146">Habilitación del usuario de administrador para un registro existente</span><span class="sxs-lookup"><span data-stu-id="bca3a-146">Enable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="bca3a-147">Deshabilitación del usuario de administrador para un registro existente</span><span class="sxs-lookup"><span data-stu-id="bca3a-147">Disable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a><span data-ttu-id="bca3a-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bca3a-148">Next steps</span></span>
* [<span data-ttu-id="bca3a-149">Insertar la primera imagen mediante la CLI de Docker</span><span class="sxs-lookup"><span data-stu-id="bca3a-149">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
