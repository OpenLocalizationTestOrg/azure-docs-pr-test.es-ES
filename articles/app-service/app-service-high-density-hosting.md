---
title: hospedaje de densidad de aaaHigh en el servicio de aplicaciones de Azure | Documentos de Microsoft
description: Hospedaje de alta densidad en Azure App Service
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: a903cb78-4927-47b0-8427-56412c4e3e64
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: byvinyal
ms.openlocfilehash: a10cb81ace13ba6992b572a44361061ecf72b266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="high-density-hosting-on-azure-app-service"></a><span data-ttu-id="638f7-103">Hospedaje de alta densidad en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="638f7-103">High density hosting on Azure App Service</span></span>
<span data-ttu-id="638f7-104">Cuando se usa el servicio de aplicaciones, la aplicación se separa de la capacidad de hello asignada tooit por dos conceptos:</span><span class="sxs-lookup"><span data-stu-id="638f7-104">When using App Service, your application is decoupled from hello capacity allocated tooit by two concepts:</span></span>

* <span data-ttu-id="638f7-105">**Hola aplicación:** representa la aplicación hello y su configuración en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="638f7-105">**hello Application:** Represents hello app and its runtime configuration.</span></span> <span data-ttu-id="638f7-106">Por ejemplo, incluye Hola debe cargar la versión de .NET que hello en tiempo de ejecución, configuración de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="638f7-106">For example, it includes hello version of .NET that hello runtime should load, hello app settings.</span></span>
* <span data-ttu-id="638f7-107">**Hola Plan de servicio de aplicaciones:** define Hola características de capacidad de hello, el conjunto de características disponibles y proximidad de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="638f7-107">**hello App Service Plan:** Defines hello characteristics of hello capacity, available feature set, and locality of hello application.</span></span> <span data-ttu-id="638f7-108">Por ejemplo, las características podrían ser una máquina grande (cuatro núcleos), cuatro instancias y características Premium del este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="638f7-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span></span>

<span data-ttu-id="638f7-109">Aplicación siempre está vinculado tooan plan de servicio de aplicaciones, pero un plan de servicio de aplicaciones puede proporcionar capacidad tooone o más aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="638f7-109">An app is always linked tooan App Service plan, but an App Service plan can provide capacity tooone or more apps.</span></span>

<span data-ttu-id="638f7-110">Como resultado, plataforma Hola proporciona Hola flexibilidad tooisolate una única aplicación o tiene varias aplicaciones compartir recursos mediante el uso compartido de un plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="638f7-110">As a result, hello platform provides hello flexibility tooisolate a single app or have multiple apps share resources by sharing an App Service plan.</span></span>

<span data-ttu-id="638f7-111">Sin embargo, cuando varias aplicaciones comparten un plan del Servicio de aplicaciones, una instancia de esa aplicación se ejecuta en cada instancia de ese plan.</span><span class="sxs-lookup"><span data-stu-id="638f7-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span></span>

## <a name="per-app-scaling"></a><span data-ttu-id="638f7-112">Escalado por aplicación</span><span class="sxs-lookup"><span data-stu-id="638f7-112">Per app scaling</span></span>
<span data-ttu-id="638f7-113">*Escalado por aplicación* es una característica que se puede habilitar en el nivel del plan del Servicio de aplicaciones y usar después por aplicación.</span><span class="sxs-lookup"><span data-stu-id="638f7-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span></span>

<span data-ttu-id="638f7-114">El escalado por aplicación escala una aplicación de forma independiente desde el plan del Servicio de aplicaciones que lo hospeda.</span><span class="sxs-lookup"><span data-stu-id="638f7-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span></span> <span data-ttu-id="638f7-115">De esta manera, un servicio de aplicaciones puede ser plan escalar too10 instancias, pero se puede establecer una aplicación toouse solo cinco.</span><span class="sxs-lookup"><span data-stu-id="638f7-115">This way, an App Service plan can be scaled too10 instances, but an app can be set toouse only five.</span></span>

   >[!NOTE]
   ><span data-ttu-id="638f7-116">El escalado por aplicación solo está disponible para los planes de App Service de SKU **premium**.</span><span class="sxs-lookup"><span data-stu-id="638f7-116">Per app scaling is available only for **Premium** SKU App Service plans</span></span>
   >

### <a name="per-app-scaling-using-powershell"></a><span data-ttu-id="638f7-117">Escalado por aplicación mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="638f7-117">Per app scaling using PowerShell</span></span>

<span data-ttu-id="638f7-118">Puede crear un plan configurado como un *por aplicación escalado* plan pasando hello ```-perSiteScaling $true``` atributo toohello ```New-AzureRmAppServicePlan``` commandlet</span><span class="sxs-lookup"><span data-stu-id="638f7-118">You can create a plan configured as a *Per app scaling* plan by passing in hello ```-perSiteScaling $true``` attribute toohello ```New-AzureRmAppServicePlan``` commandlet</span></span>

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

