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
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a><span data-ttu-id="64434-103">Configuración de conexiones VPN S2S activo-activo con Azure VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="64434-103">Configure active-active S2S VPN connections with Azure VPN Gateways</span></span>

<span data-ttu-id="64434-104">Este artículo le guiará a través de hello pasos toocreate activo-activo entre-local y las conexiones de red virtual a red virtual con el modelo de implementación del Administrador de recursos de Hola y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64434-104">This article walks you through hello steps toocreate active-active cross-premises and VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-highly-available-cross-premises-connections"></a><span data-ttu-id="64434-105">Acerca de las conexiones entre entornos locales de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="64434-105">About Highly Available Cross-Premises Connections</span></span>
<span data-ttu-id="64434-106">tooachieve alta disponibilidad para entre entornos y la conectividad de red virtual a red virtual, debe implementar varias puertas de enlace VPN y establecer varias conexiones en paralelo entre las redes y Azure.</span><span class="sxs-lookup"><span data-stu-id="64434-106">tooachieve high availability for cross-premises and VNet-to-VNet connectivity, you should deploy multiple VPN gateways and establish multiple parallel connections between your networks and Azure.</span></span> <span data-ttu-id="64434-107">Consulte [Conectividad de alta disponibilidad entre locales y de red virtual a red virtual](vpn-gateway-highlyavailable.md) para información general de las opciones de conectividad y la topología.</span><span class="sxs-lookup"><span data-stu-id="64434-107">Please see [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) for an overview of connectivity options and topology.</span></span>

<span data-ttu-id="64434-108">Este artículo proporciona instrucciones de hello tooset seguridad un activo / activo entre entornos conexión VPN y activo / activo conexión entre dos redes virtuales:</span><span class="sxs-lookup"><span data-stu-id="64434-108">This article provides hello instructions tooset up an active-active cross-premises VPN connection, and active-active connection between two virtual networks:</span></span>

