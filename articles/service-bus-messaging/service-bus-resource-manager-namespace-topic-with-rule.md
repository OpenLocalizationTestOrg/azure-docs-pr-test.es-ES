---
title: "aaaCreate suscripción de tema de Bus de servicio de Azure y regla con la plantilla del Administrador de recursos de Azure | Documentos de Microsoft"
description: "Creación de un espacio de nombres de Bus de servicio con un tema, una suscripción y una regla mediante una plantilla de Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9e0aaf58-0214-4bca-bd00-d29c08f9b1bc
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: dbc46da8491aee4d0c73bd4db90c696008920df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a>Creación de un espacio de nombres de Bus de servicio con un tema, una suscripción y una regla mediante una plantilla de Azure Resource Manager

Este artículo muestra cómo toouse una plantilla de administrador de recursos de Azure crea un espacio de nombres de Bus de servicio con un tema, la suscripción y la regla (filtro). Aprenderá cómo toodefine qué recursos se implementan y cómo toodefine parámetros que especifican cuando se ejecuta la implementación de Hola. Puede usar esta plantilla para sus propias implementaciones o personalizarlo toomeet los requisitos

Para más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates] (Creación de plantillas de Azure Resource Manager).

Para más información sobre prácticas y patrones de convenciones de nomenclatura de recursos de Azure, consulte [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources](Convenciones de nomenclatura recomendadas para los recursos de Azure).

Para la plantilla completa de hello, vea hello [espacio de nombres de Bus de servicio con el tema y suscripción, regla] [ Service Bus namespace with topic, subscription, and rule] plantilla.

> [!NOTE]
> Hola siguiendo las plantillas del Administrador de recursos de Azure está disponible para su descarga e implementación.
> 
> * [Creación de un espacio de nombres de Bus de servicio con regla de autorización y cola](service-bus-resource-manager-namespace-auth-rule.md)
> * [Creación de un espacio de nombres de Bus de servicio con cola](service-bus-resource-manager-namespace-queue.md)
> * [Creación de un espacio de nombres de bus de servicio](service-bus-resource-manager-namespace.md)
> * [Creación de un espacio de nombres de Bus de servicio con un tema y una suscripción](service-bus-resource-manager-namespace-topic.md)
> 
> toocheck para las plantillas de hello más recientes, visite hello [plantillas de inicio rápido de Azure] [ Azure Quickstart Templates] galería y búsqueda de Bus de servicio.
> 
> 

## <a name="what-will-you-deploy"></a>¿Qué va a implementar?

Con esta plantilla, implementará un espacio de nombres de Bus de servicio con un tema, una suscripción y una regla (filtro).

Los [temas y suscripciones de Service Bus](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) proporcionan una o varias formas de comunicación en un patrón *publicación/suscripción*. Cuando se usan temas y suscripciones, componentes de una aplicación distribuida no se comunican directamente entre sí, en su lugar que intercambian mensajes a través del tema que actúa como intermediario. Un tema de tooa de suscripción es similar a una cola virtual que recibe copias de mensajes que se enviaron toohello tema. Un filtro de suscripción le permite toospecify que envían los mensajes tooa tema debe aparecer dentro de una suscripción de tema específico.

## <a name="what-are-rules-filters"></a>¿Cuáles son las reglas (filtros)?

En muchos escenarios, los mensajes que tienen características específicas deben procesarse de maneras diferentes. tooenable esto, puede configurar mensajes de toofind de las suscripciones que tienen propiedades concretas y, a continuación, realizan propiedades toothose de modificaciones. Aunque las suscripciones de Bus de servicio ven todos los mensajes enviados toohello tema, puede copiar solo un subconjunto de esas cola de mensajes toohello suscripción virtual. Esto se consigue mediante los filtros de suscripción. toolearn más información acerca de las reglas (filtros), consulte [reglas y acciones](service-bus-queues-topics-subscriptions.md#rules-and-actions).

toorun Hola implementación automáticamente, haga clic en hello después de botón:

[![Implementar tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)

## <a name="parameters"></a>parameters

Con el Administrador de recursos de Azure, debe definir parámetros para los valores que desee toospecify cuando se implementa Hola plantilla. plantilla de Hello incluye una sección denominada `Parameters` que contiene todos los valores de parámetro de Hola. Debe definir un parámetro para aquellos valores que varían en función de que va a implementar el proyecto de Hola o según va a implementar en el entorno de Hola. No se define parámetros para valores que permanezcan siempre Hola igual. Cada valor de parámetro se usa en hello plantilla toodefine Hola los recursos que se implementan.

plantilla de Hello define Hola parámetros siguientes:

### <a name="servicebusnamespacename"></a>serviceBusNamespaceName
nombre de Hola de toocreate de espacio de nombres de Bus de servicio de Hola.

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a>serviceBusTopicName
nombre de Hola de tema de hello creado en el espacio de nombres de Bus de servicio de Hola.

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a>serviceBusSubscriptionName
nombre de Hola de suscripción de hello creado en el espacio de nombres de Bus de servicio de Hola.

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a>serviceBusRuleName
nombre de Hola de rule(filter) Hola creado en el espacio de nombres de Bus de servicio de Hola.

```json
   "serviceBusRuleName": {
   "type": "string",
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
Crea un espacio de nombres de Bus de servicio estándar de tipo **Mensajería**con tema, suscripción y reglas.

```json
 "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "sku": {
            "name": "Standard",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]"
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {},
                "resources": [{
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusRuleName')]",
                    "type": "Rules",
                    "dependsOn": [
                        "[parameters('serviceBusSubscriptionName')]"
                    ],
                    "properties": {
                        "filter": {
                            "sqlExpression": "StoreName = 'Store1'"
                        },
                        "action": {
                            "sqlExpression": "set FilterTag = 'true'"
                        }
                    }
                }]
            }]
        }]
    }]
```

## <a name="commands-toorun-deployment"></a>Implementación de toorun de comandos
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a>Azure CLI
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha creado e implementado recursos con el Administrador de recursos de Azure, obtenga información acerca de cómo toomanage estos recursos mediante la visualización de estos artículos:

* [Administración de Azure Service Bus](service-bus-management-libraries.md)
* [Administración de Service Bus con PowerShell](service-bus-manage-with-ps.md)
* [Administrar recursos de Service Bus con hello Explorador de Bus de servicio](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

