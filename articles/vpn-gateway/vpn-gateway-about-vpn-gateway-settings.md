---
title: "configuración de puerta de enlace de aaaVPN para las conexiones de Azure entre entornos | Documentos de Microsoft"
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
ms.openlocfilehash: 01229d99fa37e30e00aa00f939f488d631b5593c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a><span data-ttu-id="15437-103">Acerca de la configuración de la puerta de enlace de VPN</span><span class="sxs-lookup"><span data-stu-id="15437-103">About VPN Gateway configuration settings</span></span>

<span data-ttu-id="15437-104">Una puerta de enlace de VPN es un tipo de puerta de enlace de red virtual que envía tráfico cifrado entre la red virtual y la ubicación local a través de una conexión pública.</span><span class="sxs-lookup"><span data-stu-id="15437-104">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span></span> <span data-ttu-id="15437-105">También puede utilizar un tráfico de toosend de puerta de enlace VPN entre redes virtuales en hello red troncal de Azure.</span><span class="sxs-lookup"><span data-stu-id="15437-105">You can also use a VPN gateway toosend traffic between virtual networks across hello Azure backbone.</span></span>

<span data-ttu-id="15437-106">Una conexión de puerta de enlace VPN se basa en la configuración de Hola de varios recursos, cada uno de los cuales contiene valores configurables.</span><span class="sxs-lookup"><span data-stu-id="15437-106">A VPN gateway connection relies on hello configuration of multiple resources, each of which contains configurable settings.</span></span> <span data-ttu-id="15437-107">secciones de Hello en este artículo describen los recursos de Hola y opciones relacionadas con la puerta de enlace VPN de tooa para una red virtual que creó en el modelo de implementación del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="15437-107">hello sections in this article discuss hello resources and settings that relate tooa VPN gateway for a virtual network created in Resource Manager deployment model.</span></span> <span data-ttu-id="15437-108">Puede encontrar descripciones y diagramas de topología para cada solución de conexión en hello [acerca de la puerta de enlace VPN](vpn-gateway-about-vpngateways.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="15437-108">You can find descriptions and topology diagrams for each connection solution in hello [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span>

## <span data-ttu-id="15437-109"><a name="gwtype"></a>Tipos de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="15437-109"><a name="gwtype"></a>Gateway types</span></span>

<span data-ttu-id="15437-110">Cada red virtual solo puede tener una puerta de enlace de red de cada tipo.</span><span class="sxs-lookup"><span data-stu-id="15437-110">Each virtual network can only have one virtual network gateway of each type.</span></span> <span data-ttu-id="15437-111">Cuando se crea una puerta de enlace de red virtual, debe asegurarse de que es correcto para la configuración del tipo de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="15437-111">When you are creating a virtual network gateway, you must make sure that hello gateway type is correct for your configuration.</span></span>

<span data-ttu-id="15437-112">Hola valores disponibles para el GatewayType - son:</span><span class="sxs-lookup"><span data-stu-id="15437-112">hello available values for -GatewayType are:</span></span>

* <span data-ttu-id="15437-113">VPN</span><span class="sxs-lookup"><span data-stu-id="15437-113">Vpn</span></span>
* <span data-ttu-id="15437-114">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="15437-114">ExpressRoute</span></span>

<span data-ttu-id="15437-115">Una puerta de enlace VPN requiere hello `-GatewayType` *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="15437-115">A VPN gateway requires hello `-GatewayType` *Vpn*.</span></span>

<span data-ttu-id="15437-116">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="15437-116">Example:</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <span data-ttu-id="15437-117"><a name="gwsku"></a>SKU de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="15437-117"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-hello-gateway-sku"></a><span data-ttu-id="15437-118">Configurar la puerta de enlace de hello SKU</span><span class="sxs-lookup"><span data-stu-id="15437-118">Configure hello gateway SKU</span></span>

#### <a name="azure-portal"></a><span data-ttu-id="15437-119">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="15437-119">Azure portal</span></span>

<span data-ttu-id="15437-120">Si usas hello toocreate portal Azure una puerta de enlace de red virtual del Administrador de recursos, puede seleccionar SKU de puerta de enlace de hello mediante el uso de la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="15437-120">If you use hello Azure portal toocreate a Resource Manager virtual network gateway, you can select hello gateway SKU by using hello dropdown.</span></span> <span data-ttu-id="15437-121">Opciones de Hola con que se presentan corresponden toohello tipo de puerta de enlace y el tipo VPN que seleccione.</span><span class="sxs-lookup"><span data-stu-id="15437-121">hello options you are presented with correspond toohello Gateway type and VPN type that you select.</span></span>

#### <a name="powershell"></a><span data-ttu-id="15437-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="15437-122">PowerShell</span></span>

<span data-ttu-id="15437-123">el ejemplo siguiente se PowerShell Hello especifica hello `-GatewaySku` como VpnGw1.</span><span class="sxs-lookup"><span data-stu-id="15437-123">hello following PowerShell example specifies hello `-GatewaySku` as VpnGw1.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <span data-ttu-id="15437-124"><a name="resize"></a>Cambio de tamaño de una SKU de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="15437-124"><a name="resize"></a>Change (resize) a gateway SKU</span></span>

<span data-ttu-id="15437-125">Si desea que tooupgrade su tooa SKU de puerta de enlace SKU más eficaz, puede usar hello `Resize-AzureRmVirtualNetworkGateway` cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15437-125">If you want tooupgrade your gateway SKU tooa more powerful SKU, you can use hello `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span></span> <span data-ttu-id="15437-126">También puede cambiar el tamaño de la SKU de puerta de enlace Hola con este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="15437-126">You can also downgrade hello gateway SKU size using this cmdlet.</span></span>

<span data-ttu-id="15437-127">Hola PowerShell ejemplo siguiente se muestra que un SKU de puerta de enlace se cambia el tamaño tooVpnGw2.</span><span class="sxs-lookup"><span data-stu-id="15437-127">hello following PowerShell example shows a gateway SKU being resized tooVpnGw2.</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <span data-ttu-id="15437-128"><a name="connectiontype"></a>Tipos de conexión</span><span class="sxs-lookup"><span data-stu-id="15437-128"><a name="connectiontype"></a>Connection types</span></span>

<span data-ttu-id="15437-129">En el modelo de implementación del Administrador de recursos de hello, cada configuración requiere un tipo de conexión de puerta de enlace de red virtual específica.</span><span class="sxs-lookup"><span data-stu-id="15437-129">In hello Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span></span> <span data-ttu-id="15437-130">Hello PowerShell Administrador de recursos disponibles los valores de `-ConnectionType` son:</span><span class="sxs-lookup"><span data-stu-id="15437-130">hello available Resource Manager PowerShell values for `-ConnectionType` are:</span></span>

* <span data-ttu-id="15437-131">IPsec</span><span class="sxs-lookup"><span data-stu-id="15437-131">IPsec</span></span>
* <span data-ttu-id="15437-132">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="15437-132">Vnet2Vnet</span></span>
* <span data-ttu-id="15437-133">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="15437-133">ExpressRoute</span></span>
* <span data-ttu-id="15437-134">VPNClient</span><span class="sxs-lookup"><span data-stu-id="15437-134">VPNClient</span></span>

<span data-ttu-id="15437-135">En el siguiente ejemplo de PowerShell de hello, creamos una conexión de S2S que requiere el tipo de conexión de hello *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="15437-135">In hello following PowerShell example, we create a S2S connection that requires hello connection type *IPsec*.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <span data-ttu-id="15437-136"><a name="vpntype"></a>Tipos de VPN</span><span class="sxs-lookup"><span data-stu-id="15437-136"><a name="vpntype"></a>VPN types</span></span>

<span data-ttu-id="15437-137">Cuando se crea la puerta de enlace de red virtual de Hola para una configuración de puerta de enlace VPN, debe especificar un tipo VPN.</span><span class="sxs-lookup"><span data-stu-id="15437-137">When you create hello virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span></span> <span data-ttu-id="15437-138">Hola tipo VPN que elija depende de topología de conexión de Hola que desea toocreate.</span><span class="sxs-lookup"><span data-stu-id="15437-138">hello VPN type that you choose depends on hello connection topology that you want toocreate.</span></span> <span data-ttu-id="15437-139">Por ejemplo, una conexión de P2S requiere un tipo de VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="15437-139">For example, a P2S connection requires a RouteBased VPN type.</span></span> <span data-ttu-id="15437-140">Un tipo VPN también puede depender de hardware de Hola que está usando.</span><span class="sxs-lookup"><span data-stu-id="15437-140">A VPN type can also depend on hello hardware that you are using.</span></span> <span data-ttu-id="15437-141">Las configuraciones de S2S requieren un dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="15437-141">S2S configurations require a VPN device.</span></span> <span data-ttu-id="15437-142">Algunos dispositivos VPN solo serán compatibles con un determinado tipo de VPN.</span><span class="sxs-lookup"><span data-stu-id="15437-142">Some VPN devices only support a certain VPN type.</span></span>

<span data-ttu-id="15437-143">Hola seleccione el tipo de VPN debe cumplir todos los requisitos de conexión de hello para la solución de hello que desea toocreate.</span><span class="sxs-lookup"><span data-stu-id="15437-143">hello VPN type you select must satisfy all hello connection requirements for hello solution you want toocreate.</span></span> <span data-ttu-id="15437-144">Por ejemplo, si desea que toocreate una conexión de puerta de enlace de VPN de S2S y una conexión de puerta de enlace de VPN de P2S para Hola misma red virtual, se utilizaría el tipo de VPN *RouteBased* porque P2S requiere un tipo RouteBased VPN.</span><span class="sxs-lookup"><span data-stu-id="15437-144">For example, if you want toocreate a S2S VPN gateway connection and a P2S VPN gateway connection for hello same virtual network, you would use VPN type *RouteBased* because P2S requires a RouteBased VPN type.</span></span> <span data-ttu-id="15437-145">También necesitaría tooverify que el dispositivo VPN admite una conexión VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="15437-145">You would also need tooverify that your VPN device supported a RouteBased VPN connection.</span></span> 

<span data-ttu-id="15437-146">Una vez creada una puerta de enlace de red virtual, no se puede cambiar el tipo de VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="15437-146">Once a virtual network gateway has been created, you can't change hello VPN type.</span></span> <span data-ttu-id="15437-147">Tener toodelete Hola puerta de enlace de red virtual y cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="15437-147">You have toodelete hello virtual network gateway and create a new one.</span></span> <span data-ttu-id="15437-148">Hay dos tipos de VPN:</span><span class="sxs-lookup"><span data-stu-id="15437-148">There are two VPN types:</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="15437-149">el ejemplo siguiente se PowerShell Hello especifica hello `-VpnType` como *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="15437-149">hello following PowerShell example specifies hello `-VpnType` as *RouteBased*.</span></span> <span data-ttu-id="15437-150">Cuando se crea una puerta de enlace, debe asegurarse de que ese hello - VpnType es correcto para su configuración.</span><span class="sxs-lookup"><span data-stu-id="15437-150">When you are creating a gateway, you must make sure that hello -VpnType is correct for your configuration.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <span data-ttu-id="15437-151"><a name="requirements"></a>Requisitos de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="15437-151"><a name="requirements"></a>Gateway requirements</span></span>

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <span data-ttu-id="15437-152"><a name="gwsub"></a>Subred de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="15437-152"><a name="gwsub"></a>Gateway subnet</span></span>

<span data-ttu-id="15437-153">Antes de crear una puerta de enlace de VPN, debe crear una subred de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="15437-153">Before you create a VPN gateway, you must create a gateway subnet.</span></span> <span data-ttu-id="15437-154">subred de puerta de enlace de Hello contiene direcciones IP de hello esa puerta de enlace de red virtual de hello las máquinas virtuales y servicios de uso.</span><span class="sxs-lookup"><span data-stu-id="15437-154">hello gateway subnet contains hello IP addresses that hello virtual network gateway VMs and services use.</span></span> <span data-ttu-id="15437-155">Al crear la puerta de enlace de red virtual, puerta de enlace de máquinas virtuales son subred de puerta de enlace de toohello implementado y configurado con la configuración de puerta de enlace VPN de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="15437-155">When you create your virtual network gateway, gateway VMs are deployed toohello gateway subnet and configured with hello required VPN gateway settings.</span></span> <span data-ttu-id="15437-156">Nunca debe implementar la subred de puerta de enlace de toohello nada (por ejemplo, máquinas virtuales adicionales).</span><span class="sxs-lookup"><span data-stu-id="15437-156">You must never deploy anything else (for example, additional VMs) toohello gateway subnet.</span></span> <span data-ttu-id="15437-157">subred de puerta de enlace de Hello debe denominarse "GatewaySubnet" toowork correctamente.</span><span class="sxs-lookup"><span data-stu-id="15437-157">hello gateway subnet must be named 'GatewaySubnet' toowork properly.</span></span> <span data-ttu-id="15437-158">Nombres de subred de puerta de enlace de hello permite "GatewaySubnet" Azure sabe que esto es el enlace de red virtual Hola de subred toodeploy hello las máquinas virtuales y servicios a.</span><span class="sxs-lookup"><span data-stu-id="15437-158">Naming hello gateway subnet 'GatewaySubnet' lets Azure know that this is hello subnet toodeploy hello virtual network gateway VMs and services to.</span></span>

<span data-ttu-id="15437-159">Cuando se crea la subred de puerta de enlace de hello, especifica Hola número de direcciones IP que Hola subred contiene.</span><span class="sxs-lookup"><span data-stu-id="15437-159">When you create hello gateway subnet, you specify hello number of IP addresses that hello subnet contains.</span></span> <span data-ttu-id="15437-160">direcciones IP de Hello en la subred de puerta de enlace de hello son la puerta de enlace de toohello asignado las máquinas virtuales y servicios de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="15437-160">hello IP addresses in hello gateway subnet are allocated toohello gateway VMs and gateway services.</span></span> <span data-ttu-id="15437-161">Algunas configuraciones requieren más direcciones IP que otras.</span><span class="sxs-lookup"><span data-stu-id="15437-161">Some configurations require more IP addresses than others.</span></span> <span data-ttu-id="15437-162">Buscar en las instrucciones de hello para la configuración de Hola que desee toocreate y comprobar esa subred de puerta de enlace de hello desea toocreate cumple estos requisitos.</span><span class="sxs-lookup"><span data-stu-id="15437-162">Look at hello instructions for hello configuration that you want toocreate and verify that hello gateway subnet you want toocreate meets those requirements.</span></span> <span data-ttu-id="15437-163">Además, puede que desee toomake seguro de que la subred de puerta de enlace contiene suficientes IP direcciones tooaccommodate posibles futuras configuraciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="15437-163">Additionally, you may want toomake sure your gateway subnet contains enough IP addresses tooaccommodate possible future additional configurations.</span></span> <span data-ttu-id="15437-164">Aunque es posible crear una subred de puerta de enlace tan pequeña como /29, se recomienda que sea /28 o mayor (/28, /27, /26, etc.).</span><span class="sxs-lookup"><span data-stu-id="15437-164">While you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /28 or larger (/28, /27, /26 etc.).</span></span> <span data-ttu-id="15437-165">De este modo, si agrega funcionalidad de hello futura, no tienen tootear la puerta de enlace, a continuación, elimine y vuelva a hello tooallow de subred de puerta de enlace de más direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="15437-165">That way, if you add functionality in hello future, you won't have tootear your gateway, then delete and recreate hello gateway subnet tooallow for more IP addresses.</span></span>

<span data-ttu-id="15437-166">Hello siguiente ejemplo de PowerShell del Administrador de recursos muestra una subred de puerta de enlace con el nombre GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="15437-166">hello following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span></span> <span data-ttu-id="15437-167">Puede ver la notación CIDR Hola especifica un /27, que permite suficientes direcciones IP para la mayoría de las configuraciones que existen actualmente.</span><span class="sxs-lookup"><span data-stu-id="15437-167">You can see hello CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <span data-ttu-id="15437-168"><a name="lng"></a>Puertas de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="15437-168"><a name="lng"></a>Local network gateways</span></span>

<span data-ttu-id="15437-169">Al crear una configuración de puerta de enlace VPN, puerta de enlace de red local de hello suele representa la ubicación local.</span><span class="sxs-lookup"><span data-stu-id="15437-169">When creating a VPN gateway configuration, hello local network gateway often represents your on-premises location.</span></span> <span data-ttu-id="15437-170">En el modelo de implementación clásica de hello, puerta de enlace de red local de Hola era tooas que se hace referencia un sitio Local.</span><span class="sxs-lookup"><span data-stu-id="15437-170">In hello classic deployment model, hello local network gateway was referred tooas a Local Site.</span></span> 

<span data-ttu-id="15437-171">Asigne un nombre de puerta de enlace de red local de hello, Hola dirección IP pública del dispositivo VPN de hello local y especificar los prefijos de dirección de Hola que se encuentran en la ubicación local de Hola.</span><span class="sxs-lookup"><span data-stu-id="15437-171">You give hello local network gateway a name, hello public IP address of hello on-premises VPN device, and specify hello address prefixes that are located on hello on-premises location.</span></span> <span data-ttu-id="15437-172">Azure examina prefijos de dirección de destino de hello para el tráfico de red, consulta la configuración de Hola que ha especificado para la puerta de enlace de red local y enruta paquetes según corresponda.</span><span class="sxs-lookup"><span data-stu-id="15437-172">Azure looks at hello destination address prefixes for network traffic, consults hello configuration that you have specified for your local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="15437-173">También debe especificar puertas de enlace de red local para configuraciones de red virtual a red virtual local que usan una conexión de puerta de enlace de VPN.</span><span class="sxs-lookup"><span data-stu-id="15437-173">You also specify local network gateways for VNet-to-VNet configurations that use a VPN gateway connection.</span></span>

<span data-ttu-id="15437-174">Hola PowerShell ejemplo siguiente crea una nueva puerta de enlace de red local:</span><span class="sxs-lookup"><span data-stu-id="15437-174">hello following PowerShell example creates a new local network gateway:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

<span data-ttu-id="15437-175">En ciertas ocasiones necesitará configuración de puerta de enlace de red local toomodify Hola.</span><span class="sxs-lookup"><span data-stu-id="15437-175">Sometimes you need toomodify hello local network gateway settings.</span></span> <span data-ttu-id="15437-176">Por ejemplo, al agregar o modificar el intervalo de direcciones de hello, si Hola cambio o dirección IP del dispositivo VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="15437-176">For example, when you add or modify hello address range, or if hello IP address of hello VPN device changes.</span></span> <span data-ttu-id="15437-177">Para una red virtual clásica, puede cambiar esta configuración en el portal clásico de hello en la página redes locales de Hola.</span><span class="sxs-lookup"><span data-stu-id="15437-177">For a classic VNet, you can change these settings in hello classic portal on hello Local Networks page.</span></span> <span data-ttu-id="15437-178">Para Resource Manager, consulte [Modificación de la configuración de la puerta de enlace de red local mediante PowerShell](vpn-gateway-modify-local-network-gateway.md)</span><span class="sxs-lookup"><span data-stu-id="15437-178">For Resource Manager, see [Modify local network gateway settings using PowerShell](vpn-gateway-modify-local-network-gateway.md).</span></span>

## <span data-ttu-id="15437-179"><a name="resources"></a>API de REST y cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="15437-179"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>

<span data-ttu-id="15437-180">Para recursos técnicos adicionales y requisitos de sintaxis específica cuando se usa la API de REST, cmdlets de PowerShell o CLI de Azure para las configuraciones de puerta de enlace de VPN, vea Hola siguientes páginas:</span><span class="sxs-lookup"><span data-stu-id="15437-180">For additional technical resources and specific syntax requirements when using REST APIs, PowerShell cmdlets, or Azure CLI for VPN Gateway configurations, see hello following pages:</span></span>

| <span data-ttu-id="15437-181">**Clásico**</span><span class="sxs-lookup"><span data-stu-id="15437-181">**Classic**</span></span> | <span data-ttu-id="15437-182">**Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="15437-182">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="15437-183">PowerShell</span><span class="sxs-lookup"><span data-stu-id="15437-183">PowerShell</span></span>](/powershell/module/azure#networking) |[<span data-ttu-id="15437-184">PowerShell</span><span class="sxs-lookup"><span data-stu-id="15437-184">PowerShell</span></span>](/powershell/module/azurerm.network#vpn) |
| [<span data-ttu-id="15437-185">API DE REST</span><span class="sxs-lookup"><span data-stu-id="15437-185">REST API</span></span>](https://msdn.microsoft.com/library/jj154113) |[<span data-ttu-id="15437-186">API de REST</span><span class="sxs-lookup"><span data-stu-id="15437-186">REST API</span></span>](/rest/api/network/virtualnetworkgateways) |
| <span data-ttu-id="15437-187">No compatible</span><span class="sxs-lookup"><span data-stu-id="15437-187">Not supported</span></span> | [<span data-ttu-id="15437-188">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="15437-188">Azure CLI</span></span>](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a><span data-ttu-id="15437-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="15437-189">Next steps</span></span>

<span data-ttu-id="15437-190">Para más información sobre las configuraciones de conexión disponibles, vea [About VPN Gateway (Acerca de VPN Gateway)](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="15437-190">For more information about available connection configurations, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>