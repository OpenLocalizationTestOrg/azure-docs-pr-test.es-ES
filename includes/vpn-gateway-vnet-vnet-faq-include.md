<span data-ttu-id="713d7-101">Las preguntas más frecuentes sobre red virtual a red virtual se aplican a las conexiones VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="713d7-101">The VNet-to-VNet FAQ applies to VPN Gateway connections.</span></span> <span data-ttu-id="713d7-102">Si busca información sobre el emparejamiento de redes virtuales, consulte [Emparejamiento de redes virtuales](../articles/virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="713d7-102">If you are looking for VNet Peering, see [Virtual Network Peering](../articles/virtual-network/virtual-network-peering-overview.md)</span></span>

### <a name="does-azure-charge-for-traffic-between-vnets"></a><span data-ttu-id="713d7-103">¿Cobra Azure por el tráfico entre redes virtuales?</span><span class="sxs-lookup"><span data-stu-id="713d7-103">Does Azure charge for traffic between VNets?</span></span>

<span data-ttu-id="713d7-104">El tráfico entre redes virtuales dentro de la misma región es gratuito en ambas direcciones cuando se usa una conexión de puerta de enlace de VPN.</span><span class="sxs-lookup"><span data-stu-id="713d7-104">VNet-to-VNet traffic within the same region is free for both directions when using a VPN gateway connection.</span></span> <span data-ttu-id="713d7-105">El tráfico de salida de red virtual a red virtual entre regiones se cobra según las tarifas de transferencia de datos de salida entre redes virtuales en función de las regiones de origen.</span><span class="sxs-lookup"><span data-stu-id="713d7-105">Cross region VNet-to-VNet egress traffic is charged with the outbound inter-VNet data transfer rates based on the source regions.</span></span> <span data-ttu-id="713d7-106">Para más información, consulte la [página de precios de VPN Gateway](https://azure.microsoft.com/pricing/details/vpn-gateway/).</span><span class="sxs-lookup"><span data-stu-id="713d7-106">Refer to the [VPN Gateway pricing page](https://azure.microsoft.com/pricing/details/vpn-gateway/) for details.</span></span> <span data-ttu-id="713d7-107">Si va a conectar sus redes virtuales mediante emparejamiento de VNet en lugar de VPN Gateway, consulte la [página de precios de Virtual Network](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="713d7-107">If you are connecting your VNets using VNet Peering, rather than VPN Gateway, see the [Virtual Network pricing page](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>

### <a name="does-vnet-to-vnet-traffic-travel-across-the-internet"></a><span data-ttu-id="713d7-108">¿Viaja el tráfico entre dos redes virtuales a través de Internet?</span><span class="sxs-lookup"><span data-stu-id="713d7-108">Does VNet-to-VNet traffic travel across the Internet?</span></span>

<span data-ttu-id="713d7-109">No.</span><span class="sxs-lookup"><span data-stu-id="713d7-109">No.</span></span> <span data-ttu-id="713d7-110">Viaja por la red troncal de Microsoft Azure, no por Internet.</span><span class="sxs-lookup"><span data-stu-id="713d7-110">VNet-to-VNet traffic travels across the Microsoft Azure backbone, not the Internet.</span></span>

### <a name="is-vnet-to-vnet-traffic-secure"></a><span data-ttu-id="713d7-111">¿Es seguro el tráfico entre dos redes virtuales?</span><span class="sxs-lookup"><span data-stu-id="713d7-111">Is VNet-to-VNet traffic secure?</span></span>

<span data-ttu-id="713d7-112">Sí, se protege mediante cifrado IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="713d7-112">Yes, it is protected by IPsec/IKE encryption.</span></span>

### <a name="do-i-need-a-vpn-device-to-connect-vnets-together"></a><span data-ttu-id="713d7-113">¿Necesito un dispositivo VPN para conectar redes virtuales?</span><span class="sxs-lookup"><span data-stu-id="713d7-113">Do I need a VPN device to connect VNets together?</span></span>

<span data-ttu-id="713d7-114">No.</span><span class="sxs-lookup"><span data-stu-id="713d7-114">No.</span></span> <span data-ttu-id="713d7-115">La conexión simultánea de varias redes virtuales de Azure no requiere dispositivos VPN, a menos que sea necesaria la conectividad entre locales.</span><span class="sxs-lookup"><span data-stu-id="713d7-115">Connecting multiple Azure virtual networks together doesn't require a VPN device unless cross-premises connectivity is required.</span></span>

### <a name="do-my-vnets-need-to-be-in-the-same-region"></a><span data-ttu-id="713d7-116">¿Deben estar mis redes virtuales en la misma región?</span><span class="sxs-lookup"><span data-stu-id="713d7-116">Do my VNets need to be in the same region?</span></span>

<span data-ttu-id="713d7-117">No.</span><span class="sxs-lookup"><span data-stu-id="713d7-117">No.</span></span> <span data-ttu-id="713d7-118">Las redes virtuales pueden estar en la misma región de Azure o en regiones distintas (ubicaciones).</span><span class="sxs-lookup"><span data-stu-id="713d7-118">The virtual networks can be in the same or different Azure regions (locations).</span></span>

### <a name="if-the-vnets-are-not-in-the-same-subscription-do-the-subscriptions-need-to-be-associated-with-the-same-ad-tenant"></a><span data-ttu-id="713d7-119">Si las redes virtuales no están en la misma suscripción, ¿las suscripciones tienen que estar asociadas con el mismo inquilino de AD?</span><span class="sxs-lookup"><span data-stu-id="713d7-119">If the VNets are not in the same subscription, do the subscriptions need to be associated with the same AD tenant?</span></span>

<span data-ttu-id="713d7-120">Nº</span><span class="sxs-lookup"><span data-stu-id="713d7-120">No.</span></span>

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a><span data-ttu-id="713d7-121">¿Puedo usar las conexiones entre dos redes virtuales con conexiones multisitio?</span><span class="sxs-lookup"><span data-stu-id="713d7-121">Can I use VNet-to-VNet along with multi-site connections?</span></span>

<span data-ttu-id="713d7-122">Sí.</span><span class="sxs-lookup"><span data-stu-id="713d7-122">Yes.</span></span> <span data-ttu-id="713d7-123">La conectividad de red virtual se puede usar de forma simultánea con VPN de varios sitios.</span><span class="sxs-lookup"><span data-stu-id="713d7-123">Virtual network connectivity can be used simultaneously with multi-site VPNs.</span></span>

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a><span data-ttu-id="713d7-124">¿A cuántos sitios locales y redes virtuales se puede conectar una red virtual?</span><span class="sxs-lookup"><span data-stu-id="713d7-124">How many on-premises sites and virtual networks can one virtual network connect to?</span></span>

<span data-ttu-id="713d7-125">Consulte la tabla [Requisitos de la puerta de enlace](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="713d7-125">See [Gateway requirements](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements) table.</span></span>

### <a name="can-i-use-vnet-to-vnet-to-connect-vms-or-cloud-services-outside-of-a-vnet"></a><span data-ttu-id="713d7-126">¿Puedo usar la conexión entre dos redes virtuales para conectar máquinas virtuales o servicios en la nube fuera de una red virtual?</span><span class="sxs-lookup"><span data-stu-id="713d7-126">Can I use VNet-to-VNet to connect VMs or cloud services outside of a VNet?</span></span>

<span data-ttu-id="713d7-127">No.</span><span class="sxs-lookup"><span data-stu-id="713d7-127">No.</span></span> <span data-ttu-id="713d7-128">VNet a VNet admite la conexión de redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="713d7-128">VNet-to-VNet supports connecting virtual networks.</span></span> <span data-ttu-id="713d7-129">No admite la conexión de máquinas virtuales ni servicios en la nube que no estén en una red virtual.</span><span class="sxs-lookup"><span data-stu-id="713d7-129">It does not support connecting virtual machines or cloud services that are not in a virtual network.</span></span>

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a><span data-ttu-id="713d7-130">¿Abarca redes virtuales un servicio en la nube o un punto de conexión de equilibrio de carga?</span><span class="sxs-lookup"><span data-stu-id="713d7-130">Can a cloud service or a load balancing endpoint span VNets?</span></span>

<span data-ttu-id="713d7-131">No.</span><span class="sxs-lookup"><span data-stu-id="713d7-131">No.</span></span> <span data-ttu-id="713d7-132">Un servicio en la nube o un punto de conexión de equilibrio de carga no puede abarcar varias redes virtuales, aunque estas estén conectadas entre sí.</span><span class="sxs-lookup"><span data-stu-id="713d7-132">A cloud service or a load balancing endpoint can't span across virtual networks, even if they are connected together.</span></span>

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a><span data-ttu-id="713d7-133">¿Puedo usar un tipo de VPN PolicyBased para las conexiones entre dos redes virtuales o multisitio?</span><span class="sxs-lookup"><span data-stu-id="713d7-133">Can I used a PolicyBased VPN type for VNet-to-VNet or Multi-Site connections?</span></span>

<span data-ttu-id="713d7-134">No.</span><span class="sxs-lookup"><span data-stu-id="713d7-134">No.</span></span> <span data-ttu-id="713d7-135">Las conexiones entre dos redes virtuales y multisitio requieren puertas de enlace de VPN de Azure con tipos de VPN RouteBased (antes denominado enrutamiento dinámico).</span><span class="sxs-lookup"><span data-stu-id="713d7-135">VNet-to-VNet and Multi-Site connections require Azure VPN gateways with RouteBased (previously called Dynamic Routing) VPN types.</span></span>

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-to-another-vnet-with-a-policybased-vpn-type"></a><span data-ttu-id="713d7-136">¿Puedo conectar una red virtual con un tipo de VPN RouteBased a otra red virtual con un tipo de VPN PolicyBased?</span><span class="sxs-lookup"><span data-stu-id="713d7-136">Can I connect a VNet with a RouteBased VPN Type to another VNet with a PolicyBased VPN type?</span></span>

<span data-ttu-id="713d7-137">No, ambas redes virtuales TIENEN QUE usar VPN basadas en enrutamiento (antes denominado enrutamiento dinámico).</span><span class="sxs-lookup"><span data-stu-id="713d7-137">No, both virtual networks MUST be using route-based (previously called Dynamic Routing) VPNs.</span></span>

### <a name="do-vpn-tunnels-share-bandwidth"></a><span data-ttu-id="713d7-138">¿Comparten ancho de banda los túneles de VPN?</span><span class="sxs-lookup"><span data-stu-id="713d7-138">Do VPN tunnels share bandwidth?</span></span>

<span data-ttu-id="713d7-139">Sí.</span><span class="sxs-lookup"><span data-stu-id="713d7-139">Yes.</span></span> <span data-ttu-id="713d7-140">Todos los túneles de VPN de la red virtual comparten el ancho de banda disponible en la puerta de enlace de VPN de Azure y el mismo SLA de tiempo de actividad de puerta de enlace de VPN en Azure.</span><span class="sxs-lookup"><span data-stu-id="713d7-140">All VPN tunnels of the virtual network share the available bandwidth on the Azure VPN gateway and the same VPN gateway uptime SLA in Azure.</span></span>

### <a name="are-redundant-tunnels-supported"></a><span data-ttu-id="713d7-141">¿Se admiten túneles redundantes?</span><span class="sxs-lookup"><span data-stu-id="713d7-141">Are redundant tunnels supported?</span></span>

<span data-ttu-id="713d7-142">Los túneles redundantes entre dos redes virtuales se admiten cuando la puerta de enlace de una red virtual está configurada como activa-activa.</span><span class="sxs-lookup"><span data-stu-id="713d7-142">Redundant tunnels between a pair of virtual networks are supported when one virtual network gateway is configured as active-active.</span></span>

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a><span data-ttu-id="713d7-143">¿Puedo tener espacios de direcciones superpuestos para configuraciones de red virtual a red virtual?</span><span class="sxs-lookup"><span data-stu-id="713d7-143">Can I have overlapping address spaces for VNet-to-VNet configurations?</span></span>

<span data-ttu-id="713d7-144">No.</span><span class="sxs-lookup"><span data-stu-id="713d7-144">No.</span></span> <span data-ttu-id="713d7-145">No puede tener intervalos de direcciones de IP superpuestos.</span><span class="sxs-lookup"><span data-stu-id="713d7-145">You can't have overlapping IP address ranges.</span></span>

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a><span data-ttu-id="713d7-146">¿Puede haber espacios de direcciones superpuestos entre las redes virtuales conectadas y los sitios locales?</span><span class="sxs-lookup"><span data-stu-id="713d7-146">Can there be overlapping address spaces among connected virtual networks and on-premises local sites?</span></span>

<span data-ttu-id="713d7-147">No.</span><span class="sxs-lookup"><span data-stu-id="713d7-147">No.</span></span> <span data-ttu-id="713d7-148">No puede tener intervalos de direcciones de IP superpuestos.</span><span class="sxs-lookup"><span data-stu-id="713d7-148">You can't have overlapping IP address ranges.</span></span>



