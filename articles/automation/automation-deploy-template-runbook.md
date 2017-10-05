---
title: "Implementación de una plantilla de Azure Resource Manager en un runbook de Azure Automation | Microsoft Docs"
description: Procedimiento para implementar una plantilla de Azure Resource Manager almacenada en Azure Storage desde un runbook
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
ms.openlocfilehash: e511eee2f9eac3969b15ad3d45558dc7034f330a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a><span data-ttu-id="42d61-104">Implementación de una plantilla de Azure Resource Manager en un runbook de Azure Automation PowerShell</span><span class="sxs-lookup"><span data-stu-id="42d61-104">Deploy an Azure Resource Manager template in an Azure Automation PowerShell runbook</span></span>

<span data-ttu-id="42d61-105">Puede escribir un [runbook de Azure Automation PowerShell](automation-first-runbook-textual-powershell.md) que implemente un recurso de Azure mediante una [plantilla de Azure Resource Manager](../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="42d61-105">You can write an [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) that deploys an Azure resource by using an [Azure Resource Management template](../azure-resource-manager/resource-manager-create-first-template.md).</span></span>

<span data-ttu-id="42d61-106">Al hacerlo, puede automatizar la implementación de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="42d61-106">By doing this, you can automate deployment of Azure resources.</span></span> <span data-ttu-id="42d61-107">Puede mantener las plantillas de Resource Manager en una ubicación central segura como Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="42d61-107">You can maintain your Resource Manager templates in a central,secure location such as Azure Storage.</span></span>

<span data-ttu-id="42d61-108">En este tema, crearemos un runbook de PowerShell que use una plantilla de Resource Manager almacenada en [Azure Storage](../storage/common/storage-introduction.md) para implementar una nueva cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="42d61-108">In this topic, we create a PowerShell runbook that uses an Resource Manager template stored in [Azure Storage](../storage/common/storage-introduction.md) to deploy a new Azure Storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42d61-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="42d61-109">Prerequisites</span></span>

<span data-ttu-id="42d61-110">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="42d61-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="42d61-111">Suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="42d61-111">Azure subscription.</span></span> <span data-ttu-id="42d61-112">Si aún no tiene ninguna, puede [activar las ventajas de la suscripción a MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o <a href="/pricing/free-account/" target="_blank">[registrarse para obtener una cuenta gratis](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="42d61-112">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="42d61-113">[Cuenta de Automatización](automation-sec-configure-azure-runas-account.md) para contener el Runbook y autenticarse en recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="42d61-113">[Automation account](automation-sec-configure-azure-runas-account.md) to hold the runbook and authenticate to Azure resources.</span></span>  <span data-ttu-id="42d61-114">Esta cuenta debe tener permiso para iniciar y detener la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="42d61-114">This account must have permission to start and stop the virtual machine.</span></span>
* <span data-ttu-id="42d61-115">[Cuenta de Azure Storage](../storage/common/storage-create-storage-account.md) donde se va a almacenar la plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="42d61-115">[Azure Storage account](../storage/common/storage-create-storage-account.md) in which to store the Resource Manager template</span></span>
* <span data-ttu-id="42d61-116">Azure Powershell instalado en una máquina local.</span><span class="sxs-lookup"><span data-stu-id="42d61-116">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="42d61-117">Consulte [Instalación y configuración de Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) para información sobre cómo obtener Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="42d61-117">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how to get Azure PowerShell.</span></span>

## <a name="create-the-resource-manager-template"></a><span data-ttu-id="42d61-118">Creación de la plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="42d61-118">Create the Resource Manager template</span></span>

<span data-ttu-id="42d61-119">En este ejemplo, utilizamos una plantilla de Resource Manager que implementa una nueva cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="42d61-119">For this example, we use an Resource Manager template that deploys a new Azure Storage account.</span></span>

<span data-ttu-id="42d61-120">En un editor de texto, copie el texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="42d61-120">In a text editor, copy the following text:</span></span>

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

<span data-ttu-id="42d61-121">Guarde el archivo localmente como `TemplateTest.json`.</span><span class="sxs-lookup"><span data-stu-id="42d61-121">Save the file locally as `TemplateTest.json`.</span></span>

## <a name="save-the-resource-manager-template-in-azure-storage"></a><span data-ttu-id="42d61-122">Guarde la plantilla de Resource Manager en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="42d61-122">Save the Resource Manager template in Azure Storage</span></span>

<span data-ttu-id="42d61-123">Ahora, usaremos PowerShell para crear un recurso compartido de archivos de Azure Storage y cargaremos el archivo `TemplateTest.json`.</span><span class="sxs-lookup"><span data-stu-id="42d61-123">Now we use PowerShell to create an Azure Storage file share and upload the `TemplateTest.json` file.</span></span>
<span data-ttu-id="42d61-124">Para obtener instrucciones sobre cómo crear un recurso compartido de archivos y cargar un archivo en Azure Portal, consulte [Introducción a Azure File Storage en Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="42d61-124">For instructions on how to create a file share and upload a file in the Azure portal, see [Get started with Azure File storage on Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="42d61-125">Inicie PowerShell en la máquina local y ejecute los comandos siguientes para crear un recurso compartido de archivos y cargar la plantilla de Resource Manager en él.</span><span class="sxs-lookup"><span data-stu-id="42d61-125">Launch PowerShell on your local machine, and run the following commands to create a file share and upload the Resource Manager template to that file share.</span></span>

```powershell
# Login to Azure
Login-AzureRmAccount

# Get the access key for your storage account
$key = Get-AzureRmStorageAccountKey -ResourceGroupName 'MyAzureAccount' -Name 'MyStorageAccount'

# Create an Azure Storage context using the first access key
$context = New-AzureStorageContext -StorageAccountName 'MyStorageAccount' -StorageAccountKey $key[0].value

# Create a file share named 'resource-templates' in your Azure Storage account
$fileShare = New-AzureStorageShare -Name 'resource-templates' -Context $context

# Add the TemplateTest.json file to the new file share
# "TemplatePath" is the path where you saved the TemplateTest.json file
$templateFile = 'C:\TemplatePath'
Set-AzureStorageFileContent -ShareName $fileShare.Name -Context $context -Source $templateFile
```

## <a name="create-the-powershell-runbook-script"></a><span data-ttu-id="42d61-126">Creación del script del runbook de PowerShell</span><span class="sxs-lookup"><span data-stu-id="42d61-126">Create the PowerShell runbook script</span></span>

<span data-ttu-id="42d61-127">Ahora crearemos un script de PowerShell que obtenga el archivo `TemplateTest.json` desde Azure Storage e implemente la plantilla para crear una nueva cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="42d61-127">Now we create a PowerShell script that gets the `TemplateTest.json` file from Azure Storage and deploys the template to create a new Azure Storage account.</span></span>

<span data-ttu-id="42d61-128">En un editor de texto, pegue el texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="42d61-128">In a text editor, paste the following text:</span></span>

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



# Authenticate to Azure if running from Azure Automation
$ServicePrincipalConnection = Get-AutomationConnection -Name "AzureRunAsConnection"
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $ServicePrincipalConnection.TenantId `
    -ApplicationId $ServicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $ServicePrincipalConnection.CertificateThumbprint | Write-Verbose

#Set the parameter values for the Resource Manager template
$Parameters = @{
    "storageAccountType"="Standard_LRS"
    }

# Create a new context
$Context = New-AzureStorageContext -StorageAccountKey $StorageAccountKey

Get-AzureStorageFileContent -ShareName 'resource-templates' -Context $Context -path 'TemplateTest.json' -Destination 'C:\Temp'

$TemplateFile = Join-Path -Path 'C:\Temp' -ChildPath $StorageFileName

# Deploy the storage account
New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFile -TemplateParameterObject $Parameters 
``` 

<span data-ttu-id="42d61-129">Guarde el archivo localmente como `DeployTemplate.ps1`.</span><span class="sxs-lookup"><span data-stu-id="42d61-129">Save the file locally as `DeployTemplate.ps1`.</span></span>

## <a name="import-and-publish-the-runbook-into-your-azure-automation-account"></a><span data-ttu-id="42d61-130">Importación y publicación del runbook en su cuenta de Azure Automation</span><span class="sxs-lookup"><span data-stu-id="42d61-130">Import and publish the runbook into your Azure Automation account</span></span>

<span data-ttu-id="42d61-131">Ahora usaremos PowerShell para importar el runbook en su cuenta de Azure Automation y, a continuación, publicaremos el runbook.</span><span class="sxs-lookup"><span data-stu-id="42d61-131">Now we use PowerShell to import the runbook into your Azure Automation account, and then publish the runbook.</span></span>
<span data-ttu-id="42d61-132">Para obtener información acerca de cómo importar y publicar un runbook en Azure Portal, consulte [Creación o importación de un runbook en Azure Automation](automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="42d61-132">For information about how to import and publish a runbook in the Azure portal, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md).</span></span>

<span data-ttu-id="42d61-133">Para importar `DeployTemplate.ps1` en su cuenta de Automation como un runbook de PowerShell, ejecute los siguientes comandos de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="42d61-133">To import `DeployTemplate.ps1` into your Automation account as a PowerShell runbook, run the following PowerShell commands:</span></span>

```powershell
# MyPath is the path where you saved DeployTemplate.ps1
# MyResourceGroup is the name of the Azure ResourceGroup that contains your Azure Automation account
# MyAutomationAccount is the name of your Automation account
$importParams = @{
    Path = 'C:\MyPath\DeployTemplate.ps1'
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Type = 'PowerShell'
}
Import-AzureRmAutomationRunbook @

# Publish the runbook
$publishParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
}
Publish-AzureRmAutomationRunbook @publishParams
```

## <a name="start-the-runbook"></a><span data-ttu-id="42d61-134">Inicio del runbook</span><span class="sxs-lookup"><span data-stu-id="42d61-134">Start the runbook</span></span>

<span data-ttu-id="42d61-135">Ahora iniciaremos el runbook llamando al cmdlet [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0).</span><span class="sxs-lookup"><span data-stu-id="42d61-135">Now we start the runbook by calling the [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span></span>

<span data-ttu-id="42d61-136">Para obtener información acerca de cómo iniciar un runbook en Azure Portal, consulte [Inicio de un runbook en Azure Automation](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="42d61-136">For information about how to start a runbook in the Azure portal, see [Starting a runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>

<span data-ttu-id="42d61-137">Ejecute los siguientes comandos en la consola de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="42d61-137">Run the following commands in the PowerShell console:</span></span>

```powershell
# Set up the parameters for the runbook
$runbookParams = @{
    ResourceGroupName = 'MyResourceGroup'
    StorageAccountName = 'MyStorageAccount'
    StorageAccountKey = $key[0].Value # We got this key earlier
    StorageFileName = 'TemplateTest.json' 
}

# Set up parameters for the Start-AzureRmAutomationRunbook cmdlet
$startParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
    Parameters = $runbookParams
}

# Start the runbook
$job = Start-AzureRmAutomationRunbook @startParams
```

<span data-ttu-id="42d61-138">Se ejecuta el runbook y puede comprobar su estado ejecutando `$job.Status`.</span><span class="sxs-lookup"><span data-stu-id="42d61-138">The runbook runs, and you can check its status by running `$job.Status`.</span></span>

<span data-ttu-id="42d61-139">El runbook obtiene la plantilla de Resource Manager y la utiliza para implementar una nueva cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="42d61-139">The runbook gets the Resource Manager template and uses it to deploy a new Azure Storage account.</span></span>
<span data-ttu-id="42d61-140">Puede ver que se ha creado la nueva cuenta de almacenamiento ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="42d61-140">You can see that the new storage account was created by running the following command:</span></span>
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a><span data-ttu-id="42d61-141">Resumen</span><span class="sxs-lookup"><span data-stu-id="42d61-141">Summary</span></span>

<span data-ttu-id="42d61-142">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="42d61-142">That's it!</span></span> <span data-ttu-id="42d61-143">Ahora puede usar las plantillas de Resource Manager, Azure Automation y Azure Storage para implementar todos los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="42d61-143">Now you can use Azure Automation and Azure Storage, and Resource Manager templates to deploy all your Azure resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42d61-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="42d61-144">Next steps</span></span>

* <span data-ttu-id="42d61-145">Para más información sobre las plantillas de Resource Manager, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="42d61-145">To learn more about Resource Manager templates, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="42d61-146">Para empezar a trabajar con Azure Storage, consulte [Introducción a Azure Storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="42d61-146">To get started with Azure Storage, see [Introduction to Azure Storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="42d61-147">Para encontrar otros runbooks útiles de Azure Automation, consulte [Galerías de módulos y runbooks de Azure Automation](automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="42d61-147">To find other useful Azure Automation runbooks, see [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>
* <span data-ttu-id="42d61-148">Para encontrar otras plantillas útiles de Resource Manager, consulte [Plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/).</span><span class="sxs-lookup"><span data-stu-id="42d61-148">To find other useful Resource Manager templates, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/)</span></span>

