---
title: "aplicaciones que aaaPublish tooindividual los usuarios en una colección de RemoteApp de Azure (versión preliminar) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo puede publicar los usuarios tooindividual de aplicaciones, en lugar de función grupos en Azure RemoteApp."
services: remoteapp-preview
documentationcenter: 
author: piotrci
manager: mbaldwin
editor: 
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: 87b435552ddbfc2c6d03aeb01d95a44985e71f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-tooindividual-users-in-an-azure-remoteapp-collection-preview"></a><span data-ttu-id="4eabc-103">Publicar aplicaciones que los usuarios tooindividual en una colección de RemoteApp de Azure (vista previa)</span><span class="sxs-lookup"><span data-stu-id="4eabc-103">Publish applications tooindividual users in an Azure RemoteApp collection (Preview)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4eabc-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="4eabc-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="4eabc-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="4eabc-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="4eabc-106">Este artículo se explica cómo los usuarios de toopublish aplicaciones tooindividual en una colección de RemoteApp de Azure.</span><span class="sxs-lookup"><span data-stu-id="4eabc-106">This article explains how toopublish applications tooindividual users in an Azure RemoteApp collection.</span></span> <span data-ttu-id="4eabc-107">Esto es una nueva funcionalidad en Azure RemoteApp, actualmente en vista previa privada y pioneros disponible tooselect solo para fines de evaluación.</span><span class="sxs-lookup"><span data-stu-id="4eabc-107">This is new functionality in Azure RemoteApp, currently in private preview and available only tooselect early adopters for evaluation purposes.</span></span>

<span data-ttu-id="4eabc-108">Originalmente Azure RemoteApp habilitado solo un modo de publicación de aplicaciones: Administrador de hello podría publicar aplicaciones de imagen de Hola y estarían tooall visible a los usuarios en la colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="4eabc-108">Originally Azure RemoteApp enabled only one way of publishing applications: hello administrator would publish apps from hello image and they would be visible tooall users in hello collection.</span></span>

<span data-ttu-id="4eabc-109">Un escenario común es tooinclude muchas aplicaciones en una sola imagen e implementación una colección de los costos de administración de tooreduce de orden.</span><span class="sxs-lookup"><span data-stu-id="4eabc-109">A common scenario is tooinclude many applications in a single image and deploy one collection in order tooreduce management costs.</span></span> <span data-ttu-id="4eabc-110">A menudo no todas las aplicaciones son usuarios de tooall relevante: administradores preferirían a los usuarios de toopublish aplicaciones tooindividual no ver aplicaciones innecesarias en su aplicación de fuentes de distribución.</span><span class="sxs-lookup"><span data-stu-id="4eabc-110">Oftentimes not all applications are relevant tooall users – administrators would prefer toopublish apps tooindividual users so they don’t see unnecessary applications in their application feed.</span></span>

<span data-ttu-id="4eabc-111">Ahora, esto es posible en Azure RemoteApp: actualmente solo como una característica de versión preliminar limitada.</span><span class="sxs-lookup"><span data-stu-id="4eabc-111">This is now possible in Azure RemoteApp – currently as a limited preview feature.</span></span> <span data-ttu-id="4eabc-112">Este es un breve resumen de la nueva funcionalidad de hello:</span><span class="sxs-lookup"><span data-stu-id="4eabc-112">Here is a brief summary of hello new functionality:</span></span>

1. <span data-ttu-id="4eabc-113">Una colección se puede establecer de uno de estos dos modos:</span><span class="sxs-lookup"><span data-stu-id="4eabc-113">A collection can be set into one of two modes:</span></span>
   
   * <span data-ttu-id="4eabc-114">modo de recopilación original Hello, donde pueden ver todos los usuarios de una colección de todas las aplicaciones publicadas.</span><span class="sxs-lookup"><span data-stu-id="4eabc-114">hello original collection mode, where all users in a collection can see all published applications.</span></span> <span data-ttu-id="4eabc-115">Se trata de modo predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="4eabc-115">This is hello default mode.</span></span>
   * <span data-ttu-id="4eabc-116">nuevo modo de aplicación Hola, donde los usuarios sólo verán las aplicaciones que se han asignado explícitamente toothem</span><span class="sxs-lookup"><span data-stu-id="4eabc-116">hello new application mode, where users only see applications that have been explicitly assigned toothem</span></span>
