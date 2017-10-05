---
title: "Conexión de las puertas de enlace Azure VPN Gateway en varios dispositivos VPN locales basados en directivas: Azure Resource Manager: PowerShell | Microsoft Docs"
description: "Este artículo le guiará a través de la configuración de la puerta de enlace Azure VPN Gateway basada en rutas de Azure para varios dispositivos VPN basados en directivas con Azure Resource Manager y PowerShell."
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
ms.openlocfilehash: 17211379ec61891982a02efca6730ca0da87c1ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="connect-azure-vpn-gateways-to-multiple-on-premises-policy-based-vpn-devices-using-powershell"></a><span data-ttu-id="fca47-103">Conexión de puertas de enlace Azure VPN Gateway a varios dispositivos VPN locales basados en directivas con PowerShell</span><span class="sxs-lookup"><span data-stu-id="fca47-103">Connect Azure VPN gateways to multiple on-premises policy-based VPN devices using PowerShell</span></span>

<span data-ttu-id="fca47-104">Este artículo le ayuda a configurar una puerta de enlace de VPN basada en rutas de Azure para conectarse a varios dispositivos VPN locales basados en directivas al aprovechar las directivas IPsec/IKE personalizadas en las conexiones VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="fca47-104">This article helps you configure an Azure route-based VPN gateway to connect to multiple on-premises policy-based VPN devices leveraging custom IPsec/IKE policies on S2S VPN connections.</span></span>

## <a name="about-policy-based-and-route-based-vpn-gateways"></a><span data-ttu-id="fca47-105">Acerca de las puertas de enlace de VPN basadas en directivas y en rutas</span><span class="sxs-lookup"><span data-stu-id="fca47-105">About policy-based and route-based VPN gateways</span></span>

<span data-ttu-id="fca47-106">Los dispositivos VPN basados en directivas *frente* a los basados en rutas se diferencian en la forma en la que se establecen los selectores de tráfico IPsec en una conexión:</span><span class="sxs-lookup"><span data-stu-id="fca47-106">Policy- *vs.* route-based VPN devices differ in how the IPsec traffic selectors are set on a connection:</span></span>

* <span data-ttu-id="fca47-107">Los dispositivos VPN **basados en directivas** usan las combinaciones de prefijos de ambas redes para definir la forma en la que se cifra/descifra el tráfico a través de túneles IPsec.</span><span class="sxs-lookup"><span data-stu-id="fca47-107">**Policy-based** VPN devices use the combinations of prefixes from both networks to define how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="fca47-108">Normalmente se basa en dispositivos de firewall que realizan el filtrado de paquetes.</span><span class="sxs-lookup"><span data-stu-id="fca47-108">It is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="fca47-109">El cifrado y descifrado de túneles IPsec se agregan al motor de procesamiento y al filtrado de paquetes.</span><span class="sxs-lookup"><span data-stu-id="fca47-109">IPsec tunnel encryption and decryption are added to the packet filtering and processing engine.</span></span>
* <span data-ttu-id="fca47-110">Los dispositivos VPN **basados en rutas** usan selectores de tráfico universales (caracteres comodín) y permiten a las tablas de reenvío/enrutamiento dirigir el tráfico a distintos túneles IPsec.</span><span class="sxs-lookup"><span data-stu-id="fca47-110">**Route-based** VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic to different IPsec tunnels.</span></span> <span data-ttu-id="fca47-111">Normalmente se basa en plataformas de enrutador donde cada túnel IPsec se modela como una interfaz de red o VTI (interfaz de túnel virtual).</span><span class="sxs-lookup"><span data-stu-id="fca47-111">It is typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

<span data-ttu-id="fca47-112">Los diagramas siguientes resaltan los dos modelos:</span><span class="sxs-lookup"><span data-stu-id="fca47-112">The following diagrams highlight the two models:</span></span>

