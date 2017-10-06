---
title: "aaaProvision una caché en Redis mediante el Administrador de recursos de Azure | Documentos de Microsoft"
description: "Use el Administrador de recursos de Azure plantilla toodeploy una caché en Redis de Azure."
services: app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: ce6f5372-7038-4655-b1c5-108f7c148282
ms.service: cache
ms.workload: web
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 46e7b3b2493ac51dbe6bab0b086304802afc5d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-redis-cache-using-a-template"></a>Creación de una Caché en Redis mediante una plantilla
En este tema, aprenderá cómo toocreate una plantilla de Azure Resource Manager que implementa una caché en Redis. caché de Hello puede utilizarse con un almacenamiento cuenta tookeep diagnóstico los datos existentes. También aprenderá cómo toodefine qué recursos se implementan y cómo toodefine parámetros que especifican cuando se ejecuta la implementación de Hola. Puede usar esta plantilla para sus propias implementaciones o personalizarlo toomeet sus requisitos.

Actualmente, se comparten la configuración de diagnóstico para todas las memorias caché en hello misma región para una suscripción. La actualización de una memoria caché en la región de hello afecta a todas las demás cachés región Hola.

Para obtener más información sobre la creación de plantillas, consulte [Creación de plantillas de Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).

Para la plantilla de hello completa, consulte [plantilla caché de Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).

> [!NOTE]
> Plantillas de administrador de recursos para hello nueva [nivel Premium](cache-premium-tier-intro.md) están disponibles. 
> 
> * [Crear una caché en Redis Premium con agrupación en clústeres](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [Crear una caché en Redis Premium con persistencia de datos](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [Crear una caché en Redis Premium con una red virtual y agrupación en clústeres opcional](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> toocheck para las plantillas de hello más recientes, consulte [plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/) y busque `Redis Cache`.
> 
> 

## <a name="what-you-will-deploy"></a>Lo que implementará
En esta plantilla, implementará una caché en Redis de Azure que utiliza una cuenta de almacenamiento de datos de diagnóstico.

toorun Hola implementación automáticamente, haga clic en hello después de botón:

[![Implementar tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)

## <a name="parameters"></a>parameters
Con el Administrador de recursos de Azure, se definen parámetros para los valores que desee toospecify cuando se implementa Hola plantilla. plantilla de Hello incluye una sección denominada parámetros que contiene todos los valores de parámetro de Hola.
Debe definir un parámetro para aquellos valores que varían en función de que va a implementar el proyecto de Hola o según va a implementar en el entorno de Hola. No se define parámetros para valores que permanezcan siempre Hola igual. Cada valor de parámetro se usa en hello plantilla toodefine Hola los recursos que se implementan. 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a>redisCacheLocation
ubicación de Hola de hello caché en Redis. Para un rendimiento óptimo, utilice Hola misma ubicación como Hola toobe de aplicación que se usa con la caché de Hola.

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a>existingDiagnosticsStorageAccountName
nombre de Hola de hello toouse de cuenta de almacenamiento existente para diagnósticos. 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a>enableNonSslPort
Un valor booleano que indica si tooallow acceden a través de puertos no SSL.

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a>diagnosticsStatus
Un valor que indica si están activados los diagnósticos. Utilice ON (activados) u OFF (desactivados).

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-toodeploy"></a>Toodeploy de recursos
### <a name="redis-cache"></a>Redis Cache
Crea Hola caché en Redis de Azure.

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('redisCacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[parameters('redisCacheLocation')]",
      "properties": {
        "enableNonSslPort": "[parameters('enableNonSslPort')]",
        "sku": {
          "capacity": "[parameters('redisCacheCapacity')]",
          "family": "[parameters('redisCacheFamily')]",
          "name": "[parameters('redisCacheSKU')]"
        }
      },
      "resources": [
        {
          "apiVersion": "2015-07-01",
          "type": "Microsoft.Cache/redis/providers/diagnosticsettings",
          "name": "[concat(parameters('redisCacheName'), '/Microsoft.Insights/service')]",
          "location": "[parameters('redisCacheLocation')]",
          "dependsOn": [
            "[concat('Microsoft.Cache/Redis/', parameters('redisCacheName'))]"
          ],
          "properties": {
            "status": "[parameters('diagnosticsStatus')]",
            "storageAccountName": "[parameters('existingDiagnosticsStorageAccountName')]"
          }
        }
      ]
    }



## <a name="commands-toorun-deployment"></a>Implementación de toorun de comandos
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a>Azure CLI
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


