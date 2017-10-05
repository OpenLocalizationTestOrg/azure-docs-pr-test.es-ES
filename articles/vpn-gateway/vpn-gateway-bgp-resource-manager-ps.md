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
ms.openlocfilehash: b00a3fe7ba4b12c2e9c486188c292cd6fafb60a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-bgp-on-azure-vpn-gateways-using-powershell"></a><span data-ttu-id="c4975-103">Configuración de BGP para Azure VPN Gateway con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4975-103">How to configure BGP on Azure VPN Gateways using PowerShell</span></span>
<span data-ttu-id="c4975-104">Este artículo le guiará por los pasos para habilitar BGP en una conexión de VPN de sitio a sitio (S2S) entre locales y una conexión de red virtual a red virtual mediante el modelo de implementación de Resource Manager y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4975-104">This article walks you through the steps to enable BGP on a cross-premises Site-to-Site (S2S) VPN connection and a VNet-to-VNet connection using the Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-bgp"></a><span data-ttu-id="c4975-105">Información acerca de BGP</span><span class="sxs-lookup"><span data-stu-id="c4975-105">About BGP</span></span>
<span data-ttu-id="c4975-106">BGP es el protocolo de enrutamiento estándar usado habitualmente en Internet para intercambiar información de enrutamiento y disponibilidad entre dos o más redes.</span><span class="sxs-lookup"><span data-stu-id="c4975-106">BGP is the standard routing protocol commonly used in the Internet to exchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="c4975-107">BGP permite que las puertas de enlace de VPN de Azure y los dispositivos VPN locales, denominados vecinos o pares BGP, intercambien "rutas" que comunicarán a ambas puertas de enlace la disponibilidad y la posibilidad de que dichos prefijos pasen a través de las puertas de enlace o los enrutadores implicados.</span><span class="sxs-lookup"><span data-stu-id="c4975-107">BGP enables the Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, to exchange "routes" that will inform both gateways on the availability and reachability for those prefixes to go through the gateways or routers involved.</span></span> <span data-ttu-id="c4975-108">BGP también puede permitir el enrutamiento del tránsito entre varias redes mediante la propagación de las rutas que una puerta de enlace de BGP aprende de un par BGP a todos los demás pares BGP.</span><span class="sxs-lookup"><span data-stu-id="c4975-108">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer to all other BGP peers.</span></span>

