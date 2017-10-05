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
ms.openlocfilehash: a9f71b566ffdb163f95634835f64589a700d712f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a><span data-ttu-id="360a9-103">Configuración de conexiones VPN S2S activo-activo con Azure VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="360a9-103">Configure active-active S2S VPN connections with Azure VPN Gateways</span></span>

<span data-ttu-id="360a9-104">Este artículo le guiará por los pasos para crear conexiones activo-activo entre entornos locales y de red virtual a red virtual mediante el modelo de implementación de Resource Manager y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="360a9-104">This article walks you through the steps to create active-active cross-premises and VNet-to-VNet connections using the Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-highly-available-cross-premises-connections"></a><span data-ttu-id="360a9-105">Acerca de las conexiones entre entornos locales de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="360a9-105">About Highly Available Cross-Premises Connections</span></span>
<span data-ttu-id="360a9-106">Para lograr una alta disponibilidad en la conectividad de red virtual a red virtual y entre entornos locales, debe implementar varias puertas de enlace VPN y establecer varias conexiones en paralelo entre sus redes y Azure.</span><span class="sxs-lookup"><span data-stu-id="360a9-106">To achieve high availability for cross-premises and VNet-to-VNet connectivity, you should deploy multiple VPN gateways and establish multiple parallel connections between your networks and Azure.</span></span> <span data-ttu-id="360a9-107">Consulte [Conectividad de alta disponibilidad entre locales y de red virtual a red virtual](vpn-gateway-highlyavailable.md) para información general de las opciones de conectividad y la topología.</span><span class="sxs-lookup"><span data-stu-id="360a9-107">Please see [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) for an overview of connectivity options and topology.</span></span>

<span data-ttu-id="360a9-108">Este artículo proporciona instrucciones para configurar una conexión VPN activo-activo entre entornos locales, y una conexión activo-activo entre dos redes virtuales:</span><span class="sxs-lookup"><span data-stu-id="360a9-108">This article provides the instructions to set up an active-active cross-premises VPN connection, and active-active connection between two virtual networks:</span></span>