* [<span data-ttu-id="64434-109">Parte 1: Creación y configuración de Azure VPN Gateway en el modo activo-activo</span><span class="sxs-lookup"><span data-stu-id="64434-109">Part 1 - Create and configure your Azure VPN gateway in active-active mode</span></span>](#aagateway)
* [<span data-ttu-id="64434-110">Parte 2: Establecimiento de conexiones activo-activo entre entornos locales</span><span class="sxs-lookup"><span data-stu-id="64434-110">Part 2 - Establish active-active cross-premises connections</span></span>](#aacrossprem)
* [<span data-ttu-id="64434-111">Parte 3: Establecimiento de conexiones activo-activo de red virtual a red virtual</span><span class="sxs-lookup"><span data-stu-id="64434-111">Part 3 - Establish active-active VNet-to-VNet connections</span></span>](#aav2v)
* [<span data-ttu-id="64434-112">Parte 4: Actualización de una puerta de enlace existente entre activo-activo y activo-en espera</span><span class="sxs-lookup"><span data-stu-id="64434-112">Part 4 - Update existing gateway between active-active and active-standby</span></span>](#aaupdate)

<span data-ttu-id="64434-113">Puede combinar estos toobuild conjuntamente una topología de red más compleja, de alta disponibilidad que satisfaga sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="64434-113">You can combine these together toobuild a more complex, highly available network topology that meets your needs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="64434-114">Tenga en cuenta que el modo activo / activo de hello usa Hola solo después de SKU:</span><span class="sxs-lookup"><span data-stu-id="64434-114">Please note that hello active-active mode uses only hello following SKUs:</span></span> 
  * <span data-ttu-id="64434-115">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="64434-115">VpnGw1, VpnGw2, VpnGw3</span></span>
  * <span data-ttu-id="64434-116">Alto rendimiento (para SKU heredadas anteriores)</span><span class="sxs-lookup"><span data-stu-id="64434-116">HighPerformance (for old legacy SKUs)</span></span>
> 
> 

## <span data-ttu-id="64434-117"><a name ="aagateway"></a>Parte 1: Creación y configuración de puertas de enlace VPN activo-activo</span><span class="sxs-lookup"><span data-stu-id="64434-117"><a name ="aagateway"></a>Part 1 - Create and configure active-active VPN gateways</span></span>
<span data-ttu-id="64434-118">Hola pasos configurará la puerta de enlace de VPN de Azure en los modos activo / activo.</span><span class="sxs-lookup"><span data-stu-id="64434-118">hello following steps will configure your Azure VPN gateway in active-active modes.</span></span> <span data-ttu-id="64434-119">Hola las diferencias principales entre puertas de enlace de hello activo / activo y reserva activa:</span><span class="sxs-lookup"><span data-stu-id="64434-119">hello key differences between hello active-active and active-standby gateways:</span></span>

* <span data-ttu-id="64434-120">Necesita dos configuraciones de IP de puerta de enlace toocreate con dos direcciones IP públicas</span><span class="sxs-lookup"><span data-stu-id="64434-120">You need toocreate two Gateway IP configurations with two public IP addresses</span></span>
* <span data-ttu-id="64434-121">Necesita establecer hello EnableActiveActiveFeature marca</span><span class="sxs-lookup"><span data-stu-id="64434-121">You need set hello EnableActiveActiveFeature flag</span></span>
* <span data-ttu-id="64434-122">puerta de enlace de Hello SKU debe ser VpnGw1, VpnGw2, VpnGw3 o alto rendimiento (SKU heredado).</span><span class="sxs-lookup"><span data-stu-id="64434-122">hello gateway SKU must be VpnGw1, VpnGw2, VpnGw3, or HighPerformance (legacy SKU).</span></span>

<span data-ttu-id="64434-123">Hello otras propiedades son Hola igual que las puertas de enlace de hello no activo / activo.</span><span class="sxs-lookup"><span data-stu-id="64434-123">hello other properties are hello same as hello non-active-active gateways.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="64434-124">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="64434-124">Before you begin</span></span>
* <span data-ttu-id="64434-125">Compruebe que tiene una suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="64434-125">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="64434-126">Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="64434-126">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="64434-127">Necesitará tooinstall hello Azure Resource Manager cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64434-127">You'll need tooinstall hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="64434-128">Vea [información general de Azure PowerShell](/powershell/azure/overview) para obtener más información acerca de cómo instalar los cmdlets de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="64434-128">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="64434-129">Paso 1: Creación y configuración de VNet1</span><span class="sxs-lookup"><span data-stu-id="64434-129">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="64434-130">1. Declaración de las variables</span><span class="sxs-lookup"><span data-stu-id="64434-130">1. Declare your variables</span></span>
<span data-ttu-id="64434-131">Para este ejercicio, comenzaremos declarando las variables.</span><span class="sxs-lookup"><span data-stu-id="64434-131">For this exercise, we'll start by declaring our variables.</span></span> <span data-ttu-id="64434-132">ejemplo de Hola siguiente declara las variables de hello con valores de hello para este ejercicio.</span><span class="sxs-lookup"><span data-stu-id="64434-132">hello example below declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="64434-133">Ser seguro de valores de hello tooreplace con su propio cuando se configura para la producción.</span><span class="sxs-lookup"><span data-stu-id="64434-133">Be sure tooreplace hello values with your own when configuring for production.</span></span> <span data-ttu-id="64434-134">Puede utilizar estas variables si está ejecutando a través de hello pasos toobecome familiarizado con este tipo de configuración.</span><span class="sxs-lookup"><span data-stu-id="64434-134">You can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="64434-135">Modificar variables de hello y, a continuación, copie y pegue en la consola de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64434-135">Modify hello variables, and then copy and paste into your PowerShell console.</span></span>

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="64434-136">2. Conectar tooyour suscripción y crear un nuevo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="64434-136">2. Connect tooyour subscription and create a new resource group</span></span>
<span data-ttu-id="64434-137">Asegúrese de que cambie hello toouse de modo tooPowerShell cmdlets del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="64434-137">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="64434-138">Para obtener más información, consulte [Uso de Windows PowerShell con el Administrador de recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="64434-138">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="64434-139">Abra la consola de PowerShell y conectar con tooyour cuenta.</span><span class="sxs-lookup"><span data-stu-id="64434-139">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="64434-140">Usar hello después toohelp de ejemplo que conectarse:</span><span class="sxs-lookup"><span data-stu-id="64434-140">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="64434-141">3. Creación de TestVNet1</span><span class="sxs-lookup"><span data-stu-id="64434-141">3. Create TestVNet1</span></span>
<span data-ttu-id="64434-142">ejemplo de Hola siguiente crea una red virtual denominada TestVNet1 y tres subredes, un GatewaySubnet llamado, uno llamado front-end y un back-end de llamada.</span><span class="sxs-lookup"><span data-stu-id="64434-142">hello sample below creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="64434-143">Al reemplazar valores, es importante que siempre asigne el nombre GatewaySubnet a la subred de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="64434-143">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="64434-144">Si usa otro, se producirá un error al crear la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="64434-144">If you name it something else, your gateway creation will fail.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a><span data-ttu-id="64434-145">Paso 2: crear la puerta de enlace VPN de Hola para TestVNet1 con el modo activo / activo</span><span class="sxs-lookup"><span data-stu-id="64434-145">Step 2 - Create hello VPN gateway for TestVNet1 with active-active mode</span></span>
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a><span data-ttu-id="64434-146">1. Crear direcciones IP públicas de Hola y configuraciones de IP de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="64434-146">1. Create hello public IP addresses and gateway IP configurations</span></span>
<span data-ttu-id="64434-147">Solicitud dos pública direcciones toobe toohello asignado puerta de enlace IP que creará para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="64434-147">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="64434-148">También definirá subred hello y las configuraciones de IP necesarias.</span><span class="sxs-lookup"><span data-stu-id="64434-148">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a><span data-ttu-id="64434-149">2. Creación de puerta de enlace VPN de hello con una configuración activo / activo</span><span class="sxs-lookup"><span data-stu-id="64434-149">2. Create hello VPN gateway with active-active configuration</span></span>
<span data-ttu-id="64434-150">Crear puerta de enlace de red virtual de Hola para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="64434-150">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="64434-151">Tenga en cuenta que hay dos entradas de GatewayIpConfig y hello EnableActiveActiveFeature marca está establecida.</span><span class="sxs-lookup"><span data-stu-id="64434-151">Note that there are two GatewayIpConfig entries, and hello EnableActiveActiveFeature flag is set.</span></span> <span data-ttu-id="64434-152">Crear una puerta de enlace puede tardar un rato (45 minutos o más toocomplete).</span><span class="sxs-lookup"><span data-stu-id="64434-152">Creating a gateway can take a while (45 minutes or more toocomplete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a><span data-ttu-id="64434-153">3. Obtener direcciones IP públicas de hello puerta de enlace y dirección IP del mismo nivel de BGP de Hola</span><span class="sxs-lookup"><span data-stu-id="64434-153">3. Obtain hello gateway public IP addresses and hello BGP Peer IP address</span></span>
<span data-ttu-id="64434-154">Una vez creada la puerta de enlace de hello, necesitará tooobtain Hola BGP del mismo nivel IPAddress en hello puerta de enlace de VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="64434-154">Once hello gateway is created, you will need tooobtain hello BGP Peer IP address on hello Azure VPN Gateway.</span></span> <span data-ttu-id="64434-155">Esta dirección es necesario tooconfigure Hola puerta de enlace de VPN de Azure como un par BGP para los dispositivos VPN local.</span><span class="sxs-lookup"><span data-stu-id="64434-155">This address is needed tooconfigure hello Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

<span data-ttu-id="64434-156">Usar hello después cmdlets tooshow Hola dos direcciones IP públicas asignadas a la puerta de enlace VPN y sus direcciones IP de BGP del mismo nivel correspondientes para cada instancia de puerta de enlace:</span><span class="sxs-lookup"><span data-stu-id="64434-156">Use hello following cmdlets tooshow hello two public IP addresses allocated for your VPN gateway, and their corresponding BGP Peer IP addresses for each gateway instance:</span></span>

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

<span data-ttu-id="64434-157">orden de Hola de direcciones IP públicas de Hola para instancias de puerta de enlace de Hola y Hola direcciones de emparejamiento de BGP correspondientes son Hola igual.</span><span class="sxs-lookup"><span data-stu-id="64434-157">hello order of hello public IP addresses for hello gateway instances and hello corresponding BGP Peering Addresses are hello same.</span></span> <span data-ttu-id="64434-158">En este ejemplo, la puerta de enlace de hello VM con la dirección IP pública de 40.112.190.5 utilizará 10.12.255.4 como su dirección de emparejamiento de BGP y puerta de enlace de hello con 138.91.156.129 utilizará 10.12.255.5.</span><span class="sxs-lookup"><span data-stu-id="64434-158">In this example, hello gateway VM with public IP of 40.112.190.5 will use 10.12.255.4 as its BGP Peering Address, and hello gateway with 138.91.156.129 will use 10.12.255.5.</span></span> <span data-ttu-id="64434-159">Esta información es necesaria cuando configura su local de dispositivos VPN que se conectan puerta de enlace de toohello activo / activo.</span><span class="sxs-lookup"><span data-stu-id="64434-159">This information is needed when you set up your on premises VPN devices connecting toohello active-active gateway.</span></span> <span data-ttu-id="64434-160">puerta de enlace de Hola se muestra en el diagrama de Hola a continuación con todas las direcciones:</span><span class="sxs-lookup"><span data-stu-id="64434-160">hello gateway is shown in hello diagram below with all addresses:</span></span>

![puerta de enlace activo-activo](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

<span data-ttu-id="64434-162">Una vez creada la puerta de enlace de hello, puede usar esta puerta de enlace tooestablish activo-activo entre entornos o conexión de red virtual a red virtual.</span><span class="sxs-lookup"><span data-stu-id="64434-162">Once hello gateway is created, you can use this gateway tooestablish active-active cross-premises or VNet-to-VNet connection.</span></span> <span data-ttu-id="64434-163">Hola siguientes secciones le guiará a través de hello pasos toocomplete Hola ejercicio.</span><span class="sxs-lookup"><span data-stu-id="64434-163">hello following sections will walk through hello steps toocomplete hello exercise.</span></span>

## <span data-ttu-id="64434-164"><a name ="aacrossprem"></a>Parte 2: Establecimiento de una conexión activo-activo entre entornos locales</span><span class="sxs-lookup"><span data-stu-id="64434-164"><a name ="aacrossprem"></a>Part 2 - Establish an active-active cross-premises connection</span></span>
<span data-ttu-id="64434-165">tooestablish una conexión entre entornos, necesita una puerta de enlace de red Local toorepresent toocreate dispositivo VPN local y una puerta de enlace de conexión tooconnect Hola VPN de Azure con puerta de enlace de red local de Hola.</span><span class="sxs-lookup"><span data-stu-id="64434-165">tooestablish a cross-premises connection, you need toocreate a Local Network Gateway toorepresent your on-premises VPN device, and a Connection tooconnect hello Azure VPN gateway with hello local network gateway.</span></span> <span data-ttu-id="64434-166">En este ejemplo, puerta de enlace de VPN de Azure de hello está en modo activo / activo.</span><span class="sxs-lookup"><span data-stu-id="64434-166">In this example, hello Azure VPN gateway is in active-active mode.</span></span> <span data-ttu-id="64434-167">Como resultado, incluso si hay solo uno local dispositivo VPN (puerta de enlace de red local) y recursos de una conexión, ambas instancias de puerta de enlace de VPN de Azure establecerán túneles VPN S2S con dispositivo de hello en local.</span><span class="sxs-lookup"><span data-stu-id="64434-167">As a result, even though there is only one on-premises VPN device (local network gateway) and one connection resource, both Azure VPN gateway instances will establish S2S VPN tunnels with hello on-premises device.</span></span>

<span data-ttu-id="64434-168">Antes de continuar, asegúrese de que ha completado la [parte 1](#aagateway) de este ejercicio.</span><span class="sxs-lookup"><span data-stu-id="64434-168">Before proceeding, please make sure you have completed [Part 1](#aagateway) of this exercise.</span></span>

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a><span data-ttu-id="64434-169">Paso 1: crear y configurar la puerta de enlace de red local de Hola</span><span class="sxs-lookup"><span data-stu-id="64434-169">Step 1 - Create and configure hello local network gateway</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="64434-170">1. Declaración de las variables</span><span class="sxs-lookup"><span data-stu-id="64434-170">1. Declare your variables</span></span>
<span data-ttu-id="64434-171">Este ejercicio seguirá toobuild configuración de Hola que se muestra en el diagrama de Hola.</span><span class="sxs-lookup"><span data-stu-id="64434-171">This exercise will continue toobuild hello configuration shown in hello diagram.</span></span> <span data-ttu-id="64434-172">Ser seguro tooreplace valores de hello con hello las que desea que toouse para la configuración.</span><span class="sxs-lookup"><span data-stu-id="64434-172">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

<span data-ttu-id="64434-173">Un par de cosas toonote con respecto a los parámetros de puerta de enlace de red local de hello:</span><span class="sxs-lookup"><span data-stu-id="64434-173">A couple of things toonote regarding hello local network gateway parameters:</span></span>

* <span data-ttu-id="64434-174">puerta de enlace de red local de Hello puede estar en Hola iguales o diferentes y ubicación de recurso de grupo como Hola puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="64434-174">hello local network gateway can be in hello same or different location and resource group as hello VPN gateway.</span></span> <span data-ttu-id="64434-175">Este ejemplo muestra en ellos en distintos grupos de recursos, pero en hello misma ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="64434-175">This example shows them in different resource groups but in hello same Azure location.</span></span>
* <span data-ttu-id="64434-176">Si hay un único dispositivo VPN local tal y como se muestra arriba, conexión de hello activo / activo puede trabajar con o sin el protocolo BGP.</span><span class="sxs-lookup"><span data-stu-id="64434-176">If there is only one on-premises VPN device as shown above, hello active-active connection can work with or without BGP protocol.</span></span> <span data-ttu-id="64434-177">Este ejemplo utiliza para la conexión entre entornos de hello BGP.</span><span class="sxs-lookup"><span data-stu-id="64434-177">This example uses BGP for hello cross-premises connection.</span></span>
* <span data-ttu-id="64434-178">Si se habilita BGP, prefijo Hola necesita toodeclare para puerta de enlace de red local de hello es la dirección de host de Hola de su dirección IP de BGP del mismo nivel en el dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="64434-178">If BGP is enabled, hello prefix you need toodeclare for hello local network gateway is hello host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="64434-179">En este caso, es un prefijo /32 de "10.52.255.253/32".</span><span class="sxs-lookup"><span data-stu-id="64434-179">In this case, it's a /32 prefix of "10.52.255.253/32".</span></span>
* <span data-ttu-id="64434-180">Como recordatorio, debe usar diferentes ASN de BGP entre las redes locales y la red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="64434-180">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="64434-181">Si se hello mismo, deberá toochange el ASN VNet si el dispositivo VPN local ya utiliza Hola ASN toopeer con otros vecinos BGP.</span><span class="sxs-lookup"><span data-stu-id="64434-181">If they are hello same, you need toochange your VNet ASN if your on-premises VPN device already uses hello ASN toopeer with other BGP neighbors.</span></span>

#### <a name="2-create-hello-local-network-gateway-for-site5"></a><span data-ttu-id="64434-182">2. Crear puerta de enlace de red local de Hola para Site5</span><span class="sxs-lookup"><span data-stu-id="64434-182">2. Create hello local network gateway for Site5</span></span>
<span data-ttu-id="64434-183">Antes de continuar, asegúrese de que está conectado aún tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="64434-183">Before you continue, please make sure you are still connected tooSubscription 1.</span></span> <span data-ttu-id="64434-184">Crear grupo de recursos de hello si no se ha creado.</span><span class="sxs-lookup"><span data-stu-id="64434-184">Create hello resource group if it is not yet created.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="64434-185">Paso 2: conectar la puerta de enlace de red virtual de Hola y puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="64434-185">Step 2 - Connect hello VNet gateway and local network gateway</span></span>
#### <a name="1-get-hello-two-gateways"></a><span data-ttu-id="64434-186">1. Obtener Hola dos puertas de enlace</span><span class="sxs-lookup"><span data-stu-id="64434-186">1. Get hello two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a><span data-ttu-id="64434-187">2. Crear conexiones de hello TestVNet1 tooSite5</span><span class="sxs-lookup"><span data-stu-id="64434-187">2. Create hello TestVNet1 tooSite5 connection</span></span>
<span data-ttu-id="64434-188">En este paso, creará conexión Hola de TestVNet1 tooSite5_1 con "EnableBGP" establecido demasiado$ True.</span><span class="sxs-lookup"><span data-stu-id="64434-188">In this step, you will create hello connection from TestVNet1 tooSite5_1 with "EnableBGP" set too$True.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a><span data-ttu-id="64434-189">3. Parámetros VPN y BGP para el dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="64434-189">3. VPN and BGP parameters for your on-premises VPN device</span></span>
<span data-ttu-id="64434-190">ejemplo de Hola siguiente enumera los parámetros de Hola que se especificará en la sección de configuración de BGP de hello en dispositivo VPN local para este ejercicio:</span><span class="sxs-lookup"><span data-stu-id="64434-190">hello example below lists hello parameters you will enter into hello BGP configuration section on your on-premises VPN device for this exercise:</span></span>

    - <span data-ttu-id="64434-191">ASN de Site5            : 65050</span><span class="sxs-lookup"><span data-stu-id="64434-191">Site5 ASN            : 65050</span></span>
    - <span data-ttu-id="64434-192">IP de BGP Site5: 10.52.255.253</span><span class="sxs-lookup"><span data-stu-id="64434-192">Site5 BGP IP         : 10.52.255.253</span></span>
    - <span data-ttu-id="64434-193">Agrega el prefijo tooannounce: (por ejemplo) 10.51.0.0/16 y 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="64434-193">Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span></span>
    - <span data-ttu-id="64434-194">ASN de red virtual de Azure: 65010</span><span class="sxs-lookup"><span data-stu-id="64434-194">Azure VNet ASN       : 65010</span></span>
    - <span data-ttu-id="64434-195">Azure red virtual BGP IP 1: 10.12.255.4 para too40.112.190.5 de túnel</span><span class="sxs-lookup"><span data-stu-id="64434-195">Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5</span></span>
    - <span data-ttu-id="64434-196">Azure red virtual BGP IP 2: 10.12.255.5 para too138.91.156.129 de túnel</span><span class="sxs-lookup"><span data-stu-id="64434-196">Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129</span></span>
    - <span data-ttu-id="64434-197">Rutas estáticas: destino 10.12.255.4/32, nexthop Hola VPN túnel interfaz too40.112.190.5 destino 10.12.255.5/32, nexthop Hola VPN túnel interfaz too138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="64434-197">Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5                        Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129</span></span>
    - <span data-ttu-id="64434-198">eBGP salto múltiple: asegúrese de opción de "salto múltiple" hello eBGP está habilitada en el dispositivo si es necesario</span><span class="sxs-lookup"><span data-stu-id="64434-198">eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed</span></span>

<span data-ttu-id="64434-199">debe establecerse la conexión de Hello después de unos minutos y sesión Hola BGP del mismo nivel se iniciarán una vez establecida la conexión IPsec Hola.</span><span class="sxs-lookup"><span data-stu-id="64434-199">hello connection should be established after a few minutes, and hello BGP peering session will start once hello IPsec connection is established.</span></span> <span data-ttu-id="64434-200">En este ejemplo hasta ahora ha configurado un único dispositivo VPN local, resultante en el diagrama de Hola que se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="64434-200">This example so far has configured only one on-premises VPN device, resulting in hello diagram shown below:</span></span>

![activo-activo-entre entornos locales](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a><span data-ttu-id="64434-202">Paso 3: conectar dos local VPN dispositivos toohello activo-activo puerta de enlace VPN</span><span class="sxs-lookup"><span data-stu-id="64434-202">Step 3 - Connect two on-premises VPN devices toohello active-active VPN gateway</span></span>
<span data-ttu-id="64434-203">Si tiene dos dispositivos VPN en hello mismo local red, puede lograr redundancia dual por conexión Hola VPN de Azure puerta de enlace toohello segundo dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="64434-203">If you have two VPN devices at hello same on-premises network, you can achieve dual redundancy by connecting hello Azure VPN gateway toohello second VPN device.</span></span>

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a><span data-ttu-id="64434-204">1. Crear puerta de enlace de red local segundo Hola para Site5</span><span class="sxs-lookup"><span data-stu-id="64434-204">1. Create hello second local network gateway for Site5</span></span>
<span data-ttu-id="64434-205">Tenga en cuenta que dirección IP de puerta de enlace de hello, prefijo de dirección y dirección de emparejamiento de BGP de puerta de enlace de red local segundo hello no deben solaparse con hello anterior red local puerta de enlace de hello misma red en local.</span><span class="sxs-lookup"><span data-stu-id="64434-205">Note that hello gateway IP address, address prefix, and BGP peering address for hello second local network gateway must not overlap with hello previous local network gateway for hello same on-premises network.</span></span>

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a><span data-ttu-id="64434-206">2. Conectar la puerta de enlace de red virtual de Hola y la segunda la puerta de enlace de red local Hola</span><span class="sxs-lookup"><span data-stu-id="64434-206">2. Connect hello VNet gateway and hello second local network gateway</span></span>
<span data-ttu-id="64434-207">Crear la conexión de Hola desde TestVNet1 tooSite5_2 con "EnableBGP" establecido demasiado$ True</span><span class="sxs-lookup"><span data-stu-id="64434-207">Create hello connection from TestVNet1 tooSite5_2 with "EnableBGP" set too$True</span></span>

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a><span data-ttu-id="64434-208">3. Los parámetros VPN y BGP para el segundo dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="64434-208">3. VPN and BGP parameters for your second on-premises VPN device</span></span>
<span data-ttu-id="64434-209">De forma similar, siguientes listas de parámetros de Hola entrará en el dispositivo VPN de la segunda hello:</span><span class="sxs-lookup"><span data-stu-id="64434-209">Similarly, below lists hello parameters you will enter into hello second VPN device:</span></span>

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

<span data-ttu-id="64434-210">Una vez que se han establecido conexión hello (túneles), tendrá dos dispositivos VPN redundancia y túneles que conectan la red local y Azure:</span><span class="sxs-lookup"><span data-stu-id="64434-210">Once hello connection (tunnels) are established, you will have dual redundant VPN devices and tunnels connecting your on-premises network and Azure:</span></span>

![redundancia-dual-entre entornos locales](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <span data-ttu-id="64434-212"><a name ="aav2v"></a>Parte 3: Establecimiento de una conexión activo-activo de red virtual a red virtual</span><span class="sxs-lookup"><span data-stu-id="64434-212"><a name ="aav2v"></a>Part 3 - Establish an active-active VNet-to-VNet connection</span></span>
<span data-ttu-id="64434-213">En esta sección se crea una conexión de red virtual a red virtual activo-activo con BGP.</span><span class="sxs-lookup"><span data-stu-id="64434-213">This section creates an active-active VNet-to-VNet connection with BGP.</span></span> 

<span data-ttu-id="64434-214">Estas instrucciones Hola continuar de los pasos anteriores Hola mencionados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="64434-214">hello instructions below continue from hello previous steps listed above.</span></span> <span data-ttu-id="64434-215">Debe completar [parte 1](#aagateway) toocreate TestVNet1 y configurar Hola puerta de enlace de VPN con BGP.</span><span class="sxs-lookup"><span data-stu-id="64434-215">You must complete [Part 1](#aagateway) toocreate and configure TestVNet1 and hello VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a><span data-ttu-id="64434-216">Paso 1: crear la puerta de enlace VPN de hello y TestVNet2</span><span class="sxs-lookup"><span data-stu-id="64434-216">Step 1 - Create TestVNet2 and hello VPN gateway</span></span>
<span data-ttu-id="64434-217">Es importante toomake seguro de que el espacio de direcciones IP de Hola de hello nueva red virtual, TestVNet2, no se superponen con ninguno de los intervalos de red virtual.</span><span class="sxs-lookup"><span data-stu-id="64434-217">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="64434-218">En este ejemplo, redes virtuales de hello pertenecen toohello misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="64434-218">In this example, hello virtual networks belong toohello same subscription.</span></span> <span data-ttu-id="64434-219">Puede configurar las conexiones de red virtual a red virtual entre distintas suscripciones; Consulte demasiado[configurar una conexión de red virtual a red virtual](vpn-gateway-vnet-vnet-rm-ps.md) toolearn más detalles.</span><span class="sxs-lookup"><span data-stu-id="64434-219">You can set up VNet-to-VNet connections between different subscriptions; please refer too[Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) toolearn more details.</span></span> <span data-ttu-id="64434-220">Asegúrese de agregar Hola "-EnableBgp $True" al crear Hola conexiones tooenable BGP.</span><span class="sxs-lookup"><span data-stu-id="64434-220">Make sure you add hello "-EnableBgp $True" when creating hello connections tooenable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="64434-221">1. Declaración de las variables</span><span class="sxs-lookup"><span data-stu-id="64434-221">1. Declare your variables</span></span>
<span data-ttu-id="64434-222">Ser seguro tooreplace valores de hello con hello las que desea que toouse para la configuración.</span><span class="sxs-lookup"><span data-stu-id="64434-222">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

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

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a><span data-ttu-id="64434-223">2. Crear TestVNet2 Hola nuevo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="64434-223">2. Create TestVNet2 in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a><span data-ttu-id="64434-224">3. Crear puerta de enlace VPN de hello activo / activo para TestVNet2</span><span class="sxs-lookup"><span data-stu-id="64434-224">3. Create hello active-active VPN gateway for TestVNet2</span></span>
<span data-ttu-id="64434-225">Solicitud dos pública direcciones toobe toohello asignado puerta de enlace IP que creará para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="64434-225">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="64434-226">También definirá subred hello y las configuraciones de IP necesarias.</span><span class="sxs-lookup"><span data-stu-id="64434-226">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

<span data-ttu-id="64434-227">Crear puerta de enlace VPN de hello con hello como marca de "EnableActiveActiveFeature" hello y número.</span><span class="sxs-lookup"><span data-stu-id="64434-227">Create hello VPN gateway with hello AS number and hello "EnableActiveActiveFeature" flag.</span></span> <span data-ttu-id="64434-228">Tenga en cuenta que es necesario reemplazar predeterminado Hola ASN en las puertas de enlace de VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="64434-228">Note that you must override hello default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="64434-229">Hola ASN para hello conectado las redes virtuales debe ser diferente tooenable BGP y el enrutamiento de tránsito.</span><span class="sxs-lookup"><span data-stu-id="64434-229">hello ASNs for hello connected VNets must be different tooenable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="64434-230">Paso 2: conectar hello TestVNet1 y TestVNet2 puertas de enlace</span><span class="sxs-lookup"><span data-stu-id="64434-230">Step 2 - Connect hello TestVNet1 and TestVNet2 gateways</span></span>
<span data-ttu-id="64434-231">En este ejemplo, las puertas de enlace se encuentran en hello misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="64434-231">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="64434-232">Puede completar este paso en hello misma sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64434-232">You can complete this step in hello same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="64434-233">1. Obtenga ambas puertas de enlace</span><span class="sxs-lookup"><span data-stu-id="64434-233">1. Get both gateways</span></span>
<span data-ttu-id="64434-234">Asegúrese de que inicie sesión y conectarse tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="64434-234">Make sure you log in and connect tooSubscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="64434-235">2. Cree ambas conexiones</span><span class="sxs-lookup"><span data-stu-id="64434-235">2. Create both connections</span></span>
<span data-ttu-id="64434-236">En este paso, creará conexión Hola de TestVNet1 tooTestVNet2 y conexión Hola de TestVNet2 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="64434-236">In this step, you will create hello connection from TestVNet1 tooTestVNet2, and hello connection from TestVNet2 tooTestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="64434-237">Ser seguro tooenable BGP para las conexiones de ambos.</span><span class="sxs-lookup"><span data-stu-id="64434-237">Be sure tooenable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="64434-238">Después de completar estos pasos, se establecerá la conexión de hello en unos minutos y la sesión de emparejamiento de BGP Hola volverá a estar en una vez que se completa la conexión de red virtual a red virtual de hello con redundancia dual:</span><span class="sxs-lookup"><span data-stu-id="64434-238">After completing these steps, hello connection will be establish in a few minutes, and hello BGP peering session will be up once hello VNet-to-VNet connection is completed with dual redundancy:</span></span>

![activo-activo-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <span data-ttu-id="64434-240"><a name ="aaupdate"></a>Parte 4: Actualización de una puerta de enlace existente entre activo-activo y activo-en espera</span><span class="sxs-lookup"><span data-stu-id="64434-240"><a name ="aaupdate"></a>Part 4 - Update existing gateway between active-active and active-standby</span></span>
<span data-ttu-id="64434-241">Hola última sección describe cómo puede configurar una puerta de enlace de VPN de Azure existente desde el modo de reserva activa tooactive activo, o viceversa.</span><span class="sxs-lookup"><span data-stu-id="64434-241">hello last section will describe how you can configure an existing Azure VPN gateway from active-standby tooactive-active mode, or vice versa.</span></span>

> [!NOTE]
> <span data-ttu-id="64434-242">Esta sección incluye Hola pasos tooresize una SKU heredada (SKU antigua) de una puerta de enlace VPN ya se ha creado de tooHighPerformance estándar.</span><span class="sxs-lookup"><span data-stu-id="64434-242">This section includes hello steps tooresize a legacy SKU (old SKU) of an already created VPN gateway from Standard tooHighPerformance.</span></span> <span data-ttu-id="64434-243">Estos pasos no actualizan un antiguo tooone heredado de SKU de hello SKU nuevo.</span><span class="sxs-lookup"><span data-stu-id="64434-243">These steps do not upgrade an old legacy SKU tooone of hello new SKUs.</span></span>
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a><span data-ttu-id="64434-244">Configurar una puerta de enlace de puerta de enlace de reserva activa tooactive activo</span><span class="sxs-lookup"><span data-stu-id="64434-244">Configure an active-standby gateway tooactive-active gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="64434-245">1. Parámetros de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="64434-245">1. Gateway parameters</span></span>
<span data-ttu-id="64434-246">Hola siguiente ejemplo convierte una puerta de enlace de reserva activa en una puerta de enlace de activo / activo.</span><span class="sxs-lookup"><span data-stu-id="64434-246">hello following example converts an active-standby gateway into an active-active gateway.</span></span> <span data-ttu-id="64434-247">Necesita toocreate otra dirección IP pública y luego agregar una segunda configuración IP de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="64434-247">You need toocreate another public IP address, then add a second Gateway IP configuration.</span></span> <span data-ttu-id="64434-248">A continuación se muestra hello utilizan parámetros:</span><span class="sxs-lookup"><span data-stu-id="64434-248">Below shows hello parameters used:</span></span>

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

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a><span data-ttu-id="64434-249">2. Crear dirección IP pública de Hola, a continuación, agregue la configuración de IP de puerta de enlace segundo Hola</span><span class="sxs-lookup"><span data-stu-id="64434-249">2. Create hello public IP address, then add hello second gateway IP configuration</span></span>

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a><span data-ttu-id="64434-250">3. Habilitar la puerta de enlace de Hola de modo y actualización de activo / activo</span><span class="sxs-lookup"><span data-stu-id="64434-250">3. Enable active-active mode and update hello gateway</span></span>
<span data-ttu-id="64434-251">Debe establecer el objeto de puerta de enlace de hello en actualización real de PowerShell tootrigger Hola.</span><span class="sxs-lookup"><span data-stu-id="64434-251">You must set hello gateway object in PowerShell tootrigger hello actual update.</span></span> <span data-ttu-id="64434-252">Hola SKU de puerta de enlace de red virtual de hello también se puede cambiar tooHighPerformance (cuyo tamaño ha cambiado) desde que se creó anteriormente como estándar.</span><span class="sxs-lookup"><span data-stu-id="64434-252">hello SKU of hello virtual network gateway must also be changed (resized) tooHighPerformance since it was created previously as Standard.</span></span>

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

<span data-ttu-id="64434-253">Esta actualización puede tardar 30 minutos de too45.</span><span class="sxs-lookup"><span data-stu-id="64434-253">This update can take 30 too45 minutes.</span></span>

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a><span data-ttu-id="64434-254">Configurar una puerta de enlace de tooactive el modo de espera de puerta de enlace de activo / activo</span><span class="sxs-lookup"><span data-stu-id="64434-254">Configure an active-active gateway tooactive-standby gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="64434-255">1. Parámetros de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="64434-255">1. Gateway parameters</span></span>
<span data-ttu-id="64434-256">Use Hola mismo parámetros que antes, obtener el nombre de Hola Hola de configuración de IP que desee tooremove.</span><span class="sxs-lookup"><span data-stu-id="64434-256">Use hello same parameters as above, get hello name of hello IP configuration you want tooremove.</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a><span data-ttu-id="64434-257">2. Quitar la configuración de IP de puerta de enlace de Hola y deshabilitar el modo activo / activo Hola</span><span class="sxs-lookup"><span data-stu-id="64434-257">2. Remove hello gateway IP configuration and disable hello active-active mode</span></span>
<span data-ttu-id="64434-258">De igual forma, debe establecer objeto de puerta de enlace de hello en actualización real de PowerShell tootrigger Hola.</span><span class="sxs-lookup"><span data-stu-id="64434-258">Similarly, you must set hello gateway object in PowerShell tootrigger hello actual update.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

<span data-ttu-id="64434-259">Esta actualización puede tardar hasta too30 demasiado 45 minutos.</span><span class="sxs-lookup"><span data-stu-id="64434-259">This update can take up too30 too 45 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64434-260">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="64434-260">Next steps</span></span>
<span data-ttu-id="64434-261">Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour.</span><span class="sxs-lookup"><span data-stu-id="64434-261">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="64434-262">Consulte [Creación de una máquina virtual que ejecuta Windows en el Portal de Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para ver los pasos.</span><span class="sxs-lookup"><span data-stu-id="64434-262">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
