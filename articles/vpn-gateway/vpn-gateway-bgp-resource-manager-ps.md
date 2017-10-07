---
title: "Configuración de BGP en Azure VPN Gateway: Resource Manager: PowerShell | Microsoft Docs"
description: "Este artículo le guiará a la hora de configurar BGP con puertas de enlace de VPN de Azure por medio de Azure Resource Manager y PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 905b11a7-1333-482c-820b-0fd0f44238e5
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: yushwang
ms.openlocfilehash: a9d13ae6b319e2efa8965dc2955c9b89ac3fd12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-bgp-on-azure-vpn-gateways-using-powershell"></a>¿Cómo tooconfigure BGP en puertas de enlace de VPN de Azure con PowerShell
Este artículo le guiará a través de hello pasos tooenable BGP en una conexión de VPN de sitio a sitio (S2S) entre entornos y una conexión de red virtual a red virtual con el modelo de implementación del Administrador de recursos de Hola y PowerShell.

## <a name="about-bgp"></a>Información acerca de BGP
BGP es frecuente en hello tooexchange enrutamiento y alcance de la información de Internet entre dos o más redes de protocolo de enrutamiento estándar Hola. BGP permite puertas de enlace de VPN de Azure de Hola y los dispositivos VPN local, que se llama a los pares BGP o a los vecinos, tooexchange "enruta" que le informará de las puertas de enlace en la disponibilidad de Hola y accesibilidad de los prefijos toogo a través de las puertas de enlace de Hola o enrutadores implicados. BGP también puede habilitar el enrutamiento del tránsito entre varias redes mediante la propagación de las rutas de una puerta de enlace BGP aprende desde una BGP del mismo nivel tooall otros pares BGP.

Vea [información general de BGP con puertas de enlace de VPN de Azure](vpn-gateway-bgp-overview.md) para obtener más información sobre los beneficios de BGP y toounderstand requisitos técnicos de Hola y consideraciones de uso de BGP.

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a>Introducción a BGP en puertas de enlace de VPN de Azure

Este artículo le guiará a través de Hola Hola de toodo pasos siguientes tareas:

