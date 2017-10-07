---
title: "aaaCreate una aplicación de lógica mediante una plantilla de Azure | Documentos de Microsoft"
description: "Utilice un toodeploy de plantilla de Azure Resource Manager una aplicación lógica para definir los flujos de trabajo."
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7574cc7c-e5a1-4b7c-97f6-0cffb1a5d536
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; mandia
ms.openlocfilehash: efbacb534fc7f11e9b593aae4383480ce3a1752f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-logic-app-using-a-template"></a>Creación de una aplicación lógica mediante una plantilla
Las plantillas proporcionan una forma rápida toouse conectores diferentes dentro de una aplicación de lógica. Las aplicaciones lógicas incluye plantillas de Azure Resource Manager para toocreate una aplicación de la lógica que puede ser usado toodefine flujos de trabajo empresariales. Puede definir qué recursos se implementan y cómo toodefine parámetros al implementar la aplicación lógica. Puede usar esta plantilla para sus propios escenarios empresariales, o personalizar toomeet sus requisitos.

Para obtener más detalles sobre las propiedades de la aplicación hello lógica, consulte [API de administración de flujo de trabajo de aplicación lógica](https://msdn.microsoft.com/library/azure/mt643788.aspx). 

Para obtener ejemplos de la propia definición de hello, consulte [definiciones de aplicación lógica de autor](logic-apps-author-definitions.md). 

Para obtener más información sobre la creación de plantillas, consulte [Creación de plantillas de Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).

Para la plantilla de hello completa, consulte [plantilla de aplicación lógica](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).

## <a name="what-you-deploy"></a>¿Qué se puede implementar?
Con esta plantilla, implementará una aplicación lógica.

implementación de hello toorun automáticamente, seleccione Hola después de botón:  

[![Implementar tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)

## <a name="parameters"></a>parameters
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a>testUri
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-toodeploy"></a>Toodeploy de recursos
### <a name="logic-app"></a>Aplicación lógica
Crea la aplicación de la lógica de hello.

plantillas de Hello usa un valor de parámetro para el nombre de la aplicación hello lógica. Establece la ubicación de Hola de toohello de aplicación lógica de hello misma ubicación que el grupo de recursos de Hola. 

Esta definición en particular ejecuta una vez cada hora y pings Hola ubicación especificada en hello **testUri** parámetro. 

    {
      "type": "Microsoft.Logic/workflows",
      "apiVersion": "2016-06-01",
      "name": "[parameters('logicAppName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "LogicApp"
      },
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      }
    }


## <a name="commands-toorun-deployment"></a>Implementación de toorun de comandos
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Azure CLI
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



