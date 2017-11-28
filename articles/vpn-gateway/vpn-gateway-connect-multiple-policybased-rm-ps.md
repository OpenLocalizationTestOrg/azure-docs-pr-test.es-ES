---
title: 'Conecte los dispositivos VPN basada en directivas de VPN de Azure puertas de enlace toomultiple local: Azure Resource Manager: PowerShell | Documentos de Microsoft'
description: "Este artículo le guiará a través de configuración de Azure basadas en enrutamiento puerta de enlace toomultiple basada en directivas VPN dispositivos VPN mediante el Administrador de recursos de Azure y PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/27/2017
ms.author: yushwang
ms.openlocfilehash: 866c78d96305207106a66cc3300c355e4b6bfbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-vpn-gateways-toomultiple-on-premises-policy-based-vpn-devices-using-powershell"></a><span data-ttu-id="bceab-103">Conectar VPN de Azure puertas de enlace toomultiple local basada en directivas VPN dispositivos con PowerShell</span><span class="sxs-lookup"><span data-stu-id="bceab-103">Connect Azure VPN gateways toomultiple on-premises policy-based VPN devices using PowerShell</span></span>

<span data-ttu-id="bceab-104">En este artículo le ayuda a configurar un Azure basadas en enrutamiento puerta de enlace tooconnect toomultiple local basada en directivas VPN los dispositivos VPN aprovechar las directivas de IPsec/IKE personalizadas en las conexiones VPN de S2S.</span><span class="sxs-lookup"><span data-stu-id="bceab-104">This article helps you configure an Azure route-based VPN gateway tooconnect toomultiple on-premises policy-based VPN devices leveraging custom IPsec/IKE policies on S2S VPN connections.</span></span>

## <a name="about-policy-based-and-route-based-vpn-gateways"></a><span data-ttu-id="bceab-105">Acerca de las puertas de enlace de VPN basadas en directivas y en rutas</span><span class="sxs-lookup"><span data-stu-id="bceab-105">About policy-based and route-based VPN gateways</span></span>

<span data-ttu-id="bceab-106">Directivas: *frente a* basadas en enrutamiento de los dispositivos VPN difieren en cómo se establecen los selectores de tráfico de IPsec de hello en una conexión:</span><span class="sxs-lookup"><span data-stu-id="bceab-106">Policy- *vs.* route-based VPN devices differ in how hello IPsec traffic selectors are set on a connection:</span></span>

* <span data-ttu-id="bceab-107">**Basada en directivas** dispositivos VPN utilizan combinaciones de Hola de prefijos de ambos toodefine redes cómo se cifra y descifra el tráfico a través de túneles de IPsec.</span><span class="sxs-lookup"><span data-stu-id="bceab-107">**Policy-based** VPN devices use hello combinations of prefixes from both networks toodefine how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="bceab-108">Normalmente se basa en dispositivos de firewall que realizan el filtrado de paquetes.</span><span class="sxs-lookup"><span data-stu-id="bceab-108">It is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="bceab-109">Descifrado y cifrado de túnel de IPsec se agregan toohello el filtrado de paquetes y el motor de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="bceab-109">IPsec tunnel encryption and decryption are added toohello packet filtering and processing engine.</span></span>
* <span data-ttu-id="bceab-110">**Basadas en enrutamiento** dispositivos VPN utilizan selectores de tráfico y para cualquier (comodín) y las tablas de permiten enrutamiento/reenvío túneles de IPsec toodifferent de dirigir el tráfico.</span><span class="sxs-lookup"><span data-stu-id="bceab-110">**Route-based** VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic toodifferent IPsec tunnels.</span></span> <span data-ttu-id="bceab-111">Normalmente se basa en plataformas de enrutador donde cada túnel IPsec se modela como una interfaz de red o VTI (interfaz de túnel virtual).</span><span class="sxs-lookup"><span data-stu-id="bceab-111">It is typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

<span data-ttu-id="bceab-112">Hello diagramas siguientes resaltan dos modelos de hello:</span><span class="sxs-lookup"><span data-stu-id="bceab-112">hello following diagrams highlight hello two models:</span></span>

