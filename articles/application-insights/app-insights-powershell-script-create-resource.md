---
title: aaaPowerShell script toocreate un recurso de Application Insights | Documentos de Microsoft
description: "Automatice la creación de recursos de Application Insights."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: f0082c9b-43ad-4576-a417-4ea8e0daf3d9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/19/2016
ms.author: bwren
ms.openlocfilehash: 2ac00376d38026d64c2c5deabfaca60588924510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-script-toocreate-an-application-insights-resource"></a>Script de PowerShell toocreate un recurso de Application Insights


Cuando desee toomonitor una nueva aplicación - o una nueva versión de una aplicación - con [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), configurar un recurso nuevo en Microsoft Azure. Este recurso es donde se analiza y muestra los datos de telemetría de hello de la aplicación. 

Puede automatizar la creación de hello de un nuevo recurso mediante PowerShell.

Por ejemplo, si está desarrollando una aplicación de dispositivo móvil, es probable que, en cualquier momento, haya varias versiones publicadas de la aplicación en uso por los clientes. No desea tooget Hola telemetría resultantes distintas versiones mezcladas. Para obtener un nuevo recurso de la toocreate del proceso de compilación para cada compilación.

> [!NOTE]
> Si desea toocreate un conjunto de recursos todos al mismo Hola de tiempo, considere la posibilidad de [crear recursos de hello usando una plantilla de Azure](app-insights-powershell.md).
> 
> 

## <a name="script-toocreate-an-application-insights-resource"></a>Secuencia de comandos toocreate un recurso de Application Insights
Vea las especificaciones de hello cmdlet pertinente:

* [New-AzureRmResource](https://msdn.microsoft.com/library/mt652510.aspx)
* [New-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt678995.aspx)

*Script de PowerShell*  

```PowerShell


###########################################
# Set Values
###########################################

# If running manually, uncomment before hello first 
# execution toologin toohello Azure Portal:

# Add-AzureRmAccount / Login-AzureRmAccount

# Set hello name of hello Application Insights Resource

$appInsightsName = "TestApp"

# Set hello application name used for hello value of hello Tag "AppInsightsApp" 

$applicationTagName = "MyApp"

# Set hello name of hello Resource Group toouse.  
# Default is hello application name.
$resourceGroupName = "MyAppResourceGroup"

###################################################
# Create hello Resource and Output hello name and iKey
###################################################

# Select hello azure subscription
Select-AzureSubscription -SubscriptionName "MySubscription"

# Create hello App Insights Resource


$resource = New-AzureRmResource `
  -ResourceName $appInsightsName `
  -ResourceGroupName $resourceGroupName `
  -Tag @{ applicationType = "web"; applicationName = $applicationTagName} `
  -ResourceType "Microsoft.Insights/components" `
  -Location "East US" `  # or North Europe, West Europe, South Central US
  -PropertyObject @{"Application_Type"="web"} `
  -Force

# Give owner access toohello team

New-AzureRmRoleAssignment `
  -SignInName "myteam@fabrikam.com" `
  -RoleDefinitionName Owner `
  -Scope $resource.ResourceId 


# Display iKey
Write-Host "App Insights Name = " $resource.Name
Write-Host "IKey = " $resource.Properties.InstrumentationKey

```

## <a name="what-toodo-with-hello-ikey"></a>¿Qué toodo con iKey Hola
Cada recurso se identifica por su clave de instrumentación (iKey). Hola iKey es una salida de script de creación de recursos de Hola. El script de compilación debe proporcionar Hola iKey toohello que Application Insights SDK incrustada en la aplicación.

Hay dos maneras toomake Hola iKey disponible toohello SDK:

* En [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md): 
  * `<instrumentationkey>`*ikey*`</instrumentationkey>`
* O bien en el [código de inicialización](app-insights-api-custom-events-metrics.md): 
  * `Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`

## <a name="see-also"></a>Otras referencias
* [Crear Application Insights y recursos de pruebas web a partir de plantillas](app-insights-powershell.md)
* [Configurar la supervisión de diagnósticos de Azure con PowerShell](app-insights-powershell-azure-diagnostics.md) 
* [Establecimiento de alertas mediante PowerShell](app-insights-powershell-alerts.md)