<span data-ttu-id="638f7-119">Si desea que un servicio de aplicación existente tooupdate planear toouse esta característica:</span><span class="sxs-lookup"><span data-stu-id="638f7-119">If you want tooupdate an existing App Service plan toouse this feature:</span></span> 

- <span data-ttu-id="638f7-120">obtener el plan de destino de Hola```Get-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="638f7-120">get hello target plan ```Get-AzureRmAppServicePlan```</span></span>
- <span data-ttu-id="638f7-121">Modificar propiedad de hello localmente```$newASP.PerSiteScaling = $true```</span><span class="sxs-lookup"><span data-stu-id="638f7-121">modifying hello property locally ```$newASP.PerSiteScaling = $true```</span></span>
- <span data-ttu-id="638f7-122">registrar su tooazure de espera de cambios```Set-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="638f7-122">posting your changes back tooazure ```Set-AzureRmAppServicePlan```</span></span> 

```
# Get hello new App Service Plan and modify hello "PerSiteScaling" property.
$newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
$newASP

#Modify hello local copy toouse "PerSiteScaling" property.
$newASP.PerSiteScaling = $true
$newASP
    
#Post updated app service plan back tooazure
Set-AzureRmAppServicePlan $newASP
```

<span data-ttu-id="638f7-123">En el nivel de aplicación Hola, necesitamos tooconfigure número de Hola de instancias que se puede usar la aplicación hello en el plan de servicio de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="638f7-123">At hello app level, we need tooconfigure hello number of instances hello app can use in hello app service plan.</span></span>

<span data-ttu-id="638f7-124">En el ejemplo de Hola a continuación, aplicación hello es tootwo limitado instancias sin tener en cuenta el número de instancias Hola subyacente aplicación servicio plan escalas out a.</span><span class="sxs-lookup"><span data-stu-id="638f7-124">In hello example below, hello app is limited tootwo instances regardless of how many instances hello underlying app service plan scales out to.</span></span>

