---
title: 'Ejemplo de Script de PowerShell: aaaAzure implementar plantilla | Documentos de Microsoft'
description: Script de ejemplo para implementar una plantilla de Azure Resource Manager.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 536b8ccecad4ed8a4c4a4139c6bf4600e2eb9405
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-deployment---powershell-script"></a><span data-ttu-id="1e9de-103">Implementación de plantillas de Azure Resource Manager: script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e9de-103">Azure Resource Manager template deployment - PowerShell script</span></span>

<span data-ttu-id="1e9de-104">Este script implementa un grupo de recursos de tooa de plantilla de administrador de recursos en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="1e9de-104">This script deploys a Resource Manager template tooa resource group in your subscription.</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1e9de-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1e9de-105">Sample script</span></span>

```powershell
<#
 .SYNOPSIS
    Deploys a template tooAzure

 .DESCRIPTION
    Deploys an Azure Resource Manager template
#>

param (
    [Parameter(Mandatory)]
    #hello subscription id where hello template will be deployed.
    [string]$SubscriptionId,  

    [Parameter(Mandatory)]
    #hello resource group where hello template will be deployed. Can be hello name of an existing or a new resource group.
    [string]$ResourceGroupName, 

    #Optional, a resource group location. If specified, will try toocreate a new resource group in this location. If not specified, assumes resource group is existing.
    [string]$ResourceGroupLocation, 

    #hello deployment name.
    [Parameter(Mandatory)]
    [string]$DeploymentName,    

    #Path toohello template file. Defaults tootemplate.json.
    [string]$TemplateFilePath = "template.json",  

    #Path toohello parameters file. Defaults tooparameters.json. If file is not found, will prompt for parameter values based on template.
    [string]$ParametersFilePath = "parameters.json"
)

$ErrorActionPreference = "Stop"

# Login tooAzure and select subscription
Write-Output "Logging in"
Login-AzureRmAccount
Write-Output "Selecting subscription '$SubscriptionId'"
Select-AzureRmSubscription -SubscriptionID $SubscriptionId

# Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $ResourceGroupName -ErrorAction SilentlyContinue
if ( -not $ResourceGroup ) {
    Write-Output "Could not find resource group '$ResourceGroupName' - will create it"
    if ( -not $ResourceGroupLocation ) {
        $ResourceGroupLocation = Read-Host -Prompt 'Enter location for resource group'
    }
    Write-Output "Creating resource group '$ResourceGroupName' in location '$ResourceGroupLocation'"
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else {
    Write-Output "Using existing resource group '$ResourceGroupName'"
}

# Start hello deployment
Write-Output "Starting deployment"
if ( Test-Path $ParametersFilePath ) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath -TemplateParameterFile $ParametersFilePath
}
else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath
}
``` 

## <a name="clean-up-deployment"></a><span data-ttu-id="1e9de-106">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="1e9de-106">Clean up deployment</span></span> 

<span data-ttu-id="1e9de-107">Siguiente ejecución Hola comandos tooremove grupo de recursos de Hola y todos sus recursos.</span><span class="sxs-lookup"><span data-stu-id="1e9de-107">Run hello following command tooremove hello resource group and all its resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1e9de-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="1e9de-108">Script explanation</span></span>

<span data-ttu-id="1e9de-109">Este script utiliza Hola después de la implementación de comandos toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="1e9de-109">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="1e9de-110">Cada elemento de la documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="1e9de-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1e9de-111">Comando</span><span class="sxs-lookup"><span data-stu-id="1e9de-111">Command</span></span> | <span data-ttu-id="1e9de-112">Notas</span><span class="sxs-lookup"><span data-stu-id="1e9de-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1e9de-113">Register-AzureRmResourceProvider</span><span class="sxs-lookup"><span data-stu-id="1e9de-113">Register-AzureRmResourceProvider</span></span>](/powershell/module/azurerm.resources/register-azurermresourceprovider) | <span data-ttu-id="1e9de-114">Registra un proveedor de recursos para que sus tipos de recursos pueden ser implementado tooyour suscripción.</span><span class="sxs-lookup"><span data-stu-id="1e9de-114">Registers a resource provider so its resource types can be deployed tooyour subscription.</span></span>  |
| [<span data-ttu-id="1e9de-115">Get-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1e9de-115">Get-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | <span data-ttu-id="1e9de-116">Obtiene los grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="1e9de-116">Gets resource groups.</span></span>  |
| [<span data-ttu-id="1e9de-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1e9de-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="1e9de-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="1e9de-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1e9de-119">New-AzureRmResourceGroupDeployment</span><span class="sxs-lookup"><span data-stu-id="1e9de-119">New-AzureRmResourceGroupDeployment</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) | <span data-ttu-id="1e9de-120">Agrega un grupo de recursos de tooa de implementación de Azure.</span><span class="sxs-lookup"><span data-stu-id="1e9de-120">Adds an Azure deployment tooa resource group.</span></span>  |
| [<span data-ttu-id="1e9de-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1e9de-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="1e9de-122">Quita un grupo de recursos y todos los recursos incluidos en él.</span><span class="sxs-lookup"><span data-stu-id="1e9de-122">Removes a resource group and all resources contained within.</span></span> |



## <a name="next-steps"></a><span data-ttu-id="1e9de-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1e9de-123">Next steps</span></span>
* <span data-ttu-id="1e9de-124">Para una plantilla de toodeploying introducción, consulte [implementar los recursos con plantillas de administrador de recursos y Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="1e9de-124">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="1e9de-125">Para más información sobre la implementación de una plantilla que requiere un token de SAS, vea [Implementación de una plantilla privada con el token de SAS](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="1e9de-125">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="1e9de-126">toodefine parámetros de plantilla, vea [crear plantillas](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="1e9de-126">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="1e9de-127">Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="1e9de-127">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

