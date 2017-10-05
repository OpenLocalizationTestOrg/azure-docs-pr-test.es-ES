---
title: Script de PowerShell para crear un recurso de Application Insights | Microsoft Docs
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
ms.openlocfilehash: a828af9c7d207dd84cc626fc70206018fd67e2dd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="powershell-script-to-create-an-application-insights-resource"></a><span data-ttu-id="29989-103">Script de PowerShell para crear un recurso de Application Insights</span><span class="sxs-lookup"><span data-stu-id="29989-103">PowerShell script to create an Application Insights resource</span></span>


<span data-ttu-id="29989-104">Cuando desee supervisar una nueva aplicación —o una nueva versión de una aplicación— con [Application Insights para Visual Studio](https://azure.microsoft.com/services/application-insights/), configure un recurso nuevo en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="29989-104">When you want to monitor a new application - or a new version of an application - with [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), you set up a new resource in Microsoft Azure.</span></span> <span data-ttu-id="29989-105">Este recurso es donde se analizan y muestran los datos de telemetría procedentes de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="29989-105">This resource is where the telemetry data from your app is analyzed and displayed.</span></span> 

<span data-ttu-id="29989-106">Puede automatizar la creación de un nuevo recurso mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29989-106">You can automate the creation of a new resource by using PowerShell.</span></span>

<span data-ttu-id="29989-107">Por ejemplo, si está desarrollando una aplicación de dispositivo móvil, es probable que, en cualquier momento, haya varias versiones publicadas de la aplicación en uso por los clientes.</span><span class="sxs-lookup"><span data-stu-id="29989-107">For example, if you are developing a mobile device app, it's likely that, at any time, there will be several published versions of your app in use by your customers.</span></span> <span data-ttu-id="29989-108">No querrá obtener los resultados de telemetría mezclados de las diferentes versiones.</span><span class="sxs-lookup"><span data-stu-id="29989-108">You don't want to get the telemetry results from different versions mixed up.</span></span> <span data-ttu-id="29989-109">Por tanto, hará que el proceso de compilación cree un nuevo recurso para cada compilación.</span><span class="sxs-lookup"><span data-stu-id="29989-109">So you get your build process to create a new resource for each build.</span></span>

> [!NOTE]
> <span data-ttu-id="29989-110">Si desea crear un conjunto de recursos todos al mismo tiempo, considere la posibilidad de [crear los recursos mediante una plantilla de Azure](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="29989-110">If you want to create a set of resources all at the same time, consider [creating the resources using an Azure template](app-insights-powershell.md).</span></span>
> 
> 

## <a name="script-to-create-an-application-insights-resource"></a><span data-ttu-id="29989-111">Script para crear un recurso en Application Insights</span><span class="sxs-lookup"><span data-stu-id="29989-111">Script to create an Application Insights resource</span></span>
<span data-ttu-id="29989-112">Consulte las especificaciones de cmdlet pertinentes:</span><span class="sxs-lookup"><span data-stu-id="29989-112">See the relevant cmdlet specs:</span></span>

* [<span data-ttu-id="29989-113">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="29989-113">New-AzureRmResource</span></span>](https://msdn.microsoft.com/library/mt652510.aspx)
* [<span data-ttu-id="29989-114">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="29989-114">New-AzureRmRoleAssignment</span></span>](https://msdn.microsoft.com/library/mt678995.aspx)

<span data-ttu-id="29989-115">*Script de PowerShell*</span><span class="sxs-lookup"><span data-stu-id="29989-115">*PowerShell Script*</span></span>  

```PowerShell


###########################################
# Set Values
###########################################

# If running manually, uncomment before the first 
# execution to login to the Azure Portal:

# Add-AzureRmAccount / Login-AzureRmAccount

# Set the name of the Application Insights Resource

$appInsightsName = "TestApp"

# Set the application name used for the value of the Tag "AppInsightsApp" 

$applicationTagName = "MyApp"

# Set the name of the Resource Group to use.  
# Default is the application name.
$resourceGroupName = "MyAppResourceGroup"

###################################################
# Create the Resource and Output the name and iKey
###################################################

# Select the azure subscription
Select-AzureSubscription -SubscriptionName "MySubscription"

# Create the App Insights Resource


$resource = New-AzureRmResource `
  -ResourceName $appInsightsName `
  -ResourceGroupName $resourceGroupName `
  -Tag @{ applicationType = "web"; applicationName = $applicationTagName} `
  -ResourceType "Microsoft.Insights/components" `
  -Location "East US" `  # or North Europe, West Europe, South Central US
  -PropertyObject @{"Application_Type"="web"} `
  -Force

# Give owner access to the team

New-AzureRmRoleAssignment `
  -SignInName "myteam@fabrikam.com" `
  -RoleDefinitionName Owner `
  -Scope $resource.ResourceId 


# Display iKey
Write-Host "App Insights Name = " $resource.Name
Write-Host "IKey = " $resource.Properties.InstrumentationKey

```

## <a name="what-to-do-with-the-ikey"></a><span data-ttu-id="29989-116">Qué hacer con el valor iKey</span><span class="sxs-lookup"><span data-stu-id="29989-116">What to do with the iKey</span></span>
<span data-ttu-id="29989-117">Cada recurso se identifica por su clave de instrumentación (iKey).</span><span class="sxs-lookup"><span data-stu-id="29989-117">Each resource is identified by its instrumentation key (iKey).</span></span> <span data-ttu-id="29989-118">El valor iKey es un resultado del script de creación de recursos.</span><span class="sxs-lookup"><span data-stu-id="29989-118">The iKey is an output of the resource creation script.</span></span> <span data-ttu-id="29989-119">El script de compilación debe proporcionar el valor iKey al SDK de Application Insights insertado en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="29989-119">Your build script should provide the iKey to the Application Insights SDK embedded in your app.</span></span>

<span data-ttu-id="29989-120">Hay dos maneras de hacer que el valor iKey esté disponible para el SDK:</span><span class="sxs-lookup"><span data-stu-id="29989-120">There are two ways to make the iKey available to the SDK:</span></span>

* <span data-ttu-id="29989-121">En [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="29989-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span> 
  * <span data-ttu-id="29989-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span><span class="sxs-lookup"><span data-stu-id="29989-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span></span>
* <span data-ttu-id="29989-123">O bien en el [código de inicialización](app-insights-api-custom-events-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="29989-123">Or in [initialization code](app-insights-api-custom-events-metrics.md):</span></span> 
  * <span data-ttu-id="29989-124">`Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span><span class="sxs-lookup"><span data-stu-id="29989-124">`Microsoft.ApplicationInsights.Extensibility.
TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span></span>

## <a name="see-also"></a><span data-ttu-id="29989-125">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="29989-125">See also</span></span>
* [<span data-ttu-id="29989-126">Crear Application Insights y recursos de pruebas web a partir de plantillas</span><span class="sxs-lookup"><span data-stu-id="29989-126">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="29989-127">Configurar la supervisión de diagnósticos de Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="29989-127">Set up monitoring of Azure diagnostics with PowerShell</span></span>](app-insights-powershell-azure-diagnostics.md) 
* [<span data-ttu-id="29989-128">Establecimiento de alertas mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="29989-128">Set alerts by using PowerShell</span></span>](app-insights-powershell-alerts.md)

