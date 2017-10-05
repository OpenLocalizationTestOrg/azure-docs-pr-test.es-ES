---
title: "Configuración de la tunelización forzada para conexiones de sitio a sitio de Azure: Resource Manager | Microsoft Docs"
description: "Cómo redirigir o forzar todo el tráfico vinculado a Internet a la ubicación local."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cbe58db8-b598-4c9f-ac88-62c865eb8721
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 207c53924863eb51ee369fe46d5ad12fb1905c53
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="configure-forced-tunneling-using-the-azure-resource-manager-deployment-model"></a><span data-ttu-id="8e4d1-103">Configuración de la tunelización forzada mediante el modelo de implementación de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8e4d1-103">Configure forced tunneling using the Azure Resource Manager deployment model</span></span>

<span data-ttu-id="8e4d1-104">La tunelización forzada permite redirigir o forzar todo el tráfico vinculado a Internet de vuelta a su ubicación local a través de un túnel VPN de sitio a sitio para inspección y auditoría.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="8e4d1-105">Se trata de un requisito de seguridad crítico en la mayoría de las directivas de las empresas de TI.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="8e4d1-106">Sin la tunelización forzada, el tráfico vinculado a Internet desde las máquinas virtuales en Azure siempre atravesará desde la infraestructura de red de Azure directamente a Internet, sin la opción que permite inspeccionar o auditar el tráfico.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure always traverses from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span></span> <span data-ttu-id="8e4d1-107">Un acceso no autorizado a Internet puede provocar la divulgación de información u otros tipos de infracciones de seguridad.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-107">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

<span data-ttu-id="8e4d1-108">Este artículo lo guiará a través del proceso de configuración de la tunelización forzada para redes virtuales creadas mediante el modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-108">This article walks you through configuring forced tunneling for virtual networks created using the Resource Manager deployment model.</span></span> <span data-ttu-id="8e4d1-109">La tunelización forzada puede configurarse mediante el uso de PowerShell, no a través del portal.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-109">Forced tunneling can be configured by using PowerShell, not through the portal.</span></span> <span data-ttu-id="8e4d1-110">Si desea configurar la tunelización forzada para el modelo de implementación clásica, seleccione el artículo clásico de la lista desplegable siguiente:</span><span class="sxs-lookup"><span data-stu-id="8e4d1-110">If you want to configure forced tunneling for the classic deployment model, select classic article from the following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8e4d1-111">PowerShell: clásico</span><span class="sxs-lookup"><span data-stu-id="8e4d1-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="8e4d1-112">PowerShell: administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="8e4d1-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a><span data-ttu-id="8e4d1-113">Información acerca de la tunelización forzada</span><span class="sxs-lookup"><span data-stu-id="8e4d1-113">About forced tunneling</span></span>

<span data-ttu-id="8e4d1-114">El siguiente diagrama ilustra cómo funciona la tunelización forzada.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-114">The following diagram illustrates how forced tunneling works.</span></span> 

