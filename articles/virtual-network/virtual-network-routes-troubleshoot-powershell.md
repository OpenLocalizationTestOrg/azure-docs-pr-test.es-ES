---
title: rutas de aaaTroubleshoot - PowerShell | Documentos de Microsoft
description: "Obtenga información acerca de cómo tootroubleshoot enruta en modelo de implementación de Azure Resource Manager Hola con Azure PowerShell."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bf7dc5e7-9399-460e-8e0d-8992dbed98a6
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 7a07806df5c1d0caee921187e6ad29f6755ab535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a><span data-ttu-id="7f011-103">Solución de problemas de rutas mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f011-103">Troubleshoot routes using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f011-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="7f011-104">Azure Portal</span></span>](virtual-network-routes-troubleshoot-portal.md)
> * [<span data-ttu-id="7f011-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f011-105">PowerShell</span></span>](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="7f011-106">Si se producen tooor de problemas de conectividad de red de la máquina Virtual (VM) de Azure, las rutas que pueden influir en los flujos de tráfico de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7f011-106">If you are experiencing network connectivity issues tooor from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span></span> <span data-ttu-id="7f011-107">Este artículo proporciona información general sobre las capacidades de diagnóstico para rutas toohelp seguir solucionando el problema.</span><span class="sxs-lookup"><span data-stu-id="7f011-107">This article provides an overview of diagnostics capabilities for routes toohelp troubleshoot further.</span></span>

<span data-ttu-id="7f011-108">Las tablas de rutas están asociadas con subredes y son eficaces en todas las interfaces de red (NIC) en cada subred específica.</span><span class="sxs-lookup"><span data-stu-id="7f011-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span></span> <span data-ttu-id="7f011-109">Hola siguientes tipos de rutas puede ser aplicados tooeach interfaz de red:</span><span class="sxs-lookup"><span data-stu-id="7f011-109">hello following types of routes can be applied tooeach network interface:</span></span>

* <span data-ttu-id="7f011-110">**Rutas del sistema:** de forma predeterminada, cada subred creada en Azure Virtual Network (VNet) tiene tablas de rutas del sistema que permiten el tráfico de red virtual local, el tráfico local a través de las puertas de enlace VPN y el tráfico de Internet.</span><span class="sxs-lookup"><span data-stu-id="7f011-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span></span> <span data-ttu-id="7f011-111">Las rutas del sistema existen también para las redes virtuales emparejadas.</span><span class="sxs-lookup"><span data-stu-id="7f011-111">System routes also exist for peered VNets.</span></span>
* <span data-ttu-id="7f011-112">**Las rutas BGP:** propaga toonetwork interfaces a través de ExpressRoute o las conexiones VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="7f011-112">**BGP routes:** Propagated toonetwork interfaces through ExpressRoute or site-to-site VPN connections.</span></span> <span data-ttu-id="7f011-113">Obtener más información sobre el enrutamiento de BGP leyendo hello [BGP con puertas de enlace VPN](../vpn-gateway/vpn-gateway-bgp-overview.md) y [ExpressRoute Introducción](../expressroute/expressroute-introduction.md) artículos.</span><span class="sxs-lookup"><span data-stu-id="7f011-113">Learn more about BGP routing by reading hello [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span></span>
* <span data-ttu-id="7f011-114">**Rutas definidas por el usuario (UDR):** si se utilizan los dispositivos de red virtual o se fuerza el túnel tráfico tooan de red local a través de una VPN de sitio a sitio, puede tener rutas definidas por el usuario (UDRs) asociadas a la tabla de rutas de subred.</span><span class="sxs-lookup"><span data-stu-id="7f011-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic tooan on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span></span> <span data-ttu-id="7f011-115">Si no está familiarizado con UDRs, leer hello [rutas definidas por el usuario](virtual-networks-udr-overview.md#user-defined-routes) artículo.</span><span class="sxs-lookup"><span data-stu-id="7f011-115">If you're not familiar with UDRs, read hello [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span></span>

<span data-ttu-id="7f011-116">Con hello varias rutas que pueden ser aplicados tooa interfaz de red, puede ser difícil toodetermine rutas que agregado entrarán en vigor.</span><span class="sxs-lookup"><span data-stu-id="7f011-116">With hello various routes that can be applied tooa network interface, it can be difficult toodetermine which aggregate routes are effective.</span></span> <span data-ttu-id="7f011-117">toohelp solucionar problemas de conectividad de red de máquina virtual, puede ver todas las rutas efectivas de Hola para una interfaz de red en el modelo de implementación de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7f011-117">toohelp troubleshoot VM network connectivity, you can view all hello effective routes for a network interface in hello Azure Resource Manager deployment model.</span></span>

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="7f011-118">Uso de flujo de tráfico VM de rutas efectivas tootroubleshoot</span><span class="sxs-lookup"><span data-stu-id="7f011-118">Using Effective Routes tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="7f011-119">Este artículo usa Hola siguiendo el escenario como un tooillustrate de ejemplo cómo enruta tootroubleshoot Hola efectivo para una interfaz de red:</span><span class="sxs-lookup"><span data-stu-id="7f011-119">This article uses hello following scenario as an example tooillustrate how tootroubleshoot hello effective routes for a network interface:</span></span>

<span data-ttu-id="7f011-120">Una máquina virtual (*VM1*) conectado toohello red virtual (*VNet1*, prefijo: 10.9.0.0/16) se produce un error tooconnect tooa VM(VM3) en una red virtual recién peered (*VNet3*, prefijo 10.10.0.0/16).</span><span class="sxs-lookup"><span data-stu-id="7f011-120">A VM (*VM1*) connected toohello VNet (*VNet1*, prefix: 10.9.0.0/16) fails tooconnect tooa VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span></span> <span data-ttu-id="7f011-121">No hay ningún UDRs o BGP enruta aplicada tooVM1-NIC1 red interfaz conectada toohello VM, se aplican sólo las rutas del sistema.</span><span class="sxs-lookup"><span data-stu-id="7f011-121">There are no UDRs or BGP routes applied tooVM1-NIC1 network interface connected toohello VM, only system routes are applied.</span></span>

<span data-ttu-id="7f011-122">Este artículo explica cómo toodetermine Hola causa de errores de conexión de hello, con capacidad de rutas efectivas en el modelo de implementación de administración de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="7f011-122">This article explains how toodetermine hello cause of hello connection failure, using effective routes capability in Azure Resource Management deployment model.</span></span>
<span data-ttu-id="7f011-123">Aunque ejemplo de Hola utiliza sólo las rutas del sistema, Hola mismos pasos puede ser usado toodetermine errores de conexión entrantes y salientes a través de cualquier tipo de ruta.</span><span class="sxs-lookup"><span data-stu-id="7f011-123">While hello example uses only system routes, hello same steps can be used toodetermine inbound and outbound connection failures over any route type.</span></span>

> [!NOTE]
> <span data-ttu-id="7f011-124">Si la máquina virtual tiene más de una NIC conectada, compruebe rutas efectivas para cada uno de hello tooand problemas conectividad de red de toodiagnose de NIC de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7f011-124">If your VM has more than one NIC attached, check effective routes for each of hello NICs toodiagnose network connectivity issues tooand from a VM.</span></span>
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a><span data-ttu-id="7f011-125">Visualización de las rutas eficaces para una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7f011-125">View effective routes for a virtual machine</span></span>
<span data-ttu-id="7f011-126">toosee Hola agregado rutas que se aplica tooa VM, Hola completa siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="7f011-126">toosee hello aggregate routes that are applied tooa VM, complete hello following steps:</span></span>

### <a name="view-effective-routes-for-a-network-interface"></a><span data-ttu-id="7f011-127">Visualización de las rutas eficaces para una interfaz de red</span><span class="sxs-lookup"><span data-stu-id="7f011-127">View effective routes for a network interface</span></span>
<span data-ttu-id="7f011-128">toosee Hola agregado rutas de interfaz de red tooa aplicado, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="7f011-128">toosee hello aggregate routes that are applied tooa network interface, complete hello following steps:</span></span>

1. <span data-ttu-id="7f011-129">Inicie un tooAzure de sesión y de inicio de sesión de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="7f011-129">Start an Azure PowerShell session and login tooAzure.</span></span> <span data-ttu-id="7f011-130">Si no está familiarizado con PowerShell de Azure, lea hello [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) artículo.</span><span class="sxs-lookup"><span data-stu-id="7f011-130">If you’re not familiar with Azure PowerShell, read hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="7f011-131">Hello siguiente comando devuelve toda la interfaz de red de tooa rutas aplicadas denominado *VM1 NIC1* en grupo de recursos de hello *RG1*.</span><span class="sxs-lookup"><span data-stu-id="7f011-131">hello following command returns all routes applied tooa network interface named *VM1-NIC1* in hello resource group *RG1*.</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="7f011-132">Si no conoce el nombre de Hola de una interfaz de red, escriba Hola siguiendo los nombres de comando tooretrieve Hola de todas las interfaces de red en un group.* de recursos</span><span class="sxs-lookup"><span data-stu-id="7f011-132">If you don’t know hello name of a network interface, type hello following command tooretrieve hello names of all network interfaces in a resource group.*</span></span>
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   <span data-ttu-id="7f011-133">Hello salida siguiente busca un resultado similar toohello cada Hola de subred de ruta aplicado toohello A que NIC está conectada:</span><span class="sxs-lookup"><span data-stu-id="7f011-133">hello following output looks similar toohello output for each route applied toohello subnet hello NIC is connected to:</span></span>
   
       Name :
       State : Active
       AddressPrefix : {10.9.0.0/16}
       NextHopType : VNetLocal
       NextHopIpAddress : {}
   
       Name :
       State : Active
       AddressPrefix : {0.0.0.0/16}
       NextHopType : Internet
       NextHopIpAddress : {}
   
   <span data-ttu-id="7f011-134">Tenga en cuenta siguiente de hello en la salida de hello:</span><span class="sxs-lookup"><span data-stu-id="7f011-134">Notice hello following in hello output:</span></span>
   
   * <span data-ttu-id="7f011-135">**Nombre**: nombre de ruta efectiva Hola puede estar vacío, a menos que especifique explícitamente para rutas definidas por el usuario.</span><span class="sxs-lookup"><span data-stu-id="7f011-135">**Name**: Name of hello effective route may be empty, unless explicitly specified, for user-defined routes.</span></span> 
   * <span data-ttu-id="7f011-136">**Estado**: indica el estado de ruta efectiva Hola.</span><span class="sxs-lookup"><span data-stu-id="7f011-136">**State**: Indicates state of hello effective route.</span></span> <span data-ttu-id="7f011-137">Los valores posibles son "Activo" o "No válido"</span><span class="sxs-lookup"><span data-stu-id="7f011-137">Possible values are "Active" or "Invalid"</span></span>
   * <span data-ttu-id="7f011-138">**AddressPrefixes**: especifica el prefijo de dirección de Hola de ruta efectiva de hello en la notación CIDR.</span><span class="sxs-lookup"><span data-stu-id="7f011-138">**AddressPrefixes**: Specifies hello address prefix of hello effective route in CIDR notation.</span></span> 
   * <span data-ttu-id="7f011-139">**nextHopType**: indica el próximo salto de Hola para hello dada la ruta.</span><span class="sxs-lookup"><span data-stu-id="7f011-139">**nextHopType**: Indicates hello next hop for hello given route.</span></span> <span data-ttu-id="7f011-140">Los valores posibles son *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering* o *Null*.</span><span class="sxs-lookup"><span data-stu-id="7f011-140">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span></span> <span data-ttu-id="7f011-141">Un valor de *Null* para **nextHopType** en un UDR puede indicar una ruta no válida.</span><span class="sxs-lookup"><span data-stu-id="7f011-141">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span></span> <span data-ttu-id="7f011-142">Por ejemplo, si **nextHopType** es *VirtualAppliance* y Hola network appliance virtual VM no está en un estado de aprovisionamiento/ejecución.</span><span class="sxs-lookup"><span data-stu-id="7f011-142">For example, if **nextHopType** is *VirtualAppliance* and hello network virtual appliance VM is not in a provisioned/running state.</span></span> <span data-ttu-id="7f011-143">Si **nextHopType** es *VPNGateway* y no hay ninguna puerta de enlace aprovisionado/ejecución Hola red virtual especificada, ruta de hello puede no ser válida.</span><span class="sxs-lookup"><span data-stu-id="7f011-143">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in hello given VNet, hello route may become invalid.</span></span>
   * <span data-ttu-id="7f011-144">**NextHopIpAddress**: especifica Hola dirección IP de próximo salto de Hola de ruta efectiva Hola.</span><span class="sxs-lookup"><span data-stu-id="7f011-144">**NextHopIpAddress**: Specifies hello IP address of hello next hop of hello effective route.</span></span>
   
   <span data-ttu-id="7f011-145">Hello siguiente comando devuelve las rutas de hello en una tabla tooview más fácil:</span><span class="sxs-lookup"><span data-stu-id="7f011-145">hello following command returns hello routes in an easier tooview table:</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   <span data-ttu-id="7f011-146">Hola salida siguiente es algunos de los resultados de hello recibidos de escenario de hello descrito anteriormente:</span><span class="sxs-lookup"><span data-stu-id="7f011-146">hello following output is some of hello output received for hello scenario described previously:</span></span>
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. <span data-ttu-id="7f011-147">No hay ninguna ruta aparece toohello *oesteee. UU.-VNet3* red virtual (prefijo 10.10.0.0/16)** de *VNet1 oesteee. UU.* (prefijo 10.9.0.0/16) en la salida de hello del paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f011-147">There is no route listed toohello *WestUS-VNet3* VNet (Prefix 10.10.0.0/16)** from *WestUS-VNet1* (Prefix 10.9.0.0/16) in hello output from hello previous step.</span></span> <span data-ttu-id="7f011-148">Como se muestra en hello después de la imagen, Hola vínculo de intercambio de tráfico de red virtual con hello *oesteee. UU.-VNet3* red virtual está en hello *Disconnected* estado.</span><span class="sxs-lookup"><span data-stu-id="7f011-148">As shown in hello following picture, hello VNet peering link with hello *WestUS-VNet3* VNet is in hello *Disconnected* state.</span></span>
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    <span data-ttu-id="7f011-149">vínculo de Hello bidireccional de emparejamiento de Hola se interrumpe, que explica por qué VM1 no se pudo conectar tooVM3 Hola *oesteee. UU.-VNet3* red virtual.</span><span class="sxs-lookup"><span data-stu-id="7f011-149">hello bi-directional link for hello peering is broken, which explains why VM1 could not connect tooVM3 in hello *WestUS-VNet3* VNet.</span></span> <span data-ttu-id="7f011-150">Configure un vínculo de emparejamiento de red virtual bidireccional para las redes virtuales *WestUS-VNet1* y *WestUS-VNet3*.</span><span class="sxs-lookup"><span data-stu-id="7f011-150">Setup a bi-directional VNet peering link again for *WestUS-VNet1* and *WestUS-VNet3* VNets.</span></span> <span data-ttu-id="7f011-151">salida de Hello devuelto después de vínculo de intercambio de tráfico de red virtual de Hola se establece correctamente la siguiente:</span><span class="sxs-lookup"><span data-stu-id="7f011-151">hello output returned after hello VNet peering link is correctly established follows:</span></span>
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    <span data-ttu-id="7f011-152">Una vez que determine el problema de hello, puede agregar, quitar, o cambiar las rutas y tablas de rutas.</span><span class="sxs-lookup"><span data-stu-id="7f011-152">Once you determine hello issue, you can add, remove, or change routes and route tables.</span></span> <span data-ttu-id="7f011-153">Hola de tipo siguientes comando toosee una lista de comandos de hello usa toodo así:</span><span class="sxs-lookup"><span data-stu-id="7f011-153">Type hello following command toosee a list of hello commands used toodo so:</span></span>
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a><span data-ttu-id="7f011-154">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="7f011-154">Considerations</span></span>
<span data-ttu-id="7f011-155">Unos tookeep cosas en cuenta al revisar la lista de Hola de rutas devuelve:</span><span class="sxs-lookup"><span data-stu-id="7f011-155">A few things tookeep in mind when reviewing hello list of routes returned:</span></span>

* <span data-ttu-id="7f011-156">El enrutamiento se basa en coincidencia de prefijo más larga (LPM) entre las rutas UDR, BGP y del sistema.</span><span class="sxs-lookup"><span data-stu-id="7f011-156">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span></span> <span data-ttu-id="7f011-157">Si hay más de una ruta con hello mismo LPM coinciden, entonces se seleccionará una ruta en función de su origen en hello siguiendo el orden:</span><span class="sxs-lookup"><span data-stu-id="7f011-157">If there is more than one route with hello same LPM match, then a route is selected based on its origin in hello following order:</span></span>
  
  * <span data-ttu-id="7f011-158">Ruta definida por el usuario</span><span class="sxs-lookup"><span data-stu-id="7f011-158">User-defined route</span></span>
  * <span data-ttu-id="7f011-159">Ruta BGP</span><span class="sxs-lookup"><span data-stu-id="7f011-159">BGP route</span></span>
  * <span data-ttu-id="7f011-160">Ruta del sistema (predeterminado)</span><span class="sxs-lookup"><span data-stu-id="7f011-160">System (Default) route</span></span>
    
    <span data-ttu-id="7f011-161">Con rutas efectivas, sólo puede ver las rutas efectivas que sean iguales LPM basado en todas las rutas de hello disponible.</span><span class="sxs-lookup"><span data-stu-id="7f011-161">With effective routes, you can only see effective routes that are LPM match based on all hello availble routes.</span></span> <span data-ttu-id="7f011-162">Mostrando cómo rutas Hola se evalúan realmente de una NIC determinada, resulta mucho más fácil tootroubleshoot específico las rutas que pueden afectar a la conectividad de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7f011-162">By showing how hello routes are actually evaluated for a given NIC, this makes it a lot easier tootroubleshoot specific routes that may be impacting connectivity to/from your VM.</span></span>
* <span data-ttu-id="7f011-163">Si tiene UDRs y envían tráfico tooa virtual otros dispositivos de red (NVA), con *VirtualAppliance* como **nextHopType**, compruebe que el reenvío IP está habilitado en el tráfico de hello NVA receptora Hola o se quitan los paquetes.</span><span class="sxs-lookup"><span data-stu-id="7f011-163">If you have UDRs and are sending traffic tooa network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on hello NVA receiving hello traffic or packets are dropped.</span></span> 
* <span data-ttu-id="7f011-164">Si está habilitado el protocolo de túnel forzado, todo el tráfico saliente de Internet será local tooon enrutado.</span><span class="sxs-lookup"><span data-stu-id="7f011-164">If Forced tunneling is enabled, all outbound Internet traffic will be routed tooon-premises.</span></span> <span data-ttu-id="7f011-165">RDP/SSH de tooyour Internet que VM no funcionen con esta configuración, dependiendo de cómo Hola local controla este tráfico.</span><span class="sxs-lookup"><span data-stu-id="7f011-165">RDP/SSH from Internet tooyour VM may not work with this setting, depending on how hello on-premises handles this traffic.</span></span> 
  <span data-ttu-id="7f011-166">Puede habilitar la tunelización forzada:</span><span class="sxs-lookup"><span data-stu-id="7f011-166">Forced-tunneling can be enabled:</span></span>
  * <span data-ttu-id="7f011-167">Si utiliza VPN de sitio a sitio, estableciendo una ruta definida por el usuario (UDR) con nextHopType como VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="7f011-167">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span></span>
  * <span data-ttu-id="7f011-168">Si se anuncia una ruta predeterminada a través de BGP</span><span class="sxs-lookup"><span data-stu-id="7f011-168">If a default route is advertised over BGP</span></span>
* <span data-ttu-id="7f011-169">Para la red virtual emparejamiento tráfico toowork correctamente, una ruta de sistema con **nextHopType** *VNetPeering* debe existir para hello emparejar el intervalo de prefijo de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="7f011-169">For VNet peering traffic toowork correctly, a system route with **nextHopType** *VNetPeering* must exist for hello peered VNet’s prefix range.</span></span> <span data-ttu-id="7f011-170">Si una ruta de este tipo no existe y Hola de intercambio de tráfico de red virtual vínculo parece correcta:</span><span class="sxs-lookup"><span data-stu-id="7f011-170">If such a route doesn’t exist and hello VNet peering link looks OK:</span></span>
  * <span data-ttu-id="7f011-171">Espere unos segundos y vuelva a intentar si es un vínculo de emparejamiento recién establecido.</span><span class="sxs-lookup"><span data-stu-id="7f011-171">Wait a few seconds and retry if it's a newly established peering link.</span></span> <span data-ttu-id="7f011-172">En ocasiones, toma más rutas toopropagate tooall interfaces de red de hello en una subred.</span><span class="sxs-lookup"><span data-stu-id="7f011-172">It occasionally takes longer toopropagate routes tooall hello network interfaces in a subnet.</span></span>
  * <span data-ttu-id="7f011-173">Las reglas del grupo de seguridad de red (NSG) que pueden influir en los flujos de tráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f011-173">Network Security Group (NSG) rules may be impacting hello traffic flows.</span></span> <span data-ttu-id="7f011-174">Para obtener más información, vea hello [solucionar problemas de grupos de seguridad de red](virtual-network-nsg-troubleshoot-powershell.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="7f011-174">For more information, see hello [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-powershell.md) article.</span></span>

