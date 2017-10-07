---
title: "configuración de puerta de enlace de aaaVPN para las conexiones de Azure entre entornos | Documentos de Microsoft"
description: "Obtenga información sobre la configuración de VPN Gateway para las puertas de enlace de red virtual de Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: ae665bc5-0089-45d0-a0d5-bc0ab4e79899
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: cherylmc
ms.openlocfilehash: 01229d99fa37e30e00aa00f939f488d631b5593c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a>Acerca de la configuración de la puerta de enlace de VPN

Una puerta de enlace de VPN es un tipo de puerta de enlace de red virtual que envía tráfico cifrado entre la red virtual y la ubicación local a través de una conexión pública. También puede utilizar un tráfico de toosend de puerta de enlace VPN entre redes virtuales en hello red troncal de Azure.

Una conexión de puerta de enlace VPN se basa en la configuración de Hola de varios recursos, cada uno de los cuales contiene valores configurables. secciones de Hello en este artículo describen los recursos de Hola y opciones relacionadas con la puerta de enlace VPN de tooa para una red virtual que creó en el modelo de implementación del Administrador de recursos. Puede encontrar descripciones y diagramas de topología para cada solución de conexión en hello [acerca de la puerta de enlace VPN](vpn-gateway-about-vpngateways.md) artículo.

## <a name="gwtype"></a>Tipos de puerta de enlace

Cada red virtual solo puede tener una puerta de enlace de red de cada tipo. Cuando se crea una puerta de enlace de red virtual, debe asegurarse de que es correcto para la configuración del tipo de puerta de enlace de Hola.

Hola valores disponibles para el GatewayType - son:

* VPN
* ExpressRoute

Una puerta de enlace VPN requiere hello `-GatewayType` *Vpn*.

Ejemplo:

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <a name="gwsku"></a>SKU de puerta de enlace

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-hello-gateway-sku"></a>Configurar la puerta de enlace de hello SKU

#### <a name="azure-portal"></a>Azure Portal

Si usas hello toocreate portal Azure una puerta de enlace de red virtual del Administrador de recursos, puede seleccionar SKU de puerta de enlace de hello mediante el uso de la lista desplegable de Hola. Opciones de Hola con que se presentan corresponden toohello tipo de puerta de enlace y el tipo VPN que seleccione.

#### <a name="powershell"></a>PowerShell

el ejemplo siguiente se PowerShell Hello especifica hello `-GatewaySku` como VpnGw1.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <a name="resize"></a>Cambio de tamaño de una SKU de puerta de enlace

Si desea que tooupgrade su tooa SKU de puerta de enlace SKU más eficaz, puede usar hello `Resize-AzureRmVirtualNetworkGateway` cmdlet de PowerShell. También puede cambiar el tamaño de la SKU de puerta de enlace Hola con este cmdlet.

Hola PowerShell ejemplo siguiente se muestra que un SKU de puerta de enlace se cambia el tamaño tooVpnGw2.

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <a name="connectiontype"></a>Tipos de conexión

En el modelo de implementación del Administrador de recursos de hello, cada configuración requiere un tipo de conexión de puerta de enlace de red virtual específica. Hello PowerShell Administrador de recursos disponibles los valores de `-ConnectionType` son:

* IPsec
* Vnet2Vnet
* ExpressRoute
* VPNClient

En el siguiente ejemplo de PowerShell de hello, creamos una conexión de S2S que requiere el tipo de conexión de hello *IPsec*.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <a name="vpntype"></a>Tipos de VPN

Cuando se crea la puerta de enlace de red virtual de Hola para una configuración de puerta de enlace VPN, debe especificar un tipo VPN. Hola tipo VPN que elija depende de topología de conexión de Hola que desea toocreate. Por ejemplo, una conexión de P2S requiere un tipo de VPN RouteBased. Un tipo VPN también puede depender de hardware de Hola que está usando. Las configuraciones de S2S requieren un dispositivo VPN. Algunos dispositivos VPN solo serán compatibles con un determinado tipo de VPN.

Hola seleccione el tipo de VPN debe cumplir todos los requisitos de conexión de hello para la solución de hello que desea toocreate. Por ejemplo, si desea que toocreate una conexión de puerta de enlace de VPN de S2S y una conexión de puerta de enlace de VPN de P2S para Hola misma red virtual, se utilizaría el tipo de VPN *RouteBased* porque P2S requiere un tipo RouteBased VPN. También necesitaría tooverify que el dispositivo VPN admite una conexión VPN RouteBased. 

Una vez creada una puerta de enlace de red virtual, no se puede cambiar el tipo de VPN de Hola. Tener toodelete Hola puerta de enlace de red virtual y cree uno nuevo. Hay dos tipos de VPN:

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

