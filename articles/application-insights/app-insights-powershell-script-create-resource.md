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
# <a name="powershell-script-toocreate-an-application-insights-resource"></a><span data-ttu-id="25b48-103">Script de PowerShell toocreate un recurso de Application Insights</span><span class="sxs-lookup"><span data-stu-id="25b48-103">PowerShell script toocreate an Application Insights resource</span></span>


<span data-ttu-id="25b48-104">Cuando desee toomonitor una nueva aplicación - o una nueva versión de una aplicación - con [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), configurar un recurso nuevo en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="25b48-104">When you want toomonitor a new application - or a new version of an application - with [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), you set up a new resource in Microsoft Azure.</span></span> <span data-ttu-id="25b48-105">Este recurso es donde se analiza y muestra los datos de telemetría de hello de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="25b48-105">This resource is where hello telemetry data from your app is analyzed and displayed.</span></span> 

<span data-ttu-id="25b48-106">Puede automatizar la creación de hello de un nuevo recurso mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25b48-106">You can automate hello creation of a new resource by using PowerShell.</span></span>

<span data-ttu-id="25b48-107">Por ejemplo, si está desarrollando una aplicación de dispositivo móvil, es probable que, en cualquier momento, haya varias versiones publicadas de la aplicación en uso por los clientes.</span><span class="sxs-lookup"><span data-stu-id="25b48-107">For example, if you are developing a mobile device app, it's likely that, at any time, there will be several published versions of your app in use by your customers.</span></span> <span data-ttu-id="25b48-108">No desea tooget Hola telemetría resultantes distintas versiones mezcladas.</span><span class="sxs-lookup"><span data-stu-id="25b48-108">You don't want tooget hello telemetry results from different versions mixed up.</span></span> <span data-ttu-id="25b48-109">Para obtener un nuevo recurso de la toocreate del proceso de compilación para cada compilación.</span><span class="sxs-lookup"><span data-stu-id="25b48-109">So you get your build process toocreate a new resource for each build.</span></span>

> [!NOTE]
> <span data-ttu-id="25b48-110">Si desea toocreate un conjunto de recursos todos al mismo Hola de tiempo, considere la posibilidad de [crear recursos de hello usando una plantilla de Azure](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="25b48-110">If you want toocreate a set of resources all at hello same time, consider [creating hello resources using an Azure template](app-insights-powershell.md).</span></span>
> 
> 

## <a name="script-toocreate-an-application-insights-resource"></a><span data-ttu-id="25b48-111">Secuencia de comandos toocreate un recurso de Application Insights</span><span class="sxs-lookup"><span data-stu-id="25b48-111">Script toocreate an Application Insights resource</span></span>
<span data-ttu-id="25b48-112">Vea las especificaciones de hello cmdlet pertinente:</span><span class="sxs-lookup"><span data-stu-id="25b48-112">See hello relevant cmdlet specs:</span></span>

* [<span data-ttu-id="25b48-113">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="25b48-113">New-AzureRmResource</span></span>](https://msdn.microsoft.com/library/mt652510.aspx)
* [<span data-ttu-id="25b48-114">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="25b48-114">New-AzureRmRoleAssignment</span></span>](https://msdn.microsoft.com/library/mt678995.aspx)

<span data-ttu-id="25b48-115">*Script de PowerShell*</span><span class="sxs-lookup"><span data-stu-id="25b48-115">*PowerShell Script*</span></span>  

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

## <a name="what-toodo-with-hello-ikey"></a><span data-ttu-id="25b48-116">¿Qué toodo con iKey Hola</span><span class="sxs-lookup"><span data-stu-id="25b48-116">What toodo with hello iKey</span></span>
<span data-ttu-id="25b48-117">Cada recurso se identifica por su clave de instrumentación (iKey).</span><span class="sxs-lookup"><span data-stu-id="25b48-117">Each resource is identified by its instrumentation key (iKey).</span></span> <span data-ttu-id="25b48-118">Hola iKey es una salida de script de creación de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="25b48-118">hello iKey is an output of hello resource creation script.</span></span> <span data-ttu-id="25b48-119">El script de compilación debe proporcionar Hola iKey toohello que Application Insights SDK incrustada en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="25b48-119">Your build script should provide hello iKey toohello Application Insights SDK embedded in your app.</span></span>

<span data-ttu-id="25b48-120">Hay dos maneras toomake Hola iKey disponible toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="25b48-120">There are two ways toomake hello iKey available toohello SDK:</span></span>

* <span data-ttu-id="25b48-121">En [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="25b48-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span> 
  * <span data-ttu-id="25b48-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span><span class="sxs-lookup"><span data-stu-id="25b48-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span></span>
* <span data-ttu-id="25b48-123">O bien en el [código de inicialización](app-insights-api-custom-events-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="25b48-123">Or in [initialization code](app-insights-api-custom-events-metrics.md):</span></span> 
  * <span data-ttu-id="25b48-124">`Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span><span class="sxs-lookup"><span data-stu-id="25b48-124">`Microsoft.ApplicationInsights.Extensibility.
TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span></span>

## <a name="see-also"></a><span data-ttu-id="25b48-125">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="25b48-125">See also</span></span>
* [<span data-ttu-id="25b48-126">Crear Application Insights y recursos de pruebas web a partir de plantillas</span><span class="sxs-lookup"><span data-stu-id="25b48-126">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="25b48-127">Configurar la supervisión de diagnósticos de Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="25b48-127">Set up monitoring of Azure diagnostics with PowerShell</span></span>](app-insights-powershell-azure-diagnostics.md) 
* [<span data-ttu-id="25b48-128">Establecimiento de alertas mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="25b48-128">Set alerts by using PowerShell</span></span>](app-insights-powershell-alerts.md)

