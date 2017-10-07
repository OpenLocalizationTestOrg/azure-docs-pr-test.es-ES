---
title: recursos de Service Bus de Azure de aaaCreate usando plantillas del Administrador de recursos de Azure | Documentos de Microsoft
description: "Utilizar la creación de Azure Resource Manager plantillas tooautomate Hola de recursos de Bus de servicio"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 24f6a207-0fa4-49cf-8a58-963f9e2fd655
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: e539902cae307b63ae7c332580e2064761331ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a>Creación de recursos de Bus de servicio con las plantillas de Azure Resource Manager

Este artículo se describe cómo toocreate e implementar recursos de Bus de servicio mediante plantillas, PowerShell y proveedor de recursos de Bus de servicio de hello Azure Resource Manager.

Plantillas de administrador de recursos de Azure ayudan a definir hello toodeploy de recursos para una solución y toospecify parámetros y variables que permiten valores tooinput para diferentes entornos. plantilla de Hello consta de JSON y expresiones que puede utilizar valores de tooconstruct para su implementación. Para obtener información detallada sobre cómo escribir plantillas del Administrador de recursos de Azure y una explicación del formato de la plantilla de hello, consulte [estructura y la sintaxis de plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

> [!NOTE]
> Hola ejemplos en esta presentación de artículo cómo toouse Azure Resource Manager toocreate un espacio de nombres de Bus de servicio y la mensajería de entidad (cola). Para obtener ejemplos de la plantilla, visite hello [Galería de plantillas de inicio rápido de Azure] [ Azure Quickstart Templates gallery] y busque "Bus de servicio".
>
>

## <a name="service-bus-resource-manager-templates"></a>Plantillas de Resource Manager para Service Bus

Estas plantillas de Service Bus y Azure Resource Manager están disponibles para su descarga e implementación. Haga clic en hello siguientes vínculos para obtener más información acerca de cada uno, con plantillas de toohello de vínculos en GitHub:

* [Creación de un espacio de nombres de bus de servicio](service-bus-resource-manager-namespace.md)
* [Creación de un espacio de nombres de Bus de servicio con cola](service-bus-resource-manager-namespace-queue.md)
* [Creación de un espacio de nombres de Bus de servicio con un tema y una suscripción](service-bus-resource-manager-namespace-topic.md)
* [Creación de un espacio de nombres de Bus de servicio con regla de autorización y cola](service-bus-resource-manager-namespace-auth-rule.md)
* [Creación de un espacio de nombres de Service Bus con un tema, una suscripción y una regla](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a>Implementación con PowerShell

Hello siguiente procedimiento describe cómo toouse PowerShell toodeploy una plantilla de administrador de recursos de Azure que crea un **estándar** de nivel de espacio de nombres de Bus de servicio y una cola dentro de ese espacio de nombres. En este ejemplo se basa en hello [crear un espacio de nombres de Bus de servicio con cola](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) plantilla. flujo de trabajo aproximado de Hello es como sigue:

1. Instale PowerShell.
2. Crear plantilla de Hola y (opcionalmente) un archivo de parámetros.
3. En PowerShell, inicie sesión en tooyour cuenta de Azure.
4. Si no existe, cree un nuevo grupo de recursos.
5. Probar la implementación de Hola.
6. Si lo desea, establezca el modo de implementación de Hola.
7. Implementar la plantilla de Hola.

Para obtener información completa sobre la implementación de plantillas de Azure Resource Manager, vea [Implementación de recursos con las plantillas de Azure Resource Manager][Deploy resources with Azure Resource Manager templates].

### <a name="install-powershell"></a>Instale PowerShell.

Instale Azure PowerShell siguiendo las instrucciones de hello en [Introducción a Azure PowerShell](/powershell/azure/get-started-azureps).

### <a name="create-a-template"></a>Creación de una plantilla

Hola de clon o una copia [201-servicebus-Crear-cola](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) plantilla desde GitHub:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by hello template"
            }
        }
    },
    "variables": {
        "location": "[resourceGroup().location]",
        "sbVersion": "[parameters('serviceBusApiVersion')]",
        "defaultSASKeyName": "RootManageSharedAccessKey",
        "authRuleResourceId": "[resourceId('Microsoft.ServiceBus/namespaces/authorizationRules', parameters('serviceBusNamespaceName'), variables('defaultSASKeyName'))]"
    },
    "resources": [{
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
                "path": "[parameters('serviceBusQueueName')]"
            }
        }]
    }],
    "outputs": {
        "NamespaceConnectionString": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryConnectionString]"
        },
        "SharedAccessPolicyPrimaryKey": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryKey]"
        }
    }
}
```

### <a name="create-a-parameters-file-optional"></a>Creación de un archivo de parámetros (opcional)

toouse un archivo de parámetros opcionales, Hola copia [201-servicebus-Crear-cola](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) archivo. Reemplazar el valor de Hola de `serviceBusNamespaceName` con nombre hello del espacio de nombres de Bus de servicio de Hola que desee toocreate en esta implementación y reemplazar el valor de Hola de `serviceBusQueueName` con el nombre de Hola de cola de hello desea toocreate.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "value": "<myNamespaceName>"
        },
        "serviceBusQueueName": {
            "value": "<myQueueName>"
        },
        "serviceBusApiVersion": {
            "value": "2015-08-01"
        }
    }
}
```

