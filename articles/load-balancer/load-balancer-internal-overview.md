---
title: "Información general sobre el equilibrador de carga interno | Microsoft Docs"
description: "Información general sobre el equilibrador de carga interno y sus características. Cómo funciona un equilibrador de carga en Azure y posibles escenarios para configurar extremos internos"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: d324aaf8ec2c8766d5cf11452158d14c19cba4d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="91f5a-103">Información general sobre el equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="91f5a-103">Internal load balancer overview</span></span>

<span data-ttu-id="91f5a-104">A diferencia del equilibrador de carga accesible desde Internet, el equilibrador de carga interno (ILB) solo dirige el tráfico a los recursos dentro del servicio en la nube o mediante VPN para acceder la infraestructura de Azure.</span><span class="sxs-lookup"><span data-stu-id="91f5a-104">Unlike the Internet facing load balancer, the internal load balancer (ILB) directs traffic only to resources inside the cloud service or using VPN to access the Azure infrastructure.</span></span> <span data-ttu-id="91f5a-105">La infraestructura restringe el acceso a las direcciones IP virtuales de carga equilibrada de un servicio en la nube o una red virtual para que nunca se expongan directamente a un punto de conexión de Internet.</span><span class="sxs-lookup"><span data-stu-id="91f5a-105">The infrastructure restricts access to the load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed to an Internet endpoint.</span></span> <span data-ttu-id="91f5a-106">Esto permite que las aplicaciones de línea de negocio (LOB) internas se ejecuten en Azure y se tenga acceso a ellas desde la nube o los recursos locales.</span><span class="sxs-lookup"><span data-stu-id="91f5a-106">This enables internal line of business (LOB) applications to run in Azure and be accessed from within the cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="91f5a-107">Por qué es posible que sea necesario un equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="91f5a-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="91f5a-108">El equilibrio de carga interno (ILB) de Azure proporciona equilibrio de carga entre las máquinas virtuales que residen dentro de un servicio en la nube o en una red virtual con un ámbito regional.</span><span class="sxs-lookup"><span data-stu-id="91f5a-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="91f5a-109">Para obtener información sobre el uso y la configuración de redes virtuales con un ámbito regional, consulte [Redes virtuales regionales](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) en el blog de Azure.</span><span class="sxs-lookup"><span data-stu-id="91f5a-109">For information about the use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in the Azure blog.</span></span> <span data-ttu-id="91f5a-110">Las redes virtuales existentes que se han configurado para un grupo de afinidad no pueden usar ILB.</span><span class="sxs-lookup"><span data-stu-id="91f5a-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="91f5a-111">ILB permite los siguientes tipos de equilibrio de carga:</span><span class="sxs-lookup"><span data-stu-id="91f5a-111">ILB enables the following types of load balancing:</span></span>

