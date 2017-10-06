---
title: "aaaAutomate visión de la aplicación de Azure con PowerShell | Documentos de Microsoft"
description: "Automatice la creación de recursos, alertas y pruebas de disponibilidad en PowerShell mediante una plantilla de Azure Resource Manager."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9f73b87f-be63-4847-88c8-368543acad8b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: bwren
ms.openlocfilehash: ebd336eafba58a690a0e8ffbd1c74f7e93dbb682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
#  <a name="create-application-insights-resources-using-powershell"></a><span data-ttu-id="3841b-103">Creación de recursos de Application Insights mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="3841b-103">Create Application Insights resources using PowerShell</span></span>
<span data-ttu-id="3841b-104">Este artículo muestra cómo tooautomate Hola creación y actualización de [Application Insights](app-insights-overview.md) recursos automáticamente mediante el uso de administración de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="3841b-104">This article shows you how tooautomate hello creation and update of [Application Insights](app-insights-overview.md) resources automatically by using Azure Resource Management.</span></span> <span data-ttu-id="3841b-105">Puede hacerlo, por ejemplo, como parte de un proceso de compilación.</span><span class="sxs-lookup"><span data-stu-id="3841b-105">You might, for example, do so as part of a build process.</span></span> <span data-ttu-id="3841b-106">Junto con el recurso de Application Insights de hello básico, puede crear [disponibilidad las pruebas web](app-insights-monitor-web-app-availability.md), configuraré [alertas](app-insights-alerts.md), hello establezca [precios esquema](app-insights-pricing.md)y crear otro Azure recursos.</span><span class="sxs-lookup"><span data-stu-id="3841b-106">Along with hello basic Application Insights resource, you can create [availability web tests](app-insights-monitor-web-app-availability.md), set up [alerts](app-insights-alerts.md), set hello [pricing scheme](app-insights-pricing.md), and create other Azure resources.</span></span>

