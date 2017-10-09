---
title: 'Conectar su tooan de red local red virtual de Azure: VPN de sitio a sitio: Portal | Documentos de Microsoft'
description: "Una conexión de IPsec desde el entorno local de red tooan red virtual de Azure a través de toocreate de pasos Hola Internet pública. Estos pasos le ayudarán a crear una conexión de puerta de enlace VPN de sitio a sitio entre entornos mediante el portal de Hola."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a><span data-ttu-id="cadb7-104">Crear una conexión de sitio a sitio en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cadb7-104">Create a Site-to-Site connection in hello Azure portal</span></span>

<span data-ttu-id="cadb7-105">Este artículo muestra cómo toouse Hola toocreate portal Azure una conexión de puerta de enlace VPN de sitio a sitio desde su toohello de red local red virtual.</span><span class="sxs-lookup"><span data-stu-id="cadb7-105">This article shows you how toouse hello Azure portal toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="cadb7-106">pasos de Hello en este artículo aplican toohello modelo de implementación de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="cadb7-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="cadb7-107">También puede crear esta configuración con una herramienta de implementación diferentes o un modelo de implementación seleccionando una opción diferente de hello lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="cadb7-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cadb7-108">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cadb7-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="cadb7-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cadb7-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="cadb7-110">CLI</span><span class="sxs-lookup"><span data-stu-id="cadb7-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="cadb7-111">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="cadb7-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