* [Parte 1: Habilitar BGP en la puerta de enlace de VPN de Azure](#enablebgp)
* [Parte 2: Establecer una conexión entre locales con BGP](#crossprembgp)
* [Parte 3: Establecer una conexión de red virtual a red virtual con BGP](#v2vbgp)

Cada parte de instrucciones de hello constituye una piedra angular para habilitar BGP en la conectividad de red. Si completa todas las tres partes, generar topología Hola tal como se muestra en hello siguiente diagrama:

![Topología de BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

Puede combinar elementos juntos toobuild una red de tránsito más complejos y de múltiples saltos, que satisfaga sus necesidades.

## <a name ="enablebgp"></a>Parte 1: configurar BGP en hello puerta de enlace de VPN de Azure
pasos de configuración de Hello configurar Hola parámetros BGP de puerta de enlace de VPN de Azure de hello como se muestra en hello siguiente diagrama:

![Puerta de enlace de BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a>Antes de empezar
* Compruebe que tiene una suscripción a Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Instalar cmdlets de PowerShell del Administrador de recursos de Azure de Hola. Para obtener más información acerca de cómo instalar los cmdlets de PowerShell de hello, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview). 

### <a name="step-1---create-and-configure-vnet1"></a>Paso 1: Creación y configuración de VNet1
#### <a name="1-declare-your-variables"></a>1. Declaración de las variables
Para este ejercicio, se empieza por declarar las variables. Hello en el ejemplo siguiente se declara las variables de hello con valores de hello para este ejercicio. Ser seguro de valores de hello tooreplace con su propio cuando se configura para la producción. Puede utilizar estas variables si está ejecutando a través de hello pasos toobecome familiarizado con este tipo de configuración. Modificar variables de hello y, a continuación, copie y pegue en la consola de PowerShell.

```powershell
$Sub1 = "Replace_With_Your_Subcription_Name"
$RG1 = "TestBGPRG1"
$Location1 = "East US"
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
$GWIPName1 = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection12 = "VNet1toVNet2"
$Connection15 = "VNet1toSite5"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Conectar tooyour suscripción y crear un nuevo grupo de recursos
Hola toouse cmdlets del Administrador de recursos, asegúrese de cambiar el modo de tooPowerShell. Para obtener más información, consulte [Uso de Windows PowerShell con el Administrador de recursos](../powershell-azure-resource-manager.md).

Abra la consola de PowerShell y conectar con tooyour cuenta. Usar hello después toohelp de ejemplo que conectarse:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. Creación de TestVNet1
Hello en el ejemplo siguiente crea una red virtual denominada TestVNet1 y tres subredes, un GatewaySubnet llamado, uno llamado front-end y un back-end de llamada. Al reemplazar valores, es importante que siempre asigne el nombre GatewaySubnet a la subred de la puerta de enlace. Si usa otro, se produce un error al crear la puerta de enlace.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-bgp-parameters"></a>Paso 2: crear Hola puerta de enlace VPN para TestVNet1 con parámetros BGP
#### <a name="1-create-hello-ip-and-subnet-configurations"></a>1. Crear configuraciones de IP y una subred de Hola
Solicitar una pública dirección toobe toohello asignado puerta de enlace IP que creará para la red virtual. También definirá las configuraciones IP y subred Hola necesario.

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-hello-vpn-gateway-with-hello-as-number"></a>2. Crear puerta de enlace VPN de hello con hello como número
Crear puerta de enlace de red virtual de Hola para TestVNet1. BGP requiere un basadas en enrutamiento puerta de enlace VPN y también Hola suma parámetro, - Asn tooset Hola ASN (número de AS) para TestVNet1. Si no establece el parámetro ASN hello, se asigna ASN 65515. Crear una puerta de enlace puede tardar un tiempo (30 minutos o más toocomplete).

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-hello-azure-bgp-peer-ip-address"></a>3. Obtener dirección IP de Azure BGP del mismo nivel de Hola
Una vez creada la puerta de enlace de hello, necesita tooobtain Hola BGP del mismo nivel IP dirección en hello puerta de enlace de VPN de Azure. Esta dirección es necesario tooconfigure Hola puerta de enlace de VPN de Azure como un par BGP para los dispositivos VPN local.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

último comando de Hello muestra configuraciones de BGP correspondientes de hello en hello puerta de enlace de VPN de Azure; Por ejemplo:

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

Una vez creada la puerta de enlace de hello, puede usar esta conexión de puerta de enlace tooestablish entre entornos o conexión de red virtual a red virtual con BGP. Hello en las siguientes secciones se abordan Hola pasos toocomplete Hola ejercicio.

## <a name ="crossprembbgp"></a>Parte 2: Establecer una conexión entre locales con BGP

tooestablish una conexión entre entornos, necesita una puerta de enlace de red Local toorepresent toocreate dispositivo VPN local y una puerta de enlace de conexión tooconnect Hola VPN con puerta de enlace de red local de Hola. Aunque hay artículos que le guiarán a través de estos pasos, este artículo contiene parámetros de configuración de BGP de Hola de hello propiedades adicionales toospecify necesarios.

![BGP entre locales](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

Antes de continuar, asegúrese de que ha completado la [parte 1](#enablebgp) de este ejercicio.

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>Paso 1: crear y configurar la puerta de enlace de red local de Hola

#### <a name="1-declare-your-variables"></a>1. Declaración de las variables

Este ejercicio continúa toobuild configuración de Hola que se muestra en el diagrama de Hola. Ser seguro tooreplace valores de hello con hello las que desea que toouse para la configuración.

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

Un par de cosas toonote con respecto a los parámetros de puerta de enlace de red local de hello:

* puerta de enlace de red local de Hello puede estar en Hola iguales o diferentes y ubicación de recurso de grupo como Hola puerta de enlace VPN. Este ejemplo los muestra en distintos grupos de recursos en diferentes ubicaciones.
* prefijo mínima Hola necesita toodeclare para puerta de enlace de red local de hello es la dirección de host de Hola de su dirección IP de BGP del mismo nivel en el dispositivo VPN. En este caso, es un prefijo /32 de "10.52.255.254/32".
* Como recordatorio, debe usar diferentes ASN de BGP entre las redes locales y la red virtual de Azure. Si se hello mismo, deberá toochange el ASN VNet si el dispositivo VPN local ya utiliza Hola ASN toopeer con otros vecinos BGP.

Antes de continuar, asegúrese de que está conectado aún tooSubscription 1.

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2. Crear puerta de enlace de red local de Hola para Site5

Estar seguro de grupo de recursos de hello toocreate si no se creó, antes de crear la puerta de enlace de red local de Hola. Observe Hola dos parámetros adicionales para la puerta de enlace de red local de hello: Asn y BgpPeerAddress.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>Paso 2: conectar la puerta de enlace de red virtual de Hola y puerta de enlace de red local

#### <a name="1-get-hello-two-gateways"></a>1. Obtener Hola dos puertas de enlace

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2. Crear conexiones de hello TestVNet1 tooSite5

En este paso, se crea la conexión de Hola de TestVNet1 tooSite5. Debe especificar "-EnableBGP $True" tooenable BGP para esta conexión. Tal y como se indicó anteriormente, es posible toohave conexiones BGP y no BGP en Hola misma puerta de enlace de VPN de Azure. A menos que el BGP está habilitado en la propiedad de conexión de hello, Azure no habilitará BGP para esta conexión, aunque los parámetros BGP ya están configuradas en las puertas de enlace.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

Hello en el ejemplo siguiente se enumera los parámetros de hello que escriba en la sección de configuración de BGP de hello en dispositivo VPN local para este ejercicio:

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being hello VPN tunnel interface on your device
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

una vez establecida la conexión IPsec hello, se establece conexión de Hello después de unos minutos y se inicia sesión BGP emparejamiento Hola.

## <a name ="v2vbgp"></a>Parte 3: Establecer una conexión de red virtual a red virtual con BGP

En esta sección se agrega una conexión de red virtual a red virtual con BGP, como se muestra en hello siguiente diagrama:

![BGP para conexiones de red virtual a red virtual](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

continuar Hola siguiendo las instrucciones de los pasos anteriores de Hola. Debe completar [parte I](#enablebgp) toocreate TestVNet1 y configurar Hola puerta de enlace de VPN con BGP. 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>Paso 1: crear la puerta de enlace VPN de hello y TestVNet2

Es importante toomake seguro de que el espacio de direcciones IP de Hola de hello nueva red virtual, TestVNet2, no se superponen con ninguno de los intervalos de red virtual.

En este ejemplo, redes virtuales de hello pertenecen toohello misma suscripción. Se pueden configurar conexiones de red virtual a red virtual entre distintas suscripciones. Para obtener más información, consulte [Configuración de una conexión de red virtual a red virtual](vpn-gateway-vnet-vnet-rm-ps.md). Asegúrese de agregar Hola "-EnableBgp $True" al crear Hola conexiones tooenable BGP.

#### <a name="1-declare-your-variables"></a>1. Declaración de las variables

Ser seguro tooreplace valores de hello con hello las que desea que toouse para la configuración.

```powershell
$RG2 = "TestBGPRG2"
$Location2 = "West US"
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
$GWIPName2 = "VNet2GWIP"
$GWIPconfName2 = "gwipconf2"
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

#### <a name="3-create-hello-vpn-gateway-for-testvnet2-with-bgp-parameters"></a>3. Crear puerta de enlace VPN de Hola para TestVNet2 con parámetros BGP

Solicitar una pública dirección toobe toohello asignado puerta de enlace IP creará para la red virtual y definir configuraciones de IP y subred Hola necesario.

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

Crear puerta de enlace VPN de hello con hello como número. Debe reemplazar predeterminado Hola ASN en las puertas de enlace de VPN de Azure. Hola ASN para hello conectado las redes virtuales debe ser diferente tooenable BGP y el enrutamiento de tránsito.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
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

En este paso, creará conexión Hola de TestVNet1 tooTestVNet2 y conexión de Hola de TestVNet2 tooTestVNet1.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> Ser seguro tooenable BGP para las conexiones de ambos.
> 
> 

Después de completar estos pasos, se establece la conexión de hello después de unos minutos. sesión de emparejamiento de BGP Hola está activo cuando se haya completado Hola conexión de red virtual a red virtual.

Si ha completado las tres partes de este ejercicio, han establecido Hola después de la topología de red:

![BGP para conexiones de red virtual a red virtual](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a>Pasos siguientes

Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour. Consulte [Creación de una máquina virtual que ejecuta Windows en el Portal de Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para ver los pasos.
