---
title: "regla de autorización de Bus de servicio aaaCreate con plantilla del Administrador de recursos de Azure | Documentos de Microsoft"
description: "Creación de una regla de autorización de Bus de servicio para un espacio de nombres y una cola mediante una plantilla de Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f1443a0-5fa8-4d90-8637-1a977ef0b1f0
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 48df97849281d3b47e9d722d4e821c874644be59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-authorization-rule-for-namespace-and-queue-using-an-azure-resource-manager-template"></a>Creación de una regla de autorización de Bus de servicio para un espacio de nombres y una cola mediante una plantilla de Azure Resource Manager

Este artículo se muestra cómo toouse una plantilla de administrador de recursos de Azure que crea un [regla de autorización](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) para un espacio de nombres de Bus de servicio y una cola. Obtendrá información sobre cómo toodefine qué recursos se implementan y cómo toodefine parámetros que especifican cuando se ejecuta la implementación de Hola. Puede usar esta plantilla para sus propias implementaciones o personalizarlo toomeet sus requisitos.

Para más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates] (Creación de plantillas de Azure Resource Manager).

Para la plantilla completa de hello, vea hello [plantilla de regla de autorización de Bus de servicio] [ Service Bus auth rule template] en GitHub.

> [!NOTE]
> Hola siguiendo las plantillas del Administrador de recursos de Azure está disponible para su descarga e implementación.
> 
> * [Creación de un espacio de nombres de bus de servicio](service-bus-resource-manager-namespace.md)
> * [Creación de un espacio de nombres de Bus de servicio con cola](service-bus-resource-manager-namespace-queue.md)
> * [Creación de un espacio de nombres de Bus de servicio con un tema y una suscripción](service-bus-resource-manager-namespace-topic.md)
> * [Create a Service Bus namespace with topic, subscription, and rule](service-bus-resource-manager-namespace-topic-with-rule.md) (Creación de un espacio de nombres de Service Bus con tema, suscripción y regla)
> 
> toocheck para las plantillas de hello más recientes, visite hello [plantillas de inicio rápido de Azure] [ Azure Quickstart Templates] galería y busque "Bus de servicio".
> 
> 

## <a name="what-will-you-deploy"></a>¿Qué va a implementar?
Con esta plantilla, implementará una regla de autorización de Bus de servicio para una entidad de mensajería y espacio de nombres (una cola en este caso).

Esta plantilla usa la [firma de acceso compartido (SAS)](service-bus-sas.md) para la autenticación. SAS permite que las aplicaciones tooauthenticate tooService Bus mediante una clave de acceso configurada en el espacio de nombres de Hola o en hello entidad (cola o tema) de mensajería con qué derechos específicos que están asociados. A continuación, puede usar esta clave toogenerate un token SAS que los clientes pueden usar a su vez tooauthenticate tooService Bus.

toorun Hola implementación automáticamente, haga clic en hello después de botón:

[![Implementar tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)

## <a name="parameters"></a>parameters

Con el Administrador de recursos de Azure, se definen parámetros para los valores que desee toospecify cuando se implementa Hola plantilla. plantilla de Hello incluye una sección denominada `Parameters` que contiene todos los valores de parámetro de Hola. Debe definir un parámetro para aquellos valores que varían en función de que va a implementar el proyecto de Hola o según va a implementar en el entorno de Hola. No se define parámetros para valores que siempre permanecerá Hola igual. Cada valor de parámetro se usa en hello plantilla toodefine Hola los recursos que se implementan.

plantilla de Hello define Hola parámetros siguientes.

### <a name="servicebusnamespacename"></a>serviceBusNamespaceName
nombre de Hola de toocreate de espacio de nombres de Bus de servicio de Hola.

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="namespaceauthorizationrulename"></a>namespaceAuthorizationRuleName
nombre de Hola de regla de autorización de hello para el espacio de nombres de Hola.

```json
"namespaceAuthorizationRuleName ": {
"type": "string"
}
```

### <a name="servicebusqueuename"></a>serviceBusQueueName
nombre de Hola de cola de hello en el espacio de nombres de Bus de servicio de Hola.

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a>serviceBusApiVersion
versión de API de Service Bus de Hola de plantilla de Hola.

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a>Toodeploy de recursos
Crea un espacio de nombres de Bus de servicio estándar de tipo **Mensajería**y una regla de autorización de Bus de servicio para el espacio de nombres y la entidad.

```json
"resources": [
        {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusNamespaceName')]",
            "type": "Microsoft.ServiceBus/namespaces",
            "location": "[variables('location')]",
            "kind": "Messaging",
            "sku": {
                "name": "StandardSku",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusQueueName')]",
                    "type": "Queues",
                    "dependsOn": [
                        "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('serviceBusQueueName')]"
                    },
                    "resources": [
                        {
                            "apiVersion": "[variables('sbVersion')]",
                            "name": "[parameters('queueAuthorizationRuleName')]",
                            "type": "authorizationRules",
                            "dependsOn": [
                                "[parameters('serviceBusQueueName')]"
                            ],
                            "properties": {
                                "Rights": ["Listen"]
                            }
                        }
                    ]
                }
            ]
        }, {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[variables('namespaceAuthRuleName')]",
            "type": "Microsoft.ServiceBus/namespaces/authorizationRules",
            "dependsOn": ["[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"],
            "location": "[resourceGroup().location]",
            "properties": {
                "Rights": ["Send"]
            }
        }
    ]
```

## <a name="commands-toorun-deployment"></a>Implementación de toorun de comandos
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="azure-cli"></a>Azure CLI
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha creado e implementado recursos con el Administrador de recursos de Azure, obtenga información acerca de cómo toomanage estos recursos mediante la visualización de estos artículos:

* [Administración de Service Bus con PowerShell](service-bus-powershell-how-to-provision.md)
* [Administrar recursos de Service Bus con hello Explorador de Bus de servicio](https://github.com/paolosalvatori/ServiceBusExplorer/releases)
* [Autenticación y autorización de Bus de servicio](service-bus-authentication-and-authorization.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus auth rule template]: https://github.com/Azure/azure-quickstart-templates/blob/master/301-servicebus-create-authrule-namespace-and-queue/
