---
title: "implementación de recursos de aaaAutomate para una aplicación de la función en funciones de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toobuild una plantilla de Azure Resource Manager que implementa la aplicación de la función."
services: Functions
documtationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, funciones, arquitectura sin servidor, infraestructura como código, azure resource manager"
ms.assetid: d20743e3-aab6-442c-a836-9bcea09bfd32
ms.server: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: b0df0d4ef9fe93213f7b1cb1d1e6b4e14f8b3a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a>Automatización de la implementación de recursos para una aplicación de función en Azure Functions

Puede usar un toodeploy de plantilla una aplicación de la función de administrador de recursos de Azure. En este artículo se describe Hola requerido recursos y parámetros para hacerlo. Tendrá que toodeploy obtener recursos adicionales, dependiendo de hello [desencadenadores y enlaces](functions-triggers-bindings.md) en la aplicación de la función.

Para más información sobre la creación de plantillas, consulte [Creación de plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Para obtener las plantillas de ejemplo, vea:
- [Aplicación de función en el plan de consumo]
- [Aplicación de función en el plan de App Service]

## <a name="required-resources"></a>Recursos necesarios

Una aplicación de función requiere estos recursos:

* Una cuenta de [Azure Storage](../storage/index.md).
* Un plan de hospedaje (plan de consumo o plan de App Service).
* Una aplicación de función. 

### <a name="storage-account"></a>Cuenta de almacenamiento

Se necesita una cuenta de Azure Storage para una aplicación de función. Se necesita una cuenta de uso general que admita blobs, tablas, colas y archivos. Para más información, vea [Requisitos de la cuenta de almacenamiento de Azure Functions](functions-create-function-app-portal.md#storage-account-requirements).

```json
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2015-06-15",
    "location": "[resourceGroup().location]",
    "properties": {
        "accountType": "[parameters('storageAccountType')]"
    }
}
```

Además, Hola propiedades `AzureWebJobsStorage` y `AzureWebJobsDashboard` debe especificarse como configuración de la aplicación en la configuración de sitio de Hola. en tiempo de ejecución de funciones de Azure de Hello usa hello `AzureWebJobsStorage` toocreate las colas internas de la cadena de conexión. Hola la cadena de conexión `AzureWebJobsDashboard` es toolog usado tooAzure tabla almacenamiento y power hello **Monitor** portal Hola de.

Estas propiedades se especifican en hello `appSettings` colección Hola `siteConfig` objeto:

```json
"appSettings": [
    {
        "name": "AzureWebJobsStorage",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    },
    {
        "name": "AzureWebJobsDashboard",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    }
```    

### <a name="hosting-plan"></a>Plan de hospedaje

definición de Hola de hello plan de hospedaje varía, dependiendo de si utiliza un plan de consumo o servicio de aplicaciones. Vea [implementar una aplicación de la función en el plan de consumo de hello](#consumption) y [implementar una aplicación de función en el plan de servicio de aplicación Hola](#app-service-plan).

### <a name="function-app"></a>Aplicación de función

recurso de la función aplicación Hola se define mediante un recurso de tipo **Microsoft.Web/Site** y tipo **functionapp**:

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ]
```

<a name="consumption"></a>

## <a name="deploy-a-function-app-on-hello-consumption-plan"></a>Implementar una aplicación de la función en el plan de consumo de Hola

Puede ejecutar una aplicación de función en dos modos diferentes: Hola hello plan de servicio de aplicaciones y el plan de consumo. plan de consumo de Hello asigna automáticamente la capacidad de proceso cuando el código se ejecuta, admita la ampliación horizontal como carga de toohandle necesarios y, a continuación, se escala hacia abajo cuando no se está ejecutando el código. Por lo tanto, no tiene toopay para máquinas virtuales inactivas y no tiene capacidad de tooreserve de antemano. toolearn más sobre el hospedaje de planes, consulte [planes de servicio de aplicaciones y de consumo de funciones de Azure](functions-scale.md).

Para obtener una plantilla de Azure Resource Manager de ejemplo, vea [Aplicación de función en el plan de consumo].

### <a name="create-a-consumption-plan"></a>Crear un plan de consumo

Un plan de consumo es un tipo especial de recurso de "granja de servidores". Se especifica mediante hello `Dynamic` valor de hello `computeMode` y `sku` propiedades:

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "computeMode": "Dynamic",
        "sku": "Dynamic"
    }
}
```

### <a name="create-a-function-app"></a>Creación de una aplicación de función

Además, un plan de consumo requiere dos configuraciones adicionales en la configuración de sitio de hello: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` y `WEBSITE_CONTENTSHARE`. Estas propiedades configuran Hola almacenamiento cuenta y la ruta donde se almacenan el código de aplicación de función de Hola y la configuración.

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ],
    "properties": {
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "siteConfig": {
            "appSettings": [
                {
                    "name": "AzureWebJobsDashboard",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "AzureWebJobsStorage",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTAZUREFILECONNECTIONSTRING",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTSHARE",
                    "value": "[toLower(variables('functionAppName'))]"
                },
                {
                    "name": "FUNCTIONS_EXTENSION_VERSION",
                    "value": "~1"
                }
            ]
        }
    }
}
```                    

<a name="app-service-plan"></a> 

## <a name="deploy-a-function-app-on-hello-app-service-plan"></a>Implementar una aplicación de la función en hello plan de servicio de aplicaciones

Hola plan de servicio de aplicaciones, la aplicación de la función se ejecuta en máquinas virtuales dedicadas en Basic, Standard y Premium SKU, aplicaciones tooweb similar. Para obtener más información acerca del funcionamiento de hello plan de servicio de aplicaciones, vea hello [información general detallada de planes de servicio de aplicaciones de Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Para obtener una plantilla de Azure Resource Manager de ejemplo, vea [Aplicación de función en el plan de App Service].

### <a name="create-an-app-service-plan"></a>Creación de un plan del Servicio de aplicaciones

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "sku": "[parameters('sku')]",
        "workerSize": "[parameters('workerSize')]",
        "hostingEnvironment": "",
        "numberOfWorkers": 1
    }
}
```

### <a name="create-a-function-app"></a>Creación de una aplicación de función 

Después de seleccionar una opción de escalado, cree una aplicación de función. aplicación Hello es contenedor de Hola que contiene todas las funciones.

Una aplicación de función tiene muchos recursos secundarios que puede usar en la implementación, incluidas la configuración de la aplicación y las opciones de control del código fuente. También puede elegir hello tooremove **sourcecontrols** recurso secundario y use otra [opción de implementación](functions-continuous-deployment.md) en su lugar.

> [!IMPORTANT]
> toosuccessfully implementar su aplicación mediante el Administrador de recursos de Azure, es importante toounderstand forma en que se implementan los recursos en Azure. En el siguiente ejemplo de Hola, se aplican las configuraciones de nivel superior mediante **siteConfig**. Es importante tooset nivel estas configuraciones en un principio, porque transmite información toohello funciones en tiempo de ejecución e implementación el motor. Se necesita información de nivel superior antes de secundarios de hello **sourcecontrols/web** se aplica un recurso. Aunque es posible tooconfigure estos valores en Hola nivel secundario **config/appSettings** recurso, en algunos casos se debe implementar la aplicación de la función *antes de* **config/appSettings**  se aplica. Por ejemplo, cuando se usan funciones con [Logic Apps](../logic-apps/index.md), las funciones son una dependencia de otro recurso.

```json
{
  "apiVersion": "2015-08-01",
  "name": "[parameters('appName')]",
  "type": "Microsoft.Web/sites",
  "kind": "functionapp",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Web/serverfarms', parameters('appName'))]"
  ],
  "properties": {
     "serverFarmId": "[variables('appServicePlanName')]",
     "siteConfig": {
        "alwaysOn": true,
        "appSettings": [
            { "name": "FUNCTIONS_EXTENSION_VERSION", "value": "~1" },
            { "name": "Project", "value": "src" }
        ]
     }
  },
  "resources": [
     {
        "apiVersion": "2015-08-01",
        "name": "appsettings",
        "type": "config",
        "dependsOn": [
          "[resourceId('Microsoft.Web/Sites', parameters('appName'))]",
          "[resourceId('Microsoft.Web/Sites/sourcecontrols', parameters('appName'), 'web')]",
          "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
        ],
        "properties": {
          "AzureWebJobsStorage": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]",
          "AzureWebJobsDashboard": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
        }
     },
     {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/sites/', parameters('appName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('sourceCodeRepositoryURL')]",
            "branch": "[parameters('sourceCodeBranch')]",
            "IsManualIntegration": "[parameters('sourceCodeManualIntegration')]"
          }
     }
  ]
}
```
> [!TIP]
> Esta plantilla utiliza hello [proyecto](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) valor de la configuración de aplicación, que establece el directorio base hello en qué Hola motor de implementación de funciones (Kudu) es para código que se pueden implementar. En nuestro repositorio, nuestro funciones están en una subcarpeta de hello **src** carpeta. Por lo tanto, en el anterior ejemplo de Hola, establecemos el valor de configuración de aplicación de hello demasiado`src`. Si las funciones están en la raíz de hello del repositorio, o si no va a implementar desde el control de código fuente, puede quitar este valor de configuración de aplicación.

## <a name="deploy-your-template"></a>Implementación de la plantilla

Puede usar cualquiera de hello después formas toodeploy la plantilla:

* [PowerShell](../azure-resource-manager/resource-group-template-deploy.md)
* [CLI de Azure](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [Portal de Azure](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [API DE REST](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-tooazure-button"></a>Botón tooAzure implementar

Reemplace ```<url-encoded-path-to-azuredeploy-json>``` con un [codificados de dirección URL](https://www.bing.com/search?q=url+encode) versión de la ruta de acceso sin procesar de Hola de su `azuredeploy.json` archivo en GitHub.

A continuación se muestra un ejemplo que usa Markdown:

```markdown
[![Deploy tooAzure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

A continuación se muestra un ejemplo que usa HTML:

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a>Pasos siguientes

Más información acerca de cómo toodevelop y configurar las funciones de Azure.

* [Azure Functions developer reference](functions-reference.md)
* [Funcionamiento de tooconfigure Azure en configuración de la aplicación](functions-how-to-use-azure-function-app-settings.md)
* [Creación de su primera función de Azure](functions-create-first-azure-function.md)

<!-- LINKS -->

[Aplicación de función en el plan de consumo]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[Aplicación de función en el plan de App Service]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
