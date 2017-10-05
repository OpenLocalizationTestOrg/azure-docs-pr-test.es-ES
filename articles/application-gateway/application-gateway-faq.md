---
title: "Preguntas más frecuentes sobre Azure Application Gateway | Microsoft Docs"
description: "Esta página proporciona respuestas a las preguntas más frecuentes acerca de Azure Application Gateway"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 4e6244d92f41e0aa5c8a70db0db2881036984247
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a><span data-ttu-id="cf7e4-103">Preguntas más frecuentes sobre Application Gateway</span><span class="sxs-lookup"><span data-stu-id="cf7e4-103">Frequently asked questions for Application Gateway</span></span>

## <a name="general"></a><span data-ttu-id="cf7e4-104">General</span><span class="sxs-lookup"><span data-stu-id="cf7e4-104">General</span></span>

<span data-ttu-id="cf7e4-105">**P. ¿Qué es Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-105">**Q. What is Application Gateway?**</span></span>

<span data-ttu-id="cf7e4-106">Azure Application Gateway es un controlador de entrega de aplicaciones (ADC) como servicio que ofrece diversas funcionalidades de equilibrio de carga de nivel 7 para sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-106">Azure Application Gateway is an Application Delivery Controller (ADC) as a service, offering various layer 7 load balancing capabilities for your applications.</span></span> <span data-ttu-id="cf7e4-107">Ofrece un servicio altamente disponible y escalable que está completamente administrado por Azure.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-107">It offers highly available and scalable service, which is fully managed by Azure.</span></span>

<span data-ttu-id="cf7e4-108">**P. ¿Qué características admite Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-108">**Q. What features does Application Gateway support?**</span></span>

<span data-ttu-id="cf7e4-109">Application Gateway admite la descarga de SSL y SSL de un extremo a otro, Firewall de aplicaciones web, afinidad de sesión basada en cookies, enrutamiento basado en ruta de dirección URL, alojamiento de varios sitios y muchas otras más.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-109">Application Gateway supports SSL offloading and end to end SSL, Web Application Firewall, cookie-based session affinity, url path-based routing, multi site hosting, and others.</span></span> <span data-ttu-id="cf7e4-110">Para obtener una lista completa de las características admitidas, visite [Introducción a Application Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cf7e4-110">For a full list of supported features, visit [Introduction to Application Gateway](application-gateway-introduction.md)</span></span>

<span data-ttu-id="cf7e4-111">**P. ¿Cuál es la diferencia entre Application Gateway y Azure Load Balancer?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-111">**Q. What is the difference between Application Gateway and Azure Load Balancer?**</span></span>

<span data-ttu-id="cf7e4-112">Application Gateway es un equilibrador de carga de nivel 7, lo que significa que funciona solo tráfico web (HTTP/HTTPS/WebSocket).</span><span class="sxs-lookup"><span data-stu-id="cf7e4-112">Application Gateway is a layer 7 load balancer, which means it works with web traffic only (HTTP/HTTPS/WebSocket).</span></span> <span data-ttu-id="cf7e4-113">Admite funcionalidades como la terminación SSL, la afinidad de sesión basada en cookies y la distribución round robin para el tráfico de equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-113">It supports capabilities such as SSL termination, cookie-based session affinity, and round robin for load balancing traffic.</span></span> <span data-ttu-id="cf7e4-114">Load Balancer equilibra la carga de tráfico en el nivel 4 (TCP/UDP).</span><span class="sxs-lookup"><span data-stu-id="cf7e4-114">Load Balancer, load balances traffic at layer 4 (TCP/UDP).</span></span>

<span data-ttu-id="cf7e4-115">**P. ¿Qué protocolos admite Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-115">**Q. What protocols does Application Gateway support?**</span></span>

<span data-ttu-id="cf7e4-116">Application Gateway admite HTTP, HTTPS y WebSocket.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-116">Application Gateway supports HTTP, HTTPS, and WebSocket.</span></span>

<span data-ttu-id="cf7e4-117">**P. ¿Qué recursos son compatibles actualmente como parte del grupo de back-end?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-117">**Q. What resources are supported today as part of backend pool?**</span></span>

<span data-ttu-id="cf7e4-118">Los grupos de back-end pueden constar de NIC, conjuntos de escalado de máquinas virtuales, direcciones IP públicas e internas, nombres de dominio completos (FQDN) y servidores back-end multiinquilino como Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-118">Backend pools can be composed of NICs, virtual machine scale sets, public IPs, internal IPs, fully qualified domain names (FQDN), and multi-tenant back-ends like Azure Web Apps.</span></span> <span data-ttu-id="cf7e4-119">Los miembros del grupo de back-end de Application Gateway no están asociados a un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-119">Application Gateway backend pool members are not tied to an availability set.</span></span> <span data-ttu-id="cf7e4-120">Los miembros de grupos de back-end pueden estar repartidos entre clústeres, centros de datos o fuera de Azure siempre y cuando dispongan de conectividad IP.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-120">Members of backend pools can be across clusters, data centers, or outside of Azure as long as they have IP connectivity.</span></span>

<span data-ttu-id="cf7e4-121">**P. ¿En qué regiones está disponible el servicio?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-121">**Q. What regions is the service available in?**</span></span>

<span data-ttu-id="cf7e4-122">Application Gateway está disponible en todas las regiones de Azure global.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-122">Application Gateway is available in all regions of global Azure.</span></span> <span data-ttu-id="cf7e4-123">También está disponible en [Azure China](https://www.azure.cn/) y [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)</span><span class="sxs-lookup"><span data-stu-id="cf7e4-123">It is also available in [Azure China](https://www.azure.cn/) and [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)</span></span>

