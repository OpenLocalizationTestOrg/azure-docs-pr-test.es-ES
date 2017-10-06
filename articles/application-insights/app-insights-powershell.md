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
#  <a name="create-application-insights-resources-using-powershell"></a>Creación de recursos de Application Insights mediante PowerShell
Este artículo muestra cómo tooautomate Hola creación y actualización de [Application Insights](app-insights-overview.md) recursos automáticamente mediante el uso de administración de recursos de Azure. Puede hacerlo, por ejemplo, como parte de un proceso de compilación. Junto con el recurso de Application Insights de hello básico, puede crear [disponibilidad las pruebas web](app-insights-monitor-web-app-availability.md), configuraré [alertas](app-insights-alerts.md), hello establezca [precios esquema](app-insights-pricing.md)y crear otro Azure recursos.

Hola toocreating clave estos recursos son las plantillas de JSON para [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md). En pocas palabras, es el procedimiento de hello: Descargar Hola JSON definiciones de recursos existentes; parametrizar determinados valores como los nombres; y, a continuación, ejecute plantilla Hola siempre que lo desee toocreate un nuevo recurso. Puede empaquetar varios recursos juntos, toocreate que todo en uno Enhorabuena: por ejemplo, un monitor de aplicaciones con pruebas de disponibilidad, las alertas y almacenamiento para la exportación continua. No hay algunos toosome matices de parametrizaciones hello, que se explican aquí.

## <a name="one-time-setup"></a>Instalación única
Si no ha usado PowerShell con su suscripción de Azure antes:

Instale el módulo de Powershell de Azure de hello en la máquina de Hola donde desea que las secuencias de comandos de toorun hello:

1. Instale el [Instalador de plataforma web de Microsoft (v5 o superior)](http://www.microsoft.com/web/downloads/platform.aspx).
2. Usar tooinstall Microsoft Azure Powershell.

## <a name="create-an-azure-resource-manager-template"></a>Creación de una plantilla de Azure Resource Manager
Cree un nuevo archivo .json. Vamos a llamarlo `template1.json` en este ejemplo. Copie este contenido en él:

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



## <a name="create-application-insights-resources"></a>Creación de recursos de Application Insights
1. En PowerShell, inicie sesión en tooAzure:
   
    `Login-AzureRmAccount`
2. Ejecute un comando similar al siguiente:
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * `-ResourceGroupName`es grupo de Hola donde desea nuevos recursos de toocreate Hola.
   * `-TemplateFile`debe aparecer antes de parámetros personalizados Hola.
   * `-appName`nombre de Hola de hello recursos toocreate.

Puede agregar otros parámetros: encontrará sus descripciones en la sección de parámetros de Hola de plantilla de Hola.

## <a name="tooget-hello-instrumentation-key"></a>clave de instrumentación de hello tooget
Después de crear un recurso de aplicación, querrá clave de instrumentación de hello: 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-hello-price-plan"></a>Establecer plan de precios de Hola

Puede establecer hello [plan de precios](app-insights-pricing.md).

toocreate un recurso de aplicación con plan de precios de Enterprise hello, con plantilla Hola anterior:

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|priceCode|plan|
|---|---|
|1|Básico|
|2|Enterprise|

* Si solo desea plan de precios básico de toouse Hola predeterminado, puede omitir hello CurrentBillingFeatures provienen de la plantilla de Hola.
* Si desea plan de precios de hello toochange después de que se ha creado el recurso de componente de hello, puede usar una plantilla que omite el recurso de Hola "Type Microsoft.Insights/Components". Además, omitir hello `dependsOn` nodo de hello recursos de facturación. 

tooverify Hola plan de precios actualizada, buscar en la hoja de Hola "Características + precios" en el Explorador de Hola. **Actualizar vista del explorador de hello** toomake asegurarse de ver el estado más reciente de Hola.



## <a name="add-a-metric-alert"></a>Agregar una alerta de métrica

tooset una alerta métrica en hello mismo tiempo como el recurso de aplicación, mezcla código similar al siguiente en el archivo de plantilla de hello:

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

Cuando se invoca la plantilla de hello, opcionalmente, puede agregar este parámetro:

    `-responseTime 2`

También puede parametrizar otros campos. 

toofind los nombres de tipo hello y detalles de configuración de otras reglas de alerta, crear una regla manualmente y, a continuación, inspeccione en [Azure Resource Manager](https://resources.azure.com/). 


## <a name="add-an-availability-test"></a>Agregar una prueba de disponibilidad

En este ejemplo es para una prueba de ping (tootest una sola página).  

**Hay dos partes** en una prueba de disponibilidad: propia prueba de Hola y alerta de Hola que le informa de errores.

Combinar Hola siguiente código en el archivo de plantilla de Hola que crea la aplicación hello.

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

códigos de hello toodiscover para otras ubicaciones de prueba, o la creación de hello de tooautomate de pruebas web más complejas, un ejemplo de cómo crear manualmente y, a continuación, se parametrizan código de hello de [Azure Resource Manager](https://resources.azure.com/).

## <a name="add-more-resources"></a>Agregar más recursos

creación de hello tooautomate de cualquier otro recurso de cualquier tipo, un ejemplo de cómo crear manualmente y, a continuación, copie y parametrizar su código de [Azure Resource Manager](https://resources.azure.com/). 

1. Abra el [Administrador de recursos de Azure](https://resources.azure.com/). Navegar hacia abajo por `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour de recursos de aplicación. 
   
    ![Navegación en el Explorador de recursos de Azure](./media/app-insights-powershell/01.png)
   
    *Componentes* es Hola recursos básicos de Application Insights para mostrar las aplicaciones. Hay recursos independientes para hello asociados a las reglas de alertas y las pruebas de web de disponibilidad.
2. Hola copia JSON del componente de hello en el lugar adecuado de hello en `template1.json`.
3. Elimine estas propiedades:
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. Abra secciones de pruebas Web y alertrules hello y copie hello JSON para elementos individuales en la plantilla. (No se copian de los nodos de pruebas Web o alertrules Hola: vaya a elementos de hello en ellos.)
   
    Cada prueba web tiene una regla de alerta asociada, por lo que tendrá toocopy de ellos.
   
    También puede incluir alertas en las métricas. [Nombres de métricas](app-insights-powershell-alerts.md#metric-names).
5. Inserte esta línea en cada recurso:
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-hello-template"></a>Parametrizar la plantilla de Hola
Ahora tiene nombres específicos de hello tooreplace con parámetros. demasiado[parametrizar una plantilla](../azure-resource-manager/resource-group-authoring-templates.md), escribir expresiones que utilizan un [conjunto de funciones auxiliares](../azure-resource-manager/resource-group-template-functions.md). 

No se puede parametrizar sólo una parte de una cadena, por lo que usar `concat()` toobuild cadenas.

Estos son ejemplos de sustituciones Hola querrá toomake. Hay varias repeticiones de cada sustitución. Y puede que tenga otras en la plantilla. Estos ejemplos utilizan parámetros de Hola y las variables que se ha definido en parte superior de Hola de plantilla de Hola.

| find | reemplazar por |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| `"myappname"` (minúscula) |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/>Elimine el Guid y el identificador. |

### <a name="set-dependencies-between-hello-resources"></a>Definir dependencias entre recursos de Hola
Azure debe configurar los recursos de hello en un orden estricto. toomake que el programa de instalación se completa antes de hello comienza a continuación, agregue las líneas de dependencia:

* Recurso de prueba en la disponibilidad de hello:
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* En el recurso de alerta de Hola para una prueba de disponibilidad:
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a>Pasos siguientes
Otros artículos de automatización:

* [Script de PowerShell para crear un recurso de Application Insights](app-insights-powershell-script-create-resource.md) : método rápido sin necesidad de plantilla.
* [Uso de PowerShell para configurar alertas en Application Insights](app-insights-powershell-alerts.md)
* [Creación de pruebas web](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [Enviar información de diagnóstico de Azure tooApplication](app-insights-powershell-azure-diagnostics.md)
* [Implementar tooAzure desde GitHub](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [Creación de anotaciones de versión](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

