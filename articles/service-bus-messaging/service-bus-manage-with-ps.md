---
title: recursos de Service Bus de Azure de aaaUse PowerShell toomanage | Documentos de Microsoft
description: "Usar toocreate de módulo de PowerShell y administrar recursos de Bus de servicio"
services: service-bus-messaging
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: sethm
ms.openlocfilehash: 737044def913c5798e7e05fc4f1aeece76c8f4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-service-bus-resources"></a>Usar recursos de Bus de servicio de toomanage de PowerShell

Microsoft Azure PowerShell es un entorno de scripting que puede usar toocontrol y automatizar la implementación de Hola y administración de servicios de Azure. Este artículo se describe cómo hello toouse [módulo de PowerShell del Administrador de recursos del Bus de servicio](/powershell/module/azurerm.servicebus) tooprovision y administrar las entidades de Bus de servicio (espacios de nombres, colas, temas y suscripciones) mediante una consola de PowerShell de Azure local o secuencia de comandos.

Las entidades de Service Bus también se pueden administrar mediante plantillas de Azure Resource Manager. Para obtener más información, vea el artículo de hello [recursos de Bus de servicio crear usando plantillas del Administrador de recursos de Azure](service-bus-resource-manager-overview.md).

## <a name="prerequisites"></a>Requisitos previos

Antes de empezar, necesitará siguiente hello:

* Una suscripción de Azure. Para obtener más información sobre cómo obtener una suscripción, consulte [Opciones de compra][purchase options], [ofertas para miembros][member offers] o [cuenta gratuita][free account].
* Un equipo con Azure PowerShell. Para obtener instrucciones, consulte [Introducción a los cmdlets de Azure PowerShell](/powershell/azure/get-started-azureps).
* Una descripción general de scripts de PowerShell, paquetes de NuGet y Hola .NET Framework.

## <a name="get-started"></a>Primeros pasos

Hola primer paso es toouse PowerShell toolog en tooyour cuenta de Azure y suscripción de Azure. Siga las instrucciones de hello en [empezar a trabajar con cmdlets de PowerShell de Azure](/powershell/azure/get-started-azureps) toolog en tooyour cuenta de Azure y recuperar y acceder a recursos de hello en su suscripción de Azure.

## <a name="provision-a-service-bus-namespace"></a>Aprovisionar un espacio de nombres de Service Bus

Al trabajar con espacios de nombres de Bus de servicio, puede usar hello [Get AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), y [AzureRmServiceBusNamespace conjunto](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.

Este ejemplo crea algunas variables locales en el script de Hola; `$Namespace` y `$Location`.

* `$Namespace`es el nombre de Hola de Hola de espacio de nombres de Bus de servicio con el que se desea toowork.
* `$Location`identifica el centro de datos de hello en el que se ofrece el espacio de nombres de Hola.
* `$CurrentNamespace`almacena el espacio de nombres de referencia de Hola que se recuperan (o crear).

En un script real, `$Namespace` y `$Location` se pueden pasar como parámetros.

Esta parte del script de Hola Hola siguientes:

1. El nombre especificado de intentos tooretrieve un espacio de nombres de Bus de servicio con hello.
2. Si se encuentra el espacio de nombres de hello, informa de lo que se encontró.
3. Si no se encuentra el espacio de nombres de hello, se crea el espacio de nombres de hello y, a continuación, recupera Hola que acaba de crear espacio de nombres.
   
    ``` powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a>Creación de una regla de autorización de espacios de nombres

Hello en el ejemplo siguiente se muestra cómo usar las reglas de autorización de espacio de nombres de toomanage Hola [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Conjunto AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), y [cmdlets Remove-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).

```powershell
# Query toosee if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if hello rule already exists or needs toobe created
if ($CurrentRule)
{
    Write-Host "hello $AuthRule rule already exists for hello namespace $Namespace."
}
else
{
    Write-Host "hello $AuthRule rule does not exist."
    Write-Host "Creating hello $AuthRule rule for hello $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "hello $AuthRule rule for hello $Namespace namespace has been successfully created."

    Write-Host "Setting rights on hello namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights toohello namespace"
    $authRuleObj.Rights.Add("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj
    $authRuleObj.Rights.Add("Manage")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Show value of primary key"
    $CurrentKey = Get-AzureRmServiceBusNamespaceKey -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
        
    Write-Host "Remove this authorization rule"
    Remove-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
}
```

## <a name="create-a-queue"></a>Creación de una cola

toocreate una cola o tema, realice una comprobación de espacio de nombres mediante el script de Hola en la sección anterior de Hola. A continuación, cree la cola de hello:

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "hello queue $QueueName already exists in hello $Location region:"
}
else
{
    Write-Host "hello $QueueName queue does not exist."
    Write-Host "Creating hello $QueueName queue in hello $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "hello $QueueName queue in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a>Modificación de las propiedades de una cola

Después de ejecutar script de Hola Hola sección anterior, puede usar hello [AzureRmServiceBusQueue conjunto](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) propiedades de hello tooupdate de cmdlet de una cola, como en el siguiente ejemplo de Hola:

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a>Aprovisionamiento de otras entidades de Service Bus

Puede usar hello [módulo de PowerShell de Service Bus](/powershell/module/azurerm.servicebus) tooprovision otras entidades, como temas y suscripciones. Estos cmdlets son sintácticamente similar cmdlets de creación de cola toohello mostrados en la sección anterior de Hola.

## <a name="next-steps"></a>Pasos siguientes

- Consulte documentación del módulo de PowerShell Administrador de recursos del Bus de servicio completa de hello [aquí](/powershell/module/azurerm.servicebus). Esta página enumera todos los cmdlets disponibles.
- Para obtener información sobre el uso de plantillas del Administrador de recursos de Azure, vea el artículo de hello [recursos de Bus de servicio crear usando plantillas del Administrador de recursos de Azure](service-bus-resource-manager-overview.md).
- Información sobre las [bibliotecas de administración de .NET de Service Bus](service-bus-management-libraries.md).

Hay algunas formas alternativas toomanage entidades de Bus de servicio, como se describe en estas entradas de blog:

* [¿Cómo toocreate Service Bus colas, temas y suscripciones mediante un script de PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [¿Cómo toocreate un Namespace de Bus de servicio y un centro de eventos mediante un script de PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [Scripts de PowerShell de Service Bus](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
