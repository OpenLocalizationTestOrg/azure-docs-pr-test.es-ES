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
# <a name="high-density-hosting-on-azure-app-service"></a>Hospedaje de alta densidad en Azure App Service
Cuando se usa el servicio de aplicaciones, la aplicación se separa de la capacidad de hello asignada tooit por dos conceptos:

* **Hola aplicación:** representa la aplicación hello y su configuración en tiempo de ejecución. Por ejemplo, incluye Hola debe cargar la versión de .NET que hello en tiempo de ejecución, configuración de la aplicación hello.
* **Hola Plan de servicio de aplicaciones:** define Hola características de capacidad de hello, el conjunto de características disponibles y proximidad de la aplicación hello. Por ejemplo, las características podrían ser una máquina grande (cuatro núcleos), cuatro instancias y características Premium del este de EE. UU.

Aplicación siempre está vinculado tooan plan de servicio de aplicaciones, pero un plan de servicio de aplicaciones puede proporcionar capacidad tooone o más aplicaciones.

Como resultado, plataforma Hola proporciona Hola flexibilidad tooisolate una única aplicación o tiene varias aplicaciones compartir recursos mediante el uso compartido de un plan de servicio de aplicaciones.

Sin embargo, cuando varias aplicaciones comparten un plan del Servicio de aplicaciones, una instancia de esa aplicación se ejecuta en cada instancia de ese plan.

## <a name="per-app-scaling"></a>Escalado por aplicación
*Escalado por aplicación* es una característica que se puede habilitar en el nivel del plan del Servicio de aplicaciones y usar después por aplicación.

El escalado por aplicación escala una aplicación de forma independiente desde el plan del Servicio de aplicaciones que lo hospeda. De esta manera, un servicio de aplicaciones puede ser plan escalar too10 instancias, pero se puede establecer una aplicación toouse solo cinco.

   >[!NOTE]
   >El escalado por aplicación solo está disponible para los planes de App Service de SKU **premium**.
   >

### <a name="per-app-scaling-using-powershell"></a>Escalado por aplicación mediante PowerShell

Puede crear un plan configurado como un *por aplicación escalado* plan pasando hello ```-perSiteScaling $true``` atributo toohello ```New-AzureRmAppServicePlan``` commandlet

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

Si desea que un servicio de aplicación existente tooupdate planear toouse esta característica: 

- obtener el plan de destino de Hola```Get-AzureRmAppServicePlan```
- Modificar propiedad de hello localmente```$newASP.PerSiteScaling = $true```
- registrar su tooazure de espera de cambios```Set-AzureRmAppServicePlan``` 

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

En el nivel de aplicación Hola, necesitamos tooconfigure número de Hola de instancias que se puede usar la aplicación hello en el plan de servicio de aplicación Hola.

En el ejemplo de Hola a continuación, aplicación hello es tootwo limitado instancias sin tener en cuenta el número de instancias Hola subyacente aplicación servicio plan escalas out a.

```
# Get hello app we want tooconfigure toouse "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify hello NumberOfWorkers setting toohello desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back tooazure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> $newapp.SiteConfig.NumberOfWorkers es diferente de $newapp.MaxNumberOfWorkers. Por cada aplicación escala utiliza $newapp. Características de escala de SiteConfig.NumberOfWorkers toodetermine Hola de aplicación hello.

### <a name="per-app-scaling-using-azure-resource-manager"></a>Escalado por aplicación mediante Azure Resource Manager

siguiente Hello *plantilla de Azure Resource Manager* crea:

- Un plan de servicio de aplicaciones que se escala too10 instancias
- una aplicación que ha configurado tooscale tooa máximo de cinco instancias.

Hello plan de servicio de aplicaciones para desarrolladores establece hello **PerSiteScaling** propiedad tootrue ```"perSiteScaling": true```. aplicación Hello es establecer hello **número de trabajadores** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.

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

## <a name="recommended-configuration-for-high-density-hosting"></a>Configuración recomendada para el hospedaje de alta densidad
El escalado por aplicación es una característica que está habilitada en las regiones de Azure globales y los entornos de App Service. Sin embargo, Hola recomendado estrategia consiste en usar sus características avanzadas de aprovechar de tootake entornos del servicio de aplicación y grupos más grandes de Hola de capacidad.  

Siga estos pasos tooconfigure alta densidad para las aplicaciones de hospedaje:

1. Configurar el entorno del servicio de aplicación Hola y elija un grupo de trabajo que está dedicado toohello alta densidad escenario de alojamiento.
1. Crear un único plan de servicio de aplicaciones y escalar toouse todos Hola capacidad disponible en el grupo de trabajo de Hola.
1. Establecer hello PerSiteScaling marca tootrue en hello plan de servicio de aplicaciones.
1. Nuevas aplicaciones se crean y se asignan toothat plan de servicio de aplicaciones con la **numberOfWorkers** propiedad establecida demasiado**1**. Con esta configuración produce Hola mayor densidad posible en este grupo de trabajo.
1. número de Hola de trabajos se puede configurar independientemente por recursos adicionales de toogrant la aplicación según sea necesario. Por ejemplo:
    - Puede establecer una aplicación de uso elevado **numberOfWorkers** demasiado**3** toohave más capacidad para esa aplicación de procesamiento. 
    - Aplicaciones de poco uso establecería **numberOfWorkers** demasiado**1**.

## <a name="next-steps"></a>Pasos siguientes

- [Introducción detallada sobre los planes de Azure App Service](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [Introducción tooApp entorno del servicio](../app-service-web/app-service-app-service-environment-intro.md)
