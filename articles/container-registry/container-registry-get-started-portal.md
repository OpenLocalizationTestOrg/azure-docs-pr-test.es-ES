---
title: registro Docker privada aaaCreate - portal de Azure | Documentos de Microsoft
description: Empezar a crear y administrar registros de contenedor de Docker privados con hello portal de Azure
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
ms.openlocfilehash: 40f3ce44fea26e5fbeca865c9da6df55c2df9511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-portal"></a><span data-ttu-id="811e0-103">Crear un registro de contenedor de Docker privado mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="811e0-103">Create a private Docker container registry using hello Azure portal</span></span>
<span data-ttu-id="811e0-104">Usar hello toocreate portal Azure un registro de contenedor y administrar su configuración.</span><span class="sxs-lookup"><span data-stu-id="811e0-104">Use hello Azure portal toocreate a container registry and manage its settings.</span></span> <span data-ttu-id="811e0-105">También puede crear y administrar registros de contenedor con hello [comandos de CLI de Azure 2.0](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) o mediante programación con registro de contenedor de hello [API de REST](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="811e0-105">You can also create and manage container registries using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>

<span data-ttu-id="811e0-106">En el fondo y conceptos, vea [Hola información general sobre](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="811e0-106">For background and concepts, see [hello overview](container-registry-intro.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="811e0-107">Creación de un registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="811e0-107">Create a container registry</span></span>
1. <span data-ttu-id="811e0-108">Hola [portal de Azure](https://portal.azure.com), haga clic en **+ nuevo**.</span><span class="sxs-lookup"><span data-stu-id="811e0-108">In hello [Azure portal](https://portal.azure.com), click **+ New**.</span></span>
2. <span data-ttu-id="811e0-109">Busque en marketplace Hola para **registro de contenedor de Azure**.</span><span class="sxs-lookup"><span data-stu-id="811e0-109">Search hello marketplace for **Azure container registry**.</span></span>
3. <span data-ttu-id="811e0-110">Seleccione **Azure Container Registry**, con el publicador **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="811e0-110">Select **Azure Container Registry**, with publisher **Microsoft**.</span></span>
    <span data-ttu-id="811e0-111">![Servicio Container Registry en Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span><span class="sxs-lookup"><span data-stu-id="811e0-111">![Container Registry service in Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span></span>
4. <span data-ttu-id="811e0-112">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="811e0-112">Click **Create**.</span></span> <span data-ttu-id="811e0-113">Hola **registro de contenedor de Azure** aparece hoja.</span><span class="sxs-lookup"><span data-stu-id="811e0-113">hello **Azure Container Registry** blade appears.</span></span>

    ![Configuración de Container Registry](./media/container-registry-get-started-portal/container-registry-settings.png)
5. <span data-ttu-id="811e0-115">Hola **registro de contenedor de Azure** hoja, escriba Hola siguiente información.</span><span class="sxs-lookup"><span data-stu-id="811e0-115">In hello **Azure Container Registry** blade, enter hello following information.</span></span> <span data-ttu-id="811e0-116">Cuando haya terminado, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="811e0-116">Click **Create** when you are done.</span></span>

    <span data-ttu-id="811e0-117">a.</span><span class="sxs-lookup"><span data-stu-id="811e0-117">a.</span></span> <span data-ttu-id="811e0-118">**Nombre del registro**: un nombre de dominio de nivel superior único global para el registro específico.</span><span class="sxs-lookup"><span data-stu-id="811e0-118">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="811e0-119">En este ejemplo, es el nombre del registro de hello *myRegistry01*, pero sustituir un nombre único de su elección.</span><span class="sxs-lookup"><span data-stu-id="811e0-119">In this example, hello registry name is *myRegistry01*, but substitute a unique name of your own.</span></span> <span data-ttu-id="811e0-120">Hola nombre puede contener sólo letras y números.</span><span class="sxs-lookup"><span data-stu-id="811e0-120">hello name can contain only letters and numbers.</span></span>

    <span data-ttu-id="811e0-121">b.</span><span class="sxs-lookup"><span data-stu-id="811e0-121">b.</span></span> <span data-ttu-id="811e0-122">**Grupo de recursos**: seleccione una existente [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) o nombre de tipo hello para uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="811e0-122">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span>

    <span data-ttu-id="811e0-123">c.</span><span class="sxs-lookup"><span data-stu-id="811e0-123">c.</span></span> <span data-ttu-id="811e0-124">**Ubicación**: seleccione la ubicación de centro de datos Azure donde es el servicio de hello [disponibles](https://azure.microsoft.com/regions/services/), como **Ee.uu. Central sur**.</span><span class="sxs-lookup"><span data-stu-id="811e0-124">**Location**: Select an Azure datacenter location where hello service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="811e0-125">d.</span><span class="sxs-lookup"><span data-stu-id="811e0-125">d.</span></span> <span data-ttu-id="811e0-126">**El usuario administrador**: si lo desea, habilitar un registro de hello de tooaccess de usuario de administrador.</span><span class="sxs-lookup"><span data-stu-id="811e0-126">**Admin user**: If you want, enable an admin user tooaccess hello registry.</span></span> <span data-ttu-id="811e0-127">Puede cambiar esta configuración después de crear el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="811e0-127">You can change this setting after creating hello registry.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="811e0-128">Además de acceso tooproviding a través de una cuenta de usuario de administrador, los registros de contenedor admiten la autenticación respaldada por entidades de servicio de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="811e0-128">In addition tooproviding access through an admin user account, container registries support authentication backed by Azure Active Directory service principals.</span></span> <span data-ttu-id="811e0-129">Para más información y otras consideraciones, consulte [Authenticate with the container registry](container-registry-authentication.md) (Autenticación con el registro de contenedor).</span><span class="sxs-lookup"><span data-stu-id="811e0-129">For more information and considerations, see [Authenticate with a container registry](container-registry-authentication.md).</span></span>
      >

    <span data-ttu-id="811e0-130">e.</span><span class="sxs-lookup"><span data-stu-id="811e0-130">e.</span></span> <span data-ttu-id="811e0-131">**Cuenta de almacenamiento**: usar Hola predeterminada configuración toocreate una [cuenta de almacenamiento](../storage/common/storage-introduction.md), o seleccione una cuenta de almacenamiento existente en hello misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="811e0-131">**Storage account**: Use hello default setting toocreate a [storage account](../storage/common/storage-introduction.md), or select an existing storage account in hello same location.</span></span> <span data-ttu-id="811e0-132">Premium Storage no se admite actualmente.</span><span class="sxs-lookup"><span data-stu-id="811e0-132">Currently Premium Storage is not supported.</span></span>

## <a name="manage-registry-settings"></a><span data-ttu-id="811e0-133">Administración de la configuración del registro</span><span class="sxs-lookup"><span data-stu-id="811e0-133">Manage registry settings</span></span>
<span data-ttu-id="811e0-134">Después de crear el registro de hello, buscar Hola configuración del registro a partir de hello **registros de contenedor** hoja en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="811e0-134">After creating hello registry, find hello registry settings by starting at hello **Container Registries** blade in hello portal.</span></span> <span data-ttu-id="811e0-135">Por ejemplo, tendrá que toolog de configuración de hello en el registro de tooyour, o puede tener tooenable o deshabilitar al usuario de administrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="811e0-135">For example, you might need hello settings toolog in tooyour registry, or you might want tooenable or disable hello admin user.</span></span>

1. <span data-ttu-id="811e0-136">En hello **registros de contenedor** hoja, haga clic en nombre de Hola de seguridad del registro.</span><span class="sxs-lookup"><span data-stu-id="811e0-136">On hello **Container Registries** blade, click hello name of your registry.</span></span>

    ![Hoja Registro de contenedor](./media/container-registry-get-started-portal/container-registry-blade.png)
2. <span data-ttu-id="811e0-138">Haga clic en configuración de acceso de toomanage, **clave de acceso**.</span><span class="sxs-lookup"><span data-stu-id="811e0-138">toomanage access settings, click **Access key**.</span></span>

    ![Acceso al registro de contenedor](./media/container-registry-get-started-portal/container-registry-access.png)
3. <span data-ttu-id="811e0-140">Tenga en cuenta Hola después de configuración:</span><span class="sxs-lookup"><span data-stu-id="811e0-140">Note hello following settings:</span></span>

   * <span data-ttu-id="811e0-141">**Servidor de inicio de sesión** -nombre completo de hello usar toolog en el registro de toohello.</span><span class="sxs-lookup"><span data-stu-id="811e0-141">**Login server** - hello fully qualified name you use toolog in toohello registry.</span></span> <span data-ttu-id="811e0-142">En este ejemplo, es `myregistry01.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="811e0-142">In this example, it is `myregistry01.azurecr.io`.</span></span>
   * <span data-ttu-id="811e0-143">**El usuario administrador** : alternar tooenable o deshabilitar la cuenta de usuario de administrador del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="811e0-143">**Admin user** - Toggle tooenable or disable hello registry's admin user account.</span></span>
   * <span data-ttu-id="811e0-144">**Nombre de usuario** y **contraseña** -Hola credenciales de cuenta de usuario de administrador de hello (si está habilitado) puede usar toolog en el registro de toohello.</span><span class="sxs-lookup"><span data-stu-id="811e0-144">**Username** and **Password** - hello credentials of hello admin user account (if enabled) you can use toolog in toohello registry.</span></span> <span data-ttu-id="811e0-145">Si lo desea, puede volver a generar contraseñas de Hola.</span><span class="sxs-lookup"><span data-stu-id="811e0-145">You can optionally regenerate hello passwords.</span></span> <span data-ttu-id="811e0-146">Se crean dos contraseñas para que pueda mantener registro toohello de conexiones mediante el uso de una contraseña mientras regenera Hola otra contraseña.</span><span class="sxs-lookup"><span data-stu-id="811e0-146">Two passwords are created so that you can maintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="811e0-147">tooauthenticate con una entidad de servicio en su lugar, vea [autenticar con un registro de contenedor de Docker privado](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="811e0-147">tooauthenticate with a service principal instead, see [Authenticate with a private Docker container registry](container-registry-authentication.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="811e0-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="811e0-148">Next steps</span></span>
* [<span data-ttu-id="811e0-149">Insertar la primera imagen con hello CLI de Docker</span><span class="sxs-lookup"><span data-stu-id="811e0-149">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
