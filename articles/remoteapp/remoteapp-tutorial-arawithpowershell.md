---
title: cmdlets de PowerShell con Azure RemoteApp aaaUse | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse cmdlets de Windows PowerShell en Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a><span data-ttu-id="813ae-103">Uso de cmdlets de Windows PowerShell con Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="813ae-103">Use Windows PowerShell cmdlets with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="813ae-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="813ae-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="813ae-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="813ae-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

 <span data-ttu-id="813ae-106">Puede usar tooadminister de cmdlets de PowerShell de Azure RemoteApp hello y mantener las colecciones.</span><span class="sxs-lookup"><span data-stu-id="813ae-106">You can use hello Azure RemoteApp PowerShell cmdlets tooadminister and maintain your collections.</span></span> <span data-ttu-id="813ae-107">Usar hello después tooget de información que se inició.</span><span class="sxs-lookup"><span data-stu-id="813ae-107">Use hello following information tooget started.</span></span>

## <a name="get-hello-cmdlets"></a><span data-ttu-id="813ae-108">Obtener Hola cmdlets</span><span class="sxs-lookup"><span data-stu-id="813ae-108">Get hello cmdlets</span></span>
- - -
<span data-ttu-id="813ae-109">En primer lugar descargar cmdlets de Powershell de Azure de hello [aquí](http://go.microsoft.com/?linkid=9811175), Hola RemoteApp cmdlets se incluyen en ella.</span><span class="sxs-lookup"><span data-stu-id="813ae-109">First download hello Azure Powershell cmdlets [here](http://go.microsoft.com/?linkid=9811175), hello RemoteApp cmdlets are included in it.</span></span> 

<span data-ttu-id="813ae-110">Extraer del repositorio hello [ayuda de cmdlet de Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="813ae-110">Check out hello [Azure RemoteApp cmdlet help](/powershell/module/azure?view=azuresmps-3.7.0).</span></span>

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a><span data-ttu-id="813ae-111">Configurar la suscripción de toouse de cmdlets de Azure</span><span class="sxs-lookup"><span data-stu-id="813ae-111">Configure Azure cmdlets toouse your subscription</span></span>
- - -
<span data-ttu-id="813ae-112">Siga [esta guía](/powershell/azure/overview) para poder usar cmdlets de hello en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="813ae-112">Follow [this guide](/powershell/azure/overview) so you can use hello cmdlets against your Azure subscription.</span></span>

<span data-ttu-id="813ae-113">Puede usar estos tooget pasos incluye una rápida introducción:</span><span class="sxs-lookup"><span data-stu-id="813ae-113">You can use these steps tooget started quickly:</span></span>

1. <span data-ttu-id="813ae-114">Descargue e instale hello [cmdlets de PowerShell de Azure](http://go.microsoft.com/?linkid=9811175).</span><span class="sxs-lookup"><span data-stu-id="813ae-114">Download and install hello [Azure PowerShell cmdlets](http://go.microsoft.com/?linkid=9811175).</span></span>
2. <span data-ttu-id="813ae-115">Inicie Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="813ae-115">Launch Microsoft Azure PowerShell.</span></span>
3. <span data-ttu-id="813ae-116">Ejecutar **Add-AzureAccount** tooauthenticate tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="813ae-116">Run **Add-AzureAccount** tooauthenticate tooyour Azure subscription.</span></span> <span data-ttu-id="813ae-117">Cuando se le solicite, escriba Hola el mismo nombre de usuario y la contraseña que usa toosign en tooAzure portal.</span><span class="sxs-lookup"><span data-stu-id="813ae-117">When prompted, enter hello same user name and password that you use toosign in tooAzure portal.</span></span>  
4. <span data-ttu-id="813ae-118">Ejecutar **Get-AzureSubscription** suscripciones de hello toolist asociadas con su cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="813ae-118">Run **Get-AzureSubscription** toolist hello subscriptions associated with your user account.</span></span> 
5. <span data-ttu-id="813ae-119">Ejecutar **Select-AzureSubscription - SubscriptionName &lt;nombre de la suscripción&gt;**  o **Select-AzureSubscription - SubscriptionId &lt;Id. de suscripción&gt;**  toospecify Hola suscripción toouse.</span><span class="sxs-lookup"><span data-stu-id="813ae-119">Run **Select-AzureSubscription -SubscriptionName &lt;subscription name&gt;** or **Select-AzureSubscription -SubscriptionId &lt;subscription ID&gt;** toospecify hello subscription toouse.</span></span>

<span data-ttu-id="813ae-120">Enhorabuena, la consola de PowerShell de Azure está configurado y listo toouse.</span><span class="sxs-lookup"><span data-stu-id="813ae-120">Congratulations, your Azure PowerShell console is configured and ready toouse.</span></span> <span data-ttu-id="813ae-121">Tenga en cuenta que, cada vez que inicie la consola de Azure PowerShell Hola Hola, necesitará toorepeate los pasos 2 a 5.</span><span class="sxs-lookup"><span data-stu-id="813ae-121">Be aware that you'll need toorepeate steps 2 through 5 each time you start hello hello Azure PowerShell console.</span></span>  


## <a name="list-all-collections"></a><span data-ttu-id="813ae-122">Lista de todas las colecciones</span><span class="sxs-lookup"><span data-stu-id="813ae-122">List all collections</span></span>
- - -
     <span data-ttu-id="813ae-123">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="813ae-123">Get-AzureRemoteAppCollection</span></span>

## <a name="delete-a-collection"></a><span data-ttu-id="813ae-124">Eliminación de una colección</span><span class="sxs-lookup"><span data-stu-id="813ae-124">Delete a collection</span></span>
- - -
    <span data-ttu-id="813ae-125">Remove-AzureRemoteAppCollection <enter collection name></span><span class="sxs-lookup"><span data-stu-id="813ae-125">Remove-AzureRemoteAppCollection <enter collection name></span></span>

<span data-ttu-id="813ae-126">Ejemplo: `Remove-AzureRemoteAppCollection ContosoProduction`.</span><span class="sxs-lookup"><span data-stu-id="813ae-126">Example:  `Remove-AzureRemoteAppCollection ContosoProduction`.</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="813ae-127">Creación de una colección en la nube</span><span class="sxs-lookup"><span data-stu-id="813ae-127">Create a cloud collection</span></span>
- - -
<span data-ttu-id="813ae-128">Es sencillo, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="813ae-128">It's simple, run hello following command:</span></span>

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

<span data-ttu-id="813ae-129">Hola encima comando publica automáticamente las aplicaciones de Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio y Word).</span><span class="sxs-lookup"><span data-stu-id="813ae-129">hello above command automatically publishes Microsoft Office 365 applications (Excel, OneNote, Outlook, PowerPoint, Visio and Word).</span></span>

<span data-ttu-id="813ae-130">Creación de la colección puede tardar 30 minutos o más toocomplete.</span><span class="sxs-lookup"><span data-stu-id="813ae-130">Collection creation can take 30 minutes or longer toocomplete.</span></span> <span data-ttu-id="813ae-131">Por lo tanto, este comando devuelve un identificador de seguimiento que se puede utilizar como sigue:</span><span class="sxs-lookup"><span data-stu-id="813ae-131">Therefore, this command returns a tracking ID that you can use as follows:</span></span>

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

<span data-ttu-id="813ae-132">Después de realiza la recopilación de hello, puede agregar la recopilación de toohello de usuarios con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="813ae-132">After hello collection is done, you can add users toohello collection with hello following command:</span></span>

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

<span data-ttu-id="813ae-133">¡Y ya está!</span><span class="sxs-lookup"><span data-stu-id="813ae-133">And you're done!</span></span> <span data-ttu-id="813ae-134">Ese usuario debe ser capaz de tooconnect toohello con cliente de Azure RemoteApp Hola encontró [aquí](https://www.remoteapp.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="813ae-134">That user should be able tooconnect toohello application using hello Azure RemoteApp client found [here](https://www.remoteapp.windowsazure.com/).</span></span>

## <a name="available-cmdlets"></a><span data-ttu-id="813ae-135">Cmdlets disponibles</span><span class="sxs-lookup"><span data-stu-id="813ae-135">Available cmdlets</span></span>
<span data-ttu-id="813ae-136">Hay muchos otros comandos que tenemos, documentación de Hola para ellos estará disponible en breve:</span><span class="sxs-lookup"><span data-stu-id="813ae-136">There are lots of other commands that we have, hello documentation for them will be coming shortly:</span></span>

<span data-ttu-id="813ae-137">Cmdlets básicos de la colección de RemoteApp</span><span class="sxs-lookup"><span data-stu-id="813ae-137">Basic RemoteApp Collection cmdlets:</span></span> 

* <span data-ttu-id="813ae-138">New-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="813ae-138">New-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="813ae-139">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="813ae-139">Get-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="813ae-140">Set-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="813ae-140">Set-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="813ae-141">Update-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="813ae-141">Update-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="813ae-142">Remove-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="813ae-142">Remove-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="813ae-143">Add-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="813ae-143">Add-AzureRemoteAppUser</span></span>
* <span data-ttu-id="813ae-144">Get-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="813ae-144">Get-AzureRemoteAppUser</span></span>
* <span data-ttu-id="813ae-145">Remove-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="813ae-145">Remove-AzureRemoteAppUser</span></span>
* <span data-ttu-id="813ae-146">Get-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="813ae-146">Get-AzureRemoteAppSession</span></span>
* <span data-ttu-id="813ae-147">Disconnect-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="813ae-147">Disconnect-AzureRemoteAppSession</span></span>
* <span data-ttu-id="813ae-148">Invoke-AzureRemoteAppSessionLogoff</span><span class="sxs-lookup"><span data-stu-id="813ae-148">Invoke-AzureRemoteAppSessionLogoff</span></span>
* <span data-ttu-id="813ae-149">Send-AzureRemoteAppSessionMessage</span><span class="sxs-lookup"><span data-stu-id="813ae-149">Send-AzureRemoteAppSessionMessage</span></span>
* <span data-ttu-id="813ae-150">Get-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="813ae-150">Get-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="813ae-151">Get-AzureRemoteAppStartMenuProgram</span><span class="sxs-lookup"><span data-stu-id="813ae-151">Get-AzureRemoteAppStartMenuProgram</span></span>
* <span data-ttu-id="813ae-152">Publish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="813ae-152">Publish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="813ae-153">Unpublish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="813ae-153">Unpublish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="813ae-154">Get-AzureRemoteAppCollectionUsageDetails</span><span class="sxs-lookup"><span data-stu-id="813ae-154">Get-AzureRemoteAppCollectionUsageDetails</span></span>
* <span data-ttu-id="813ae-155">Get-AzureRemoteAppCollectionUsageSummary</span><span class="sxs-lookup"><span data-stu-id="813ae-155">Get-AzureRemoteAppCollectionUsageSummary</span></span>
* <span data-ttu-id="813ae-156">Get-AzureRemoteAppPlan</span><span class="sxs-lookup"><span data-stu-id="813ae-156">Get-AzureRemoteAppPlan</span></span>

<span data-ttu-id="813ae-157">Cmdlets de red virtual de RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="813ae-157">RemoteApp virtual network cmdlets:</span></span>

* <span data-ttu-id="813ae-158">New-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="813ae-158">New-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="813ae-159">Get-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="813ae-159">Get-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="813ae-160">Set-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="813ae-160">Set-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="813ae-161">Remove-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="813ae-161">Remove-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="813ae-162">Get-AzureRemoteAppVpnDevice</span><span class="sxs-lookup"><span data-stu-id="813ae-162">Get-AzureRemoteAppVpnDevice</span></span>
* <span data-ttu-id="813ae-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span><span class="sxs-lookup"><span data-stu-id="813ae-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span></span>
* <span data-ttu-id="813ae-164">Reset-AzureRemoteAppVpnSharedKey</span><span class="sxs-lookup"><span data-stu-id="813ae-164">Reset-AzureRemoteAppVpnSharedKey</span></span>

<span data-ttu-id="813ae-165">Cmdlets de imagen de plantilla de RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="813ae-165">RemoteApp template image cmdlets:</span></span>

* <span data-ttu-id="813ae-166">New-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="813ae-166">New-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="813ae-167">Get-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="813ae-167">Get-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="813ae-168">Rename-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="813ae-168">Rename-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="813ae-169">Remove-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="813ae-169">Remove-AzureRemoteAppTemplateImage</span></span>

<span data-ttu-id="813ae-170">Otros cmdlets de RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="813ae-170">Other RemoteApp cmdlets:</span></span>

* <span data-ttu-id="813ae-171">Get-AzureRemoteAppLocation</span><span class="sxs-lookup"><span data-stu-id="813ae-171">Get-AzureRemoteAppLocation</span></span>
* <span data-ttu-id="813ae-172">Get-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="813ae-172">Get-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="813ae-173">Set-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="813ae-173">Set-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="813ae-174">Get-AzureRemoteAppOperationResult</span><span class="sxs-lookup"><span data-stu-id="813ae-174">Get-AzureRemoteAppOperationResult</span></span>

