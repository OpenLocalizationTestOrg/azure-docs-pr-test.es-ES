---
title: "Planeamiento y diseño de conexiones entre sitios locales: Azure VPN Gateway | Microsoft Docs"
description: "Obtenga información acerca del planeamiento y diseño de VPN Gateway para conexiones entre sitios locales, híbridos y entre redes virtuales"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d5aaab83-4e74-4484-8bf0-cc465811e757
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/27/2017
ms.author: cherylmc
ms.openlocfilehash: 3d4587ba31d163384212eca88a7e2c0ba8f3b21f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a><span data-ttu-id="d8b18-103">Planeamiento y diseño de VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="d8b18-103">Planning and design for VPN Gateway</span></span>

<span data-ttu-id="d8b18-104">Planear y diseñar configuraciones entre sitios locales y entre redes virtuales puede resultar simple o complejo, según las necesidades de la red.</span><span class="sxs-lookup"><span data-stu-id="d8b18-104">Planning and designing your cross-premises and VNet-to-VNet configurations can be either simple, or complicated, depending on your networking needs.</span></span> <span data-ttu-id="d8b18-105">Este artículo le guía a través de las consideraciones de diseño y planeamiento básicas.</span><span class="sxs-lookup"><span data-stu-id="d8b18-105">This article walks you through basic planning and design considerations.</span></span>

## <span data-ttu-id="d8b18-106"><a name="planning"></a>Planeamiento</span><span class="sxs-lookup"><span data-stu-id="d8b18-106"><a name="planning"></a>Planning</span></span>

### <span data-ttu-id="d8b18-107"><a name="compare"></a>Opciones de conectividad entre locales</span><span class="sxs-lookup"><span data-stu-id="d8b18-107"><a name="compare"></a>Cross-premises connectivity options</span></span>

<span data-ttu-id="d8b18-108">Si desea que tooconnect local de forma segura sitios tooa de red virtual, por lo que tiene tres toodo de maneras diferentes: sitio a sitio, punto a sitio y ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d8b18-108">If you want tooconnect your on-premises sites securely tooa virtual network, you have three different ways toodo so: Site-to-Site, Point-to-Site, and ExpressRoute.</span></span> <span data-ttu-id="d8b18-109">Comparar conexiones entre entornos diferentes de Hola que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="d8b18-109">Compare hello different cross-premises connections that are available.</span></span> <span data-ttu-id="d8b18-110">opción de Hola que elija puede depender de diversas consideraciones, como:</span><span class="sxs-lookup"><span data-stu-id="d8b18-110">hello option you choose can depend on various considerations, such as:</span></span>

* <span data-ttu-id="d8b18-111">¿Qué tipo de rendimiento requiere la solución?</span><span class="sxs-lookup"><span data-stu-id="d8b18-111">What kind of throughput does your solution require?</span></span>
* <span data-ttu-id="d8b18-112">¿Desea toocommunicate sobre Hola red pública de Internet a través de VPN segura, o a través de una conexión privada?</span><span class="sxs-lookup"><span data-stu-id="d8b18-112">Do you want toocommunicate over hello public Internet via secure VPN, or over a private connection?</span></span>
* <span data-ttu-id="d8b18-113">¿Tiene un toouse disponible de dirección IP pública?</span><span class="sxs-lookup"><span data-stu-id="d8b18-113">Do you have a public IP address available toouse?</span></span>
* <span data-ttu-id="d8b18-114">¿Piensa toouse un dispositivo VPN?</span><span class="sxs-lookup"><span data-stu-id="d8b18-114">Are you planning toouse a VPN device?</span></span> <span data-ttu-id="d8b18-115">Si es así, ¿es compatible?</span><span class="sxs-lookup"><span data-stu-id="d8b18-115">If so, is it compatible?</span></span>
* <span data-ttu-id="d8b18-116">¿Va a conectar solo algunos equipos o desea establecer una conexión persistente para su sitio?</span><span class="sxs-lookup"><span data-stu-id="d8b18-116">Are you connecting just a few computers, or do you want a persistent connection for your site?</span></span>
* <span data-ttu-id="d8b18-117">¿Qué tipo de puerta de enlace VPN es necesario para la solución de hello desea toocreate?</span><span class="sxs-lookup"><span data-stu-id="d8b18-117">What type of VPN gateway is required for hello solution you want toocreate?</span></span>
* <span data-ttu-id="d8b18-118">¿Qué SKU de puerta de enlace se debe usar?</span><span class="sxs-lookup"><span data-stu-id="d8b18-118">Which gateway SKU should you use?</span></span>

