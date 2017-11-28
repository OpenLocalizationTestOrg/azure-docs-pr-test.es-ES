---
title: repositorios de registro del contenedor de aaaAzure | Documentos de Microsoft
description: "¿Cómo toouse repositorios de registro de contenedor de Azure para las imágenes de Docker"
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
ms.openlocfilehash: 448fb812f537c9502041ce5fb372b0681a9dac4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-powershell"></a><span data-ttu-id="fb673-103">Crear un registro de contenedor de Docker privado mediante hello Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb673-103">Create a private Docker container registry using hello Azure PowerShell</span></span>
<span data-ttu-id="fb673-104">Usar comandos de [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate un registro de contenedor y administrar su configuración desde el equipo de Windows.</span><span class="sxs-lookup"><span data-stu-id="fb673-104">Use commands in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate a container registry and manage its settings from your Windows computer.</span></span> <span data-ttu-id="fb673-105">También puede crear y administrar registros de contenedor con hello [portal de Azure](container-registry-get-started-portal.md), hello [CLI de Azure](container-registry-get-started-azure-cli.md), o mediante programación con registro de contenedor de hello [API de REST](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="fb673-105">You can also create and manage container registries using hello [Azure portal](container-registry-get-started-portal.md), hello [Azure CLI](container-registry-get-started-azure-cli.md), or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="fb673-106">En el fondo y conceptos, vea [Hola información general](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="fb673-106">For background and concepts, see [hello overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="fb673-107">Para una lista de los cmdlets compatibles, consulte el artículo sobre los [Cmdlets de administración de Azure Container Registry](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span><span class="sxs-lookup"><span data-stu-id="fb673-107">For a full list of supported cmdlets, see [Azure Container Registry Management Cmdlets](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="fb673-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fb673-108">Prerequisites</span></span>
* <span data-ttu-id="fb673-109">**Azure PowerShell**: tooinstall y empezar a trabajar con Azure PowerShell, vea hello [las instrucciones de instalación](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="fb673-109">**Azure PowerShell**: tooinstall and get started with Azure PowerShell, see hello [installation instructions](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="fb673-110">Inicie sesión en tooyour suscripción de Azure ejecutando `Login-AzureRMAccount`.</span><span class="sxs-lookup"><span data-stu-id="fb673-110">Log in tooyour Azure subscription by running `Login-AzureRMAccount`.</span></span> <span data-ttu-id="fb673-111">Para más información, consulte el artículo de [introducción a Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span><span class="sxs-lookup"><span data-stu-id="fb673-111">For more information, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span></span>
* <span data-ttu-id="fb673-112">**Grupo de recursos**: cree un [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) antes de crear un registro de contenedor o utilice un grupo de recursos ya existente.</span><span class="sxs-lookup"><span data-stu-id="fb673-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="fb673-113">Asegúrese de que el grupo de recursos de hello está en una ubicación donde hello servicio de registro de contenedor es [disponibles](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="fb673-113">Make sure hello resource group is in a location where hello Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="fb673-114">toocreate un grupo de recursos con PowerShell de Azure, consulte [Hola referencia de PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span><span class="sxs-lookup"><span data-stu-id="fb673-114">toocreate a resource group using Azure PowerShell, see [hello PowerShell reference](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span></span>
* <span data-ttu-id="fb673-115">**Cuenta de almacenamiento** (opcional): crear un estándar Azure [cuenta de almacenamiento](../storage/common/storage-introduction.md) tooback registro de contenedor de Hola Hola misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="fb673-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) tooback hello container registry in hello same location.</span></span> <span data-ttu-id="fb673-116">Si no especifica una cuenta de almacenamiento al crear un registro con `New-AzureRMContainerRegistry`, comando hello crea uno automáticamente.</span><span class="sxs-lookup"><span data-stu-id="fb673-116">If you don't specify a storage account when creating a registry with `New-AzureRMContainerRegistry`, hello command creates one for you.</span></span> <span data-ttu-id="fb673-117">toocreate un almacenamiento de la cuenta con PowerShell, vea [Hola referencia de PowerShell](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span><span class="sxs-lookup"><span data-stu-id="fb673-117">toocreate a storage account using PowerShell, see [hello PowerShell reference](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span></span> <span data-ttu-id="fb673-118">Premium Storage no se admite actualmente.</span><span class="sxs-lookup"><span data-stu-id="fb673-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="fb673-119">**Entidad de servicio** (opcional): cuando crea un registro con PowerShell, el acceso a este no está configurado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="fb673-119">**Service principal** (optional): When you create a registry with PowerShell, by default it is not set up for access.</span></span> <span data-ttu-id="fb673-120">Según sus necesidades, puede asignar un registro de tooa principal de servicio de Azure Active Directory existente o crear y asignar una nueva.</span><span class="sxs-lookup"><span data-stu-id="fb673-120">Depending on your needs, you can assign an existing Azure Active Directory service principal tooa registry or create and assign a new one.</span></span> <span data-ttu-id="fb673-121">Como alternativa, puede habilitar la cuenta de usuario de administrador del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="fb673-121">Alternatively, you can enable hello registry's admin user account.</span></span> <span data-ttu-id="fb673-122">Vea las secciones de hello más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="fb673-122">See hello sections later in this article.</span></span> <span data-ttu-id="fb673-123">Para obtener más información acerca del acceso del registro, consulte [autenticar con registro de contenedor de hello](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fb673-123">For more information about registry access, see [Authenticate with hello container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="fb673-124">Creación de un registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="fb673-124">Create a container registry</span></span>
<span data-ttu-id="fb673-125">Ejecute hello `New-AzureRMContainerRegistry` comando toocreate un registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="fb673-125">Run hello `New-AzureRMContainerRegistry` command toocreate a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="fb673-126">Cuando cree un registro, especifique un nombre de dominio de nivel superior único global que contenga solo letras y números.</span><span class="sxs-lookup"><span data-stu-id="fb673-126">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="fb673-127">nombre del registro de Hello en los ejemplos de hello `MyRegistry`, pero sustituir un nombre único de su elección.</span><span class="sxs-lookup"><span data-stu-id="fb673-127">hello registry name in hello examples is `MyRegistry`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="fb673-128">Hola el siguiente comando utiliza Hola del registro de contenedor de parámetros mínimos toocreate `MyRegistry` en grupo de recursos de hello `MyResourceGroup` Hola Ee.uu. Central sur ubicación:</span><span class="sxs-lookup"><span data-stu-id="fb673-128">hello following command uses hello minimal parameters toocreate container registry `MyRegistry` in hello resource group `MyResourceGroup` in hello South Central US location:</span></span>

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* <span data-ttu-id="fb673-129">`-StorageAccountName` es opcional.</span><span class="sxs-lookup"><span data-stu-id="fb673-129">`-StorageAccountName` is optional.</span></span> <span data-ttu-id="fb673-130">Si no se especifica, se crea una cuenta de almacenamiento con un nombre que consta del nombre del registro de hello y una marca de tiempo en hello especifica el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="fb673-130">If not specified, a storage account is created with a name consisting of hello registry name and a timestamp in hello specified resource group.</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="fb673-131">Asignación de una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="fb673-131">Assign a service principal</span></span>
<span data-ttu-id="fb673-132">Usar comandos de PowerShell tooassign Azure Active Directory [entidad de servicio](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa registro.</span><span class="sxs-lookup"><span data-stu-id="fb673-132">Use PowerShell commands tooassign an Azure Active Directory [service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa registry.</span></span> <span data-ttu-id="fb673-133">Hello entidad de servicio en estos ejemplos se asigna el rol de propietario de hello, pero puede asignar [otros roles](../active-directory/role-based-access-control-configure.md) si desea.</span><span class="sxs-lookup"><span data-stu-id="fb673-133">hello service principal in these examples is assigned hello Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal"></a><span data-ttu-id="fb673-134">Creación de una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="fb673-134">Create a service principal</span></span>
<span data-ttu-id="fb673-135">En el siguiente comando de hello, se crea una nueva entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="fb673-135">In hello following command, a new service principal is created.</span></span> <span data-ttu-id="fb673-136">Especifique una contraseña segura con hello `-Password` parámetro.</span><span class="sxs-lookup"><span data-stu-id="fb673-136">Specify a strong password with hello `-Password` parameter.</span></span>

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a><span data-ttu-id="fb673-137">Asignación de una entidad de servicio nueva o existente</span><span class="sxs-lookup"><span data-stu-id="fb673-137">Assign a new or existing service principal</span></span>
<span data-ttu-id="fb673-138">Puede asignar un nuevo o por un registro de tooa principal de servicio existente.</span><span class="sxs-lookup"><span data-stu-id="fb673-138">You can assign a new or an existing service principal tooa registry.</span></span> <span data-ttu-id="fb673-139">tooassign el registro de toohello de propietario rol acceso, que se ejecute un toohello similar de comando siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fb673-139">tooassign it Owner role access toohello registry, run a command similar toohello following example:</span></span>

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-toohello-registry-with-hello-service-principal"></a><span data-ttu-id="fb673-140">Inicie sesión en el registro de toohello con la entidad de servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="fb673-140">Sign in toohello registry with hello service principal</span></span>
<span data-ttu-id="fb673-141">Después de asignar el registro de hello servicio toohello principal, puede iniciar sesión con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="fb673-141">After assigning hello service principal toohello registry, you can sign in using hello following command:</span></span>

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a><span data-ttu-id="fb673-142">Administración de las credenciales de administrador</span><span class="sxs-lookup"><span data-stu-id="fb673-142">Manage admin credentials</span></span>
<span data-ttu-id="fb673-143">Se crea automáticamente una cuenta de administrador para cada registro de contenedor, que estará deshabilitada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="fb673-143">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="fb673-144">Hello en los ejemplos siguientes muestran comandos de PowerShell toomanage credenciales de administrador de hello para el registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="fb673-144">hello following examples show PowerShell commands toomanage hello admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="fb673-145">Obtención de las credenciales de administrador</span><span class="sxs-lookup"><span data-stu-id="fb673-145">Obtain admin user credentials</span></span>
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="fb673-146">Habilitación del usuario de administrador para un registro existente</span><span class="sxs-lookup"><span data-stu-id="fb673-146">Enable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="fb673-147">Deshabilitación del usuario de administrador para un registro existente</span><span class="sxs-lookup"><span data-stu-id="fb673-147">Disable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a><span data-ttu-id="fb673-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fb673-148">Next steps</span></span>
* [<span data-ttu-id="fb673-149">Insertar la primera imagen con hello CLI de Docker</span><span class="sxs-lookup"><span data-stu-id="fb673-149">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