el ejemplo siguiente se PowerShell Hello especifica hello `-VpnType` como *RouteBased*. Cuando se crea una puerta de enlace, debe asegurarse de que ese hello - VpnType es correcto para su configuración.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <a name="requirements"></a>Requisitos de la puerta de enlace

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <a name="gwsub"></a>Subred de puerta de enlace

Antes de crear una puerta de enlace de VPN, debe crear una subred de puerta de enlace. subred de puerta de enlace de Hello contiene direcciones IP de hello esa puerta de enlace de red virtual de hello las máquinas virtuales y servicios de uso. Al crear la puerta de enlace de red virtual, puerta de enlace de máquinas virtuales son subred de puerta de enlace de toohello implementado y configurado con la configuración de puerta de enlace VPN de hello necesario. Nunca debe implementar la subred de puerta de enlace de toohello nada (por ejemplo, máquinas virtuales adicionales). subred de puerta de enlace de Hello debe denominarse "GatewaySubnet" toowork correctamente. Nombres de subred de puerta de enlace de hello permite "GatewaySubnet" Azure sabe que esto es el enlace de red virtual Hola de subred toodeploy hello las máquinas virtuales y servicios a.

Cuando se crea la subred de puerta de enlace de hello, especifica Hola número de direcciones IP que Hola subred contiene. direcciones IP de Hello en la subred de puerta de enlace de hello son la puerta de enlace de toohello asignado las máquinas virtuales y servicios de puerta de enlace. Algunas configuraciones requieren más direcciones IP que otras. Buscar en las instrucciones de hello para la configuración de Hola que desee toocreate y comprobar esa subred de puerta de enlace de hello desea toocreate cumple estos requisitos. Además, puede que desee toomake seguro de que la subred de puerta de enlace contiene suficientes IP direcciones tooaccommodate posibles futuras configuraciones adicionales. Aunque es posible crear una subred de puerta de enlace tan pequeña como /29, se recomienda que sea /28 o mayor (/28, /27, /26, etc.). De este modo, si agrega funcionalidad de hello futura, no tienen tootear la puerta de enlace, a continuación, elimine y vuelva a hello tooallow de subred de puerta de enlace de más direcciones IP.

Hello siguiente ejemplo de PowerShell del Administrador de recursos muestra una subred de puerta de enlace con el nombre GatewaySubnet. Puede ver la notación CIDR Hola especifica un /27, que permite suficientes direcciones IP para la mayoría de las configuraciones que existen actualmente.

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <a name="lng"></a>Puertas de enlace de red local

Al crear una configuración de puerta de enlace VPN, puerta de enlace de red local de hello suele representa la ubicación local. En el modelo de implementación clásica de hello, puerta de enlace de red local de Hola era tooas que se hace referencia un sitio Local. 

Asigne un nombre de puerta de enlace de red local de hello, Hola dirección IP pública del dispositivo VPN de hello local y especificar los prefijos de dirección de Hola que se encuentran en la ubicación local de Hola. Azure examina prefijos de dirección de destino de hello para el tráfico de red, consulta la configuración de Hola que ha especificado para la puerta de enlace de red local y enruta paquetes según corresponda. También debe especificar puertas de enlace de red local para configuraciones de red virtual a red virtual local que usan una conexión de puerta de enlace de VPN.

Hola PowerShell ejemplo siguiente crea una nueva puerta de enlace de red local:

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

En ciertas ocasiones necesitará configuración de puerta de enlace de red local toomodify Hola. Por ejemplo, al agregar o modificar el intervalo de direcciones de hello, si Hola cambio o dirección IP del dispositivo VPN de Hola. Para una red virtual clásica, puede cambiar esta configuración en el portal clásico de hello en la página redes locales de Hola. Para Resource Manager, consulte [Modificación de la configuración de la puerta de enlace de red local mediante PowerShell](vpn-gateway-modify-local-network-gateway.md)

## <a name="resources"></a>API de REST y cmdlets de PowerShell

Para recursos técnicos adicionales y requisitos de sintaxis específica cuando se usa la API de REST, cmdlets de PowerShell o CLI de Azure para las configuraciones de puerta de enlace de VPN, vea Hola siguientes páginas:

| **Clásico** | **Resource Manager** |
| --- | --- |
| [PowerShell](/powershell/module/azure#networking) |[PowerShell](/powershell/module/azurerm.network#vpn) |
| [API DE REST](https://msdn.microsoft.com/library/jj154113) |[API de REST](/rest/api/network/virtualnetworkgateways) |
| No compatible | [CLI de Azure](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre las configuraciones de conexión disponibles, vea [About VPN Gateway (Acerca de VPN Gateway)](vpn-gateway-about-vpngateways.md).