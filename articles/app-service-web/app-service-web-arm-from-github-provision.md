---
title: "aaaDeploy una aplicación web que está vinculado el repositorio de GitHub de tooa | Documentos de Microsoft"
description: "Utilice un toodeploy de plantilla de Azure Resource Manager una aplicación web que contiene un proyecto desde un repositorio de GitHub."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 32739607-85fe-43c8-a4dc-1feb46d93a4d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: 8b23416c4c06a60991517e6ee4cd82bebc5a9d73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-linked-tooa-github-repository"></a>Implementar un repositorio de GitHub de web app vinculado tooa
En este tema, obtendrá información sobre cómo toocreate una plantilla de Azure Resource Manager que se puede implementar una aplicación web que está había vinculado tooa proyecto en un repositorio de GitHub. Obtendrá información sobre cómo toodefine qué recursos se implementan y cómo toodefine parámetros que especifican cuando se ejecuta la implementación de Hola. Puede usar esta plantilla para sus propias implementaciones o personalizarlo toomeet sus requisitos.

Para obtener más información sobre la creación de plantillas, consulte [Creación de plantillas de Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).

Para la plantilla de hello completa, consulte [Web App vinculado plantilla tooGitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a>Lo que implementará
Con esta plantilla, se implementará una aplicación web que contiene el código de hello desde un proyecto en GitHub.

toorun Hola implementación automáticamente, haga clic en hello después de botón:

[![Implementar tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)

## <a name="parameters"></a>parameters
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a>repoURL
dirección URL de Hello para el repositorio de GitHub que contiene Hola proyecto toodeploy. Este parámetro contiene un valor predeterminado, pero este valor es solo previsto tooshow también cómo tooprovide Hola dirección URL para el repositorio. Puede usar este valor pruebas plantilla Hola pero resulta conveniente tooprovide Hola URL su propio repositorio cuando se trabaja con plantilla Hola.

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a>branch
rama de Hola de hello repositorio toouse al implementar la aplicación hello. valor predeterminado de Hello es principal, pero puede proporcionar nombre Hola de alguna de las bifurcaciones en el repositorio de Hola que desea toodeploy.

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-toodeploy"></a>Toodeploy de recursos
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a>Aplicación web
Crea la aplicación web de hello que está vinculado toohello proyecto en GitHub. 

Especificar nombre de Hola de aplicación web de hello a través de hello **siteName** parámetro y la ubicación de Hola de aplicación web de hello a través de hello **siteLocation** parámetro. Hola **dependsOn** elemento, plantilla de Hola define aplicación web de hello como dependiente de plan de hospedaje de servicio de Hola. Dado que es dependiente de hello plan de hospedaje, aplicación web de hello no se crea hasta Hola plan de hospedaje ha terminado de crear. Hola **dependsOn** elemento es solo el orden de implementación toospecify usado. Si no marca la aplicación web de hello como dependiente de plan de hospedaje de Hola, Azure Resource Manager intentará toocreate los recursos en hello mismo tiempo y puede que aparezca un error si se crea la aplicación web de hello antes de hello plan de hospedaje.

aplicación web de Hello también tiene un recurso secundario que se define en **recursos** sección más adelante. Este recurso secundario define el control de código fuente para proyecto de hello implementado con la aplicación web de hello. En esta plantilla, control de código fuente de hello es vinculado tooa repositorio de GitHub determinado. repositorio de GitHub de Hola se define con código de hello **"Dirección URL del repositorio": "https://github.com/davidebbo-test/Mvc52Application.git"** podría URL del repositorio de codificar de forma rígida hello cuando desee toocreate una plantilla que implementa varias veces una proyecto solo requieren un mínimo de parámetros Hola.
En lugar de codificar de forma rígida Hola dirección URL del repositorio, puede agregar un parámetro de dirección URL de repositorio de Hola y usar ese valor para hello **dirección URL del repositorio** propiedad.

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
      ],
      "properties": {
        "serverFarmId": "[parameters('hostingPlanName')]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/Sites', parameters('siteName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('repoURL')]",
            "branch": "[parameters('branch')]",
            "IsManualIntegration": true
          }
        }
      ]
    }

## <a name="commands-toorun-deployment"></a>Implementación de toorun de comandos
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Azure CLI

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a>CLI de Azure 2.0

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> Para el contenido del archivo JSON de parámetros de hello, consulte [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).
>
>