### <span data-ttu-id="d8b18-119"><a name="planningtable"></a>Tabla de planeación</span><span class="sxs-lookup"><span data-stu-id="d8b18-119"><a name="planningtable"></a>Planning table</span></span>

<span data-ttu-id="d8b18-120">Hello en la tabla siguiente puede ayudarle a decidir la mejor opción de conectividad hello para la solución.</span><span class="sxs-lookup"><span data-stu-id="d8b18-120">hello following table can help you decide hello best connectivity option for your solution.</span></span>

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <span data-ttu-id="d8b18-121"><a name="gwsku"></a>SKU de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="d8b18-121"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <span data-ttu-id="d8b18-122"><a name="wf"></a>Flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="d8b18-122"><a name="wf"></a>Workflow</span></span>

<span data-ttu-id="d8b18-123">Hello siguiente lista se describen Hola flujo de trabajo común para la conectividad de la nube:</span><span class="sxs-lookup"><span data-stu-id="d8b18-123">hello following list outlines hello common workflow for cloud connectivity:</span></span>

1. <span data-ttu-id="d8b18-124">Diseño y plan de que espacios de la dirección de Hola de topología y la lista de conectividad para todas las redes desean tooconnect.</span><span class="sxs-lookup"><span data-stu-id="d8b18-124">Design and plan your connectivity topology and list hello address spaces for all networks you want tooconnect.</span></span>
2. <span data-ttu-id="d8b18-125">Cree una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="d8b18-125">Create an Azure virtual network.</span></span> 
3. <span data-ttu-id="d8b18-126">Crear una puerta de enlace VPN para la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8b18-126">Create a VPN gateway for hello virtual network.</span></span>
4. <span data-ttu-id="d8b18-127">Crear y configurar las redes de tooon locales de las conexiones u otras redes virtuales (según sea necesario).</span><span class="sxs-lookup"><span data-stu-id="d8b18-127">Create and configure connections tooon-premises networks or other virtual networks (as needed).</span></span>
5. <span data-ttu-id="d8b18-128">Cree y configure una conexión de punto a sitio para su puerta de enlace de Azure VPN Gateway (según sea necesario).</span><span class="sxs-lookup"><span data-stu-id="d8b18-128">Create and configure a Point-to-Site connection for your Azure VPN gateway (as needed).</span></span>

## <span data-ttu-id="d8b18-129"><a name="design"></a>Diseño</span><span class="sxs-lookup"><span data-stu-id="d8b18-129"><a name="design"></a>Design</span></span>
### <span data-ttu-id="d8b18-130"><a name="topologies"></a>Topologías de conexión</span><span class="sxs-lookup"><span data-stu-id="d8b18-130"><a name="topologies"></a>Connection topologies</span></span>

