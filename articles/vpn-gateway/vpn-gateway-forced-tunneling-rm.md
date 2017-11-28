---
title: "Configuración de la tunelización forzada para conexiones de sitio a sitio de Azure: Resource Manager | Microsoft Docs"
description: "Cómo tooredirect o 'force' todos los tooyour de espera de tráfico de vinculado a Internet en ubicación y local."
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
ms.openlocfilehash: 6bc52c04ab0749a674c9863be5e4f9a9f7c98df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-azure-resource-manager-deployment-model"></a><span data-ttu-id="d8765-103">Configurar la tunelización forzada mediante el modelo de implementación de hello Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d8765-103">Configure forced tunneling using hello Azure Resource Manager deployment model</span></span>

<span data-ttu-id="d8765-104">Forzada permite redirigir o "forzar" todos los vinculado a Internet tráfico tooyour back-ubicación de local a través de un túnel VPN de sitio a sitio para inspección y auditoría de túnel.</span><span class="sxs-lookup"><span data-stu-id="d8765-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="d8765-105">Se trata de un requisito de seguridad crítico en la mayoría de las directivas de las empresas de TI.</span><span class="sxs-lookup"><span data-stu-id="d8765-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="d8765-106">Sin la tunelización forzada, tráfico de Internet desde las máquinas virtuales en Azure siempre atraviesa de infraestructura de red de Azure directamente out toohello Internet, sin Hola opción tooallow se tooinspect o auditoría tráfico Hola.</span><span class="sxs-lookup"><span data-stu-id="d8765-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure always traverses from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="d8765-107">Acceso de Internet no autorizado puede provocar potencialmente la divulgación de tooinformation u otros tipos de infracciones de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d8765-107">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

<span data-ttu-id="d8765-108">Este artículo le guiará a través de configuración forzada de túnel para redes virtuales creadas mediante el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8765-108">This article walks you through configuring forced tunneling for virtual networks created using hello Resource Manager deployment model.</span></span> <span data-ttu-id="d8765-109">La tunelización forzada puede configurarse mediante el uso de PowerShell, no a través del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8765-109">Forced tunneling can be configured by using PowerShell, not through hello portal.</span></span> <span data-ttu-id="d8765-110">Si desea tooconfigure tunelización para el modelo de implementación clásica de hello forzada, seleccione artículo clásico de hello después de la lista desplegable:</span><span class="sxs-lookup"><span data-stu-id="d8765-110">If you want tooconfigure forced tunneling for hello classic deployment model, select classic article from hello following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8765-111">PowerShell: clásico</span><span class="sxs-lookup"><span data-stu-id="d8765-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="d8765-112">PowerShell: administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="d8765-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a><span data-ttu-id="d8765-113">Información acerca de la tunelización forzada</span><span class="sxs-lookup"><span data-stu-id="d8765-113">About forced tunneling</span></span>

<span data-ttu-id="d8765-114">Hola siguiente diagrama ilustra forzada cómo funciona la tunelización.</span><span class="sxs-lookup"><span data-stu-id="d8765-114">hello following diagram illustrates how forced tunneling works.</span></span> 