### <a name="policy-based-vpn-example"></a><span data-ttu-id="bceab-113">Ejemplo de VPN basada en directivas</span><span class="sxs-lookup"><span data-stu-id="bceab-113">Policy-based VPN example</span></span>
![basada en directivas](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a><span data-ttu-id="bceab-115">Ejemplo de VPN basada en rutas</span><span class="sxs-lookup"><span data-stu-id="bceab-115">Route-based VPN example</span></span>
![basada en rutas](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a><span data-ttu-id="bceab-117">Compatibilidad de Azure con VPN basada en directivas</span><span class="sxs-lookup"><span data-stu-id="bceab-117">Azure support for policy-based VPN</span></span>
<span data-ttu-id="bceab-118">Actualmente, Azure admite los dos modos de puertas de enlace de VPN: puertas de enlace de VPN basadas en directivas y puertas de enlace de VPN basadas en rutas.</span><span class="sxs-lookup"><span data-stu-id="bceab-118">Currently, Azure supports both modes of VPN gateways: route-based VPN gateways and policy-based VPN gateways.</span></span> <span data-ttu-id="bceab-119">Se crean en distintas plataformas internas, lo que da lugar a diferentes especificaciones:</span><span class="sxs-lookup"><span data-stu-id="bceab-119">They are built on different internal platforms, which result in different specifications:</span></span>

|                          | <span data-ttu-id="bceab-120">**Puerta de enlace de VPN PolicyBased**</span><span class="sxs-lookup"><span data-stu-id="bceab-120">**PolicyBased VPN Gateway**</span></span> | <span data-ttu-id="bceab-121">**Puerta de enlace de VPN RouteBased**</span><span class="sxs-lookup"><span data-stu-id="bceab-121">**RouteBased VPN Gateway**</span></span>               |
| ---                      | ---                         | ---                                      |
| <span data-ttu-id="bceab-122">**SKU de puerta de enlace de Azure**</span><span class="sxs-lookup"><span data-stu-id="bceab-122">**Azure Gateway SKU**</span></span>    | <span data-ttu-id="bceab-123">Básica</span><span class="sxs-lookup"><span data-stu-id="bceab-123">Basic</span></span>                       | <span data-ttu-id="bceab-124">Básica, Estándar, HighPerformance</span><span class="sxs-lookup"><span data-stu-id="bceab-124">Basic, Standard, HighPerformance</span></span>         |
| <span data-ttu-id="bceab-125">**Versión de IKE**</span><span class="sxs-lookup"><span data-stu-id="bceab-125">**IKE version**</span></span>          | <span data-ttu-id="bceab-126">IKEv1</span><span class="sxs-lookup"><span data-stu-id="bceab-126">IKEv1</span></span>                       | <span data-ttu-id="bceab-127">IKEv2</span><span class="sxs-lookup"><span data-stu-id="bceab-127">IKEv2</span></span>                                    |
| <span data-ttu-id="bceab-128">**Máx. de conexiones de sitio a sitio**</span><span class="sxs-lookup"><span data-stu-id="bceab-128">**Max. S2S connections**</span></span> | <span data-ttu-id="bceab-129">**1**</span><span class="sxs-lookup"><span data-stu-id="bceab-129">**1**</span></span>                       | <span data-ttu-id="bceab-130">Básica o Estándar: 10</span><span class="sxs-lookup"><span data-stu-id="bceab-130">Basic/Standard: 10</span></span><br> <span data-ttu-id="bceab-131">HighPerformance: 30</span><span class="sxs-lookup"><span data-stu-id="bceab-131">HighPerformance: 30</span></span> |
|                          |                             |                                          |

<span data-ttu-id="bceab-132">Con la directiva de IPsec/IKE personalizada hello, ahora puede configurar Azure basadas en enrutamiento VPN puertas de enlace toouse tráfico basado en prefijo selectores con la opción "**PolicyBasedTrafficSelectors**", tooconnect tooon local basada en directivas de los dispositivos VPN.</span><span class="sxs-lookup"><span data-stu-id="bceab-132">With hello custom IPsec/IKE policy, you can now configure Azure route-based VPN gateways toouse prefix-based traffic selectors with option "**PolicyBasedTrafficSelectors**", tooconnect tooon-premises policy-based VPN devices.</span></span> <span data-ttu-id="bceab-133">Esta funcionalidad le permite tooconnect de red virtual de Azure y toomultiple de puerta de enlace VPN dispositivos VPN/firewall basada en directivas, quitar el límite de conexión única Hola de hello actuales Azure basada en directivas con puertas de enlace VPN local.</span><span class="sxs-lookup"><span data-stu-id="bceab-133">This capability allows you tooconnect from an Azure virtual network and VPN gateway toomultiple on-premises policy-based VPN/firewall devices, removing hello single connection limit from hello current Azure policy-based VPN gateways.</span></span>

> [!IMPORTANT]
> 1. <span data-ttu-id="bceab-134">tooenable esta conectividad, deben admitir los dispositivos VPN basada en directivas locales **IKEv2** tooconnect toohello Azure basadas en enrutamiento puertas de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="bceab-134">tooenable this connectivity, your on-premises policy-based VPN devices must support **IKEv2** tooconnect toohello Azure route-based VPN gateways.</span></span> <span data-ttu-id="bceab-135">Compruebe las especificaciones del dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="bceab-135">Check your VPN device specifications.</span></span>
> 2. <span data-ttu-id="bceab-136">redes locales de Hello conexión a través de los dispositivos VPN basada en directivas con este mecanismo solo pueden conectar toohello red virtual de Azure; **no están en tránsito redes locales de tooother o redes virtuales a través de bienvenida la misma puerta de enlace de VPN de Azure**.</span><span class="sxs-lookup"><span data-stu-id="bceab-136">hello on-premises networks connecting through policy-based VPN devices with this mechanism can only connect toohello Azure virtual network; **they cannot transit tooother on-premises networks or virtual networks via hello same Azure VPN gateway**.</span></span>
> 3. <span data-ttu-id="bceab-137">opción de configuración de Hello es parte de la directiva de conexión de IPsec/IKE personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="bceab-137">hello configuration option is part of hello custom IPsec/IKE connection policy.</span></span> <span data-ttu-id="bceab-138">Si habilita la opción de selector de hello tráfico basada en directivas, debe especificar la directiva completa de hello (algoritmos de cifrado e integridad de IPsec/IKE, ventajas claves y vigencias de SA).</span><span class="sxs-lookup"><span data-stu-id="bceab-138">If you enable hello policy-based traffic selector option, you must specify hello complete policy (IPsec/IKE encryption and integrity algorithms, key strengths, and SA lifetimes).</span></span>

<span data-ttu-id="bceab-139">Hola siguiente diagrama muestra por qué el enrutamiento del tránsito a través de puerta de enlace VPN de Azure no funciona con la opción de hello basada en directivas:</span><span class="sxs-lookup"><span data-stu-id="bceab-139">hello following diagram shows why transit routing via Azure VPN gateway doesn't work with hello policy-based option:</span></span>

![tránsito basado en directivas](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

<span data-ttu-id="bceab-141">Tal y como se muestra en el diagrama de hello, puerta de enlace de VPN de Azure de hello tiene selectores de tráfico de hello tooeach de red virtual de los prefijos de red local hello, pero no los prefijos de las conexiones entre Hola.</span><span class="sxs-lookup"><span data-stu-id="bceab-141">As shown in hello diagram, hello Azure VPN gateway has traffic selectors from hello virtual network tooeach of hello on-premises network prefixes, but not hello cross-connection prefixes.</span></span> <span data-ttu-id="bceab-142">Por ejemplo, el sitio local 2, sitio 3 y 4 pueden cada comunican tooVNet1 respectivamente, pero no se pueden conectar a través de hello Azure VPN gateway tooeach otros.</span><span class="sxs-lookup"><span data-stu-id="bceab-142">For example, on-premises site 2, site 3, and site 4 can each communicate tooVNet1 respectively, but cannot connect via hello Azure VPN gateway tooeach other.</span></span> <span data-ttu-id="bceab-143">diagrama de Hello muestra hello selectores de tráfico que no están disponibles en la puerta de enlace de VPN de Azure de hello en esta configuración de conexión cruzada.</span><span class="sxs-lookup"><span data-stu-id="bceab-143">hello diagram shows hello cross-connect traffic selectors that are not available in hello Azure VPN gateway under this configuration.</span></span>

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="bceab-144">Configuración de los selectores de tráfico basados en directivas en una conexión</span><span class="sxs-lookup"><span data-stu-id="bceab-144">Configure policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="bceab-145">Hello instrucciones de este artículo, siga Hola mismo ejemplo tal y como se describe en [directiva configurar IPsec/IKE para las conexiones de S2S o red virtual a red virtual](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish una conexión VPN de S2S.</span><span class="sxs-lookup"><span data-stu-id="bceab-145">hello instructions in this article follow hello same example as described in [Configure IPsec/IKE policy for S2S or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish a S2S VPN connection.</span></span> <span data-ttu-id="bceab-146">Esto se muestra en hello siguiente diagrama:</span><span class="sxs-lookup"><span data-stu-id="bceab-146">This is shown in hello following diagram:</span></span>

![s2s-policy](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

<span data-ttu-id="bceab-148">Hola tooenable de flujo de trabajo esta conectividad:</span><span class="sxs-lookup"><span data-stu-id="bceab-148">hello workflow tooenable this connectivity:</span></span>
1. <span data-ttu-id="bceab-149">Crear red virtual de hello, la puerta de enlace VPN y la puerta de enlace de red local para la conexión entre entornos</span><span class="sxs-lookup"><span data-stu-id="bceab-149">Create hello virtual network, VPN gateway, and local network gateway for your cross-premises connection</span></span>
2. <span data-ttu-id="bceab-150">Cree una directiva IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="bceab-150">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="bceab-151">Aplicar la directiva de hello cuando se crea una conexión de S2S o red virtual a red virtual, y **habilitar selectores de tráfico basado en directiva de hello** en conexión Hola</span><span class="sxs-lookup"><span data-stu-id="bceab-151">Apply hello policy when you create a S2S or VNet-to-VNet connection, and **enable hello policy-based traffic selectors** on hello connection</span></span>
4. <span data-ttu-id="bceab-152">Si ya se creó la conexión de hello, puede aplicar o actualizar la conexión existente de hello directiva tooan</span><span class="sxs-lookup"><span data-stu-id="bceab-152">If hello connection is already created, you can apply or update hello policy tooan existing connection</span></span>

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="bceab-153">Habilitación de los selectores de tráfico basados en directivas en una conexión</span><span class="sxs-lookup"><span data-stu-id="bceab-153">Enable policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="bceab-154">Asegúrese de que ha completado [parte 3 de artículo de directiva de IPsec/IKE configurar hello](vpn-gateway-ipsecikepolicy-rm-powershell.md) para esta sección.</span><span class="sxs-lookup"><span data-stu-id="bceab-154">Make sure you have completed [Part 3 of hello Configure IPsec/IKE policy article](vpn-gateway-ipsecikepolicy-rm-powershell.md) for this section.</span></span> <span data-ttu-id="bceab-155">Hola siguiendo el ejemplo se utiliza Hola mismos parámetros y pasos:</span><span class="sxs-lookup"><span data-stu-id="bceab-155">hello following example uses hello same parameters and steps:</span></span>

### <a name="step-1---create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="bceab-156">Paso 1: crear la red virtual de hello, la puerta de enlace VPN y la puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="bceab-156">Step 1 - Create hello virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables--connect-tooyour-subscription"></a><span data-ttu-id="bceab-157">1. Declare las variables de & Conectar tooyour suscripción</span><span class="sxs-lookup"><span data-stu-id="bceab-157">1. Declare your variables & connect tooyour subscription</span></span>
<span data-ttu-id="bceab-158">Para este ejercicio, se empieza por declarar las variables.</span><span class="sxs-lookup"><span data-stu-id="bceab-158">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="bceab-159">Ser seguro de valores de hello tooreplace con su propio cuando se configura para la producción.</span><span class="sxs-lookup"><span data-stu-id="bceab-159">Be sure tooreplace hello values with your own when configuring for production.</span></span>

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
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
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```
<span data-ttu-id="bceab-160">Hola toouse cmdlets del Administrador de recursos, asegúrese de cambiar el modo de tooPowerShell.</span><span class="sxs-lookup"><span data-stu-id="bceab-160">toouse hello Resource Manager cmdlets, make sure you switch tooPowerShell mode.</span></span> <span data-ttu-id="bceab-161">Para obtener más información, consulte [Uso de Windows PowerShell con el Administrador de recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="bceab-161">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="bceab-162">Abra la consola de PowerShell y conectar con tooyour cuenta.</span><span class="sxs-lookup"><span data-stu-id="bceab-162">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="bceab-163">Usar hello después toohelp de ejemplo que conectarse:</span><span class="sxs-lookup"><span data-stu-id="bceab-163">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="bceab-164">2. Crear red virtual de hello, la puerta de enlace VPN y la puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="bceab-164">2. Create hello virtual network, VPN gateway, and local network gateway</span></span>
<span data-ttu-id="bceab-165">Hola de ejemplo siguiente crea la red virtual de hello, TestVNet1 con tres subredes y puerta de enlace VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="bceab-165">hello following example creates hello virtual network, TestVNet1 with three subnets, and hello VPN gateway.</span></span> <span data-ttu-id="bceab-166">Al reemplazar valores, es importante que siempre asigne el nombre "GatewaySubnet" a la subred de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="bceab-166">When substituting values, it's important that you always name your gateway subnet specifically 'GatewaySubnet'.</span></span> <span data-ttu-id="bceab-167">Si usa otro, se produce un error al crear la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="bceab-167">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a><span data-ttu-id="bceab-168">Paso 2: Creación de una conexión VPN de sitio a sitio con una directiva IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="bceab-168">Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="bceab-169">1. Cree una directiva IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="bceab-169">1. Create an IPsec/IKE policy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bceab-170">Necesita una directiva de IPsec/IKE en orden tooenable "UsePolicyBasedTrafficSelectors" opción de conexión de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="bceab-170">You need toocreate an IPsec/IKE policy in order tooenable "UsePolicyBasedTrafficSelectors" option on hello connection.</span></span>

<span data-ttu-id="bceab-171">Hello en el ejemplo siguiente se crea una directiva de IPsec/IKE con estos algoritmos y parámetros:</span><span class="sxs-lookup"><span data-stu-id="bceab-171">hello following example creates an IPsec/IKE policy with these algorithms and parameters:</span></span>
* <span data-ttu-id="bceab-172">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="bceab-172">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="bceab-173">IPsec: AES256, SHA256, PFS24, vigencia de SA de 3600 segundos y 2048 KB</span><span class="sxs-lookup"><span data-stu-id="bceab-173">IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a><span data-ttu-id="bceab-174">2. Crear la conexión de VPN de S2S de hello en los selectores de tráfico basada en directivas y la directiva de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="bceab-174">2. Create hello S2S VPN connection with policy-based traffic selectors and IPsec/IKE policy</span></span>
<span data-ttu-id="bceab-175">Crear una conexión VPN de S2S y aplicar la directiva de IPsec/IKE Hola creado en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="bceab-175">Create an S2S VPN connection and apply hello IPsec/IKE policy created in hello previous step.</span></span> <span data-ttu-id="bceab-176">Tenga en cuenta los parámetros adicionales de Hola "-UsePolicyBasedTrafficSelectors $True" lo que permite a los selectores de tráfico basada en directivas en conexión Hola.</span><span class="sxs-lookup"><span data-stu-id="bceab-176">Be aware of hello additional parameter "-UsePolicyBasedTrafficSelectors $True"  which enables policy-based traffic selectors on hello connection.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="bceab-177">Después de completar los pasos de hello, Hola conexión VPN S2S usará Hola directiva IPsec/IKE definida y habilitar a selectores de tráfico basada en directivas en conexión Hola.</span><span class="sxs-lookup"><span data-stu-id="bceab-177">After completing hello steps, hello S2S VPN connection will use hello IPsec/IKE policy defined, and enable policy-based traffic selectors on hello connection.</span></span> <span data-ttu-id="bceab-178">Puede repetir Hola mismo pasos tooadd más conexiones tooadditional basada en directivas VPN dispositivos locales de Hola misma puerta de enlace de VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="bceab-178">You can repeat hello same steps tooadd more connections tooadditional on-premises policy-based VPN devices from hello same Azure VPN gateway.</span></span>

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a><span data-ttu-id="bceab-179">Actualización de los selectores de tráfico basados en directivas para una conexión</span><span class="sxs-lookup"><span data-stu-id="bceab-179">Update policy-based traffic selectors for a connection</span></span>
<span data-ttu-id="bceab-180">Hola última sección muestra cómo los selectores de tráfico basado en directiva de hello tooupdate opción para una conexión VPN de S2S existente.</span><span class="sxs-lookup"><span data-stu-id="bceab-180">hello last section shows you how tooupdate hello policy-based traffic selectors option for an existing  S2S VPN connection.</span></span>

### <a name="1-get-hello-connection"></a><span data-ttu-id="bceab-181">1. Obtener la conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="bceab-181">1. Get hello connection</span></span>
<span data-ttu-id="bceab-182">Obtener el recurso de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="bceab-182">Get hello connection resource.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-hello-policy-based-traffic-selectors-option"></a><span data-ttu-id="bceab-183">2. Hola tráfico basada en directivas selectores opción Check</span><span class="sxs-lookup"><span data-stu-id="bceab-183">2. Check hello policy-based traffic selectors option</span></span>
<span data-ttu-id="bceab-184">Hello la línea siguiente se muestra si se utilizan los selectores de tráfico basado en directiva de Hola para conexión de hello:</span><span class="sxs-lookup"><span data-stu-id="bceab-184">hello following line shows whether hello policy-based traffic selectors are used for hello connection:</span></span>

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

<span data-ttu-id="bceab-185">Si la línea hello devuelve "**True**", a continuación, selectores de tráfico basada en directivas se configuran en la conexión de hello; en caso contrario, devuelve "**False**."</span><span class="sxs-lookup"><span data-stu-id="bceab-185">If hello line returns "**True**", then policy-based traffic selectors are configured on hello connection; otherwise it returns "**False**."</span></span>

### <a name="3-update-hello-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="bceab-186">3. Actualizar los selectores de tráfico basado en directiva de hello en una conexión</span><span class="sxs-lookup"><span data-stu-id="bceab-186">3. Update hello policy-based traffic selectors on a connection</span></span>
<span data-ttu-id="bceab-187">Una vez que obtenga el recurso de conexión de hello, puede habilitar o deshabilitar la opción de Hola.</span><span class="sxs-lookup"><span data-stu-id="bceab-187">Once you obtain hello connection resource, you can enable or disable hello option.</span></span>

#### <a name="disable-usepolicybasedtrafficselectors"></a><span data-ttu-id="bceab-188">Deshabilitación de UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="bceab-188">Disable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="bceab-189">Hello en el ejemplo siguiente se deshabilita la opción de selectores de tráfico basada en directivas de hello, pero deja Hola sin cambios de directiva de IPsec/IKE:</span><span class="sxs-lookup"><span data-stu-id="bceab-189">hello following example disables hello policy-based traffic selectors option, but leaves hello IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a><span data-ttu-id="bceab-190">Habilitación de UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="bceab-190">Enable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="bceab-191">el ejemplo siguiente se Hello permite opción selectores de hello tráfico basada en directivas, pero deja Hola sin cambios de directiva de IPsec/IKE:</span><span class="sxs-lookup"><span data-stu-id="bceab-191">hello following example enables hello policy-based traffic selectors option, but leaves hello IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a><span data-ttu-id="bceab-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bceab-192">Next steps</span></span>
<span data-ttu-id="bceab-193">Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour.</span><span class="sxs-lookup"><span data-stu-id="bceab-193">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="bceab-194">Consulte [Creación de una máquina virtual que ejecuta Windows en el Portal de Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para ver los pasos.</span><span class="sxs-lookup"><span data-stu-id="bceab-194">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>

<span data-ttu-id="bceab-195">Consulte también [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) (Configuración de la directiva IPsec/IKE para conexiones VPN de sitio a sitio o de red virtual a red virtual) para obtener más información sobre las directivas IPsec/IKE personalizadas.</span><span class="sxs-lookup"><span data-stu-id="bceab-195">Also review [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) for more details on custom IPsec/IKE policies.</span></span>
