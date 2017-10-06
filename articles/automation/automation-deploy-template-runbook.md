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
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a>Implementación de una plantilla de Azure Resource Manager en un runbook de Azure Automation PowerShell

Puede escribir un [runbook de Azure Automation PowerShell](automation-first-runbook-textual-powershell.md) que implemente un recurso de Azure mediante una [plantilla de Azure Resource Manager](../azure-resource-manager/resource-manager-create-first-template.md).

Al hacerlo, puede automatizar la implementación de los recursos de Azure. Puede mantener las plantillas de Resource Manager en una ubicación central segura como Azure Storage.

En este tema, crearemos un runbook de PowerShell que usa una plantilla de administrador de recursos almacenada en [el almacenamiento de Azure](../storage/common/storage-introduction.md) toodeploy una nueva cuenta de almacenamiento de Azure.

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial, necesita Hola siguientes:

* Suscripción de Azure. Si aún no tiene ninguna, puede [activar las ventajas de la suscripción a MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o <a href="/pricing/free-account/" target="_blank">[registrarse para obtener una cuenta gratis](https://azure.microsoft.com/free/).
* [Cuenta de automatización](automation-sec-configure-azure-runas-account.md) toohold Hola runbook y autenticar tooAzure recursos.  Esta cuenta debe tener permiso toostart y detener la máquina virtual de Hola.
* [Cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md) en qué plantilla de administrador de recursos de hello toostore
* Azure Powershell instalado en una máquina local. Vea [instalar y configurar Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) para obtener información acerca de cómo tooget PowerShell de Azure.

## <a name="create-hello-resource-manager-template"></a>Crear plantilla de administrador de recursos de Hola

En este ejemplo, utilizamos una plantilla de Resource Manager que implementa una nueva cuenta de Azure Storage.

En un editor de texto, copie Hola siguiente texto:

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

Guardar archivo de hello localmente como `TemplateTest.json`.

## <a name="save-hello-resource-manager-template-in-azure-storage"></a>Guarde la plantilla de administrador de recursos de hello en el almacenamiento de Azure

Ahora se usa PowerShell toocreate un recurso compartido de archivos de almacenamiento de Azure y cargar hello `TemplateTest.json` archivo.
Para obtener instrucciones sobre cómo toocreate un archivo de recurso compartido y cargar un archivo en hello portal de Azure, consulte [Introducción al almacenamiento de archivos de Azure en Windows](../storage/files/storage-dotnet-how-to-use-files.md).

Inicie PowerShell en el equipo local y ejecute hello después toocreate un recurso compartido de archivos de comandos y cargar el recurso compartido de archivos de toothat de plantilla del Administrador de recursos Hola.

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

## <a name="create-hello-powershell-runbook-script"></a>Crear script de runbook de PowerShell de Hola

Ahora es crear un script de PowerShell que obtiene hello `TemplateTest.json` de archivos desde el almacenamiento de Azure e implementa Hola plantilla toocreate una nueva cuenta de almacenamiento de Azure.

En un editor de texto, pegue Hola siguiente texto:

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

Guardar archivo de hello localmente como `DeployTemplate.ps1`.

## <a name="import-and-publish-hello-runbook-into-your-azure-automation-account"></a>Importar y publicar el runbook de hello en su cuenta de automatización de Azure

Ahora se usa PowerShell tooimport Hola runbook en su cuenta de automatización de Azure y, a continuación, publicar el runbook de Hola.
Para obtener información acerca de cómo tooimport y publicar un runbook en hello portal de Azure, consulte [crear o importar un runbook en automatización de Azure](automation-creating-importing-runbook.md).

tooimport `DeployTemplate.ps1` en su cuenta de automatización como un runbook de PowerShell, ejecute hello siga los comandos de PowerShell:

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

## <a name="start-hello-runbook"></a>Iniciar runbook Hola

Ahora se inicia runbook Hola Hola que realiza la llamada [AzureRmAutomationRunbook inicio](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.

Para obtener información acerca de cómo toostart un runbook en hello portal de Azure, consulte [a partir de un runbook en automatización de Azure](automation-starting-a-runbook.md).

Ejecute hello siga los comandos en la consola de PowerShell de hello:

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

Hola se ejecuta runbook, y puede comprobar su estado mediante la ejecución de `$job.Status`.

Hola runbook Obtiene la plantilla de administrador de recursos de Hola y utiliza toodeploy una nueva cuenta de almacenamiento de Azure.
Puede ver que se ha creado la nueva cuenta de almacenamiento Hola ejecutando el siguiente comando de hello:
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a>Resumen

Eso es todo. Ahora puede usar Automatización de Azure y almacenamiento de Azure y el Administrador de recursos plantillas toodeploy todos los recursos de Azure.

## <a name="next-steps"></a>Pasos siguientes

* toolearn más acerca de las plantillas de administrador de recursos, consulte [Introducción al administrador de recursos de Azure](../azure-resource-manager/resource-group-overview.md)
* tooget a trabajar con el almacenamiento de Azure, consulte [Introducción tooAzure almacenamiento](../storage/common/storage-introduction.md).
* toofind otros útiles runbooks de automatización de Azure, consulte [galerías de módulos y runbooks de automatización de Azure](automation-runbook-gallery.md).
* toofind otras plantillas de administrador de recursos útiles, vea [plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/)