![Tunelización forzada](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

<span data-ttu-id="d8765-116">En el ejemplo de Hola anterior, Hola front-end no se fuerza la subred de túnel.</span><span class="sxs-lookup"><span data-stu-id="d8765-116">In hello example above, hello Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="d8765-117">las cargas de trabajo de Hello en la subred de front-end de hello pueden continuar tooaccept y responder las solicitudes de toocustomer de hello Internet directamente.</span><span class="sxs-lookup"><span data-stu-id="d8765-117">hello workloads in hello Frontend subnet can continue tooaccept and respond toocustomer requests from hello Internet directly.</span></span> <span data-ttu-id="d8765-118">Hello subredes de nivel intermedio y back-end se convierten obligatoriamente túnel.</span><span class="sxs-lookup"><span data-stu-id="d8765-118">hello Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="d8765-119">Las conexiones de salida de estos toohello dos subredes Internet será tooan forzado o redirigida volver al sitio local a través de una de hello que túneles VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="d8765-119">Any outbound connections from these two subnets toohello Internet will be forced or redirected back tooan on-premises site via one of hello S2S VPN tunnels.</span></span>

<span data-ttu-id="d8765-120">Esto le permite toorestrict e inspeccionar el acceso a Internet desde las máquinas virtuales o servicios de nube de Azure, mientras continúa tooenable su arquitectura de servicio de varios niveles necesaria.</span><span class="sxs-lookup"><span data-stu-id="d8765-120">This allows you toorestrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing tooenable your multi-tier service architecture required.</span></span> <span data-ttu-id="d8765-121">Si no hay ningún cargas de trabajo orientado a Internet en las redes virtuales, también se pueden aplicar forzada túnel toohello todo redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="d8765-121">If there are no Internet-facing workloads in your virtual networks, you also can apply forced tunneling toohello entire virtual networks.</span></span>

## <a name="requirements-and-considerations"></a><span data-ttu-id="d8765-122">Requisitos y consideraciones</span><span class="sxs-lookup"><span data-stu-id="d8765-122">Requirements and considerations</span></span>

<span data-ttu-id="d8765-123">La tunelización forzada en Azure se configura a través de rutas definidas por el usuario de redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="d8765-123">Forced tunneling in Azure is configured via virtual network user-defined routes.</span></span> <span data-ttu-id="d8765-124">Redirigir el tráfico tooan local de sitio se expresa como una puerta de enlace de VPN de Azure de toohello de ruta predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d8765-124">Redirecting traffic tooan on-premises site is expressed as a Default Route toohello Azure VPN gateway.</span></span> <span data-ttu-id="d8765-125">Para obtener más información sobre las redes virtuales y las rutas definidas por el usuario, consulte [Rutas definidas por el usuario y reenvío IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8765-125">For more information about user-defined routing and virtual networks, see [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>

* <span data-ttu-id="d8765-126">Cada subred de la red virtual tiene una tabla de enrutamiento del sistema integrada.</span><span class="sxs-lookup"><span data-stu-id="d8765-126">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="d8765-127">tabla de enrutamiento de sistema de Hello tiene Hola los tres grupos de rutas siguientes:</span><span class="sxs-lookup"><span data-stu-id="d8765-127">hello system routing table has hello following three groups of routes:</span></span>
  
  * <span data-ttu-id="d8765-128">**Las rutas de red virtual locales:** directamente toohello máquinas virtuales de destino en hello misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="d8765-128">**Local VNet routes:** Directly toohello destination VMs in hello same virtual network.</span></span>
  * <span data-ttu-id="d8765-129">**Rutas locales:** toohello puerta de enlace de VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="d8765-129">**On-premises routes:** toohello Azure VPN gateway.</span></span>
  * <span data-ttu-id="d8765-130">**Ruta predeterminada:** toohello directamente Internet.</span><span class="sxs-lookup"><span data-stu-id="d8765-130">**Default route:** Directly toohello Internet.</span></span> <span data-ttu-id="d8765-131">Se quitan los paquetes destinados toohello las direcciones IP privadas no cubiertas por las rutas de hello dos anteriores.</span><span class="sxs-lookup"><span data-stu-id="d8765-131">Packets destined toohello private IP addresses not covered by hello previous two routes are dropped.</span></span>
* <span data-ttu-id="d8765-132">Este procedimiento utiliza rutas definidas por el usuario (UDR) toocreate una tooadd de tabla de enrutamiento una ruta predeterminada y, a continuación, asociar Hola enrutamiento tabla tooyour red virtual subredes tooenable forzado túnel en esas subredes.</span><span class="sxs-lookup"><span data-stu-id="d8765-132">This procedure uses user-defined routes (UDR) toocreate a routing table tooadd a default route, and then associate hello routing table tooyour VNet subnet(s) tooenable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="d8765-133">La tunelización forzada debe asociarse a una red virtual que tenga una puerta de enlace de VPN basada en rutas.</span><span class="sxs-lookup"><span data-stu-id="d8765-133">Forced tunneling must be associated with a VNet that has a route-based VPN gateway.</span></span> <span data-ttu-id="d8765-134">Deberá tooset un sitio denominado"predeterminado" entre la red virtual de hello entre entornos sitios locales toohello conectado.</span><span class="sxs-lookup"><span data-stu-id="d8765-134">You need tooset a "default site" among hello cross-premises local sites connected toohello virtual network.</span></span> <span data-ttu-id="d8765-135">Además, Hola local dispositivo VPN debe configurarse mediante 0.0.0.0/0 como selectores de tráfico.</span><span class="sxs-lookup"><span data-stu-id="d8765-135">Also, hello on-premises VPN device must be configured using 0.0.0.0/0 as traffic selectors.</span></span> 
* <span data-ttu-id="d8765-136">La tunelización forzada de ExpressRoute no se configura mediante este mecanismo, pero en su lugar, se habilita de forma anunciando una ruta predeterminada a través de hello BGP de ExpressRoute sesiones de emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="d8765-136">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via hello ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="d8765-137">Para obtener más información, vea hello [documentación de ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).</span><span class="sxs-lookup"><span data-stu-id="d8765-137">For more information, see hello [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/).</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="d8765-138">Información general sobre la configuración</span><span class="sxs-lookup"><span data-stu-id="d8765-138">Configuration overview</span></span>

<span data-ttu-id="d8765-139">Hola procedimiento le ayuda a crear un grupo de recursos y una red virtual.</span><span class="sxs-lookup"><span data-stu-id="d8765-139">hello following procedure helps you create a resource group and a VNet.</span></span> <span data-ttu-id="d8765-140">Después, creará una puerta de enlace de VPN y configurará la tunelización forzada.</span><span class="sxs-lookup"><span data-stu-id="d8765-140">You'll then create a VPN gateway and configure forced tunneling.</span></span> <span data-ttu-id="d8765-141">En este procedimiento, la red virtual de hello 'Red virtual de varios niveles' no tiene tres subredes: 'Front-end', 'Nivel intermedio' y 'Back-end', con cuatro entre entornos conexiones: 'DefaultSiteHQ' y tres bifurcaciones.</span><span class="sxs-lookup"><span data-stu-id="d8765-141">In this procedure, hello virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend', with four cross-premises connections: 'DefaultSiteHQ', and three Branches.</span></span>

<span data-ttu-id="d8765-142">pasos del procedimiento Hola establecer hello 'DefaultSiteHQ' como conexión de sitio predeterminado de hello tunelización forzada y configurar hello 'Nivel intermedio' y 'Back-end' subredes toouse tunelización forzada.</span><span class="sxs-lookup"><span data-stu-id="d8765-142">hello procedure steps set hello 'DefaultSiteHQ' as hello default site connection for forced tunneling, and configure hello 'Midtier' and 'Backend' subnets toouse forced tunneling.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d8765-143">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="d8765-143">Before you begin</span></span>

<span data-ttu-id="d8765-144">Instalar versión más reciente de Hola de hello cmdlets de PowerShell del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d8765-144">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="d8765-145">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener más información acerca de cómo instalar los cmdlets de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8765-145">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <a name="toolog-in"></a><span data-ttu-id="d8765-146">toolog en</span><span class="sxs-lookup"><span data-stu-id="d8765-146">toolog in</span></span>

[!INCLUDE [toolog in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a><span data-ttu-id="d8765-147">Configuración de la tunelización forzada</span><span class="sxs-lookup"><span data-stu-id="d8765-147">Configure forced tunneling</span></span>

1. <span data-ttu-id="d8765-148">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d8765-148">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. <span data-ttu-id="d8765-149">Cree una red virtual y especifique las subredes.</span><span class="sxs-lookup"><span data-stu-id="d8765-149">Create a virtual network and specify subnets.</span></span>

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. <span data-ttu-id="d8765-150">Crear Hola puertas de enlace de red local.</span><span class="sxs-lookup"><span data-stu-id="d8765-150">Create hello local network gateways.</span></span>

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. <span data-ttu-id="d8765-151">Crear regla de ruta y la tabla de ruta de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8765-151">Create hello route table and route rule.</span></span>

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. <span data-ttu-id="d8765-152">Asociar Hola ruta tabla toohello nivel intermedio y las subredes de back-end.</span><span class="sxs-lookup"><span data-stu-id="d8765-152">Associate hello route table toohello Midtier and Backend subnets.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="d8765-153">Crear Hola puerta de enlace con un sitio predeterminado.</span><span class="sxs-lookup"><span data-stu-id="d8765-153">Create hello Gateway with a default site.</span></span> <span data-ttu-id="d8765-154">Este paso toma algunas toocomplete de tiempo, en ocasiones 45 minutos o más, porque para crear y configurar la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8765-154">This step takes some time toocomplete, sometimes 45 minutes or more, because you are creating and configuring hello gateway.</span></span><br> <span data-ttu-id="d8765-155">Hola **- GatewayDefaultSite** es Hola parámetro del cmdlet que permite Hola forzada toowork de configuración de enrutamiento, eche un vistazo tooconfigure cuidado esta opción correctamente.</span><span class="sxs-lookup"><span data-stu-id="d8765-155">hello **-GatewayDefaultSite** is hello cmdlet parameter that allows hello forced routing configuration toowork, so take care tooconfigure this setting properly.</span></span> <span data-ttu-id="d8765-156">Este parámetro solo está disponible en PowerShell 1.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="d8765-156">This parameter is available in PowerShell 1.0 or later.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. <span data-ttu-id="d8765-157">Establecer las conexiones VPN de sitio a sitio Hola.</span><span class="sxs-lookup"><span data-stu-id="d8765-157">Establish hello Site-to-Site VPN connections.</span></span>

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