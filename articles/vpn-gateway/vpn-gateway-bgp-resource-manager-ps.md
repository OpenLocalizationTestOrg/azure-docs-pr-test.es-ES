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
# <a name="how-tooconfigure-bgp-on-azure-vpn-gateways-using-powershell"></a><span data-ttu-id="b3836-103">¿Cómo tooconfigure BGP en puertas de enlace de VPN de Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3836-103">How tooconfigure BGP on Azure VPN Gateways using PowerShell</span></span>
<span data-ttu-id="b3836-104">Este artículo le guiará a través de hello pasos tooenable BGP en una conexión de VPN de sitio a sitio (S2S) entre entornos y una conexión de red virtual a red virtual con el modelo de implementación del Administrador de recursos de Hola y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3836-104">This article walks you through hello steps tooenable BGP on a cross-premises Site-to-Site (S2S) VPN connection and a VNet-to-VNet connection using hello Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-bgp"></a><span data-ttu-id="b3836-105">Información acerca de BGP</span><span class="sxs-lookup"><span data-stu-id="b3836-105">About BGP</span></span>
<span data-ttu-id="b3836-106">BGP es frecuente en hello tooexchange enrutamiento y alcance de la información de Internet entre dos o más redes de protocolo de enrutamiento estándar Hola.</span><span class="sxs-lookup"><span data-stu-id="b3836-106">BGP is hello standard routing protocol commonly used in hello Internet tooexchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="b3836-107">BGP permite puertas de enlace de VPN de Azure de Hola y los dispositivos VPN local, que se llama a los pares BGP o a los vecinos, tooexchange "enruta" que le informará de las puertas de enlace en la disponibilidad de Hola y accesibilidad de los prefijos toogo a través de las puertas de enlace de Hola o enrutadores implicados.</span><span class="sxs-lookup"><span data-stu-id="b3836-107">BGP enables hello Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, tooexchange "routes" that will inform both gateways on hello availability and reachability for those prefixes toogo through hello gateways or routers involved.</span></span> <span data-ttu-id="b3836-108">BGP también puede habilitar el enrutamiento del tránsito entre varias redes mediante la propagación de las rutas de una puerta de enlace BGP aprende desde una BGP del mismo nivel tooall otros pares BGP.</span><span class="sxs-lookup"><span data-stu-id="b3836-108">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer tooall other BGP peers.</span></span>

<span data-ttu-id="b3836-109">Vea [información general de BGP con puertas de enlace de VPN de Azure](vpn-gateway-bgp-overview.md) para obtener más información sobre los beneficios de BGP y toounderstand requisitos técnicos de Hola y consideraciones de uso de BGP.</span><span class="sxs-lookup"><span data-stu-id="b3836-109">See [Overview of BGP with Azure VPN Gateways](vpn-gateway-bgp-overview.md) for more discussion on benefits of BGP and toounderstand hello technical requirements and considerations of using BGP.</span></span>

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a><span data-ttu-id="b3836-110">Introducción a BGP en puertas de enlace de VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="b3836-110">Getting started with BGP on Azure VPN gateways</span></span>

<span data-ttu-id="b3836-111">Este artículo le guiará a través de Hola Hola de toodo pasos siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="b3836-111">This article walks you through hello steps toodo hello following tasks:</span></span>

