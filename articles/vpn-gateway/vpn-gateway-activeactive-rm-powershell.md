---
title: "Configuración de conexiones VPN S2S activo-activo para VPN Gateway: Azure Resource Manager: PowerShell | Microsoft Docs"
description: "Este artículo le guiará a la hora de configurar conexiones activo-activo con Azure VPN Gateway usando Azure Resource Manager y PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: yushwang
ms.openlocfilehash: 964eedc7698e42bf0e082f0105845f2a339daf57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a>Configuración de conexiones VPN S2S activo-activo con Azure VPN Gateway

Este artículo le guiará a través de hello pasos toocreate activo-activo entre-local y las conexiones de red virtual a red virtual con el modelo de implementación del Administrador de recursos de Hola y PowerShell.

## <a name="about-highly-available-cross-premises-connections"></a>Acerca de las conexiones entre entornos locales de alta disponibilidad
tooachieve alta disponibilidad para entre entornos y la conectividad de red virtual a red virtual, debe implementar varias puertas de enlace VPN y establecer varias conexiones en paralelo entre las redes y Azure. Consulte [Conectividad de alta disponibilidad entre locales y de red virtual a red virtual](vpn-gateway-highlyavailable.md) para información general de las opciones de conectividad y la topología.

Este artículo proporciona instrucciones de hello tooset seguridad un activo / activo entre entornos conexión VPN y activo / activo conexión entre dos redes virtuales:

