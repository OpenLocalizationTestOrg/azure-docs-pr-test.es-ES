---
title: "Configuración de la tunelización forzada para conexiones de sitio a sitio de Azure: modelo clásico | Microsoft Docs"
description: "Cómo tooredirect o 'force' todos los tooyour de espera de tráfico de vinculado a Internet en ubicación y local."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 35b3a9ea370f9f962572629a69cc9aed16a87837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a><span data-ttu-id="3d9fd-103">Configurar la tunelización forzada mediante modelo de implementación clásica de Hola</span><span class="sxs-lookup"><span data-stu-id="3d9fd-103">Configure forced tunneling using hello classic deployment model</span></span>

<span data-ttu-id="3d9fd-104">Forzada permite redirigir o "forzar" todos los vinculado a Internet tráfico tooyour back-ubicación de local a través de un túnel VPN de sitio a sitio para inspección y auditoría de túnel.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="3d9fd-105">Se trata de un requisito de seguridad crítico en la mayoría de las directivas de las empresas de TI.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="3d9fd-106">Sin la tunelización forzada, tráfico de Internet desde las máquinas virtuales en Azure atravesará siempre desde la infraestructura de red de Azure directamente out toohello Internet, sin Hola opción tooallow se tooinspect o auditoría tráfico Hola.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="3d9fd-107">Acceso de Internet no autorizado puede provocar potencialmente la divulgación de tooinformation u otros tipos de infracciones de seguridad.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-107">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="3d9fd-108">Este artículo le guiará a través de configuración forzada de túnel para redes virtuales creadas mediante el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-108">This article walks you through configuring forced tunneling for virtual networks created using hello classic deployment model.</span></span> <span data-ttu-id="3d9fd-109">La tunelización forzada puede configurarse mediante el uso de PowerShell, no a través del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-109">Forced tunneling can be configured by using PowerShell, not through hello portal.</span></span> <span data-ttu-id="3d9fd-110">Si desea tooconfigure tunelización para modelo de implementación del Administrador de recursos de hello forzada, seleccione artículo clásico de hello después de la lista desplegable:</span><span class="sxs-lookup"><span data-stu-id="3d9fd-110">If you want tooconfigure forced tunneling for hello Resource Manager deployment model, select classic article from hello following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3d9fd-111">PowerShell: clásico</span><span class="sxs-lookup"><span data-stu-id="3d9fd-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="3d9fd-112">PowerShell: administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="3d9fd-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a><span data-ttu-id="3d9fd-113">Requisitos y consideraciones</span><span class="sxs-lookup"><span data-stu-id="3d9fd-113">Requirements and considerations</span></span>
<span data-ttu-id="3d9fd-114">La tunelización forzada en Azure se configura a través de rutas definidas por el usuario (UDR) de redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-114">Forced tunneling in Azure is configured via virtual network user-defined routes (UDR).</span></span> <span data-ttu-id="3d9fd-115">Redirigir el tráfico tooan local de sitio se expresa como una puerta de enlace de VPN de Azure de toohello de ruta predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-115">Redirecting traffic tooan on-premises site is expressed as a Default Route toohello Azure VPN gateway.</span></span> <span data-ttu-id="3d9fd-116">Hello siguiente sección enumeran hello las limitaciones actuales de la tabla de enrutamiento de Hola y rutas para una red Virtual de Azure:</span><span class="sxs-lookup"><span data-stu-id="3d9fd-116">hello following section lists hello current limitation of hello routing table and routes for an Azure Virtual Network:</span></span>

* <span data-ttu-id="3d9fd-117">Cada subred de la red virtual tiene una tabla de enrutamiento del sistema integrada.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-117">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="3d9fd-118">tabla de enrutamiento de sistema de Hello tiene Hola los tres grupos de rutas siguientes:</span><span class="sxs-lookup"><span data-stu-id="3d9fd-118">hello system routing table has hello following three groups of routes:</span></span>

  * <span data-ttu-id="3d9fd-119">**Las rutas de red virtual locales:** directamente toohello máquinas virtuales de destino en hello misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-119">**Local VNet routes:** Directly toohello destination VMs in hello same virtual network.</span></span>
  * <span data-ttu-id="3d9fd-120">**Rutas locales:** toohello puerta de enlace de VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-120">**On-premises routes:** toohello Azure VPN gateway.</span></span>
  * <span data-ttu-id="3d9fd-121">**Ruta predeterminada:** toohello directamente Internet.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-121">**Default route:** Directly toohello Internet.</span></span> <span data-ttu-id="3d9fd-122">Los paquetes destinados toohello las direcciones IP privadas no cubiertas por las rutas de hello dos anteriores que se van a quitar.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-122">Packets destined toohello private IP addresses not covered by hello previous two routes will be dropped.</span></span>
