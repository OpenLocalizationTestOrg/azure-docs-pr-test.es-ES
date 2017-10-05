---
title: "Publicación de aplicaciones para usuarios individuales en una colección de Azure RemoteApp (versión preliminar) | Microsoft Docs"
description: Aprenda a publicar aplicaciones para usuarios individuales, en lugar de para grupos en Azure RemoteApp.
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
ms.openlocfilehash: c94ffffdec3e46ed08d941ee58dcf17b432e1dad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="publish-applications-to-individual-users-in-an-azure-remoteapp-collection-preview"></a><span data-ttu-id="3643b-103">Publicación de aplicaciones para usuarios individuales en una colección de Azure RemoteApp (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="3643b-103">Publish applications to individual users in an Azure RemoteApp collection (Preview)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3643b-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="3643b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3643b-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="3643b-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3643b-106">En este artículo se explica cómo publicar aplicaciones para usuarios individuales en una colección de Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3643b-106">This article explains how to publish applications to individual users in an Azure RemoteApp collection.</span></span> <span data-ttu-id="3643b-107">Esta es una nueva funcionalidad de Azure RemoteApp, actualmente en estado de "versión preliminar privada" disponible solo para usuarios pioneros seleccionados con fines de evaluación.</span><span class="sxs-lookup"><span data-stu-id="3643b-107">This is new functionality in Azure RemoteApp, currently in private preview and available only to select early adopters for evaluation purposes.</span></span>

<span data-ttu-id="3643b-108">Originalmente Azure RemoteApp solo permitía una manera de "publicar"aplicaciones: el administrador publicaba las aplicaciones a partir de la imagen y estas eran visibles para todos los usuarios de la colección.</span><span class="sxs-lookup"><span data-stu-id="3643b-108">Originally Azure RemoteApp enabled only one way of publishing applications: the administrator would publish apps from the image and they would be visible to all users in the collection.</span></span>

<span data-ttu-id="3643b-109">Un escenario común consiste en incluir muchas aplicaciones en una sola imagen e implementar una colección con el fin de reducir los costos de administración.</span><span class="sxs-lookup"><span data-stu-id="3643b-109">A common scenario is to include many applications in a single image and deploy one collection in order to reduce management costs.</span></span> <span data-ttu-id="3643b-110">A menudo, no todas las aplicaciones son pertinentes para todos los usuarios: los administradores prefieren publicar aplicaciones para usuarios individuales para que no vean las aplicaciones innecesarias en su fuente de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3643b-110">Oftentimes not all applications are relevant to all users – administrators would prefer to publish apps to individual users so they don’t see unnecessary applications in their application feed.</span></span>

<span data-ttu-id="3643b-111">Ahora, esto es posible en Azure RemoteApp: actualmente solo como una característica de versión preliminar limitada.</span><span class="sxs-lookup"><span data-stu-id="3643b-111">This is now possible in Azure RemoteApp – currently as a limited preview feature.</span></span> <span data-ttu-id="3643b-112">Este es un breve resumen de la nueva funcionalidad:</span><span class="sxs-lookup"><span data-stu-id="3643b-112">Here is a brief summary of the new functionality:</span></span>

1. <span data-ttu-id="3643b-113">Una colección se puede establecer de uno de estos dos modos:</span><span class="sxs-lookup"><span data-stu-id="3643b-113">A collection can be set into one of two modes:</span></span>
   
   * <span data-ttu-id="3643b-114">el modo de recopilación original, en el que todos los usuarios de una colección pueden ver todas las aplicaciones publicadas.</span><span class="sxs-lookup"><span data-stu-id="3643b-114">the original collection mode, where all users in a collection can see all published applications.</span></span> <span data-ttu-id="3643b-115">Este es el modo predeterminado.</span><span class="sxs-lookup"><span data-stu-id="3643b-115">This is the default mode.</span></span>
   * <span data-ttu-id="3643b-116">el nuevo modo de aplicación, en el que los usuarios solo ven las aplicaciones que se han asignado explícitamente a ellos</span><span class="sxs-lookup"><span data-stu-id="3643b-116">the new application mode, where users only see applications that have been explicitly assigned to them</span></span>
2. <span data-ttu-id="3643b-117">Por el momento, el modo de aplicación solo se puede habilitar mediante cmdlets de PowerShell de Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3643b-117">At the moment the application mode can only be enabled using Azure RemoteApp PowerShell cmdlets.</span></span>
   
   * <span data-ttu-id="3643b-118">Si se establece en modo de aplicación, la asignación de usuario en la colección no se puede administrar a través del Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3643b-118">When set to application mode, user assignment in the collection cannot be managed through the Azure portal.</span></span> <span data-ttu-id="3643b-119">La asignación de usuario se debe administrar mediante cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3643b-119">User assignment has to be managed through PowerShell cmdlets.</span></span>
3. <span data-ttu-id="3643b-120">Los usuarios solo verán aquellas aplicaciones publicadas directamente para ellos.</span><span class="sxs-lookup"><span data-stu-id="3643b-120">Users will only see the applications published directly to them.</span></span> <span data-ttu-id="3643b-121">No obstante, un usuario podría iniciar las demás aplicaciones disponibles en la imagen accediendo a ellas directamente en el sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="3643b-121">However, it may still be possible for a user to launch the other applications available on the image by accessing them directly in the operating system.</span></span>
   
   * <span data-ttu-id="3643b-122">Esta característica no proporciona un bloqueo de aplicaciones seguro; solo limita la visibilidad de la fuente de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3643b-122">This feature does not provide a secure lockdown of applications; it only limits visibility in the application feed.</span></span>
   * <span data-ttu-id="3643b-123">Si necesita impedir que los usuarios accedan a todas las aplicaciones, deberá utilizar colecciones independientes.</span><span class="sxs-lookup"><span data-stu-id="3643b-123">If you need to isolate users from applications, you will need to use separate collections for that.</span></span>

## <a name="how-to-get-azure-remoteapp-powershell-cmdlets"></a><span data-ttu-id="3643b-124">Obtención de los cmdlets de PowerShell de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="3643b-124">How to get Azure RemoteApp PowerShell cmdlets</span></span>
<span data-ttu-id="3643b-125">Para probar la nueva funcionalidad de la versión preliminar, debe usar los cmdlets de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3643b-125">To try the new preview functionality, you will need to use Azure PowerShell cmdlets.</span></span> <span data-ttu-id="3643b-126">Actualmente no se puede usar el Portal de administración de Azure para habilitar el modo de publicación de nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="3643b-126">It is currently not possible to use the Azure Management portal to enable the new application publishing mode.</span></span>

<span data-ttu-id="3643b-127">En primer lugar, asegúrese de tener el [módulo de Azure PowerShell](/powershell/azure/overview) instalado.</span><span class="sxs-lookup"><span data-stu-id="3643b-127">First, make sure you have the [Azure PowerShell module](/powershell/azure/overview) installed.</span></span>

<span data-ttu-id="3643b-128">A continuación, inicie la consola de PowerShell en modo de administrador y ejecute el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3643b-128">Then launch the PowerShell console in administrator mode and run the following cmdlet:</span></span>

        Add-AzureAccount

<span data-ttu-id="3643b-129">Se le pedirá el nombre de usuario y la contraseña de Azure.</span><span class="sxs-lookup"><span data-stu-id="3643b-129">It will prompt you for your Azure user name and password.</span></span> <span data-ttu-id="3643b-130">Cuando haya iniciado sesión, podrá ejecutar los cmdlets de Azure RemoteApp en las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="3643b-130">Once signed in, you will be able to run Azure RemoteApp cmdlets against your Azure subscriptions.</span></span>

## <a name="how-to-check-which-mode-a-collection-is-in"></a><span data-ttu-id="3643b-131">Cómo comprobar en qué modo está una colección</span><span class="sxs-lookup"><span data-stu-id="3643b-131">How to check which mode a collection is in</span></span>
<span data-ttu-id="3643b-132">Ejecute el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3643b-132">Run the following cmdlet:</span></span>

        Get-AzureRemoteAppCollection <collectionName>

![Comprobación del modo de recopilación](./media/remoteapp-perapp/araacllelvel.png)

<span data-ttu-id="3643b-134">La propiedad AclLevel puede tener los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="3643b-134">The AclLevel property can have the following values:</span></span>

* <span data-ttu-id="3643b-135">Recopilación: el modo de publicación original.</span><span class="sxs-lookup"><span data-stu-id="3643b-135">Collection: the original publishing mode.</span></span> <span data-ttu-id="3643b-136">Todos los usuarios pueden ver todas las aplicaciones publicadas.</span><span class="sxs-lookup"><span data-stu-id="3643b-136">All users see all published apps.</span></span>
* <span data-ttu-id="3643b-137">Aplicación: el nuevo modo de publicación</span><span class="sxs-lookup"><span data-stu-id="3643b-137">Application: the new publishing mode.</span></span> <span data-ttu-id="3643b-138">Los usuarios solo pueden ver las aplicaciones publicadas directamente para ellos.</span><span class="sxs-lookup"><span data-stu-id="3643b-138">Users see only the apps published directly to them.</span></span>

## <a name="how-to-switch-to-application-publishing-mode"></a><span data-ttu-id="3643b-139">Cómo cambiar al modo de publicación de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="3643b-139">How to switch to application publishing mode</span></span>
<span data-ttu-id="3643b-140">Ejecute el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3643b-140">Run the following cmdlet:</span></span>

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

<span data-ttu-id="3643b-141">Se conservará el estado de publicación de la aplicación: inicialmente, todos los usuarios verán las aplicaciones originales publicadas.</span><span class="sxs-lookup"><span data-stu-id="3643b-141">Application publishing state will be preserved: initially all users will see all of the original published apps.</span></span>

## <a name="how-to-list-users-who-can-see-a-specific-application"></a><span data-ttu-id="3643b-142">Cómo enumerar los usuarios que pueden ver una aplicación específica</span><span class="sxs-lookup"><span data-stu-id="3643b-142">How to list users who can see a specific application</span></span>
<span data-ttu-id="3643b-143">Ejecute el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3643b-143">Run the following cmdlet:</span></span>

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

<span data-ttu-id="3643b-144">Este cmdlet permite enumerar todos los usuarios que pueden ver la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3643b-144">This lists all users who can see the application.</span></span>

<span data-ttu-id="3643b-145">Nota: Puede ver los alias de la aplicación (denominados "appAlias" en la sintaxis anterior) mediante la ejecución de Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span><span class="sxs-lookup"><span data-stu-id="3643b-145">Note: You can see the application aliases (called "app alias" in the syntax above) by running Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span></span>

## <a name="how-to-assign-an-application-to-a-user"></a><span data-ttu-id="3643b-146">Cómo asignar una aplicación a un usuario</span><span class="sxs-lookup"><span data-stu-id="3643b-146">How to assign an application to a user</span></span>
<span data-ttu-id="3643b-147">Ejecute el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3643b-147">Run the following cmdlet:</span></span>

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

<span data-ttu-id="3643b-148">El usuario verá ahora la aplicación en el cliente de RemoteApp de Azure y podrá conectarse a ella.</span><span class="sxs-lookup"><span data-stu-id="3643b-148">The user will now see the application in the Azure RemoteApp client and will be able to connect to it.</span></span>

## <a name="how-to-remove-an-application-from-a-user"></a><span data-ttu-id="3643b-149">Cómo quitar una aplicación de un usuario</span><span class="sxs-lookup"><span data-stu-id="3643b-149">How to remove an application from a user</span></span>
<span data-ttu-id="3643b-150">Ejecute el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3643b-150">Run the following cmdlet:</span></span>

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a><span data-ttu-id="3643b-151">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="3643b-151">Providing feedback</span></span>
<span data-ttu-id="3643b-152">Agradecemos sus comentarios y sugerencias sobre esta característica de la versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="3643b-152">We appreciate your feedback and suggestions regarding this preview feature.</span></span> <span data-ttu-id="3643b-153">Rellene la [encuesta](http://www.instant.ly/s/FDdrb) para que podamos conocer su opinión.</span><span class="sxs-lookup"><span data-stu-id="3643b-153">Please fill out the [survey](http://www.instant.ly/s/FDdrb) to let us know what you think.</span></span>

## <a name="havent-had-a-chance-to-try-the-preview-feature"></a><span data-ttu-id="3643b-154">¿No ha tenido la oportunidad de probar la característica en la versión preliminar?</span><span class="sxs-lookup"><span data-stu-id="3643b-154">Haven't had a chance to try the preview feature?</span></span>
<span data-ttu-id="3643b-155">Si no ha participado aún en la versión preliminar, use esta [encuesta](http://www.instant.ly/s/AY83p) para solicitar acceso.</span><span class="sxs-lookup"><span data-stu-id="3643b-155">If you have not participated in the preview yet, please use this [survey](http://www.instant.ly/s/AY83p) to request access.</span></span>