* [Parte 1: Creación y configuración de Azure VPN Gateway en el modo activo-activo](#aagateway)
* [Parte 2: Establecimiento de conexiones activo-activo entre entornos locales](#aacrossprem)
* [Parte 3: Establecimiento de conexiones activo-activo de red virtual a red virtual](#aav2v)
* [Parte 4: Actualización de una puerta de enlace existente entre activo-activo y activo-en espera](#aaupdate)

Puede combinar estos toobuild conjuntamente una topología de red más compleja, de alta disponibilidad que satisfaga sus necesidades.

> [!IMPORTANT]
> Tenga en cuenta que el modo activo / activo de hello usa Hola solo después de SKU: 
  * VpnGw1, VpnGw2, VpnGw3
  * Alto rendimiento (para SKU heredadas anteriores)
> 
> 

## <a name ="aagateway"></a>Parte 1: Creación y configuración de puertas de enlace VPN activo-activo
Hola pasos configurará la puerta de enlace de VPN de Azure en los modos activo / activo. Hola las diferencias principales entre puertas de enlace de hello activo / activo y reserva activa:

* Necesita dos configuraciones de IP de puerta de enlace toocreate con dos direcciones IP públicas
* Necesita establecer hello EnableActiveActiveFeature marca
* puerta de enlace de Hello SKU debe ser VpnGw1, VpnGw2, VpnGw3 o alto rendimiento (SKU heredado).

Hello otras propiedades son Hola igual que las puertas de enlace de hello no activo / activo. 

### <a name="before-you-begin"></a>Antes de empezar
* Compruebe que tiene una suscripción a Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Necesitará tooinstall hello Azure Resource Manager cmdlets de PowerShell. Vea [información general de Azure PowerShell](/powershell/azure/overview) para obtener más información acerca de cómo instalar los cmdlets de PowerShell de Hola.

### <a name="step-1---create-and-configure-vnet1"></a>Paso 1: Creación y configuración de VNet1
#### <a name="1-declare-your-variables"></a>1. Declaración de las variables
Para este ejercicio, comenzaremos declarando las variables. ejemplo de Hola siguiente declara las variables de hello con valores de hello para este ejercicio. Ser seguro de valores de hello tooreplace con su propio cuando se configura para la producción. Puede utilizar estas variables si está ejecutando a través de hello pasos toobecome familiarizado con este tipo de configuración. Modificar variables de hello y, a continuación, copie y pegue en la consola de PowerShell.

```powershell
$Sub1 = "Ross"
$RG1 = "TestAARG1"
$Location1 = "West US"
$VNetName1 = "TestVNet1"
$FESubName1 = "FrontEnd"
$BESubName1 = "Backend"
$GWSubName1 = "GatewaySubnet"
$VNetPrefix11 = "10.11.0.0/16"
$VNetPrefix12 = "10.12.0.0/16"
$FESubPrefix1 = "10.11.0.0/24"
$BESubPrefix1 = "10.12.0.0/24"
$GWSubPrefix1 = "10.12.255.0/27"
$VNet1ASN = 65010
$DNS1 = "8.8.8.8"
$GWName1 = "VNet1GW"
$GW1IPName1 = "VNet1GWIP1"
$GW1IPName2 = "VNet1GWIP2"
$GW1IPconf1 = "gw1ipconf1"
$GW1IPconf2 = "gw1ipconf2"
$Connection12 = "VNet1toVNet2"
$Connection151 = "VNet1toSite5_1"
$Connection152 = "VNet1toSite5_2"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Conectar tooyour suscripción y crear un nuevo grupo de recursos
Asegúrese de que cambie hello toouse de modo tooPowerShell cmdlets del Administrador de recursos. Para obtener más información, consulte [Uso de Windows PowerShell con el Administrador de recursos](../powershell-azure-resource-manager.md).

Abra la consola de PowerShell y conectar con tooyour cuenta. Usar hello después toohelp de ejemplo que conectarse:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. Creación de TestVNet1
ejemplo de Hola siguiente crea una red virtual denominada TestVNet1 y tres subredes, un GatewaySubnet llamado, uno llamado front-end y un back-end de llamada. Al reemplazar valores, es importante que siempre asigne el nombre GatewaySubnet a la subred de la puerta de enlace. Si usa otro, se producirá un error al crear la puerta de enlace.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a>Paso 2: crear la puerta de enlace VPN de Hola para TestVNet1 con el modo activo / activo
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a>1. Crear direcciones IP públicas de Hola y configuraciones de IP de puerta de enlace
Solicitud dos pública direcciones toobe toohello asignado puerta de enlace IP que creará para la red virtual. También definirá subred hello y las configuraciones de IP necesarias.

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a>2. Creación de puerta de enlace VPN de hello con una configuración activo / activo
Crear puerta de enlace de red virtual de Hola para TestVNet1. Tenga en cuenta que hay dos entradas de GatewayIpConfig y hello EnableActiveActiveFeature marca está establecida. Crear una puerta de enlace puede tardar un rato (45 minutos o más toocomplete).

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a>3. Obtener direcciones IP públicas de hello puerta de enlace y dirección IP del mismo nivel de BGP de Hola
Una vez creada la puerta de enlace de hello, necesitará tooobtain Hola BGP del mismo nivel IPAddress en hello puerta de enlace de VPN de Azure. Esta dirección es necesario tooconfigure Hola puerta de enlace de VPN de Azure como un par BGP para los dispositivos VPN local.

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

Usar hello después cmdlets tooshow Hola dos direcciones IP públicas asignadas a la puerta de enlace VPN y sus direcciones IP de BGP del mismo nivel correspondientes para cada instancia de puerta de enlace:

```powershell

    PS D:\> $gw1pip1.IpAddress
    40.112.190.5

    PS D:\> $gw1pip2.IpAddress
    138.91.156.129

    PS D:\> $vnet1gw.BgpSettingsText
    {
      "Asn": 65010,
      "BgpPeeringAddress": "10.12.255.4,10.12.255.5",
      "PeerWeight": 0
    }
```

orden de Hola de direcciones IP públicas de Hola para instancias de puerta de enlace de Hola y Hola direcciones de emparejamiento de BGP correspondientes son Hola igual. En este ejemplo, la puerta de enlace de hello VM con la dirección IP pública de 40.112.190.5 utilizará 10.12.255.4 como su dirección de emparejamiento de BGP y puerta de enlace de hello con 138.91.156.129 utilizará 10.12.255.5. Esta información es necesaria cuando configura su local de dispositivos VPN que se conectan puerta de enlace de toohello activo / activo. puerta de enlace de Hola se muestra en el diagrama de Hola a continuación con todas las direcciones:

![puerta de enlace activo-activo](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

Una vez creada la puerta de enlace de hello, puede usar esta puerta de enlace tooestablish activo-activo entre entornos o conexión de red virtual a red virtual. Hola siguientes secciones le guiará a través de hello pasos toocomplete Hola ejercicio.

## <a name ="aacrossprem"></a>Parte 2: Establecimiento de una conexión activo-activo entre entornos locales
tooestablish una conexión entre entornos, necesita una puerta de enlace de red Local toorepresent toocreate dispositivo VPN local y una puerta de enlace de conexión tooconnect Hola VPN de Azure con puerta de enlace de red local de Hola. En este ejemplo, puerta de enlace de VPN de Azure de hello está en modo activo / activo. Como resultado, incluso si hay solo uno local dispositivo VPN (puerta de enlace de red local) y recursos de una conexión, ambas instancias de puerta de enlace de VPN de Azure establecerán túneles VPN S2S con dispositivo de hello en local.

Antes de continuar, asegúrese de que ha completado la [parte 1](#aagateway) de este ejercicio.

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>Paso 1: crear y configurar la puerta de enlace de red local de Hola
#### <a name="1-declare-your-variables"></a>1. Declaración de las variables
Este ejercicio seguirá toobuild configuración de Hola que se muestra en el diagrama de Hola. Ser seguro tooreplace valores de hello con hello las que desea que toouse para la configuración.

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

Un par de cosas toonote con respecto a los parámetros de puerta de enlace de red local de hello:

* puerta de enlace de red local de Hello puede estar en Hola iguales o diferentes y ubicación de recurso de grupo como Hola puerta de enlace VPN. Este ejemplo muestra en ellos en distintos grupos de recursos, pero en hello misma ubicación de Azure.
* Si hay un único dispositivo VPN local tal y como se muestra arriba, conexión de hello activo / activo puede trabajar con o sin el protocolo BGP. Este ejemplo utiliza para la conexión entre entornos de hello BGP.
* Si se habilita BGP, prefijo Hola necesita toodeclare para puerta de enlace de red local de hello es la dirección de host de Hola de su dirección IP de BGP del mismo nivel en el dispositivo VPN. En este caso, es un prefijo /32 de "10.52.255.253/32".
* Como recordatorio, debe usar diferentes ASN de BGP entre las redes locales y la red virtual de Azure. Si se hello mismo, deberá toochange el ASN VNet si el dispositivo VPN local ya utiliza Hola ASN toopeer con otros vecinos BGP.

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2. Crear puerta de enlace de red local de Hola para Site5
Antes de continuar, asegúrese de que está conectado aún tooSubscription 1. Crear grupo de recursos de hello si no se ha creado.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>Paso 2: conectar la puerta de enlace de red virtual de Hola y puerta de enlace de red local
#### <a name="1-get-hello-two-gateways"></a>1. Obtener Hola dos puertas de enlace

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2. Crear conexiones de hello TestVNet1 tooSite5
En este paso, creará conexión Hola de TestVNet1 tooSite5_1 con "EnableBGP" establecido demasiado$ True.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a>3. Parámetros VPN y BGP para el dispositivo VPN local
ejemplo de Hola siguiente enumera los parámetros de Hola que se especificará en la sección de configuración de BGP de hello en dispositivo VPN local para este ejercicio:

    - ASN de Site5            : 65050
    - IP de BGP Site5: 10.52.255.253
    - Agrega el prefijo tooannounce: (por ejemplo) 10.51.0.0/16 y 10.52.0.0/16
    - ASN de red virtual de Azure: 65010
    - Azure red virtual BGP IP 1: 10.12.255.4 para too40.112.190.5 de túnel
    - Azure red virtual BGP IP 2: 10.12.255.5 para too138.91.156.129 de túnel
    - Rutas estáticas: destino 10.12.255.4/32, nexthop Hola VPN túnel interfaz too40.112.190.5 destino 10.12.255.5/32, nexthop Hola VPN túnel interfaz too138.91.156.129
    - eBGP salto múltiple: asegúrese de opción de "salto múltiple" hello eBGP está habilitada en el dispositivo si es necesario

debe establecerse la conexión de Hello después de unos minutos y sesión Hola BGP del mismo nivel se iniciarán una vez establecida la conexión IPsec Hola. En este ejemplo hasta ahora ha configurado un único dispositivo VPN local, resultante en el diagrama de Hola que se muestra a continuación:

![activo-activo-entre entornos locales](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a>Paso 3: conectar dos local VPN dispositivos toohello activo-activo puerta de enlace VPN
Si tiene dos dispositivos VPN en hello mismo local red, puede lograr redundancia dual por conexión Hola VPN de Azure puerta de enlace toohello segundo dispositivo VPN.

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a>1. Crear puerta de enlace de red local segundo Hola para Site5
Tenga en cuenta que dirección IP de puerta de enlace de hello, prefijo de dirección y dirección de emparejamiento de BGP de puerta de enlace de red local segundo hello no deben solaparse con hello anterior red local puerta de enlace de hello misma red en local.

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a>2. Conectar la puerta de enlace de red virtual de Hola y la segunda la puerta de enlace de red local Hola
Crear la conexión de Hola desde TestVNet1 tooSite5_2 con "EnableBGP" establecido demasiado$ True

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a>3. Los parámetros VPN y BGP para el segundo dispositivo VPN local
De forma similar, siguientes listas de parámetros de Hola entrará en el dispositivo VPN de la segunda hello:

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5
                         Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

Una vez que se han establecido conexión hello (túneles), tendrá dos dispositivos VPN redundancia y túneles que conectan la red local y Azure:

![redundancia-dual-entre entornos locales](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <a name ="aav2v"></a>Parte 3: Establecimiento de una conexión activo-activo de red virtual a red virtual
En esta sección se crea una conexión de red virtual a red virtual activo-activo con BGP. 

Estas instrucciones Hola continuar de los pasos anteriores Hola mencionados anteriormente. Debe completar [parte 1](#aagateway) toocreate TestVNet1 y configurar Hola puerta de enlace de VPN con BGP. 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>Paso 1: crear la puerta de enlace VPN de hello y TestVNet2
Es importante toomake seguro de que el espacio de direcciones IP de Hola de hello nueva red virtual, TestVNet2, no se superponen con ninguno de los intervalos de red virtual.

En este ejemplo, redes virtuales de hello pertenecen toohello misma suscripción. Puede configurar las conexiones de red virtual a red virtual entre distintas suscripciones; Consulte demasiado[configurar una conexión de red virtual a red virtual](vpn-gateway-vnet-vnet-rm-ps.md) toolearn más detalles. Asegúrese de agregar Hola "-EnableBgp $True" al crear Hola conexiones tooenable BGP.

#### <a name="1-declare-your-variables"></a>1. Declaración de las variables
Ser seguro tooreplace valores de hello con hello las que desea que toouse para la configuración.

```powershell
$RG2 = "TestAARG2"
$Location2 = "East US"
$VNetName2 = "TestVNet2"
$FESubName2 = "FrontEnd"
$BESubName2 = "Backend"
$GWSubName2 = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$VNet2ASN = 65020
$DNS2 = "8.8.8.8"
$GWName2 = "VNet2GW"
$GW2IPName1 = "VNet2GWIP1"
$GW2IPconf1 = "gw2ipconf1"
$GW2IPName2 = "VNet2GWIP2"
$GW2IPconf2 = "gw2ipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a>2. Crear TestVNet2 Hola nuevo grupo de recursos

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a>3. Crear puerta de enlace VPN de hello activo / activo para TestVNet2
Solicitud dos pública direcciones toobe toohello asignado puerta de enlace IP que creará para la red virtual. También definirá subred hello y las configuraciones de IP necesarias.

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

Crear puerta de enlace VPN de hello con hello como marca de "EnableActiveActiveFeature" hello y número. Tenga en cuenta que es necesario reemplazar predeterminado Hola ASN en las puertas de enlace de VPN de Azure. Hola ASN para hello conectado las redes virtuales debe ser diferente tooenable BGP y el enrutamiento de tránsito.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a>Paso 2: conectar hello TestVNet1 y TestVNet2 puertas de enlace
En este ejemplo, las puertas de enlace se encuentran en hello misma suscripción. Puede completar este paso en hello misma sesión de PowerShell.

#### <a name="1-get-both-gateways"></a>1. Obtenga ambas puertas de enlace
Asegúrese de que inicie sesión y conectarse tooSubscription 1.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a>2. Cree ambas conexiones
En este paso, creará conexión Hola de TestVNet1 tooTestVNet2 y conexión Hola de TestVNet2 tooTestVNet1.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> Ser seguro tooenable BGP para las conexiones de ambos.
> 
> 

Después de completar estos pasos, se establecerá la conexión de hello en unos minutos y la sesión de emparejamiento de BGP Hola volverá a estar en una vez que se completa la conexión de red virtual a red virtual de hello con redundancia dual:

![activo-activo-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <a name ="aaupdate"></a>Parte 4: Actualización de una puerta de enlace existente entre activo-activo y activo-en espera
Hola última sección describe cómo puede configurar una puerta de enlace de VPN de Azure existente desde el modo de reserva activa tooactive activo, o viceversa.

> [!NOTE]
> Esta sección incluye Hola pasos tooresize una SKU heredada (SKU antigua) de una puerta de enlace VPN ya se ha creado de tooHighPerformance estándar. Estos pasos no actualizan un antiguo tooone heredado de SKU de hello SKU nuevo.
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a>Configurar una puerta de enlace de puerta de enlace de reserva activa tooactive activo
#### <a name="1-gateway-parameters"></a>1. Parámetros de la puerta de enlace
Hola siguiente ejemplo convierte una puerta de enlace de reserva activa en una puerta de enlace de activo / activo. Necesita toocreate otra dirección IP pública y luego agregar una segunda configuración IP de puerta de enlace. A continuación se muestra hello utilizan parámetros:

```powershell
$GWName = "TestVNetAA1GW"
$VNetName = "TestVNetAA1"
$RG = "TestVPNActiveActive01"
$GWIPName2 = "gwpip2"
$GWIPconf2 = "gw1ipconf2"

$vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$location = $gw.Location
```

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a>2. Crear dirección IP pública de Hola, a continuación, agregue la configuración de IP de puerta de enlace segundo Hola

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a>3. Habilitar la puerta de enlace de Hola de modo y actualización de activo / activo
Debe establecer el objeto de puerta de enlace de hello en actualización real de PowerShell tootrigger Hola. Hola SKU de puerta de enlace de red virtual de hello también se puede cambiar tooHighPerformance (cuyo tamaño ha cambiado) desde que se creó anteriormente como estándar.

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

Esta actualización puede tardar 30 minutos de too45.

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a>Configurar una puerta de enlace de tooactive el modo de espera de puerta de enlace de activo / activo
#### <a name="1-gateway-parameters"></a>1. Parámetros de la puerta de enlace
Use Hola mismo parámetros que antes, obtener el nombre de Hola Hola de configuración de IP que desee tooremove.

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a>2. Quitar la configuración de IP de puerta de enlace de Hola y deshabilitar el modo activo / activo Hola
De igual forma, debe establecer objeto de puerta de enlace de hello en actualización real de PowerShell tootrigger Hola.

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

Esta actualización puede tardar hasta too30 demasiado 45 minutos.

## <a name="next-steps"></a>Pasos siguientes
Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour. Consulte [Creación de una máquina virtual que ejecuta Windows en el Portal de Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para ver los pasos.
