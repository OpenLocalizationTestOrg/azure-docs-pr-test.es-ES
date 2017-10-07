---
title: espacio de nombres de Bus de servicio de Azure de aaaCreate y poner en cola con la plantilla del Administrador de recursos de Azure | Documentos de Microsoft
description: "Creación de un espacio de nombres de Bus de servicio y una cola mediante una plantilla de Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a6bfb5fd-7b98-4588-8aa1-9d5f91b599b6
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: f230878b7c557bdd80d74da0de5a85ba4ee99ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-and-a-queue-using-an-azure-resource-manager-template"></a>Creación de un espacio de nombres de Bus de servicio mediante una plantilla de Azure Resource Manager

Este artículo muestra cómo toouse una plantilla de administrador de recursos de Azure crea un espacio de nombres de Bus de servicio y una cola dentro de ese espacio de nombres. Obtendrá información sobre cómo toodefine qué recursos se implementan y cómo toodefine parámetros que especifican cuando se ejecuta la implementación de Hola. Puede usar esta plantilla para sus propias implementaciones o personalizarlo toomeet sus requisitos.

Para más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates] (Creación de plantillas de Azure Resource Manager).

Para la plantilla completa de hello, vea hello [plantilla de espacio de nombres y de cola de Bus de servicio] [ Service Bus namespace and queue template] en GitHub.

> [!NOTE]
> Hola siguiendo las plantillas del Administrador de recursos de Azure está disponible para su descarga e implementación.
> 
> * [Creación de un espacio de nombres de Bus de servicio con regla de autorización y cola](service-bus-resource-manager-namespace-auth-rule.md)
> * [Creación de un espacio de nombres de Bus de servicio con un tema y una suscripción](service-bus-resource-manager-namespace-topic.md)
> * [Creación de un espacio de nombres de bus de servicio](service-bus-resource-manager-namespace.md)
> * [Create a Service Bus namespace with topic, subscription, and rule](service-bus-resource-manager-namespace-topic-with-rule.md) (Creación de un espacio de nombres de Service Bus con tema, suscripción y regla)
> 
> toocheck para las plantillas de hello más recientes, visite hello [plantillas de inicio rápido de Azure] [ Azure Quickstart Templates] galería y busque "Bus de servicio".
> 
> 

## <a name="what-will-you-deploy"></a>¿Qué va a implementar?

Con esta plantilla, implementará un espacio de nombres de Bus de servicio con una cola.

[Colas de Service Bus](service-bus-queues-topics-subscriptions.md#queues) ofrecen primero en ENTRAR, primero en salir (FIFO) mensaje entrega tooone o varios consumidores en competencia.

toorun Hola implementación automáticamente, haga clic en hello después de botón:

[![Implementar tooAzure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)

## <a name="parameters"></a>parameters

Con el Administrador de recursos de Azure, se definen parámetros para los valores que desee toospecify cuando se implementa Hola plantilla. plantilla de Hello incluye una sección denominada `Parameters` que contiene todos los valores de parámetro de Hola. Debe definir un parámetro para aquellos valores que varían en función de que va a implementar el proyecto de Hola o según va a implementar en el entorno de Hola. No se define parámetros para valores que siempre permanecerá Hola igual. Cada valor de parámetro se usa en hello plantilla toodefine Hola los recursos que se implementan.

plantilla de Hello define Hola parámetros siguientes.

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

### <a name="servicebusqueuename"></a>serviceBusQueueName
nombre de Hola de cola de hello creada en el espacio de nombres de Bus de servicio de Hola.

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
Crea un espacio de nombres de Bus de servicio estándar de tipo **Mensajería**con una cola.

```json
"resources ": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]",
            }
        }]
    }]
```

## <a name="commands-toorun-deployment"></a>Implementación de toorun de comandos
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="azure-cli"></a>Azure CLI

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha creado e implementado recursos con el Administrador de recursos de Azure, obtenga información acerca de cómo toomanage estos recursos mediante la visualización de estos artículos:

* [Administración de Service Bus con PowerShell](service-bus-manage-with-ps.md)
* [Administrar recursos de Service Bus con hello Explorador de Bus de servicio](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace and queue template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus queues]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
