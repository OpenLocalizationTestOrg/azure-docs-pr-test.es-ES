---
title: "Configuración de dispositivos VPN de terceros para su conexión con puertas de enlace de VPN de Azure | Microsoft Docs"
description: "Este artículo proporciona información general sobre configuraciones de dispositivos VPN de terceros para conectarse a puertas de enlace de VPN de Azure."
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
ms.openlocfilehash: 72dab85bb882b05d72cef26bef70437695b70416
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-3rd-party-vpn-device-configurations"></a><span data-ttu-id="09726-103">Información general sobre configuraciones de dispositivos VPN de terceros</span><span class="sxs-lookup"><span data-stu-id="09726-103">Overview of 3rd party VPN device configurations</span></span>
<span data-ttu-id="09726-104">Este artículo proporciona información general sobre configuraciones de dispositivos VPN locales para conectarse a puertas de enlace de VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="09726-104">This article provides an overview of on-premises VPN device configurations for connecting to Azure VPN gateways.</span></span> <span data-ttu-id="09726-105">La red virtual de Azure de ejemplo y la configuración de la puerta de enlace de VPN se usarán para conectarse a distintos dispositivos VPN locales con los mismos parámetros.</span><span class="sxs-lookup"><span data-stu-id="09726-105">The sample Azure virtual network and VPN gateway setup will be used to connect to different on-premises VPN devices with the same parameters.</span></span>