2. <span data-ttu-id="4eabc-117">En el momento de hello en modo de aplicación Hola solo puede habilitarse mediante cmdlets de PowerShell de Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="4eabc-117">At hello moment hello application mode can only be enabled using Azure RemoteApp PowerShell cmdlets.</span></span>
   
   * <span data-ttu-id="4eabc-118">Al establecer el modo de tooapplication, asignación de usuario en el conjunto de hello no se pueden administrar a través de Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4eabc-118">When set tooapplication mode, user assignment in hello collection cannot be managed through hello Azure portal.</span></span> <span data-ttu-id="4eabc-119">Asignación de usuario tiene toobe administra a través de los cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4eabc-119">User assignment has toobe managed through PowerShell cmdlets.</span></span>
3. <span data-ttu-id="4eabc-120">Los usuarios sólo verán las aplicaciones de hello directamente publican toothem.</span><span class="sxs-lookup"><span data-stu-id="4eabc-120">Users will only see hello applications published directly toothem.</span></span> <span data-ttu-id="4eabc-121">Sin embargo, es aún posible para un usuario toolaunch Hola otras aplicaciones disponibles en la imagen de hello mediante el acceso a ellos directamente en el sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4eabc-121">However, it may still be possible for a user toolaunch hello other applications available on hello image by accessing them directly in hello operating system.</span></span>
   
   * <span data-ttu-id="4eabc-122">Esta característica no proporciona un bloqueo seguro de aplicaciones; sólo limita la visibilidad en la aplicación hello fuente de distribución.</span><span class="sxs-lookup"><span data-stu-id="4eabc-122">This feature does not provide a secure lockdown of applications; it only limits visibility in hello application feed.</span></span>
   * <span data-ttu-id="4eabc-123">Si necesita tooisolate a los usuarios de aplicaciones, necesitará toouse de colecciones independientes para.</span><span class="sxs-lookup"><span data-stu-id="4eabc-123">If you need tooisolate users from applications, you will need toouse separate collections for that.</span></span>

## <a name="how-tooget-azure-remoteapp-powershell-cmdlets"></a><span data-ttu-id="4eabc-124">¿Cómo tooget cmdlets de PowerShell de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="4eabc-124">How tooget Azure RemoteApp PowerShell cmdlets</span></span>
<span data-ttu-id="4eabc-125">tootry Hola nueva funcionalidad de vista previa, necesitará toouse cmdlets de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="4eabc-125">tootry hello new preview functionality, you will need toouse Azure PowerShell cmdlets.</span></span> <span data-ttu-id="4eabc-126">Actualmente no es toouse posibles hello Azure Management portal tooenable Hola nueva publicación modo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="4eabc-126">It is currently not possible toouse hello Azure Management portal tooenable hello new application publishing mode.</span></span>

<span data-ttu-id="4eabc-127">En primer lugar, asegúrese de que tiene hello [módulo Azure PowerShell](/powershell/azure/overview) instalado.</span><span class="sxs-lookup"><span data-stu-id="4eabc-127">First, make sure you have hello [Azure PowerShell module](/powershell/azure/overview) installed.</span></span>

<span data-ttu-id="4eabc-128">A continuación, iniciar la consola de PowerShell de hello en modo de administrador y ejecución Hola siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4eabc-128">Then launch hello PowerShell console in administrator mode and run hello following cmdlet:</span></span>

        Add-AzureAccount

<span data-ttu-id="4eabc-129">Se le pedirá el nombre de usuario y la contraseña de Azure.</span><span class="sxs-lookup"><span data-stu-id="4eabc-129">It will prompt you for your Azure user name and password.</span></span> <span data-ttu-id="4eabc-130">Una vez iniciado sesión, se efectuarán toorun capaz de cmdlets de Azure RemoteApp en las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="4eabc-130">Once signed in, you will be able toorun Azure RemoteApp cmdlets against your Azure subscriptions.</span></span>

## <a name="how-toocheck-which-mode-a-collection-is-in"></a><span data-ttu-id="4eabc-131">¿Cómo toocheck de modo que una colección está en</span><span class="sxs-lookup"><span data-stu-id="4eabc-131">How toocheck which mode a collection is in</span></span>
<span data-ttu-id="4eabc-132">Ejecute hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4eabc-132">Run hello following cmdlet:</span></span>

        Get-AzureRemoteAppCollection <collectionName>

![Modo de recopilación de Hola de comprobación](./media/remoteapp-perapp/araacllelvel.png)

<span data-ttu-id="4eabc-134">Hola AclLevel propiedad puede tener Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="4eabc-134">hello AclLevel property can have hello following values:</span></span>

