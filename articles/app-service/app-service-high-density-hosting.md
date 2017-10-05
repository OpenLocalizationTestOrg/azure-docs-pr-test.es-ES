---
title: Hospedaje de alta densidad en Azure App Service | Microsoft Docs
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
ms.openlocfilehash: 459a310a719695f6366470976d857ec2f9d6f4a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="high-density-hosting-on-azure-app-service"></a><span data-ttu-id="e0811-103">Hospedaje de alta densidad en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e0811-103">High density hosting on Azure App Service</span></span>
<span data-ttu-id="e0811-104">Cuando se utilice App Service, la aplicación se desacoplará de la capacidad que se le ha asignado por dos conceptos:</span><span class="sxs-lookup"><span data-stu-id="e0811-104">When using App Service, your application is decoupled from the capacity allocated to it by two concepts:</span></span>

* <span data-ttu-id="e0811-105">**La aplicación:** representa la aplicación y la configuración de su sistema en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="e0811-105">**The Application:** Represents the app and its runtime configuration.</span></span> <span data-ttu-id="e0811-106">Por ejemplo, incluye la versión de .NET que el sistema en tiempo de ejecución debe cargar, la configuración de la aplicación, etc.</span><span class="sxs-lookup"><span data-stu-id="e0811-106">For example, it includes the version of .NET that the runtime should load, the app settings.</span></span>
* <span data-ttu-id="e0811-107">**El plan de App Service:** define las características de la capacidad, el conjunto de características disponibles y la localidad de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0811-107">**The App Service Plan:** Defines the characteristics of the capacity, available feature set, and locality of the application.</span></span> <span data-ttu-id="e0811-108">Por ejemplo, las características podrían ser una máquina grande (cuatro núcleos), cuatro instancias y características Premium del este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="e0811-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span></span>

<span data-ttu-id="e0811-109">Una aplicación siempre está vinculada a un plan del Servicio de aplicaciones, pero un plan del Servicio de aplicaciones puede proporcionar capacidad para una o más aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e0811-109">An app is always linked to an App Service plan, but an App Service plan can provide capacity to one or more apps.</span></span>

<span data-ttu-id="e0811-110">Como resultado, la plataforma ofrece flexibilidad para aislar una sola aplicación o tiene varias aplicaciones que comparten recursos al compartir un plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="e0811-110">As a result, the platform provides the flexibility to isolate a single app or have multiple apps share resources by sharing an App Service plan.</span></span>

<span data-ttu-id="e0811-111">Sin embargo, cuando varias aplicaciones comparten un plan del Servicio de aplicaciones, una instancia de esa aplicación se ejecuta en cada instancia de ese plan.</span><span class="sxs-lookup"><span data-stu-id="e0811-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span></span>

## <a name="per-app-scaling"></a><span data-ttu-id="e0811-112">Escalado por aplicación</span><span class="sxs-lookup"><span data-stu-id="e0811-112">Per app scaling</span></span>
<span data-ttu-id="e0811-113">*Escalado por aplicación* es una característica que se puede habilitar en el nivel del plan del Servicio de aplicaciones y usar después por aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0811-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span></span>

<span data-ttu-id="e0811-114">El escalado por aplicación escala una aplicación de forma independiente desde el plan del Servicio de aplicaciones que lo hospeda.</span><span class="sxs-lookup"><span data-stu-id="e0811-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span></span> <span data-ttu-id="e0811-115">De esta manera, se puede escalar un plan de App Service a 10 instancias, pero se puede configurar una aplicación para usar solo cinco.</span><span class="sxs-lookup"><span data-stu-id="e0811-115">This way, an App Service plan can be scaled to 10 instances, but an app can be set to use only five.</span></span>

   >[!NOTE]
   ><span data-ttu-id="e0811-116">El escalado por aplicación solo está disponible para los planes de App Service de SKU **premium**.</span><span class="sxs-lookup"><span data-stu-id="e0811-116">Per app scaling is available only for **Premium** SKU App Service plans</span></span>
   >

### <a name="per-app-scaling-using-powershell"></a><span data-ttu-id="e0811-117">Escalado por aplicación mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0811-117">Per app scaling using PowerShell</span></span>

