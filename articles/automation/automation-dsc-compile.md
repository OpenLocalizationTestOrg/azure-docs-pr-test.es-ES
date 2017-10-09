---
title: "aaaCompiling configuraciones de DSC de automatización de Azure | Documentos de Microsoft"
description: "Este artículo se describe cómo toocompile las configuraciones de configuración de estado deseado (DSC) para la automatización de Azure."
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
ms.assetid: 49f20b31-4fa5-4712-b1c7-8f4409f1aecc
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 02/07/2017
ms.author: magoedte; eslesar
ms.openlocfilehash: b195311318a2d7431c4d6b29f4b9a5f3a0a0a9a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a>Compilación de configuraciones en DSC de Automatización de Azure

Puede compilar configuraciones de configuración de estado deseado (DSC) de dos maneras con automatización de Azure: Hola portal de Azure y con Windows PowerShell. Hello tabla siguiente le ayudará a determinar cuándo toouse qué método basándose en características de Hola de cada uno:

### <a name="azure-portal"></a>Azure Portal

* Método más sencillo con la interfaz de usuario interactiva
* Valores de parámetro simples de formulario tooprovide
* Seguimiento sencillo del estado del trabajo
* Acceso autenticado con inicio de sesión de Azure

### <a name="windows-powershell"></a>Windows PowerShell

* Llamar desde la línea de comandos con los cmdlets de Windows PowerShell
* Poder incluirse en una solución automatizada con varios pasos
* Proporcionar valores de parámetro simples y complejos
* Realizar el seguimiento del estado del trabajo
* Cliente requerido toosupport cmdlets de PowerShell
* Pasar ConfigurationData
* Compilar configuraciones que usan credenciales

Una vez que haya decidido en un método de compilación, puede seguir Hola respectivos procedimientos a continuación toostart compilar.

## <a name="compiling-a-dsc-configuration-with-hello-azure-portal"></a>Compilar una configuración de DSC con hello portal de Azure

1. En su cuenta de Automation, haga clic en **DSC Configurations** (Configuraciones DSC).
2. Haga clic en una configuración tooopen su hoja.
3. Haga clic en **Compilar**.
4. Si configuración de hello no tiene parámetros, es posible que tooconfirm solicitada si desea que toocompile lo. Si la configuración de hello tiene parámetros, Hola **compilar configuración** hoja se abrirá por lo que puede proporcionar valores de parámetro. Vea hello [ **parámetros básicos** ](#basic-parameters) sección para obtener más información sobre parámetros.
5. Hola **trabajo de compilación** hoja se abre para que puede realizar un seguimiento de estado del trabajo de compilación de Hola y Hola configuraciones del nodo (documentos MOF de configuración) que ocasiona toobe colocado en hello servidor de extracción de DSC de automatización de Azure.

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a>Compilación de una configuración DSC con Windows PowerShell

Puede usar [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart compilar con Windows PowerShell. Hola siguiente código de ejemplo inicia la compilación de una configuración de DSC conocida como **SampleConfig**.

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

`Start-AzureRmAutomationDscCompilationJob`Devuelve una compilación de trabajos que se puede usar tootrack su estado de objeto. A continuación, puede usar este objeto de trabajo de compilación con [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine estado de Hola de trabajo de compilación de Hola y [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview sus secuencias (salida). Hola siguiente código de ejemplo inicia la compilación del programa Hola a **SampleConfig** configuración, espera hasta que se ha completado y, a continuación, muestra sus secuencias.

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a>Parámetros básicos
Declaración de parámetro en las configuraciones de DSC, incluidos los tipos de parámetros y propiedades, funciona igual Hola como en los runbooks de automatización de Azure. Vea [a partir de un runbook en automatización de Azure](automation-starting-a-runbook.md) toolearn más información acerca de los parámetros del runbook.

Hello en el ejemplo siguiente se utiliza dos parámetros llamados **NombreCaracterística** y **IsPresent**, valores de hello de toodetermine de propiedades de hello **ParametersExample.sample** nodo configuración, generada durante la compilación.

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]

        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = "Present"
    if($IsPresent -eq $false)
    {
        $EnsureString = "Absent"
    }

    Node "sample"
    {
        WindowsFeature ($FeatureName + "Feature")
        {
            Ensure = $EnsureString
            Name = $FeatureName
        }
    }
}
```

Puede compilar las configuraciones de DSC que usan parámetros básicos en el portal de DSC de automatización de Azure de Hola o con Azure PowerShell:

### <a name="portal"></a>Portal

En el portal de hello, puede especificar valores de parámetro después de hacer clic **compilar**.

![texto alternativo](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a>PowerShell

PowerShell requiere parámetros en un [hashtable](http://technet.microsoft.com/library/hh847780.aspx) donde clave Hola coincide con el nombre del parámetro de Hola y el valor de hello es igual al valor del parámetro hello.

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

Para obtener información acerca de cómo pasar PSCredentials como parámetros, consulte más abajo la sección <a href="#credential-assets">**Recursos de credenciales**</a> .

## <a name="configurationdata"></a>ConfigurationData
**ConfigurationData** permite tooseparate configuración estructural de cualquier configuración específica del entorno durante el uso de DSC de PowerShell. Vea [separar "Qué" de "Where" en el DSC de PowerShell](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn más información sobre **ConfigurationData**.

> [!NOTE]
> Puede usar **ConfigurationData** cuando se compila en DSC de automatización de Azure con Azure PowerShell, pero no en hello portal de Azure.

Hello ejemplo DSC configuración siguiente utiliza **ConfigurationData** a través de hello **$ConfigurationData** y **$AllNodes** palabras clave. También necesitará hello [ **xWebAdministration** módulo](https://www.powershellgallery.com/packages/xWebAdministration/) en este ejemplo:

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure   = "Present"
        }
    }
}
```

Puede compilar la configuración de DSC Hola anteriormente con PowerShell. Hola situada bajo PowerShell agrega dos toohello de configuraciones de nodo servidor de extracción de DSC de automatización de Azure: **ConfigurationDataSample.MyVM1** y **ConfigurationDataSample.MyVM3**:

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "MyVM1"
            Role = "WebServer"
        },
        @{
            NodeName = "MyVM2"
            Role = "SQLServer"
        },
        @{
            NodeName = "MyVM3"
            Role = "WebServer"
        }
    )

    NonNodeData = @{
        SomeMessage = "I love Azure Automation DSC!"
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ConfigurationDataSample" -ConfigurationData $ConfigData
```

## <a name="assets"></a>Recursos

Referencias de activos son Hola igual en runbooks y las configuraciones de DSC de automatización de Azure. Vea Hola siguientes para obtener más información:

* [Certificados](automation-certificates.md)
* [Conexiones](automation-connections.md)
* [Credenciales](automation-credentials.md)
* [Variables](automation-variables.md)

### <a name="credential-assets"></a>Recursos de credenciales

Mientras que las configuraciones DSC en Azure Automation pueden hacer referencia a los recursos de credenciales mediante **Get-AzureRmAutomationCredential**, los recursos de credenciales también se pueden pasar mediante parámetros, si se desea. Si una configuración toma un parámetro de **PSCredential** escribe, debe tener un nombre de cadena de hello toopass de un activo de credencial de automatización de Azure como valor del parámetro de ese, en lugar de un objeto PSCredential. Entre bastidores de hello, se recuperará y pasa toohello configuración activo de credencial de automatización de Azure Hola con ese nombre.

Mantener las credenciales seguras en configuraciones de nodo (documentos de configuración de MOF) requiere cifrado de credenciales de hello en el archivo MOF de configuración de nodo de Hola. Automatización de Azure tiene un paso más y cifra el archivo MOF completo de Hola. Sin embargo, actualmente debe indicar DSC de PowerShell es correcto para toobe de credenciales en texto sin formato que produce durante la generación de MOF de configuración de nodo, porque no sabe DSC de PowerShell que automatización de Azure se pueden cifrar archivo MOF de hello completa después de su generación a través de un trabajo de compilación.

Puede indicar que DSC de PowerShell que es correcto para toobe de credenciales que se va a producir en texto sin formato en la configuración de nodo de hello genera MOF con [ **ConfigurationData**](#configurationdata). Debería pasar `PSDscAllowPlainTextPassword = $true` a través de **ConfigurationData** para el nombre de cada bloque de nodo que aparece en la configuración de DSC de Hola y usa las credenciales.

Hello en el ejemplo siguiente se muestra una configuración de DSC que usa un recurso de credencial de automatización.

```powershell
Configuration CredentialSample
{
    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -AutomationAccountName "AutomationAcct" -Name "SomeCredentialAsset"

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $Cred
        }
    }
}
```

Puede compilar la configuración de DSC Hola anteriormente con PowerShell. Hola situada bajo PowerShell agrega dos toohello de configuraciones de nodo servidor de extracción de DSC de automatización de Azure: **CredentialSample.MyVM1** y **CredentialSample.MyVM2**.

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "*"
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = "MyVM1"
        },
        @{
            NodeName = "MyVM2"
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "CredentialSample" -ConfigurationData $ConfigData
```