* <span data-ttu-id="91f5a-112">En un servicio en la nube, entre máquinas virtuales y un conjunto de máquinas virtuales que residen en el mismo servicio en la nube (consulte la Ilustración 1).</span><span class="sxs-lookup"><span data-stu-id="91f5a-112">Within a cloud service, from virtual machines to a set of virtual machines that reside within the same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="91f5a-113">En una red virtual, entre las máquinas virtuales de la red virtual y un conjunto de máquinas virtuales que residen en el mismo servicio en la nube de la red virtual (consulte la Ilustración 2).</span><span class="sxs-lookup"><span data-stu-id="91f5a-113">Within a virtual network, from virtual machines in the virtual network to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 2).</span></span>
* <span data-ttu-id="91f5a-114">En una red virtual entre locales, entre los equipos locales y un conjunto de máquinas virtuales que residen en el mismo servicio en la nube de la red virtual (consulte la Ilustración 3).</span><span class="sxs-lookup"><span data-stu-id="91f5a-114">For a cross-premises virtual network, from on-premises computers to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 3).</span></span>
* <span data-ttu-id="91f5a-115">Aplicaciones de niveles múltiples accesibles desde Internet en las que los niveles back-end no son accesibles desde Internet, sino que requieren equilibrio de carga para el tráfico que procede del nivel accesible desde Internet.</span><span class="sxs-lookup"><span data-stu-id="91f5a-115">Internet-facing, multi-tier applications in which the back-end tiers are not Internet-facing but require load balancing for traffic from the Internet-facing tier.</span></span>
* <span data-ttu-id="91f5a-116">Equilibrio de carga para las aplicaciones LOB hospedadas en Azure sin requerir hardware ni software adicional de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="91f5a-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="91f5a-117">Se incluyen los servidores locales del conjunto de equipos de cuyo tráfico se va a equilibrar la carga.</span><span class="sxs-lookup"><span data-stu-id="91f5a-117">Including on-premises servers in the set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="91f5a-118">Aplicaciones de niveles múltiples accesibles desde Internet</span><span class="sxs-lookup"><span data-stu-id="91f5a-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="91f5a-119">El nivel web tiene extremos accesibles desde Internet para clientes de Internet y forma parte de un conjunto con equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="91f5a-119">The web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="91f5a-120">El equilibrador de carga distribuye el tráfico que procede de los clientes web en el puerto TCP 443 (HTTPS) a los servidores web.</span><span class="sxs-lookup"><span data-stu-id="91f5a-120">The load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) to the web servers.</span></span>

<span data-ttu-id="91f5a-121">Los servidores de base de datos están detrás de un extremo ILB que los servidores web usan para el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="91f5a-121">The database servers are behind an ILB endpoint which the web servers use for storage.</span></span> <span data-ttu-id="91f5a-122">Este es el extremo con equilibrio de carga del servicio de base de datos, de cuyo tráfico se va a equilibrar la carga entre los servidores de base de datos del conjunto ILB.</span><span class="sxs-lookup"><span data-stu-id="91f5a-122">This database service load balanced endpoint, which traffic is load balanced across the database servers in the ILB set.</span></span>

<span data-ttu-id="91f5a-123">La imagen siguiente muestra la aplicación de niveles múltiples accesible desde Internet dentro del mismo servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="91f5a-123">The following image shows the Internet facing multi-tier application within the same cloud service.</span></span>

