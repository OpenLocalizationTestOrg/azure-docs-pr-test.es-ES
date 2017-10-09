---
title: "aaaAbout 3ª parte dispositivo configuración tooconnect tooAzure VPN puertas de enlace VPN | Documentos de Microsoft"
description: "Este artículo proporciona información general sobre 3rd configuraciones de dispositivo VPN de entidad para conectar las puertas de enlace VPN de tooAzure."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: 3bb4fc94bc625386c2d0a02e1dcbdeb38ee0665e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-3rd-party-vpn-device-configurations"></a>Información general sobre configuraciones de dispositivos VPN de terceros
Este artículo proporciona información general sobre las configuraciones de dispositivos VPN locales para conectar las puertas de enlace VPN de tooAzure. ejemplo de Hola a red virtual de Azure y VPN puerta de enlace el programa de instalación será dispositivos VPN locales que toodifferent tooconnect usado con hello mismos parámetros.

## <a name="device-requirements"></a>Requisitos del dispositivo
Las puertas de enlace de VPN de Azure usan los conjuntos de protocolos IPsec o IKE estándar para túneles VPN S2S. Consulte demasiado[dispositivos VPN sobre](vpn-gateway-about-vpn-devices.md) para hello detallado parámetros de protocolo IPsec/IKE y algoritmos criptográficos predeterminados para las puertas de enlace de VPN de Azure. Puede especificar opcionalmente Hola exactamente la combinación de algoritmos criptográficos y las ventajas claves para una conexión específica, como se describe en [sobre los requisitos de cifrado](vpn-gateway-about-compliance-crypto.md).

## <a name ="singletunnel"></a>Túnel VPN único
topología primera Hola consta de un solo túnel de VPN de S2S entre una puerta de enlace de VPN de Azure y el dispositivo VPN local. Opcionalmente puede configurar BGP a través del túnel VPN de Hola.

![túnel único](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

Consulte demasiado[configurar conexión de sitio a sitio](vpn-gateway-howto-site-to-site-resource-manager-portal.md) para obtener instrucciones detalladas, paso a paso. Hello las secciones siguientes enumeran parámetros Hola y proporcionan un toohelp de secuencia de comandos de PowerShell de ejemplo empezar a.

### <a name="network-and-vpn-gateway-information"></a>Información de puerta de enlace de VPN y de red
En esta sección se indican los parámetros de Hola para obtener ejemplos de hello anteriores.

| **Parámetro**                | **Valor**                    |
| ---                          | ---                          |
| Prefijos de dirección de red virtual        | 10.11.0.0/16<br>10.12.0.0/16 |
| Dirección IP de la puerta de enlace de VPN de Azure         | Dirección IP de la puerta de enlace de VPN de Azure         |
| Prefijos de direcciones locales | 10.51.0.0/16<br>10.52.0.0/16 |
| Dirección IP del dispositivo VPN local    | Dirección IP del dispositivo VPN local    |
| *ASN de BGP de red virtual                | 65010                        |
| *Dirección IP del par BGP de Azure           | 10.12.255.30                 |
| *ASN de BGP local         | 65050                        |
| *Dirección IP del par BGP local     | 10.52.255.254                |

* (*) Parámetros opcionales solo para BGP

### <a name="sample-powershell-script"></a>Script de PowerShell de ejemplo
[Crear una conexión VPN de S2S mediante PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) se incluyen instrucciones detalladas de Hola. Esta sección proporciona una tooget de secuencia de comandos de ejemplo que se inició.

```powershell
# Declare your variables

$Sub1          = "Replace_With_Your_Subcription_Name"
$RG1           = "TestRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$VNet1ASN      = 65010
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GWIPName1     = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection15  = "VNet1toSite5"
$LNGName5      = "Site5"
$LNGPrefix50   = "10.52.255.254/32"
$LNGPrefix51   = "10.51.0.0/16"
$LNGPrefix52   = "10.52.0.0/16"
$LNGIP5        = "Your_VPN_Device_IP"
$LNGASN5       = 65050
$BGPPeerIP5    = "10.52.255.254"

# Connect tooyour subscription and create a new resource group

Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1

# Create virtual network

$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

# Create VPN gateway

$gwpip1    = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1     = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN

# Create local network gateway

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix51,$LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5

# Create hello S2S VPN connection

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False
```

### <a name ="policybased"></a>[Opcional] Usar directivas personalizadas de IPsec/IKE con "UsePolicyBasedTrafficSelectors"
Si los dispositivos VPN son compatibles con los selectores de tráfico "y a cualquier" (configuración según/VTI-basadas en enrutamiento), necesitará toocreate una directiva de IPsec/IKE personalizada y configurar la opción de "UsePolicyBasedTrafficSelectors" como se describe en [este artículo ](vpn-gateway-connect-multiple-policybased-rm-ps.md).

> [!IMPORTANT]
> Necesita una directiva de IPsec/IKE en orden tooenable "UsePolicyBasedTrafficSelectors" opción de conexión de hello toocreate.

script de ejemplo de Hola siguiente crea una directiva de IPsec/IKE con hello siguientes algoritmos y parámetros:
* IKEv2: AES256, SHA384, DHGroup24
* IPsec: AES256, SHA1, PFS24, vigencia de SA 7200 segundos y 20480000 KB (20 GB)

A continuación, aplica la directiva de Hola y permite "UesPolicyBasedTrafficSelectors" en la conexión de Hola.

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <a name ="bgp"></a>[Opcional] Usar BGP en una conexión VPN S2S
También puede usar BGP en conexión Hola. Consulte [BGP para puerta de enlace de VPN](vpn-gateway-bgp-resource-manager-ps.md). Hay dos diferencias:

prefijos de direcciones locales de Hello pueden ser una dirección de host único, la dirección IP Hola local BGP del mismo nivel:

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

Debe establecer "-EnableBGP" demasiado$ True al crear conexión hello:

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a>Pasos siguientes
Vea [configuración activo / activo VPN las puertas de enlace para las conexiones de red virtual a red virtual y entre entornos](vpn-gateway-activeactive-rm-powershell.md) para las conexiones de red virtual a red virtual y pasos tooconfigure de activo / activo entre entornos.