<span data-ttu-id="d8b18-131">Comience por mirar diagramas Hola Hola [acerca de la puerta de enlace VPN](vpn-gateway-about-vpngateways.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="d8b18-131">Start by looking at hello diagrams in hello [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span> <span data-ttu-id="d8b18-132">artículo de Hello contiene diagramas básicos, modelos de implementación de Hola para cada topología y las herramientas de implementación disponibles hello toodeploy puede usar la configuración.</span><span class="sxs-lookup"><span data-stu-id="d8b18-132">hello article contains basic diagrams, hello deployment models for each topology, and hello available deployment tools you can use toodeploy your configuration.</span></span>

### <span data-ttu-id="d8b18-133"><a name="designbasics"></a>Conceptos básicos del diseño</span><span class="sxs-lookup"><span data-stu-id="d8b18-133"><a name="designbasics"></a>Design basics</span></span>

<span data-ttu-id="d8b18-134">Hola siguientes secciones describe conceptos básicos de puerta de enlace VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8b18-134">hello following sections discuss hello VPN gateway basics.</span></span> 

#### <span data-ttu-id="d8b18-135"><a name="servicelimits"></a>Límites de servicios de red</span><span class="sxs-lookup"><span data-stu-id="d8b18-135"><a name="servicelimits"></a>Networking services limits</span></span>

<span data-ttu-id="d8b18-136">Desplácese por hello tablas tooview [límites de servicios de red](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="d8b18-136">Scroll through hello tables tooview [networking services limits](../azure-subscription-service-limits.md#networking-limits).</span></span> <span data-ttu-id="d8b18-137">límites de Hello mencionados pueden afectar a su diseño.</span><span class="sxs-lookup"><span data-stu-id="d8b18-137">hello limits listed may impact your design.</span></span>

#### <span data-ttu-id="d8b18-138"><a name="subnets"></a>Acerca de las subredes</span><span class="sxs-lookup"><span data-stu-id="d8b18-138"><a name="subnets"></a>About subnets</span></span>

<span data-ttu-id="d8b18-139">Al crear conexiones, debe tener en cuenta los intervalos de subred.</span><span class="sxs-lookup"><span data-stu-id="d8b18-139">When you are creating connections, you must consider your subnet ranges.</span></span> <span data-ttu-id="d8b18-140">Los intervalos de direcciones de subred no se pueden superponer.</span><span class="sxs-lookup"><span data-stu-id="d8b18-140">You cannot have overlapping subnet address ranges.</span></span> <span data-ttu-id="d8b18-141">Una subred que se superpone es cuando una ubicación local o de red virtual contiene hello contiene el mismo espacio de direcciones que Hola a otra ubicación.</span><span class="sxs-lookup"><span data-stu-id="d8b18-141">An overlapping subnet is when one virtual network or on-premises location contains hello same address space that hello other location contains.</span></span> <span data-ttu-id="d8b18-142">Esto significa que necesita a los ingenieros de red para su toocarve de redes de instalaciones locales fuera de un intervalo para toouse para la IP de Azure direccionamiento espacio/subredes.</span><span class="sxs-lookup"><span data-stu-id="d8b18-142">This means that you need your network engineers for your local on-premises networks toocarve out a range for you toouse for your Azure IP addressing space/subnets.</span></span> <span data-ttu-id="d8b18-143">Necesita espacio de direcciones que no se está utilizando en red de hello en instalaciones locales.</span><span class="sxs-lookup"><span data-stu-id="d8b18-143">You need address space that is not being used on hello local on-premises network.</span></span>

<span data-ttu-id="d8b18-144">También es importante evitar las subredes superpuestas cuando se trabaja con conexiones entre redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="d8b18-144">Avoiding overlapping subnets is also important when you are working with VNet-to-VNet connections.</span></span> <span data-ttu-id="d8b18-145">Si se superponen las subredes y una dirección IP existe en el envío de Hola y redes virtuales de destino, las conexiones de red virtual a red virtual producirá un error.</span><span class="sxs-lookup"><span data-stu-id="d8b18-145">If your subnets overlap and an IP address exists in both hello sending and destination VNets, VNet-to-VNet connections fail.</span></span> <span data-ttu-id="d8b18-146">Azure no puede enrutar Hola datos toohello otra VNet como dirección de destino de hello forma parte de hello envío de red virtual.</span><span class="sxs-lookup"><span data-stu-id="d8b18-146">Azure can't route hello data toohello other VNet because hello destination address is part of hello sending VNet.</span></span>

<span data-ttu-id="d8b18-147">Las puertas de enlace de VPN requieren una subred específica llamada subred de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="d8b18-147">VPN Gateways require a specific subnet called a gateway subnet.</span></span> <span data-ttu-id="d8b18-148">Todas las subredes de puerta de enlace deben denominarse GatewaySubnet toowork correctamente.</span><span class="sxs-lookup"><span data-stu-id="d8b18-148">All gateway subnets must be named GatewaySubnet toowork properly.</span></span> <span data-ttu-id="d8b18-149">Asegúrese de no tooname la subred de puerta de enlace de otro nombre y no implementar máquinas virtuales o la subred de puerta de enlace de toohello nada.</span><span class="sxs-lookup"><span data-stu-id="d8b18-149">Be sure not tooname your gateway subnet a different name, and don't deploy VMs or anything else toohello gateway subnet.</span></span> <span data-ttu-id="d8b18-150">Consulte [Subredes de puerta de enlace](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span><span class="sxs-lookup"><span data-stu-id="d8b18-150">See [Gateway Subnets](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span></span>

#### <span data-ttu-id="d8b18-151"><a name="local"></a>Acerca de las puertas de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="d8b18-151"><a name="local"></a>About local network gateways</span></span>

<span data-ttu-id="d8b18-152">puerta de enlace de red local de Hello suele hacer referencia a ubicación de tooyour local.</span><span class="sxs-lookup"><span data-stu-id="d8b18-152">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="d8b18-153">En el modelo de implementación clásica de hello, puerta de enlace de red local de hello es tooas que se hace referencia un sitio de red Local.</span><span class="sxs-lookup"><span data-stu-id="d8b18-153">In hello classic deployment model, hello local network gateway is referred tooas a Local Network Site.</span></span> <span data-ttu-id="d8b18-154">Cuando se configura una puerta de enlace de red local, asígnele un nombre, especifique la dirección IP pública de hello de dispositivo VPN de hello local y especificar los prefijos de dirección de Hola que estén en la ubicación local de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8b18-154">When you configure a local network gateway, you give it a name, specify hello public IP address of hello on-premises VPN device, and specify hello address prefixes that are in hello on-premises location.</span></span> <span data-ttu-id="d8b18-155">Azure examina prefijos de dirección de destino de hello para el tráfico de red, consulta configuración Hola que ha especificado para la puerta de enlace de red local de Hola y enruta paquetes según corresponda.</span><span class="sxs-lookup"><span data-stu-id="d8b18-155">Azure looks at hello destination address prefixes for network traffic, consults hello configuration that you have specified for hello local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="d8b18-156">Puede modificar los prefijos de direcciones de hello según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d8b18-156">You can modify hello address prefixes as needed.</span></span> <span data-ttu-id="d8b18-157">Para más información, consulte [Puertas de enlace de red](vpn-gateway-about-vpn-gateway-settings.md#lng).</span><span class="sxs-lookup"><span data-stu-id="d8b18-157">For more information, see [Local network gateways](vpn-gateway-about-vpn-gateway-settings.md#lng).</span></span>

#### <span data-ttu-id="d8b18-158"><a name="gwtype"></a>Acerca de los tipos de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="d8b18-158"><a name="gwtype"></a>About gateway types</span></span>

<span data-ttu-id="d8b18-159">Seleccionar tipo de puerta de enlace correcto de hello para la topología es fundamental.</span><span class="sxs-lookup"><span data-stu-id="d8b18-159">Selecting hello correct gateway type for your topology is critical.</span></span> <span data-ttu-id="d8b18-160">Si selecciona un tipo incorrecto hello, la puerta de enlace no funcionará correctamente.</span><span class="sxs-lookup"><span data-stu-id="d8b18-160">If you select hello wrong type, your gateway won't work properly.</span></span> <span data-ttu-id="d8b18-161">tipo de puerta de enlace de Hello especifica cómo se conecta Hola puerta de enlace y un valor de configuración necesarios para el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8b18-161">hello gateway type specifies how hello gateway itself connects and is a required configuration setting for hello Resource Manager deployment model.</span></span>

<span data-ttu-id="d8b18-162">tipos de puerta de enlace de Hello son:</span><span class="sxs-lookup"><span data-stu-id="d8b18-162">hello gateway types are:</span></span>

* <span data-ttu-id="d8b18-163">VPN</span><span class="sxs-lookup"><span data-stu-id="d8b18-163">Vpn</span></span>
* <span data-ttu-id="d8b18-164">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="d8b18-164">ExpressRoute</span></span>

#### <span data-ttu-id="d8b18-165"><a name="connectiontype"></a>Acerca de los tipos de conexión</span><span class="sxs-lookup"><span data-stu-id="d8b18-165"><a name="connectiontype"></a>About connection types</span></span>

<span data-ttu-id="d8b18-166">Cada configuración requiere un tipo de conexión específico.</span><span class="sxs-lookup"><span data-stu-id="d8b18-166">Each configuration requires a specific connection type.</span></span> <span data-ttu-id="d8b18-167">tipos de conexión de Hello son:</span><span class="sxs-lookup"><span data-stu-id="d8b18-167">hello connection types are:</span></span>

* <span data-ttu-id="d8b18-168">IPsec</span><span class="sxs-lookup"><span data-stu-id="d8b18-168">IPsec</span></span>
* <span data-ttu-id="d8b18-169">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="d8b18-169">Vnet2Vnet</span></span>
* <span data-ttu-id="d8b18-170">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="d8b18-170">ExpressRoute</span></span>
* <span data-ttu-id="d8b18-171">VPNClient</span><span class="sxs-lookup"><span data-stu-id="d8b18-171">VPNClient</span></span>

#### <span data-ttu-id="d8b18-172"><a name="vpntype"></a>Acerca de los tipos de VPN</span><span class="sxs-lookup"><span data-stu-id="d8b18-172"><a name="vpntype"></a>About VPN types</span></span>

<span data-ttu-id="d8b18-173">Cada configuración requiere un tipo específico de VPN específico.</span><span class="sxs-lookup"><span data-stu-id="d8b18-173">Each configuration requires a specific VPN type.</span></span> <span data-ttu-id="d8b18-174">Si combina dos configuraciones, como la creación de una conexión de sitio a sitio y un toohello de conexión de punto a sitio misma red virtual, debe usar un tipo VPN que cumple los requisitos de conexión.</span><span class="sxs-lookup"><span data-stu-id="d8b18-174">If you are combining two configurations, such as creating a Site-to-Site connection and a Point-to-Site connection toohello same VNet, you must use a VPN type that satisfies both connection requirements.</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="d8b18-175">Hello en las tablas siguientes muestran Hola VPN tipo tal y como se asigna la configuración de conexión de tooeach.</span><span class="sxs-lookup"><span data-stu-id="d8b18-175">hello following tables show hello VPN type as it maps tooeach connection configuration.</span></span> <span data-ttu-id="d8b18-176">Asegúrese de hello seguro de tipo VPN para la configuración de Hola de coincidencias de puerta de enlace que desea toocreate.</span><span class="sxs-lookup"><span data-stu-id="d8b18-176">Make sure hello VPN type for your gateway matches hello configuration that you want toocreate.</span></span> 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <span data-ttu-id="d8b18-177"><a name="devices"></a>Dispositivos VPN para conexiones de sitio a sitio</span><span class="sxs-lookup"><span data-stu-id="d8b18-177"><a name="devices"></a>VPN devices for Site-to-Site connections</span></span>

<span data-ttu-id="d8b18-178">conexión de tooconfigure un sitio a sitio, independientemente del modelo de implementación, debe Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d8b18-178">tooconfigure a Site-to-Site connection, regardless of deployment model, you need hello following items:</span></span>

* <span data-ttu-id="d8b18-179">Un dispositivo VPN compatible con Azure VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="d8b18-179">A VPN device that is compatible with Azure VPN gateways</span></span>
* <span data-ttu-id="d8b18-180">Una dirección IP IPv4 pública que no se encuentre detrás de un NAT.</span><span class="sxs-lookup"><span data-stu-id="d8b18-180">A public-facing IPv4 IP address that is not behind a NAT</span></span>

<span data-ttu-id="d8b18-181">Necesita experiencia toohave configurar el dispositivo VPN, o bien pedirle a alguien que puede configurar automáticamente dispositivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8b18-181">You need toohave experience configuring your VPN device, or have someone that can configure hello device for you.</span></span>

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <span data-ttu-id="d8b18-182"><a name="forcedtunnel"></a>Considerar el enrutamiento de túnel forzado</span><span class="sxs-lookup"><span data-stu-id="d8b18-182"><a name="forcedtunnel"></a>Consider forced tunnel routing</span></span>

<span data-ttu-id="d8b18-183">La tunelización forzada se puede configurar en la mayoría de las configuraciones.</span><span class="sxs-lookup"><span data-stu-id="d8b18-183">For most configurations, you can configure forced tunneling.</span></span> <span data-ttu-id="d8b18-184">Forzada permite redirigir o "forzar" todos los vinculado a Internet tráfico tooyour back-ubicación de local a través de un túnel VPN de sitio a sitio para inspección y auditoría de túnel.</span><span class="sxs-lookup"><span data-stu-id="d8b18-184">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="d8b18-185">Se trata de un requisito de seguridad crítico en la mayoría de las directivas de las empresas de TI.</span><span class="sxs-lookup"><span data-stu-id="d8b18-185">This is a critical security requirement for most enterprise IT policies.</span></span> 

<span data-ttu-id="d8b18-186">Sin la tunelización forzada, tráfico de Internet desde las máquinas virtuales en Azure atravesará siempre desde la infraestructura de red de Azure directamente out toohello Internet, sin Hola opción tooallow se tooinspect o auditoría tráfico Hola.</span><span class="sxs-lookup"><span data-stu-id="d8b18-186">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="d8b18-187">Acceso de Internet no autorizado puede provocar potencialmente la divulgación de tooinformation u otros tipos de infracciones de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d8b18-187">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

<span data-ttu-id="d8b18-188">Ambos modelos de implementación permiten configurar una conexión de tunelización forzada mediante distintas herramientas.</span><span class="sxs-lookup"><span data-stu-id="d8b18-188">A forced tunneling connection can be configured in both deployment models and by using different tools.</span></span> <span data-ttu-id="d8b18-189">Para obtener más información, consulte [Configuración de la tunelización forzada](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="d8b18-189">For more information, see [Configure forced tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>

<span data-ttu-id="d8b18-190">**Diagrama de tunelización forzada**</span><span class="sxs-lookup"><span data-stu-id="d8b18-190">**Forced tunneling diagram**</span></span>

![Diagrama de tunelización forzada de Azure VPN Gateway](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a><span data-ttu-id="d8b18-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d8b18-192">Next steps</span></span>

<span data-ttu-id="d8b18-193">Vea hello [preguntas más frecuentes de puerta de enlace de VPN](vpn-gateway-vpn-faq.md) y [acerca de la puerta de enlace VPN](vpn-gateway-about-vpngateways.md) artículos para toohelp de información más con el diseño.</span><span class="sxs-lookup"><span data-stu-id="d8b18-193">See hello [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) and [About VPN Gateway](vpn-gateway-about-vpngateways.md) articles for more information toohelp you with your design.</span></span>

<span data-ttu-id="d8b18-194">Para obtener más información acerca de la configuración de puerta de enlace específica, consulte [Acerca de la configuración de VPN Gateway](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="d8b18-194">For more information about specific gateway settings, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>