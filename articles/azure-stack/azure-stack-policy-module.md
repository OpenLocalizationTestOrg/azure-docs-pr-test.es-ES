---
title: "Hola aaaUse módulo de directivas de pila de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconstrain una toobehave de suscripción de Azure como una suscripción de la pila de Azure"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 937ef34f-14d4-4ea9-960b-362ba986f000
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/28/2017
ms.author: helaw
ms.openlocfilehash: a9d01b759d7c4a248f727de682a71a7655ed12d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-policy-using-hello-azure-stack-policy-module"></a><span data-ttu-id="0f55d-103">Administrar la directiva de Azure mediante Hola módulo de directivas de pila de Azure</span><span class="sxs-lookup"><span data-stu-id="0f55d-103">Manage Azure policy using hello Azure Stack Policy Module</span></span>
<span data-ttu-id="0f55d-104">módulo de directivas de la pila de Azure de Hello permite tooconfigure una suscripción de Azure con hello mismo control de versiones y el servicio de disponibilidad como la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="0f55d-104">hello Azure Stack Policy module allows you tooconfigure an Azure subscription with hello same versioning and service availability as Azure Stack.</span></span>  <span data-ttu-id="0f55d-105">módulo de Hello usa hello **AzureRMPolicyAssignment New** cmdlet toocreate una directiva de Azure, que limita los tipos de recursos de Hola y de servicios disponibles en una suscripción.</span><span class="sxs-lookup"><span data-stu-id="0f55d-105">hello module uses hello **New-AzureRMPolicyAssignment** cmdlet toocreate an Azure policy, which limits hello resource types and services available in a subscription.</span></span>  <span data-ttu-id="0f55d-106">Una vez completado, puede usar las aplicaciones de toodevelop de suscripción de Azure destinadas a la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="0f55d-106">Once complete, you can use your Azure subscription toodevelop apps targeted for Azure Stack.</span></span>  

## <a name="install-hello-module"></a><span data-ttu-id="0f55d-107">Instalar el módulo de Hola</span><span class="sxs-lookup"><span data-stu-id="0f55d-107">Install hello module</span></span>
1. <span data-ttu-id="0f55d-108">Instalar versión requerida de Hola de hello AzureRM PowerShell módulo, como se describe en el paso 1 de [instale PowerShell para Azure pila](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="0f55d-108">Install hello required version of hello AzureRM PowerShell module, as described in Step1 of [Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span>   
2. [<span data-ttu-id="0f55d-109">Descargar herramientas de Azure pila Hola desde GitHub</span><span class="sxs-lookup"><span data-stu-id="0f55d-109">Download hello Azure Stack tools from GitHub</span></span>](azure-stack-powershell-download.md)  
3. <span data-ttu-id="0f55d-110">[Configure PowerShell for use with Azure Stack](azure-stack-powershell-configure-user.md) (Configuración de PowerShell para usarlo con Azure Stack)</span><span class="sxs-lookup"><span data-stu-id="0f55d-110">[Configure PowerShell for use with Azure Stack](azure-stack-powershell-configure-user.md)</span></span>

4. <span data-ttu-id="0f55d-111">Importe el módulo de Hola AzureStack.Policy.psm1:</span><span class="sxs-lookup"><span data-stu-id="0f55d-111">Import hello AzureStack.Policy.psm1 module:</span></span>

   ```PowerShell
   Import-Module .\Policy\AzureStack.Policy.psm1
   ```

## <a name="apply-policy-toosubscription"></a><span data-ttu-id="0f55d-112">Aplicar directiva toosubscription</span><span class="sxs-lookup"><span data-stu-id="0f55d-112">Apply policy toosubscription</span></span>
<span data-ttu-id="0f55d-113">Hola siguiente comando puede ser tooapply usa una directiva predeterminada de la pila de Azure con su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="0f55d-113">hello following command can be used tooapply a default Azure Stack policy against your Azure subscription.</span></span> <span data-ttu-id="0f55d-114">Antes de ejecutarla, reemplace *Azure Subscription Name* por el nombre de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="0f55d-114">Before running, replace *Azure Subscription Name* with your Azure subscription.</span></span>

```PowerShell
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
$subscriptionID = $s.Subscription.SubscriptionId
$rgName = 'AzureStack'
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID

```

## <a name="apply-policy-tooa-resource-group"></a><span data-ttu-id="0f55d-115">Aplicar el grupo de recursos de tooa de directiva</span><span class="sxs-lookup"><span data-stu-id="0f55d-115">Apply policy tooa resource group</span></span>
<span data-ttu-id="0f55d-116">Puede que desee tooapply directivas en un método más granular.</span><span class="sxs-lookup"><span data-stu-id="0f55d-116">You may want tooapply policies in a more granular method.</span></span>  <span data-ttu-id="0f55d-117">Por ejemplo, puede tener otros recursos que se ejecutan en hello misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="0f55d-117">As an example, you may have other resources running in hello same subscription.</span></span>  <span data-ttu-id="0f55d-118">Puede establecer el ámbito de hello directiva aplicación tooa grupo de recursos específico, lo que le permite probar sus aplicaciones para la pila de Azure con recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="0f55d-118">You can scope hello policy application tooa specific resource group, which lets you test your apps for Azure Stack using Azure resources.</span></span> <span data-ttu-id="0f55d-119">Antes de ejecutarla, reemplace *Azure Subscription Name* por el nombre de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="0f55d-119">Before running, replace *Azure Subscription Name* with your Azure subscription name.</span></span>

```PowerShell
$resourceGroupName = ‘myRG01’
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID/resourceGroups/$rgName

```

## <a name="policy-in-action"></a><span data-ttu-id="0f55d-120">Directiva en acción</span><span class="sxs-lookup"><span data-stu-id="0f55d-120">Policy in action</span></span>
<span data-ttu-id="0f55d-121">Una vez haya implementado Hola directiva de Azure, recibirá un error cuando intente toodeploy un recurso que prohibido por la directiva.</span><span class="sxs-lookup"><span data-stu-id="0f55d-121">Once you've deployed hello Azure policy, you receive an error when you try toodeploy a resource that prohibited by policy.</span></span>  

![Resultado del error de implementación de un recurso debido a la restricción de la directiva](./media/azure-stack-policy-module/image1.png)

## <a name="next-steps"></a><span data-ttu-id="0f55d-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0f55d-123">Next steps</span></span>
[<span data-ttu-id="0f55d-124">Implementación de plantillas con PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f55d-124">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)

[<span data-ttu-id="0f55d-125">Implementación de plantillas con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="0f55d-125">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="0f55d-126">Implementación de plantillas con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0f55d-126">Deploy Templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)
