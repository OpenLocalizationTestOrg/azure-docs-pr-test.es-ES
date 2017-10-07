---
title: aaaUsing PowerShell toosetup Application Insights en un Azure | Documentos de Microsoft
description: "Automatizar tooApplication de toopipe de configurar diagnósticos de Azure Insights."
services: application-insights
documentationcenter: .net
author: sbtron
manager: carmonm
ms.assetid: 4ac803a8-f424-4c0c-b18f-4b9c189a64a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/17/2015
ms.author: bwren
ms.openlocfilehash: c48a5d8eb23df162522860935af876063aaa6976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a>Usar PowerShell tooset una visión de la aplicación para una aplicación web de Azure
[Microsoft Azure](https://azure.com) puede ser [configurar diagnósticos de Azure toosend](app-insights-azure-diagnostics.md) demasiado[Azure Application Insights](app-insights-overview.md). Diagnósticos de Hola relacionan tooAzure servicios en la nube y máquinas virtuales de Azure. Se complementa la telemetría de Hola que ha enviado desde dentro de la aplicación hello mediante Hola Application Insights SDK. Como parte de automatizar el proceso de Hola de creación de nuevos recursos en Azure, puede configurar diagnósticos mediante PowerShell.

## <a name="azure-template"></a>Plantilla de Azure
Si la aplicación web de hello en Azure y crear los recursos mediante una plantilla de Azure Resource Manager, puede configurar Application Insights mediante la adición de este nodo de recursos de toohello:

    {
      resources: [
        /* Create Application Insights resource */
        {
          "apiVersion": "2015-05-01",
          "type": "microsoft.insights/components",
          "name": "nameOfAIAppResource",
          "location": "centralus",
          "kind": "web",
          "properties": { "ApplicationId": "nameOfAIAppResource" },
          "dependsOn": [
            "[concat('Microsoft.Web/sites/', myWebAppName)]"
          ]
        }
       ]
     } 

* `nameOfAIAppResource`-un nombre para el recurso de Application Insights de Hola
* `myWebAppName`-Id. de Hola de aplicación web de hello

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>Habilitar la extensión de diagnósticos como parte de la implementación de un servicio en la nube
Hola `New-AzureDeployment` cmdlet tiene un parámetro `ExtensionConfiguration`, que toma una matriz de configuraciones de diagnóstico. Estos informes pueden crearse mediante hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet. Por ejemplo:

```ps

    $service_package = "CloudService.cspkg"
    $service_config = "ServiceConfiguration.Cloud.cscfg"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

    $primary_storagekey = (Get-AzureStorageKey `
     -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
       -StorageAccountName $diagnostics_storagename `
       -StorageAccountKey $primary_storagekey

    $webrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WebRole" -Storage_context $storageContext `
      -DiagnosticsConfigurationPath $webrole_diagconfigpath
    $workerrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WorkerRole" `
      -StorageContext $storage_context `
      -DiagnosticsConfigurationPath $workerrole_diagconfigpath

    New-AzureDeployment `
      -ServiceName $service_name `
      -Slot Production `
      -Package $service_package `
      -Configuration $service_config `
      -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)

``` 

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>Habilitar la extensión de diagnóstico en un servicio en la nube existente
En un servicio existente, use `Set-AzureServiceDiagnosticsExtension`.

```ps

    $service_name = "MyService"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"
    $primary_storagekey = (Get-AzureStorageKey `
         -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
        -StorageAccountName $diagnostics_storagename `
        -StorageAccountKey $primary_storagekey

    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $webrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WebRole" 
    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $workerrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WorkerRole"
```

## <a name="get-current-diagnostics-extension-configuration"></a>Obtener la configuración actual de la extensión de diagnósticos
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a>Eliminar la extensión de diagnósticos
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

Si ha habilitado extensión de diagnósticos de hello mediante `Set-AzureServiceDiagnosticsExtension` o `New-AzureServiceDiagnosticsExtensionConfig` sin el parámetro de función de hello, a continuación, puede quitar Hola extensión mediante `Remove-AzureServiceDiagnosticsExtension` sin el parámetro de función de Hola. Si se usa el parámetro de función de hello al habilitar la extensión de hello, a continuación, debe también usarse al quitar la extensión de Hola.

extensión de diagnósticos de hello tooremove de cada rol individual:

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a>Otras referencias
* [Supervisión de aplicaciones de Servicios en la nube de Azure con Application Insights](app-insights-cloudservices.md)
* [Enviar información de diagnóstico de Azure tooApplication](app-insights-azure-diagnostics.md)
* [Automatización de la configuración de alertas](app-insights-powershell-alerts.md)