## <a name="importing-node-configurations"></a>Importación de configuraciones de nodo

También puede importar configuraciones de nodo (MOF) que se hayan compilado fuera de Azure. Una ventaja de esta posibilidad es que las configuraciones de nodo pueden estar firmadas.
Una configuración de nodo firmado se comprueba localmente en un nodo administrado por agente Hola DSC, asegurándose de que la configuración de hello está aplicada toohello nodo procede de un origen autorizado.

> [!NOTE]
> Puede usar importar configuraciones firmadas en su cuenta de Azure Automation, pero Azure Automation no admite actualmente la compilación de configuraciones firmadas.

> [!NOTE]
> Un archivo de configuración de nodo debe ser no superior a 1 MB tooallow se toobe importado en automatización de Azure.

Puede obtener información sobre cómo las configuraciones de nodo de toosign en https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.

### <a name="importing-a-node-configuration-in-hello-azure-portal"></a>Importar una configuración de nodo en hello portal de Azure

1. En su cuenta de Automation, haga clic en **DSC node configurations** (Configuraciones de nodo DSC).

    ![Configuraciones de nodo DSC](./media/automation-dsc-compile/node-config.png)
2. Hola **configuraciones del nodo DSC** hoja, haga clic en **agregar un NodeConfiguration**.
3. Hola **importación** hoja, haga clic en el icono de carpeta hello toohello siguiente **archivo de configuración de nodo** toobrowse de cuadro de texto para un archivo de configuración de nodo (MOF) en el equipo local.

    ![Buscar archivo local](./media/automation-dsc-compile/import-browse.png)
4. Escriba un nombre en hello **nombre de configuración** cuadro de texto. Este nombre debe coincidir con hello de configuración de Hola desde el que se compiló la configuración del nodo Hola.
5. Haga clic en **Aceptar**.

### <a name="importing-a-node-configuration-with-powershell"></a>Importación de una configuración de nodo con PowerShell

Puede usar hello [AzureRmAutomationDscNodeConfiguration de importación](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport una configuración de nodo en su cuenta de automatización.

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