* <span data-ttu-id="3d9fd-123">Con la versión de Hola de rutas definidas por el usuario, puede crear un tooadd de tabla de enrutamiento una ruta predeterminada y, a continuación, asociar Hola enrutamiento tabla tooyour red virtual subredes tooenable forzado túnel en esas subredes.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-123">With hello release of user-defined routes, you can create a routing table tooadd a default route, and then associate hello routing table tooyour VNet subnet(s) tooenable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="3d9fd-124">Deberá tooset un sitio denominado"predeterminado" entre la red virtual de hello entre entornos sitios locales toohello conectado.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-124">You need tooset a "default site" among hello cross-premises local sites connected toohello virtual network.</span></span>
* <span data-ttu-id="3d9fd-125">La tunelización forzada debe asociarse a una red virtual que tiene una puerta de enlace de VPN de enrutamiento dinámico (no una puerta de enlace estática).</span><span class="sxs-lookup"><span data-stu-id="3d9fd-125">Forced tunneling must be associated with a VNet that has a dynamic routing VPN gateway (not a static gateway).</span></span>
* <span data-ttu-id="3d9fd-126">La tunelización forzada de ExpressRoute no se configura mediante este mecanismo, pero en su lugar, se habilita de forma anunciando una ruta predeterminada a través de hello BGP de ExpressRoute sesiones de emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-126">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via hello ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="3d9fd-127">Vea hello [documentación de ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-127">Please see hello [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/) for more information.</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="3d9fd-128">Información general sobre la configuración</span><span class="sxs-lookup"><span data-stu-id="3d9fd-128">Configuration overview</span></span>
<span data-ttu-id="3d9fd-129">En el siguiente ejemplo de Hola Hola front-end no se fuerza la subred de túnel.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-129">In hello following example, hello Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="3d9fd-130">las cargas de trabajo de Hello en la subred de front-end de hello pueden continuar tooaccept y responder las solicitudes de toocustomer de hello Internet directamente.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-130">hello workloads in hello Frontend subnet can continue tooaccept and respond toocustomer requests from hello Internet directly.</span></span> <span data-ttu-id="3d9fd-131">Hello subredes de nivel intermedio y back-end se convierten obligatoriamente túnel.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-131">hello Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="3d9fd-132">Las conexiones de salida de estos toohello dos subredes Internet será tooan forzado o redirigida volver al sitio local a través de una de hello que túneles VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-132">Any outbound connections from these two subnets toohello Internet will be forced or redirected back tooan on-premises site via one of hello S2S VPN tunnels.</span></span>

<span data-ttu-id="3d9fd-133">Esto le permite toorestrict e inspeccionar el acceso a Internet desde las máquinas virtuales o servicios de nube de Azure, mientras continúa tooenable su arquitectura de servicio de varios niveles necesaria.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-133">This allows you toorestrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing tooenable your multi-tier service architecture required.</span></span> <span data-ttu-id="3d9fd-134">También puede aplicar forzada túnel toohello todo redes virtuales si no hay ningún cargas de trabajo orientado a Internet en las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-134">You also can apply forced tunneling toohello entire virtual networks if there are no Internet-facing workloads in your virtual networks.</span></span>