![Tunelización forzada](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

<span data-ttu-id="8e4d1-116">En el ejemplo anterior, la subred Frontend no usa la tunelización forzada.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-116">In the example above, the Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="8e4d1-117">Las cargas de trabajo de la subred Frontend pueden continuar para aceptar y responder a las solicitudes de los clientes directamente desde Internet.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-117">The workloads in the Frontend subnet can continue to accept and respond to customer requests from the Internet directly.</span></span> <span data-ttu-id="8e4d1-118">Las subredes Mid-tier y Backend usan la tunelización forzada.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-118">The Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="8e4d1-119">Las conexiones salientes desde estas dos subredes a Internet se fuerzan o redirigen a un sitio local a través de uno de los túneles VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-119">Any outbound connections from these two subnets to the Internet will be forced or redirected back to an on-premises site via one of the S2S VPN tunnels.</span></span>

<span data-ttu-id="8e4d1-120">Esto permite restringir e inspeccionar el acceso a Internet desde sus máquinas virtuales o servicios en la nube en Azure, al tiempo que continúa posibilitando la arquitectura de varios niveles de servicio necesaria.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-120">This allows you to restrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing to enable your multi-tier service architecture required.</span></span> <span data-ttu-id="8e4d1-121">Si no hay ninguna carga de trabajo a través de Internet en las redes virtuales, también tiene la opción de aplicar la tunelización forzada a redes virtuales completas.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-121">If there are no Internet-facing workloads in your virtual networks, you also can apply forced tunneling to the entire virtual networks.</span></span>

## <a name="requirements-and-considerations"></a><span data-ttu-id="8e4d1-122">Requisitos y consideraciones</span><span class="sxs-lookup"><span data-stu-id="8e4d1-122">Requirements and considerations</span></span>

<span data-ttu-id="8e4d1-123">La tunelización forzada en Azure se configura a través de rutas definidas por el usuario de redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-123">Forced tunneling in Azure is configured via virtual network user-defined routes.</span></span> <span data-ttu-id="8e4d1-124">La redirección del tráfico a un sitio local se expresa como una ruta predeterminada a la puerta de enlace de VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-124">Redirecting traffic to an on-premises site is expressed as a Default Route to the Azure VPN gateway.</span></span> <span data-ttu-id="8e4d1-125">Para obtener más información sobre las redes virtuales y las rutas definidas por el usuario, consulte [Rutas definidas por el usuario y reenvío IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8e4d1-125">For more information about user-defined routing and virtual networks, see [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>

* <span data-ttu-id="8e4d1-126">Cada subred de la red virtual tiene una tabla de enrutamiento del sistema integrada.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-126">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="8e4d1-127">La tabla de enrutamiento del sistema tiene los siguientes tres grupos de rutas:</span><span class="sxs-lookup"><span data-stu-id="8e4d1-127">The system routing table has the following three groups of routes:</span></span>
  
  * <span data-ttu-id="8e4d1-128">**Rutas de redes virtuales locales:** directamente a las máquinas virtuales de destino en la misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-128">**Local VNet routes:** Directly to the destination VMs in the same virtual network.</span></span>
  * <span data-ttu-id="8e4d1-129">**Rutas locales:** a Azure VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-129">**On-premises routes:** To the Azure VPN gateway.</span></span>
  * <span data-ttu-id="8e4d1-130">**Ruta predeterminada** : directamente a Internet.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-130">**Default route:** Directly to the Internet.</span></span> <span data-ttu-id="8e4d1-131">Los paquetes destinados a las direcciones IP privadas que no están cubiertos por las dos rutas anteriores se anularán.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-131">Packets destined to the private IP addresses not covered by the previous two routes are dropped.</span></span>
* <span data-ttu-id="8e4d1-132">Este procedimiento usa las rutas definidas por el usuario para crear una tabla de enrutamiento para agregar una ruta predeterminada y, a continuación, asociar la tabla de enrutamiento a las subredes de la red virtual para habilitar la tunelización forzada en esas subredes.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-132">This procedure uses user-defined routes (UDR) to create a routing table to add a default route, and then associate the routing table to your VNet subnet(s) to enable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="8e4d1-133">La tunelización forzada debe asociarse a una red virtual que tenga una puerta de enlace de VPN basada en rutas.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-133">Forced tunneling must be associated with a VNet that has a route-based VPN gateway.</span></span> <span data-ttu-id="8e4d1-134">Deberá establecer un "sitio predeterminado" entre los sitios locales entre entornos conectados a la red virtual.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-134">You need to set a "default site" among the cross-premises local sites connected to the virtual network.</span></span> <span data-ttu-id="8e4d1-135">Además, el dispositivo VPN local debe configurarse con 0.0.0.0/0 como selectores de tráfico.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-135">Also, the on-premises VPN device must be configured using 0.0.0.0/0 as traffic selectors.</span></span> 
* <span data-ttu-id="8e4d1-136">La tunelización forzada ExpressRoute no se configura mediante este mecanismo, sino que se habilita mediante el anuncio de una ruta predeterminada a través de las sesiones de emparejamiento BGP de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-136">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via the ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="8e4d1-137">Para obtener más información, consulte la [documentación de ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).</span><span class="sxs-lookup"><span data-stu-id="8e4d1-137">For more information, see the [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/).</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="8e4d1-138">Información general sobre la configuración</span><span class="sxs-lookup"><span data-stu-id="8e4d1-138">Configuration overview</span></span>

<span data-ttu-id="8e4d1-139">El procedimiento siguiente lo ayudará a crear un grupo de recursos y una red virtual.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-139">The following procedure helps you create a resource group and a VNet.</span></span> <span data-ttu-id="8e4d1-140">Después, creará una puerta de enlace de VPN y configurará la tunelización forzada.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-140">You'll then create a VPN gateway and configure forced tunneling.</span></span> <span data-ttu-id="8e4d1-141">En el procedimiento, la red virtual 'MultiTier-VNet' tiene tres subredes: 'Frontend', 'Midtier' y 'Backend' con cuatro conexiones entre entornos: 'DefaultSiteHQ' y tres 'ramas'.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-141">In this procedure, the virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend', with four cross-premises connections: 'DefaultSiteHQ', and three Branches.</span></span>

<span data-ttu-id="8e4d1-142">Los pasos del procedimiento establecerán 'DefaultSiteHQ' como la conexión de sitio predeterminada para la tunelización forzada y configurarán las subredes 'Midtier' y 'Backend' para que usen dicha tunelización.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-142">The procedure steps set the 'DefaultSiteHQ' as the default site connection for forced tunneling, and configure the 'Midtier' and 'Backend' subnets to use forced tunneling.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8e4d1-143">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="8e4d1-143">Before you begin</span></span>

<span data-ttu-id="8e4d1-144">Instale la versión más reciente de los cmdlets de PowerShell de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-144">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="8e4d1-145">Consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) para más información sobre cómo instalar los cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-145">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span>

### <a name="to-log-in"></a><span data-ttu-id="8e4d1-146">Para iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="8e4d1-146">To log in</span></span>

[!INCLUDE [To log in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a><span data-ttu-id="8e4d1-147">Configuración de la tunelización forzada</span><span class="sxs-lookup"><span data-stu-id="8e4d1-147">Configure forced tunneling</span></span>

1. <span data-ttu-id="8e4d1-148">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-148">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. <span data-ttu-id="8e4d1-149">Cree una red virtual y especifique las subredes.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-149">Create a virtual network and specify subnets.</span></span>

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. <span data-ttu-id="8e4d1-150">Cree las puertas de enlace de red local.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-150">Create the local network gateways.</span></span>

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. <span data-ttu-id="8e4d1-151">Cree la tabla de enrutamiento y la regla de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-151">Create the route table and route rule.</span></span>

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. <span data-ttu-id="8e4d1-152">Asocie la tabla de enrutamiento creada anteriormente a las subredes Midtier y Back-end.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-152">Associate the route table to the Midtier and Backend subnets.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="8e4d1-153">Cree la puerta de enlace con un sitio predeterminado.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-153">Create the Gateway with a default site.</span></span> <span data-ttu-id="8e4d1-154">Este paso tarda algún tiempo en completarse, a veces 45 minutos o más, dado que va a crear y configurar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-154">This step takes some time to complete, sometimes 45 minutes or more, because you are creating and configuring the gateway.</span></span><br> <span data-ttu-id="8e4d1-155">**-GatewayDefaultSite** es el parámetro de cmdlet que permite que funcione la configuración de enrutamiento forzado, así que tenga cuidado al configurar este valor correctamente.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-155">The **-GatewayDefaultSite** is the cmdlet parameter that allows the forced routing configuration to work, so take care to configure this setting properly.</span></span> <span data-ttu-id="8e4d1-156">Este parámetro solo está disponible en PowerShell 1.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-156">This parameter is available in PowerShell 1.0 or later.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. <span data-ttu-id="8e4d1-157">Establezca las conexiones VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="8e4d1-157">Establish the Site-to-Site VPN connections.</span></span>

  ```powershell
  $gateway = Get-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling"
  $lng1 = Get-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" 
  $lng2 = Get-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" 
  $lng3 = Get-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" 
  $lng4 = Get-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" 
    
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng1 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng2 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng3 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection4" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng4 -ConnectionType IPsec -SharedKey "preSharedKey"
    
  Get-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling"
  ```