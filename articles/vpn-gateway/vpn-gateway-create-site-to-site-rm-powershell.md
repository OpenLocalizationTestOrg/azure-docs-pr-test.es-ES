---
title: 'Conectar su tooan de red local red virtual de Azure: VPN de sitio a sitio: PowerShell | Documentos de Microsoft'
description: "Una conexión de IPsec desde el entorno local de red tooan red virtual de Azure a través de toocreate de pasos Hola Internet pública. Estos pasos le ayudarán a crear una conexión de VPN Gateway de sitio a sitio entre locales mediante PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a>Creación de una red virtual con una conexión VPN de sitio a sitio mediante PowerShell

Este artículo muestra cómo toouse conexión de puerta de enlace VPN de PowerShell toocreate un sitio a sitio desde el entorno local de red toohello red virtual. pasos de Hello en este artículo aplican toohello modelo de implementación de administrador de recursos. También puede crear esta configuración con una herramienta de implementación diferentes o un modelo de implementación seleccionando una opción diferente de hello lista siguiente:

> [!div class="op_single_selector"]
> * [Portal de Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portal de Azure clásico](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [Portal clásico (clásico)](vpn-gateway-site-to-site-create.md)
> 
>


Una conexión de puerta de enlace VPN de sitio a sitio es tooconnect utilizado en sus instalaciones de red tooan red virtual de Azure a través de un túnel VPN de IPsec/IKE (IKEv1 o IKEv2). Este tipo de conexión requiere una VPN dispositivo situado en local que tiene un tooit de dirección asignada de IP pública con orientación externa. Para más información acerca de las puertas de enlace VPN, consulte [Acerca de VPN Gateway](vpn-gateway-about-vpngateways.md).

![Diagrama de la conexión entre locales de VPN Gateway de sitio a sitio](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <a name="before"></a>Antes de empezar

Compruebe que se ha cumplido hello siguiendo criterios antes de comenzar la configuración:

* Asegúrese de que tiene un dispositivo VPN compatible y alguna persona tooconfigure capaz de él. Para más información acerca de los dispositivos VPN compatibles y su configuración, consulte [Acerca de los dispositivos VPN](vpn-gateway-about-vpn-devices.md).
* Compruebe que tiene una dirección IPv4 pública externa para el dispositivo VPN. Esta dirección IP no puede estar detrás de un NAT.
* Si no está familiarizado con intervalos de direcciones IP de hello ubicados en configuración de red local, deberá toocoordinate con alguien que pueda proporcionarle estos detalles para usted. Al crear esta configuración, debe especificar prefijos para intervalo de direcciones IP con hello que Azure enrutará la ubicación de tooyour local. Ninguna de las subredes de saludo de la red local puede enumerar sobre el regazo con subredes de red virtual de Hola que desee tooconnect a.
* Instalar versión más reciente de Hola de hello cmdlets de PowerShell del Administrador de recursos de Azure. Cmdlets de PowerShell se actualizan con frecuencia y, normalmente deberá tooupdate su funcionalidad característica más reciente de Hola de PowerShell cmdlets tooget. Si no actualiza los cmdlets de PowerShell, pueden producir un error en los valores de hello especificados. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener más información sobre cómo descargar e instalar los cmdlets de PowerShell.

### <a name="example"></a>Valores del ejemplo

ejemplos de Hello en este artículo utiliza Hola después de valores. Puede usar estos toocreate valores un entorno de prueba, o consulte toothem toobetter comprender los ejemplos de hello en este artículo.

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <a name="Login"></a>1. Conectar tooyour suscripción

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="VNet"></a>2. Creación de una red virtual y una puerta de enlace

Si no tiene una red virtual, créela. Al crear una red virtual, asegúrese de que los espacios de direcciones de hello especificados no superponen con cualquiera de los espacios de direcciones de Hola que existen en la red local.

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="vnet"></a>toocreate una red virtual y una subred de puerta de enlace

Este ejemplo crea una red virtual y una subred de la puerta de enlace. Si ya tiene una red virtual que necesita una subred de puerta de enlace para ver tooadd [tooadd una puerta de enlace subred tooa red virtual que ya ha creado](#gatewaysubnet).

Cree un grupo de recursos:

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

Cree la red virtual.

1. Establecer variables de Hola.

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. Crear red virtual de Hola.

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <a name="gatewaysubnet"></a>una red virtual de puerta de enlace subred tooa tooadd ya ha creado

1. Establecer variables de Hola.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. Crear una subred de puerta de enlace de Hola.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. Establecer configuración de Hola.

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## 3. <a name="localnet"></a>Crear puerta de enlace de red local de Hola

puerta de enlace de red local de Hello suele hacer referencia a ubicación de tooyour local. Se asigne un nombre mediante el cual Azure puede consulte tooit y luego especifique la dirección IP de Hola a sitio Hola de hello local VPN dispositivo toowhich creará una conexión. También especificar prefijos de direcciones IP de Hola que se enrutará a través del dispositivo VPN de toohello de puerta de enlace VPN de Hola. Especifique los prefijos de direcciones Hola son prefijos de hello ubicados en la red local. Si cambia su red local, puede actualizar fácilmente los prefijos de Hola.

Usar hello siguientes valores:

* Hola *GatewayIPAddress* es la dirección IP de hello de dispositivo VPN local. El dispositivo VPN no se encuentra detrás de un NAT.
* Hola *AddressPrefix* es local de espacio de direcciones.

tooadd una puerta de enlace de red local con un prefijo de dirección única:

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

tooadd una puerta de enlace de red local con varios prefijos de direcciones:

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

toomodify prefijos de direcciones IP para la puerta de enlace de red local:<br>
A veces los prefijos de la puerta de enlace de red local cambian. Hola pasos seguir toomodify su dirección IP prefijos dependen de si ha creado una conexión de puerta de enlace VPN. Vea hello [prefijos de direcciones IP de modificar una puerta de enlace de red local](#modify) sección de este artículo.

## <a name="PublicIP"></a>4. Solicite una dirección IP pública

Una puerta de enlace VPN debe tener una dirección IP pública. Solicitar el recurso de dirección IP hello y, a continuación, hacer referencia tooit al crear la puerta de enlace de red virtual. dirección IP de Hola se asigna dinámicamente toohello recursos cuando se crea la puerta de enlace VPN de Hola. Actualmente, VPN Gateway solo admite la asignación de direcciones IP públicas *dinámicas*. No se puede solicitar una asignación de direcciones IP públicas estáticas. Sin embargo, esto no significa que se cambia la dirección IP de hello después de que se le ha asignado tooyour puerta de enlace VPN. cambios en la dirección IP pública hello cuando se Hola puerta de enlace de única vez de Hola se elimina y vuelve a crear. No cambia cuando se cambia el tamaño, se restablece o se realizan actualizaciones u otras operaciones de mantenimiento interno de una puerta de enlace VPN.

Solicitar una dirección IP pública que se va a asignar la red virtual de tooyour puerta de enlace VPN.

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <a name="GatewayIPConfig"></a>5. Crear configuración de direcciones IP de puerta de enlace de Hola

configuración de puerta de enlace de Hello define la subred de Hola y Hola toouse de dirección IP pública. Usar hello siguiendo el ejemplo toocreate la configuración de puerta de enlace:

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <a name="CreateGateway"></a>6. Crear puerta de enlace VPN de Hola

Crear puerta de enlace VPN de red virtual de Hola. Crear una puerta de enlace VPN puede tardar hasta too45 minutos o más toocomplete.

Usar hello siguientes valores:

* Hola *- el GatewayType* para un sitio a sitio es configuración *Vpn*. tipo de puerta de enlace de Hello siempre es configuración toohello específico que va a implementar. Por ejemplo, otras configuraciones de puerta de enlace pueden requerir GatewayType ExpressRoute.
* Hola *- VpnType* puede ser *RouteBased* (llamada tooas una puerta de enlace dinámico en algunos documentos), o *PolicyBased* (denominada tooas una puerta de enlace estática en algunos documentos ). Para más información sobre los tipos de Puertas de enlace de VPN, consulte [Información acerca de VPN Gateway](vpn-gateway-about-vpngateways.md).
* Seleccione Hola SKU de puerta de enlace que desea toouse. Hay limitaciones de configuración para determinadas SKU. Consulte [SKU de puertas de enlace](vpn-gateway-about-vpn-gateway-settings.md#gwsku) para más información. Si se produce un error al crear la puerta de enlace VPN de hello sobre hello - GatewaySku, compruebe que ha instalado la versión más reciente de Hola Hola de cmdlets de PowerShell.

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <a name="ConfigureVPNDevice"></a>7. Configurar el dispositivo VPN

Red local de las conexiones de sitio a sitio tooan requieren un dispositivo VPN. En este paso, se configura el dispositivo VPN. Al configurar el dispositivo VPN, necesita Hola siguiente:

- Una clave compartida. Esto es Hola mismo compartido clave que se especifique al crear la conexión VPN de sitio a sitio. En estos ejemplos se utiliza una clave compartida básica. Se recomienda que generar un toouse clave más compleja.
- Hola dirección IP pública de la puerta de enlace de red virtual. Puede ver la dirección IP pública hello mediante Hola portal de Azure, PowerShell o CLI. Hola toofind dirección IP pública de la puerta de enlace de red virtual con PowerShell, el siguiente ejemplo de Hola de uso:

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>8. Crear la conexión de VPN de Hola

A continuación, cree la conexión de VPN de sitio a sitio de hello entre la puerta de enlace de red virtual y el dispositivo VPN. Ser seguro tooreplace Hola valores por los suyos propios. clave compartida de Hello debe coincidir con valor de Hola que utilizó para la configuración del dispositivo VPN. Tenga en cuenta que hello '-ConnectionType' para el sitio a sitio es *IPsec*.

1. Establecer variables de Hola.
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. Crear conexiones de Hola.
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

Después de un valor bajo al Hola se establecerá la conexión.

## <a name="toverify"></a>9. Compruebe la conexión de VPN de Hola

Hay unos tooverify de maneras diferentes de la conexión VPN.

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="connectVM"></a>máquina virtual de tooconnect tooa

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <a name="modify"></a>Modificación de los prefijos las direcciones IP de una puerta de enlace de red local

Si cambian los prefijos de direcciones IP de Hola que desee enrutar tooyour ubicación, puede modificar la puerta de enlace de red local de Hola. Se proporcionan dos conjuntos de instrucciones: instrucciones de Hola que elija dependen de si ya ha creado la conexión de puerta de enlace.

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="modifygwipaddress"></a>Modificar la dirección IP de puerta de enlace de hello una puerta de enlace de red local

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>Pasos siguientes

*  Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour. Consulte [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) para más información.
* Para obtener información sobre BGP, consulte hello [información general de BGP](vpn-gateway-bgp-overview.md) y [cómo tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