```
# Get hello app we want tooconfigure toouse "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify hello NumberOfWorkers setting toohello desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back tooazure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> <span data-ttu-id="638f7-125">$newapp.SiteConfig.NumberOfWorkers es diferente de $newapp.MaxNumberOfWorkers.</span><span class="sxs-lookup"><span data-stu-id="638f7-125">$newapp.SiteConfig.NumberOfWorkers is different form $newapp.MaxNumberOfWorkers.</span></span> <span data-ttu-id="638f7-126">Por cada aplicación escala utiliza $newapp. Características de escala de SiteConfig.NumberOfWorkers toodetermine Hola de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="638f7-126">Per app scaling uses $newapp.SiteConfig.NumberOfWorkers toodetermine hello scale characteristics of hello app.</span></span>

### <a name="per-app-scaling-using-azure-resource-manager"></a><span data-ttu-id="638f7-127">Escalado por aplicación mediante Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="638f7-127">Per app scaling using Azure Resource Manager</span></span>

<span data-ttu-id="638f7-128">siguiente Hello *plantilla de Azure Resource Manager* crea:</span><span class="sxs-lookup"><span data-stu-id="638f7-128">hello following *Azure Resource Manager template* creates:</span></span>

- <span data-ttu-id="638f7-129">Un plan de servicio de aplicaciones que se escala too10 instancias</span><span class="sxs-lookup"><span data-stu-id="638f7-129">An App Service plan that's scaled out too10 instances</span></span>
- <span data-ttu-id="638f7-130">una aplicación que ha configurado tooscale tooa máximo de cinco instancias.</span><span class="sxs-lookup"><span data-stu-id="638f7-130">an app that's configured tooscale tooa max of five instances.</span></span>

<span data-ttu-id="638f7-131">Hello plan de servicio de aplicaciones para desarrolladores establece hello **PerSiteScaling** propiedad tootrue ```"perSiteScaling": true```.</span><span class="sxs-lookup"><span data-stu-id="638f7-131">hello App Service plan is setting hello **PerSiteScaling** property tootrue ```"perSiteScaling": true```.</span></span> <span data-ttu-id="638f7-132">aplicación Hello es establecer hello **número de trabajadores** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.</span><span class="sxs-lookup"><span data-stu-id="638f7-132">hello app is setting hello **number of workers** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.</span></span>

```
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters":{
        "appServicePlanName": { "type": "string" },
        "appName": { "type": "string" }
        },
    "resources": [
    {
        "comments": "App Service Plan with per site perSiteScaling = true",
        "type": "Microsoft.Web/serverFarms",
        "sku": {
            "name": "P1",
            "tier": "Premium",
            "size": "P1",
            "family": "P",
            "capacity": 10
            },
        "name": "[parameters('appServicePlanName')]",
        "apiVersion": "2015-08-01",
        "location": "West US",
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "perSiteScaling": true
        }
    },
    {
        "type": "Microsoft.Web/sites",
        "name": "[parameters('appName')]",
        "apiVersion": "2015-08-01-preview",
        "location": "West US",
        "dependsOn": [ "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" ],
        "properties": { "serverFarmId": "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" },
        "resources": [ {
                "comments": "",
                "type": "config",
                "name": "web",
                "apiVersion": "2015-08-01",
                "location": "West US",
                "dependsOn": [ "[resourceId('Microsoft.Web/Sites', parameters('appName'))]" ],
                "properties": { "numberOfWorkers": "5" }
            } ]
        }]
}
```

## <a name="recommended-configuration-for-high-density-hosting"></a><span data-ttu-id="638f7-133">Configuración recomendada para el hospedaje de alta densidad</span><span class="sxs-lookup"><span data-stu-id="638f7-133">Recommended configuration for high density hosting</span></span>
<span data-ttu-id="638f7-134">El escalado por aplicación es una característica que está habilitada en las regiones de Azure globales y los entornos de App Service.</span><span class="sxs-lookup"><span data-stu-id="638f7-134">Per app scaling is a feature that is enabled in both global Azure regions and App Service Environments.</span></span> <span data-ttu-id="638f7-135">Sin embargo, Hola recomendado estrategia consiste en usar sus características avanzadas de aprovechar de tootake entornos del servicio de aplicación y grupos más grandes de Hola de capacidad.</span><span class="sxs-lookup"><span data-stu-id="638f7-135">However, hello recommended strategy is to use App Service Environments tootake advantage of their advanced features and hello larger pools of capacity.</span></span>  

<span data-ttu-id="638f7-136">Siga estos pasos tooconfigure alta densidad para las aplicaciones de hospedaje:</span><span class="sxs-lookup"><span data-stu-id="638f7-136">Follow these steps tooconfigure high density hosting for your apps:</span></span>

1. <span data-ttu-id="638f7-137">Configurar el entorno del servicio de aplicación Hola y elija un grupo de trabajo que está dedicado toohello alta densidad escenario de alojamiento.</span><span class="sxs-lookup"><span data-stu-id="638f7-137">Configure hello App Service Environment and choose a worker pool that is dedicated toohello high density hosting scenario.</span></span>
1. <span data-ttu-id="638f7-138">Crear un único plan de servicio de aplicaciones y escalar toouse todos Hola capacidad disponible en el grupo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="638f7-138">Create a single App Service plan, and scale it toouse all hello available capacity on hello worker pool.</span></span>
1. <span data-ttu-id="638f7-139">Establecer hello PerSiteScaling marca tootrue en hello plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="638f7-139">Set hello PerSiteScaling flag tootrue on hello App Service plan.</span></span>
1. <span data-ttu-id="638f7-140">Nuevas aplicaciones se crean y se asignan toothat plan de servicio de aplicaciones con la **numberOfWorkers** propiedad establecida demasiado**1**.</span><span class="sxs-lookup"><span data-stu-id="638f7-140">New apps are created and assigned toothat App Service plan with the **numberOfWorkers** property set too**1**.</span></span> <span data-ttu-id="638f7-141">Con esta configuración produce Hola mayor densidad posible en este grupo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="638f7-141">Using this configuration yields hello highest density possible on this worker pool.</span></span>
1. <span data-ttu-id="638f7-142">número de Hola de trabajos se puede configurar independientemente por recursos adicionales de toogrant la aplicación según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="638f7-142">hello number of workers can be configured independently per app toogrant additional resources as needed.</span></span> <span data-ttu-id="638f7-143">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="638f7-143">For example:</span></span>
    - <span data-ttu-id="638f7-144">Puede establecer una aplicación de uso elevado **numberOfWorkers** demasiado**3** toohave más capacidad para esa aplicación de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="638f7-144">A high-use app can set **numberOfWorkers** too**3** toohave more processing capacity for that app.</span></span> 
    - <span data-ttu-id="638f7-145">Aplicaciones de poco uso establecería **numberOfWorkers** demasiado**1**.</span><span class="sxs-lookup"><span data-stu-id="638f7-145">Low-use apps would set **numberOfWorkers** too**1**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="638f7-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="638f7-146">Next Steps</span></span>

- [<span data-ttu-id="638f7-147">Introducción detallada sobre los planes de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="638f7-147">Azure App Service plans in-depth overview</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [<span data-ttu-id="638f7-148">Introducción tooApp entorno del servicio</span><span class="sxs-lookup"><span data-stu-id="638f7-148">Introduction tooApp Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
