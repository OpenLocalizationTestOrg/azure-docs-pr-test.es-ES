---
title: "Automatización de Azure Application Insights con PowerShell | Microsoft Docs"
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
ms.openlocfilehash: 88dbb9515300f847789bc889911cdeff5f5bdb53
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
#  <a name="create-application-insights-resources-using-powershell"></a><span data-ttu-id="91b04-103">Creación de recursos de Application Insights mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="91b04-103">Create Application Insights resources using PowerShell</span></span>
<span data-ttu-id="91b04-104">Este artículo muestra cómo automatizar la creación y actualización de los recursos de [Application Insights](app-insights-overview.md) automáticamente mediante Azure Resource Management.</span><span class="sxs-lookup"><span data-stu-id="91b04-104">This article shows you how to automate the creation and update of [Application Insights](app-insights-overview.md) resources automatically by using Azure Resource Management.</span></span> <span data-ttu-id="91b04-105">Puede hacerlo, por ejemplo, como parte de un proceso de compilación.</span><span class="sxs-lookup"><span data-stu-id="91b04-105">You might, for example, do so as part of a build process.</span></span> <span data-ttu-id="91b04-106">Junto con el recurso básico de Application Insights, puede crear [pruebas web de disponibilidad](app-insights-monitor-web-app-availability.md), [configurar alertas](app-insights-alerts.md), establecer el [esquema de precios](app-insights-pricing.md) y crear otros recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="91b04-106">Along with the basic Application Insights resource, you can create [availability web tests](app-insights-monitor-web-app-availability.md), set up [alerts](app-insights-alerts.md), set the [pricing scheme](app-insights-pricing.md), and create other Azure resources.</span></span>

