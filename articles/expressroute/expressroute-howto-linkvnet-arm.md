---
title: 'Vincular un circuito de ExpressRoute de tooan de red virtual: PowerShell: Azure | Documentos de Microsoft'
description: "Este documento proporciona información general sobre cómo toolink virtual redes (redes virtuales) tooExpressRoute circuitos utilizando el modelo de implementación del Administrador de recursos de Hola y PowerShell."
services: expressroute
documentationcenter: na
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: daacb6e5-705a-456f-9a03-c4fc3f8c1f7e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: ganesr
ms.openlocfilehash: e75a9f6b42fa8e1a579e4f19882ec99b277b545f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a>Conectarse a un circuito de ExpressRoute de tooan de red virtual
> [!div class="op_single_selector"]
> * [Portal de Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [CLI de Azure](howto-linkvnet-cli.md)
> * [Vídeo: Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (clásico)](expressroute-howto-linkvnet-classic.md)
>

En este artículo le ayuda a vincular circuitos ExpressRoute de tooAzure de redes virtuales (Vnet) mediante el modelo de implementación del Administrador de recursos de Hola y PowerShell. Redes virtuales pueden ser Hola misma suscripción o parte de otra suscripción. Este artículo también muestra cómo vincular tooupdate una red virtual. 

## <a name="before-you-begin"></a>Antes de empezar
* Instalar versión más reciente de Hola de módulos de PowerShell de Azure de Hola. Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).
* Hola de revisión [requisitos previos](expressroute-prerequisites.md), [requisitos de enrutamiento](expressroute-routing.md), y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.
* Tiene que tener un circuito ExpressRoute activo. 
  * Siga las instrucciones de hello demasiado[crear un circuito ExpressRoute](expressroute-howto-circuit-arm.md) y tener habilitada por el proveedor de conectividad de circuito de Hola. 
  * Asegúrese de que dispone de un emparejamiento privado de Azure configurado para el circuito. Vea hello [configurar el enrutamiento de](expressroute-howto-routing-arm.md) artículo para las instrucciones de enrutamiento. 
  * Asegúrese de que el emparejamiento privado Azure está configurado y Hola emparejamiento de BGP entre la red y Microsoft está activo para que se puede habilitar la conectividad de extremo a extremo.
  * Asegúrese de que ha creado y aprovisionado totalmente una red virtual y una puerta de enlace de red virtual. Siga las instrucciones de hello demasiado[crear una puerta de enlace de red virtual para ExpressRoute](expressroute-howto-add-gateway-resource-manager.md). Una puerta de enlace de red virtual para ExpressRoute usa Hola el GatewayType 'ExpressRoute', no VPN.

* Puede vincular una circuito de ExpressRoute estándar de too10 redes virtuales tooa. Todas las redes virtuales deben estar en hello misma región geopolíticos cuando se usa un circuito de ExpressRoute estándar. 

* Puede vincular una red virtual fuera de la región geopolítica de Hola de hello circuito de ExpressRoute o conectar un mayor número de redes virtuales tooyour circuito ExpressRoute si ha habilitado el complemento de hello ExpressRoute premium. Comprobar hello [preguntas más frecuentes sobre](expressroute-faqs.md) para obtener más detalles sobre el complemento de hello premium.


## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Conectar una red virtual en hello mismo circuito de tooa de suscripción
Puede conectarse un tooan de puerta de enlace de red virtual circuito ExpressRoute mediante Hola siguiente cmdlet. Asegúrese de que esa puerta de enlace de red virtual de Hola se crea y está listo para crear un vínculo antes de ejecutar el cmdlet de hello:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Conectar una red virtual en un circuito de tooa otra suscripción
Puede compartir un circuito ExpressRoute entre varias suscripciones. Hola figura siguiente muestra un sencillo esquema de cómo compartir funciona para los circuitos ExpressRoute en varias suscripciones.