* <span data-ttu-id="4eabc-135">Colección: Hola publicación modo original.</span><span class="sxs-lookup"><span data-stu-id="4eabc-135">Collection: hello original publishing mode.</span></span> <span data-ttu-id="4eabc-136">Todos los usuarios pueden ver todas las aplicaciones publicadas.</span><span class="sxs-lookup"><span data-stu-id="4eabc-136">All users see all published apps.</span></span>
* <span data-ttu-id="4eabc-137">Aplicación: Hola nuevo modo de publicación.</span><span class="sxs-lookup"><span data-stu-id="4eabc-137">Application: hello new publishing mode.</span></span> <span data-ttu-id="4eabc-138">Los usuarios ver solo las aplicaciones de hello directamente publicarán toothem.</span><span class="sxs-lookup"><span data-stu-id="4eabc-138">Users see only hello apps published directly toothem.</span></span>

## <a name="how-tooswitch-tooapplication-publishing-mode"></a><span data-ttu-id="4eabc-139">Cómo el modo de publicación de tooapplication tooswitch</span><span class="sxs-lookup"><span data-stu-id="4eabc-139">How tooswitch tooapplication publishing mode</span></span>
<span data-ttu-id="4eabc-140">Ejecute hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4eabc-140">Run hello following cmdlet:</span></span>

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

<span data-ttu-id="4eabc-141">Se conservará el estado de publicación de aplicación: inicialmente todos los usuarios verán todas las aplicaciones publicadas original Hola.</span><span class="sxs-lookup"><span data-stu-id="4eabc-141">Application publishing state will be preserved: initially all users will see all of hello original published apps.</span></span>

## <a name="how-toolist-users-who-can-see-a-specific-application"></a><span data-ttu-id="4eabc-142">Cómo los usuarios de toolist que pueden ver una aplicación específica</span><span class="sxs-lookup"><span data-stu-id="4eabc-142">How toolist users who can see a specific application</span></span>
<span data-ttu-id="4eabc-143">Ejecute hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4eabc-143">Run hello following cmdlet:</span></span>

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

<span data-ttu-id="4eabc-144">Esta acción muestra todos los usuarios que pueden ver la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="4eabc-144">This lists all users who can see hello application.</span></span>

<span data-ttu-id="4eabc-145">Nota: Puede ver el alias de la aplicación de hello (denominados "alias de la aplicación" en la sintaxis de hello anterior) mediante la ejecución de Get-AzureRemoteAppProgram - nombreDeColección <collectionName>.</span><span class="sxs-lookup"><span data-stu-id="4eabc-145">Note: You can see hello application aliases (called "app alias" in hello syntax above) by running Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span></span>

## <a name="how-tooassign-an-application-tooa-user"></a><span data-ttu-id="4eabc-146">¿Cómo tooassign un usuario de tooa la aplicación</span><span class="sxs-lookup"><span data-stu-id="4eabc-146">How tooassign an application tooa user</span></span>
<span data-ttu-id="4eabc-147">Ejecute hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4eabc-147">Run hello following cmdlet:</span></span>

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

<span data-ttu-id="4eabc-148">usuario de Hello ahora podrán disfrutar aplicación hello en el cliente de Azure RemoteApp hello y será capaz de tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="4eabc-148">hello user will now see hello application in hello Azure RemoteApp client and will be able tooconnect tooit.</span></span>

## <a name="how-tooremove-an-application-from-a-user"></a><span data-ttu-id="4eabc-149">¿Cómo tooremove una aplicación de un usuario</span><span class="sxs-lookup"><span data-stu-id="4eabc-149">How tooremove an application from a user</span></span>
<span data-ttu-id="4eabc-150">Ejecute hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4eabc-150">Run hello following cmdlet:</span></span>

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a><span data-ttu-id="4eabc-151">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="4eabc-151">Providing feedback</span></span>
<span data-ttu-id="4eabc-152">Agradecemos sus comentarios y sugerencias sobre esta característica de la versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="4eabc-152">We appreciate your feedback and suggestions regarding this preview feature.</span></span> <span data-ttu-id="4eabc-153">Rellene hello [encuesta](http://www.instant.ly/s/FDdrb) toolet nos conocer su opinión.</span><span class="sxs-lookup"><span data-stu-id="4eabc-153">Please fill out hello [survey](http://www.instant.ly/s/FDdrb) toolet us know what you think.</span></span>

## <a name="havent-had-a-chance-tootry-hello-preview-feature"></a><span data-ttu-id="4eabc-154">¿No he tenido una característica de vista previa de oportunidad tootry Hola?</span><span class="sxs-lookup"><span data-stu-id="4eabc-154">Haven't had a chance tootry hello preview feature?</span></span>
<span data-ttu-id="4eabc-155">Si no ha participado en vista previa de hello todavía, use este [encuesta](http://www.instant.ly/s/AY83p) toorequest acceso.</span><span class="sxs-lookup"><span data-stu-id="4eabc-155">If you have not participated in hello preview yet, please use this [survey](http://www.instant.ly/s/AY83p) toorequest access.</span></span>