### <a name="policy-based-vpn-example"></a><span data-ttu-id="fca47-113">Ejemplo de VPN basada en directivas</span><span class="sxs-lookup"><span data-stu-id="fca47-113">Policy-based VPN example</span></span>
![basada en directivas](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a><span data-ttu-id="fca47-115">Ejemplo de VPN basada en rutas</span><span class="sxs-lookup"><span data-stu-id="fca47-115">Route-based VPN example</span></span>
![basada en rutas](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a><span data-ttu-id="fca47-117">Compatibilidad de Azure con VPN basada en directivas</span><span class="sxs-lookup"><span data-stu-id="fca47-117">Azure support for policy-based VPN</span></span>
<span data-ttu-id="fca47-118">Actualmente, Azure admite los dos modos de puertas de enlace de VPN: puertas de enlace de VPN basadas en directivas y puertas de enlace de VPN basadas en rutas.</span><span class="sxs-lookup"><span data-stu-id="fca47-118">Currently, Azure supports both modes of VPN gateways: route-based VPN gateways and policy-based VPN gateways.</span></span> <span data-ttu-id="fca47-119">Se crean en distintas plataformas internas, lo que da lugar a diferentes especificaciones:</span><span class="sxs-lookup"><span data-stu-id="fca47-119">They are built on different internal platforms, which result in different specifications:</span></span>

|                          | <span data-ttu-id="fca47-120">**Puerta de enlace de VPN PolicyBased**</span><span class="sxs-lookup"><span data-stu-id="fca47-120">**PolicyBased VPN Gateway**</span></span> | <span data-ttu-id="fca47-121">**Puerta de enlace de VPN RouteBased**</span><span class="sxs-lookup"><span data-stu-id="fca47-121">**RouteBased VPN Gateway**</span></span>               |
| ---                      | ---                         | ---                                      |
| <span data-ttu-id="fca47-122">**SKU de puerta de enlace de Azure**</span><span class="sxs-lookup"><span data-stu-id="fca47-122">**Azure Gateway SKU**</span></span>    | <span data-ttu-id="fca47-123">Básica</span><span class="sxs-lookup"><span data-stu-id="fca47-123">Basic</span></span>                       | <span data-ttu-id="fca47-124">Básica, Estándar, HighPerformance</span><span class="sxs-lookup"><span data-stu-id="fca47-124">Basic, Standard, HighPerformance</span></span>         |
| <span data-ttu-id="fca47-125">**Versión de IKE**</span><span class="sxs-lookup"><span data-stu-id="fca47-125">**IKE version**</span></span>          | <span data-ttu-id="fca47-126">IKEv1</span><span class="sxs-lookup"><span data-stu-id="fca47-126">IKEv1</span></span>                       | <span data-ttu-id="fca47-127">IKEv2</span><span class="sxs-lookup"><span data-stu-id="fca47-127">IKEv2</span></span>                                    |
| <span data-ttu-id="fca47-128">**Máx. de conexiones de sitio a sitio**</span><span class="sxs-lookup"><span data-stu-id="fca47-128">**Max. S2S connections**</span></span> | <span data-ttu-id="fca47-129">**1**</span><span class="sxs-lookup"><span data-stu-id="fca47-129">**1**</span></span>                       | <span data-ttu-id="fca47-130">Básica o Estándar: 10</span><span class="sxs-lookup"><span data-stu-id="fca47-130">Basic/Standard: 10</span></span><br> <span data-ttu-id="fca47-131">HighPerformance: 30</span><span class="sxs-lookup"><span data-stu-id="fca47-131">HighPerformance: 30</span></span> |
|                          |                             |                                          |

<span data-ttu-id="fca47-132">Con la directiva IPsec/IKE personalizada, ahora puede configurar puertas de enlace Azure VPN Gateway basadas en rutas para usar selectores de tráfico basados en prefijo con la opción "**PolicyBasedTrafficSelectors**" para conectarse a dispositivos VPN locales basados en directivas.</span><span class="sxs-lookup"><span data-stu-id="fca47-132">With the custom IPsec/IKE policy, you can now configure Azure route-based VPN gateways to use prefix-based traffic selectors with option "**PolicyBasedTrafficSelectors**", to connect to on-premises policy-based VPN devices.</span></span> <span data-ttu-id="fca47-133">Esta capacidad le permite conectarse desde una red virtual de Azure y una puerta de enlace Azure VPN Gateway a varios dispositivos VPN/firewall locales basados en directivas y quitar el límite de conexión único de las actuales puertas de enlace Azure VPN Gateway basadas en directivas.</span><span class="sxs-lookup"><span data-stu-id="fca47-133">This capability allows you to connect from an Azure virtual network and VPN gateway to multiple on-premises policy-based VPN/firewall devices, removing the single connection limit from the current Azure policy-based VPN gateways.</span></span>

> [!IMPORTANT]
> 1. <span data-ttu-id="fca47-134">Para habilitar esta conectividad, los dispositivos VPN locales basados en directivas deben admitir **IKEv2** para conectarse a las puertas de enlace Azure VPN Gateway basadas en rutas.</span><span class="sxs-lookup"><span data-stu-id="fca47-134">To enable this connectivity, your on-premises policy-based VPN devices must support **IKEv2** to connect to the Azure route-based VPN gateways.</span></span> <span data-ttu-id="fca47-135">Compruebe las especificaciones del dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="fca47-135">Check your VPN device specifications.</span></span>
> 2. <span data-ttu-id="fca47-136">Las redes locales que se conectan a través de dispositivos VPN basados en directivas con este mecanismo solo pueden conectarse a la red virtual de Azure; **no se permite el tránsito a otras redes locales o redes virtuales a través de la misma puerta de enlace de VPN de Azure**.</span><span class="sxs-lookup"><span data-stu-id="fca47-136">The on-premises networks connecting through policy-based VPN devices with this mechanism can only connect to the Azure virtual network; **they cannot transit to other on-premises networks or virtual networks via the same Azure VPN gateway**.</span></span>
> 3. <span data-ttu-id="fca47-137">La opción de configuración forma parte de la directiva de conexión IPsec/IKE personalizada.</span><span class="sxs-lookup"><span data-stu-id="fca47-137">The configuration option is part of the custom IPsec/IKE connection policy.</span></span> <span data-ttu-id="fca47-138">Si habilita la opción de selector de tráfico basado en directivas, debe especificar la directiva completa (vigencias de SA, puntos clave, algoritmos de integridad y cifrado IPsec/IKE).</span><span class="sxs-lookup"><span data-stu-id="fca47-138">If you enable the policy-based traffic selector option, you must specify the complete policy (IPsec/IKE encryption and integrity algorithms, key strengths, and SA lifetimes).</span></span>

<span data-ttu-id="fca47-139">El diagrama siguiente muestra por qué el enrutamiento del tránsito a través de la puerta de enlace de VPN de Azure no funciona con la opción basada en directivas:</span><span class="sxs-lookup"><span data-stu-id="fca47-139">The following diagram shows why transit routing via Azure VPN gateway doesn't work with the policy-based option:</span></span>

![tránsito basado en directivas](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

<span data-ttu-id="fca47-141">Como se muestra en el diagrama, la puerta de enlace de VPN de Azure tiene selectores de tráfico desde la red virtual a cada prefijo de red local, pero no a los prefijos de conexión cruzada.</span><span class="sxs-lookup"><span data-stu-id="fca47-141">As shown in the diagram, the Azure VPN gateway has traffic selectors from the virtual network to each of the on-premises network prefixes, but not the cross-connection prefixes.</span></span> <span data-ttu-id="fca47-142">Por ejemplo, los sitios 2, 3 y 4 locales pueden comunicarse con VNet1, pero no se pueden conectar entre sí a través de la puerta de enlace de VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="fca47-142">For example, on-premises site 2, site 3, and site 4 can each communicate to VNet1 respectively, but cannot connect via the Azure VPN gateway to each other.</span></span> <span data-ttu-id="fca47-143">El diagrama muestra los selectores de tráfico de conexión cruzada que no están disponibles en la puerta de enlace Azure VPN Gateway en esta configuración.</span><span class="sxs-lookup"><span data-stu-id="fca47-143">The diagram shows the cross-connect traffic selectors that are not available in the Azure VPN gateway under this configuration.</span></span>

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="fca47-144">Configuración de los selectores de tráfico basados en directivas en una conexión</span><span class="sxs-lookup"><span data-stu-id="fca47-144">Configure policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="fca47-145">Las instrucciones de este artículo siguen el mismo ejemplo de [Configurar una directiva de IPsec o IKE para conexiones VPN de sitio a sitio o de red virtual a red virtual](vpn-gateway-ipsecikepolicy-rm-powershell.md) para establecer una conexión VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="fca47-145">The instructions in this article follow the same example as described in [Configure IPsec/IKE policy for S2S or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) to establish a S2S VPN connection.</span></span> <span data-ttu-id="fca47-146">Se muestra en el diagrama siguiente:</span><span class="sxs-lookup"><span data-stu-id="fca47-146">This is shown in the following diagram:</span></span>

![s2s-policy](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

<span data-ttu-id="fca47-148">El flujo de trabajo para habilitar esta conectividad:</span><span class="sxs-lookup"><span data-stu-id="fca47-148">The workflow to enable this connectivity:</span></span>
1. <span data-ttu-id="fca47-149">Cree la red virtual, la puerta de enlace VPN y la puerta de enlace de red local para la conexión entre locales.</span><span class="sxs-lookup"><span data-stu-id="fca47-149">Create the virtual network, VPN gateway, and local network gateway for your cross-premises connection</span></span>
2. <span data-ttu-id="fca47-150">Cree una directiva IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="fca47-150">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="fca47-151">Aplique la directiva cuando se cree una conexión de sitio a sitio o de red virtual a red virtual, y **habilite los selectores de tráfico basados en directivas** en la conexión.</span><span class="sxs-lookup"><span data-stu-id="fca47-151">Apply the policy when you create a S2S or VNet-to-VNet connection, and **enable the policy-based traffic selectors** on the connection</span></span>
4. <span data-ttu-id="fca47-152">Si ya se ha creado la conexión, puede aplicar la directiva a una conexión existente o actualizarla.</span><span class="sxs-lookup"><span data-stu-id="fca47-152">If the connection is already created, you can apply or update the policy to an existing connection</span></span>

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="fca47-153">Habilitación de los selectores de tráfico basados en directivas en una conexión</span><span class="sxs-lookup"><span data-stu-id="fca47-153">Enable policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="fca47-154">Asegúrese de haber completado la [parte 3 del artículo Configurar una directiva de IPsec o IKE](vpn-gateway-ipsecikepolicy-rm-powershell.md) para esta sección.</span><span class="sxs-lookup"><span data-stu-id="fca47-154">Make sure you have completed [Part 3 of the Configure IPsec/IKE policy article](vpn-gateway-ipsecikepolicy-rm-powershell.md) for this section.</span></span> <span data-ttu-id="fca47-155">El ejemplo siguiente usa los mismos parámetros y pasos:</span><span class="sxs-lookup"><span data-stu-id="fca47-155">The following example uses the same parameters and steps:</span></span>

### <a name="step-1---create-the-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="fca47-156">Paso 1: Creación de la red virtual, la puerta de enlace de VPN y la puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="fca47-156">Step 1 - Create the virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables--connect-to-your-subscription"></a><span data-ttu-id="fca47-157">1. Declaración de las variables y conexión a su suscripción</span><span class="sxs-lookup"><span data-stu-id="fca47-157">1. Declare your variables & connect to your subscription</span></span>
<span data-ttu-id="fca47-158">Para este ejercicio, se empieza por declarar las variables.</span><span class="sxs-lookup"><span data-stu-id="fca47-158">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="fca47-159">Asegúrese de reemplazar los valores por los suyos propios cuando realice la configuración para el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="fca47-159">Be sure to replace the values with your own when configuring for production.</span></span>

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
<span data-ttu-id="fca47-160">Para usar los cmdlets de Resource Manager, asegúrese de cambiar al modo de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fca47-160">To use the Resource Manager cmdlets, make sure you switch to PowerShell mode.</span></span> <span data-ttu-id="fca47-161">Para obtener más información, consulte [Uso de Windows PowerShell con el Administrador de recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="fca47-161">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="fca47-162">Abre la consola de PowerShell y conéctate a tu cuenta.</span><span class="sxs-lookup"><span data-stu-id="fca47-162">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="fca47-163">Use el siguiente ejemplo para ayudarle a conectarse:</span><span class="sxs-lookup"><span data-stu-id="fca47-163">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-the-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="fca47-164">2. Creación de la red virtual, la puerta de enlace de VPN y la puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="fca47-164">2. Create the virtual network, VPN gateway, and local network gateway</span></span>
<span data-ttu-id="fca47-165">En el ejemplo siguiente se crea la red virtual, TestVNet1, con tres subredes y la puerta de enlace de VPN.</span><span class="sxs-lookup"><span data-stu-id="fca47-165">The following example creates the virtual network, TestVNet1 with three subnets, and the VPN gateway.</span></span> <span data-ttu-id="fca47-166">Al reemplazar valores, es importante que siempre asigne el nombre "GatewaySubnet" a la subred de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="fca47-166">When substituting values, it's important that you always name your gateway subnet specifically 'GatewaySubnet'.</span></span> <span data-ttu-id="fca47-167">Si usa otro, se produce un error al crear la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="fca47-167">If you name it something else, your gateway creation fails.</span></span>

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

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a><span data-ttu-id="fca47-168">Paso 2: Creación de una conexión VPN de sitio a sitio con una directiva IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="fca47-168">Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="fca47-169">1. Cree una directiva IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="fca47-169">1. Create an IPsec/IKE policy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fca47-170">Debe crear una directiva IPsec/IKE para habilitar la opción "UsePolicyBasedTrafficSelectors" en la conexión.</span><span class="sxs-lookup"><span data-stu-id="fca47-170">You need to create an IPsec/IKE policy in order to enable "UsePolicyBasedTrafficSelectors" option on the connection.</span></span>

<span data-ttu-id="fca47-171">El ejemplo siguiente crea una directiva IPsec/IKE con estos algoritmos y parámetros:</span><span class="sxs-lookup"><span data-stu-id="fca47-171">The following example creates an IPsec/IKE policy with these algorithms and parameters:</span></span>
* <span data-ttu-id="fca47-172">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="fca47-172">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="fca47-173">IPsec: AES256, SHA256, PFS24, vigencia de SA de 3600 segundos y 2048 KB</span><span class="sxs-lookup"><span data-stu-id="fca47-173">IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-the-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a><span data-ttu-id="fca47-174">2. Creación de una conexión VPN de sitio a sitio con selectores de tráfico basados en directivas y directiva IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="fca47-174">2. Create the S2S VPN connection with policy-based traffic selectors and IPsec/IKE policy</span></span>
<span data-ttu-id="fca47-175">Cree una conexión VPN de sitio a sitio y aplique la directiva IPsec/IKE creada en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="fca47-175">Create an S2S VPN connection and apply the IPsec/IKE policy created in the previous step.</span></span> <span data-ttu-id="fca47-176">Tenga en cuenta el parámetro adicional "-UsePolicyBasedTrafficSelectors $True", que habilita los selectores de tráfico basados en directivas en la conexión.</span><span class="sxs-lookup"><span data-stu-id="fca47-176">Be aware of the additional parameter "-UsePolicyBasedTrafficSelectors $True"  which enables policy-based traffic selectors on the connection.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="fca47-177">Después de completar los pasos, la conexión VPN de sitio a sitio usará la directiva IPsec/IKE definida y habilitará los selectores de tráfico basados en directivas en la conexión.</span><span class="sxs-lookup"><span data-stu-id="fca47-177">After completing the steps, the S2S VPN connection will use the IPsec/IKE policy defined, and enable policy-based traffic selectors on the connection.</span></span> <span data-ttu-id="fca47-178">Puede repetir los mismos pasos para agregar más conexiones a los dispositivos VPN locales adicionales basados en directivas desde la misma puerta de enlace Azure VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="fca47-178">You can repeat the same steps to add more connections to additional on-premises policy-based VPN devices from the same Azure VPN gateway.</span></span>

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a><span data-ttu-id="fca47-179">Actualización de los selectores de tráfico basados en directivas para una conexión</span><span class="sxs-lookup"><span data-stu-id="fca47-179">Update policy-based traffic selectors for a connection</span></span>
<span data-ttu-id="fca47-180">La última sección muestra cómo actualizar la opción de selectores de tráfico basados en directivas para una conexión VPN de sitio a sitio existente.</span><span class="sxs-lookup"><span data-stu-id="fca47-180">The last section shows you how to update the policy-based traffic selectors option for an existing  S2S VPN connection.</span></span>

### <a name="1-get-the-connection"></a><span data-ttu-id="fca47-181">1. Obtención de la conexión</span><span class="sxs-lookup"><span data-stu-id="fca47-181">1. Get the connection</span></span>
<span data-ttu-id="fca47-182">Obtenga el recurso de conexión.</span><span class="sxs-lookup"><span data-stu-id="fca47-182">Get the connection resource.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-the-policy-based-traffic-selectors-option"></a><span data-ttu-id="fca47-183">2. Comprobación de la opción de selectores de tráfico basados en directivas</span><span class="sxs-lookup"><span data-stu-id="fca47-183">2. Check the policy-based traffic selectors option</span></span>
<span data-ttu-id="fca47-184">La siguiente línea muestra si se usan los selectores de tráfico basados en directivas para la conexión:</span><span class="sxs-lookup"><span data-stu-id="fca47-184">The following line shows whether the policy-based traffic selectors are used for the connection:</span></span>

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

<span data-ttu-id="fca47-185">Si la línea devuelve "**True**", los selectores de tráfico basados en directivas están configurados en la conexión; en caso contrario, devuelve "**False**".</span><span class="sxs-lookup"><span data-stu-id="fca47-185">If the line returns "**True**", then policy-based traffic selectors are configured on the connection; otherwise it returns "**False**."</span></span>

### <a name="3-update-the-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="fca47-186">3. Actualización de los selectores de tráfico basados en directivas en una conexión</span><span class="sxs-lookup"><span data-stu-id="fca47-186">3. Update the policy-based traffic selectors on a connection</span></span>
<span data-ttu-id="fca47-187">Una vez que obtenga el recurso de conexión, puede habilitar o deshabilitar la opción.</span><span class="sxs-lookup"><span data-stu-id="fca47-187">Once you obtain the connection resource, you can enable or disable the option.</span></span>

#### <a name="disable-usepolicybasedtrafficselectors"></a><span data-ttu-id="fca47-188">Deshabilitación de UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="fca47-188">Disable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="fca47-189">En el ejemplo siguiente se deshabilita la opción de selectores de tráfico basados en directivas, pero se deja sin modificar la directiva IPsec/IKE:</span><span class="sxs-lookup"><span data-stu-id="fca47-189">The following example disables the policy-based traffic selectors option, but leaves the IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a><span data-ttu-id="fca47-190">Habilitación de UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="fca47-190">Enable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="fca47-191">En el ejemplo siguiente se habilita la opción de selectores de tráfico basados en directivas y se deja sin modificar la directiva IPsec/IKE:</span><span class="sxs-lookup"><span data-stu-id="fca47-191">The following example enables the policy-based traffic selectors option, but leaves the IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a><span data-ttu-id="fca47-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fca47-192">Next steps</span></span>
<span data-ttu-id="fca47-193">Una vez completada la conexión, puede agregar máquinas virtuales a las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="fca47-193">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="fca47-194">Consulte [Creación de una máquina virtual que ejecuta Windows en el Portal de Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para ver los pasos.</span><span class="sxs-lookup"><span data-stu-id="fca47-194">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>

<span data-ttu-id="fca47-195">Consulte también [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) (Configuración de la directiva IPsec/IKE para conexiones VPN de sitio a sitio o de red virtual a red virtual) para obtener más información sobre las directivas IPsec/IKE personalizadas.</span><span class="sxs-lookup"><span data-stu-id="fca47-195">Also review [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) for more details on custom IPsec/IKE policies.</span></span>
