---
title: Uso de cmdlets de PowerShell con RemoteApp de Azure | Microsoft Docs
description: "Vea cómo usar los cmdlets de Windows PowerShell con Azure RemoteApp"
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
ms.openlocfilehash: 699b20a4dadd4ecaff57e2cc80355fe545360663
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a><span data-ttu-id="ac808-103">Uso de cmdlets de Windows PowerShell con Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="ac808-103">Use Windows PowerShell cmdlets with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ac808-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="ac808-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ac808-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="ac808-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

 <span data-ttu-id="ac808-106">Puede usar los cmdlets de PowerShell de RemoteApp de Azure para administrar y mantener las colecciones.</span><span class="sxs-lookup"><span data-stu-id="ac808-106">You can use the Azure RemoteApp PowerShell cmdlets to administer and maintain your collections.</span></span> <span data-ttu-id="ac808-107">Use la siguiente información para comenzar.</span><span class="sxs-lookup"><span data-stu-id="ac808-107">Use the following information to get started.</span></span>

## <a name="get-the-cmdlets"></a><span data-ttu-id="ac808-108">Obtención de los cmdlets</span><span class="sxs-lookup"><span data-stu-id="ac808-108">Get the cmdlets</span></span>
- - -
<span data-ttu-id="ac808-109">En primer lugar, descargue [aquí](http://go.microsoft.com/?linkid=9811175)los cmdlets de Azure PowerShell, que incluyen los de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ac808-109">First download the Azure Powershell cmdlets [here](http://go.microsoft.com/?linkid=9811175), the RemoteApp cmdlets are included in it.</span></span> 

<span data-ttu-id="ac808-110">Consulte la [ayuda de cmdlets de Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="ac808-110">Check out the [Azure RemoteApp cmdlet help](/powershell/module/azure?view=azuresmps-3.7.0).</span></span>

## <a name="configure-azure-cmdlets-to-use-your-subscription"></a><span data-ttu-id="ac808-111">Configuración de los cmdlets de Azure para usar su suscripción</span><span class="sxs-lookup"><span data-stu-id="ac808-111">Configure Azure cmdlets to use your subscription</span></span>
- - -
<span data-ttu-id="ac808-112">Siga [esta guía](/powershell/azure/overview) para poder usar los cmdlets en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac808-112">Follow [this guide](/powershell/azure/overview) so you can use the cmdlets against your Azure subscription.</span></span>

<span data-ttu-id="ac808-113">Puede usar estos pasos para una introducción rápida:</span><span class="sxs-lookup"><span data-stu-id="ac808-113">You can use these steps to get started quickly:</span></span>

1. <span data-ttu-id="ac808-114">Descargue e instale los [cmdlets de Azure PowerShell](http://go.microsoft.com/?linkid=9811175).</span><span class="sxs-lookup"><span data-stu-id="ac808-114">Download and install the [Azure PowerShell cmdlets](http://go.microsoft.com/?linkid=9811175).</span></span>
2. <span data-ttu-id="ac808-115">Inicie Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac808-115">Launch Microsoft Azure PowerShell.</span></span>
3. <span data-ttu-id="ac808-116">Ejecute **Add-AzureAccount** para autenticarse en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac808-116">Run **Add-AzureAccount** to authenticate to your Azure subscription.</span></span> <span data-ttu-id="ac808-117">Cuando se le solicite, escriba el mismo nombre de usuario y contraseña que usó para iniciar sesión en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac808-117">When prompted, enter the same user name and password that you use to sign in to Azure portal.</span></span>  
4. <span data-ttu-id="ac808-118">Ejecute **Get-AzureSubscription** para enumerar las suscripciones asociadas a su cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="ac808-118">Run **Get-AzureSubscription** to list the subscriptions associated with your user account.</span></span> 
5. <span data-ttu-id="ac808-119">Ejecute **Select-AzureSubscription -SubscriptionName &lt;nombre de la suscripción&gt;** o **Select-AzureSubscription -SubscriptionId &lt;ID de la suscripción&gt;** para especificar la suscripción que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="ac808-119">Run **Select-AzureSubscription -SubscriptionName &lt;subscription name&gt;** or **Select-AzureSubscription -SubscriptionId &lt;subscription ID&gt;** to specify the subscription to use.</span></span>

<span data-ttu-id="ac808-120">Enhorabuena, la consola de Azure PowerShell se ha configurado y está lista para usarse.</span><span class="sxs-lookup"><span data-stu-id="ac808-120">Congratulations, your Azure PowerShell console is configured and ready to use.</span></span> <span data-ttu-id="ac808-121">Tenga en cuenta que necesitará repetir los pasos del 2 al 5 cada vez que inicie la consola de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac808-121">Be aware that you'll need to repeate steps 2 through 5 each time you start the the Azure PowerShell console.</span></span>  


## <a name="list-all-collections"></a><span data-ttu-id="ac808-122">Lista de todas las colecciones</span><span class="sxs-lookup"><span data-stu-id="ac808-122">List all collections</span></span>
- - -
     <span data-ttu-id="ac808-123">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="ac808-123">Get-AzureRemoteAppCollection</span></span>

## <a name="delete-a-collection"></a><span data-ttu-id="ac808-124">Eliminación de una colección</span><span class="sxs-lookup"><span data-stu-id="ac808-124">Delete a collection</span></span>
- - -
    <span data-ttu-id="ac808-125">Remove-AzureRemoteAppCollection <enter collection name></span><span class="sxs-lookup"><span data-stu-id="ac808-125">Remove-AzureRemoteAppCollection <enter collection name></span></span>

<span data-ttu-id="ac808-126">Ejemplo: `Remove-AzureRemoteAppCollection ContosoProduction`.</span><span class="sxs-lookup"><span data-stu-id="ac808-126">Example:  `Remove-AzureRemoteAppCollection ContosoProduction`.</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="ac808-127">Creación de una colección en la nube</span><span class="sxs-lookup"><span data-stu-id="ac808-127">Create a cloud collection</span></span>
- - -
<span data-ttu-id="ac808-128">Es sencillo, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ac808-128">It's simple, run the following command:</span></span>

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

<span data-ttu-id="ac808-129">El comando anterior publica automáticamente las aplicaciones de Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio y Word).</span><span class="sxs-lookup"><span data-stu-id="ac808-129">The above command automatically publishes Microsoft Office 365 applications (Excel, OneNote, Outlook, PowerPoint, Visio and Word).</span></span>

<span data-ttu-id="ac808-130">La creación de la colección puede tardar 30 minutos o más en completarse.</span><span class="sxs-lookup"><span data-stu-id="ac808-130">Collection creation can take 30 minutes or longer to complete.</span></span> <span data-ttu-id="ac808-131">Por lo tanto, este comando devuelve un identificador de seguimiento que se puede utilizar como sigue:</span><span class="sxs-lookup"><span data-stu-id="ac808-131">Therefore, this command returns a tracking ID that you can use as follows:</span></span>

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

<span data-ttu-id="ac808-132">Cuando la colección esté lista, puede agregar usuarios a la colección con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ac808-132">After the collection is done, you can add users to the collection with the following command:</span></span>

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

<span data-ttu-id="ac808-133">¡Y ya está!</span><span class="sxs-lookup"><span data-stu-id="ac808-133">And you're done!</span></span> <span data-ttu-id="ac808-134">Ese usuario debería ser capaz de conectarse a la aplicación mediante el cliente de Azure RemoteApp que se encuentra [aquí](https://www.remoteapp.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="ac808-134">That user should be able to connect to the application using the Azure RemoteApp client found [here](https://www.remoteapp.windowsazure.com/).</span></span>

## <a name="available-cmdlets"></a><span data-ttu-id="ac808-135">Cmdlets disponibles</span><span class="sxs-lookup"><span data-stu-id="ac808-135">Available cmdlets</span></span>
<span data-ttu-id="ac808-136">Tenemos muchos otros comandos, cuya información se pondrá pronto a disposición de los usuarios:</span><span class="sxs-lookup"><span data-stu-id="ac808-136">There are lots of other commands that we have, the documentation for them will be coming shortly:</span></span>

<span data-ttu-id="ac808-137">Cmdlets básicos de la colección de RemoteApp</span><span class="sxs-lookup"><span data-stu-id="ac808-137">Basic RemoteApp Collection cmdlets:</span></span> 

* <span data-ttu-id="ac808-138">New-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="ac808-138">New-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="ac808-139">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="ac808-139">Get-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="ac808-140">Set-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="ac808-140">Set-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="ac808-141">Update-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="ac808-141">Update-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="ac808-142">Remove-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="ac808-142">Remove-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="ac808-143">Add-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="ac808-143">Add-AzureRemoteAppUser</span></span>
* <span data-ttu-id="ac808-144">Get-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="ac808-144">Get-AzureRemoteAppUser</span></span>
* <span data-ttu-id="ac808-145">Remove-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="ac808-145">Remove-AzureRemoteAppUser</span></span>
* <span data-ttu-id="ac808-146">Get-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="ac808-146">Get-AzureRemoteAppSession</span></span>
* <span data-ttu-id="ac808-147">Disconnect-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="ac808-147">Disconnect-AzureRemoteAppSession</span></span>
* <span data-ttu-id="ac808-148">Invoke-AzureRemoteAppSessionLogoff</span><span class="sxs-lookup"><span data-stu-id="ac808-148">Invoke-AzureRemoteAppSessionLogoff</span></span>
* <span data-ttu-id="ac808-149">Send-AzureRemoteAppSessionMessage</span><span class="sxs-lookup"><span data-stu-id="ac808-149">Send-AzureRemoteAppSessionMessage</span></span>
* <span data-ttu-id="ac808-150">Get-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="ac808-150">Get-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="ac808-151">Get-AzureRemoteAppStartMenuProgram</span><span class="sxs-lookup"><span data-stu-id="ac808-151">Get-AzureRemoteAppStartMenuProgram</span></span>
* <span data-ttu-id="ac808-152">Publish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="ac808-152">Publish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="ac808-153">Unpublish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="ac808-153">Unpublish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="ac808-154">Get-AzureRemoteAppCollectionUsageDetails</span><span class="sxs-lookup"><span data-stu-id="ac808-154">Get-AzureRemoteAppCollectionUsageDetails</span></span>
* <span data-ttu-id="ac808-155">Get-AzureRemoteAppCollectionUsageSummary</span><span class="sxs-lookup"><span data-stu-id="ac808-155">Get-AzureRemoteAppCollectionUsageSummary</span></span>
* <span data-ttu-id="ac808-156">Get-AzureRemoteAppPlan</span><span class="sxs-lookup"><span data-stu-id="ac808-156">Get-AzureRemoteAppPlan</span></span>

<span data-ttu-id="ac808-157">Cmdlets de red virtual de RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="ac808-157">RemoteApp virtual network cmdlets:</span></span>

* <span data-ttu-id="ac808-158">New-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="ac808-158">New-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="ac808-159">Get-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="ac808-159">Get-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="ac808-160">Set-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="ac808-160">Set-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="ac808-161">Remove-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="ac808-161">Remove-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="ac808-162">Get-AzureRemoteAppVpnDevice</span><span class="sxs-lookup"><span data-stu-id="ac808-162">Get-AzureRemoteAppVpnDevice</span></span>
* <span data-ttu-id="ac808-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span><span class="sxs-lookup"><span data-stu-id="ac808-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span></span>
* <span data-ttu-id="ac808-164">Reset-AzureRemoteAppVpnSharedKey</span><span class="sxs-lookup"><span data-stu-id="ac808-164">Reset-AzureRemoteAppVpnSharedKey</span></span>

<span data-ttu-id="ac808-165">Cmdlets de imagen de plantilla de RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="ac808-165">RemoteApp template image cmdlets:</span></span>

* <span data-ttu-id="ac808-166">New-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="ac808-166">New-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="ac808-167">Get-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="ac808-167">Get-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="ac808-168">Rename-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="ac808-168">Rename-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="ac808-169">Remove-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="ac808-169">Remove-AzureRemoteAppTemplateImage</span></span>

<span data-ttu-id="ac808-170">Otros cmdlets de RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="ac808-170">Other RemoteApp cmdlets:</span></span>

* <span data-ttu-id="ac808-171">Get-AzureRemoteAppLocation</span><span class="sxs-lookup"><span data-stu-id="ac808-171">Get-AzureRemoteAppLocation</span></span>
* <span data-ttu-id="ac808-172">Get-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="ac808-172">Get-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="ac808-173">Set-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="ac808-173">Set-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="ac808-174">Get-AzureRemoteAppOperationResult</span><span class="sxs-lookup"><span data-stu-id="ac808-174">Get-AzureRemoteAppOperationResult</span></span>

