---
title: "Uso del módulo de directivas de Azure Stack | Microsoft Docs"
description: "Aprenda a restringir una suscripción de Azure para que se comporte como una suscripción de Azure Stack"
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
ms.openlocfilehash: 22251dd0428b959069dfc392f4ccdda19b08b9de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-policy-using-the-azure-stack-policy-module"></a><span data-ttu-id="d4b54-103">Administración de la directiva de Azure con el módulo de directivas de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d4b54-103">Manage Azure policy using the Azure Stack Policy Module</span></span>
<span data-ttu-id="d4b54-104">El módulo de directivas de Azure Stack le permite configurar una suscripción de Azure con la misma disponibilidad de servicios y control de versiones que Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="d4b54-104">The Azure Stack Policy module allows you to configure an Azure subscription with the same versioning and service availability as Azure Stack.</span></span>  <span data-ttu-id="d4b54-105">El módulo utiliza el cmdlet **New-AzureRMPolicyAssignment** para crear una directiva de Azure, lo que limita los tipos de recursos y los servicios disponibles en una suscripción.</span><span class="sxs-lookup"><span data-stu-id="d4b54-105">The module uses the **New-AzureRMPolicyAssignment** cmdlet to create an Azure policy, which limits the resource types and services available in a subscription.</span></span>  <span data-ttu-id="d4b54-106">Una vez completado, puede usar su suscripción de Azure para desarrollar aplicaciones destinadas a Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="d4b54-106">Once complete, you can use your Azure subscription to develop apps targeted for Azure Stack.</span></span>  

## <a name="install-the-module"></a><span data-ttu-id="d4b54-107">Instalación del módulo</span><span class="sxs-lookup"><span data-stu-id="d4b54-107">Install the module</span></span>
1. <span data-ttu-id="d4b54-108">Instale la versión requerida del módulo de PowerShell AzureRM, tal y como se describe en el paso 1 de [Instalación de PowerShell para Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="d4b54-108">Install the required version of the AzureRM PowerShell module, as described in Step1 of [Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span>   
2. <span data-ttu-id="d4b54-109">[Descargue las herramientas de Azure Stack desde GitHub](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="d4b54-109">[Download the Azure Stack tools from GitHub](azure-stack-powershell-download.md)</span></span>  
3. <span data-ttu-id="d4b54-110">[Configure PowerShell for use with Azure Stack](azure-stack-powershell-configure-user.md) (Configuración de PowerShell para usarlo con Azure Stack)</span><span class="sxs-lookup"><span data-stu-id="d4b54-110">[Configure PowerShell for use with Azure Stack](azure-stack-powershell-configure-user.md)</span></span>

4. <span data-ttu-id="d4b54-111">Importe el módulo AzureStack.Policy.psm1:</span><span class="sxs-lookup"><span data-stu-id="d4b54-111">Import the AzureStack.Policy.psm1 module:</span></span>

   ```PowerShell
   Import-Module .\Policy\AzureStack.Policy.psm1
   ```

## <a name="apply-policy-to-subscription"></a><span data-ttu-id="d4b54-112">Aplicación de la directiva a la suscripción</span><span class="sxs-lookup"><span data-stu-id="d4b54-112">Apply policy to subscription</span></span>
<span data-ttu-id="d4b54-113">El comando siguiente puede utilizarse para aplicar una directiva predeterminada de Azure Stack con su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4b54-113">The following command can be used to apply a default Azure Stack policy against your Azure subscription.</span></span> <span data-ttu-id="d4b54-114">Antes de ejecutarla, reemplace *Azure Subscription Name* por el nombre de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4b54-114">Before running, replace *Azure Subscription Name* with your Azure subscription.</span></span>

```PowerShell
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
$subscriptionID = $s.Subscription.SubscriptionId
$rgName = 'AzureStack'
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID

```

## <a name="apply-policy-to-a-resource-group"></a><span data-ttu-id="d4b54-115">Aplicación de la directiva a un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="d4b54-115">Apply policy to a resource group</span></span>
<span data-ttu-id="d4b54-116">Puede aplicar las directivas de una forma más específica.</span><span class="sxs-lookup"><span data-stu-id="d4b54-116">You may want to apply policies in a more granular method.</span></span>  <span data-ttu-id="d4b54-117">Por ejemplo, puede tener otros recursos que se ejecuten en la misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="d4b54-117">As an example, you may have other resources running in the same subscription.</span></span>  <span data-ttu-id="d4b54-118">Puede delimitar la aplicación de directivas a un grupo de recursos específico, lo que le permite probar sus aplicaciones para Azure Stack con recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4b54-118">You can scope the policy application to a specific resource group, which lets you test your apps for Azure Stack using Azure resources.</span></span> <span data-ttu-id="d4b54-119">Antes de ejecutarla, reemplace *Azure Subscription Name* por el nombre de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4b54-119">Before running, replace *Azure Subscription Name* with your Azure subscription name.</span></span>

```PowerShell
$resourceGroupName = ‘myRG01’
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID/resourceGroups/$rgName

```

## <a name="policy-in-action"></a><span data-ttu-id="d4b54-120">Directiva en acción</span><span class="sxs-lookup"><span data-stu-id="d4b54-120">Policy in action</span></span>
<span data-ttu-id="d4b54-121">Una vez haya implementado la directiva de Azure, recibe un error al intentar implementar un recurso prohibido por la directiva.</span><span class="sxs-lookup"><span data-stu-id="d4b54-121">Once you've deployed the Azure policy, you receive an error when you try to deploy a resource that prohibited by policy.</span></span>  

![Resultado del error de implementación de un recurso debido a la restricción de la directiva](./media/azure-stack-policy-module/image1.png)

## <a name="next-steps"></a><span data-ttu-id="d4b54-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d4b54-123">Next steps</span></span>
[<span data-ttu-id="d4b54-124">Implementación de plantillas con PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4b54-124">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)

[<span data-ttu-id="d4b54-125">Implementación de plantillas con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="d4b54-125">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="d4b54-126">Implementación de plantillas con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d4b54-126">Deploy Templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)
