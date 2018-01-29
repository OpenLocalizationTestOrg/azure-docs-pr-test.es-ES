---
title: Uso de PowerShell para configurar Application Insights en Azure | Microsoft Docs
description: "Configuración automática de Diagnósticos de Azure para canalización a Application Insights"
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
ms.author: mbullwin
ms.openlocfilehash: 46f148cc69a8e36500dc351f74fa87576eb86a6b
ms.sourcegitcommit: e462e5cca2424ce36423f9eff3a0cf250ac146ad
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/01/2017
---
# <a name="using-powershell-to-set-up-application-insights-for-an-azure-web-app"></a>Uso de PowerShell para configurar Application Insights para una aplicación web de Azure
[Microsoft Azure](https://azure.com) puede [configurarse para que envíe diagnósticos de Azure](app-insights-azure-diagnostics.md) a [Azure Application Insights](app-insights-overview.md). Los diagnósticos están relacionados con Servicios en la nube de Azure y Máquinas virtuales de Azure. Complementan la telemetría que se envía desde la aplicación mediante el SDK de Application Insights. Como parte de la automatización del proceso de creación de nuevos recursos en Azure, puede configurar diagnósticos mediante PowerShell.

## <a name="azure-template"></a>Plantilla de Azure
Si la aplicación web está en Azure y crea los recursos mediante una plantilla de Azure Resource Manager, puede configurar Application Insights agregando lo siguiente al nodo de recursos:

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

* `nameOfAIAppResource` : nombre para el recurso de Application Insights
* `myWebAppName` : identificador de la aplicación web

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>Habilitar la extensión de diagnósticos como parte de la implementación de un servicio en la nube
El cmdlet `New-AzureDeployment` tiene un parámetro `ExtensionConfiguration`, que toma una matriz de configuraciones de diagnósticos. Estas pueden crearse mediante el cmdlet `New-AzureServiceDiagnosticsExtensionConfig` . Por ejemplo:

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

Si ha habilitado la extensión de diagnósticos mediante `Set-AzureServiceDiagnosticsExtension` o `New-AzureServiceDiagnosticsExtensionConfig` sin el parámetro Role, puede quitar la extensión mediante `Remove-AzureServiceDiagnosticsExtension` sin el parámetro Role. Si ha usado el parámetro Role al habilitar la extensión, debe utilizarlo también al quitar la extensión.

Para quitar la extensión de diagnóstico de cada rol individual:

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a>Consulte también
* [Supervisión de aplicaciones de Servicios en la nube de Azure con Application Insights](app-insights-cloudservices.md)
* [Envío de Azure Diagnostics a Application Insights](app-insights-azure-diagnostics.md)
* [Automatización de la configuración de alertas](app-insights-powershell-alerts.md)