<span data-ttu-id="e0811-118">Puede crear un plan configurado como de *escalado por aplicación* pasando el atributo ```-perSiteScaling $true``` al commandlet ```New-AzureRmAppServicePlan```.</span><span class="sxs-lookup"><span data-stu-id="e0811-118">You can create a plan configured as a *Per app scaling* plan by passing in the ```-perSiteScaling $true``` attribute to the ```New-AzureRmAppServicePlan``` commandlet</span></span>

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

<span data-ttu-id="e0811-119">Si desea actualizar un plan de App Service existente para usar esta característica:</span><span class="sxs-lookup"><span data-stu-id="e0811-119">If you want to update an existing App Service plan to use this feature:</span></span> 

- <span data-ttu-id="e0811-120">obtenga el plan de destino ```Get-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="e0811-120">get the target plan ```Get-AzureRmAppServicePlan```</span></span>
- <span data-ttu-id="e0811-121">modifique la propiedad localmente ```$newASP.PerSiteScaling = $true```</span><span class="sxs-lookup"><span data-stu-id="e0811-121">modifying the property locally ```$newASP.PerSiteScaling = $true```</span></span>
- <span data-ttu-id="e0811-122">publique los cambios en Azure ```Set-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="e0811-122">posting your changes back to azure ```Set-AzureRmAppServicePlan```</span></span> 

```
# Get the new App Service Plan and modify the "PerSiteScaling" property.
$newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
$newASP

#Modify the local copy to use "PerSiteScaling" property.
$newASP.PerSiteScaling = $true
$newASP
    
#Post updated app service plan back to azure
Set-AzureRmAppServicePlan $newASP
```

<span data-ttu-id="e0811-123">En el nivel de aplicación, es necesario configurar el número de instancias que puede usar la aplicación en el plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="e0811-123">At the app level, we need to configure the number of instances the app can use in the app service plan.</span></span>

<span data-ttu-id="e0811-124">En el ejemplo siguiente, la aplicación está limitada a dos instancias, independientemente de la cantidad de estas a las que se escale horizontalmente el plan de App Service subyacente.</span><span class="sxs-lookup"><span data-stu-id="e0811-124">In the example below, the app is limited to two instances regardless of how many instances the underlying app service plan scales out to.</span></span>