<span data-ttu-id="cadb7-112">Una conexión de puerta de enlace VPN de sitio a sitio es tooconnect utilizado en sus instalaciones de red tooan red virtual de Azure a través de un túnel VPN de IPsec/IKE (IKEv1 o IKEv2).</span><span class="sxs-lookup"><span data-stu-id="cadb7-112">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="cadb7-113">Este tipo de conexión requiere una VPN dispositivo situado en local que tiene un tooit de dirección asignada de IP pública con orientación externa.</span><span class="sxs-lookup"><span data-stu-id="cadb7-113">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="cadb7-114">Para más información acerca de las puertas de enlace VPN, consulte [Acerca de VPN Gateway](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="cadb7-114">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Diagrama de la conexión entre locales de VPN Gateway de sitio a sitio](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a><span data-ttu-id="cadb7-116">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="cadb7-116">Before you begin</span></span>

<span data-ttu-id="cadb7-117">Compruebe que se ha cumplido hello siguiendo criterios antes de comenzar la configuración:</span><span class="sxs-lookup"><span data-stu-id="cadb7-117">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="cadb7-118">Asegúrese de que tiene un dispositivo VPN compatible y alguna persona tooconfigure capaz de él.</span><span class="sxs-lookup"><span data-stu-id="cadb7-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="cadb7-119">Para más información acerca de los dispositivos VPN compatibles y su configuración, consulte [Acerca de los dispositivos VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="cadb7-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="cadb7-120">Compruebe que tiene una dirección IPv4 pública externa para el dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="cadb7-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="cadb7-121">Esta dirección IP no puede estar detrás de un NAT.</span><span class="sxs-lookup"><span data-stu-id="cadb7-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="cadb7-122">Si no está familiarizado con intervalos de direcciones IP de hello ubicados en configuración de red local, deberá toocoordinate con alguien que pueda proporcionarle estos detalles para usted.</span><span class="sxs-lookup"><span data-stu-id="cadb7-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="cadb7-123">Al crear esta configuración, debe especificar prefijos para intervalo de direcciones IP con hello que Azure enrutará la ubicación de tooyour local.</span><span class="sxs-lookup"><span data-stu-id="cadb7-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="cadb7-124">Ninguna de las subredes de saludo de la red local puede enumerar sobre el regazo con subredes de red virtual de Hola que desee tooconnect a.</span><span class="sxs-lookup"><span data-stu-id="cadb7-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span> 

### <span data-ttu-id="cadb7-125"><a name="values"></a>Valores del ejemplo</span><span class="sxs-lookup"><span data-stu-id="cadb7-125"><a name="values"></a>Example values</span></span>

<span data-ttu-id="cadb7-126">ejemplos de Hello en este artículo utiliza Hola después de valores.</span><span class="sxs-lookup"><span data-stu-id="cadb7-126">hello examples in this article use hello following values.</span></span> <span data-ttu-id="cadb7-127">Puede usar estos toocreate valores un entorno de prueba, o consulte toothem toobetter comprender los ejemplos de hello en este artículo.</span><span class="sxs-lookup"><span data-stu-id="cadb7-127">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

* <span data-ttu-id="cadb7-128">**Nombre de red virtual:** TestVNet1</span><span class="sxs-lookup"><span data-stu-id="cadb7-128">**VNet Name:** TestVNet1</span></span>
* <span data-ttu-id="cadb7-129">**Espacio de direcciones:**</span><span class="sxs-lookup"><span data-stu-id="cadb7-129">**Address Space:**</span></span> 
  * <span data-ttu-id="cadb7-130">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="cadb7-130">10.11.0.0/16</span></span>
  * <span data-ttu-id="cadb7-131">10.12.0.0/16 (opcional para este ejercicio)</span><span class="sxs-lookup"><span data-stu-id="cadb7-131">10.12.0.0/16 (optional for this exercise)</span></span>
* <span data-ttu-id="cadb7-132">**Subredes:**</span><span class="sxs-lookup"><span data-stu-id="cadb7-132">**Subnets:**</span></span>
  * <span data-ttu-id="cadb7-133">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="cadb7-133">FrontEnd: 10.11.0.0/24</span></span>
  * <span data-ttu-id="cadb7-134">BackEnd: 10.12.0.0/24 (opcional para este ejercicio)</span><span class="sxs-lookup"><span data-stu-id="cadb7-134">BackEnd: 10.12.0.0/24 (optional for this exercise)</span></span>
* <span data-ttu-id="cadb7-135">**GatewaySubnet:** 10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="cadb7-135">**GatewaySubnet:** 10.11.255.0/27</span></span>
* <span data-ttu-id="cadb7-136">**Grupo de recursos:** TestRG1</span><span class="sxs-lookup"><span data-stu-id="cadb7-136">**Resource Group:** TestRG1</span></span>
* <span data-ttu-id="cadb7-137">**Ubicación:** este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="cadb7-137">**Location:** East US</span></span>
* <span data-ttu-id="cadb7-138">**Servidor DNS:** opcional.</span><span class="sxs-lookup"><span data-stu-id="cadb7-138">**DNS Server:** Optional.</span></span> <span data-ttu-id="cadb7-139">dirección IP de saludo del servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="cadb7-139">hello IP address of your DNS server.</span></span>
* <span data-ttu-id="cadb7-140">**Nombre de la puerta de enlace de red virtual:** VNet1GW</span><span class="sxs-lookup"><span data-stu-id="cadb7-140">**Virtual Network Gateway Name:** VNet1GW</span></span>
* <span data-ttu-id="cadb7-141">**Dirección IP pública:** VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="cadb7-141">**Public IP:** VNet1GWIP</span></span>
* <span data-ttu-id="cadb7-142">**Tipo de VPN:** basada en rutas</span><span class="sxs-lookup"><span data-stu-id="cadb7-142">**VPN Type:** Route-based</span></span>
* <span data-ttu-id="cadb7-143">**Tipo de conexión:** de sitio a sitio (IPsec)</span><span class="sxs-lookup"><span data-stu-id="cadb7-143">**Connection Type:** Site-to-site (IPsec)</span></span>
* <span data-ttu-id="cadb7-144">**Tipo de puerta de enlace:** VPN</span><span class="sxs-lookup"><span data-stu-id="cadb7-144">**Gateway Type:** VPN</span></span>
* <span data-ttu-id="cadb7-145">**Nombre de la puerta de enlace de red local:** Site2</span><span class="sxs-lookup"><span data-stu-id="cadb7-145">**Local Network Gateway Name:** Site2</span></span>
* <span data-ttu-id="cadb7-146">**Nombre de conexión:** VNet1toSite2</span><span class="sxs-lookup"><span data-stu-id="cadb7-146">**Connection Name:** VNet1toSite2</span></span>

## <span data-ttu-id="cadb7-147"><a name="CreatVNet"></a>1. Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="cadb7-147"><a name="CreatVNet"></a>1. Create a virtual network</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="cadb7-148"><a name="dns"></a>2. Especificación de un servidor DNS</span><span class="sxs-lookup"><span data-stu-id="cadb7-148"><a name="dns"></a>2. Specify a DNS server</span></span>

<span data-ttu-id="cadb7-149">DNS no es necesario toocreate un sitio a sitio conexión.</span><span class="sxs-lookup"><span data-stu-id="cadb7-149">DNS is not required toocreate a Site-to-Site connection.</span></span> <span data-ttu-id="cadb7-150">Sin embargo, si desea toohave la resolución de nombres para los recursos de red virtual tooyour implementada, debe especificar un servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="cadb7-150">However, if you want toohave name resolution for resources that are deployed tooyour virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="cadb7-151">Esta opción permite especificar el servidor DNS de Hola que quiere toouse de resolución de nombres para esta red virtual.</span><span class="sxs-lookup"><span data-stu-id="cadb7-151">This setting lets you specify hello DNS server that you want toouse for name resolution for this virtual network.</span></span> <span data-ttu-id="cadb7-152">No crea un servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="cadb7-152">It does not create a DNS server.</span></span> <span data-ttu-id="cadb7-153">Para más información acerca de la resolución de nombres, consulte [Resolución de nombres para las máquinas virtuales e instancias de rol](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="cadb7-153">For more information about name resolution, see [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="cadb7-154"><a name="gatewaysubnet"></a>3. Crear una subred de puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="cadb7-154"><a name="gatewaysubnet"></a>3. Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="cadb7-155"><a name="VNetGateway"></a>4. Crear puerta de enlace VPN de Hola</span><span class="sxs-lookup"><span data-stu-id="cadb7-155"><a name="VNetGateway"></a>4. Create hello VPN gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <span data-ttu-id="cadb7-156"><a name="LocalNetworkGateway"></a>5. Crear puerta de enlace de red local de Hola</span><span class="sxs-lookup"><span data-stu-id="cadb7-156"><a name="LocalNetworkGateway"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="cadb7-157">puerta de enlace de red local de Hello suele hacer referencia a ubicación de tooyour local.</span><span class="sxs-lookup"><span data-stu-id="cadb7-157">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="cadb7-158">Se asigne un nombre mediante el cual Azure puede consulte tooit y luego especifique la dirección IP de Hola a sitio Hola de hello local VPN dispositivo toowhich creará una conexión.</span><span class="sxs-lookup"><span data-stu-id="cadb7-158">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="cadb7-159">También especificar prefijos de direcciones IP de Hola que se enrutará a través del dispositivo VPN de toohello de puerta de enlace VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="cadb7-159">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="cadb7-160">Especifique los prefijos de direcciones Hola son prefijos de hello ubicados en la red local.</span><span class="sxs-lookup"><span data-stu-id="cadb7-160">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="cadb7-161">Si los cambios de red local o necesita toochange Hola la dirección IP para el dispositivo VPN de hello, puede actualizar fácilmente los valores de hello más tarde.</span><span class="sxs-lookup"><span data-stu-id="cadb7-161">If your on-premises network changes or you need toochange hello public IP address for hello VPN device, you can easily update hello values later.</span></span>

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <span data-ttu-id="cadb7-162"><a name="VPNDevice"></a>6. Configurar el dispositivo VPN</span><span class="sxs-lookup"><span data-stu-id="cadb7-162"><a name="VPNDevice"></a>6. Configure your VPN device</span></span>

<span data-ttu-id="cadb7-163">Red local de las conexiones de sitio a sitio tooan requieren un dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="cadb7-163">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="cadb7-164">En este paso, se configura el dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="cadb7-164">In this step, you configure your VPN device.</span></span> <span data-ttu-id="cadb7-165">Al configurar el dispositivo VPN, necesita Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="cadb7-165">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="cadb7-166">Una clave compartida.</span><span class="sxs-lookup"><span data-stu-id="cadb7-166">A shared key.</span></span> <span data-ttu-id="cadb7-167">Esto es Hola mismo compartido clave que se especifique al crear la conexión VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="cadb7-167">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="cadb7-168">En estos ejemplos se utiliza una clave compartida básica.</span><span class="sxs-lookup"><span data-stu-id="cadb7-168">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="cadb7-169">Se recomienda que generar un toouse clave más compleja.</span><span class="sxs-lookup"><span data-stu-id="cadb7-169">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="cadb7-170">Hola dirección IP pública de la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="cadb7-170">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="cadb7-171">Puede ver la dirección IP pública hello mediante Hola portal de Azure, PowerShell o CLI.</span><span class="sxs-lookup"><span data-stu-id="cadb7-171">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="cadb7-172">Hola toofind dirección IP pública de la puerta de enlace VPN con hello portal de Azure, navegue demasiado**puertas de enlace de red Virtual**, a continuación, haga clic en nombre de saludo de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="cadb7-172">toofind hello Public IP address of your VPN gateway using hello Azure portal, navigate too**Virtual network gateways**, then click hello name of your gateway.</span></span>

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <span data-ttu-id="cadb7-173"><a name="CreateConnection"></a>7. Crear la conexión de VPN de Hola</span><span class="sxs-lookup"><span data-stu-id="cadb7-173"><a name="CreateConnection"></a>7. Create hello VPN connection</span></span>

<span data-ttu-id="cadb7-174">Crear la conexión de VPN de sitio a sitio Hola entre la puerta de enlace de red virtual y el dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="cadb7-174">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span>

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <span data-ttu-id="cadb7-175"><a name="VerifyConnection"></a>8. Compruebe la conexión de VPN de Hola</span><span class="sxs-lookup"><span data-stu-id="cadb7-175"><a name="VerifyConnection"></a>8. Verify hello VPN connection</span></span>

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="cadb7-176"><a name="connectVM"></a>máquina virtual de tooconnect tooa</span><span class="sxs-lookup"><span data-stu-id="cadb7-176"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="cadb7-177"><a name="reset"></a>¿Cómo tooreset una puerta de enlace VPN</span><span class="sxs-lookup"><span data-stu-id="cadb7-177"><a name="reset"></a>How tooreset a VPN gateway</span></span>

<span data-ttu-id="cadb7-178">Restablecer una puerta de enlace de VPN de Azure es útil si se pierde la conectividad VPN entre locales en uno o varios túneles VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="cadb7-178">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="cadb7-179">En esta situación, los dispositivos VPN local son todo funciona correctamente, pero son tooestablish imposibilidad de túneles de IPsec con puertas de enlace de VPN de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="cadb7-179">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="cadb7-180">Para conocer los pasos, consulte [Restablecimiento de una puerta de enlace de VPN](vpn-gateway-resetgw-classic.md).</span><span class="sxs-lookup"><span data-stu-id="cadb7-180">For steps, see [Reset a VPN gateway](vpn-gateway-resetgw-classic.md).</span></span>

## <span data-ttu-id="cadb7-181"><a name="resize"></a>¿Cómo toochange una puerta de enlace de SKU (cambio de tamaño de una puerta de enlace)</span><span class="sxs-lookup"><span data-stu-id="cadb7-181"><a name="resize"></a>How toochange a gateway SKU (resize a gateway)</span></span>

<span data-ttu-id="cadb7-182">Para los pasos de hello toochange una SKU de puerta de enlace, vea [SKU de puerta de enlace](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="cadb7-182">For hello steps toochange a gateway SKU, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cadb7-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cadb7-183">Next steps</span></span>

* <span data-ttu-id="cadb7-184">Para obtener información sobre BGP, consulte hello [información general de BGP](vpn-gateway-bgp-overview.md) y [cómo tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="cadb7-184">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="cadb7-185">Para más información acerca de la tunelización forzada, consulte la [información acerca de la tunelización forzada](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="cadb7-185">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="cadb7-186">Para obtener información acerca de las conexiones activo/activo de alta disponibilidad, consulte [Conectividad de alta disponibilidad entre locales y de red virtual a red virtual](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="cadb7-186">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
