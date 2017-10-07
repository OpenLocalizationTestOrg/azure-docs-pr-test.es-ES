---
title: "aaaPass JSON objeto tooan runbook de automatización de Azure | Documentos de Microsoft"
description: "¿Cómo toopass parámetros tooa runbook como un objeto JSON"
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
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 8229a16015d549927ead5496c70e9fb391d35498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="pass-a-json-object-tooan-azure-automation-runbook"></a>Pasar un runbook de automatización de Azure de tooan de objeto JSON

Puede ser datos toostore útil que desea toopass tooa runbook en un archivo JSON.
Por ejemplo, podría crear un archivo JSON que contiene todos los parámetros de hello desea toopass tooa runbook.
toodo, tiene tooconvert Hola JSON tooa cadena y, a continuación, convertir Hola string tooa PowerShell (objeto) antes de pasar su runbook toohello de contenido.

En este ejemplo, vamos a crear un script de PowerShell que llame [AzureRmAutomationRunbook inicio](https://msdn.microsoft.com/library/mt603661.aspx) toostart un runbook de PowerShell, pasar el contenido de Hola de hello JSON toohello runbook.
Hola PowerShell runbook inicia una máquina virtual de Azure, obtiene los parámetros de Hola para hello VM de Hola JSON que se pasó en.

## <a name="prerequisites"></a>Requisitos previos
toocomplete este tutorial, necesita Hola siguientes:

* Suscripción de Azure. Si aún no tiene ninguna, puede [activar las ventajas de la suscripción a MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o <a href="/pricing/free-account/" target="_blank">[registrarse para obtener una cuenta gratis](https://azure.microsoft.com/free/).
* [Cuenta de automatización](automation-sec-configure-azure-runas-account.md) toohold Hola runbook y autenticar tooAzure recursos.  Esta cuenta debe tener permiso toostart y detener la máquina virtual de Hola.
* Una máquina virtual de Azure. Detendremos e iniciaremos esta máquina, por lo que no debería ser una máquina virtual de producción.
* Azure Powershell instalado en una máquina local. Vea [instalar y configurar Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) para obtener información acerca de cómo tooget PowerShell de Azure.

## <a name="create-hello-json-file"></a>Crear archivo JSON de hello

Escriba lo siguiente Hola de prueba en un archivo de texto y guárdelo como `test.json` en algún lugar en el equipo local.

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-hello-runbook"></a>Crear Hola runbook

Cree un runbook de PowerShell denominado "Test-Json" en Azure Automation.
toolearn toocreate un nuevo runbook de PowerShell, vea [mi primer runbook de PowerShell](automation-first-runbook-textual-powershell.md).

datos JSON de tooaccept hello, Hola runbook debe tomar un objeto como un parámetro de entrada.

Hola runbook, a continuación, puede usar propiedades de hello definidas en hello JSON.

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect tooAzure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object tooactual JSON
$json = $json | ConvertFrom-Json

# Use hello values from hello JSON object as hello parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 Guarde y publique este runbook en su cuenta de Automation.

## <a name="call-hello-runbook-from-powershell"></a>Llamada Hola runbook de PowerShell

Ahora puede llamar a runbook Hola desde el equipo local mediante el uso de PowerShell de Azure.
Ejecute hello siga los comandos de PowerShell:

1. Inicie sesión en tooAzure:
   ```powershell
   Login-AzureRmAccount
   ```
    Se está tooenter solicitada sus credenciales de Azure.
1. Para obtener contenido de hello del archivo JSON de hello y convertir tooa cadena:
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    `JsonPath`es la ruta de acceso de Hola donde guardó el archivo JSON de hello.
1. Convertir el contenido de la cadena de hello `$json` tooa objeto de PowerShell:
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. Crear una tabla hash para los parámetros de Hola para `Start-AzureRmAutomstionRunbook`:
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   Tenga en cuenta que se va a establecer valor de Hola de `Parameters` toohello objeto de PowerShell que contiene valores de hello de archivo JSON de hello. 
1. Iniciar runbook Hola
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

Hola runbook usa valores de hello de hello JSON archivo toostart una máquina virtual.

## <a name="next-steps"></a>Pasos siguientes

* toolearn más información acerca de la edición de runbooks de flujo de trabajo de PowerShell y PowerShell con un editor de texto, consulte [edición textuales runbooks en automatización de Azure](automation-edit-textual-runbook.md) 
* toolearn más información sobre la creación e importación de runbooks, vea [crear o importar un runbook en automatización de Azure](automation-creating-importing-runbook.md)


