---
title: "Creación de un registro privado de Docker: Azure Portal | Microsoft Docs"
description: "Introducción a la creación y la administración de registros de contenedor privados de Docker mediante Azure Portal"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7fbbb56d775ee96c9a44363a4e41d4fc3c630582
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-private-docker-container-registry-using-the-azure-portal"></a><span data-ttu-id="a2a99-103">Creación de un registro de contenedor privado de Docker con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a2a99-103">Create a private Docker container registry using the Azure portal</span></span>
<span data-ttu-id="a2a99-104">Use Azure Portal para crear un registro de contenedor y administrar su configuración.</span><span class="sxs-lookup"><span data-stu-id="a2a99-104">Use the Azure portal to create a container registry and manage its settings.</span></span> <span data-ttu-id="a2a99-105">También puede crear y administrar registros de contenedor mediante los [comandos de la CLI de Azure 2.0](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) o mediante programación con la [API de REST](https://go.microsoft.com/fwlink/p/?linkid=834376) de Container Registry.</span><span class="sxs-lookup"><span data-stu-id="a2a99-105">You can also create and manage container registries using the [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>

<span data-ttu-id="a2a99-106">Para más información sobre el entorno y los conceptos, consulte [la información general](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="a2a99-106">For background and concepts, see [the overview](container-registry-intro.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="a2a99-107">Creación de un registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="a2a99-107">Create a container registry</span></span>
1. <span data-ttu-id="a2a99-108">En [Azure Portal](https://portal.azure.com), haga clic **+ Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="a2a99-108">In the [Azure portal](https://portal.azure.com), click **+ New**.</span></span>
2. <span data-ttu-id="a2a99-109">Busque en el Marketplace **Azure Container Registry**.</span><span class="sxs-lookup"><span data-stu-id="a2a99-109">Search the marketplace for **Azure container registry**.</span></span>
3. <span data-ttu-id="a2a99-110">Seleccione **Azure Container Registry**, con el publicador **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="a2a99-110">Select **Azure Container Registry**, with publisher **Microsoft**.</span></span>
    <span data-ttu-id="a2a99-111">![Servicio Container Registry en Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span><span class="sxs-lookup"><span data-stu-id="a2a99-111">![Container Registry service in Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span></span>
4. <span data-ttu-id="a2a99-112">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a2a99-112">Click **Create**.</span></span> <span data-ttu-id="a2a99-113">Aparece la hoja **Azure Container Registry**.</span><span class="sxs-lookup"><span data-stu-id="a2a99-113">The **Azure Container Registry** blade appears.</span></span>

    ![Configuración de Container Registry](./media/container-registry-get-started-portal/container-registry-settings.png)
5. <span data-ttu-id="a2a99-115">En la hoja **Azure Container Registry**, escriba la siguiente información.</span><span class="sxs-lookup"><span data-stu-id="a2a99-115">In the **Azure Container Registry** blade, enter the following information.</span></span> <span data-ttu-id="a2a99-116">Cuando haya terminado, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a2a99-116">Click **Create** when you are done.</span></span>

    <span data-ttu-id="a2a99-117">a.</span><span class="sxs-lookup"><span data-stu-id="a2a99-117">a.</span></span> <span data-ttu-id="a2a99-118">**Nombre del registro**: un nombre de dominio de nivel superior único global para el registro específico.</span><span class="sxs-lookup"><span data-stu-id="a2a99-118">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="a2a99-119">En este ejemplo, el nombre del registro es *myRegistry01*, pero puede sustituirlo por un nombre único de su elección.</span><span class="sxs-lookup"><span data-stu-id="a2a99-119">In this example, the registry name is *myRegistry01*, but substitute a unique name of your own.</span></span> <span data-ttu-id="a2a99-120">El nombre puede contener solo letras y números.</span><span class="sxs-lookup"><span data-stu-id="a2a99-120">The name can contain only letters and numbers.</span></span>

    <span data-ttu-id="a2a99-121">b.</span><span class="sxs-lookup"><span data-stu-id="a2a99-121">b.</span></span> <span data-ttu-id="a2a99-122">**Grupo de recursos**: seleccione un [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) existente o escriba el nombre para crear uno.</span><span class="sxs-lookup"><span data-stu-id="a2a99-122">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span>

    <span data-ttu-id="a2a99-123">c.</span><span class="sxs-lookup"><span data-stu-id="a2a99-123">c.</span></span> <span data-ttu-id="a2a99-124">**Ubicación**: seleccione una ubicación para el centro de datos de Azure en la que el servicio esté [disponible](https://azure.microsoft.com/regions/services/) como, por ejemplo, **centro-sur de EE. UU**.</span><span class="sxs-lookup"><span data-stu-id="a2a99-124">**Location**: Select an Azure datacenter location where the service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="a2a99-125">d.</span><span class="sxs-lookup"><span data-stu-id="a2a99-125">d.</span></span> <span data-ttu-id="a2a99-126">**Usuario administrador**: si lo desea, habilite un usuario administrador para acceder al registro.</span><span class="sxs-lookup"><span data-stu-id="a2a99-126">**Admin user**: If you want, enable an admin user to access the registry.</span></span> <span data-ttu-id="a2a99-127">Puede cambiar esta configuración después de crear el registro.</span><span class="sxs-lookup"><span data-stu-id="a2a99-127">You can change this setting after creating the registry.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="a2a99-128">Además de proporcionar acceso a través de una cuenta de usuario de administrador, los registros de contenedor admiten la autenticación respaldada por entidades de servicio de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a2a99-128">In addition to providing access through an admin user account, container registries support authentication backed by Azure Active Directory service principals.</span></span> <span data-ttu-id="a2a99-129">Para más información y otras consideraciones, consulte [Authenticate with the container registry](container-registry-authentication.md) (Autenticación con el registro de contenedor).</span><span class="sxs-lookup"><span data-stu-id="a2a99-129">For more information and considerations, see [Authenticate with a container registry](container-registry-authentication.md).</span></span>
      >

    <span data-ttu-id="a2a99-130">e.</span><span class="sxs-lookup"><span data-stu-id="a2a99-130">e.</span></span> <span data-ttu-id="a2a99-131">**Cuenta de almacenamiento**: use la configuración predeterminada para crear una [cuenta de almacenamiento](../storage/common/storage-introduction.md) o seleccione una cuenta de almacenamiento existente en la misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="a2a99-131">**Storage account**: Use the default setting to create a [storage account](../storage/common/storage-introduction.md), or select an existing storage account in the same location.</span></span> <span data-ttu-id="a2a99-132">Premium Storage no se admite actualmente.</span><span class="sxs-lookup"><span data-stu-id="a2a99-132">Currently Premium Storage is not supported.</span></span>

## <a name="manage-registry-settings"></a><span data-ttu-id="a2a99-133">Administración de la configuración del registro</span><span class="sxs-lookup"><span data-stu-id="a2a99-133">Manage registry settings</span></span>
<span data-ttu-id="a2a99-134">Después de crear el registro, busque la configuración de este iniciando la hoja **Registros de contenedor** del portal.</span><span class="sxs-lookup"><span data-stu-id="a2a99-134">After creating the registry, find the registry settings by starting at the **Container Registries** blade in the portal.</span></span> <span data-ttu-id="a2a99-135">Por ejemplo, necesitará la configuración para iniciar sesión en el registro, o puede que desee habilitar o deshabilitar el usuario administrador.</span><span class="sxs-lookup"><span data-stu-id="a2a99-135">For example, you might need the settings to log in to your registry, or you might want to enable or disable the admin user.</span></span>

1. <span data-ttu-id="a2a99-136">En la hoja **Registros de contenedor**, haga clic en el nombre del registro.</span><span class="sxs-lookup"><span data-stu-id="a2a99-136">On the **Container Registries** blade, click the name of your registry.</span></span>

    ![Hoja Registro de contenedor](./media/container-registry-get-started-portal/container-registry-blade.png)
2. <span data-ttu-id="a2a99-138">Para administrar la configuración de acceso, haga clic en **Clave de acceso**.</span><span class="sxs-lookup"><span data-stu-id="a2a99-138">To manage access settings, click **Access key**.</span></span>

    ![Acceso al registro de contenedor](./media/container-registry-get-started-portal/container-registry-access.png)
3. <span data-ttu-id="a2a99-140">Tenga en cuenta la siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="a2a99-140">Note the following settings:</span></span>

   * <span data-ttu-id="a2a99-141">**Servidor de inicio de sesión**: el nombre completo que usa para iniciar sesión en el registro.</span><span class="sxs-lookup"><span data-stu-id="a2a99-141">**Login server** - The fully qualified name you use to log in to the registry.</span></span> <span data-ttu-id="a2a99-142">En este ejemplo, es `myregistry01.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="a2a99-142">In this example, it is `myregistry01.azurecr.io`.</span></span>
   * <span data-ttu-id="a2a99-143">**Usuario administrador**: elija habilitar o deshabilitar la cuenta de usuario administrador del registro.</span><span class="sxs-lookup"><span data-stu-id="a2a99-143">**Admin user** - Toggle to enable or disable the registry's admin user account.</span></span>
   * <span data-ttu-id="a2a99-144">**Nombre de usuario** y **contraseña**: las credenciales de la cuenta de usuario administrador (si está habilitado) que puede usar para iniciar sesión en el registro.</span><span class="sxs-lookup"><span data-stu-id="a2a99-144">**Username** and **Password** - The credentials of the admin user account (if enabled) you can use to log in to the registry.</span></span> <span data-ttu-id="a2a99-145">Si lo desea, puede volver a generar la contraseña.</span><span class="sxs-lookup"><span data-stu-id="a2a99-145">You can optionally regenerate the passwords.</span></span> <span data-ttu-id="a2a99-146">Se crean dos contraseñas para que pueda mantener las conexiones en el registro mediante una contraseña mientras vuelve a generar la contraseña de la otra.</span><span class="sxs-lookup"><span data-stu-id="a2a99-146">Two passwords are created so that you can maintain connections to the registry by using one password while you regenerate the other password.</span></span> <span data-ttu-id="a2a99-147">Para autenticarse con una entidad de servicio en su lugar, consulte [Autenticación con un registro de contenedor privado de Docker](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a2a99-147">To authenticate with a service principal instead, see [Authenticate with a private Docker container registry](container-registry-authentication.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2a99-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a2a99-148">Next steps</span></span>
* [<span data-ttu-id="a2a99-149">Insertar la primera imagen mediante la CLI de Docker</span><span class="sxs-lookup"><span data-stu-id="a2a99-149">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
