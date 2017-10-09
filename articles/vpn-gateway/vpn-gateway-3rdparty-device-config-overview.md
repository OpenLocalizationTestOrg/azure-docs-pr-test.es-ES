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
# <a name="overview-of-3rd-party-vpn-device-configurations"></a><span data-ttu-id="bdd00-103">Información general sobre configuraciones de dispositivos VPN de terceros</span><span class="sxs-lookup"><span data-stu-id="bdd00-103">Overview of 3rd party VPN device configurations</span></span>
<span data-ttu-id="bdd00-104">Este artículo proporciona información general sobre las configuraciones de dispositivos VPN locales para conectar las puertas de enlace VPN de tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bdd00-104">This article provides an overview of on-premises VPN device configurations for connecting tooAzure VPN gateways.</span></span> <span data-ttu-id="bdd00-105">ejemplo de Hola a red virtual de Azure y VPN puerta de enlace el programa de instalación será dispositivos VPN locales que toodifferent tooconnect usado con hello mismos parámetros.</span><span class="sxs-lookup"><span data-stu-id="bdd00-105">hello sample Azure virtual network and VPN gateway setup will be used tooconnect toodifferent on-premises VPN devices with hello same parameters.</span></span>

## <a name="device-requirements"></a><span data-ttu-id="bdd00-106">Requisitos del dispositivo</span><span class="sxs-lookup"><span data-stu-id="bdd00-106">Device requirements</span></span>
<span data-ttu-id="bdd00-107">Las puertas de enlace de VPN de Azure usan los conjuntos de protocolos IPsec o IKE estándar para túneles VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="bdd00-107">Azure VPN gateways use standard IPsec/IKE protocol suites for S2S VPN tunnels.</span></span> <span data-ttu-id="bdd00-108">Consulte demasiado[dispositivos VPN sobre](vpn-gateway-about-vpn-devices.md) para hello detallado parámetros de protocolo IPsec/IKE y algoritmos criptográficos predeterminados para las puertas de enlace de VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="bdd00-108">Refer too[About VPN devices](vpn-gateway-about-vpn-devices.md) for hello detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="bdd00-109">Puede especificar opcionalmente Hola exactamente la combinación de algoritmos criptográficos y las ventajas claves para una conexión específica, como se describe en [sobre los requisitos de cifrado](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="bdd00-109">You can optionally specify hello exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span>

## <span data-ttu-id="bdd00-110"><a name ="singletunnel"></a>Túnel VPN único</span><span class="sxs-lookup"><span data-stu-id="bdd00-110"><a name ="singletunnel"></a>Single VPN tunnel</span></span>
<span data-ttu-id="bdd00-111">topología primera Hola consta de un solo túnel de VPN de S2S entre una puerta de enlace de VPN de Azure y el dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="bdd00-111">hello first topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="bdd00-112">Opcionalmente puede configurar BGP a través del túnel VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="bdd00-112">You can optionally configure BGP across hello VPN tunnel.</span></span>

![túnel único](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

<span data-ttu-id="bdd00-114">Consulte demasiado[configurar conexión de sitio a sitio](vpn-gateway-howto-site-to-site-resource-manager-portal.md) para obtener instrucciones detalladas, paso a paso.</span><span class="sxs-lookup"><span data-stu-id="bdd00-114">Refer too[Configure site-to-site connection](vpn-gateway-howto-site-to-site-resource-manager-portal.md) for detailed, step-by-step guidance.</span></span> <span data-ttu-id="bdd00-115">Hello las secciones siguientes enumeran parámetros Hola y proporcionan un toohelp de secuencia de comandos de PowerShell de ejemplo empezar a.</span><span class="sxs-lookup"><span data-stu-id="bdd00-115">hello following sections list hello parameters and provide a sample PowerShell script toohelp you get started.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="bdd00-116">Información de puerta de enlace de VPN y de red</span><span class="sxs-lookup"><span data-stu-id="bdd00-116">Network and VPN gateway information</span></span>
<span data-ttu-id="bdd00-117">En esta sección se indican los parámetros de Hola para obtener ejemplos de hello anteriores.</span><span class="sxs-lookup"><span data-stu-id="bdd00-117">This section list hello parameters for hello examples above.</span></span>

| <span data-ttu-id="bdd00-118">**Parámetro**</span><span class="sxs-lookup"><span data-stu-id="bdd00-118">**Parameter**</span></span>                | <span data-ttu-id="bdd00-119">**Valor**</span><span class="sxs-lookup"><span data-stu-id="bdd00-119">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="bdd00-120">Prefijos de dirección de red virtual</span><span class="sxs-lookup"><span data-stu-id="bdd00-120">VNet address prefixes</span></span>        | <span data-ttu-id="bdd00-121">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="bdd00-121">10.11.0.0/16</span></span><br><span data-ttu-id="bdd00-122">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="bdd00-122">10.12.0.0/16</span></span> |
| <span data-ttu-id="bdd00-123">Dirección IP de la puerta de enlace de VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="bdd00-123">Azure VPN gateway IP</span></span>         | <span data-ttu-id="bdd00-124">Dirección IP de la puerta de enlace de VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="bdd00-124">Azure VPN Gateway IP</span></span>         |
| <span data-ttu-id="bdd00-125">Prefijos de direcciones locales</span><span class="sxs-lookup"><span data-stu-id="bdd00-125">On-premises address prefixes</span></span> | <span data-ttu-id="bdd00-126">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="bdd00-126">10.51.0.0/16</span></span><br><span data-ttu-id="bdd00-127">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="bdd00-127">10.52.0.0/16</span></span> |
| <span data-ttu-id="bdd00-128">Dirección IP del dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="bdd00-128">On-premises VPN device IP</span></span>    | <span data-ttu-id="bdd00-129">Dirección IP del dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="bdd00-129">On-premises VPN device IP</span></span>    |
| <span data-ttu-id="bdd00-130">*ASN de BGP de red virtual</span><span class="sxs-lookup"><span data-stu-id="bdd00-130">*VNet BGP ASN</span></span>                | <span data-ttu-id="bdd00-131">65010</span><span class="sxs-lookup"><span data-stu-id="bdd00-131">65010</span></span>                        |
| <span data-ttu-id="bdd00-132">*Dirección IP del par BGP de Azure</span><span class="sxs-lookup"><span data-stu-id="bdd00-132">*Azure BGP peer IP</span></span>           | <span data-ttu-id="bdd00-133">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="bdd00-133">10.12.255.30</span></span>                 |
| <span data-ttu-id="bdd00-134">*ASN de BGP local</span><span class="sxs-lookup"><span data-stu-id="bdd00-134">*On-premises BGP ASN</span></span>         | <span data-ttu-id="bdd00-135">65050</span><span class="sxs-lookup"><span data-stu-id="bdd00-135">65050</span></span>                        |
| <span data-ttu-id="bdd00-136">*Dirección IP del par BGP local</span><span class="sxs-lookup"><span data-stu-id="bdd00-136">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="bdd00-137">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="bdd00-137">10.52.255.254</span></span>                |

* <span data-ttu-id="bdd00-138">(*) Parámetros opcionales solo para BGP</span><span class="sxs-lookup"><span data-stu-id="bdd00-138">(*) Optional parameters for BGP only</span></span>

### <a name="sample-powershell-script"></a><span data-ttu-id="bdd00-139">Script de PowerShell de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bdd00-139">Sample PowerShell script</span></span>
<span data-ttu-id="bdd00-140">[Crear una conexión VPN de S2S mediante PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) se incluyen instrucciones detalladas de Hola.</span><span class="sxs-lookup"><span data-stu-id="bdd00-140">[Create a S2S VPN connection using PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) has hello detailed instructions.</span></span> <span data-ttu-id="bdd00-141">Esta sección proporciona una tooget de secuencia de comandos de ejemplo que se inició.</span><span class="sxs-lookup"><span data-stu-id="bdd00-141">This section provides a sample script tooget you started.</span></span>

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

### <span data-ttu-id="bdd00-142"><a name ="policybased"></a>[Opcional] Usar directivas personalizadas de IPsec/IKE con "UsePolicyBasedTrafficSelectors"</span><span class="sxs-lookup"><span data-stu-id="bdd00-142"><a name ="policybased"></a> [Optional] Use custom IPsec/IKE policy with "UsePolicyBasedTrafficSelectors"</span></span>
<span data-ttu-id="bdd00-143">Si los dispositivos VPN son compatibles con los selectores de tráfico "y a cualquier" (configuración según/VTI-basadas en enrutamiento), necesitará toocreate una directiva de IPsec/IKE personalizada y configurar la opción de "UsePolicyBasedTrafficSelectors" como se describe en [este artículo ](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="bdd00-143">If your VPN devices do not support "any-to-any" traffic selectors (route-based/VTI-based configuration), you will need toocreate a custom IPsec/IKE policy and configure "UsePolicyBasedTrafficSelectors" option as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bdd00-144">Necesita una directiva de IPsec/IKE en orden tooenable "UsePolicyBasedTrafficSelectors" opción de conexión de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="bdd00-144">You need toocreate an IPsec/IKE policy in order tooenable "UsePolicyBasedTrafficSelectors" option on hello connection.</span></span>

<span data-ttu-id="bdd00-145">script de ejemplo de Hola siguiente crea una directiva de IPsec/IKE con hello siguientes algoritmos y parámetros:</span><span class="sxs-lookup"><span data-stu-id="bdd00-145">hello sample script below creates an IPsec/IKE policy with hello following algorithms and parameters:</span></span>
* <span data-ttu-id="bdd00-146">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="bdd00-146">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="bdd00-147">IPsec: AES256, SHA1, PFS24, vigencia de SA 7200 segundos y 20480000 KB (20 GB)</span><span class="sxs-lookup"><span data-stu-id="bdd00-147">IPsec: AES256, SHA1, PFS24, SA Lifetime 7200 seconds & 20480000KB (20GB)</span></span>

<span data-ttu-id="bdd00-148">A continuación, aplica la directiva de Hola y permite "UesPolicyBasedTrafficSelectors" en la conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="bdd00-148">It then applies hello policy and enables "UesPolicyBasedTrafficSelectors" on hello connection.</span></span>

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <span data-ttu-id="bdd00-149"><a name ="bgp"></a>[Opcional] Usar BGP en una conexión VPN S2S</span><span class="sxs-lookup"><span data-stu-id="bdd00-149"><a name ="bgp"></a>[Optional] Use BGP on S2S VPN connection</span></span>
<span data-ttu-id="bdd00-150">También puede usar BGP en conexión Hola.</span><span class="sxs-lookup"><span data-stu-id="bdd00-150">You can optionally use BGP on hello connection.</span></span> <span data-ttu-id="bdd00-151">Consulte [BGP para puerta de enlace de VPN](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="bdd00-151">See [BGP for VPN gateway](vpn-gateway-bgp-resource-manager-ps.md).</span></span> <span data-ttu-id="bdd00-152">Hay dos diferencias:</span><span class="sxs-lookup"><span data-stu-id="bdd00-152">There are two differences:</span></span>

<span data-ttu-id="bdd00-153">prefijos de direcciones locales de Hello pueden ser una dirección de host único, la dirección IP Hola local BGP del mismo nivel:</span><span class="sxs-lookup"><span data-stu-id="bdd00-153">hello on-premises address prefixes can be a single host address, hello on-premises BGP peer IP address:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

<span data-ttu-id="bdd00-154">Debe establecer "-EnableBGP" demasiado$ True al crear conexión hello:</span><span class="sxs-lookup"><span data-stu-id="bdd00-154">You must set "-EnableBGP" too$True when creating hello connection:</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a><span data-ttu-id="bdd00-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bdd00-155">Next steps</span></span>
<span data-ttu-id="bdd00-156">Vea [configuración activo / activo VPN las puertas de enlace para las conexiones de red virtual a red virtual y entre entornos](vpn-gateway-activeactive-rm-powershell.md) para las conexiones de red virtual a red virtual y pasos tooconfigure de activo / activo entre entornos.</span><span class="sxs-lookup"><span data-stu-id="bdd00-156">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps tooconfigure active-active cross-premises and VNet-to-VNet connections.</span></span>