Cada una de las nubes más pequeñas de hello en nube de gran tamaño hello es toorepresent usado suscripciones que pertenecen los departamentos de toodifferent dentro de una organización. Cada uno de los departamentos de Hola de organización de hello puede utilizar su propia suscripción para implementar sus servicios, pero se puede compartir una sola red de ExpressRoute circuito tooconnect tooyour atrás local. Un departamento único (en este ejemplo: TI) puede poseer el circuito de ExpressRoute Hola. Otras suscripciones dentro de la organización de hello pueden utilizar el circuito de ExpressRoute Hola.

> [!NOTE]
> Cargos de conectividad y ancho de banda de circuito de ExpressRoute de Hola será propietario de la suscripción de toohello aplicado. Todas las redes virtuales compartan Hola mismo ancho de banda.
> 
> 

![Conectividad entre suscripciones](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a>Administración: los propietarios de circuito y los usuarios de circuito

Hola 'propietario del circuito' es un usuario autorizado de alimentación de hello recursos de circuito de ExpressRoute. propietario del circuito Hola puede crear autorizaciones que se pueden canjear por 'usuarios del circuito'. Los usuarios de circuito son propietarios de red virtual puertas de enlace que no están en Hola misma suscripción como Hola circuito de ExpressRoute. Los usuarios del circuito pueden canjear autorizaciones (una autorización por red virtual).

propietario del circuito Hello tiene Hola power toomodify y revocar las autorizaciones en cualquier momento. Revocar el resultado de una autorización en todas las conexiones de vínculo que se va a eliminar de suscripción de hello cuyo acceso se ha revocado.

### <a name="circuit-owner-operations"></a>Operaciones del propietario del circuito

**toocreate una autorización**

propietario del circuito Hola crea una autorización. Esto resulta en hello creación de una clave de autorización que puede ser utilizados por un tooconnect de usuario de circuito su toohello de puertas de enlace de red virtual circuito de ExpressRoute. Una autorización solo es válida para una conexión.

Hola cmdlet fragmento siguiente muestra cómo toocreate una autorización:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


Hola toothis de respuesta contendrá el estado y la clave de autorización de hello:

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



**tooreview autorizaciones**

propietario del circuito Hola puede revisar todas las autorizaciones que se ejecutan en un circuito concreto mediante la ejecución de hello siguiente cmdlet:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

**tooadd autorizaciones**

propietario del circuito Hola puede agregar autorizaciones mediante Hola siguiente cmdlet:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

**toodelete autorizaciones**

propietario del circuito Hola puede revocar o eliminar un autorizaciones toohello usuario ejecutando Hola siguiente cmdlet:

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a>Operaciones del usuario del circuito

usuario de circuito de Hello necesita Id. del mismo nivel de hello y una clave de autorización de propietario del circuito Hola. clave de autorización de Hello es un GUID.

Identificador del mismo nivel se puede comprobar de hello siguiente comando:

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

**tooredeem una autorización de conexión**

usuario de circuito de Hello puede ejecutar Hola siguiente cmdlet tooredeem una autorización de vínculo:

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

**toorelease una autorización de conexión**

Puede liberar una autorización mediante la eliminación de la conexión de Hola que vincula la red virtual del toohello de circuito ExpressRoute Hola.

## <a name="modify-a-virtual-network-connection"></a>Modificación de una conexión de red virtual
Puede actualizar ciertas propiedades de una conexión de red virtual. 

**peso de conexión de hello tooupdate**

La red virtual puede ser circuitos ExpressRoute de toomultiple conectado. Puede recibir Hola mismo prefijo de más de un circuito de ExpressRoute. toochoose qué tráfico de toosend conexión destinados a este prefijo, puede cambiar *RoutingWeight* de una conexión. El tráfico se enviará en conexión Hola con hello mayor *RoutingWeight*.

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

Hola intervalo de *RoutingWeight* es too32000 0. valor predeterminado de Hello es 0.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre ExpressRoute, consulte hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).