* [<span data-ttu-id="360a9-109">Parte 1: Creación y configuración de Azure VPN Gateway en el modo activo-activo</span><span class="sxs-lookup"><span data-stu-id="360a9-109">Part 1 - Create and configure your Azure VPN gateway in active-active mode</span></span>](#aagateway)
* [<span data-ttu-id="360a9-110">Parte 2: Establecimiento de conexiones activo-activo entre entornos locales</span><span class="sxs-lookup"><span data-stu-id="360a9-110">Part 2 - Establish active-active cross-premises connections</span></span>](#aacrossprem)
* [<span data-ttu-id="360a9-111">Parte 3: Establecimiento de conexiones activo-activo de red virtual a red virtual</span><span class="sxs-lookup"><span data-stu-id="360a9-111">Part 3 - Establish active-active VNet-to-VNet connections</span></span>](#aav2v)
* [<span data-ttu-id="360a9-112">Parte 4: Actualización de una puerta de enlace existente entre activo-activo y activo-en espera</span><span class="sxs-lookup"><span data-stu-id="360a9-112">Part 4 - Update existing gateway between active-active and active-standby</span></span>](#aaupdate)

<span data-ttu-id="360a9-113">Puede combinar todos estos elementos para crear una red más compleja de alta disponibilidad que satisfaga sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="360a9-113">You can combine these together to build a more complex, highly available network topology that meets your needs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="360a9-114">Tenga en cuenta que el modo activo / activo usa sólo las SKU siguientes:</span><span class="sxs-lookup"><span data-stu-id="360a9-114">Please note that the active-active mode uses only the following SKUs:</span></span> 
  * <span data-ttu-id="360a9-115">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="360a9-115">VpnGw1, VpnGw2, VpnGw3</span></span>
  * <span data-ttu-id="360a9-116">Alto rendimiento (para SKU heredadas anteriores)</span><span class="sxs-lookup"><span data-stu-id="360a9-116">HighPerformance (for old legacy SKUs)</span></span>
> 
> 

## <span data-ttu-id="360a9-117"><a name ="aagateway"></a>Parte 1: Creación y configuración de puertas de enlace VPN activo-activo</span><span class="sxs-lookup"><span data-stu-id="360a9-117"><a name ="aagateway"></a>Part 1 - Create and configure active-active VPN gateways</span></span>
<span data-ttu-id="360a9-118">Los pasos a continuación configurarán Azure VPN Gateway en modos activo-activo.</span><span class="sxs-lookup"><span data-stu-id="360a9-118">The following steps will configure your Azure VPN gateway in active-active modes.</span></span> <span data-ttu-id="360a9-119">Las diferencias clave entre las puertas de enlace activo-activo y activo-en espera:</span><span class="sxs-lookup"><span data-stu-id="360a9-119">The key differences between the active-active and active-standby gateways:</span></span>

* <span data-ttu-id="360a9-120">Tiene que crear dos configuraciones de IP de puerta de enlace con dos direcciones IP públicas</span><span class="sxs-lookup"><span data-stu-id="360a9-120">You need to create two Gateway IP configurations with two public IP addresses</span></span>
* <span data-ttu-id="360a9-121">Tiene que establecer la marca EnableActiveActiveFeature</span><span class="sxs-lookup"><span data-stu-id="360a9-121">You need set the EnableActiveActiveFeature flag</span></span>
* <span data-ttu-id="360a9-122">La SKU de puerta de enlace debe ser VpnGw1, VpnGw2, VpnGw3 o HighPerformance (SKU heredada).</span><span class="sxs-lookup"><span data-stu-id="360a9-122">The gateway SKU must be VpnGw1, VpnGw2, VpnGw3, or HighPerformance (legacy SKU).</span></span>

<span data-ttu-id="360a9-123">Las demás propiedades son las mismas que las de las puertas de enlace que no son activo-activo.</span><span class="sxs-lookup"><span data-stu-id="360a9-123">The other properties are the same as the non-active-active gateways.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="360a9-124">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="360a9-124">Before you begin</span></span>
* <span data-ttu-id="360a9-125">Compruebe que tiene una suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="360a9-125">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="360a9-126">Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="360a9-126">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="360a9-127">Necesitará instalar los cmdlets de PowerShell del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="360a9-127">You'll need to install the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="360a9-128">Vea [Información general sobre Azure PowerShell](/powershell/azure/overview) para obtener más información sobre la instalación de los cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="360a9-128">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span>

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="360a9-129">Paso 1: Creación y configuración de VNet1</span><span class="sxs-lookup"><span data-stu-id="360a9-129">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="360a9-130">1. Declaración de las variables</span><span class="sxs-lookup"><span data-stu-id="360a9-130">1. Declare your variables</span></span>
<span data-ttu-id="360a9-131">Para este ejercicio, comenzaremos declarando las variables.</span><span class="sxs-lookup"><span data-stu-id="360a9-131">For this exercise, we'll start by declaring our variables.</span></span> <span data-ttu-id="360a9-132">En el ejemplo siguiente, se declaran las variables con los valores para este ejercicio.</span><span class="sxs-lookup"><span data-stu-id="360a9-132">The example below declares the variables using the values for this exercise.</span></span> <span data-ttu-id="360a9-133">Asegúrese de reemplazar los valores por los suyos propios cuando realice la configuración para el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="360a9-133">Be sure to replace the values with your own when configuring for production.</span></span> <span data-ttu-id="360a9-134">Puede usar estas variables si está practicando los pasos para familiarizarse con este tipo de configuración.</span><span class="sxs-lookup"><span data-stu-id="360a9-134">You can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="360a9-135">Modifique las variables y después copie y pegue todo en la consola de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="360a9-135">Modify the variables, and then copy and paste into your PowerShell console.</span></span>

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

#### <a name="2-connect-to-your-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="360a9-136">2. Conexión a su suscripción y creación de un nuevo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="360a9-136">2. Connect to your subscription and create a new resource group</span></span>
<span data-ttu-id="360a9-137">Asegúrese de cambiar el modo de PowerShell para que use los cmdlets del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="360a9-137">Make sure you switch to PowerShell mode to use the Resource Manager cmdlets.</span></span> <span data-ttu-id="360a9-138">Para obtener más información, consulte [Uso de Windows PowerShell con el Administrador de recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="360a9-138">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="360a9-139">Abre la consola de PowerShell y conéctate a tu cuenta.</span><span class="sxs-lookup"><span data-stu-id="360a9-139">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="360a9-140">Use el siguiente ejemplo para ayudarle a conectarse:</span><span class="sxs-lookup"><span data-stu-id="360a9-140">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="360a9-141">3. Creación de TestVNet1</span><span class="sxs-lookup"><span data-stu-id="360a9-141">3. Create TestVNet1</span></span>
<span data-ttu-id="360a9-142">En el ejemplo siguiente se crea una red virtual denominada TestVNet1 y tres subredes llamadas: GatewaySubnet, FrontEnd y Backend.</span><span class="sxs-lookup"><span data-stu-id="360a9-142">The sample below creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="360a9-143">Al reemplazar valores, es importante que siempre asigne el nombre GatewaySubnet a la subred de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="360a9-143">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="360a9-144">Si usa otro, se producirá un error al crear la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="360a9-144">If you name it something else, your gateway creation will fail.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-the-vpn-gateway-for-testvnet1-with-active-active-mode"></a><span data-ttu-id="360a9-145">Paso 2: Creación de la puerta de enlace de VPN para TestVNet1 con modo activo-activo</span><span class="sxs-lookup"><span data-stu-id="360a9-145">Step 2 - Create the VPN gateway for TestVNet1 with active-active mode</span></span>
#### <a name="1-create-the-public-ip-addresses-and-gateway-ip-configurations"></a><span data-ttu-id="360a9-146">1. Creación de las configuraciones de direcciones de IP públicas y la IP de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="360a9-146">1. Create the public IP addresses and gateway IP configurations</span></span>
<span data-ttu-id="360a9-147">Solicite que se asignen dos direcciones IP públicas a la puerta de enlace que creará para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="360a9-147">Request two public IP addresses to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="360a9-148">También definirá las configuraciones de subred y de IP necesarias.</span><span class="sxs-lookup"><span data-stu-id="360a9-148">You'll also define the subnet and IP configurations required.</span></span>

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-the-vpn-gateway-with-active-active-configuration"></a><span data-ttu-id="360a9-149">2. Creación de la puerta de enlace VPN con una configuración activo-activo</span><span class="sxs-lookup"><span data-stu-id="360a9-149">2. Create the VPN gateway with active-active configuration</span></span>
<span data-ttu-id="360a9-150">Cree la puerta de enlace de red virtual para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="360a9-150">Create the virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="360a9-151">Tenga en cuenta que hay dos entradas de GatewayIpConfig y la marca EnableActiveActiveFeature está establecida.</span><span class="sxs-lookup"><span data-stu-id="360a9-151">Note that there are two GatewayIpConfig entries, and the EnableActiveActiveFeature flag is set.</span></span> <span data-ttu-id="360a9-152">Se tardan unos 45 minutos o algo más en crear una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="360a9-152">Creating a gateway can take a while (45 minutes or more to complete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-the-gateway-public-ip-addresses-and-the-bgp-peer-ip-address"></a><span data-ttu-id="360a9-153">3. Obtención de las direcciones IP públicas de puerta de enlace y la dirección IP del par BGP</span><span class="sxs-lookup"><span data-stu-id="360a9-153">3. Obtain the gateway public IP addresses and the BGP Peer IP address</span></span>
<span data-ttu-id="360a9-154">Una vez creada la puerta de enlace, debe obtener la dirección IP del par BGP en la puerta de enlace de VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="360a9-154">Once the gateway is created, you will need to obtain the BGP Peer IP address on the Azure VPN Gateway.</span></span> <span data-ttu-id="360a9-155">Esta dirección es necesaria para configurar la puerta de enlace de VPN de Azure como par BGP para los dispositivos de VPN local.</span><span class="sxs-lookup"><span data-stu-id="360a9-155">This address is needed to configure the Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

<span data-ttu-id="360a9-156">Use los siguientes cmdlets para mostrar las dos direcciones IP públicas asignadas a la puerta de enlace VPN y sus correspondientes direcciones IP del par BGP para cada instancia de puerta de enlace:</span><span class="sxs-lookup"><span data-stu-id="360a9-156">Use the following cmdlets to show the two public IP addresses allocated for your VPN gateway, and their corresponding BGP Peer IP addresses for each gateway instance:</span></span>

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

<span data-ttu-id="360a9-157">El orden de las direcciones IP públicas para las instancias de puerta de enlace y las direcciones de emparejamiento BGP correspondiente es el mismo.</span><span class="sxs-lookup"><span data-stu-id="360a9-157">The order of the public IP addresses for the gateway instances and the corresponding BGP Peering Addresses are the same.</span></span> <span data-ttu-id="360a9-158">En este ejemplo, la máquina virtual de la puerta de enlace con la IP pública 40.112.190.5 utilizará 10.12.255.4 como su dirección de emparejamiento BGP y la puerta de enlace con 138.91.156.129 usará 10.12.255.5.</span><span class="sxs-lookup"><span data-stu-id="360a9-158">In this example, the gateway VM with public IP of 40.112.190.5 will use 10.12.255.4 as its BGP Peering Address, and the gateway with 138.91.156.129 will use 10.12.255.5.</span></span> <span data-ttu-id="360a9-159">Esta información es necesaria cuando configura los dispositivos VPN locales en conexión con la puerta de enlace activo-activo.</span><span class="sxs-lookup"><span data-stu-id="360a9-159">This information is needed when you set up your on premises VPN devices connecting to the active-active gateway.</span></span> <span data-ttu-id="360a9-160">La puerta de enlace se muestra en el diagrama siguiente con todas las direcciones:</span><span class="sxs-lookup"><span data-stu-id="360a9-160">The gateway is shown in the diagram below with all addresses:</span></span>

![puerta de enlace activo-activo](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

<span data-ttu-id="360a9-162">Una vez creada la puerta de enlace, puede usarla para establecer conexión activo-activo entre entornos locales o de red virtual a red virtual.</span><span class="sxs-lookup"><span data-stu-id="360a9-162">Once the gateway is created, you can use this gateway to establish active-active cross-premises or VNet-to-VNet connection.</span></span> <span data-ttu-id="360a9-163">Las siguientes secciones le guiarán por los pasos necesarios para completar el ejercicio.</span><span class="sxs-lookup"><span data-stu-id="360a9-163">The following sections will walk through the steps to complete the exercise.</span></span>

## <span data-ttu-id="360a9-164"><a name ="aacrossprem"></a>Parte 2: Establecimiento de una conexión activo-activo entre entornos locales</span><span class="sxs-lookup"><span data-stu-id="360a9-164"><a name ="aacrossprem"></a>Part 2 - Establish an active-active cross-premises connection</span></span>
<span data-ttu-id="360a9-165">Para establecer una conexión entre locales, debe crear una puerta de enlace de red local para representar el dispositivo VPN local y una conexión para conectarse a la puerta de enlace de VPN de Azure con la puerta de enlace de red local.</span><span class="sxs-lookup"><span data-stu-id="360a9-165">To establish a cross-premises connection, you need to create a Local Network Gateway to represent your on-premises VPN device, and a Connection to connect the Azure VPN gateway with the local network gateway.</span></span> <span data-ttu-id="360a9-166">En este ejemplo, la instancia de Azure VPN Gateway está en modo activo-activo.</span><span class="sxs-lookup"><span data-stu-id="360a9-166">In this example, the Azure VPN gateway is in active-active mode.</span></span> <span data-ttu-id="360a9-167">Como resultado, aunque hay solo un dispositivo VPN local (puerta de enlace de red local) y un recurso de conexión, ambas instancias de Azure VPN Gateway establecerán túneles VPN de S2S con el dispositivo local.</span><span class="sxs-lookup"><span data-stu-id="360a9-167">As a result, even though there is only one on-premises VPN device (local network gateway) and one connection resource, both Azure VPN gateway instances will establish S2S VPN tunnels with the on-premises device.</span></span>

<span data-ttu-id="360a9-168">Antes de continuar, asegúrese de que ha completado la [parte 1](#aagateway) de este ejercicio.</span><span class="sxs-lookup"><span data-stu-id="360a9-168">Before proceeding, please make sure you have completed [Part 1](#aagateway) of this exercise.</span></span>

### <a name="step-1---create-and-configure-the-local-network-gateway"></a><span data-ttu-id="360a9-169">Paso 1: Cree y configure la puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="360a9-169">Step 1 - Create and configure the local network gateway</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="360a9-170">1. Declaración de las variables</span><span class="sxs-lookup"><span data-stu-id="360a9-170">1. Declare your variables</span></span>
<span data-ttu-id="360a9-171">Este ejercicio continuará generando la configuración mostrada en el diagrama.</span><span class="sxs-lookup"><span data-stu-id="360a9-171">This exercise will continue to build the configuration shown in the diagram.</span></span> <span data-ttu-id="360a9-172">Asegúrese de reemplazar los valores por los que desea usar para su configuración.</span><span class="sxs-lookup"><span data-stu-id="360a9-172">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

<span data-ttu-id="360a9-173">Un par de cosas a tener en cuenta con respecto a los parámetros de la puerta de enlace de red local:</span><span class="sxs-lookup"><span data-stu-id="360a9-173">A couple of things to note regarding the local network gateway parameters:</span></span>

* <span data-ttu-id="360a9-174">La puerta de enlace de red local puede estar en la misma ubicación y grupo de recursos que la puerta de enlace de VPN o en otros distintos.</span><span class="sxs-lookup"><span data-stu-id="360a9-174">The local network gateway can be in the same or different location and resource group as the VPN gateway.</span></span> <span data-ttu-id="360a9-175">Este ejemplo los muestra en distintos grupos de recursos pero en la misma ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="360a9-175">This example shows them in different resource groups but in the same Azure location.</span></span>
* <span data-ttu-id="360a9-176">Si hay un único dispositivo VPN local como se muestra anteriormente, la conexión activo-activo puede trabajar con o sin el protocolo BGP.</span><span class="sxs-lookup"><span data-stu-id="360a9-176">If there is only one on-premises VPN device as shown above, the active-active connection can work with or without BGP protocol.</span></span> <span data-ttu-id="360a9-177">Este ejemplo utiliza BGP para la conexión entre redes locales.</span><span class="sxs-lookup"><span data-stu-id="360a9-177">This example uses BGP for the cross-premises connection.</span></span>
* <span data-ttu-id="360a9-178">Si BGP está habilitado el prefijo que debe declarar para la puerta de enlace de red local es la dirección del host de la dirección IP del par BGP en el dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="360a9-178">If BGP is enabled, the prefix you need to declare for the local network gateway is the host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="360a9-179">En este caso, es un prefijo /32 de "10.52.255.253/32".</span><span class="sxs-lookup"><span data-stu-id="360a9-179">In this case, it's a /32 prefix of "10.52.255.253/32".</span></span>
* <span data-ttu-id="360a9-180">Como recordatorio, debe usar diferentes ASN de BGP entre las redes locales y la red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="360a9-180">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="360a9-181">Si son iguales, tiene que cambiar el ASN de la red virtual si el dispositivo VPN local ya utiliza el ASN para emparejarse con otros vecinos de BGP.</span><span class="sxs-lookup"><span data-stu-id="360a9-181">If they are the same, you need to change your VNet ASN if your on-premises VPN device already uses the ASN to peer with other BGP neighbors.</span></span>

#### <a name="2-create-the-local-network-gateway-for-site5"></a><span data-ttu-id="360a9-182">2. Cree las puertas de enlace de red local para Site5</span><span class="sxs-lookup"><span data-stu-id="360a9-182">2. Create the local network gateway for Site5</span></span>
<span data-ttu-id="360a9-183">Antes de continuar, asegúrese de que sigue conectado a la suscripción 1.</span><span class="sxs-lookup"><span data-stu-id="360a9-183">Before you continue, please make sure you are still connected to Subscription 1.</span></span> <span data-ttu-id="360a9-184">Cree el grupo de recursos si aún no se ha creado.</span><span class="sxs-lookup"><span data-stu-id="360a9-184">Create the resource group if it is not yet created.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-the-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="360a9-185">Paso 2: Conecte la puerta de enlace de red virtual y la puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="360a9-185">Step 2 - Connect the VNet gateway and local network gateway</span></span>
#### <a name="1-get-the-two-gateways"></a><span data-ttu-id="360a9-186">1. Obtenga las dos puertas de enlace</span><span class="sxs-lookup"><span data-stu-id="360a9-186">1. Get the two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-the-testvnet1-to-site5-connection"></a><span data-ttu-id="360a9-187">2. Cree la conexión de TestVNet1 a Site5</span><span class="sxs-lookup"><span data-stu-id="360a9-187">2. Create the TestVNet1 to Site5 connection</span></span>
<span data-ttu-id="360a9-188">En este paso, creará la conexión de TestVNet1 a Site5_1 con "EnableBGP" establecido como $True.</span><span class="sxs-lookup"><span data-stu-id="360a9-188">In this step, you will create the connection from TestVNet1 to Site5_1 with "EnableBGP" set to $True.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a><span data-ttu-id="360a9-189">3. Parámetros VPN y BGP para el dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="360a9-189">3. VPN and BGP parameters for your on-premises VPN device</span></span>
<span data-ttu-id="360a9-190">En el ejemplo siguiente se enumeran los parámetros que deberá especificar en la sección de configuración de BGP en el dispositivo VPN local para este ejercicio:</span><span class="sxs-lookup"><span data-stu-id="360a9-190">The example below lists the parameters you will enter into the BGP configuration section on your on-premises VPN device for this exercise:</span></span>

    - <span data-ttu-id="360a9-191">ASN de Site5            : 65050</span><span class="sxs-lookup"><span data-stu-id="360a9-191">Site5 ASN            : 65050</span></span>
    - <span data-ttu-id="360a9-192">IP de BGP Site5: 10.52.255.253</span><span class="sxs-lookup"><span data-stu-id="360a9-192">Site5 BGP IP         : 10.52.255.253</span></span>
    - <span data-ttu-id="360a9-193">Prefijos para anunciar: (por ejemplo), 10.51.0.0/16 y 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="360a9-193">Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span></span>
    - <span data-ttu-id="360a9-194">ASN de red virtual de Azure: 65010</span><span class="sxs-lookup"><span data-stu-id="360a9-194">Azure VNet ASN       : 65010</span></span>
    - <span data-ttu-id="360a9-195">IP 1 de BGP de red virtual de Azure: 10.12.255.4 de túnel para 40.112.190.5</span><span class="sxs-lookup"><span data-stu-id="360a9-195">Azure VNet BGP IP 1  : 10.12.255.4 for tunnel to 40.112.190.5</span></span>
    - <span data-ttu-id="360a9-196">IP 2 de BGP de red virtual de Azure: 10.12.255.5 de túnel para 138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="360a9-196">Azure VNet BGP IP 2  : 10.12.255.5 for tunnel to 138.91.156.129</span></span>
    - <span data-ttu-id="360a9-197">Rutas estáticas        : destino 10.12.255.4/32, próximo salto de la interfaz del túnel VPN para 40.112.190.5                        Destino 10.12.255.5/32, próximo salto de la interfaz del túnel VPN para 138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="360a9-197">Static routes        : Destination 10.12.255.4/32, nexthop the VPN tunnel interface to 40.112.190.5                        Destination 10.12.255.5/32, nexthop the VPN tunnel interface to 138.91.156.129</span></span>
    - <span data-ttu-id="360a9-198">Salto múltiple de eBGP        : asegúrese de que la opción de "salto múltiple" eBGP está habilitada en el dispositivo, si es necesario</span><span class="sxs-lookup"><span data-stu-id="360a9-198">eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed</span></span>

<span data-ttu-id="360a9-199">La conexión debe establecerse después de unos minutos y se iniciará la sesión de emparejamiento BGP una vez establecida la conexión IPsec.</span><span class="sxs-lookup"><span data-stu-id="360a9-199">The connection should be established after a few minutes, and the BGP peering session will start once the IPsec connection is established.</span></span> <span data-ttu-id="360a9-200">En este ejemplo hasta ahora se ha configurado un solo dispositivo VPN local, con el resultado que se muestra en el diagrama a continuación:</span><span class="sxs-lookup"><span data-stu-id="360a9-200">This example so far has configured only one on-premises VPN device, resulting in the diagram shown below:</span></span>

![activo-activo-entre entornos locales](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-to-the-active-active-vpn-gateway"></a><span data-ttu-id="360a9-202">Paso 3: Conexión de dos dispositivos VPN locales con la puerta de enlace VPN activo-activo</span><span class="sxs-lookup"><span data-stu-id="360a9-202">Step 3 - Connect two on-premises VPN devices to the active-active VPN gateway</span></span>
<span data-ttu-id="360a9-203">Si tiene dos dispositivos VPN en la misma red local, puede lograr redundancia dual conectando Azure VPN Gateway al segundo dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="360a9-203">If you have two VPN devices at the same on-premises network, you can achieve dual redundancy by connecting the Azure VPN gateway to the second VPN device.</span></span>

#### <a name="1-create-the-second-local-network-gateway-for-site5"></a><span data-ttu-id="360a9-204">1. Creación de la puertas de enlace de red local para Site5</span><span class="sxs-lookup"><span data-stu-id="360a9-204">1. Create the second local network gateway for Site5</span></span>
<span data-ttu-id="360a9-205">Tenga en cuenta que la dirección IP de puerta de enlace, el prefijo de dirección y la dirección de emparejamiento de BGP para la segunda puerta de enlace de red local no pueden solaparse con la puerta de enlace de red local anterior en la misma red local.</span><span class="sxs-lookup"><span data-stu-id="360a9-205">Note that the gateway IP address, address prefix, and BGP peering address for the second local network gateway must not overlap with the previous local network gateway for the same on-premises network.</span></span>

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-the-vnet-gateway-and-the-second-local-network-gateway"></a><span data-ttu-id="360a9-206">2. Paso 2: Conexión de la puerta de enlace de red virtual y la segunda puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="360a9-206">2. Connect the VNet gateway and the second local network gateway</span></span>
<span data-ttu-id="360a9-207">Cree la conexión de TestVNet1 a Site5_2 con "EnableBGP" establecido como $True</span><span class="sxs-lookup"><span data-stu-id="360a9-207">Create the connection from TestVNet1 to Site5_2 with "EnableBGP" set to $True</span></span>

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a><span data-ttu-id="360a9-208">3. Los parámetros VPN y BGP para el segundo dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="360a9-208">3. VPN and BGP parameters for your second on-premises VPN device</span></span>
<span data-ttu-id="360a9-209">De forma similar, a continuación se indican los parámetros que tendrá que especificar en el segundo dispositivo VPN:</span><span class="sxs-lookup"><span data-stu-id="360a9-209">Similarly, below lists the parameters you will enter into the second VPN device:</span></span>

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel to 40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel to 138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop the VPN tunnel interface to 40.112.190.5
                         Destination 10.12.255.5/32, nexthop the VPN tunnel interface to 138.91.156.129
- eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="360a9-210">Una vez que se establece la conexión (túneles), tendrá dos dispositivos VPN redundantes y túneles que conectan la red local y Azure:</span><span class="sxs-lookup"><span data-stu-id="360a9-210">Once the connection (tunnels) are established, you will have dual redundant VPN devices and tunnels connecting your on-premises network and Azure:</span></span>

![redundancia-dual-entre entornos locales](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <span data-ttu-id="360a9-212"><a name ="aav2v"></a>Parte 3: Establecimiento de una conexión activo-activo de red virtual a red virtual</span><span class="sxs-lookup"><span data-stu-id="360a9-212"><a name ="aav2v"></a>Part 3 - Establish an active-active VNet-to-VNet connection</span></span>
<span data-ttu-id="360a9-213">En esta sección se crea una conexión de red virtual a red virtual activo-activo con BGP.</span><span class="sxs-lookup"><span data-stu-id="360a9-213">This section creates an active-active VNet-to-VNet connection with BGP.</span></span> 

<span data-ttu-id="360a9-214">Las instrucciones que siguen son continuación de los pasos anteriores ya explicados.</span><span class="sxs-lookup"><span data-stu-id="360a9-214">The instructions below continue from the previous steps listed above.</span></span> <span data-ttu-id="360a9-215">Tiene que completar la [Parte 1](#aagateway) para crear y configurar TestVNet1 y VPN Gateway con BGP.</span><span class="sxs-lookup"><span data-stu-id="360a9-215">You must complete [Part 1](#aagateway) to create and configure TestVNet1 and the VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-the-vpn-gateway"></a><span data-ttu-id="360a9-216">Paso 1: cree TestVNet2 y la puerta de enlace de VPN</span><span class="sxs-lookup"><span data-stu-id="360a9-216">Step 1 - Create TestVNet2 and the VPN gateway</span></span>
<span data-ttu-id="360a9-217">Es importante asegurarse de que el espacio de direcciones IP de la red virtual nueva, TestVNet2, no se solape con ninguno de sus intervalos de red virtual.</span><span class="sxs-lookup"><span data-stu-id="360a9-217">It is important to make sure that the IP address space of the new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="360a9-218">En este ejemplo, las redes virtuales pertenecen a la misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="360a9-218">In this example, the virtual networks belong to the same subscription.</span></span> <span data-ttu-id="360a9-219">Puede configurar las conexiones de red virtual a red virtual entre distintas suscripciones, para ello consulte [Configuración de una conexión de red virtual a red virtual](vpn-gateway-vnet-vnet-rm-ps.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="360a9-219">You can set up VNet-to-VNet connections between different subscriptions; please refer to [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) to learn more details.</span></span> <span data-ttu-id="360a9-220">Asegúrese de agregar "-EnableBgp True" al crear las conexiones para habilitar BGP.</span><span class="sxs-lookup"><span data-stu-id="360a9-220">Make sure you add the "-EnableBgp $True" when creating the connections to enable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="360a9-221">1. Declaración de las variables</span><span class="sxs-lookup"><span data-stu-id="360a9-221">1. Declare your variables</span></span>
<span data-ttu-id="360a9-222">Asegúrese de reemplazar los valores por los que desea usar para su configuración.</span><span class="sxs-lookup"><span data-stu-id="360a9-222">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

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

#### <a name="2-create-testvnet2-in-the-new-resource-group"></a><span data-ttu-id="360a9-223">2. Cree TestVNet2 en el nuevo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="360a9-223">2. Create TestVNet2 in the new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-the-active-active-vpn-gateway-for-testvnet2"></a><span data-ttu-id="360a9-224">3. Creación de la puerta de enlace VPN activo-activo para TestVNet2</span><span class="sxs-lookup"><span data-stu-id="360a9-224">3. Create the active-active VPN gateway for TestVNet2</span></span>
<span data-ttu-id="360a9-225">Solicite que se asignen dos direcciones IP públicas a la puerta de enlace que creará para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="360a9-225">Request two public IP addresses to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="360a9-226">También definirá las configuraciones de subred y de IP necesarias.</span><span class="sxs-lookup"><span data-stu-id="360a9-226">You'll also define the subnet and IP configurations required.</span></span>

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

<span data-ttu-id="360a9-227">Cree la puerta de enlace VPN con el número de AS y la marca "EnableActiveActiveFeature".</span><span class="sxs-lookup"><span data-stu-id="360a9-227">Create the VPN gateway with the AS number and the "EnableActiveActiveFeature" flag.</span></span> <span data-ttu-id="360a9-228">Tenga en cuenta que debe reemplazar el valor predeterminado del ASN en las puertas de enlace de VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="360a9-228">Note that you must override the default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="360a9-229">Los ASN para las redes virtuales conectadas deben ser diferentes para habilitar el enrutamiento de tránsito y de BGP.</span><span class="sxs-lookup"><span data-stu-id="360a9-229">The ASNs for the connected VNets must be different to enable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-the-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="360a9-230">Paso 2: Conecte las puertas de enlace de TestVNet1 y TestVNet2</span><span class="sxs-lookup"><span data-stu-id="360a9-230">Step 2 - Connect the TestVNet1 and TestVNet2 gateways</span></span>
<span data-ttu-id="360a9-231">En este ejemplo, ambas puertas de enlace están en la misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="360a9-231">In this example, both gateways are in the same subscription.</span></span> <span data-ttu-id="360a9-232">Puede completar este paso en la misma sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="360a9-232">You can complete this step in the same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="360a9-233">1. Obtenga ambas puertas de enlace</span><span class="sxs-lookup"><span data-stu-id="360a9-233">1. Get both gateways</span></span>
<span data-ttu-id="360a9-234">Asegúrese de iniciar sesión y conectarse a la suscripción 1.</span><span class="sxs-lookup"><span data-stu-id="360a9-234">Make sure you log in and connect to Subscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="360a9-235">2. Cree ambas conexiones</span><span class="sxs-lookup"><span data-stu-id="360a9-235">2. Create both connections</span></span>
<span data-ttu-id="360a9-236">En este paso, creará la conexión de TestVNet1 a TestVNet2 y viceversa.</span><span class="sxs-lookup"><span data-stu-id="360a9-236">In this step, you will create the connection from TestVNet1 to TestVNet2, and the connection from TestVNet2 to TestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="360a9-237">Asegúrese de habilitar BGP para AMBAS conexiones.</span><span class="sxs-lookup"><span data-stu-id="360a9-237">Be sure to enable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="360a9-238">Después de completar estos pasos, la conexión se establecerá en unos minutos y la sesión de emparejamiento de BGP se iniciará una vez se complete la conexión de red virtual a red virtual con redundancia dual:</span><span class="sxs-lookup"><span data-stu-id="360a9-238">After completing these steps, the connection will be establish in a few minutes, and the BGP peering session will be up once the VNet-to-VNet connection is completed with dual redundancy:</span></span>

![activo-activo-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <span data-ttu-id="360a9-240"><a name ="aaupdate"></a>Parte 4: Actualización de una puerta de enlace existente entre activo-activo y activo-en espera</span><span class="sxs-lookup"><span data-stu-id="360a9-240"><a name ="aaupdate"></a>Part 4 - Update existing gateway between active-active and active-standby</span></span>
<span data-ttu-id="360a9-241">La última sección describe cómo configurar una instancia de Azure VPN Gateway existente de activo-en espera a modo activo-activo o viceversa.</span><span class="sxs-lookup"><span data-stu-id="360a9-241">The last section will describe how you can configure an existing Azure VPN gateway from active-standby to active-active mode, or vice versa.</span></span>

> [!NOTE]
> <span data-ttu-id="360a9-242">Esta sección incluye los pasos para cambiar el tamaño de una SKU heredada (SKU antigua) de una puerta de enlace VPN ya creada desde la versión Standard a HighPerformance.</span><span class="sxs-lookup"><span data-stu-id="360a9-242">This section includes the steps to resize a legacy SKU (old SKU) of an already created VPN gateway from Standard to HighPerformance.</span></span> <span data-ttu-id="360a9-243">Estos pasos no actualizan una SKU heredada anterior a una de las SKU nuevas.</span><span class="sxs-lookup"><span data-stu-id="360a9-243">These steps do not upgrade an old legacy SKU to one of the new SKUs.</span></span>
> 
> 

### <a name="configure-an-active-standby-gateway-to-active-active-gateway"></a><span data-ttu-id="360a9-244">Configuración de una puerta de enlace de activo-en espera a puerta de enlace activo-activo</span><span class="sxs-lookup"><span data-stu-id="360a9-244">Configure an active-standby gateway to active-active gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="360a9-245">1. Parámetros de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="360a9-245">1. Gateway parameters</span></span>
<span data-ttu-id="360a9-246">En el ejemplo siguiente se convierte una puerta de enlace de activo-en espera en puerta de enlace activo-activo.</span><span class="sxs-lookup"><span data-stu-id="360a9-246">The following example converts an active-standby gateway into an active-active gateway.</span></span> <span data-ttu-id="360a9-247">Tiene que crear otra dirección IP pública, y agregar una segunda configuración IP de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="360a9-247">You need to create another public IP address, then add a second Gateway IP configuration.</span></span> <span data-ttu-id="360a9-248">A continuación se muestran los parámetros que se utilizan:</span><span class="sxs-lookup"><span data-stu-id="360a9-248">Below shows the parameters used:</span></span>

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

#### <a name="2-create-the-public-ip-address-then-add-the-second-gateway-ip-configuration"></a><span data-ttu-id="360a9-249">2. Cree la dirección IP pública, y agregue una segunda configuración IP de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="360a9-249">2. Create the public IP address, then add the second gateway IP configuration</span></span>

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-the-gateway"></a><span data-ttu-id="360a9-250">3. Habilite el modo activo-activo y actualice la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="360a9-250">3. Enable active-active mode and update the gateway</span></span>
<span data-ttu-id="360a9-251">Tiene que establecer el objeto de puerta de enlace en PowerShell para desencadenar la actualización real.</span><span class="sxs-lookup"><span data-stu-id="360a9-251">You must set the gateway object in PowerShell to trigger the actual update.</span></span> <span data-ttu-id="360a9-252">La SKU de la puerta de enlace de red virtual debe cambiarse también (modificar su tamaño) a HighPerformance puesto que se creó anteriormente como estándar.</span><span class="sxs-lookup"><span data-stu-id="360a9-252">The SKU of the virtual network gateway must also be changed (resized) to HighPerformance since it was created previously as Standard.</span></span>

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

<span data-ttu-id="360a9-253">Esta actualización puede tardar de 30 a 45 minutos.</span><span class="sxs-lookup"><span data-stu-id="360a9-253">This update can take 30 to 45 minutes.</span></span>

### <a name="configure-an-active-active-gateway-to-active-standby-gateway"></a><span data-ttu-id="360a9-254">Configuración de una puerta de enlace de activo-activo a puerta de enlace activo-en espera</span><span class="sxs-lookup"><span data-stu-id="360a9-254">Configure an active-active gateway to active-standby gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="360a9-255">1. Parámetros de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="360a9-255">1. Gateway parameters</span></span>
<span data-ttu-id="360a9-256">Utilice los mismos parámetros que en el caso anterior, obtenga el nombre de la configuración IP que desea quitar.</span><span class="sxs-lookup"><span data-stu-id="360a9-256">Use the same parameters as above, get the name of the IP configuration you want to remove.</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-the-gateway-ip-configuration-and-disable-the-active-active-mode"></a><span data-ttu-id="360a9-257">2. Quite la configuración de IP de puerta de enlace y deshabilite el modo activo-activo</span><span class="sxs-lookup"><span data-stu-id="360a9-257">2. Remove the gateway IP configuration and disable the active-active mode</span></span>
<span data-ttu-id="360a9-258">De forma similar, tiene que establecer el objeto de puerta de enlace en PowerShell para desencadenar la actualización real.</span><span class="sxs-lookup"><span data-stu-id="360a9-258">Similarly, you must set the gateway object in PowerShell to trigger the actual update.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

<span data-ttu-id="360a9-259">Esta actualización puede tardar hasta 30 o 45 minutos.</span><span class="sxs-lookup"><span data-stu-id="360a9-259">This update can take up to 30 to  45 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="360a9-260">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="360a9-260">Next steps</span></span>
<span data-ttu-id="360a9-261">Una vez completada la conexión, puede agregar máquinas virtuales a las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="360a9-261">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="360a9-262">Consulte [Creación de una máquina virtual que ejecuta Windows en el Portal de Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para ver los pasos.</span><span class="sxs-lookup"><span data-stu-id="360a9-262">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>