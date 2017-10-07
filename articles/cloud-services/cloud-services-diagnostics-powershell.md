---
title: "aaaEnable diagnósticos en servicios de nube de Azure mediante PowerShell | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooenable diagnósticos para la nube services mediante PowerShell"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 66e08754-8639-4022-ae18-4237749ba17d
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/06/2016
ms.author: adegeo
ms.openlocfilehash: 7c7444df13edc8d7f5663e20ec7558d36aac45d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a>Habilitar el diagnóstico en Servicios en la nube de Azure mediante PowerShell
Puede recopilar datos de diagnóstico como registros de aplicaciones, etc. desde un servicio en la nube mediante los contadores de rendimiento Hola extensión de diagnósticos de Azure. Este artículo describe cómo tooenable Hola extensión de diagnósticos de Azure para un servicio de nube mediante PowerShell.  Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) de requisitos previos de hello necesarios para este artículo.

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>Habilitar la extensión de diagnósticos como parte de la implementación de un servicio en la nube
Este enfoque es el tipo de integración de toocontinuous aplicables de escenarios, donde extensión pueda habilitarse como parte de la implementación de diagnósticos de Hola Hola servicio en la nube. Al crear una nueva implementación del servicio de nube puede habilitar la extensión de diagnósticos de hello pasando hello *ExtensionConfiguration* parámetro toohello [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet. Hola *ExtensionConfiguration* parámetro toma una matriz de configuraciones de diagnóstico que pueden crearse con hello [AzureServiceDiagnosticsExtensionConfig New](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.

Hello en el ejemplo siguiente se muestra cómo se pueden habilitar los diagnósticos para un servicio de nube con un WebRole y WorkerRole, cada uno con una configuración de diagnóstico diferentes.

```powershell
$service_name = "MyService"
$service_package = "CloudService.cspkg"
$service_config = "ServiceConfiguration.Cloud.cscfg"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)
```

Si especifica el archivo de configuración de diagnósticos de hello un `StorageAccount` elemento con un nombre de cuenta de almacenamiento, a continuación, Hola `New-AzureServiceDiagnosticsExtensionConfig` cmdlet usarán automáticamente esa cuenta de almacenamiento. Para este toowork debe toobe en cuenta de almacenamiento de Hola Hola misma suscripción como Hola servicio en la nube que se está implementando.

De Azure SDK 2.6 publicación archivos de configuración de extensión de hello ulterior generados por hello MSBuild salida del destino incluirá el nombre de la cuenta de almacenamiento hello en función de la cadena de configuración de diagnósticos de hello especificado en el archivo de configuración de servicio (.cscfg) de Hola. script de Hola a continuación muestra cómo tooparse archivos de configuración de extensión de Hola de Hola resultados de destino de publicación y configurar la extensión de diagnóstico para cada rol al implementar el servicio de nube de Hola.

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find hello Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find hello RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
    $roleName = ""
    $roles = $extPath -split ".",0,"simplematch"
    if ($roles -is [system.array] -and $roles.Length -gt 1)
    {
        $roleName = $roles[1]
        $x = 2
        while ($x -le $roles.Length)
            {
               if ($roles[$x] -ne "PubConfig")
                {
                    $roleName = $roleName + "." + $roles[$x]
                }
                else
                {
                    break
                }
                $x++
            }
        $fullExtPath = Join-Path -path $extensionsSearchPath -ChildPath $extPath
        $diagnosticsconfig = New-AzureServiceDiagnosticsExtensionConfig -Role $roleName -DiagnosticsConfigurationPath $fullExtPath
        $diagnosticsConfigurations += $diagnosticsconfig
    }
}
New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration $diagnosticsConfigurations
```

Visual Studio Online, se usa un enfoque similar para implementaciones automatizadas de servicios en la nube con la extensión de diagnósticos de Hola. Consulte [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) para obtener un ejemplo completo.

Si no hay ningún `StorageAccount` se especificó en la configuración de diagnóstico de hello, deberá toopass en hello *StorageAccountName* parámetro toohello cmdlet. Si hello *StorageAccountName* se especifica el parámetro, a continuación, usará siempre cuenta de almacenamiento de Hola que se especifica en el parámetro hello y no Hola uno que se especifica en el archivo de configuración de diagnósticos de Hola Hola cmdlet.

Si pasan Hola diagnósticos Hola cuenta de almacenamiento está en una suscripción diferente de hello servicio en la nube, deberá tooexplicitly *StorageAccountName* y *StorageAccountKey* parámetros cmdlet de toohello. Hola *StorageAccountKey* parámetro no es necesario cuando diagnósticos de hello cuenta de almacenamiento está en Hola misma suscripción, como Hola cmdlet automáticamente puede consultar y establecer el valor de clave de hello al habilitar la extensión de diagnósticos de Hola. Sin embargo, si hello es la cuenta de almacenamiento de información de diagnóstico en una suscripción diferente, a continuación, Hola cmdlet podría no ser capaz de tooget clave de hello automáticamente y debe tooexplicitly especificar clave de Hola a través de hello *StorageAccountKey* parámetro.

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>Habilitar la extensión de diagnóstico en un servicio en la nube existente
Puede usar hello [AzureServiceDiagnosticsExtension conjunto](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) configuración de diagnóstico de cmdlet tooenable o actualización en un servicio de nube que ya se está ejecutando.

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a>Obtener la configuración actual de la extensión de diagnósticos
Hola de uso [AzureServiceDiagnosticsExtension Get](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget Hola actual configuración de diagnóstico para un servicio de nube.

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a>Eliminar la extensión de diagnósticos
tooturn desactivar diagnósticos en una nube de servicio se puede usar hello [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

Si ha habilitado extensión de diagnósticos de hello mediante *conjunto AzureServiceDiagnosticsExtension* o hello *New-AzureServiceDiagnosticsExtensionConfig* sin hello *rol* parámetro, a continuación, se puede quitar extensión hello mediante *Remove-AzureServiceDiagnosticsExtension* sin hello *rol* parámetro. Si hello *rol* parámetro se utiliza al habilitar la extensión de hello, a continuación, se debe también pueden usarse para quitar la extensión de Hola.

extensión de diagnósticos de hello tooremove de cada rol individual:

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a>Pasos siguientes
* Para obtener instrucciones adicionales sobre el uso de diagnósticos de Azure y otros problemas de tootroubleshoot técnicas, consulte [habilitar diagnósticos en servicios en la nube y máquinas virtuales](cloud-services-dotnet-diagnostics.md).
* Hola [esquema de configuración de diagnósticos](https://msdn.microsoft.com/library/azure/dn782207.aspx) explica Hola opciones diversas configuraciones de xml para extensión de diagnósticos de Hola.
* toolearn tooenable extensión de diagnósticos de Hola para máquinas virtuales, vea [crear una máquina Virtual de Windows con la supervisión y diagnósticos mediante la plantilla de administrador de recursos de Azure](../virtual-machines/windows/extensions-diagnostics-template.md)