<span data-ttu-id="c4975-109">Para obtener más información sobre las ventajas de BGP, así como entender los requisitos técnicos y las consideraciones sobre el uso de BGP, consulte [Información general de BGP con Azure VPN Gateway](vpn-gateway-bgp-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c4975-109">See [Overview of BGP with Azure VPN Gateways](vpn-gateway-bgp-overview.md) for more discussion on benefits of BGP and to understand the technical requirements and considerations of using BGP.</span></span>

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a><span data-ttu-id="c4975-110">Introducción a BGP en puertas de enlace de VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="c4975-110">Getting started with BGP on Azure VPN gateways</span></span>

<span data-ttu-id="c4975-111">Este artículo lo guiará a través de los pasos necesarios para realizar las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="c4975-111">This article walks you through the steps to do the following tasks:</span></span>

* [<span data-ttu-id="c4975-112">Parte 1: Habilitar BGP en la puerta de enlace de VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="c4975-112">Part 1 - Enable BGP on your Azure VPN gateway</span></span>](#enablebgp)
* [<span data-ttu-id="c4975-113">Parte 2: Establecer una conexión entre locales con BGP</span><span class="sxs-lookup"><span data-stu-id="c4975-113">Part 2 - Establish a cross-premises connection with BGP</span></span>](#crossprembgp)
* [<span data-ttu-id="c4975-114">Parte 3: Establecer una conexión de red virtual a red virtual con BGP</span><span class="sxs-lookup"><span data-stu-id="c4975-114">Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>](#v2vbgp)

<span data-ttu-id="c4975-115">Cada parte de las instrucciones constituye un bloque de creación básico para habilitar BGP en la conectividad de red.</span><span class="sxs-lookup"><span data-stu-id="c4975-115">Each part of the instructions forms a basic building block for enabling BGP in your network connectivity.</span></span> <span data-ttu-id="c4975-116">Si completa las tres partes, podrá crear la topología tal como se muestra en el diagrama siguiente:</span><span class="sxs-lookup"><span data-stu-id="c4975-116">If you complete all three parts, you build the topology as shown in the following diagram:</span></span>

![Topología de BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

<span data-ttu-id="c4975-118">Puede combinar estos elementos juntos para crear una red de tránsito más compleja y de saltos múltiples que satisfaga sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="c4975-118">You can combine parts together to build a more complex, multi-hop, transit network that meets your needs.</span></span>

## <span data-ttu-id="c4975-119"><a name ="enablebgp"></a>Parte 1: Configurar BGP en la puerta de enlace de VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="c4975-119"><a name ="enablebgp"></a>Part 1 - Configure BGP on the Azure VPN Gateway</span></span>
<span data-ttu-id="c4975-120">Los siguientes pasos de configuración permiten establecer los parámetros BGP de Azure VPN Gateway como se muestra en el diagrama siguiente:</span><span class="sxs-lookup"><span data-stu-id="c4975-120">The configuration steps set up the BGP parameters of the Azure VPN gateway as shown in the following diagram:</span></span>

![Puerta de enlace de BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a><span data-ttu-id="c4975-122">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="c4975-122">Before you begin</span></span>
* <span data-ttu-id="c4975-123">Compruebe que tiene una suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="c4975-123">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="c4975-124">Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c4975-124">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c4975-125">Instale los cmdlets de PowerShell de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c4975-125">Install the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="c4975-126">Consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview) para más información sobre cómo instalar los cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4975-126">For more information about installing the PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="c4975-127">Paso 1: Creación y configuración de VNet1</span><span class="sxs-lookup"><span data-stu-id="c4975-127">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="c4975-128">1. Declaración de las variables</span><span class="sxs-lookup"><span data-stu-id="c4975-128">1. Declare your variables</span></span>
<span data-ttu-id="c4975-129">Para este ejercicio, se empieza por declarar las variables.</span><span class="sxs-lookup"><span data-stu-id="c4975-129">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="c4975-130">En este ejemplo se declaran las variables con los valores para este ejercicio.</span><span class="sxs-lookup"><span data-stu-id="c4975-130">The following example declares the variables using the values for this exercise.</span></span> <span data-ttu-id="c4975-131">Asegúrese de reemplazar los valores por los suyos propios cuando realice la configuración para el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c4975-131">Be sure to replace the values with your own when configuring for production.</span></span> <span data-ttu-id="c4975-132">Puede usar estas variables si está practicando los pasos para familiarizarse con este tipo de configuración.</span><span class="sxs-lookup"><span data-stu-id="c4975-132">You can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="c4975-133">Modifique las variables y después copie y pegue todo en la consola de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4975-133">Modify the variables, and then copy and paste into your PowerShell console.</span></span>

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

#### <a name="2-connect-to-your-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="c4975-134">2. Conexión a su suscripción y creación de un nuevo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c4975-134">2. Connect to your subscription and create a new resource group</span></span>
<span data-ttu-id="c4975-135">Para usar los cmdlets de Resource Manager, asegúrese de cambiar al modo de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4975-135">To use the Resource Manager cmdlets, Make sure you switch to PowerShell mode.</span></span> <span data-ttu-id="c4975-136">Para obtener más información, consulte [Uso de Windows PowerShell con el Administrador de recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="c4975-136">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="c4975-137">Abre la consola de PowerShell y conéctate a tu cuenta.</span><span class="sxs-lookup"><span data-stu-id="c4975-137">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="c4975-138">Use el siguiente ejemplo para ayudarle a conectarse:</span><span class="sxs-lookup"><span data-stu-id="c4975-138">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="c4975-139">3. Creación de TestVNet1</span><span class="sxs-lookup"><span data-stu-id="c4975-139">3. Create TestVNet1</span></span>
<span data-ttu-id="c4975-140">En el siguiente ejemplo se crea una red virtual denominada "TestVNet1" y tres subredes: GatewaySubnet, FrontEnd y Backend.</span><span class="sxs-lookup"><span data-stu-id="c4975-140">The following sample creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="c4975-141">Al reemplazar valores, es importante que siempre asigne el nombre GatewaySubnet a la subred de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="c4975-141">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="c4975-142">Si usa otro, se produce un error al crear la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="c4975-142">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-the-vpn-gateway-for-testvnet1-with-bgp-parameters"></a><span data-ttu-id="c4975-143">Paso 2: Creación de la puerta de enlace de VPN para TestVNet1 con parámetros BGP</span><span class="sxs-lookup"><span data-stu-id="c4975-143">Step 2 - Create the VPN Gateway for TestVNet1 with BGP parameters</span></span>
#### <a name="1-create-the-ip-and-subnet-configurations"></a><span data-ttu-id="c4975-144">1. Cree las configuraciones de IP y de subred</span><span class="sxs-lookup"><span data-stu-id="c4975-144">1. Create the IP and subnet configurations</span></span>
<span data-ttu-id="c4975-145">Solicite que se asigne una dirección IP pública a la puerta de enlace que creará para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="c4975-145">Request a public IP address to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="c4975-146">También definirá las configuraciones de subred y de IP necesarias.</span><span class="sxs-lookup"><span data-stu-id="c4975-146">You'll also define the required subnet and IP configurations.</span></span>

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-the-vpn-gateway-with-the-as-number"></a><span data-ttu-id="c4975-147">2. Cree la puerta de enlace de VPN con el número de AS</span><span class="sxs-lookup"><span data-stu-id="c4975-147">2. Create the VPN gateway with the AS number</span></span>
<span data-ttu-id="c4975-148">Cree la puerta de enlace de red virtual para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="c4975-148">Create the virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="c4975-149">BGP requiere una VPN Gateway basada en una ruta y también el parámetro de suma, - Asn, con el fin de establecer el ASN (número de AS) para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="c4975-149">BGP requires a Route-Based VPN gateway, and also the addition parameter, -Asn, to set the ASN (AS Number) for TestVNet1.</span></span> <span data-ttu-id="c4975-150">Si no establece el parámetro ASN, se asignará ASN 65515.</span><span class="sxs-lookup"><span data-stu-id="c4975-150">If you do not set the ASN parameter, ASN 65515 is assigned.</span></span> <span data-ttu-id="c4975-151">Se tardan unos 30 minutos o algo más en crear una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="c4975-151">Creating a gateway can take a while (30 minutes or more to complete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-the-azure-bgp-peer-ip-address"></a><span data-ttu-id="c4975-152">3. Obtenga la dirección IP del par BGP de Azure</span><span class="sxs-lookup"><span data-stu-id="c4975-152">3. Obtain the Azure BGP Peer IP address</span></span>
<span data-ttu-id="c4975-153">Una vez creada la puerta de enlace, debe obtener la dirección IP del par BGP en Azure VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="c4975-153">Once the gateway is created, you need to obtain the BGP Peer IP address on the Azure VPN Gateway.</span></span> <span data-ttu-id="c4975-154">Esta dirección es necesaria para configurar la puerta de enlace de VPN de Azure como par BGP para los dispositivos de VPN local.</span><span class="sxs-lookup"><span data-stu-id="c4975-154">This address is needed to configure the Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

<span data-ttu-id="c4975-155">El último comando mostrará las configuraciones de BGP correspondientes en Azure VPN Gateway; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c4975-155">The last command shows the corresponding BGP configurations on the Azure VPN Gateway; for example:</span></span>

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

<span data-ttu-id="c4975-156">Una vez creada la puerta de enlace, puede usar esta puerta de enlace para establecer conexión entre locales o conexión de red virtual a red virtual con BGP.</span><span class="sxs-lookup"><span data-stu-id="c4975-156">Once the gateway is created, you can use this gateway to establish cross-premises connection or VNet-to-VNet connection with BGP.</span></span> <span data-ttu-id="c4975-157">Las siguientes secciones lo guiarán por los pasos necesarios para completar el ejercicio.</span><span class="sxs-lookup"><span data-stu-id="c4975-157">The following sections walk through the steps to complete the exercise.</span></span>

## <span data-ttu-id="c4975-158"><a name ="crossprembbgp"></a>Parte 2: Establecer una conexión entre locales con BGP</span><span class="sxs-lookup"><span data-stu-id="c4975-158"><a name ="crossprembbgp"></a>Part 2 - Establish a cross-premises connection with BGP</span></span>

<span data-ttu-id="c4975-159">Para establecer una conexión entre locales, debe crear una puerta de enlace de red local para representar el dispositivo VPN local y una conexión para conectarse a VPN Gateway con la puerta de enlace de red local.</span><span class="sxs-lookup"><span data-stu-id="c4975-159">To establish a cross-premises connection, you need to create a Local Network Gateway to represent your on-premises VPN device, and a Connection to connect the VPN gateway with the local network gateway.</span></span> <span data-ttu-id="c4975-160">Aunque hay artículos que lo guiarán a través de estos pasos, este contiene las propiedades adicionales necesarias para especificar los parámetros de configuración de BGP.</span><span class="sxs-lookup"><span data-stu-id="c4975-160">While there are articles that walk you through these steps, this article contains the additional properties required to specify the BGP configuration parameters.</span></span>

![BGP entre locales](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

<span data-ttu-id="c4975-162">Antes de continuar, asegúrese de que ha completado la [parte 1](#enablebgp) de este ejercicio.</span><span class="sxs-lookup"><span data-stu-id="c4975-162">Before proceeding, make sure you have completed [Part 1](#enablebgp) of this exercise.</span></span>

### <a name="step-1---create-and-configure-the-local-network-gateway"></a><span data-ttu-id="c4975-163">Paso 1: Cree y configure la puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="c4975-163">Step 1 - Create and configure the local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="c4975-164">1. Declaración de las variables</span><span class="sxs-lookup"><span data-stu-id="c4975-164">1. Declare your variables</span></span>

<span data-ttu-id="c4975-165">Este ejercicio es continuación del paso de creación de la configuración mostrada en el diagrama.</span><span class="sxs-lookup"><span data-stu-id="c4975-165">This exercise continues to build the configuration shown in the diagram.</span></span> <span data-ttu-id="c4975-166">Asegúrese de reemplazar los valores por los que desea usar para su configuración.</span><span class="sxs-lookup"><span data-stu-id="c4975-166">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

<span data-ttu-id="c4975-167">Un par de cosas a tener en cuenta con respecto a los parámetros de la puerta de enlace de red local:</span><span class="sxs-lookup"><span data-stu-id="c4975-167">A couple of things to note regarding the local network gateway parameters:</span></span>

* <span data-ttu-id="c4975-168">La puerta de enlace de red local puede estar en la misma ubicación y grupo de recursos que la puerta de enlace de VPN o en otros distintos.</span><span class="sxs-lookup"><span data-stu-id="c4975-168">The local network gateway can be in the same or different location and resource group as the VPN gateway.</span></span> <span data-ttu-id="c4975-169">Este ejemplo los muestra en distintos grupos de recursos en diferentes ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="c4975-169">This example shows them in different resource groups in different locations.</span></span>
* <span data-ttu-id="c4975-170">El prefijo mínimo que debe declarar para la puerta de enlace de red local es la dirección del host de la dirección IP del par BGP en el dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="c4975-170">The minimum prefix you need to declare for the local network gateway is the host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="c4975-171">En este caso, es un prefijo /32 de "10.52.255.254/32".</span><span class="sxs-lookup"><span data-stu-id="c4975-171">In this case, it's a /32 prefix of "10.52.255.254/32".</span></span>
* <span data-ttu-id="c4975-172">Como recordatorio, debe usar diferentes ASN de BGP entre las redes locales y la red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="c4975-172">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="c4975-173">Si son iguales, tiene que cambiar el ASN de la red virtual si el dispositivo VPN local ya utiliza el ASN para emparejarse con otros vecinos de BGP.</span><span class="sxs-lookup"><span data-stu-id="c4975-173">If they are the same, you need to change your VNet ASN if your on-premises VPN device already uses the ASN to peer with other BGP neighbors.</span></span>

<span data-ttu-id="c4975-174">Antes de continuar, asegúrese de que sigue conectado a la suscripción 1.</span><span class="sxs-lookup"><span data-stu-id="c4975-174">Before you continue, make sure you are still connected to Subscription 1.</span></span>

#### <a name="2-create-the-local-network-gateway-for-site5"></a><span data-ttu-id="c4975-175">2. Cree las puertas de enlace de red local para Site5</span><span class="sxs-lookup"><span data-stu-id="c4975-175">2. Create the local network gateway for Site5</span></span>

<span data-ttu-id="c4975-176">Asegúrese de crear el grupo de recursos si no está ya creado, antes de crear la puerta de enlace de red local.</span><span class="sxs-lookup"><span data-stu-id="c4975-176">Be sure to create the resource group if it is not created, before you create the local network gateway.</span></span> <span data-ttu-id="c4975-177">Observe los dos parámetros adicionales para la puerta de enlace de red local: Asn y BgpPeerAddress.</span><span class="sxs-lookup"><span data-stu-id="c4975-177">Notice the two additional parameters for the local network gateway: Asn and BgpPeerAddress.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-the-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="c4975-178">Paso 2: Conecte la puerta de enlace de red virtual y la puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="c4975-178">Step 2 - Connect the VNet gateway and local network gateway</span></span>

#### <a name="1-get-the-two-gateways"></a><span data-ttu-id="c4975-179">1. Obtenga las dos puertas de enlace</span><span class="sxs-lookup"><span data-stu-id="c4975-179">1. Get the two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-the-testvnet1-to-site5-connection"></a><span data-ttu-id="c4975-180">2. Cree la conexión de TestVNet1 a Site5</span><span class="sxs-lookup"><span data-stu-id="c4975-180">2. Create the TestVNet1 to Site5 connection</span></span>

<span data-ttu-id="c4975-181">En este paso, creará la conexión de TestVNet1 a Site5.</span><span class="sxs-lookup"><span data-stu-id="c4975-181">In this step, you create the connection from TestVNet1 to Site5.</span></span> <span data-ttu-id="c4975-182">Debe especificar "-EnableBGP True" para habilitar BGP para esta conexión.</span><span class="sxs-lookup"><span data-stu-id="c4975-182">You must specify "-EnableBGP $True" to enable BGP for this connection.</span></span> <span data-ttu-id="c4975-183">Como se explicó anteriormente, es posible tener conexiones BGP y no BGP para la misma puerta de enlace de VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="c4975-183">As discussed earlier, it is possible to have both BGP and non-BGP connections for the same Azure VPN Gateway.</span></span> <span data-ttu-id="c4975-184">A menos que BGP esté habilitado en la propiedad de conexión, Azure no habilitará BGP para esta conexión, aunque los parámetros BGP ya estén configurados en ambas puertas de enlace.</span><span class="sxs-lookup"><span data-stu-id="c4975-184">Unless BGP is enabled in the connection property, Azure will not enable BGP for this connection even though BGP parameters are already configured on both gateways.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

<span data-ttu-id="c4975-185">En el ejemplo siguiente se enumeran los parámetros que deberá especificar en la sección de configuración de BGP en el dispositivo VPN local para este ejercicio:</span><span class="sxs-lookup"><span data-stu-id="c4975-185">The following example lists the parameters you enter into the BGP configuration section on your on-premises VPN device for this exercise:</span></span>

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being the VPN tunnel interface on your device
- eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="c4975-186">La conexión se establece después de unos minutos y se iniciará la sesión de emparejamiento BGP una vez establecida la conexión IPsec.</span><span class="sxs-lookup"><span data-stu-id="c4975-186">The connection is established after a few minutes, and the BGP peering session starts once the IPsec connection is established.</span></span>

## <span data-ttu-id="c4975-187"><a name ="v2vbgp"></a>Parte 3: Establecer una conexión de red virtual a red virtual con BGP</span><span class="sxs-lookup"><span data-stu-id="c4975-187"><a name ="v2vbgp"></a>Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>

<span data-ttu-id="c4975-188">En esta sección se agrega una conexión de red virtual a red virtual con BGP, tal como se muestra en el diagrama siguiente:</span><span class="sxs-lookup"><span data-stu-id="c4975-188">This section adds a VNet-to-VNet connection with BGP, as shown in the following diagram:</span></span>

![BGP para conexiones de red virtual a red virtual](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

<span data-ttu-id="c4975-190">Las siguientes instrucciones son continuación de los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="c4975-190">The following instructions continue from the previous steps.</span></span> <span data-ttu-id="c4975-191">Debe completar la [Parte 1](#enablebgp) para crear y configurar TestVNet1 y la puerta de enlace de VPN con BGP.</span><span class="sxs-lookup"><span data-stu-id="c4975-191">You must complete [Part I](#enablebgp) to create and configure TestVNet1 and the VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-the-vpn-gateway"></a><span data-ttu-id="c4975-192">Paso 1: cree TestVNet2 y la puerta de enlace de VPN</span><span class="sxs-lookup"><span data-stu-id="c4975-192">Step 1 - Create TestVNet2 and the VPN gateway</span></span>

<span data-ttu-id="c4975-193">Es importante asegurarse de que el espacio de direcciones IP de la red virtual nueva, TestVNet2, no se solape con ninguno de sus intervalos de red virtual.</span><span class="sxs-lookup"><span data-stu-id="c4975-193">It is important to make sure that the IP address space of the new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="c4975-194">En este ejemplo, las redes virtuales pertenecen a la misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="c4975-194">In this example, the virtual networks belong to the same subscription.</span></span> <span data-ttu-id="c4975-195">Se pueden configurar conexiones de red virtual a red virtual entre distintas suscripciones.</span><span class="sxs-lookup"><span data-stu-id="c4975-195">You can set up VNet-to-VNet connections between different subscriptions.</span></span> <span data-ttu-id="c4975-196">Para obtener más información, consulte [Configuración de una conexión de red virtual a red virtual](vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c4975-196">For more information, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> <span data-ttu-id="c4975-197">Asegúrese de agregar "-EnableBgp True" al crear las conexiones para habilitar BGP.</span><span class="sxs-lookup"><span data-stu-id="c4975-197">Make sure you add the "-EnableBgp $True" when creating the connections to enable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="c4975-198">1. Declaración de las variables</span><span class="sxs-lookup"><span data-stu-id="c4975-198">1. Declare your variables</span></span>

<span data-ttu-id="c4975-199">Asegúrese de reemplazar los valores por los que desea usar para su configuración.</span><span class="sxs-lookup"><span data-stu-id="c4975-199">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

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

#### <a name="2-create-testvnet2-in-the-new-resource-group"></a><span data-ttu-id="c4975-200">2. Cree TestVNet2 en el nuevo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c4975-200">2. Create TestVNet2 in the new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-the-vpn-gateway-for-testvnet2-with-bgp-parameters"></a><span data-ttu-id="c4975-201">3. Cree la puerta de enlace de VPN para TestVNet2 con parámetros BGP</span><span class="sxs-lookup"><span data-stu-id="c4975-201">3. Create the VPN gateway for TestVNet2 with BGP parameters</span></span>

<span data-ttu-id="c4975-202">Solicite que se asigne una dirección IP pública a la puerta de enlace que creará para la red virtual y defina las configuraciones de IP y subred requeridas.</span><span class="sxs-lookup"><span data-stu-id="c4975-202">Request a public IP address to be allocated to the gateway you will create for your VNet and define the required subnet and IP configurations.</span></span>

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

<span data-ttu-id="c4975-203">Cree la puerta de enlace de VPN con el número de AS.</span><span class="sxs-lookup"><span data-stu-id="c4975-203">Create the VPN gateway with the AS number.</span></span> <span data-ttu-id="c4975-204">Debe reemplazar el valor predeterminado del ASN en Azure VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="c4975-204">You must override the default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="c4975-205">Los ASN para las redes virtuales conectadas deben ser diferentes para habilitar el enrutamiento de tránsito y de BGP.</span><span class="sxs-lookup"><span data-stu-id="c4975-205">The ASNs for the connected VNets must be different to enable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-the-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="c4975-206">Paso 2: Conecte las puertas de enlace de TestVNet1 y TestVNet2</span><span class="sxs-lookup"><span data-stu-id="c4975-206">Step 2 - Connect the TestVNet1 and TestVNet2 gateways</span></span>

<span data-ttu-id="c4975-207">En este ejemplo, ambas puertas de enlace están en la misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="c4975-207">In this example, both gateways are in the same subscription.</span></span> <span data-ttu-id="c4975-208">Puede completar este paso en la misma sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4975-208">You can complete this step in the same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="c4975-209">1. Obtenga ambas puertas de enlace</span><span class="sxs-lookup"><span data-stu-id="c4975-209">1. Get both gateways</span></span>

<span data-ttu-id="c4975-210">Asegúrese de iniciar sesión y conectarse a la suscripción 1.</span><span class="sxs-lookup"><span data-stu-id="c4975-210">Make sure you log in and connect to Subscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="c4975-211">2. Cree ambas conexiones</span><span class="sxs-lookup"><span data-stu-id="c4975-211">2. Create both connections</span></span>

<span data-ttu-id="c4975-212">En este paso, creará la conexión de TestVNet1 a TestVNet2 y viceversa.</span><span class="sxs-lookup"><span data-stu-id="c4975-212">In this step, you create the connection from TestVNet1 to TestVNet2, and the connection from TestVNet2 to TestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="c4975-213">Asegúrese de habilitar BGP para AMBAS conexiones.</span><span class="sxs-lookup"><span data-stu-id="c4975-213">Be sure to enable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="c4975-214">Después de completar estos pasos, se establece la conexión después de unos minutos.</span><span class="sxs-lookup"><span data-stu-id="c4975-214">After completing these steps, the connection is established after a few minutes.</span></span> <span data-ttu-id="c4975-215">La sesión de emparejamiento BGP funcionará una vez completada la conexión de red virtual a red virtual.</span><span class="sxs-lookup"><span data-stu-id="c4975-215">The BGP peering session is up once the VNet-to-VNet connection is completed.</span></span>

<span data-ttu-id="c4975-216">Si ha completado las tres partes de este ejercicio, habrá establecido la siguiente topología de red:</span><span class="sxs-lookup"><span data-stu-id="c4975-216">If you completed all three parts of this exercise, you have established the following network topology:</span></span>

![BGP para conexiones de red virtual a red virtual](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a><span data-ttu-id="c4975-218">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c4975-218">Next steps</span></span>

<span data-ttu-id="c4975-219">Una vez completada la conexión, puede agregar máquinas virtuales a las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="c4975-219">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="c4975-220">Consulte [Creación de una máquina virtual que ejecuta Windows en el Portal de Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para ver los pasos.</span><span class="sxs-lookup"><span data-stu-id="c4975-220">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>