<span data-ttu-id="cf7e4-124">**P. ¿Se trata de una implementación dedicada para mi suscripción o compartida entre los clientes?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-124">**Q. Is this a dedicated deployment for my subscription or is it shared across customers?**</span></span>

<span data-ttu-id="cf7e4-125">Application Gateway es una implementación dedicada en su red virtual.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-125">Application Gateway is a dedicated deployment in your virtual network.</span></span>

<span data-ttu-id="cf7e4-126">**P. ¿Se admite la redirección HTTP->HTTPS?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-126">**Q. Is HTTP->HTTPS redirection supported?**</span></span>

<span data-ttu-id="cf7e4-127">Se admite el redireccionamiento.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-127">Redirection is supported.</span></span> <span data-ttu-id="cf7e4-128">Visite [Introducción al redireccionamiento de Application Gateway](application-gateway-redirect-overview.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-128">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) to learn more.</span></span>

<span data-ttu-id="cf7e4-129">**P. ¿En qué orden se procesan los agentes de escucha?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-129">**Q. In what order are listeners processed?**</span></span>

<span data-ttu-id="cf7e4-130">Los agentes de escucha se procesan en el orden en que aparecen.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-130">Listeners are processed in the order they are shown.</span></span> <span data-ttu-id="cf7e4-131">Por este motivo, si un agente de escucha coincide con una solicitud entrante, se procesa primero.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-131">For that reason if a basic listener matches an incoming request it processes it first.</span></span>  <span data-ttu-id="cf7e4-132">Los agentes de escucha de varios sitios deben configurarse antes de un agente de escucha básico para asegurarse de que el tráfico se enrute al back-end correcto.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-132">Multi-site listeners should be configured before a basic listener to ensure traffic is routed to the correct back-end.</span></span>

<span data-ttu-id="cf7e4-133">**P. ¿Dónde se encuentra la dirección IP y el DNS de Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-133">**Q. Where do I find Application Gateway’s IP and DNS?**</span></span>

<span data-ttu-id="cf7e4-134">Cuando se usa una dirección IP pública como punto de conexión, esta información se puede encontrar en el recurso de la dirección IP pública o en la página de información general de Application Gateway en el portal.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-134">When using a public IP address as an endpoint, this information can be found on the public IP address resource or on the Overview page for the Application Gateway in the portal.</span></span> <span data-ttu-id="cf7e4-135">En el caso de direcciones IP internas, esta se puede encontrar en la página de información general.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-135">For internal IP addresses, this can be found on the Overview page.</span></span>

<span data-ttu-id="cf7e4-136">**P. ¿Cambia la dirección IP o el DNS durante la vigencia de Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-136">**Q. Does the IP or DNS change over the lifetime of the Application Gateway?**</span></span>

<span data-ttu-id="cf7e4-137">La dirección IP virtual puede cambiar si la puerta de enlace se detiene y la inicia otro cliente.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-137">The VIP can change if the gateway is stopped and started by the customer.</span></span> <span data-ttu-id="cf7e4-138">El DNS asociado con Application Gateway no cambia durante el ciclo de vida de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-138">The DNS associated with Application Gateway does not change over the lifecycle of the gateway.</span></span> <span data-ttu-id="cf7e4-139">Por este motivo, se recomienda utilizar un alias CNAME y hacer que señale a la dirección DNS de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-139">For this reason, it is recommended to use a CNAME alias and point it to the DNS address of the Application Gateway.</span></span>

<span data-ttu-id="cf7e4-140">**P. ¿Admite Application Gateway direcciones IP estáticas?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-140">**Q. Does Application Gateway support static IP?**</span></span>

<span data-ttu-id="cf7e4-141">No, Application Gateway no admite direcciones IP públicas estáticas, pero admite direcciones IP internas estáticas.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-141">No, Application Gateway does not support static public IP addresses, but it does support static internal IPs.</span></span>

<span data-ttu-id="cf7e4-142">**P. ¿Admite Application Gateway varias direcciones IP públicas en la puerta de enlace?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-142">**Q. Does Application Gateway support multiple public IPs on the gateway?**</span></span>

<span data-ttu-id="cf7e4-143">Solo se admite una dirección IP pública en una instancia de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-143">Only one public IP address is supported on an Application Gateway.</span></span>

<span data-ttu-id="cf7e4-144">**P. ¿Admite Application Gateway encabezados x-forwarded-for?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-144">**Q. Does Application Gateway support x-forwarded-for headers?**</span></span>

<span data-ttu-id="cf7e4-145">Sí, Application Gateway inserta encabezados x-forwarded-for, x-forwarded-proto y x-forwarded-port en la solicitud que se reenvía al back-end.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-145">Yes, Application Gateway inserts x-forwarded-for, x-forwarded-proto, and x-forwarded-port headers into the request forwarded to the backend.</span></span> <span data-ttu-id="cf7e4-146">El formato del encabezado x-forwarded-for es una lista separada por comas de IP:Port.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-146">The format for x-forwarded-for header is a comma-separated list of IP:Port.</span></span> <span data-ttu-id="cf7e4-147">Los valores válidos para x-forwarded-proto son http o https.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-147">The valid values for x-forwarded-proto are http or https.</span></span> <span data-ttu-id="cf7e4-148">X-forwarded-port especifica el puerto al que llegó la solicitud en Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-148">X-forwarded-port specifies the port at which the request reached at the Application Gateway.</span></span>