<span data-ttu-id="91b04-107">La clave para crear estos recursos es las plantillas JSON para el [Administrador de recursos de Azure](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="91b04-107">The key to creating these resources is JSON templates for [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span> <span data-ttu-id="91b04-108">En pocas palabras, el procedimiento es: descargar las definiciones JSON de los recursos existentes; parametrizar determinados valores como los nombres; y luego ejecutar la plantilla siempre que se quiera crear un nuevo recurso.</span><span class="sxs-lookup"><span data-stu-id="91b04-108">In a nutshell, the procedure is: download the JSON definitions of existing resources; parameterize certain values such as names; and then run the template whenever you want to create a new resource.</span></span> <span data-ttu-id="91b04-109">Puede empaquetar varios recursos juntos para crearlos todos en un solo paso, por ejemplo, un monitor de aplicaciones con pruebas de disponibilidad, alertas y almacenamiento para la exportación continua.</span><span class="sxs-lookup"><span data-stu-id="91b04-109">You can package several resources together, to create them all in one go - for example, an app monitor with availability tests, alerts, and storage for continuous export.</span></span> <span data-ttu-id="91b04-110">Existen algunos matices a algunas de las parametrizaciones automáticas, que se explican aquí.</span><span class="sxs-lookup"><span data-stu-id="91b04-110">There are some subtleties to some of the parameterizations, which we'll explain here.</span></span>

## <a name="one-time-setup"></a><span data-ttu-id="91b04-111">Instalación única</span><span class="sxs-lookup"><span data-stu-id="91b04-111">One-time setup</span></span>
<span data-ttu-id="91b04-112">Si no ha usado PowerShell con su suscripción de Azure antes:</span><span class="sxs-lookup"><span data-stu-id="91b04-112">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="91b04-113">Instale el módulo de Azure Powershell en la máquina donde quiere ejecutar los scripts.</span><span class="sxs-lookup"><span data-stu-id="91b04-113">Install the Azure Powershell module on the machine where you want to run the scripts:</span></span>

1. <span data-ttu-id="91b04-114">Instale el [Instalador de plataforma web de Microsoft (v5 o superior)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="91b04-114">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
2. <span data-ttu-id="91b04-115">Úselo para instalar Microsoft Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="91b04-115">Use it to install Microsoft Azure Powershell.</span></span>

## <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="91b04-116">Creación de una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="91b04-116">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="91b04-117">Cree un nuevo archivo .json. Vamos a llamarlo `template1.json` en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="91b04-117">Create a new .json file - let's call it `template1.json` in this example.</span></span> <span data-ttu-id="91b04-118">Copie este contenido en él:</span><span class="sxs-lookup"><span data-stu-id="91b04-118">Copy this content into it:</span></span>

```JSON
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "appName": {
                "type": "string",
                "metadata": {
                    "description": "Enter the application name."
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
                    "description": "Enter the application type."
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
                    "description": "Enter the application location."
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
                    "description": "Enter daily quota reset hour in UTC (0 to 23). Values outside the range will get a random reset hour."
                }
            },
            "warningThreshold": {
                "type": "int",
                "defaultValue": 90,
                "minValue": 1,
                "maxValue": 100,
                "metadata": {
                    "description": "Enter the % value of daily quota after which warning mail to be sent. "
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



## <a name="create-application-insights-resources"></a><span data-ttu-id="91b04-119">Creación de recursos de Application Insights</span><span class="sxs-lookup"><span data-stu-id="91b04-119">Create Application Insights resources</span></span>
1. <span data-ttu-id="91b04-120">En PowerShell, inicie sesión en Azure:</span><span class="sxs-lookup"><span data-stu-id="91b04-120">In PowerShell, sign in to Azure:</span></span>
   
    `Login-AzureRmAccount`
2. <span data-ttu-id="91b04-121">Ejecute un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="91b04-121">Run a command like this:</span></span>
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * <span data-ttu-id="91b04-122">`-ResourceGroupName` es el grupo donde desea crear los nuevos recursos.</span><span class="sxs-lookup"><span data-stu-id="91b04-122">`-ResourceGroupName` is the group where you want to create the new resources.</span></span>
   * <span data-ttu-id="91b04-123">`-TemplateFile` debe aparecer antes que los parámetros personalizados.</span><span class="sxs-lookup"><span data-stu-id="91b04-123">`-TemplateFile` must occur before the custom parameters.</span></span>
   * <span data-ttu-id="91b04-124">`-appName` es el nombre del recurso que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="91b04-124">`-appName` The name of the resource to create.</span></span>

<span data-ttu-id="91b04-125">Puede agregar otros parámetros, cuyas descripciones se encuentran en la sección de parámetros de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="91b04-125">You can add other parameters - you'll find their descriptions in the parameters section of the template.</span></span>

## <a name="to-get-the-instrumentation-key"></a><span data-ttu-id="91b04-126">Para obtener la clave de instrumentación</span><span class="sxs-lookup"><span data-stu-id="91b04-126">To get the instrumentation key</span></span>
<span data-ttu-id="91b04-127">Después de crear un recurso de aplicación, querrá la clave de instrumentación:</span><span class="sxs-lookup"><span data-stu-id="91b04-127">After creating an application resource, you'll want the instrumentation key:</span></span> 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-the-price-plan"></a><span data-ttu-id="91b04-128">Establecimiento del plan de precios</span><span class="sxs-lookup"><span data-stu-id="91b04-128">Set the price plan</span></span>

<span data-ttu-id="91b04-129">Puede establecer el [plan de precios](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="91b04-129">You can set the [price plan](app-insights-pricing.md).</span></span>

<span data-ttu-id="91b04-130">Para crear un recurso de aplicación con el plan de precios de Enterprise, use la plantilla anterior:</span><span class="sxs-lookup"><span data-stu-id="91b04-130">To create an app resource with the Enterprise price plan, using the template above:</span></span>

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|<span data-ttu-id="91b04-131">priceCode</span><span class="sxs-lookup"><span data-stu-id="91b04-131">priceCode</span></span>|<span data-ttu-id="91b04-132">plan</span><span class="sxs-lookup"><span data-stu-id="91b04-132">plan</span></span>|
|---|---|
|<span data-ttu-id="91b04-133">1</span><span class="sxs-lookup"><span data-stu-id="91b04-133">1</span></span>|<span data-ttu-id="91b04-134">Básico</span><span class="sxs-lookup"><span data-stu-id="91b04-134">Basic</span></span>|
|<span data-ttu-id="91b04-135">2</span><span class="sxs-lookup"><span data-stu-id="91b04-135">2</span></span>|<span data-ttu-id="91b04-136">Enterprise</span><span class="sxs-lookup"><span data-stu-id="91b04-136">Enterprise</span></span>|

* <span data-ttu-id="91b04-137">Si solo desea usar el plan de precios básico predeterminado, puede omitir el recurso CurrentBillingFeatures de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="91b04-137">If you only want to use the default Basic price plan, you can omit the CurrentBillingFeatures resource from the template.</span></span>
* <span data-ttu-id="91b04-138">Si desea cambiar el plan de precios una vez creado el recurso de componente, puede usar una plantilla que omita el recurso "microsoft.insights/components".</span><span class="sxs-lookup"><span data-stu-id="91b04-138">If you want to change the price plan after the component resource has been created, you can use a template that omits the "microsoft.insights/components" resource.</span></span> <span data-ttu-id="91b04-139">Además, omita el nodo `dependsOn` del recurso de facturación.</span><span class="sxs-lookup"><span data-stu-id="91b04-139">Also, omit the `dependsOn` node from the billing resource.</span></span> 

<span data-ttu-id="91b04-140">Para comprobar el plan de precios actualizado, consulte la hoja de características y precios en el explorador.</span><span class="sxs-lookup"><span data-stu-id="91b04-140">To verify the updated price plan, look at the "Features+pricing" blade in the browser.</span></span> <span data-ttu-id="91b04-141">**Actualice la vista de explorador** para asegurarse de ver el estado más reciente.</span><span class="sxs-lookup"><span data-stu-id="91b04-141">**Refresh the browser view** to make sure you see the latest state.</span></span>



## <a name="add-a-metric-alert"></a><span data-ttu-id="91b04-142">Agregar una alerta de métrica</span><span class="sxs-lookup"><span data-stu-id="91b04-142">Add a metric alert</span></span>

<span data-ttu-id="91b04-143">Para configurar una alerta de métrica al mismo tiempo que el recurso de aplicación, combine código similar al siguiente en el archivo de plantilla:</span><span class="sxs-lookup"><span data-stu-id="91b04-143">To set up a metric alert at the same time as your app resource, merge code like this into the template file:</span></span>

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
      // Ensure this resource is created after the app resource:
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

<span data-ttu-id="91b04-144">Al invocar la plantilla, tiene la opción de agregar este parámetro:</span><span class="sxs-lookup"><span data-stu-id="91b04-144">When you invoke the template, you can optionally add this parameter:</span></span>

    `-responseTime 2`

<span data-ttu-id="91b04-145">También puede parametrizar otros campos.</span><span class="sxs-lookup"><span data-stu-id="91b04-145">You can of course parameterize other fields.</span></span> 

<span data-ttu-id="91b04-146">Para buscar los nombres de tipo y los detalles de configuración de otras reglas de alerta, cree manualmente una regla y, a continuación, inspecciónela en [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="91b04-146">To find out the type names and configuration details of other alert rules, create a rule manually and then inspect it in [Azure Resource Manager](https://resources.azure.com/).</span></span> 


## <a name="add-an-availability-test"></a><span data-ttu-id="91b04-147">Agregar una prueba de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="91b04-147">Add an availability test</span></span>

<span data-ttu-id="91b04-148">Este ejemplo es para una prueba de ping (para probar una sola página).</span><span class="sxs-lookup"><span data-stu-id="91b04-148">This example is for a ping test (to test a single page).</span></span>  

<span data-ttu-id="91b04-149">**Hay dos partes** en una prueba de disponibilidad: la propia prueba y la alerta que informa de errores.</span><span class="sxs-lookup"><span data-stu-id="91b04-149">**There are two parts** in an availability test: the test itself, and the alert that notifies you of failures.</span></span>

<span data-ttu-id="91b04-150">Combine el código siguiente en el archivo de plantilla que crea la aplicación.</span><span class="sxs-lookup"><span data-stu-id="91b04-150">Merge the following code into the template file that creates the app.</span></span>

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
      // Availability test: part 1 configures the test
      //
      "name": "[variables('pingTestName')]",
      "type": "Microsoft.Insights/webtests",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this is created after the app resource:
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
          "WebTest": "[concat('<WebTest   Name=\"', variables('pingTestName'), '\"   Enabled=\"True\"         CssProjectStructure=\"\"    CssIteration=\"\"  Timeout=\"120\"  WorkItemIds=\"\"         xmlns=\"http://microsoft.com/schemas/VisualStudio/TeamTest/2010\"         Description=\"\"  CredentialUserName=\"\"  CredentialPassword=\"\"         PreAuthenticate=\"True\"  Proxy=\"default\"  StopOnError=\"False\"         RecordedResultFile=\"\"  ResultsLocale=\"\">  <Items>  <Request Method=\"GET\"    Version=\"1.1\"  Url=\"', parameters('Url'),   '\" ThinkTime=\"0\"  Timeout=\"300\" ParseDependentRequests=\"True\"         FollowRedirects=\"True\" RecordResult=\"True\" Cache=\"False\"         ResponseTimeGoal=\"0\"  Encoding=\"utf-8\"  ExpectedHttpStatusCode=\"200\"         ExpectedResponseUrl=\"\" ReportingName=\"\" IgnoreHttpStatusCode=\"False\" />        </Items>  <ValidationRules> <ValidationRule  Classname=\"Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleFindText, Microsoft.VisualStudio.QualityTools.WebTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a\" DisplayName=\"Find Text\"         Description=\"Verifies the existence of the specified text in the response.\"         Level=\"High\"  ExectuionOrder=\"BeforeDependents\">  <RuleParameters>        <RuleParameter Name=\"FindText\" Value=\"',   parameters('pingText'), '\" />  <RuleParameter Name=\"IgnoreCase\" Value=\"False\" />  <RuleParameter Name=\"UseRegularExpression\" Value=\"False\" />  <RuleParameter Name=\"PassIfTextFound\" Value=\"True\" />  </RuleParameters> </ValidationRule>  </ValidationRules>  </WebTest>')]"
        },
        "SyntheticMonitorId": "[variables('pingTestName')]"
      }
    },

    {
      //
      // Availability test: part 2, the alert rule
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

<span data-ttu-id="91b04-151">Para detectar los códigos de otras ubicaciones de prueba, o para automatizar la creación de pruebas web más complejas, cree un ejemplo manualmente y luego parametrice el código en [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="91b04-151">To discover the codes for other test locations, or to automate the creation of more complex web tests, create an example manually and then parameterize the code from [Azure Resource Manager](https://resources.azure.com/).</span></span>

## <a name="add-more-resources"></a><span data-ttu-id="91b04-152">Agregar más recursos</span><span class="sxs-lookup"><span data-stu-id="91b04-152">Add more resources</span></span>

<span data-ttu-id="91b04-153">Para automatizar la creación de otros recursos de cualquier variante, cree un ejemplo manualmente y luego copie y parametrice su código en [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="91b04-153">To automate the creation of any other resource of any kind, create an example manually, and then copy and parameterize its code from [Azure Resource Manager](https://resources.azure.com/).</span></span> 

1. <span data-ttu-id="91b04-154">Abra el [Administrador de recursos de Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="91b04-154">Open [Azure Resource Manager](https://resources.azure.com/).</span></span> <span data-ttu-id="91b04-155">Desplácese hacia abajo por `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components` hasta el recurso de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="91b04-155">Navigate down through `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, to your application resource.</span></span> 
   
    ![Navegación en el Explorador de recursos de Azure](./media/app-insights-powershell/01.png)
   
    <span data-ttu-id="91b04-157">*Componentes* son los recursos básicos de Application Insights para mostrar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="91b04-157">*Components* are the basic Application Insights resources for displaying applications.</span></span> <span data-ttu-id="91b04-158">Existen recursos distintos para las reglas de alerta asociadas y las pruebas web de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="91b04-158">There are separate resources for the associated alert rules and availability web tests.</span></span>
2. <span data-ttu-id="91b04-159">Copie el código JSON del componente en el lugar adecuado en `template1.json`.</span><span class="sxs-lookup"><span data-stu-id="91b04-159">Copy the JSON of the component into the appropriate place in `template1.json`.</span></span>
3. <span data-ttu-id="91b04-160">Elimine estas propiedades:</span><span class="sxs-lookup"><span data-stu-id="91b04-160">Delete these properties:</span></span>
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. <span data-ttu-id="91b04-161">Abra las secciones de pruebas web y reglas de alertas y copie el código JSON para los elementos individuales de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="91b04-161">Open the webtests and alertrules sections and copy the JSON for individual items into your template.</span></span> <span data-ttu-id="91b04-162">(No copie de los nodos de pruebas web o reglas de alerta: vaya a los elementos que hay debajo de ellos).</span><span class="sxs-lookup"><span data-stu-id="91b04-162">(Don't copy from the webtests or alertrules nodes: go into the items under them.)</span></span>
   
    <span data-ttu-id="91b04-163">Cada prueba web tiene una regla de alerta asociada, por lo que tiene que copiar las dos.</span><span class="sxs-lookup"><span data-stu-id="91b04-163">Each web test has an associated alert rule, so you have to copy both of them.</span></span>
   
    <span data-ttu-id="91b04-164">También puede incluir alertas en las métricas.</span><span class="sxs-lookup"><span data-stu-id="91b04-164">You can also include alerts on metrics.</span></span> <span data-ttu-id="91b04-165">[Nombres de métricas](app-insights-powershell-alerts.md#metric-names).</span><span class="sxs-lookup"><span data-stu-id="91b04-165">[Metric names](app-insights-powershell-alerts.md#metric-names).</span></span>
5. <span data-ttu-id="91b04-166">Inserte esta línea en cada recurso:</span><span class="sxs-lookup"><span data-stu-id="91b04-166">Insert this line in each resource:</span></span>
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-the-template"></a><span data-ttu-id="91b04-167">Parametrización de la plantilla</span><span class="sxs-lookup"><span data-stu-id="91b04-167">Parameterize the template</span></span>
<span data-ttu-id="91b04-168">Ahora, debe reemplazar los nombres específicos por parámetros.</span><span class="sxs-lookup"><span data-stu-id="91b04-168">Now you have to replace the specific names with parameters.</span></span> <span data-ttu-id="91b04-169">Para [parametrizar una plantilla](../azure-resource-manager/resource-group-authoring-templates.md), escriba expresiones mediante un [conjunto de funciones auxiliares](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="91b04-169">To [parameterize a template](../azure-resource-manager/resource-group-authoring-templates.md), you write expressions using a [set of helper functions](../azure-resource-manager/resource-group-template-functions.md).</span></span> 

<span data-ttu-id="91b04-170">No se puede parametrizar solo una parte de una cadena, así que use `concat()` para compilar las cadenas.</span><span class="sxs-lookup"><span data-stu-id="91b04-170">You can't parameterize just part of a string, so use `concat()` to build strings.</span></span>

<span data-ttu-id="91b04-171">Éstos son ejemplos de sustituciones que querrá realizar.</span><span class="sxs-lookup"><span data-stu-id="91b04-171">Here are examples of the substitutions you'll want to make.</span></span> <span data-ttu-id="91b04-172">Hay varias repeticiones de cada sustitución.</span><span class="sxs-lookup"><span data-stu-id="91b04-172">There are several occurrences of each substitution.</span></span> <span data-ttu-id="91b04-173">Y puede que tenga otras en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="91b04-173">You might need others in your template.</span></span> <span data-ttu-id="91b04-174">En estos ejemplos se usan los parámetros y las variables que se han definido en la parte superior de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="91b04-174">These examples use the parameters and variables we defined at the top of the template.</span></span>

| <span data-ttu-id="91b04-175">find</span><span class="sxs-lookup"><span data-stu-id="91b04-175">find</span></span> | <span data-ttu-id="91b04-176">reemplazar por</span><span class="sxs-lookup"><span data-stu-id="91b04-176">replace with</span></span> |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| <span data-ttu-id="91b04-177">`"myappname"` (minúscula)</span><span class="sxs-lookup"><span data-stu-id="91b04-177">`"myappname"` (lower case)</span></span> |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/><span data-ttu-id="91b04-178">Elimine el Guid y el identificador.</span><span class="sxs-lookup"><span data-stu-id="91b04-178">Delete Guid and Id.</span></span> |

### <a name="set-dependencies-between-the-resources"></a><span data-ttu-id="91b04-179">Establecimiento de dependencias entre los recursos</span><span class="sxs-lookup"><span data-stu-id="91b04-179">Set dependencies between the resources</span></span>
<span data-ttu-id="91b04-180">Azure debe instalar los recursos en un orden estricto.</span><span class="sxs-lookup"><span data-stu-id="91b04-180">Azure should set up the resources in strict order.</span></span> <span data-ttu-id="91b04-181">Para tener la seguridad de que una instalación finaliza antes de que comience la siguiente, agregue líneas de dependencia:</span><span class="sxs-lookup"><span data-stu-id="91b04-181">To make sure one setup completes before the next begins, add dependency lines:</span></span>

* <span data-ttu-id="91b04-182">En el recurso de la prueba de disponibilidad:</span><span class="sxs-lookup"><span data-stu-id="91b04-182">In the availability test resource:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* <span data-ttu-id="91b04-183">En el recurso de la alerta para una prueba de disponibilidad:</span><span class="sxs-lookup"><span data-stu-id="91b04-183">In the alert resource for an availability test:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a><span data-ttu-id="91b04-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="91b04-184">Next steps</span></span>
<span data-ttu-id="91b04-185">Otros artículos de automatización:</span><span class="sxs-lookup"><span data-stu-id="91b04-185">Other automation articles:</span></span>

* <span data-ttu-id="91b04-186">[Script de PowerShell para crear un recurso de Application Insights](app-insights-powershell-script-create-resource.md) : método rápido sin necesidad de plantilla.</span><span class="sxs-lookup"><span data-stu-id="91b04-186">[Create an Application Insights resource](app-insights-powershell-script-create-resource.md) - quick method without using a template.</span></span>
* [<span data-ttu-id="91b04-187">Uso de PowerShell para configurar alertas en Application Insights</span><span class="sxs-lookup"><span data-stu-id="91b04-187">Set up Alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="91b04-188">Creación de pruebas web</span><span class="sxs-lookup"><span data-stu-id="91b04-188">Create web tests</span></span>](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [<span data-ttu-id="91b04-189">Envío de Azure Diagnostics a Application Insights</span><span class="sxs-lookup"><span data-stu-id="91b04-189">Send Azure Diagnostics to Application Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="91b04-190">Implementación en Azure desde GitHub</span><span class="sxs-lookup"><span data-stu-id="91b04-190">Deploy to Azure from GitHub</span></span>](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [<span data-ttu-id="91b04-191">Creación de anotaciones de versión</span><span class="sxs-lookup"><span data-stu-id="91b04-191">Create release annotations</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

