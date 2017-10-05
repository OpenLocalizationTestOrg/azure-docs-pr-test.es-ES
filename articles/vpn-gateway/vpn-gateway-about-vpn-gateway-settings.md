---
title: "Configuración de una puerta de enlace de VPN para las conexiones de Azure entre locales | Microsoft Docs"
description: "Obtenga información sobre la configuración de VPN Gateway para las puertas de enlace de red virtual de Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: ae665bc5-0089-45d0-a0d5-bc0ab4e79899
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: cherylmc
ms.openlocfilehash: 07aa6946b9c3994c5afc5c88837f23567b95d8a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a><span data-ttu-id="13028-103">Acerca de la configuración de la puerta de enlace de VPN</span><span class="sxs-lookup"><span data-stu-id="13028-103">About VPN Gateway configuration settings</span></span>

<span data-ttu-id="13028-104">Una puerta de enlace de VPN es un tipo de puerta de enlace de red virtual que envía tráfico cifrado entre la red virtual y la ubicación local a través de una conexión pública.</span><span class="sxs-lookup"><span data-stu-id="13028-104">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span></span> <span data-ttu-id="13028-105">También puede utilizar una puerta de enlace de VPN para enviar tráfico entre redes virtuales a través de la red troncal de Azure.</span><span class="sxs-lookup"><span data-stu-id="13028-105">You can also use a VPN gateway to send traffic between virtual networks across the Azure backbone.</span></span>