Para obtener más información, vea hello [parámetros](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) tema.

### <a name="log-in-tooazure-and-set-hello-azure-subscription"></a>Inicie sesión en tooAzure y establecer Hola suscripción de Azure

Desde un símbolo del sistema de PowerShell, ejecute el siguiente comando de hello:

```powershell
Login-AzureRmAccount
```

Son toolog solicitada en tooyour cuenta de Azure. Después de iniciar sesión, ejecute hello después comando tooview las suscripciones disponibles.

```powershell
Get-AzureRMSubscription
```

Este comando devuelve una lista de suscripciones de Azure disponibles. Elija una suscripción para hello sesión actual ejecutando el siguiente comando de Hola. Reemplace `<YourSubscriptionId>` con hello GUID para hello suscripción de Azure que desee toouse.

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-hello-resource-group"></a>Grupo de recursos de Hola de conjunto

Si no tiene un recurso existente de grupo, cree un nuevo grupo de recursos con Hola ** New-AzureRmResourceGroup ** comando. Proporcione el nombre de hello del grupo de recursos de Hola y la ubicación que desee toouse. Por ejemplo:

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

Si se realiza correctamente, se muestra un resumen del nuevo grupo de recursos Hola.

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-hello-deployment"></a>Implementación de prueba de Hola

Validación de la implementación mediante la ejecución de hello `Test-AzureRmResourceGroupDeployment` cmdlet. Al probar la implementación de hello, proporcionar parámetros exactamente como lo haría al ejecutar la implementación de Hola.

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="create-hello-deployment"></a>Crear implementación de Hola

toocreate Hola nueva implementación, ejecute hello `New-AzureRmResourceGroupDeployment` cmdlet y proporcionar los parámetros necesarios de hello cuando se le solicite. parámetros de Hello incluyen un nombre para la implementación, el nombre de Hola de su grupo de recursos y la ruta de acceso de Hola o el archivo de plantilla de dirección URL toohello. Si hello **modo** no se especifica el parámetro, Hola valor predeterminado de **Incremental** se utiliza. Para más información, vea [Implementaciones incrementales y completas](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).

Hola después de símbolo del sistema, para los parámetros de hello tres en la ventana de PowerShell de hello:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

toospecify un archivo de parámetros en su lugar, use Hola siguiente comando.

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -TemplateParameterFile <path tooparameters file>\azuredeploy.parameters.json
```

También puede utilizar parámetros en línea cuando se ejecuta el cmdlet de implementación de Hola. comando Hello es como sigue:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -parameterName "parameterValue"
```

toorun una [completa](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) implementación, conjunto hello **modo** parámetro demasiado**completar**:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="verify-hello-deployment"></a>Comprobar la implementación de Hola
Si los recursos de Hola se implementan correctamente, se muestra un resumen de implementación de hello en la ventana de PowerShell de hello:

```powershell
DeploymentName    : MyDemoDeployment
ResourceGroupName : MyDemoRG
ProvisioningState : Succeeded
Timestamp         : 4/19/2016 10:38:30 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
                    Name             Type                       Value
                    ===============  =========================  ==========
                    serviceBusNamespaceName  String             <namespaceName>
                    serviceBusQueueName  String                 <queueName>
                    serviceBusApiVersion  String                2015-08-01

```

## <a name="next-steps"></a>Pasos siguientes
Ahora ha visto el flujo de trabajo básico de Hola y comandos para la implementación de una plantilla de Azure Resource Manager. Para obtener más información, visite Hola siguientes vínculos:

* [Información general sobre Azure Resource Manager][Azure Resource Manager overview]
* [Implementación de recursos con las plantillas de Resource Manager y Azure PowerShell][Deploy resources with Azure Resource Manager templates]
* [Creación de plantillas del Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