<span data-ttu-id="3841b-107">Hola toocreating clave estos recursos son las plantillas de JSON para [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="3841b-107">hello key toocreating these resources is JSON templates for [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span> <span data-ttu-id="3841b-108">En pocas palabras, es el procedimiento de hello: Descargar Hola JSON definiciones de recursos existentes; parametrizar determinados valores como los nombres; y, a continuación, ejecute plantilla Hola siempre que lo desee toocreate un nuevo recurso.</span><span class="sxs-lookup"><span data-stu-id="3841b-108">In a nutshell, hello procedure is: download hello JSON definitions of existing resources; parameterize certain values such as names; and then run hello template whenever you want toocreate a new resource.</span></span> <span data-ttu-id="3841b-109">Puede empaquetar varios recursos juntos, toocreate que todo en uno Enhorabuena: por ejemplo, un monitor de aplicaciones con pruebas de disponibilidad, las alertas y almacenamiento para la exportación continua.</span><span class="sxs-lookup"><span data-stu-id="3841b-109">You can package several resources together, toocreate them all in one go - for example, an app monitor with availability tests, alerts, and storage for continuous export.</span></span> <span data-ttu-id="3841b-110">No hay algunos toosome matices de parametrizaciones hello, que se explican aquí.</span><span class="sxs-lookup"><span data-stu-id="3841b-110">There are some subtleties toosome of hello parameterizations, which we'll explain here.</span></span>

## <a name="one-time-setup"></a><span data-ttu-id="3841b-111">Instalación única</span><span class="sxs-lookup"><span data-stu-id="3841b-111">One-time setup</span></span>
<span data-ttu-id="3841b-112">Si no ha usado PowerShell con su suscripción de Azure antes:</span><span class="sxs-lookup"><span data-stu-id="3841b-112">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="3841b-113">Instale el módulo de Powershell de Azure de hello en la máquina de Hola donde desea que las secuencias de comandos de toorun hello:</span><span class="sxs-lookup"><span data-stu-id="3841b-113">Install hello Azure Powershell module on hello machine where you want toorun hello scripts:</span></span>

1. <span data-ttu-id="3841b-114">Instale el [Instalador de plataforma web de Microsoft (v5 o superior)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="3841b-114">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
2. <span data-ttu-id="3841b-115">Usar tooinstall Microsoft Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="3841b-115">Use it tooinstall Microsoft Azure Powershell.</span></span>

## <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="3841b-116">Creación de una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3841b-116">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="3841b-117">Cree un nuevo archivo .json. Vamos a llamarlo `template1.json` en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3841b-117">Create a new .json file - let's call it `template1.json` in this example.</span></span> <span data-ttu-id="3841b-118">Copie este contenido en él:</span><span class="sxs-lookup"><span data-stu-id="3841b-118">Copy this content into it:</span></span>

```JSON
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "appName": {
                "type": "string",
                "metadata": {
                    "description": "Enter hello application name."
                }
            },
            "appType": {
                "type": "string",
                "defaultValue": "web",
                "allowedValues": [
                    "web",
                    "java",
                    "HockeyAppBridge",
                    "other"
                ],
                "metadata": {
                    "description": "Enter hello application type."
                }
            },
            "appLocation": {
                "type": "string",
                "defaultValue": "East US",
                "allowedValues": [
                    "South Central US",
                    "West Europe",
                    "East US",
                    "North Europe"
                ],
                "metadata": {
                    "description": "Enter hello application location."
                }
            },
            "priceCode": {
                "type": "int",
                "defaultValue": 1,
                "allowedValues": [
                    1,
                    2
                ],
                "metadata": {
                    "description": "1 = Basic, 2 = Enterprise"
                }
            },
            "dailyQuota": {
                "type": "int",
                "defaultValue": 100,
                "minValue": 1,
                "metadata": {
                    "description": "Enter daily quota in GB."
                }
            },
            "dailyQuotaResetTime": {
                "type": "int",
                "defaultValue": 24,
                "metadata": {
                    "description": "Enter daily quota reset hour in UTC (0 too23). Values outside hello range will get a random reset hour."
                }
            },
            "warningThreshold": {
                "type": "int",
                "defaultValue": 90,
                "minValue": 1,
                "maxValue": 100,
                "metadata": {
                    "description": "Enter hello % value of daily quota after which warning mail toobe sent. "
                }
            }
        },
        "variables": {
            "priceArray": [
                "Basic",
                "Application Insights Enterprise"
            ],
            "pricePlan": "[take(variables('priceArray'),parameters('priceCode'))]",
            "billingplan": "[concat(parameters('appName'),'/', variables('pricePlan')[0])]"
        },
        "resources": [
            {
                "type": "microsoft.insights/components",
                "kind": "[parameters('appType')]",
                "name": "[parameters('appName')]",
                "apiVersion": "2014-04-01",
                "location": "[parameters('appLocation')]",
                "tags": {},
                "properties": {
                    "ApplicationId": "[parameters('appName')]"
                },
                "dependsOn": []
            },
            {
                "name": "[variables('billingplan')]",
                "type": "microsoft.insights/components/CurrentBillingFeatures",
                "location": "[parameters('appLocation')]",
                "apiVersion": "2015-05-01",
                "dependsOn": [
                    "[resourceId('microsoft.insights/components', parameters('appName'))]"
                ],
                "properties": {
                    "CurrentBillingFeatures": "[variables('pricePlan')]",
                    "DataVolumeCap": {
                        "Cap": "[parameters('dailyQuota')]",
                        "WarningThreshold": "[parameters('warningThreshold')]",
                        "ResetTime": "[parameters('dailyQuotaResetTime')]"
                    }
                }
            }
        ]
    }
```



## <a name="create-application-insights-resources"></a><span data-ttu-id="3841b-119">Creación de recursos de Application Insights</span><span class="sxs-lookup"><span data-stu-id="3841b-119">Create Application Insights resources</span></span>
1. <span data-ttu-id="3841b-120">En PowerShell, inicie sesión en tooAzure:</span><span class="sxs-lookup"><span data-stu-id="3841b-120">In PowerShell, sign in tooAzure:</span></span>
   
    `Login-AzureRmAccount`
2. <span data-ttu-id="3841b-121">Ejecute un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="3841b-121">Run a command like this:</span></span>
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * <span data-ttu-id="3841b-122">`-ResourceGroupName`es grupo de Hola donde desea nuevos recursos de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="3841b-122">`-ResourceGroupName` is hello group where you want toocreate hello new resources.</span></span>
   * <span data-ttu-id="3841b-123">`-TemplateFile`debe aparecer antes de parámetros personalizados Hola.</span><span class="sxs-lookup"><span data-stu-id="3841b-123">`-TemplateFile` must occur before hello custom parameters.</span></span>
   * <span data-ttu-id="3841b-124">`-appName`nombre de Hola de hello recursos toocreate.</span><span class="sxs-lookup"><span data-stu-id="3841b-124">`-appName` hello name of hello resource toocreate.</span></span>

<span data-ttu-id="3841b-125">Puede agregar otros parámetros: encontrará sus descripciones en la sección de parámetros de Hola de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="3841b-125">You can add other parameters - you'll find their descriptions in hello parameters section of hello template.</span></span>

## <a name="tooget-hello-instrumentation-key"></a><span data-ttu-id="3841b-126">clave de instrumentación de hello tooget</span><span class="sxs-lookup"><span data-stu-id="3841b-126">tooget hello instrumentation key</span></span>
<span data-ttu-id="3841b-127">Después de crear un recurso de aplicación, querrá clave de instrumentación de hello:</span><span class="sxs-lookup"><span data-stu-id="3841b-127">After creating an application resource, you'll want hello instrumentation key:</span></span> 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-hello-price-plan"></a><span data-ttu-id="3841b-128">Establecer plan de precios de Hola</span><span class="sxs-lookup"><span data-stu-id="3841b-128">Set hello price plan</span></span>

<span data-ttu-id="3841b-129">Puede establecer hello [plan de precios](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="3841b-129">You can set hello [price plan](app-insights-pricing.md).</span></span>

<span data-ttu-id="3841b-130">toocreate un recurso de aplicación con plan de precios de Enterprise hello, con plantilla Hola anterior:</span><span class="sxs-lookup"><span data-stu-id="3841b-130">toocreate an app resource with hello Enterprise price plan, using hello template above:</span></span>

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|<span data-ttu-id="3841b-131">priceCode</span><span class="sxs-lookup"><span data-stu-id="3841b-131">priceCode</span></span>|<span data-ttu-id="3841b-132">plan</span><span class="sxs-lookup"><span data-stu-id="3841b-132">plan</span></span>|
|---|---|
|<span data-ttu-id="3841b-133">1</span><span class="sxs-lookup"><span data-stu-id="3841b-133">1</span></span>|<span data-ttu-id="3841b-134">Básico</span><span class="sxs-lookup"><span data-stu-id="3841b-134">Basic</span></span>|
|<span data-ttu-id="3841b-135">2</span><span class="sxs-lookup"><span data-stu-id="3841b-135">2</span></span>|<span data-ttu-id="3841b-136">Enterprise</span><span class="sxs-lookup"><span data-stu-id="3841b-136">Enterprise</span></span>|

* <span data-ttu-id="3841b-137">Si solo desea plan de precios básico de toouse Hola predeterminado, puede omitir hello CurrentBillingFeatures provienen de la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="3841b-137">If you only want toouse hello default Basic price plan, you can omit hello CurrentBillingFeatures resource from hello template.</span></span>
* <span data-ttu-id="3841b-138">Si desea plan de precios de hello toochange después de que se ha creado el recurso de componente de hello, puede usar una plantilla que omite el recurso de Hola "Type Microsoft.Insights/Components".</span><span class="sxs-lookup"><span data-stu-id="3841b-138">If you want toochange hello price plan after hello component resource has been created, you can use a template that omits hello "microsoft.insights/components" resource.</span></span> <span data-ttu-id="3841b-139">Además, omitir hello `dependsOn` nodo de hello recursos de facturación.</span><span class="sxs-lookup"><span data-stu-id="3841b-139">Also, omit hello `dependsOn` node from hello billing resource.</span></span> 

<span data-ttu-id="3841b-140">tooverify Hola plan de precios actualizada, buscar en la hoja de Hola "Características + precios" en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="3841b-140">tooverify hello updated price plan, look at hello "Features+pricing" blade in hello browser.</span></span> <span data-ttu-id="3841b-141">**Actualizar vista del explorador de hello** toomake asegurarse de ver el estado más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="3841b-141">**Refresh hello browser view** toomake sure you see hello latest state.</span></span>



## <a name="add-a-metric-alert"></a><span data-ttu-id="3841b-142">Agregar una alerta de métrica</span><span class="sxs-lookup"><span data-stu-id="3841b-142">Add a metric alert</span></span>

<span data-ttu-id="3841b-143">tooset una alerta métrica en hello mismo tiempo como el recurso de aplicación, mezcla código similar al siguiente en el archivo de plantilla de hello:</span><span class="sxs-lookup"><span data-stu-id="3841b-143">tooset up a metric alert at hello same time as your app resource, merge code like this into hello template file:</span></span>

```JSON
{
    parameters: { ... // existing parameters ...
            "responseTime": {
              "type": "int",
              "defaultValue": 3,
              "minValue": 1,
              "metadata": {
                "description": "Enter response time threshold in seconds."
              }
    },
    variables: { ... // existing variables ...
      // Alert names must be unique within resource group.
      "responseAlertName": "[concat('ResponseTime-', toLower(parameters('appName')))]"
    }, 
    resources: { ... // existing resources ...
     {
      //
      // Metric alert on response time
      //
      "name": "[variables('responseAlertName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this resource is created after hello app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('responseAlertName')]",
        "description": "response time alert",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/components', parameters('appName'))]",
            "metricName": "request.duration"
          },
          "threshold": "[parameters('responseTime')]", //seconds
          "windowSize": "PT15M" // Take action if changed state for 15 minutes
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

<span data-ttu-id="3841b-144">Cuando se invoca la plantilla de hello, opcionalmente, puede agregar este parámetro:</span><span class="sxs-lookup"><span data-stu-id="3841b-144">When you invoke hello template, you can optionally add this parameter:</span></span>

    `-responseTime 2`

<span data-ttu-id="3841b-145">También puede parametrizar otros campos.</span><span class="sxs-lookup"><span data-stu-id="3841b-145">You can of course parameterize other fields.</span></span> 

<span data-ttu-id="3841b-146">toofind los nombres de tipo hello y detalles de configuración de otras reglas de alerta, crear una regla manualmente y, a continuación, inspeccione en [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3841b-146">toofind out hello type names and configuration details of other alert rules, create a rule manually and then inspect it in [Azure Resource Manager](https://resources.azure.com/).</span></span> 


## <a name="add-an-availability-test"></a><span data-ttu-id="3841b-147">Agregar una prueba de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="3841b-147">Add an availability test</span></span>

<span data-ttu-id="3841b-148">En este ejemplo es para una prueba de ping (tootest una sola página).</span><span class="sxs-lookup"><span data-stu-id="3841b-148">This example is for a ping test (tootest a single page).</span></span>  

<span data-ttu-id="3841b-149">**Hay dos partes** en una prueba de disponibilidad: propia prueba de Hola y alerta de Hola que le informa de errores.</span><span class="sxs-lookup"><span data-stu-id="3841b-149">**There are two parts** in an availability test: hello test itself, and hello alert that notifies you of failures.</span></span>

<span data-ttu-id="3841b-150">Combinar Hola siguiente código en el archivo de plantilla de Hola que crea la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="3841b-150">Merge hello following code into hello template file that creates hello app.</span></span>

```JSON
{
    parameters: { ... // existing parameters here ...
      "pingURL": { "type": "string" },
      "pingText": { "type": "string" , defaultValue: ""}
    },
    variables: { ... // existing variables here ...
      "pingTestName":"[concat('PingTest-', toLower(parameters('appName')))]",
      "pingAlertRuleName": "[concat('PingAlert-', toLower(parameters('appName')), '-', subscription().subscriptionId)]"
    },
    resources: { ... // existing resources here ...
    { //
      // Availability test: part 1 configures hello test
      //
      "name": "[variables('pingTestName')]",
      "type": "Microsoft.Insights/webtests",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this is created after hello app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "Name": "[variables('pingTestName')]",
        "Description": "Basic ping test",
        "Enabled": true,
        "Frequency": 900, // 15 minutes
        "Timeout": 120, // 2 minutes
        "Kind": "ping", // single URL test
        "RetryEnabled": true,
        "Locations": [
          {
            "Id": "us-va-ash-azr"
          },
          {
            "Id": "emea-nl-ams-azr"
          },
          {
            "Id": "apac-jp-kaw-edge"
          }
        ],
        "Configuration": {
          "WebTest": "[concat('<WebTest   Name=\"', variables('pingTestName'), '\"   Enabled=\"True\"         CssProjectStructure=\"\"    CssIteration=\"\"  Timeout=\"120\"  WorkItemIds=\"\"         xmlns=\"http://microsoft.com/schemas/VisualStudio/TeamTest/2010\"         Description=\"\"  CredentialUserName=\"\"  CredentialPassword=\"\"         PreAuthenticate=\"True\"  Proxy=\"default\"  StopOnError=\"False\"         RecordedResultFile=\"\"  ResultsLocale=\"\">  <Items>  <Request Method=\"GET\"    Version=\"1.1\"  Url=\"', parameters('Url'),   '\" ThinkTime=\"0\"  Timeout=\"300\" ParseDependentRequests=\"True\"         FollowRedirects=\"True\" RecordResult=\"True\" Cache=\"False\"         ResponseTimeGoal=\"0\"  Encoding=\"utf-8\"  ExpectedHttpStatusCode=\"200\"         ExpectedResponseUrl=\"\" ReportingName=\"\" IgnoreHttpStatusCode=\"False\" />        </Items>  <ValidationRules> <ValidationRule  Classname=\"Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleFindText, Microsoft.VisualStudio.QualityTools.WebTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a\" DisplayName=\"Find Text\"         Description=\"Verifies hello existence of hello specified text in hello response.\"         Level=\"High\"  ExectuionOrder=\"BeforeDependents\">  <RuleParameters>        <RuleParameter Name=\"FindText\" Value=\"',   parameters('pingText'), '\" />  <RuleParameter Name=\"IgnoreCase\" Value=\"False\" />  <RuleParameter Name=\"UseRegularExpression\" Value=\"False\" />  <RuleParameter Name=\"PassIfTextFound\" Value=\"True\" />  </RuleParameters> </ValidationRule>  </ValidationRules>  </WebTest>')]"
        },
        "SyntheticMonitorId": "[variables('pingTestName')]"
      }
    },

    {
      //
      // Availability test: part 2, hello alert rule
      //
      "name": "[variables('pingAlertRuleName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]", 
      "dependsOn": [
        "[resourceId('Microsoft.Insights/webtests', variables('pingTestName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource",
        "[concat('hidden-link:', resourceId('Microsoft.Insights/webtests', variables('pingTestName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('pingAlertRuleName')]",
        "description": "alert for web test",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.LocationThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.LocationThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/webtests', variables('pingTestName'))]",
            "metricName": "GSMT_AvRaW"
          },
          "windowSize": "PT15M", // Take action if changed state for 15 minutes
          "failedLocationCount": 2
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

<span data-ttu-id="3841b-151">códigos de hello toodiscover para otras ubicaciones de prueba, o la creación de hello de tooautomate de pruebas web más complejas, un ejemplo de cómo crear manualmente y, a continuación, se parametrizan código de hello de [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3841b-151">toodiscover hello codes for other test locations, or tooautomate hello creation of more complex web tests, create an example manually and then parameterize hello code from [Azure Resource Manager](https://resources.azure.com/).</span></span>

## <a name="add-more-resources"></a><span data-ttu-id="3841b-152">Agregar más recursos</span><span class="sxs-lookup"><span data-stu-id="3841b-152">Add more resources</span></span>

<span data-ttu-id="3841b-153">creación de hello tooautomate de cualquier otro recurso de cualquier tipo, un ejemplo de cómo crear manualmente y, a continuación, copie y parametrizar su código de [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3841b-153">tooautomate hello creation of any other resource of any kind, create an example manually, and then copy and parameterize its code from [Azure Resource Manager](https://resources.azure.com/).</span></span> 

1. <span data-ttu-id="3841b-154">Abra el [Administrador de recursos de Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3841b-154">Open [Azure Resource Manager](https://resources.azure.com/).</span></span> <span data-ttu-id="3841b-155">Navegar hacia abajo por `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour de recursos de aplicación.</span><span class="sxs-lookup"><span data-stu-id="3841b-155">Navigate down through `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour application resource.</span></span> 
   
    ![Navegación en el Explorador de recursos de Azure](./media/app-insights-powershell/01.png)
   
    <span data-ttu-id="3841b-157">*Componentes* es Hola recursos básicos de Application Insights para mostrar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3841b-157">*Components* are hello basic Application Insights resources for displaying applications.</span></span> <span data-ttu-id="3841b-158">Hay recursos independientes para hello asociados a las reglas de alertas y las pruebas de web de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="3841b-158">There are separate resources for hello associated alert rules and availability web tests.</span></span>
2. <span data-ttu-id="3841b-159">Hola copia JSON del componente de hello en el lugar adecuado de hello en `template1.json`.</span><span class="sxs-lookup"><span data-stu-id="3841b-159">Copy hello JSON of hello component into hello appropriate place in `template1.json`.</span></span>
3. <span data-ttu-id="3841b-160">Elimine estas propiedades:</span><span class="sxs-lookup"><span data-stu-id="3841b-160">Delete these properties:</span></span>
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. <span data-ttu-id="3841b-161">Abra secciones de pruebas Web y alertrules hello y copie hello JSON para elementos individuales en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="3841b-161">Open hello webtests and alertrules sections and copy hello JSON for individual items into your template.</span></span> <span data-ttu-id="3841b-162">(No se copian de los nodos de pruebas Web o alertrules Hola: vaya a elementos de hello en ellos.)</span><span class="sxs-lookup"><span data-stu-id="3841b-162">(Don't copy from hello webtests or alertrules nodes: go into hello items under them.)</span></span>
   
    <span data-ttu-id="3841b-163">Cada prueba web tiene una regla de alerta asociada, por lo que tendrá toocopy de ellos.</span><span class="sxs-lookup"><span data-stu-id="3841b-163">Each web test has an associated alert rule, so you have toocopy both of them.</span></span>
   
    <span data-ttu-id="3841b-164">También puede incluir alertas en las métricas.</span><span class="sxs-lookup"><span data-stu-id="3841b-164">You can also include alerts on metrics.</span></span> <span data-ttu-id="3841b-165">[Nombres de métricas](app-insights-powershell-alerts.md#metric-names).</span><span class="sxs-lookup"><span data-stu-id="3841b-165">[Metric names](app-insights-powershell-alerts.md#metric-names).</span></span>
5. <span data-ttu-id="3841b-166">Inserte esta línea en cada recurso:</span><span class="sxs-lookup"><span data-stu-id="3841b-166">Insert this line in each resource:</span></span>
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-hello-template"></a><span data-ttu-id="3841b-167">Parametrizar la plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="3841b-167">Parameterize hello template</span></span>
<span data-ttu-id="3841b-168">Ahora tiene nombres específicos de hello tooreplace con parámetros.</span><span class="sxs-lookup"><span data-stu-id="3841b-168">Now you have tooreplace hello specific names with parameters.</span></span> <span data-ttu-id="3841b-169">demasiado[parametrizar una plantilla](../azure-resource-manager/resource-group-authoring-templates.md), escribir expresiones que utilizan un [conjunto de funciones auxiliares](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="3841b-169">too[parameterize a template](../azure-resource-manager/resource-group-authoring-templates.md), you write expressions using a [set of helper functions](../azure-resource-manager/resource-group-template-functions.md).</span></span> 

<span data-ttu-id="3841b-170">No se puede parametrizar sólo una parte de una cadena, por lo que usar `concat()` toobuild cadenas.</span><span class="sxs-lookup"><span data-stu-id="3841b-170">You can't parameterize just part of a string, so use `concat()` toobuild strings.</span></span>

<span data-ttu-id="3841b-171">Estos son ejemplos de sustituciones Hola querrá toomake.</span><span class="sxs-lookup"><span data-stu-id="3841b-171">Here are examples of hello substitutions you'll want toomake.</span></span> <span data-ttu-id="3841b-172">Hay varias repeticiones de cada sustitución.</span><span class="sxs-lookup"><span data-stu-id="3841b-172">There are several occurrences of each substitution.</span></span> <span data-ttu-id="3841b-173">Y puede que tenga otras en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="3841b-173">You might need others in your template.</span></span> <span data-ttu-id="3841b-174">Estos ejemplos utilizan parámetros de Hola y las variables que se ha definido en parte superior de Hola de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="3841b-174">These examples use hello parameters and variables we defined at hello top of hello template.</span></span>

| <span data-ttu-id="3841b-175">find</span><span class="sxs-lookup"><span data-stu-id="3841b-175">find</span></span> | <span data-ttu-id="3841b-176">reemplazar por</span><span class="sxs-lookup"><span data-stu-id="3841b-176">replace with</span></span> |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| <span data-ttu-id="3841b-177">`"myappname"` (minúscula)</span><span class="sxs-lookup"><span data-stu-id="3841b-177">`"myappname"` (lower case)</span></span> |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/><span data-ttu-id="3841b-178">Elimine el Guid y el identificador.</span><span class="sxs-lookup"><span data-stu-id="3841b-178">Delete Guid and Id.</span></span> |

### <a name="set-dependencies-between-hello-resources"></a><span data-ttu-id="3841b-179">Definir dependencias entre recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="3841b-179">Set dependencies between hello resources</span></span>
<span data-ttu-id="3841b-180">Azure debe configurar los recursos de hello en un orden estricto.</span><span class="sxs-lookup"><span data-stu-id="3841b-180">Azure should set up hello resources in strict order.</span></span> <span data-ttu-id="3841b-181">toomake que el programa de instalación se completa antes de hello comienza a continuación, agregue las líneas de dependencia:</span><span class="sxs-lookup"><span data-stu-id="3841b-181">toomake sure one setup completes before hello next begins, add dependency lines:</span></span>

* <span data-ttu-id="3841b-182">Recurso de prueba en la disponibilidad de hello:</span><span class="sxs-lookup"><span data-stu-id="3841b-182">In hello availability test resource:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* <span data-ttu-id="3841b-183">En el recurso de alerta de Hola para una prueba de disponibilidad:</span><span class="sxs-lookup"><span data-stu-id="3841b-183">In hello alert resource for an availability test:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a><span data-ttu-id="3841b-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3841b-184">Next steps</span></span>
<span data-ttu-id="3841b-185">Otros artículos de automatización:</span><span class="sxs-lookup"><span data-stu-id="3841b-185">Other automation articles:</span></span>

* <span data-ttu-id="3841b-186">[Script de PowerShell para crear un recurso de Application Insights](app-insights-powershell-script-create-resource.md) : método rápido sin necesidad de plantilla.</span><span class="sxs-lookup"><span data-stu-id="3841b-186">[Create an Application Insights resource](app-insights-powershell-script-create-resource.md) - quick method without using a template.</span></span>
* [<span data-ttu-id="3841b-187">Uso de PowerShell para configurar alertas en Application Insights</span><span class="sxs-lookup"><span data-stu-id="3841b-187">Set up Alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="3841b-188">Creación de pruebas web</span><span class="sxs-lookup"><span data-stu-id="3841b-188">Create web tests</span></span>](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [<span data-ttu-id="3841b-189">Enviar información de diagnóstico de Azure tooApplication</span><span class="sxs-lookup"><span data-stu-id="3841b-189">Send Azure Diagnostics tooApplication Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="3841b-190">Implementar tooAzure desde GitHub</span><span class="sxs-lookup"><span data-stu-id="3841b-190">Deploy tooAzure from GitHub</span></span>](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [<span data-ttu-id="3841b-191">Creación de anotaciones de versión</span><span class="sxs-lookup"><span data-stu-id="3841b-191">Create release annotations</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