```
# Get the app we want to configure to use "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify the NumberOfWorkers setting to the desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back to azure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> <span data-ttu-id="e0811-125">$newapp.SiteConfig.NumberOfWorkers es diferente de $newapp.MaxNumberOfWorkers.</span><span class="sxs-lookup"><span data-stu-id="e0811-125">$newapp.SiteConfig.NumberOfWorkers is different form $newapp.MaxNumberOfWorkers.</span></span> <span data-ttu-id="e0811-126">En el escalado por aplicación se usa $newapp.SiteConfig.NumberOfWorkers para determinar las características de escalado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0811-126">Per app scaling uses $newapp.SiteConfig.NumberOfWorkers to determine the scale characteristics of the app.</span></span>

### <a name="per-app-scaling-using-azure-resource-manager"></a><span data-ttu-id="e0811-127">Escalado por aplicación mediante Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e0811-127">Per app scaling using Azure Resource Manager</span></span>

<span data-ttu-id="e0811-128">La siguiente *plantilla de Azure Resource Manager* crea:</span><span class="sxs-lookup"><span data-stu-id="e0811-128">The following *Azure Resource Manager template* creates:</span></span>

- <span data-ttu-id="e0811-129">Un plan de App Service que se escala horizontalmente a 10 instancias.</span><span class="sxs-lookup"><span data-stu-id="e0811-129">An App Service plan that's scaled out to 10 instances</span></span>
- <span data-ttu-id="e0811-130">Una aplicación que está configurada para escalarse hasta un máximo de 5 instancias.</span><span class="sxs-lookup"><span data-stu-id="e0811-130">an app that's configured to scale to a max of five instances.</span></span>

<span data-ttu-id="e0811-131">El plan de App Service es establecer la propiedad **PerSiteScaling** en true ```"perSiteScaling": true```.</span><span class="sxs-lookup"><span data-stu-id="e0811-131">The App Service plan is setting the **PerSiteScaling** property to true ```"perSiteScaling": true```.</span></span> <span data-ttu-id="e0811-132">La aplicación configura el **número de trabajadores** que se va a usar en 5 ```"properties": { "numberOfWorkers": "5" }```.</span><span class="sxs-lookup"><span data-stu-id="e0811-132">The app is setting the **number of workers** to use to 5 ```"properties": { "numberOfWorkers": "5" }```.</span></span>

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

## <a name="recommended-configuration-for-high-density-hosting"></a><span data-ttu-id="e0811-133">Configuración recomendada para el hospedaje de alta densidad</span><span class="sxs-lookup"><span data-stu-id="e0811-133">Recommended configuration for high density hosting</span></span>
<span data-ttu-id="e0811-134">El escalado por aplicación es una característica que está habilitada en las regiones de Azure globales y los entornos de App Service.</span><span class="sxs-lookup"><span data-stu-id="e0811-134">Per app scaling is a feature that is enabled in both global Azure regions and App Service Environments.</span></span> <span data-ttu-id="e0811-135">Sin embargo, la estrategia recomendada es usar entornos del Servicio de aplicaciones para aprovechar sus características avanzadas y los grupos de mayor capacidad.</span><span class="sxs-lookup"><span data-stu-id="e0811-135">However, the recommended strategy is to use App Service Environments to take advantage of their advanced features and the larger pools of capacity.</span></span>  

<span data-ttu-id="e0811-136">Siga estos pasos para configurar el hospedaje de alta densidad para las aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="e0811-136">Follow these steps to configure high density hosting for your apps:</span></span>

1. <span data-ttu-id="e0811-137">Configure el entorno del App Service y elija un grupo de trabajo dedicado al escenario de hospedaje de alta densidad.</span><span class="sxs-lookup"><span data-stu-id="e0811-137">Configure the App Service Environment and choose a worker pool that is dedicated to the high density hosting scenario.</span></span>
1. <span data-ttu-id="e0811-138">Cree un único plan del Servicio de aplicaciones y escálelo para que utilice toda la capacidad disponible en el grupo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e0811-138">Create a single App Service plan, and scale it to use all the available capacity on the worker pool.</span></span>
1. <span data-ttu-id="e0811-139">Establezca la marca PerSiteScaling en true en el plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="e0811-139">Set the PerSiteScaling flag to true on the App Service plan.</span></span>
1. <span data-ttu-id="e0811-140">Las nuevas aplicaciones se crean y se asignan al plan de App Service con la propiedad **numberOfWorkers** establecida en **1**.</span><span class="sxs-lookup"><span data-stu-id="e0811-140">New apps are created and assigned to that App Service plan with the **numberOfWorkers** property set to **1**.</span></span> <span data-ttu-id="e0811-141">El uso de esta configuración produciría la máxima densidad posible en este grupo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e0811-141">Using this configuration yields the highest density possible on this worker pool.</span></span>
1. <span data-ttu-id="e0811-142">El número de trabajadores se puede configurar por separado por cada aplicación para conceder recursos adicionales según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e0811-142">The number of workers can be configured independently per app to grant additional resources as needed.</span></span> <span data-ttu-id="e0811-143">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e0811-143">For example:</span></span>
    - <span data-ttu-id="e0811-144">En una aplicación de uso elevado, puede establecer **numberOfWorkers** en **3** para que haya una mayor capacidad de procesamiento para esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0811-144">A high-use app can set **numberOfWorkers** to **3** to have more processing capacity for that app.</span></span> 
    - <span data-ttu-id="e0811-145">En las aplicaciones de poco uso se establecerá **numberOfWorkers** en **1**.</span><span class="sxs-lookup"><span data-stu-id="e0811-145">Low-use apps would set **numberOfWorkers** to **1**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0811-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e0811-146">Next Steps</span></span>

- [<span data-ttu-id="e0811-147">Introducción detallada sobre los planes de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e0811-147">Azure App Service plans in-depth overview</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [<span data-ttu-id="e0811-148">Introducción al entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e0811-148">Introduction to App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)