---
title: espacio de nombres de Bus de servicio de aaaCreate mediante una plantilla de Azure Resource Manager | Documentos de Microsoft
description: Use el Administrador de recursos de Azure plantilla toocreate un espacio de nombres de Bus de servicio
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: dc0d6482-6344-4cef-8644-d4573639f5e4
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: fddf370affe761a734991ae9b60c1e5825e54ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a>Creación de un espacio de nombres del Bus de servicio mediante una plantilla de Azure Resource Manager

Este artículo describe cómo toouse una plantilla de administrador de recursos de Azure que crea un espacio de nombres de Bus de servicio de tipo **mensajería** a una SKU Standard/Basic. artículo de Hello también define los parámetros de Hola que se especifican para la ejecución de Hola de implementación de Hola. Puede usar esta plantilla para sus propias implementaciones o personalizarlo toomeet sus requisitos.

Para más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates] (Creación de plantillas de Azure Resource Manager).

Para la plantilla completa de hello, vea hello [plantilla de espacio de nombres de Bus de servicio] [ Service Bus namespace template] en GitHub.

> [!NOTE]
> Hola siguiendo las plantillas del Administrador de recursos de Azure está disponible para su descarga e implementación. 
> 
> * [Creación de un espacio de nombres de Bus de servicio con cola](service-bus-resource-manager-namespace-queue.md)
> * [Creación de un espacio de nombres de Bus de servicio con un tema y una suscripción](service-bus-resource-manager-namespace-topic.md)
> * [Creación de un espacio de nombres de Bus de servicio con regla de autorización y cola](service-bus-resource-manager-namespace-auth-rule.md)
> * [Create a Service Bus namespace with topic, subscription, and rule](service-bus-resource-manager-namespace-topic-with-rule.md) (Creación de un espacio de nombres de Service Bus con tema, suscripción y regla)
> 
> toocheck para las plantillas de hello más recientes, visite hello [plantillas de inicio rápido de Azure] [ Azure Quickstart Templates] galería y búsqueda de Bus de servicio.
> 
> 

## <a name="what-will-you-deploy"></a>¿Qué va a implementar?
Con esta plantilla, implementará un espacio de nombres de Service Bus con una SKU de nivel [básico, estándar o premium](https://azure.microsoft.com/pricing/details/service-bus/).

toorun Hola implementación automáticamente, haga clic en hello después de botón:

[![Implementar tooAzure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)

## <a name="parameters"></a>parameters
Con el Administrador de recursos de Azure, se definen parámetros para los valores que desee toospecify cuando se implementa Hola plantilla. plantilla de Hello incluye una sección denominada `Parameters` que contiene todos los valores de parámetro de Hola. Debe definir un parámetro para aquellos valores que varían en función de que va a implementar el proyecto de Hola o según va a implementar en el entorno de Hola. No se define parámetros para valores que siempre permanecerá Hola igual. Cada valor de parámetro se usa en hello plantilla toodefine Hola los recursos que se implementan.

Esta plantilla define Hola parámetros siguientes.

### <a name="servicebusnamespacename"></a>serviceBusNamespaceName
nombre de Hola de toocreate de espacio de nombres de Bus de servicio de Hola.

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a>serviceBusSKU
nombre de Hola de hello Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.

```json
"serviceBusSku": { 
    "type": "string", 
    "allowedValues": [ 
        "Basic", 
        "Standard",
        "Premium" 
    ], 
    "defaultValue": "Standard", 
    "metadata": { 
        "description": "hello messaging tier for service Bus namespace" 
    } 

```

plantilla de Hello define los valores de hello permitidas para este parámetro (Basic, Standard o Premium) y asigna un valor predeterminado (estándar) si no se especifica ningún valor.

Para más información sobre los precios de Service Bus, consulte [Precios y facturación de Service Bus][Service Bus pricing and billing].

### <a name="servicebusapiversion"></a>serviceBusApiVersion
versión de API de Service Bus de Hola de plantilla de Hola.

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by hello template" 
       } 
```

## <a name="resources-toodeploy"></a>Toodeploy de recursos
### <a name="service-bus-namespace"></a>Espacio de nombres de Bus de servicio
Crea un espacio de nombres de Bus de servicio estándar de tipo **Mensajería**.

```json
"resources": [
    {
        "apiVersion": "[parameters('serviceBusApiVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "properties": {
        }
    }
]
```

## <a name="commands-toorun-deployment"></a>Implementación de toorun de comandos
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a>Azure CLI
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha creado e implementado recursos con el Administrador de recursos de Azure, obtenga información acerca de cómo toomanage estos recursos, lea los siguientes artículos:

* [Administración de Service Bus con PowerShell](service-bus-manage-with-ps.md)
* [Administrar recursos de Service Bus con hello Explorador de Bus de servicio](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