<span data-ttu-id="13028-106">Una conexión de puerta de enlace de VPN se basa en la configuración de varios recursos, cada uno de los cuales contiene valores configurables.</span><span class="sxs-lookup"><span data-stu-id="13028-106">A VPN gateway connection relies on the configuration of multiple resources, each of which contains configurable settings.</span></span> <span data-ttu-id="13028-107">Las secciones de este artículo tratan los recursos y la configuración relacionados con una puerta de enlace de VPN para una red virtual creada en el modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="13028-107">The sections in this article discuss the resources and settings that relate to a VPN gateway for a virtual network created in Resource Manager deployment model.</span></span> <span data-ttu-id="13028-108">Puede encontrar las descripciones y los diagramas de topología de cada solución de conexión en el artículo [Acerca de VPN Gateway](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="13028-108">You can find descriptions and topology diagrams for each connection solution in the [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span>

## <span data-ttu-id="13028-109"><a name="gwtype"></a>Tipos de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="13028-109"><a name="gwtype"></a>Gateway types</span></span>

<span data-ttu-id="13028-110">Cada red virtual solo puede tener una puerta de enlace de red de cada tipo.</span><span class="sxs-lookup"><span data-stu-id="13028-110">Each virtual network can only have one virtual network gateway of each type.</span></span> <span data-ttu-id="13028-111">Al crear una puerta de enlace de red virtual, debe asegurarse de que el tipo de puerta de enlace es el correcto para su configuración.</span><span class="sxs-lookup"><span data-stu-id="13028-111">When you are creating a virtual network gateway, you must make sure that the gateway type is correct for your configuration.</span></span>

<span data-ttu-id="13028-112">Los valores disponibles para -GatewayType son:</span><span class="sxs-lookup"><span data-stu-id="13028-112">The available values for -GatewayType are:</span></span>

* <span data-ttu-id="13028-113">VPN</span><span class="sxs-lookup"><span data-stu-id="13028-113">Vpn</span></span>
* <span data-ttu-id="13028-114">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="13028-114">ExpressRoute</span></span>

<span data-ttu-id="13028-115">Una puerta de enlace de VPN requiere `-GatewayType` *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="13028-115">A VPN gateway requires the `-GatewayType` *Vpn*.</span></span>

<span data-ttu-id="13028-116">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="13028-116">Example:</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <span data-ttu-id="13028-117"><a name="gwsku"></a>SKU de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="13028-117"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-the-gateway-sku"></a><span data-ttu-id="13028-118">Configuración de la SKU de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="13028-118">Configure the gateway SKU</span></span>

#### <a name="azure-portal"></a><span data-ttu-id="13028-119">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="13028-119">Azure portal</span></span>

<span data-ttu-id="13028-120">Si usa Azure Portal para crear una puerta de enlace de red virtual de Resource Manager, puede seleccionar la SKU de la puerta de enlace con el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="13028-120">If you use the Azure portal to create a Resource Manager virtual network gateway, you can select the gateway SKU by using the dropdown.</span></span> <span data-ttu-id="13028-121">Las opciones que se presentan corresponden con el tipo de puerta de enlace y tipo de VPN que seleccione.</span><span class="sxs-lookup"><span data-stu-id="13028-121">The options you are presented with correspond to the Gateway type and VPN type that you select.</span></span>

#### <a name="powershell"></a><span data-ttu-id="13028-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="13028-122">PowerShell</span></span>

<span data-ttu-id="13028-123">En el siguiente ejemplo de PowerShell se especifica `-GatewaySku` como VpnGw1.</span><span class="sxs-lookup"><span data-stu-id="13028-123">The following PowerShell example specifies the `-GatewaySku` as VpnGw1.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <span data-ttu-id="13028-124"><a name="resize"></a>Cambio de tamaño de una SKU de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="13028-124"><a name="resize"></a>Change (resize) a gateway SKU</span></span>

<span data-ttu-id="13028-125">Si quiere actualizar la SKU de su puerta de enlace a una SKU más eficaz, puede usar el cmdlet `Resize-AzureRmVirtualNetworkGateway` de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="13028-125">If you want to upgrade your gateway SKU to a more powerful SKU, you can use the `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span></span> <span data-ttu-id="13028-126">También puede cambiar a una versión anterior del tamaño de la SKU de puerta de enlace con este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="13028-126">You can also downgrade the gateway SKU size using this cmdlet.</span></span>

<span data-ttu-id="13028-127">En el siguiente ejemplo de PowerShell se muestra una SKU de puerta de enlace cuyo tamaño se ha cambiado a VpnGw2.</span><span class="sxs-lookup"><span data-stu-id="13028-127">The following PowerShell example shows a gateway SKU being resized to VpnGw2.</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <span data-ttu-id="13028-128"><a name="connectiontype"></a>Tipos de conexión</span><span class="sxs-lookup"><span data-stu-id="13028-128"><a name="connectiontype"></a>Connection types</span></span>

<span data-ttu-id="13028-129">En el modelo de implementación de Resource Manager, cada configuración requiere un tipo de conexión de puerta de enlace de red virtual específico.</span><span class="sxs-lookup"><span data-stu-id="13028-129">In the Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span></span> <span data-ttu-id="13028-130">Los valores de PowerShell de Resource Manager para `-ConnectionType` son:</span><span class="sxs-lookup"><span data-stu-id="13028-130">The available Resource Manager PowerShell values for `-ConnectionType` are:</span></span>

* <span data-ttu-id="13028-131">IPsec</span><span class="sxs-lookup"><span data-stu-id="13028-131">IPsec</span></span>
* <span data-ttu-id="13028-132">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="13028-132">Vnet2Vnet</span></span>
* <span data-ttu-id="13028-133">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="13028-133">ExpressRoute</span></span>
* <span data-ttu-id="13028-134">VPNClient</span><span class="sxs-lookup"><span data-stu-id="13028-134">VPNClient</span></span>

<span data-ttu-id="13028-135">En el siguiente ejemplo de PowerShell, vamos a crear una conexión de S2S que requiere el tipo de conexión *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="13028-135">In the following PowerShell example, we create a S2S connection that requires the connection type *IPsec*.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <span data-ttu-id="13028-136"><a name="vpntype"></a>Tipos de VPN</span><span class="sxs-lookup"><span data-stu-id="13028-136"><a name="vpntype"></a>VPN types</span></span>

<span data-ttu-id="13028-137">Al crear la puerta de enlace de red virtual para una configuración de puerta de enlace de VPN, debe especificar un tipo de VPN.</span><span class="sxs-lookup"><span data-stu-id="13028-137">When you create the virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span></span> <span data-ttu-id="13028-138">El tipo de VPN que elija dependerá de la topología de conexión que desee crear.</span><span class="sxs-lookup"><span data-stu-id="13028-138">The VPN type that you choose depends on the connection topology that you want to create.</span></span> <span data-ttu-id="13028-139">Por ejemplo, una conexión de P2S requiere un tipo de VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="13028-139">For example, a P2S connection requires a RouteBased VPN type.</span></span> <span data-ttu-id="13028-140">Un tipo de VPN también puede depender del hardware que se esté usando.</span><span class="sxs-lookup"><span data-stu-id="13028-140">A VPN type can also depend on the hardware that you are using.</span></span> <span data-ttu-id="13028-141">Las configuraciones de S2S requieren un dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="13028-141">S2S configurations require a VPN device.</span></span> <span data-ttu-id="13028-142">Algunos dispositivos VPN solo serán compatibles con un determinado tipo de VPN.</span><span class="sxs-lookup"><span data-stu-id="13028-142">Some VPN devices only support a certain VPN type.</span></span>

<span data-ttu-id="13028-143">El tipo de VPN que seleccione debe cumplir todos los requisitos de conexión de la solución que desea crear.</span><span class="sxs-lookup"><span data-stu-id="13028-143">The VPN type you select must satisfy all the connection requirements for the solution you want to create.</span></span> <span data-ttu-id="13028-144">Por ejemplo, si desea crear una conexión de puerta de enlace de VPN de S2S y una conexión de puerta de enlace de VPN de P2S para la misma red virtual, debería usar el tipo de VPN *RouteBased* , dado que P2S requiere un tipo de VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="13028-144">For example, if you want to create a S2S VPN gateway connection and a P2S VPN gateway connection for the same virtual network, you would use VPN type *RouteBased* because P2S requires a RouteBased VPN type.</span></span> <span data-ttu-id="13028-145">También necesitaría comprobar que el dispositivo VPN admite una conexión de VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="13028-145">You would also need to verify that your VPN device supported a RouteBased VPN connection.</span></span> 

<span data-ttu-id="13028-146">Una vez que se ha creado una puerta de enlace de red virtual, no puede cambiar el tipo de VPN.</span><span class="sxs-lookup"><span data-stu-id="13028-146">Once a virtual network gateway has been created, you can't change the VPN type.</span></span> <span data-ttu-id="13028-147">Tendrá que eliminar la puerta de enlace de red virtual y crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="13028-147">You have to delete the virtual network gateway and create a new one.</span></span> <span data-ttu-id="13028-148">Hay dos tipos de VPN:</span><span class="sxs-lookup"><span data-stu-id="13028-148">There are two VPN types:</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="13028-149">En el siguiente ejemplo de PowerShell se especifica `-VpnType` como *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="13028-149">The following PowerShell example specifies the `-VpnType` as *RouteBased*.</span></span> <span data-ttu-id="13028-150">Al crear una puerta de enlace, debe asegurarse de que el tipo de VPN es el correcto para su configuración.</span><span class="sxs-lookup"><span data-stu-id="13028-150">When you are creating a gateway, you must make sure that the -VpnType is correct for your configuration.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <span data-ttu-id="13028-151"><a name="requirements"></a>Requisitos de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="13028-151"><a name="requirements"></a>Gateway requirements</span></span>

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <span data-ttu-id="13028-152"><a name="gwsub"></a>Subred de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="13028-152"><a name="gwsub"></a>Gateway subnet</span></span>

<span data-ttu-id="13028-153">Antes de crear una puerta de enlace de VPN, debe crear una subred de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="13028-153">Before you create a VPN gateway, you must create a gateway subnet.</span></span> <span data-ttu-id="13028-154">La subred de puerta de enlace contiene las direcciones IP que usan los servicios y las máquinas virtuales de la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="13028-154">The gateway subnet contains the IP addresses that the virtual network gateway VMs and services use.</span></span> <span data-ttu-id="13028-155">Al crear la puerta de enlace de red virtual, las máquinas virtuales de puerta de enlace se implementan en la subred de puerta de enlace, y se configuran con las opciones de puerta de enlace de VPN necesarias.</span><span class="sxs-lookup"><span data-stu-id="13028-155">When you create your virtual network gateway, gateway VMs are deployed to the gateway subnet and configured with the required VPN gateway settings.</span></span> <span data-ttu-id="13028-156">No debe implementar nunca nada más (por ejemplo, máquinas virtuales adicionales) en la subred de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="13028-156">You must never deploy anything else (for example, additional VMs) to the gateway subnet.</span></span> <span data-ttu-id="13028-157">Para que la subred de puerta de enlace funcione correctamente, su nombre tiene que ser “GatewaySubnet2”.</span><span class="sxs-lookup"><span data-stu-id="13028-157">The gateway subnet must be named 'GatewaySubnet' to work properly.</span></span> <span data-ttu-id="13028-158">La asignación del nombre "GatewaySubnet" a la subred de puerta de enlace permite a Azure saber que se trata de la subred donde se implementarán las máquinas virtuales y los servicios de la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="13028-158">Naming the gateway subnet 'GatewaySubnet' lets Azure know that this is the subnet to deploy the virtual network gateway VMs and services to.</span></span>

<span data-ttu-id="13028-159">Al crear la subred de puerta de enlace, especifique el número de direcciones IP que contiene la subred.</span><span class="sxs-lookup"><span data-stu-id="13028-159">When you create the gateway subnet, you specify the number of IP addresses that the subnet contains.</span></span> <span data-ttu-id="13028-160">Las direcciones IP de la subred de puerta de enlace se asignan a las máquinas virtuales y los servicios de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="13028-160">The IP addresses in the gateway subnet are allocated to the gateway VMs and gateway services.</span></span> <span data-ttu-id="13028-161">Algunas configuraciones requieren más direcciones IP que otras.</span><span class="sxs-lookup"><span data-stu-id="13028-161">Some configurations require more IP addresses than others.</span></span> <span data-ttu-id="13028-162">Consulte los requisitos de configuración que desea crear y compruebe que la subred de puerta de enlace que desea crear los cumple.</span><span class="sxs-lookup"><span data-stu-id="13028-162">Look at the instructions for the configuration that you want to create and verify that the gateway subnet you want to create meets those requirements.</span></span> <span data-ttu-id="13028-163">Debe asegurarse también de que la subred de puerta de enlace contenga suficientes direcciones IP para acomodar posibles configuraciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="13028-163">Additionally, you may want to make sure your gateway subnet contains enough IP addresses to accommodate possible future additional configurations.</span></span> <span data-ttu-id="13028-164">Aunque es posible crear una subred de puerta de enlace tan pequeña como /29, se recomienda que sea /28 o mayor (/28, /27, /26, etc.).</span><span class="sxs-lookup"><span data-stu-id="13028-164">While you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /28 or larger (/28, /27, /26 etc.).</span></span> <span data-ttu-id="13028-165">De este modo, si agrega funcionalidad en el futuro, no tendrá que retirar la puerta de enlace y luego eliminar y volver a crear la subred de puerta de enlace para admitir más direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="13028-165">That way, if you add functionality in the future, you won't have to tear your gateway, then delete and recreate the gateway subnet to allow for more IP addresses.</span></span>

<span data-ttu-id="13028-166">En el ejemplo de PowerShell de Resource Manager siguiente, se muestra una subred de puerta de enlace con el nombre GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="13028-166">The following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span></span> <span data-ttu-id="13028-167">Puede ver que la notación CIDR especifica /27, que permite suficientes direcciones IP para la mayoría de las configuraciones que existen.</span><span class="sxs-lookup"><span data-stu-id="13028-167">You can see the CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <span data-ttu-id="13028-168"><a name="lng"></a>Puertas de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="13028-168"><a name="lng"></a>Local network gateways</span></span>

<span data-ttu-id="13028-169">Al crear una configuración de puerta de enlace de VPN, la puerta de enlace de red local a menudo representa la ubicación local.</span><span class="sxs-lookup"><span data-stu-id="13028-169">When creating a VPN gateway configuration, the local network gateway often represents your on-premises location.</span></span> <span data-ttu-id="13028-170">En el modelo de implementación clásica, la puerta de enlace de red local se conoce como un sitio local.</span><span class="sxs-lookup"><span data-stu-id="13028-170">In the classic deployment model, the local network gateway was referred to as a Local Site.</span></span> 

<span data-ttu-id="13028-171">Debe asignar un nombre a la puerta de enlace de red local, así como la dirección IP pública del dispositivo VPN local, y especificar los prefijos de dirección que se encuentran en la ubicación local.</span><span class="sxs-lookup"><span data-stu-id="13028-171">You give the local network gateway a name, the public IP address of the on-premises VPN device, and specify the address prefixes that are located on the on-premises location.</span></span> <span data-ttu-id="13028-172">Azure examina los prefijos de dirección de destino para el tráfico de red, consulta la configuración que especificó para la puerta de enlace de red local y enruta los paquetes según corresponda.</span><span class="sxs-lookup"><span data-stu-id="13028-172">Azure looks at the destination address prefixes for network traffic, consults the configuration that you have specified for your local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="13028-173">También debe especificar puertas de enlace de red local para configuraciones de red virtual a red virtual local que usan una conexión de puerta de enlace de VPN.</span><span class="sxs-lookup"><span data-stu-id="13028-173">You also specify local network gateways for VNet-to-VNet configurations that use a VPN gateway connection.</span></span>

<span data-ttu-id="13028-174">En el ejemplo siguiente de PowerShell, se crea una nueva puerta de enlace de red local:</span><span class="sxs-lookup"><span data-stu-id="13028-174">The following PowerShell example creates a new local network gateway:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

<span data-ttu-id="13028-175">A veces es necesario modificar la configuración de la puerta de enlace de red local.</span><span class="sxs-lookup"><span data-stu-id="13028-175">Sometimes you need to modify the local network gateway settings.</span></span> <span data-ttu-id="13028-176">Por ejemplo, al agregar o modificar el intervalo de direcciones, o si cambia la dirección IP del dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="13028-176">For example, when you add or modify the address range, or if the IP address of the VPN device changes.</span></span> <span data-ttu-id="13028-177">Para una red virtual clásica, puede cambiar esta configuración en el portal clásico, en la página de redes locales.</span><span class="sxs-lookup"><span data-stu-id="13028-177">For a classic VNet, you can change these settings in the classic portal on the Local Networks page.</span></span> <span data-ttu-id="13028-178">Para Resource Manager, consulte [Modificación de la configuración de la puerta de enlace de red local mediante PowerShell](vpn-gateway-modify-local-network-gateway.md)</span><span class="sxs-lookup"><span data-stu-id="13028-178">For Resource Manager, see [Modify local network gateway settings using PowerShell](vpn-gateway-modify-local-network-gateway.md).</span></span>

## <span data-ttu-id="13028-179"><a name="resources"></a>API de REST y cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="13028-179"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>

<span data-ttu-id="13028-180">Para más información sobre los recursos técnicos y los requisitos de sintaxis específicos para usar las API de REST y los cmdlets de PowerShell para configuraciones de VPN Gateway, consulte las páginas siguientes:</span><span class="sxs-lookup"><span data-stu-id="13028-180">For additional technical resources and specific syntax requirements when using REST APIs, PowerShell cmdlets, or Azure CLI for VPN Gateway configurations, see the following pages:</span></span>

| <span data-ttu-id="13028-181">**Clásico**</span><span class="sxs-lookup"><span data-stu-id="13028-181">**Classic**</span></span> | <span data-ttu-id="13028-182">**Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="13028-182">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="13028-183">PowerShell</span><span class="sxs-lookup"><span data-stu-id="13028-183">PowerShell</span></span>](/powershell/module/azure#networking) |[<span data-ttu-id="13028-184">PowerShell</span><span class="sxs-lookup"><span data-stu-id="13028-184">PowerShell</span></span>](/powershell/module/azurerm.network#vpn) |
| [<span data-ttu-id="13028-185">API DE REST</span><span class="sxs-lookup"><span data-stu-id="13028-185">REST API</span></span>](https://msdn.microsoft.com/library/jj154113) |[<span data-ttu-id="13028-186">API de REST</span><span class="sxs-lookup"><span data-stu-id="13028-186">REST API</span></span>](/rest/api/network/virtualnetworkgateways) |
| <span data-ttu-id="13028-187">No compatible</span><span class="sxs-lookup"><span data-stu-id="13028-187">Not supported</span></span> | [<span data-ttu-id="13028-188">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="13028-188">Azure CLI</span></span>](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a><span data-ttu-id="13028-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="13028-189">Next steps</span></span>

<span data-ttu-id="13028-190">Para más información sobre las configuraciones de conexión disponibles, vea [About VPN Gateway (Acerca de VPN Gateway)](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="13028-190">For more information about available connection configurations, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>