## <a name="device-requirements"></a><span data-ttu-id="09726-106">Requisitos del dispositivo</span><span class="sxs-lookup"><span data-stu-id="09726-106">Device requirements</span></span>
<span data-ttu-id="09726-107">Las puertas de enlace de VPN de Azure usan los conjuntos de protocolos IPsec o IKE estándar para túneles VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="09726-107">Azure VPN gateways use standard IPsec/IKE protocol suites for S2S VPN tunnels.</span></span> <span data-ttu-id="09726-108">Consulte [Acerca de los dispositivos VPN](vpn-gateway-about-vpn-devices.md) para obtener los parámetros detallados del protocolo IPsec o IKE y los algoritmos criptográficos predeterminados para las puertas de enlace de VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="09726-108">Refer to [About VPN devices](vpn-gateway-about-vpn-devices.md) for the detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="09726-109">También puede especificar la combinación exacta de algoritmos criptográficos y niveles de clave para una conexión específica, como se describe en [Acerca de los requisitos criptográficos](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="09726-109">You can optionally specify the exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span>

## <span data-ttu-id="09726-110"><a name ="singletunnel"></a>Túnel VPN único</span><span class="sxs-lookup"><span data-stu-id="09726-110"><a name ="singletunnel"></a>Single VPN tunnel</span></span>
<span data-ttu-id="09726-111">Esta primera topología consta de un solo túnel VPN S2S entre una puerta de enlace de VPN de Azure y el dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="09726-111">The first topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="09726-112">Opcionalmente puede configurar BGP a través del túnel VPN.</span><span class="sxs-lookup"><span data-stu-id="09726-112">You can optionally configure BGP across the VPN tunnel.</span></span>

![túnel único](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

<span data-ttu-id="09726-114">Consulte [Configurar una conexión de sitio a sitio](vpn-gateway-howto-site-to-site-resource-manager-portal.md) para obtener instrucciones detalladas paso a paso.</span><span class="sxs-lookup"><span data-stu-id="09726-114">Refer to [Configure site-to-site connection](vpn-gateway-howto-site-to-site-resource-manager-portal.md) for detailed, step-by-step guidance.</span></span> <span data-ttu-id="09726-115">Las secciones siguientes indican los parámetros y proporcionan un script de PowerShell de ejemplo para ayudarle a empezar a trabajar.</span><span class="sxs-lookup"><span data-stu-id="09726-115">The following sections list the parameters and provide a sample PowerShell script to help you get started.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="09726-116">Información de puerta de enlace de VPN y de red</span><span class="sxs-lookup"><span data-stu-id="09726-116">Network and VPN gateway information</span></span>
<span data-ttu-id="09726-117">En esta sección se muestran los parámetros de este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="09726-117">This section list the parameters for the examples above.</span></span>

| <span data-ttu-id="09726-118">**Parámetro**</span><span class="sxs-lookup"><span data-stu-id="09726-118">**Parameter**</span></span>                | <span data-ttu-id="09726-119">**Valor**</span><span class="sxs-lookup"><span data-stu-id="09726-119">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="09726-120">Prefijos de dirección de red virtual</span><span class="sxs-lookup"><span data-stu-id="09726-120">VNet address prefixes</span></span>        | <span data-ttu-id="09726-121">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="09726-121">10.11.0.0/16</span></span><br><span data-ttu-id="09726-122">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="09726-122">10.12.0.0/16</span></span> |
| <span data-ttu-id="09726-123">Dirección IP de la puerta de enlace de VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="09726-123">Azure VPN gateway IP</span></span>         | <span data-ttu-id="09726-124">Dirección IP de la puerta de enlace de VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="09726-124">Azure VPN Gateway IP</span></span>         |
| <span data-ttu-id="09726-125">Prefijos de direcciones locales</span><span class="sxs-lookup"><span data-stu-id="09726-125">On-premises address prefixes</span></span> | <span data-ttu-id="09726-126">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="09726-126">10.51.0.0/16</span></span><br><span data-ttu-id="09726-127">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="09726-127">10.52.0.0/16</span></span> |
| <span data-ttu-id="09726-128">Dirección IP del dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="09726-128">On-premises VPN device IP</span></span>    | <span data-ttu-id="09726-129">Dirección IP del dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="09726-129">On-premises VPN device IP</span></span>    |
| <span data-ttu-id="09726-130">*ASN de BGP de red virtual</span><span class="sxs-lookup"><span data-stu-id="09726-130">*VNet BGP ASN</span></span>                | <span data-ttu-id="09726-131">65010</span><span class="sxs-lookup"><span data-stu-id="09726-131">65010</span></span>                        |
| <span data-ttu-id="09726-132">*Dirección IP del par BGP de Azure</span><span class="sxs-lookup"><span data-stu-id="09726-132">*Azure BGP peer IP</span></span>           | <span data-ttu-id="09726-133">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="09726-133">10.12.255.30</span></span>                 |
| <span data-ttu-id="09726-134">*ASN de BGP local</span><span class="sxs-lookup"><span data-stu-id="09726-134">*On-premises BGP ASN</span></span>         | <span data-ttu-id="09726-135">65050</span><span class="sxs-lookup"><span data-stu-id="09726-135">65050</span></span>                        |
| <span data-ttu-id="09726-136">*Dirección IP del par BGP local</span><span class="sxs-lookup"><span data-stu-id="09726-136">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="09726-137">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="09726-137">10.52.255.254</span></span>                |

* <span data-ttu-id="09726-138">(*) Parámetros opcionales solo para BGP</span><span class="sxs-lookup"><span data-stu-id="09726-138">(*) Optional parameters for BGP only</span></span>

### <a name="sample-powershell-script"></a><span data-ttu-id="09726-139">Script de PowerShell de ejemplo</span><span class="sxs-lookup"><span data-stu-id="09726-139">Sample PowerShell script</span></span>
<span data-ttu-id="09726-140">El artículo [Creación de una conexión VPN de S2S mediante PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) tiene instrucciones detalladas.</span><span class="sxs-lookup"><span data-stu-id="09726-140">[Create a S2S VPN connection using PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) has the detailed instructions.</span></span> <span data-ttu-id="09726-141">En esta sección se proporciona un script de ejemplo para ayudarle a comenzar.</span><span class="sxs-lookup"><span data-stu-id="09726-141">This section provides a sample script to get you started.</span></span>

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

# Connect to your subscription and create a new resource group

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

# Create the S2S VPN connection

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False
```

### <span data-ttu-id="09726-142"><a name ="policybased"></a>[Opcional] Usar directivas personalizadas de IPsec/IKE con "UsePolicyBasedTrafficSelectors"</span><span class="sxs-lookup"><span data-stu-id="09726-142"><a name ="policybased"></a> [Optional] Use custom IPsec/IKE policy with "UsePolicyBasedTrafficSelectors"</span></span>
<span data-ttu-id="09726-143">Si los dispositivos VPN no admiten selectores de tráfico universales (configuración basada en enrutamiento y en VTI), debe crear una directiva personalizada de IPsec/IKE y configurar la opción "UsePolicyBasedTrafficSelectors" como se describe en [este artículo](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="09726-143">If your VPN devices do not support "any-to-any" traffic selectors (route-based/VTI-based configuration), you will need to create a custom IPsec/IKE policy and configure "UsePolicyBasedTrafficSelectors" option as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09726-144">Debe crear una directiva IPsec/IKE para habilitar la opción "UsePolicyBasedTrafficSelectors" en la conexión.</span><span class="sxs-lookup"><span data-stu-id="09726-144">You need to create an IPsec/IKE policy in order to enable "UsePolicyBasedTrafficSelectors" option on the connection.</span></span>

<span data-ttu-id="09726-145">El script de ejemplo siguiente crea una directiva IPsec/IKE con los algoritmos y parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="09726-145">The sample script below creates an IPsec/IKE policy with the following algorithms and parameters:</span></span>
* <span data-ttu-id="09726-146">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="09726-146">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="09726-147">IPsec: AES256, SHA1, PFS24, vigencia de SA 7200 segundos y 20480000 KB (20 GB)</span><span class="sxs-lookup"><span data-stu-id="09726-147">IPsec: AES256, SHA1, PFS24, SA Lifetime 7200 seconds & 20480000KB (20GB)</span></span>

<span data-ttu-id="09726-148">A continuación, se aplica la directiva y permite "UesPolicyBasedTrafficSelectors" en la conexión.</span><span class="sxs-lookup"><span data-stu-id="09726-148">It then applies the policy and enables "UesPolicyBasedTrafficSelectors" on the connection.</span></span>

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <span data-ttu-id="09726-149"><a name ="bgp"></a>[Opcional] Usar BGP en una conexión VPN S2S</span><span class="sxs-lookup"><span data-stu-id="09726-149"><a name ="bgp"></a>[Optional] Use BGP on S2S VPN connection</span></span>
<span data-ttu-id="09726-150">También puede usar BGP en la conexión.</span><span class="sxs-lookup"><span data-stu-id="09726-150">You can optionally use BGP on the connection.</span></span> <span data-ttu-id="09726-151">Consulte [BGP para puerta de enlace de VPN](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="09726-151">See [BGP for VPN gateway](vpn-gateway-bgp-resource-manager-ps.md).</span></span> <span data-ttu-id="09726-152">Hay dos diferencias:</span><span class="sxs-lookup"><span data-stu-id="09726-152">There are two differences:</span></span>

<span data-ttu-id="09726-153">Los prefijos de dirección local pueden ser una dirección de host único, la dirección IP del par BGP local:</span><span class="sxs-lookup"><span data-stu-id="09726-153">The on-premises address prefixes can be a single host address, the on-premises BGP peer IP address:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

<span data-ttu-id="09726-154">Debe establecer "-EnableBGP" en $True al crear la conexión:</span><span class="sxs-lookup"><span data-stu-id="09726-154">You must set "-EnableBGP" to $True when creating the connection:</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a><span data-ttu-id="09726-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="09726-155">Next steps</span></span>
<span data-ttu-id="09726-156">Consulte [Configuración activa-activa de puertas de enlace de VPN para conexiones entre locales y de red virtual a red virtual](vpn-gateway-activeactive-rm-powershell.md) para ver los pasos para configurar de modo activo-activo conexiones entre locales y de red virtual a red virtual.</span><span class="sxs-lookup"><span data-stu-id="09726-156">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps to configure active-active cross-premises and VNet-to-VNet connections.</span></span>

