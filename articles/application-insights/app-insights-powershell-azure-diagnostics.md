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
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a><span data-ttu-id="f610f-103">Usar PowerShell tooset una visión de la aplicación para una aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="f610f-103">Using PowerShell tooset up Application Insights for an Azure web app</span></span>
<span data-ttu-id="f610f-104">[Microsoft Azure](https://azure.com) puede ser [configurar diagnósticos de Azure toosend](app-insights-azure-diagnostics.md) demasiado[Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f610f-104">[Microsoft Azure](https://azure.com) can be [configured toosend Azure Diagnostics](app-insights-azure-diagnostics.md) too[Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="f610f-105">Diagnósticos de Hola relacionan tooAzure servicios en la nube y máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="f610f-105">hello diagnostics relate tooAzure Cloud Services and Azure VMs.</span></span> <span data-ttu-id="f610f-106">Se complementa la telemetría de Hola que ha enviado desde dentro de la aplicación hello mediante Hola Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="f610f-106">They complement hello telemetry that you send from within hello app using hello Application Insights SDK.</span></span> <span data-ttu-id="f610f-107">Como parte de automatizar el proceso de Hola de creación de nuevos recursos en Azure, puede configurar diagnósticos mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f610f-107">As part of automating hello process of creating new resources in Azure, you can configure diagnostics using PowerShell.</span></span>

## <a name="azure-template"></a><span data-ttu-id="f610f-108">Plantilla de Azure</span><span class="sxs-lookup"><span data-stu-id="f610f-108">Azure template</span></span>
<span data-ttu-id="f610f-109">Si la aplicación web de hello en Azure y crear los recursos mediante una plantilla de Azure Resource Manager, puede configurar Application Insights mediante la adición de este nodo de recursos de toohello:</span><span class="sxs-lookup"><span data-stu-id="f610f-109">If hello web app is in Azure and you create your resources using an Azure Resource Manager template, you can configure Application Insights by adding this toohello resources node:</span></span>

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

* <span data-ttu-id="f610f-110">`nameOfAIAppResource`-un nombre para el recurso de Application Insights de Hola</span><span class="sxs-lookup"><span data-stu-id="f610f-110">`nameOfAIAppResource` - a name for hello Application Insights resource</span></span>
* <span data-ttu-id="f610f-111">`myWebAppName`-Id. de Hola de aplicación web de hello</span><span class="sxs-lookup"><span data-stu-id="f610f-111">`myWebAppName` - hello id of hello web app</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="f610f-112">Habilitar la extensión de diagnósticos como parte de la implementación de un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="f610f-112">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="f610f-113">Hola `New-AzureDeployment` cmdlet tiene un parámetro `ExtensionConfiguration`, que toma una matriz de configuraciones de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="f610f-113">hello `New-AzureDeployment` cmdlet has a parameter `ExtensionConfiguration`, which takes an array of diagnostics configurations.</span></span> <span data-ttu-id="f610f-114">Estos informes pueden crearse mediante hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f610f-114">These can be created using hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span></span> <span data-ttu-id="f610f-115">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f610f-115">For example:</span></span>

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

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="f610f-116">Habilitar la extensión de diagnóstico en un servicio en la nube existente</span><span class="sxs-lookup"><span data-stu-id="f610f-116">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="f610f-117">En un servicio existente, use `Set-AzureServiceDiagnosticsExtension`.</span><span class="sxs-lookup"><span data-stu-id="f610f-117">On an existing service, use `Set-AzureServiceDiagnosticsExtension`.</span></span>

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

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="f610f-118">Obtener la configuración actual de la extensión de diagnósticos</span><span class="sxs-lookup"><span data-stu-id="f610f-118">Get current diagnostics extension configuration</span></span>
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a><span data-ttu-id="f610f-119">Eliminar la extensión de diagnósticos</span><span class="sxs-lookup"><span data-stu-id="f610f-119">Remove diagnostics extension</span></span>
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="f610f-120">Si ha habilitado extensión de diagnósticos de hello mediante `Set-AzureServiceDiagnosticsExtension` o `New-AzureServiceDiagnosticsExtensionConfig` sin el parámetro de función de hello, a continuación, puede quitar Hola extensión mediante `Remove-AzureServiceDiagnosticsExtension` sin el parámetro de función de Hola.</span><span class="sxs-lookup"><span data-stu-id="f610f-120">If you enabled hello diagnostics extension using either `Set-AzureServiceDiagnosticsExtension` or `New-AzureServiceDiagnosticsExtensionConfig` without hello Role parameter, then you can remove hello extension using `Remove-AzureServiceDiagnosticsExtension` without hello Role parameter.</span></span> <span data-ttu-id="f610f-121">Si se usa el parámetro de función de hello al habilitar la extensión de hello, a continuación, debe también usarse al quitar la extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="f610f-121">If hello Role parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="f610f-122">extensión de diagnósticos de hello tooremove de cada rol individual:</span><span class="sxs-lookup"><span data-stu-id="f610f-122">tooremove hello diagnostics extension from each individual role:</span></span>

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a><span data-ttu-id="f610f-123">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="f610f-123">See also</span></span>
* [<span data-ttu-id="f610f-124">Supervisión de aplicaciones de Servicios en la nube de Azure con Application Insights</span><span class="sxs-lookup"><span data-stu-id="f610f-124">Monitor Azure Cloud Services apps with Application Insights</span></span>](app-insights-cloudservices.md)
* [<span data-ttu-id="f610f-125">Enviar información de diagnóstico de Azure tooApplication</span><span class="sxs-lookup"><span data-stu-id="f610f-125">Send Azure Diagnostics tooApplication Insights</span></span>](app-insights-azure-diagnostics.md)
* [<span data-ttu-id="f610f-126">Automatización de la configuración de alertas</span><span class="sxs-lookup"><span data-stu-id="f610f-126">Automate configuring alerts</span></span>](app-insights-powershell-alerts.md)
