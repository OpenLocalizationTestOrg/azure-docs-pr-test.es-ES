---
title: 'Vincular un circuito de ExpressRoute de tooan de red virtual: CLI: Azure | Documentos de Microsoft'
description: "Este documento proporciona información general sobre cómo toolink virtual redes (redes virtuales) tooExpressRoute circuitos utilizando el modelo de implementación del Administrador de recursos de Hola y la CLI."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlit
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 1251f016d9b94d3fee81de1df164cb085cbe9d78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-cli"></a>Conectarse a un circuito de ExpressRoute de tooan de red virtual con CLI

En este artículo le ayuda a vincular circuitos de ExpressRoute de tooAzure de redes virtuales (Vnet) mediante la CLI. toolink mediante CLI de Azure, se deben crear redes virtuales de hello mediante modelo de implementación del Administrador de recursos de Hola. O bien pueden estar en hello misma suscripción o parte de otra suscripción. Si desea toouse tooconnect de un método diferente para el circuito de ExpressRoute de tooan de red virtual, puede seleccionar un artículo de hello lista siguiente:

> [!div class="op_single_selector"]
> * [Portal de Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [CLI de Azure](howto-linkvnet-cli.md)
> * [Vídeo: Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (clásico)](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a>Requisitos previos de configuración

* Necesita la versión más reciente de Hola de hello interfaz de línea de comandos (CLI). Para más información, consulte [Instalación de la CLI de Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).
* Necesita hello tooreview [requisitos previos](expressroute-prerequisites.md), [requisitos de enrutamiento](expressroute-routing.md), y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.
* Tiene que tener un circuito ExpressRoute activo. 
  * Siga las instrucciones de hello demasiado[crear un circuito ExpressRoute](howto-circuit-cli.md) y tener habilitada por el proveedor de conectividad de circuito de Hola. 
  * Asegúrese de que dispone de un emparejamiento privado de Azure configurado para el circuito. Vea hello [configurar el enrutamiento de](howto-routing-cli.md) artículo para las instrucciones de enrutamiento. 
  * Asegúrese de que se haya configurado un emparejamiento privado de Azure. emparejamiento de BGP de Hello entre la red y Microsoft debe ser una para que se puede habilitar la conectividad de extremo a extremo.
  * Asegúrese de que ha creado y aprovisionado totalmente una red virtual y una puerta de enlace de red virtual. Siga las instrucciones de hello demasiado[configurar una puerta de enlace de red virtual para ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli). Ser seguro toouse `--gateway-type ExpressRoute`.

* Puede vincular una circuito de ExpressRoute estándar de too10 redes virtuales tooa. Todas las redes virtuales deben estar en hello misma región geopolíticos cuando se usa un circuito de ExpressRoute estándar. 

* Si habilita el complemento de hello ExpressRoute premium, puede vincular una red virtual fuera de la región geopolítica de Hola de hello circuito de ExpressRoute o conectar un mayor número de redes virtuales tooyour circuito de ExpressRoute. Para obtener más información sobre el complemento de hello premium, vea hello [preguntas más frecuentes sobre](expressroute-faqs.md).

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Conectar una red virtual en hello mismo circuito de tooa de suscripción

Puede conectar un circuito de ExpressRoute de tooan de puerta de enlace de red virtual mediante el ejemplo de Hola. Asegúrese de que esa puerta de enlace de red virtual de Hola se crea y está listo para crear un vínculo antes de ejecutar el comando de Hola.

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Conectar una red virtual en un circuito de tooa otra suscripción

Puede compartir un circuito ExpressRoute entre varias suscripciones. Hola siguiente ilustración muestra un sencillo esquemática de cómo compartir funciona para los circuitos ExpressRoute en varias suscripciones.

Cada una de las nubes más pequeñas de hello en nube de gran tamaño hello es toorepresent usado suscripciones que pertenecen los departamentos de toodifferent dentro de una organización. Cada uno de los departamentos de Hola de organización de hello puede utilizar su propia suscripción para implementar sus servicios, pero se puede compartir una sola red de ExpressRoute circuito tooconnect tooyour atrás local. Un departamento único (en este ejemplo: TI) puede poseer el circuito de ExpressRoute Hola. Otras suscripciones dentro de la organización de hello pueden utilizar el circuito de ExpressRoute Hola.

> [!NOTE]
> Los cargos de conectividad y ancho de banda para el circuito dedicado de hello será aplicado toohello propietario del circuito de ExpressRoute. Todas las redes virtuales compartan Hola mismo ancho de banda.
> 
> 

![Conectividad entre suscripciones](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a>Administración: los propietarios del circuito y los usuarios del circuito

Hola 'Propietario del circuito' es un usuario autorizado de alimentación de hello recursos de circuito de ExpressRoute. Hola propietario del circuito puede crear autorizaciones que se pueden canjear por 'Usuarios del circuito'. Los usuarios de circuito son propietarios de red virtual puertas de enlace que no están en Hola misma suscripción como Hola circuito de ExpressRoute. Los usuarios del circuito pueden canjear autorizaciones (una autorización por red virtual).

Hola propietario del circuito tiene Hola power toomodify y revocar las autorizaciones en cualquier momento. Cuando se revoca una autorización, se eliminan todas las conexiones de vínculo de suscripción de hello cuyo acceso se ha revocado.

### <a name="circuit-owner-operations"></a>Operaciones del propietario del circuito

**toocreate una autorización**

Hola propietario del circuito crea una autorización, que crea una clave de autorización que puede ser utilizado por un usuario de circuito tooconnect su toohello de puertas de enlace de red virtual circuito de ExpressRoute. Una autorización solo es válida para una conexión.

Hola siguiente ejemplo se muestra cómo toocreate una autorización:

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

respuesta de Hello contiene el estado y clave de autorización de hello:

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

**tooreview autorizaciones**

Hola propietario del circuito puede revisar todas las autorizaciones que se emiten en un circuito concreto mediante la ejecución de hello siguiente ejemplo:

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

**tooadd autorizaciones**

Hola propietario del circuito puede agregar autorizaciones mediante el siguiente ejemplo de Hola:

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

**toodelete autorizaciones**

Hola propietario del circuito puede revocar o eliminar un autorizaciones toohello usuario ejecutando el siguiente ejemplo de Hola:

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a>Operaciones del usuario del circuito

Hola circuito usuario necesita Id. del mismo nivel de hello y una clave de autorización de propietario del circuito de Hola. clave de autorización de Hello es un GUID.

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

**tooredeem una autorización de conexión**

Hola usuario del circuito puede ejecutar después de tooredeem de ejemplo de Hola una autorización de vínculo:

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

**toorelease una autorización de conexión**

Puede liberar una autorización mediante la eliminación de la conexión de Hola que vincula la red virtual del toohello de circuito ExpressRoute Hola.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre ExpressRoute, consulte hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).