<span data-ttu-id="cf7e4-149">**P. ¿Cuánto tiempo se tarda en implementar Application Gateway? ¿Sigue funcionando Application Gateway mientras se actualiza?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-149">**Q. How long does it take to deploy an Application Gateway? Does my Application Gateway still work when being updated?**</span></span>

<span data-ttu-id="cf7e4-150">Las nuevas implementaciones de Application Gateway pueden tardar hasta 20 minutos en aprovisionarse.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-150">New Application Gateway deployments can take up to 20 minutes to provision.</span></span> <span data-ttu-id="cf7e4-151">Los cambios de tamaño y recuento de instancias no provocan interrupciones, y la puerta de enlace permanece activa durante este tiempo.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-151">Changes to instance size/count are not disruptive, and the gateway remains active during this time.</span></span>

## <a name="configuration"></a><span data-ttu-id="cf7e4-152">Configuración</span><span class="sxs-lookup"><span data-stu-id="cf7e4-152">Configuration</span></span>

<span data-ttu-id="cf7e4-153">**P. ¿Se implementa Application Gateway siempre en una red virtual?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-153">**Q. Is Application Gateway always deployed in a virtual network?**</span></span>

<span data-ttu-id="cf7e4-154">Sí, Application Gateway se implementa siempre en una red virtual.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-154">Yes, Application Gateway is always deployed in a virtual network subnet.</span></span> <span data-ttu-id="cf7e4-155">Esta subred solo puede contener instancias de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-155">This subnet can only contain Application Gateways.</span></span>

<span data-ttu-id="cf7e4-156">**P. ¿Puede Application Gateway hablar con instancias fuera de su red virtual?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-156">**Q. Can Application Gateway talk to instances outside its virtual network?**</span></span>

<span data-ttu-id="cf7e4-157">Application Gateway puede comunicarse con instancias fuera de la red virtual en la que se encuentra siempre que haya conectividad IP.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-157">Application Gateway can talk to instances outside of the virtual network that it is in as long as there is IP connectivity.</span></span> <span data-ttu-id="cf7e4-158">Si planea usar direcciones IP internas como miembros del grupo de back-end, necesitará [emparejamiento de VNET](../virtual-network/virtual-network-peering-overview.md) o [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="cf7e4-158">If you plan to use internal IPs as backend pool members, then it requires [VNET Peering](../virtual-network/virtual-network-peering-overview.md) or [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>

<span data-ttu-id="cf7e4-159">**P. ¿Puedo implementar algo más en la subred en la que está Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-159">**Q. Can I deploy anything else in the Application Gateway subnet?**</span></span>

<span data-ttu-id="cf7e4-160">No, pero se pueden implementar otras puertas de enlace de aplicación en la subred.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-160">No, but you can deploy other application gateways in the subnet.</span></span>

<span data-ttu-id="cf7e4-161">**P. ¿Se admiten grupos de seguridad de red en la subred en la que está Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-161">**Q. Are Network Security Groups supported on the Application Gateway subnet?**</span></span>

<span data-ttu-id="cf7e4-162">Se admiten grupos de seguridad de red en la subred de Application Gateway con las restricciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="cf7e4-162">Network Security Groups are supported on the Application Gateway subnet with the following restrictions:</span></span>

* <span data-ttu-id="cf7e4-163">Se deben colocar excepciones para el tráfico entrante en los puertos 65503-65534 para que el estado del back-end funcione correctamente.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-163">Exceptions must be put in for incoming traffic on ports 65503-65534 for backend health to work correctly.</span></span>

* <span data-ttu-id="cf7e4-164">No puede bloquearse la conectividad saliente de Internet.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-164">Outbound internet connectivity can not be blocked.</span></span>

* <span data-ttu-id="cf7e4-165">Se debe permitir el tráfico de la etiqueta AzureLoadBalancer.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-165">Traffic from the AzureLoadBalancer tag must be allowed.</span></span>

<span data-ttu-id="cf7e4-166">**P. ¿Cuáles son los límites de Application Gateway? ¿Puedo aumentar estos límites?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-166">**Q. What are the limits on Application Gateway? Can I increase these limits?**</span></span>