* [<span data-ttu-id="b3836-112">Parte 1: Habilitar BGP en la puerta de enlace de VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="b3836-112">Part 1 - Enable BGP on your Azure VPN gateway</span></span>](#enablebgp)
* [<span data-ttu-id="b3836-113">Parte 2: Establecer una conexión entre locales con BGP</span><span class="sxs-lookup"><span data-stu-id="b3836-113">Part 2 - Establish a cross-premises connection with BGP</span></span>](#crossprembgp)
* [<span data-ttu-id="b3836-114">Parte 3: Establecer una conexión de red virtual a red virtual con BGP</span><span class="sxs-lookup"><span data-stu-id="b3836-114">Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>](#v2vbgp)

<span data-ttu-id="b3836-115">Cada parte de instrucciones de hello constituye una piedra angular para habilitar BGP en la conectividad de red.</span><span class="sxs-lookup"><span data-stu-id="b3836-115">Each part of hello instructions forms a basic building block for enabling BGP in your network connectivity.</span></span> <span data-ttu-id="b3836-116">Si completa todas las tres partes, generar topología Hola tal como se muestra en hello siguiente diagrama:</span><span class="sxs-lookup"><span data-stu-id="b3836-116">If you complete all three parts, you build hello topology as shown in hello following diagram:</span></span>

![Topología de BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

<span data-ttu-id="b3836-118">Puede combinar elementos juntos toobuild una red de tránsito más complejos y de múltiples saltos, que satisfaga sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="b3836-118">You can combine parts together toobuild a more complex, multi-hop, transit network that meets your needs.</span></span>

## <span data-ttu-id="b3836-119"><a name ="enablebgp"></a>Parte 1: configurar BGP en hello puerta de enlace de VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="b3836-119"><a name ="enablebgp"></a>Part 1 - Configure BGP on hello Azure VPN Gateway</span></span>
<span data-ttu-id="b3836-120">pasos de configuración de Hello configurar Hola parámetros BGP de puerta de enlace de VPN de Azure de hello como se muestra en hello siguiente diagrama:</span><span class="sxs-lookup"><span data-stu-id="b3836-120">hello configuration steps set up hello BGP parameters of hello Azure VPN gateway as shown in hello following diagram:</span></span>

![Puerta de enlace de BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a><span data-ttu-id="b3836-122">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="b3836-122">Before you begin</span></span>
* <span data-ttu-id="b3836-123">Compruebe que tiene una suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="b3836-123">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="b3836-124">Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b3836-124">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b3836-125">Instalar cmdlets de PowerShell del Administrador de recursos de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3836-125">Install hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="b3836-126">Para obtener más información acerca de cómo instalar los cmdlets de PowerShell de hello, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b3836-126">For more information about installing hello PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="b3836-127">Paso 1: Creación y configuración de VNet1</span><span class="sxs-lookup"><span data-stu-id="b3836-127">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="b3836-128">1. Declaración de las variables</span><span class="sxs-lookup"><span data-stu-id="b3836-128">1. Declare your variables</span></span>
<span data-ttu-id="b3836-129">Para este ejercicio, se empieza por declarar las variables.</span><span class="sxs-lookup"><span data-stu-id="b3836-129">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="b3836-130">Hello en el ejemplo siguiente se declara las variables de hello con valores de hello para este ejercicio.</span><span class="sxs-lookup"><span data-stu-id="b3836-130">hello following example declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="b3836-131">Ser seguro de valores de hello tooreplace con su propio cuando se configura para la producción.</span><span class="sxs-lookup"><span data-stu-id="b3836-131">Be sure tooreplace hello values with your own when configuring for production.</span></span> <span data-ttu-id="b3836-132">Puede utilizar estas variables si está ejecutando a través de hello pasos toobecome familiarizado con este tipo de configuración.</span><span class="sxs-lookup"><span data-stu-id="b3836-132">You can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="b3836-133">Modificar variables de hello y, a continuación, copie y pegue en la consola de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3836-133">Modify hello variables, and then copy and paste into your PowerShell console.</span></span>

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="b3836-134">2. Conectar tooyour suscripción y crear un nuevo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b3836-134">2. Connect tooyour subscription and create a new resource group</span></span>
<span data-ttu-id="b3836-135">Hola toouse cmdlets del Administrador de recursos, asegúrese de cambiar el modo de tooPowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3836-135">toouse hello Resource Manager cmdlets, Make sure you switch tooPowerShell mode.</span></span> <span data-ttu-id="b3836-136">Para obtener más información, consulte [Uso de Windows PowerShell con el Administrador de recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b3836-136">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="b3836-137">Abra la consola de PowerShell y conectar con tooyour cuenta.</span><span class="sxs-lookup"><span data-stu-id="b3836-137">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="b3836-138">Usar hello después toohelp de ejemplo que conectarse:</span><span class="sxs-lookup"><span data-stu-id="b3836-138">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="b3836-139">3. Creación de TestVNet1</span><span class="sxs-lookup"><span data-stu-id="b3836-139">3. Create TestVNet1</span></span>
<span data-ttu-id="b3836-140">Hello en el ejemplo siguiente crea una red virtual denominada TestVNet1 y tres subredes, un GatewaySubnet llamado, uno llamado front-end y un back-end de llamada.</span><span class="sxs-lookup"><span data-stu-id="b3836-140">hello following sample creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="b3836-141">Al reemplazar valores, es importante que siempre asigne el nombre GatewaySubnet a la subred de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="b3836-141">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="b3836-142">Si usa otro, se produce un error al crear la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="b3836-142">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-bgp-parameters"></a><span data-ttu-id="b3836-143">Paso 2: crear Hola puerta de enlace VPN para TestVNet1 con parámetros BGP</span><span class="sxs-lookup"><span data-stu-id="b3836-143">Step 2 - Create hello VPN Gateway for TestVNet1 with BGP parameters</span></span>
#### <a name="1-create-hello-ip-and-subnet-configurations"></a><span data-ttu-id="b3836-144">1. Crear configuraciones de IP y una subred de Hola</span><span class="sxs-lookup"><span data-stu-id="b3836-144">1. Create hello IP and subnet configurations</span></span>
<span data-ttu-id="b3836-145">Solicitar una pública dirección toobe toohello asignado puerta de enlace IP que creará para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="b3836-145">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="b3836-146">También definirá las configuraciones IP y subred Hola necesario.</span><span class="sxs-lookup"><span data-stu-id="b3836-146">You'll also define hello required subnet and IP configurations.</span></span>

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-hello-vpn-gateway-with-hello-as-number"></a><span data-ttu-id="b3836-147">2. Crear puerta de enlace VPN de hello con hello como número</span><span class="sxs-lookup"><span data-stu-id="b3836-147">2. Create hello VPN gateway with hello AS number</span></span>
<span data-ttu-id="b3836-148">Crear puerta de enlace de red virtual de Hola para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="b3836-148">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="b3836-149">BGP requiere un basadas en enrutamiento puerta de enlace VPN y también Hola suma parámetro, - Asn tooset Hola ASN (número de AS) para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="b3836-149">BGP requires a Route-Based VPN gateway, and also hello addition parameter, -Asn, tooset hello ASN (AS Number) for TestVNet1.</span></span> <span data-ttu-id="b3836-150">Si no establece el parámetro ASN hello, se asigna ASN 65515.</span><span class="sxs-lookup"><span data-stu-id="b3836-150">If you do not set hello ASN parameter, ASN 65515 is assigned.</span></span> <span data-ttu-id="b3836-151">Crear una puerta de enlace puede tardar un tiempo (30 minutos o más toocomplete).</span><span class="sxs-lookup"><span data-stu-id="b3836-151">Creating a gateway can take a while (30 minutes or more toocomplete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-hello-azure-bgp-peer-ip-address"></a><span data-ttu-id="b3836-152">3. Obtener dirección IP de Azure BGP del mismo nivel de Hola</span><span class="sxs-lookup"><span data-stu-id="b3836-152">3. Obtain hello Azure BGP Peer IP address</span></span>
<span data-ttu-id="b3836-153">Una vez creada la puerta de enlace de hello, necesita tooobtain Hola BGP del mismo nivel IP dirección en hello puerta de enlace de VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3836-153">Once hello gateway is created, you need tooobtain hello BGP Peer IP address on hello Azure VPN Gateway.</span></span> <span data-ttu-id="b3836-154">Esta dirección es necesario tooconfigure Hola puerta de enlace de VPN de Azure como un par BGP para los dispositivos VPN local.</span><span class="sxs-lookup"><span data-stu-id="b3836-154">This address is needed tooconfigure hello Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

<span data-ttu-id="b3836-155">último comando de Hello muestra configuraciones de BGP correspondientes de hello en hello puerta de enlace de VPN de Azure; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b3836-155">hello last command shows hello corresponding BGP configurations on hello Azure VPN Gateway; for example:</span></span>

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

<span data-ttu-id="b3836-156">Una vez creada la puerta de enlace de hello, puede usar esta conexión de puerta de enlace tooestablish entre entornos o conexión de red virtual a red virtual con BGP.</span><span class="sxs-lookup"><span data-stu-id="b3836-156">Once hello gateway is created, you can use this gateway tooestablish cross-premises connection or VNet-to-VNet connection with BGP.</span></span> <span data-ttu-id="b3836-157">Hello en las siguientes secciones se abordan Hola pasos toocomplete Hola ejercicio.</span><span class="sxs-lookup"><span data-stu-id="b3836-157">hello following sections walk through hello steps toocomplete hello exercise.</span></span>

## <span data-ttu-id="b3836-158"><a name ="crossprembbgp"></a>Parte 2: Establecer una conexión entre locales con BGP</span><span class="sxs-lookup"><span data-stu-id="b3836-158"><a name ="crossprembbgp"></a>Part 2 - Establish a cross-premises connection with BGP</span></span>

<span data-ttu-id="b3836-159">tooestablish una conexión entre entornos, necesita una puerta de enlace de red Local toorepresent toocreate dispositivo VPN local y una puerta de enlace de conexión tooconnect Hola VPN con puerta de enlace de red local de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3836-159">tooestablish a cross-premises connection, you need toocreate a Local Network Gateway toorepresent your on-premises VPN device, and a Connection tooconnect hello VPN gateway with hello local network gateway.</span></span> <span data-ttu-id="b3836-160">Aunque hay artículos que le guiarán a través de estos pasos, este artículo contiene parámetros de configuración de BGP de Hola de hello propiedades adicionales toospecify necesarios.</span><span class="sxs-lookup"><span data-stu-id="b3836-160">While there are articles that walk you through these steps, this article contains hello additional properties required toospecify hello BGP configuration parameters.</span></span>

![BGP entre locales](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

<span data-ttu-id="b3836-162">Antes de continuar, asegúrese de que ha completado la [parte 1](#enablebgp) de este ejercicio.</span><span class="sxs-lookup"><span data-stu-id="b3836-162">Before proceeding, make sure you have completed [Part 1](#enablebgp) of this exercise.</span></span>

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a><span data-ttu-id="b3836-163">Paso 1: crear y configurar la puerta de enlace de red local de Hola</span><span class="sxs-lookup"><span data-stu-id="b3836-163">Step 1 - Create and configure hello local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="b3836-164">1. Declaración de las variables</span><span class="sxs-lookup"><span data-stu-id="b3836-164">1. Declare your variables</span></span>

<span data-ttu-id="b3836-165">Este ejercicio continúa toobuild configuración de Hola que se muestra en el diagrama de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3836-165">This exercise continues toobuild hello configuration shown in hello diagram.</span></span> <span data-ttu-id="b3836-166">Ser seguro tooreplace valores de hello con hello las que desea que toouse para la configuración.</span><span class="sxs-lookup"><span data-stu-id="b3836-166">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

<span data-ttu-id="b3836-167">Un par de cosas toonote con respecto a los parámetros de puerta de enlace de red local de hello:</span><span class="sxs-lookup"><span data-stu-id="b3836-167">A couple of things toonote regarding hello local network gateway parameters:</span></span>

* <span data-ttu-id="b3836-168">puerta de enlace de red local de Hello puede estar en Hola iguales o diferentes y ubicación de recurso de grupo como Hola puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="b3836-168">hello local network gateway can be in hello same or different location and resource group as hello VPN gateway.</span></span> <span data-ttu-id="b3836-169">Este ejemplo los muestra en distintos grupos de recursos en diferentes ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="b3836-169">This example shows them in different resource groups in different locations.</span></span>
* <span data-ttu-id="b3836-170">prefijo mínima Hola necesita toodeclare para puerta de enlace de red local de hello es la dirección de host de Hola de su dirección IP de BGP del mismo nivel en el dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="b3836-170">hello minimum prefix you need toodeclare for hello local network gateway is hello host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="b3836-171">En este caso, es un prefijo /32 de "10.52.255.254/32".</span><span class="sxs-lookup"><span data-stu-id="b3836-171">In this case, it's a /32 prefix of "10.52.255.254/32".</span></span>
* <span data-ttu-id="b3836-172">Como recordatorio, debe usar diferentes ASN de BGP entre las redes locales y la red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3836-172">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="b3836-173">Si se hello mismo, deberá toochange el ASN VNet si el dispositivo VPN local ya utiliza Hola ASN toopeer con otros vecinos BGP.</span><span class="sxs-lookup"><span data-stu-id="b3836-173">If they are hello same, you need toochange your VNet ASN if your on-premises VPN device already uses hello ASN toopeer with other BGP neighbors.</span></span>

<span data-ttu-id="b3836-174">Antes de continuar, asegúrese de que está conectado aún tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="b3836-174">Before you continue, make sure you are still connected tooSubscription 1.</span></span>

#### <a name="2-create-hello-local-network-gateway-for-site5"></a><span data-ttu-id="b3836-175">2. Crear puerta de enlace de red local de Hola para Site5</span><span class="sxs-lookup"><span data-stu-id="b3836-175">2. Create hello local network gateway for Site5</span></span>

<span data-ttu-id="b3836-176">Estar seguro de grupo de recursos de hello toocreate si no se creó, antes de crear la puerta de enlace de red local de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3836-176">Be sure toocreate hello resource group if it is not created, before you create hello local network gateway.</span></span> <span data-ttu-id="b3836-177">Observe Hola dos parámetros adicionales para la puerta de enlace de red local de hello: Asn y BgpPeerAddress.</span><span class="sxs-lookup"><span data-stu-id="b3836-177">Notice hello two additional parameters for hello local network gateway: Asn and BgpPeerAddress.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="b3836-178">Paso 2: conectar la puerta de enlace de red virtual de Hola y puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="b3836-178">Step 2 - Connect hello VNet gateway and local network gateway</span></span>

#### <a name="1-get-hello-two-gateways"></a><span data-ttu-id="b3836-179">1. Obtener Hola dos puertas de enlace</span><span class="sxs-lookup"><span data-stu-id="b3836-179">1. Get hello two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a><span data-ttu-id="b3836-180">2. Crear conexiones de hello TestVNet1 tooSite5</span><span class="sxs-lookup"><span data-stu-id="b3836-180">2. Create hello TestVNet1 tooSite5 connection</span></span>

<span data-ttu-id="b3836-181">En este paso, se crea la conexión de Hola de TestVNet1 tooSite5.</span><span class="sxs-lookup"><span data-stu-id="b3836-181">In this step, you create hello connection from TestVNet1 tooSite5.</span></span> <span data-ttu-id="b3836-182">Debe especificar "-EnableBGP $True" tooenable BGP para esta conexión.</span><span class="sxs-lookup"><span data-stu-id="b3836-182">You must specify "-EnableBGP $True" tooenable BGP for this connection.</span></span> <span data-ttu-id="b3836-183">Tal y como se indicó anteriormente, es posible toohave conexiones BGP y no BGP en Hola misma puerta de enlace de VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3836-183">As discussed earlier, it is possible toohave both BGP and non-BGP connections for hello same Azure VPN Gateway.</span></span> <span data-ttu-id="b3836-184">A menos que el BGP está habilitado en la propiedad de conexión de hello, Azure no habilitará BGP para esta conexión, aunque los parámetros BGP ya están configuradas en las puertas de enlace.</span><span class="sxs-lookup"><span data-stu-id="b3836-184">Unless BGP is enabled in hello connection property, Azure will not enable BGP for this connection even though BGP parameters are already configured on both gateways.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

<span data-ttu-id="b3836-185">Hello en el ejemplo siguiente se enumera los parámetros de hello que escriba en la sección de configuración de BGP de hello en dispositivo VPN local para este ejercicio:</span><span class="sxs-lookup"><span data-stu-id="b3836-185">hello following example lists hello parameters you enter into hello BGP configuration section on your on-premises VPN device for this exercise:</span></span>

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being hello VPN tunnel interface on your device
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="b3836-186">una vez establecida la conexión IPsec hello, se establece conexión de Hello después de unos minutos y se inicia sesión BGP emparejamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="b3836-186">hello connection is established after a few minutes, and hello BGP peering session starts once hello IPsec connection is established.</span></span>

## <span data-ttu-id="b3836-187"><a name ="v2vbgp"></a>Parte 3: Establecer una conexión de red virtual a red virtual con BGP</span><span class="sxs-lookup"><span data-stu-id="b3836-187"><a name ="v2vbgp"></a>Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>

<span data-ttu-id="b3836-188">En esta sección se agrega una conexión de red virtual a red virtual con BGP, como se muestra en hello siguiente diagrama:</span><span class="sxs-lookup"><span data-stu-id="b3836-188">This section adds a VNet-to-VNet connection with BGP, as shown in hello following diagram:</span></span>

![BGP para conexiones de red virtual a red virtual](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

<span data-ttu-id="b3836-190">continuar Hola siguiendo las instrucciones de los pasos anteriores de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3836-190">hello following instructions continue from hello previous steps.</span></span> <span data-ttu-id="b3836-191">Debe completar [parte I](#enablebgp) toocreate TestVNet1 y configurar Hola puerta de enlace de VPN con BGP.</span><span class="sxs-lookup"><span data-stu-id="b3836-191">You must complete [Part I](#enablebgp) toocreate and configure TestVNet1 and hello VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a><span data-ttu-id="b3836-192">Paso 1: crear la puerta de enlace VPN de hello y TestVNet2</span><span class="sxs-lookup"><span data-stu-id="b3836-192">Step 1 - Create TestVNet2 and hello VPN gateway</span></span>

<span data-ttu-id="b3836-193">Es importante toomake seguro de que el espacio de direcciones IP de Hola de hello nueva red virtual, TestVNet2, no se superponen con ninguno de los intervalos de red virtual.</span><span class="sxs-lookup"><span data-stu-id="b3836-193">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="b3836-194">En este ejemplo, redes virtuales de hello pertenecen toohello misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="b3836-194">In this example, hello virtual networks belong toohello same subscription.</span></span> <span data-ttu-id="b3836-195">Se pueden configurar conexiones de red virtual a red virtual entre distintas suscripciones.</span><span class="sxs-lookup"><span data-stu-id="b3836-195">You can set up VNet-to-VNet connections between different subscriptions.</span></span> <span data-ttu-id="b3836-196">Para obtener más información, consulte [Configuración de una conexión de red virtual a red virtual](vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b3836-196">For more information, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> <span data-ttu-id="b3836-197">Asegúrese de agregar Hola "-EnableBgp $True" al crear Hola conexiones tooenable BGP.</span><span class="sxs-lookup"><span data-stu-id="b3836-197">Make sure you add hello "-EnableBgp $True" when creating hello connections tooenable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="b3836-198">1. Declaración de las variables</span><span class="sxs-lookup"><span data-stu-id="b3836-198">1. Declare your variables</span></span>

<span data-ttu-id="b3836-199">Ser seguro tooreplace valores de hello con hello las que desea que toouse para la configuración.</span><span class="sxs-lookup"><span data-stu-id="b3836-199">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

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

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a><span data-ttu-id="b3836-200">2. Crear TestVNet2 Hola nuevo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b3836-200">2. Create TestVNet2 in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-vpn-gateway-for-testvnet2-with-bgp-parameters"></a><span data-ttu-id="b3836-201">3. Crear puerta de enlace VPN de Hola para TestVNet2 con parámetros BGP</span><span class="sxs-lookup"><span data-stu-id="b3836-201">3. Create hello VPN gateway for TestVNet2 with BGP parameters</span></span>

<span data-ttu-id="b3836-202">Solicitar una pública dirección toobe toohello asignado puerta de enlace IP creará para la red virtual y definir configuraciones de IP y subred Hola necesario.</span><span class="sxs-lookup"><span data-stu-id="b3836-202">Request a public IP address toobe allocated toohello gateway you will create for your VNet and define hello required subnet and IP configurations.</span></span>

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

<span data-ttu-id="b3836-203">Crear puerta de enlace VPN de hello con hello como número.</span><span class="sxs-lookup"><span data-stu-id="b3836-203">Create hello VPN gateway with hello AS number.</span></span> <span data-ttu-id="b3836-204">Debe reemplazar predeterminado Hola ASN en las puertas de enlace de VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3836-204">You must override hello default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="b3836-205">Hola ASN para hello conectado las redes virtuales debe ser diferente tooenable BGP y el enrutamiento de tránsito.</span><span class="sxs-lookup"><span data-stu-id="b3836-205">hello ASNs for hello connected VNets must be different tooenable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="b3836-206">Paso 2: conectar hello TestVNet1 y TestVNet2 puertas de enlace</span><span class="sxs-lookup"><span data-stu-id="b3836-206">Step 2 - Connect hello TestVNet1 and TestVNet2 gateways</span></span>

<span data-ttu-id="b3836-207">En este ejemplo, las puertas de enlace se encuentran en hello misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="b3836-207">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="b3836-208">Puede completar este paso en hello misma sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3836-208">You can complete this step in hello same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="b3836-209">1. Obtenga ambas puertas de enlace</span><span class="sxs-lookup"><span data-stu-id="b3836-209">1. Get both gateways</span></span>

<span data-ttu-id="b3836-210">Asegúrese de que inicie sesión y conectarse tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="b3836-210">Make sure you log in and connect tooSubscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="b3836-211">2. Cree ambas conexiones</span><span class="sxs-lookup"><span data-stu-id="b3836-211">2. Create both connections</span></span>

<span data-ttu-id="b3836-212">En este paso, creará conexión Hola de TestVNet1 tooTestVNet2 y conexión de Hola de TestVNet2 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="b3836-212">In this step, you create hello connection from TestVNet1 tooTestVNet2, and hello connection from TestVNet2 tooTestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="b3836-213">Ser seguro tooenable BGP para las conexiones de ambos.</span><span class="sxs-lookup"><span data-stu-id="b3836-213">Be sure tooenable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="b3836-214">Después de completar estos pasos, se establece la conexión de hello después de unos minutos.</span><span class="sxs-lookup"><span data-stu-id="b3836-214">After completing these steps, hello connection is established after a few minutes.</span></span> <span data-ttu-id="b3836-215">sesión de emparejamiento de BGP Hola está activo cuando se haya completado Hola conexión de red virtual a red virtual.</span><span class="sxs-lookup"><span data-stu-id="b3836-215">hello BGP peering session is up once hello VNet-to-VNet connection is completed.</span></span>

<span data-ttu-id="b3836-216">Si ha completado las tres partes de este ejercicio, han establecido Hola después de la topología de red:</span><span class="sxs-lookup"><span data-stu-id="b3836-216">If you completed all three parts of this exercise, you have established hello following network topology:</span></span>

![BGP para conexiones de red virtual a red virtual](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a><span data-ttu-id="b3836-218">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b3836-218">Next steps</span></span>

<span data-ttu-id="b3836-219">Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour.</span><span class="sxs-lookup"><span data-stu-id="b3836-219">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="b3836-220">Consulte [Creación de una máquina virtual que ejecuta Windows en el Portal de Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para ver los pasos.</span><span class="sxs-lookup"><span data-stu-id="b3836-220">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
