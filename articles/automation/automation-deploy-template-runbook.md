---
title: "aaaDeploy una plantilla de Azure Resource Manager en un runbook de automatización de Azure | Documentos de Microsoft"
description: "¿Cómo toodeploy una plantilla de Azure Resource Manager almacenados en el almacenamiento de Azure desde un runbook"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: powershell, runbook, json, azure automation
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 07/09/2017
ms.author: eslesar
ms.openlocfilehash: f489a8e8635a48f5a6a2f1a88e1c803f56f01832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a><span data-ttu-id="d667e-104">Implementación de una plantilla de Azure Resource Manager en un runbook de Azure Automation PowerShell</span><span class="sxs-lookup"><span data-stu-id="d667e-104">Deploy an Azure Resource Manager template in an Azure Automation PowerShell runbook</span></span>

<span data-ttu-id="d667e-105">Puede escribir un [runbook de Azure Automation PowerShell](automation-first-runbook-textual-powershell.md) que implemente un recurso de Azure mediante una [plantilla de Azure Resource Manager](../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="d667e-105">You can write an [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) that deploys an Azure resource by using an [Azure Resource Management template](../azure-resource-manager/resource-manager-create-first-template.md).</span></span>

<span data-ttu-id="d667e-106">Al hacerlo, puede automatizar la implementación de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d667e-106">By doing this, you can automate deployment of Azure resources.</span></span> <span data-ttu-id="d667e-107">Puede mantener las plantillas de Resource Manager en una ubicación central segura como Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d667e-107">You can maintain your Resource Manager templates in a central,secure location such as Azure Storage.</span></span>

<span data-ttu-id="d667e-108">En este tema, crearemos un runbook de PowerShell que usa una plantilla de administrador de recursos almacenada en [el almacenamiento de Azure](../storage/common/storage-introduction.md) toodeploy una nueva cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="d667e-108">In this topic, we create a PowerShell runbook that uses an Resource Manager template stored in [Azure Storage](../storage/common/storage-introduction.md) toodeploy a new Azure Storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d667e-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d667e-109">Prerequisites</span></span>

<span data-ttu-id="d667e-110">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="d667e-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="d667e-111">Suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d667e-111">Azure subscription.</span></span> <span data-ttu-id="d667e-112">Si aún no tiene ninguna, puede [activar las ventajas de la suscripción a MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o <a href="/pricing/free-account/" target="_blank">[registrarse para obtener una cuenta gratis](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="d667e-112">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="d667e-113">[Cuenta de automatización](automation-sec-configure-azure-runas-account.md) toohold Hola runbook y autenticar tooAzure recursos.</span><span class="sxs-lookup"><span data-stu-id="d667e-113">[Automation account](automation-sec-configure-azure-runas-account.md) toohold hello runbook and authenticate tooAzure resources.</span></span>  <span data-ttu-id="d667e-114">Esta cuenta debe tener permiso toostart y detener la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="d667e-114">This account must have permission toostart and stop hello virtual machine.</span></span>
* <span data-ttu-id="d667e-115">[Cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md) en qué plantilla de administrador de recursos de hello toostore</span><span class="sxs-lookup"><span data-stu-id="d667e-115">[Azure Storage account](../storage/common/storage-create-storage-account.md) in which toostore hello Resource Manager template</span></span>
* <span data-ttu-id="d667e-116">Azure Powershell instalado en una máquina local.</span><span class="sxs-lookup"><span data-stu-id="d667e-116">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="d667e-117">Vea [instalar y configurar Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) para obtener información acerca de cómo tooget PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="d667e-117">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how tooget Azure PowerShell.</span></span>

## <a name="create-hello-resource-manager-template"></a><span data-ttu-id="d667e-118">Crear plantilla de administrador de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="d667e-118">Create hello Resource Manager template</span></span>

<span data-ttu-id="d667e-119">En este ejemplo, utilizamos una plantilla de Resource Manager que implementa una nueva cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d667e-119">For this example, we use an Resource Manager template that deploys a new Azure Storage account.</span></span>

<span data-ttu-id="d667e-120">En un editor de texto, copie Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="d667e-120">In a text editor, copy hello following text:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

<span data-ttu-id="d667e-121">Guardar archivo de hello localmente como `TemplateTest.json`.</span><span class="sxs-lookup"><span data-stu-id="d667e-121">Save hello file locally as `TemplateTest.json`.</span></span>

## <a name="save-hello-resource-manager-template-in-azure-storage"></a><span data-ttu-id="d667e-122">Guarde la plantilla de administrador de recursos de hello en el almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="d667e-122">Save hello Resource Manager template in Azure Storage</span></span>

<span data-ttu-id="d667e-123">Ahora se usa PowerShell toocreate un recurso compartido de archivos de almacenamiento de Azure y cargar hello `TemplateTest.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="d667e-123">Now we use PowerShell toocreate an Azure Storage file share and upload hello `TemplateTest.json` file.</span></span>
<span data-ttu-id="d667e-124">Para obtener instrucciones sobre cómo toocreate un archivo de recurso compartido y cargar un archivo en hello portal de Azure, consulte [Introducción al almacenamiento de archivos de Azure en Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="d667e-124">For instructions on how toocreate a file share and upload a file in hello Azure portal, see [Get started with Azure File storage on Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="d667e-125">Inicie PowerShell en el equipo local y ejecute hello después toocreate un recurso compartido de archivos de comandos y cargar el recurso compartido de archivos de toothat de plantilla del Administrador de recursos Hola.</span><span class="sxs-lookup"><span data-stu-id="d667e-125">Launch PowerShell on your local machine, and run hello following commands toocreate a file share and upload hello Resource Manager template toothat file share.</span></span>

```powershell
# Login tooAzure
Login-AzureRmAccount

# Get hello access key for your storage account
$key = Get-AzureRmStorageAccountKey -ResourceGroupName 'MyAzureAccount' -Name 'MyStorageAccount'

# Create an Azure Storage context using hello first access key
$context = New-AzureStorageContext -StorageAccountName 'MyStorageAccount' -StorageAccountKey $key[0].value

# Create a file share named 'resource-templates' in your Azure Storage account
$fileShare = New-AzureStorageShare -Name 'resource-templates' -Context $context

# Add hello TemplateTest.json file toohello new file share
# "TemplatePath" is hello path where you saved hello TemplateTest.json file
$templateFile = 'C:\TemplatePath'
Set-AzureStorageFileContent -ShareName $fileShare.Name -Context $context -Source $templateFile
```

## <a name="create-hello-powershell-runbook-script"></a><span data-ttu-id="d667e-126">Crear script de runbook de PowerShell de Hola</span><span class="sxs-lookup"><span data-stu-id="d667e-126">Create hello PowerShell runbook script</span></span>

<span data-ttu-id="d667e-127">Ahora es crear un script de PowerShell que obtiene hello `TemplateTest.json` de archivos desde el almacenamiento de Azure e implementa Hola plantilla toocreate una nueva cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="d667e-127">Now we create a PowerShell script that gets hello `TemplateTest.json` file from Azure Storage and deploys hello template toocreate a new Azure Storage account.</span></span>

<span data-ttu-id="d667e-128">En un editor de texto, pegue Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="d667e-128">In a text editor, paste hello following text:</span></span>

```powershell
param (
    [Parameter(Mandatory=$true)]
    [string]
    $ResourceGroupName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountKey,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageFileName
)



# Authenticate tooAzure if running from Azure Automation
$ServicePrincipalConnection = Get-AutomationConnection -Name "AzureRunAsConnection"
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $ServicePrincipalConnection.TenantId `
    -ApplicationId $ServicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $ServicePrincipalConnection.CertificateThumbprint | Write-Verbose

#Set hello parameter values for hello Resource Manager template
$Parameters = @{
    "storageAccountType"="Standard_LRS"
    }

# Create a new context
$Context = New-AzureStorageContext -StorageAccountKey $StorageAccountKey

Get-AzureStorageFileContent -ShareName 'resource-templates' -Context $Context -path 'TemplateTest.json' -Destination 'C:\Temp'

$TemplateFile = Join-Path -Path 'C:\Temp' -ChildPath $StorageFileName

# Deploy hello storage account
New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFile -TemplateParameterObject $Parameters 
``` 

<span data-ttu-id="d667e-129">Guardar archivo de hello localmente como `DeployTemplate.ps1`.</span><span class="sxs-lookup"><span data-stu-id="d667e-129">Save hello file locally as `DeployTemplate.ps1`.</span></span>

## <a name="import-and-publish-hello-runbook-into-your-azure-automation-account"></a><span data-ttu-id="d667e-130">Importar y publicar el runbook de hello en su cuenta de automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="d667e-130">Import and publish hello runbook into your Azure Automation account</span></span>

<span data-ttu-id="d667e-131">Ahora se usa PowerShell tooimport Hola runbook en su cuenta de automatización de Azure y, a continuación, publicar el runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="d667e-131">Now we use PowerShell tooimport hello runbook into your Azure Automation account, and then publish hello runbook.</span></span>
<span data-ttu-id="d667e-132">Para obtener información acerca de cómo tooimport y publicar un runbook en hello portal de Azure, consulte [crear o importar un runbook en automatización de Azure](automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="d667e-132">For information about how tooimport and publish a runbook in hello Azure portal, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md).</span></span>

<span data-ttu-id="d667e-133">tooimport `DeployTemplate.ps1` en su cuenta de automatización como un runbook de PowerShell, ejecute hello siga los comandos de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d667e-133">tooimport `DeployTemplate.ps1` into your Automation account as a PowerShell runbook, run hello following PowerShell commands:</span></span>

```powershell
# MyPath is hello path where you saved DeployTemplate.ps1
# MyResourceGroup is hello name of hello Azure ResourceGroup that contains your Azure Automation account
# MyAutomationAccount is hello name of your Automation account
$importParams = @{
    Path = 'C:\MyPath\DeployTemplate.ps1'
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Type = 'PowerShell'
}
Import-AzureRmAutomationRunbook @

# Publish hello runbook
$publishParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
}
Publish-AzureRmAutomationRunbook @publishParams
```

## <a name="start-hello-runbook"></a><span data-ttu-id="d667e-134">Iniciar runbook Hola</span><span class="sxs-lookup"><span data-stu-id="d667e-134">Start hello runbook</span></span>

<span data-ttu-id="d667e-135">Ahora se inicia runbook Hola Hola que realiza la llamada [AzureRmAutomationRunbook inicio](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d667e-135">Now we start hello runbook by calling hello [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span></span>

<span data-ttu-id="d667e-136">Para obtener información acerca de cómo toostart un runbook en hello portal de Azure, consulte [a partir de un runbook en automatización de Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="d667e-136">For information about how toostart a runbook in hello Azure portal, see [Starting a runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>

<span data-ttu-id="d667e-137">Ejecute hello siga los comandos en la consola de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="d667e-137">Run hello following commands in hello PowerShell console:</span></span>

```powershell
# Set up hello parameters for hello runbook
$runbookParams = @{
    ResourceGroupName = 'MyResourceGroup'
    StorageAccountName = 'MyStorageAccount'
    StorageAccountKey = $key[0].Value # We got this key earlier
    StorageFileName = 'TemplateTest.json' 
}

# Set up parameters for hello Start-AzureRmAutomationRunbook cmdlet
$startParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
    Parameters = $runbookParams
}

# Start hello runbook
$job = Start-AzureRmAutomationRunbook @startParams
```

<span data-ttu-id="d667e-138">Hola se ejecuta runbook, y puede comprobar su estado mediante la ejecución de `$job.Status`.</span><span class="sxs-lookup"><span data-stu-id="d667e-138">hello runbook runs, and you can check its status by running `$job.Status`.</span></span>

<span data-ttu-id="d667e-139">Hola runbook Obtiene la plantilla de administrador de recursos de Hola y utiliza toodeploy una nueva cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="d667e-139">hello runbook gets hello Resource Manager template and uses it toodeploy a new Azure Storage account.</span></span>
<span data-ttu-id="d667e-140">Puede ver que se ha creado la nueva cuenta de almacenamiento Hola ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="d667e-140">You can see that hello new storage account was created by running hello following command:</span></span>
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a><span data-ttu-id="d667e-141">Resumen</span><span class="sxs-lookup"><span data-stu-id="d667e-141">Summary</span></span>

<span data-ttu-id="d667e-142">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="d667e-142">That's it!</span></span> <span data-ttu-id="d667e-143">Ahora puede usar Automatización de Azure y almacenamiento de Azure y el Administrador de recursos plantillas toodeploy todos los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d667e-143">Now you can use Azure Automation and Azure Storage, and Resource Manager templates toodeploy all your Azure resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d667e-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d667e-144">Next steps</span></span>

* <span data-ttu-id="d667e-145">toolearn más acerca de las plantillas de administrador de recursos, consulte [Introducción al administrador de recursos de Azure](../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d667e-145">toolearn more about Resource Manager templates, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="d667e-146">tooget a trabajar con el almacenamiento de Azure, consulte [Introducción tooAzure almacenamiento](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d667e-146">tooget started with Azure Storage, see [Introduction tooAzure Storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="d667e-147">toofind otros útiles runbooks de automatización de Azure, consulte [galerías de módulos y runbooks de automatización de Azure](automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="d667e-147">toofind other useful Azure Automation runbooks, see [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>
* <span data-ttu-id="d667e-148">toofind otras plantillas de administrador de recursos útiles, vea [plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/)</span><span class="sxs-lookup"><span data-stu-id="d667e-148">toofind other useful Resource Manager templates, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/)</span></span>