<span data-ttu-id="cf7e4-167">Visite [Límites de Application Gateway](../azure-subscription-service-limits.md#application-gateway-limits) para ver los límites.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-167">Visit [Application Gateway Limits](../azure-subscription-service-limits.md#application-gateway-limits) to view the limits.</span></span>

<span data-ttu-id="cf7e4-168">**P. ¿Puedo usar Application Gateway para tráfico externo e interno al mismo tiempo?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-168">**Q. Can I use Application Gateway for both external and internal traffic simultaneously?**</span></span>

<span data-ttu-id="cf7e4-169">Sí, Application Gateway admite una dirección IP interna y una dirección IP externa por cada instancia de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-169">Yes, Application Gateway supports having one internal IP and one external IP per Application Gateway.</span></span>

<span data-ttu-id="cf7e4-170">**P. ¿Se admite el emparejamiento de VNet?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-170">**Q. Is VNet peering supported?**</span></span>

<span data-ttu-id="cf7e4-171">Sí, se admite el emparejamiento de VNet y, además, es beneficioso para el tráfico de equilibrio de carga en otras redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-171">Yes, VNet peering is supported and is beneficial for load balancing traffic in other virtual networks.</span></span>

<span data-ttu-id="cf7e4-172">**P. ¿Se puede comunicar con servidores locales cuando están conectados mediante ExpressRoute o túneles VPN?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-172">**Q. Can I talk to on-premises servers when they are connected by ExpressRoute or VPN tunnels?**</span></span>

<span data-ttu-id="cf7e4-173">Sí, siempre que se permita el tráfico.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-173">Yes, as long as traffic is allowed.</span></span>

<span data-ttu-id="cf7e4-174">**P. ¿Se puede tener un grupo de back-end que preste servicio a muchas aplicaciones en puertos diferentes?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-174">**Q. Can I have one backend pool serving many applications on different ports?**</span></span>

<span data-ttu-id="cf7e4-175">Se admite la arquitectura de microservicios.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-175">Micro service architecture is supported.</span></span> <span data-ttu-id="cf7e4-176">Necesitaría varias opciones de configuración de http configuradas para realizar sondeos en puertos diferentes.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-176">You would need multiple http settings configured to probe on different ports.</span></span>

<span data-ttu-id="cf7e4-177">**P. ¿Admiten los sondeos personalizados caracteres comodín o regex en los datos de respuesta?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-177">**Q. Do custom probes support wildcards/regex on response data?**</span></span>

<span data-ttu-id="cf7e4-178">Los sondeos personalizados no admiten caracteres comodín o regex en los datos de respuesta.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-178">Custom probes do not support wildcard or regex on response data.</span></span> 

<span data-ttu-id="cf7e4-179">**P. ¿Cómo se procesan las reglas?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-179">**Q. How are rules processed?**</span></span>

<span data-ttu-id="cf7e4-180">Las reglas se procesan en el orden en que están configuradas.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-180">Rules are processed in the order they are configured.</span></span> <span data-ttu-id="cf7e4-181">Se recomienda que las reglas de varios sitios se configuren antes de las reglas básicas para reducir la posibilidad de que el tráfico se enrute al back-end inadecuado, ya que la regla básica coincidiría con el tráfico basado en el puerto antes de que se evalúe la regla de varios sitios.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-181">It is recommended that multi-site rules are configured before basic rules to reduce the chance that traffic is routed to the inappropriate backend as the basic rule would match traffic based on port prior to the multi-site rule being evaluated.</span></span>

<span data-ttu-id="cf7e4-182">**P. ¿Cómo se procesan las reglas?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-182">**Q. How are rules processed?**</span></span>

<span data-ttu-id="cf7e4-183">Las reglas se procesan en el orden en que se crearon.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-183">Rules are processed in the order they are created.</span></span> <span data-ttu-id="cf7e4-184">Se recomienda configurar las reglas multisitio antes que las reglas básicas.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-184">It is recommended that multi-site rules are configured before basic rules.</span></span> <span data-ttu-id="cf7e4-185">Al configurar primero los agentes de escucha multisitio, esta configuración reduce la probabilidad de que el tráfico se enrute al servidor no apropiado.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-185">By configuring multi-site listeners first, this configuration reduces the chance that traffic is routed to the inappropriate backend.</span></span> <span data-ttu-id="cf7e4-186">Este problema de enrutamiento puede ocurrir cuando la regla básica debería coincidir con tráfico basado en puerto antes que la regla multisitio que se va a evaluar.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-186">This routing issue can occur as the basic rule would match traffic based on port prior to the multi-site rule being evaluated.</span></span>

<span data-ttu-id="cf7e4-187">**P. ¿Qué significa el campo Host de los sondeos personalizados?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-187">**Q. What does the Host field for custom probes signify?**</span></span>

<span data-ttu-id="cf7e4-188">El campo Host especifica el nombre al que enviar el sondeo.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-188">Host field specifies the name to send the probe to.</span></span> <span data-ttu-id="cf7e4-189">Solo se puede aplicar cuando se ha configurado un entorno multisitio en Application Gateway; de lo contrario hay que usar '127.0.0.1'.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-189">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="cf7e4-190">Este valor es diferente del nombre de host de máquina virtual y está en formato \<protocolo\>://\<host\>:\<puerto\>\<ruta de acceso\>.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-190">This value is different from VM host name and is in format \<protocol\>://\<host\>:\<port\>\<path\>.</span></span>

<span data-ttu-id="cf7e4-191">**P. ¿Puedo permitir a Application Gateway el acceso a algunas direcciones IP de origen?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-191">**Q. Can I whitelist Application Gateway access to a few source IPs?**</span></span>

<span data-ttu-id="cf7e4-192">Este escenario puede hacerse mediante el uso de grupos de seguridad de red en la subred de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-192">This scenario can be done using NSGs on Application Gateway subnet.</span></span> <span data-ttu-id="cf7e4-193">Las siguientes restricciones se deben colocar en la subred en el orden de prioridad indicado:</span><span class="sxs-lookup"><span data-stu-id="cf7e4-193">The following restrictions should be put on the subnet in the listed order of priority:</span></span>

* <span data-ttu-id="cf7e4-194">Permitir el tráfico entrante de la IP o intervalo IP de origen.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-194">Allow incoming traffic from source IP/IP range.</span></span>

* <span data-ttu-id="cf7e4-195">Permitir las solicitudes entrantes de todos los orígenes a los puertos 65503-65534 para la [comunicación del estado del back-end](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="cf7e4-195">Allow incoming requests from all sources to ports 65503-65534 for [backend health communication](application-gateway-diagnostics.md).</span></span>

* <span data-ttu-id="cf7e4-196">Permitir sondeos entrantes de Azure Load Balancer (con la etiqueta AzureLoadBalancer) y el tráfico de red virtual entrante (con la etiqueta VirtualNetwork) en el [NSG](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="cf7e4-196">Allow incoming Azure Load Balancer probes (AzureLoadBalancer tag) and inbound virtual network traffic (VirtualNetwork tag) on the [NSG](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="cf7e4-197">Bloquear todo el tráfico entrante restante con una regla Denegar todo.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-197">Block all other incoming traffic with a Deny all rule.</span></span>

* <span data-ttu-id="cf7e4-198">Permitir el tráfico saliente a Internet para todos los destinos.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-198">Allow outbound traffic to the internet for all destinations.</span></span>

## <a name="performance"></a><span data-ttu-id="cf7e4-199">Rendimiento</span><span class="sxs-lookup"><span data-stu-id="cf7e4-199">Performance</span></span>

<span data-ttu-id="cf7e4-200">**P. ¿Cómo admite Application Gateway la alta disponibilidad y la escalabilidad?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-200">**Q. How does Application Gateway support high availability and scalability?**</span></span>

<span data-ttu-id="cf7e4-201">Application Gateway admite escenarios de alta disponibilidad cuando tiene dos o más instancias implementadas.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-201">Application Gateway supports high availability scenarios when you have two or more instances deployed.</span></span> <span data-ttu-id="cf7e4-202">Azure distribuye estas instancias entre dominios de actualización y de errores para asegurarse de que todas las instancias no produzcan un error al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-202">Azure distributes these instances across update and fault domains to ensure that all instances do not fail at the same time.</span></span> <span data-ttu-id="cf7e4-203">Application Gateway admite la escalabilidad mediante la adición de varias instancias de la misma puerta de enlace para compartir la carga.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-203">Application Gateway supports scalability by adding multiple instances of the same gateway to share the load.</span></span>

<span data-ttu-id="cf7e4-204">**P. ¿Cómo se puede lograr el escenario de recuperación ante desastres a través de centros de datos con Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-204">**Q. How do I achieve DR scenario across data centers with Application Gateway?**</span></span>

<span data-ttu-id="cf7e4-205">Los clientes pueden usar Traffic Manager para distribuir el tráfico a través de varias instancias de Application Gateway en distintos centros de datos.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-205">Customers can use Traffic Manager to distribute traffic across multiple Application Gateways in different datacenters.</span></span>

<span data-ttu-id="cf7e4-206">**P. ¿Se admite el escalado automático?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-206">**Q. Is auto scaling supported?**</span></span>

<span data-ttu-id="cf7e4-207">No, pero Application Gateway tiene una métrica de rendimiento que se puede utilizar para mostrar una alerta cuando se alcanza un determinado umbral.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-207">No, but Application Gateway has a throughput metric that can be used to alert you when a threshold is reached.</span></span> <span data-ttu-id="cf7e4-208">Agregar instancias manualmente o cambiar el tamaño no reinicia la puerta de enlace y no afecta al tráfico existente.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-208">Manually adding instances or changing size does not restart the gateway and does not impact existing traffic.</span></span>

<span data-ttu-id="cf7e4-209">**P. ¿Provoca el escalado o reducción vertical algún tiempo de inactividad?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-209">**Q. Does manual scale up/down cause downtime?**</span></span>

<span data-ttu-id="cf7e4-210">No hay ningún tiempo de inactividad, las instancias se distribuyen entre varios dominios de actualización y dominios de error.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-210">There is no downtime, instances are distributed across upgrade domains and fault domains.</span></span>

<span data-ttu-id="cf7e4-211">**P. ¿Puedo cambiar el tamaño de la instancia de mediano a grande sin que haya una interrupción?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-211">**Q. Can I change instance size from medium to large without disruption?**</span></span>

<span data-ttu-id="cf7e4-212">Sí, Azure distribuye las instancias entre los dominios de actualización y de errores para asegurarse de que todas las instancias no produzcan un error al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-212">Yes, Azure distributes instances across update and fault domains to ensure that all instances do not fail at the same time.</span></span> <span data-ttu-id="cf7e4-213">Application Gateway admite el escalado mediante la adición de varias instancias de la misma puerta de enlace para compartir la carga.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-213">Application Gateway supports scaling by adding multiple instances of the same gateway to share the load.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="cf7e4-214">Configuración de SSL</span><span class="sxs-lookup"><span data-stu-id="cf7e4-214">SSL Configuration</span></span>

<span data-ttu-id="cf7e4-215">**P. ¿Qué certificados se admiten en Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-215">**Q. What certificates are supported on Application Gateway?**</span></span>

<span data-ttu-id="cf7e4-216">Se admiten los certificados autofirmados, los certificados de entidad emisora de certificados y los certificados comodín.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-216">Self signed certs, CA certs, and wild-card certs are supported.</span></span> <span data-ttu-id="cf7e4-217">No se admiten los certificados de validación extendida (EV).</span><span class="sxs-lookup"><span data-stu-id="cf7e4-217">EV certs are not supported.</span></span>

<span data-ttu-id="cf7e4-218">**P. ¿Cuáles son los conjuntos de cifrado actuales que admite Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-218">**Q. What are the current cipher suites supported by Application Gateway?**</span></span>

<span data-ttu-id="cf7e4-219">Los siguientes son los conjuntos de cifrado actuales que admite Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-219">The following are the current cipher suites supported by application gateway.</span></span> <span data-ttu-id="cf7e4-220">Para aprender a personalizar opciones de SSL, visite [Configuración de versiones de directivas SSL y conjuntos de cifrado en Application Gateway](application-gateway-configure-ssl-policy-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cf7e4-220">Visit: [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) to learn how to customize SSL options.</span></span>

- <span data-ttu-id="cf7e4-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="cf7e4-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="cf7e4-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="cf7e4-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="cf7e4-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="cf7e4-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="cf7e4-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="cf7e4-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="cf7e4-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="cf7e4-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="cf7e4-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="cf7e4-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="cf7e4-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="cf7e4-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="cf7e4-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="cf7e4-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="cf7e4-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="cf7e4-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="cf7e4-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="cf7e4-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="cf7e4-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="cf7e4-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="cf7e4-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="cf7e4-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="cf7e4-233">TLS_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="cf7e4-233">TLS_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="cf7e4-234">TLS_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="cf7e4-234">TLS_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="cf7e4-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="cf7e4-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="cf7e4-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="cf7e4-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="cf7e4-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="cf7e4-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="cf7e4-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="cf7e4-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="cf7e4-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="cf7e4-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="cf7e4-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="cf7e4-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="cf7e4-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="cf7e4-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="cf7e4-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="cf7e4-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="cf7e4-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="cf7e4-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="cf7e4-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="cf7e4-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="cf7e4-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="cf7e4-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span></span>
- <span data-ttu-id="cf7e4-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="cf7e4-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span></span>

<span data-ttu-id="cf7e4-247">**P. ¿Admite Application Gateway también el recifrado del tráfico dirigido al back-end?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-247">**Q. Does Application Gateway also support re-encryption of traffic to the backend?**</span></span>

<span data-ttu-id="cf7e4-248">Sí, Application Gateway admite la descarga de SSL y SSL de extremo a extremo, lo cual permite volver a cifrar el tráfico dirigido al back-end.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-248">Yes, Application Gateway supports SSL offload, and end to end SSL, which re-encrypts the traffic to the backend.</span></span>

<span data-ttu-id="cf7e4-249">**P. ¿Se puede configurar la directiva SSL para controlar las versiones del protocolo SSL?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-249">**Q. Can I configure SSL policy to control SSL Protocol versions?**</span></span>

<span data-ttu-id="cf7e4-250">Sí, puede configurar Application Gateway para denegar TLS1.0, TLS1.1 y TLS1.2.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-250">Yes, you can configure Application Gateway to deny TLS1.0, TLS1.1, and TLS1.2.</span></span> <span data-ttu-id="cf7e4-251">SSL 2.0 y 3.0 ya están deshabilitados de forma predeterminada y no se pueden configurar.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-251">SSL 2.0 and 3.0 are already disabled by default and are not configurable.</span></span>

<span data-ttu-id="cf7e4-252">**P. ¿Puedo configurar los conjuntos de cifrado y el orden de las directivas?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-252">**Q. Can I configure cipher suites and policy order?**</span></span>

<span data-ttu-id="cf7e4-253">Sí, se admite la [configuración de conjuntos de cifrado](application-gateway-ssl-policy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cf7e4-253">Yes, [configuration of cipher suites](application-gateway-ssl-policy-overview.md) is supported.</span></span> <span data-ttu-id="cf7e4-254">Al definir una directiva personalizada, se debe habilitar al menos uno de los siguientes conjuntos de cifrado.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-254">When defining a custom policy, at least one of the following cipher suites must be enabled.</span></span> <span data-ttu-id="cf7e4-255">Application Gateway usa SHA256 para la administración de back-end.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-255">Application gateway uses SHA256 to for backend management.</span></span>

* <span data-ttu-id="cf7e4-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="cf7e4-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
* <span data-ttu-id="cf7e4-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="cf7e4-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
* <span data-ttu-id="cf7e4-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="cf7e4-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="cf7e4-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="cf7e4-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="cf7e4-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="cf7e4-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
* <span data-ttu-id="cf7e4-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="cf7e4-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

<span data-ttu-id="cf7e4-262">**P. ¿Cuántos certificados SSL se admiten?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-262">**Q. How many SSL certificates are supported?**</span></span>

<span data-ttu-id="cf7e4-263">Se admiten hasta 20 certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-263">Up to 20 SSL certificates are supported.</span></span>

<span data-ttu-id="cf7e4-264">**P. ¿Cuántos certificados de autenticación de recifrado de back-end se admiten?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-264">**Q. How many authentication certificates for backend re-encryption are supported?**</span></span>

<span data-ttu-id="cf7e4-265">Se admiten hasta 10 certificados de autenticación, con 5 como valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-265">Up to 10 authentication certificates are supported with a default of 5.</span></span>

<span data-ttu-id="cf7e4-266">**P. ¿Se integra Application Gateway con Azure Key Vault de forma nativa?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-266">**Q. Does Application Gateway integrate with Azure Key Vault natively?**</span></span>

<span data-ttu-id="cf7e4-267">No, no se integra con Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-267">No, it is not integrated with Azure Key Vault.</span></span>

## <a name="web-application-firewall-waf-configuration"></a><span data-ttu-id="cf7e4-268">Firewall de aplicaciones web (WAF): Configuración</span><span class="sxs-lookup"><span data-stu-id="cf7e4-268">Web Application Firewall (WAF) Configuration</span></span>

<span data-ttu-id="cf7e4-269">**P. ¿Ofrece la SKU de WAF todas las características disponibles con la SKU estándar?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-269">**Q. Does the WAF SKU offer all the features available with the Standard SKU?**</span></span>

<span data-ttu-id="cf7e4-270">Sí, WAF admite todas las características de la SKU estándar.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-270">Yes, WAF supports all the features in the Standard SKU.</span></span>

<span data-ttu-id="cf7e4-271">**P. ¿Qué versión de CRS admite Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-271">**Q. What is the CRS version Application Gateway supports?**</span></span>

<span data-ttu-id="cf7e4-272">Application Gateway admite CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) y CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span><span class="sxs-lookup"><span data-stu-id="cf7e4-272">Application Gateway supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span></span>

<span data-ttu-id="cf7e4-273">**P. ¿Cómo se supervisa el WAF?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-273">**Q. How do I monitor WAF?**</span></span>

<span data-ttu-id="cf7e4-274">WAF se supervisa a través del registro de diagnóstico. Puede encontrar más información sobre el registro de diagnóstico en [Métricas y registro de diagnóstico de Application Gateway](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="cf7e4-274">WAF is monitored through diagnostic logging, more information on diagnostic logging can be found at [Diagnostics Logging and Metrics for Application Gateway](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="cf7e4-275">**P. ¿Bloquea el modo de detección el tráfico?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-275">**Q. Does detection mode block traffic?**</span></span>

<span data-ttu-id="cf7e4-276">No, el modo de detección solo registra el tráfico, que desencadenó una regla de WAF.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-276">No, detection mode only logs traffic, which triggered a WAF rule.</span></span>

<span data-ttu-id="cf7e4-277">**P. ¿Cómo se personalizan las reglas de WAF?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-277">**Q. How do I customize WAF rules?**</span></span>

<span data-ttu-id="cf7e4-278">Sí, las reglas de WAF son personalizables. Para obtener más información sobre cómo personalizarlas, visite [Personalización de reglas y grupos de reglas de WAF](application-gateway-customize-waf-rules-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cf7e4-278">Yes, WAF rules are customizable, for more information on how to customize them visit [Customize WAF rule groups and rules](application-gateway-customize-waf-rules-portal.md)</span></span>

<span data-ttu-id="cf7e4-279">**P. ¿Qué reglas están disponibles actualmente?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-279">**Q. What rules are currently available?**</span></span>

<span data-ttu-id="cf7e4-280">WAF actualmente admite CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) y [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), que proporcionan una seguridad de línea de base frente a la mayoría de las 10 principales vulnerabilidades identificadas por Open Web Application Security Project (OWASP) y que se describen en [OWASP top 10 Vulnerabilities](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013) (Las 10 principales vulnerabilidades de OWASP).</span><span class="sxs-lookup"><span data-stu-id="cf7e4-280">WAF currently supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), which provide baseline security against most of the top 10 vulnerabilities identified by the Open Web Application Security Project (OWASP) found here [OWASP top 10 Vulnerabilities](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span></span>

* <span data-ttu-id="cf7e4-281">Protección contra la inyección de código SQL</span><span class="sxs-lookup"><span data-stu-id="cf7e4-281">SQL injection protection</span></span>

* <span data-ttu-id="cf7e4-282">Protección contra scripts entre sitios</span><span class="sxs-lookup"><span data-stu-id="cf7e4-282">Cross site scripting protection</span></span>

* <span data-ttu-id="cf7e4-283">Protección contra ataques web comunes, como inyección de comandos, contrabando de solicitudes HTTP, división de respuestas HTTP y ataque remoto de inclusión de archivos</span><span class="sxs-lookup"><span data-stu-id="cf7e4-283">Common Web Attacks Protection such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attack</span></span>

* <span data-ttu-id="cf7e4-284">Protección contra infracciones del protocolo HTTP</span><span class="sxs-lookup"><span data-stu-id="cf7e4-284">Protection against HTTP protocol violations</span></span>

* <span data-ttu-id="cf7e4-285">Protección contra anomalías del protocolo HTTP, como la falta de agentes de usuario de host y encabezados de aceptación</span><span class="sxs-lookup"><span data-stu-id="cf7e4-285">Protection against HTTP protocol anomalies such as missing host user-agent and accept headers</span></span>

* <span data-ttu-id="cf7e4-286">Prevención contra bots, rastreadores y escáneres</span><span class="sxs-lookup"><span data-stu-id="cf7e4-286">Prevention against bots, crawlers, and scanners</span></span>

* <span data-ttu-id="cf7e4-287">Detección de errores de configuración comunes en aplicaciones (es decir, Apache, IIS, etc.)</span><span class="sxs-lookup"><span data-stu-id="cf7e4-287">Detection of common application misconfigurations (that is, Apache, IIS, etc.)</span></span>

<span data-ttu-id="cf7e4-288">**P. ¿Admite también WAF la prevención DDoS?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-288">**Q. Does WAF also support DDoS prevention?**</span></span>

<span data-ttu-id="cf7e4-289">No, WAF no ofrece prevención DDoS.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-289">No, WAF does not provide DDoS prevention.</span></span>

## <a name="diagnostics-and-logging"></a><span data-ttu-id="cf7e4-290">Diagnósticos y registro</span><span class="sxs-lookup"><span data-stu-id="cf7e4-290">Diagnostics and Logging</span></span>

<span data-ttu-id="cf7e4-291">**P. ¿Qué tipos de registros están disponibles con Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-291">**Q. What types of logs are available with Application Gateway?**</span></span>

<span data-ttu-id="cf7e4-292">Hay tres registros disponibles para Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-292">There are three logs available for Application Gateway.</span></span> <span data-ttu-id="cf7e4-293">Para más información sobre estos registros y otras funcionalidades de diagnóstico, visite [Mantenimiento del back-end, registro de diagnóstico y métricas de Application Gateway](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="cf7e4-293">For more information on these logs and other diagnostic capabilities, visit [Backend health, diagnostics logs, and metrics for Application Gateway](application-gateway-diagnostics.md).</span></span>

- <span data-ttu-id="cf7e4-294">**ApplicationGatewayAccessLog**: este registro de acceso contiene todas las solicitudes enviadas al front-end de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-294">**ApplicationGatewayAccessLog** - The access log contains each request submitted to the Application Gateway frontend.</span></span> <span data-ttu-id="cf7e4-295">Los datos incluyen la dirección IP del autor de la llamada, la dirección URL solicitada, la latencia de la respuesta, el código de devolución y los bytes de entrada y salida. El registro de acceso se recopila cada 300 segundos.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-295">The data includes the caller's IP, URL requested, response latency, return code, bytes in and out. Access log is collected every 300 seconds.</span></span> <span data-ttu-id="cf7e4-296">Este registro contiene un registro por cada instancia de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-296">This log contains one record per instance of Application Gateway.</span></span>
- <span data-ttu-id="cf7e4-297">**ApplicationGatewayPerformanceLog**: este registro de rendimiento captura la información de rendimiento de cada instancia, incluida la cantidad total de solicitudes atendidas, el rendimiento en bytes, la cantidad de solicitudes con error y la cantidad de instancias back-end completadas correcta e incorrectamente.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-297">**ApplicationGatewayPerformanceLog** - The performance log captures performance information on per instance basis including total request served, throughput in bytes, total requests served, failed request count, healthy and unhealthy back-end instance count.</span></span>
- <span data-ttu-id="cf7e4-298">**ApplicationGatewayFirewallLog**: este registro de firewall contiene las solicitudes que se registran con el modo de detección o prevención de una puerta de enlace de aplicaciones que está configurada con el firewall de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-298">**ApplicationGatewayFirewallLog** - The firewall log contains requests that are logged through either detection or prevention mode of an application gateway that is configured with web application firewall.</span></span>

<span data-ttu-id="cf7e4-299">**P. ¿Cómo se puede saber si mis miembros del grupo de back-end están en buenas condiciones?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-299">**Q. How do I know if my backend pool members are healthy?**</span></span>

<span data-ttu-id="cf7e4-300">Puede usar el cmdlet de PowerShell `Get-AzureRmApplicationGatewayBackendHealth` o comprobar el estado a través del portal visitando [Diagnósticos de Application Gateway](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="cf7e4-300">You can use the PowerShell cmdlet `Get-AzureRmApplicationGatewayBackendHealth` or verify health through the portal by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="cf7e4-301">**P. ¿Qué es la directiva de retención en los registros de diagnóstico?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-301">**Q. What is the retention policy on the diagnostics logs?**</span></span>

<span data-ttu-id="cf7e4-302">Los registros de diagnóstico fluyen hacia la cuenta de almacenamiento de los clientes y estos pueden establecer la directiva de retención según sus preferencias.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-302">Diagnostic logs flow to the customers storage account and customers can set the retention policy based on their preference.</span></span> <span data-ttu-id="cf7e4-303">Los registros de diagnóstico también se pueden enviar a un centro de eventos o a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-303">Diagnostic logs can also be sent to an Event Hub or Log Analytics.</span></span> <span data-ttu-id="cf7e4-304">Visite [Diagnósticos de Application Gateway](application-gateway-diagnostics.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-304">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) for more details.</span></span>

<span data-ttu-id="cf7e4-305">**P. ¿Cómo se pueden obtener los registros de auditoría de Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-305">**Q. How do I get audit logs for Application Gateway?**</span></span>

<span data-ttu-id="cf7e4-306">Los registros de auditoría están disponibles para Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-306">Audit logs are available for Application Gateway.</span></span> <span data-ttu-id="cf7e4-307">En el portal, haga clic en **Registro de actividad** en la hoja de menú de una instancia de Application Gateway para tener acceso al registro de auditoría.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-307">In the portal, click **Activity Log** in the menu blade of an Application Gateway to access the audit log.</span></span> 

<span data-ttu-id="cf7e4-308">**P. ¿Se pueden establecer alertas con Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-308">**Q. Can I set alerts with Application Gateway?**</span></span>

<span data-ttu-id="cf7e4-309">Sí, Application Gateway admite alertas, y estas se configuran a partir de las métricas.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-309">Yes, Application Gateway does support alerts, alerts are configured off metrics.</span></span>  <span data-ttu-id="cf7e4-310">Application Gateway tiene actualmente una métrica de "rendimiento", que se puede configurar para que genere una alerta.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-310">Application Gateway currently has a metric of "throughput", which can be configured to alert.</span></span> <span data-ttu-id="cf7e4-311">Para más información sobre las alertas, visite [Recibir notificaciones de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="cf7e4-311">To learn more about alerts, visit [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="cf7e4-312">**P. El estado de back-end devuelve un estado desconocido, ¿que puede haberlo provocado?**</span><span class="sxs-lookup"><span data-stu-id="cf7e4-312">**Q. Backend health returns unknown status, what could be causing this status?**</span></span>

<span data-ttu-id="cf7e4-313">La razón más común es que el acceso al servidor está bloqueado por un NSG o DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-313">The most common reason is access to the backend is being blocked by an NSG or custom DNS.</span></span> <span data-ttu-id="cf7e4-314">Visite [Estado de back-end, registros de diagnóstico y métricas de Application Gateway](application-gateway-diagnostics.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="cf7e4-314">Visit [Backend health, diagnostics logging, and metrics for Application Gateway](application-gateway-diagnostics.md) to learn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf7e4-315">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cf7e4-315">Next Steps</span></span>

<span data-ttu-id="cf7e4-316">Para más información sobre Application Gateway, visite [Introducción a Application Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cf7e4-316">To learn more about Application Gateway visit [Introduction to Application Gateway](application-gateway-introduction.md).</span></span>