![Equilibrio de carga interno en un solo servicio en la nube](./media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="91f5a-125">Figura 1 - Una aplicación de niveles múltiples accesible desde Internet</span><span class="sxs-lookup"><span data-stu-id="91f5a-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="91f5a-126">Otro uso posible para una aplicación de niveles múltiples es cuando ILB se implementa en un servicio en la nube diferente al que consume el servicio para ILB.</span><span class="sxs-lookup"><span data-stu-id="91f5a-126">Another possible use for a multi-tier application is when the ILB deployed to a different cloud service than the one consuming the service for the ILB.</span></span>

<span data-ttu-id="91f5a-127">Los servicios en la nube que usan la misma red virtual tendrán acceso al extremo ILB.</span><span class="sxs-lookup"><span data-stu-id="91f5a-127">Cloud services using the same virtual network will have access to the ILB endpoint.</span></span> <span data-ttu-id="91f5a-128">En la imagen siguiente se muestran los servidores web front-end que se encuentran en un servicio en la nube diferente al del back-end de base de datos y que utilizan el punto de conexión ILB dentro de la misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="91f5a-128">The following image shows front-end web servers are in a different cloud service from the database back-end and using the ILB endpoint within the same virtual network.</span></span>

![Equilibrio de carga interno entre servicios en la nube](./media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="91f5a-130">Figura 2 - Servidores front-end en un servicio en la nube diferente</span><span class="sxs-lookup"><span data-stu-id="91f5a-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="91f5a-131">Aplicaciones de línea de negocio de Intranet</span><span class="sxs-lookup"><span data-stu-id="91f5a-131">Intranet line of business applications</span></span>

<span data-ttu-id="91f5a-132">La carga del tráfico de los clientes de la red local se equilibra entre el conjunto de servidores LOB mediante una conexión VPN a la red de Azure.</span><span class="sxs-lookup"><span data-stu-id="91f5a-132">Traffic from clients on the on-premises network get load-balanced across the set of LOB servers using VPN connection to Azure network.</span></span>

<span data-ttu-id="91f5a-133">El equipo cliente tendrá acceso a una dirección IP desde el servicio de VPN de Azure con VPN de sitio a punto.</span><span class="sxs-lookup"><span data-stu-id="91f5a-133">The client machine will have access to an IP address from Azure VPN service using point to site VPN.</span></span> <span data-ttu-id="91f5a-134">Permite el uso de la aplicación LOB hospedada detrás del punto de conexión ILB.</span><span class="sxs-lookup"><span data-stu-id="91f5a-134">It allows the use the LOB application hosted behind the ILB endpoint.</span></span>

![Equilibrio de carga interno mediante una VPN de punto a sitio](./media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="91f5a-136">Figura 3 - Aplicaciones LOB hospedadas detrás del punto de conexión ILB</span><span class="sxs-lookup"><span data-stu-id="91f5a-136">Figure 3 - LOB applications hosted behind the LB endpoint</span></span>

<span data-ttu-id="91f5a-137">Otro escenario para LOB es tener una VPN de sitio a sitio a la red virtual donde está configurado el punto de conexión ILB.</span><span class="sxs-lookup"><span data-stu-id="91f5a-137">Another scenario for the LOB is to have a site to site VPN to the virtual network where the ILB endpoint is configured.</span></span> <span data-ttu-id="91f5a-138">Esto permitirá que el tráfico de red local se enrute al punto de conexión ILB.</span><span class="sxs-lookup"><span data-stu-id="91f5a-138">This allows on-premises network traffic to be routed to the ILB endpoint.</span></span>

![Equilibrio de carga interno mediante una VPN de sitio a sitio](./media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="91f5a-140">Figura 4 - Tráfico de red local enrutado al punto de conexión ILB</span><span class="sxs-lookup"><span data-stu-id="91f5a-140">Figure 4 - On-premises network traffic routed to the ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="91f5a-141">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="91f5a-141">Limitations</span></span>

<span data-ttu-id="91f5a-142">Las configuraciones del equilibrador de carga interno no son compatibles con SNAT.</span><span class="sxs-lookup"><span data-stu-id="91f5a-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="91f5a-143">En el contexto de este documento, SNAT se refiere a la traducción de direcciones de red de origen de enmascaramiento de puertos.</span><span class="sxs-lookup"><span data-stu-id="91f5a-143">In the context of this document, SNAT refers to port masquerading source  network address translation.</span></span>  <span data-ttu-id="91f5a-144">Se aplica a escenarios donde una máquina virtual de un grupo de equilibradores de carga tiene que llegar a la dirección IP del servidor front-end del equilibrador de carga interno respectivo.</span><span class="sxs-lookup"><span data-stu-id="91f5a-144">This applies to scenarios where a VM in a load balancer pool needs to reach the respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="91f5a-145">Este escenario no es compatible con el equilibrador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="91f5a-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="91f5a-146">Se producirán errores de conexión cuando el flujo sea de carga equilibrada en la máquina virtual que ha originado ese flujo.</span><span class="sxs-lookup"><span data-stu-id="91f5a-146">Connection failures will occur when the flow is load balanced to the VM which originated the flow.</span></span> <span data-ttu-id="91f5a-147">Debe usar un equilibrador de carga de estilo proxy para estos escenarios.</span><span class="sxs-lookup"><span data-stu-id="91f5a-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="91f5a-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="91f5a-148">Next Steps</span></span>

[<span data-ttu-id="91f5a-149">Compatibilidad de Azure Resource Manager con Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="91f5a-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="91f5a-150">Introducción a la configuración de un equilibrador de carga accesible desde Internet</span><span class="sxs-lookup"><span data-stu-id="91f5a-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="91f5a-151">Introducción a la configuración de un equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="91f5a-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="91f5a-152">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="91f5a-152">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="91f5a-153">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="91f5a-153">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