![Tunelización forzada](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a><span data-ttu-id="3d9fd-136">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="3d9fd-136">Before you begin</span></span>
<span data-ttu-id="3d9fd-137">Compruebe que dispone de hello siguientes elementos antes de empezar la configuración.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-137">Verify that you have hello following items before beginning configuration.</span></span>

* <span data-ttu-id="3d9fd-138">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-138">An Azure subscription.</span></span> <span data-ttu-id="3d9fd-139">Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3d9fd-139">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3d9fd-140">Una red virtual configurada.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-140">A configured virtual network.</span></span> 
* <span data-ttu-id="3d9fd-141">versión más reciente de Hola de hello cmdlets de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-141">hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="3d9fd-142">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener más información acerca de cómo instalar los cmdlets de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-142">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

## <a name="configure-forced-tunneling"></a><span data-ttu-id="3d9fd-143">Configuración de la tunelización forzada</span><span class="sxs-lookup"><span data-stu-id="3d9fd-143">Configure forced tunneling</span></span>
<span data-ttu-id="3d9fd-144">Hola procedimiento le ayudará a especificar la tunelización forzada de una red virtual.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-144">hello following procedure will help you specify forced tunneling for a virtual network.</span></span> <span data-ttu-id="3d9fd-145">pasos de configuración de Hello corresponden toohello archivo de configuración de red de red virtual.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-145">hello configuration steps correspond toohello VNet network configuration file.</span></span>

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

<span data-ttu-id="3d9fd-146">En este ejemplo, la red virtual de hello 'Red virtual de varios niveles' no tiene tres subredes: subredes 'Front-end', 'Nivel intermedio' y "Back-end", con las conexiones locales de entre cuatro: 'DefaultSiteHQ' y tres bifurcaciones.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-146">In this example, hello virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend' subnets, with four cross premises connections: 'DefaultSiteHQ', and three Branches.</span></span> 

<span data-ttu-id="3d9fd-147">pasos de Hello establecer hello 'DefaultSiteHQ' como conexión de sitio predeterminado de hello para el túnel forzado y configurar Hola nivel intermedio y back-end subredes toouse tunelización forzada.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-147">hello steps will set hello 'DefaultSiteHQ' as hello default site connection for forced tunneling, and configure hello Midtier and Backend subnets toouse forced tunneling.</span></span>

1. <span data-ttu-id="3d9fd-148">Cree una tabla de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-148">Create a routing table.</span></span> <span data-ttu-id="3d9fd-149">Usar hello siguiente cmdlet toocreate su tabla de rutas.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-149">Use hello following cmdlet toocreate your route table.</span></span>

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. <span data-ttu-id="3d9fd-150">Agregar una tabla de enrutamiento de toohello de ruta predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-150">Add a default route toohello routing table.</span></span> 

  <span data-ttu-id="3d9fd-151">Hello en el ejemplo siguiente se agrega una ruta toohello tabla de enrutamiento predeterminada creada en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-151">hello following example adds a default route toohello routing table created in Step 1.</span></span> <span data-ttu-id="3d9fd-152">Tenga en cuenta que solo se admite la ruta de Hola es el prefijo de destino de Hola de toohello "0.0.0.0/0" salto "VPNGateway".</span><span class="sxs-lookup"><span data-stu-id="3d9fd-152">Note that hello only route supported is hello destination prefix of "0.0.0.0/0" toohello "VPNGateway" NextHop.</span></span>

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. <span data-ttu-id="3d9fd-153">Asociar subredes de hello enrutamiento tabla toohello.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-153">Associate hello routing table toohello subnets.</span></span> 

  <span data-ttu-id="3d9fd-154">Después de una tabla de enrutamiento se crea y agrega una ruta, use después tooadd de ejemplo de Hola o asociar la subred de red virtual de hello ruta tabla tooa.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-154">After a routing table is created and a route added, use hello following example tooadd or associate hello route table tooa VNet subnet.</span></span> <span data-ttu-id="3d9fd-155">ejemplo de Hola agrega Hola ruta tabla "MyRouteTable" toohello nivel intermedio y back-end subredes de varios niveles de VNet a VNet.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-155">hello example adds hello route table "MyRouteTable" toohello Midtier and Backend subnets of VNet MultiTier-VNet.</span></span>

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. <span data-ttu-id="3d9fd-156">Asigne un sitio predeterminado para la tunelización forzada.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-156">Assign a default site for forced tunneling.</span></span> 

  <span data-ttu-id="3d9fd-157">Hola anterior paso, scripts de cmdlet de ejemplo de Hola crean la tabla de enrutamiento de Hola y asociadas hello tootwo de tabla de ruta de subredes de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-157">In hello preceding step, hello sample cmdlet scripts created hello routing table and associated hello route table tootwo of hello VNet subnets.</span></span> <span data-ttu-id="3d9fd-158">paso restante de Hello es tooselect un sitio local entre las conexiones de varios sitios de Hola de red virtual de hello como sitio predeterminado de Hola o de túnel.</span><span class="sxs-lookup"><span data-stu-id="3d9fd-158">hello remaining step is tooselect a local site among hello multi-site connections of hello virtual network as hello default site or tunnel.</span></span>

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a><span data-ttu-id="3d9fd-159">Cmdlets de PowerShell adicionales</span><span class="sxs-lookup"><span data-stu-id="3d9fd-159">Additional PowerShell cmdlets</span></span>
### <a name="toodelete-a-route-table"></a><span data-ttu-id="3d9fd-160">toodelete una tabla de rutas</span><span class="sxs-lookup"><span data-stu-id="3d9fd-160">toodelete a route table</span></span>

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a><span data-ttu-id="3d9fd-161">toolist una tabla de rutas</span><span class="sxs-lookup"><span data-stu-id="3d9fd-161">toolist a route table</span></span>

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a><span data-ttu-id="3d9fd-162">toodelete una ruta de una tabla de rutas</span><span class="sxs-lookup"><span data-stu-id="3d9fd-162">toodelete a route from a route table</span></span>

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a><span data-ttu-id="3d9fd-163">tooremove una ruta de subred</span><span class="sxs-lookup"><span data-stu-id="3d9fd-163">tooremove a route from a subnet</span></span>

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a><span data-ttu-id="3d9fd-164">tabla de rutas de hello toolist asociada a una subred</span><span class="sxs-lookup"><span data-stu-id="3d9fd-164">toolist hello route table associated with a subnet</span></span>

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a><span data-ttu-id="3d9fd-165">tooremove un sitio predeterminado de una puerta de enlace de VPN de VNet</span><span class="sxs-lookup"><span data-stu-id="3d9fd-165">tooremove a default site from a VNet VPN gateway</span></span>

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```