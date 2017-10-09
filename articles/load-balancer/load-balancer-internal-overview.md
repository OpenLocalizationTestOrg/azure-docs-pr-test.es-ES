---
title: "información general del equilibrador de carga aaaInternal | Documentos de Microsoft"
description: "Información general de equilibrador de carga interno y sus características. Cómo funciona un equilibrador de carga para los extremos de Azure y posibles escenarios tooconfigure internos"
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
ms.openlocfilehash: 9a901aad224d8821c154e130e142699d57282b25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="23755-103">Información general sobre el equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="23755-103">Internal load balancer overview</span></span>

<span data-ttu-id="23755-104">A diferencia de hello Internet orientados al equilibrador de carga equilibrador de carga interno de hello (ILB) dirige el tráfico tooresources solo dentro de servicio de nube de Hola o mediante VPN tooaccess Hola infraestructura de Azure.</span><span class="sxs-lookup"><span data-stu-id="23755-104">Unlike hello Internet facing load balancer, hello internal load balancer (ILB) directs traffic only tooresources inside hello cloud service or using VPN tooaccess hello Azure infrastructure.</span></span> <span data-ttu-id="23755-105">infraestructura de Hello restringe el acceso toohello con equilibrio de carga direcciones IP virtual (VIP) de un servicio de nube o una red Virtual para que nunca será el punto de conexión de tooan directamente expuesto Internet.</span><span class="sxs-lookup"><span data-stu-id="23755-105">hello infrastructure restricts access toohello load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed tooan Internet endpoint.</span></span> <span data-ttu-id="23755-106">Esto permite una línea interna de toorun de las aplicaciones de negocio (LOB) en Azure y tener acceso desde dentro de la nube de Hola o desde recursos locales.</span><span class="sxs-lookup"><span data-stu-id="23755-106">This enables internal line of business (LOB) applications toorun in Azure and be accessed from within hello cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="23755-107">Por qué es posible que sea necesario un equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="23755-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="23755-108">El equilibrio de carga interno (ILB) de Azure proporciona equilibrio de carga entre las máquinas virtuales que residen dentro de un servicio en la nube o en una red virtual con un ámbito regional.</span><span class="sxs-lookup"><span data-stu-id="23755-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="23755-109">Para obtener información sobre el uso de Hola y la configuración de redes virtuales con un ámbito regional, consulte [redes virtuales regionales](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) Hola blog de Azure.</span><span class="sxs-lookup"><span data-stu-id="23755-109">For information about hello use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in hello Azure blog.</span></span> <span data-ttu-id="23755-110">Las redes virtuales existentes que se han configurado para un grupo de afinidad no pueden usar ILB.</span><span class="sxs-lookup"><span data-stu-id="23755-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="23755-111">ILB habilita Hola siguientes tipos de equilibrio de carga:</span><span class="sxs-lookup"><span data-stu-id="23755-111">ILB enables hello following types of load balancing:</span></span>

* <span data-ttu-id="23755-112">Dentro de un servicio de nube de máquinas virtuales tooa conjunto de máquinas virtuales que residen dentro de hello mismo servicio en la nube (consulte la figura 1).</span><span class="sxs-lookup"><span data-stu-id="23755-112">Within a cloud service, from virtual machines tooa set of virtual machines that reside within hello same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="23755-113">En una red virtual, desde máquinas virtuales en el conjunto de tooa de red virtual de Hola de máquinas virtuales que residen dentro de hello mismo servicio en la nube de hello virtual de red (consulte la figura 2).</span><span class="sxs-lookup"><span data-stu-id="23755-113">Within a virtual network, from virtual machines in hello virtual network tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 2).</span></span>
* <span data-ttu-id="23755-114">Para una red virtual entre entornos, de conjunto de tooa de equipos locales de máquinas virtuales que residen dentro de hello mismo servicio en la nube de hello virtual de red (consulte la figura 3).</span><span class="sxs-lookup"><span data-stu-id="23755-114">For a cross-premises virtual network, from on-premises computers tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 3).</span></span>
* <span data-ttu-id="23755-115">Aplicaciones accesibles desde Internet, de varios niveles en el que los niveles de back-end de hello no son accesibles desde Internet pero requieren equilibrio de carga para tráfico de capa de hello orientado a Internet.</span><span class="sxs-lookup"><span data-stu-id="23755-115">Internet-facing, multi-tier applications in which hello back-end tiers are not Internet-facing but require load balancing for traffic from hello Internet-facing tier.</span></span>
* <span data-ttu-id="23755-116">Equilibrio de carga para las aplicaciones LOB hospedadas en Azure sin requerir hardware ni software adicional de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="23755-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="23755-117">Incluir servidores locales Hola conjunto de equipos cuyo tráfico tiene una carga equilibrada.</span><span class="sxs-lookup"><span data-stu-id="23755-117">Including on-premises servers in hello set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="23755-118">Aplicaciones de niveles múltiples accesibles desde Internet</span><span class="sxs-lookup"><span data-stu-id="23755-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="23755-119">nivel de Hello web tiene extremos con conexión a Internet para clientes de Internet y forma parte de un conjunto con equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="23755-119">hello web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="23755-120">equilibrador de carga de Hello distribuye el tráfico entrante de los clientes web para TCP puerto 443 (HTTPS) toohello los servidores web.</span><span class="sxs-lookup"><span data-stu-id="23755-120">hello load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) toohello web servers.</span></span>

<span data-ttu-id="23755-121">servidores de base de datos de Hello están detrás de un punto de conexión ILB que usan servidores web de hello para el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="23755-121">hello database servers are behind an ILB endpoint which hello web servers use for storage.</span></span> <span data-ttu-id="23755-122">Esta carga del servicio de base de datos con equilibrio de punto de conexión, qué tráfico se carga equilibrada entre los servidores de base de datos de hello en hello ILB conjunto.</span><span class="sxs-lookup"><span data-stu-id="23755-122">This database service load balanced endpoint, which traffic is load balanced across hello database servers in hello ILB set.</span></span>

<span data-ttu-id="23755-123">siguiente imagen muestra de Hola Hola Internet con conexión a la aplicación de varios niveles dentro de hello mismo servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="23755-123">hello following image shows hello Internet facing multi-tier application within hello same cloud service.</span></span>

![Equilibrio de carga interno en un solo servicio en la nube](./media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="23755-125">Figura 1 - Una aplicación de niveles múltiples accesible desde Internet</span><span class="sxs-lookup"><span data-stu-id="23755-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="23755-126">Otro uso posible para una aplicación de varios nivel es cuando hello ILB implementa el servicio de nube diferente de tooa de Hola a un servicio de consumo de Hola para hello ILB.</span><span class="sxs-lookup"><span data-stu-id="23755-126">Another possible use for a multi-tier application is when hello ILB deployed tooa different cloud service than hello one consuming hello service for hello ILB.</span></span>

<span data-ttu-id="23755-127">En la nube con hello tendrá la misma red virtual de servicios tienen acceso a extremo ILB toohello.</span><span class="sxs-lookup"><span data-stu-id="23755-127">Cloud services using hello same virtual network will have access toohello ILB endpoint.</span></span> <span data-ttu-id="23755-128">Hola siguiendo la imagen se muestra en servidores front-end web están en un servicio de nube diferente de la base de datos back-end de Hola y utilizando Hola extremo ILB dentro de hello misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="23755-128">hello following image shows front-end web servers are in a different cloud service from hello database back-end and using hello ILB endpoint within hello same virtual network.</span></span>

![Equilibrio de carga interno entre servicios en la nube](./media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="23755-130">Figura 2 - Servidores front-end en un servicio en la nube diferente</span><span class="sxs-lookup"><span data-stu-id="23755-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="23755-131">Aplicaciones de línea de negocio de Intranet</span><span class="sxs-lookup"><span data-stu-id="23755-131">Intranet line of business applications</span></span>

<span data-ttu-id="23755-132">Tráfico de los clientes de red local de hello obtener el equilibrio de carga en conjunto Hola de los servidores LOB con red de tooAzure de conexión VPN.</span><span class="sxs-lookup"><span data-stu-id="23755-132">Traffic from clients on hello on-premises network get load-balanced across hello set of LOB servers using VPN connection tooAzure network.</span></span>

<span data-ttu-id="23755-133">equipo de cliente Hello tendrá acceso tooan dirección IP del servicio de VPN de Azure con VPN de punto toosite.</span><span class="sxs-lookup"><span data-stu-id="23755-133">hello client machine will have access tooan IP address from Azure VPN service using point toosite VPN.</span></span> <span data-ttu-id="23755-134">Permite Hola uso Hola aplicación LOB hospedada detrás de punto de conexión de hello ILB.</span><span class="sxs-lookup"><span data-stu-id="23755-134">It allows hello use hello LOB application hosted behind hello ILB endpoint.</span></span>

![Con VPN de punto toosite de equilibrio de carga interno](./media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="23755-136">Figura 3: aplicaciones LOB hospedadas detrás de punto de conexión de hello LB</span><span class="sxs-lookup"><span data-stu-id="23755-136">Figure 3 - LOB applications hosted behind hello LB endpoint</span></span>

<span data-ttu-id="23755-137">Otro escenario para hello LOB es toohave una red para el toohello virtual de sitio toosite VPN donde se configura el punto de conexión de hello ILB.</span><span class="sxs-lookup"><span data-stu-id="23755-137">Another scenario for hello LOB is toohave a site toosite VPN toohello virtual network where hello ILB endpoint is configured.</span></span> <span data-ttu-id="23755-138">Esto permite que el punto de conexión de local red tráfico toobe enrutado toohello ILB.</span><span class="sxs-lookup"><span data-stu-id="23755-138">This allows on-premises network traffic toobe routed toohello ILB endpoint.</span></span>

![Usar toosite VPN de sitio de equilibrio de carga interno](./media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="23755-140">Figura 4 - tráfico de red local enrutada toohello ILB extremo</span><span class="sxs-lookup"><span data-stu-id="23755-140">Figure 4 - On-premises network traffic routed toohello ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="23755-141">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="23755-141">Limitations</span></span>

<span data-ttu-id="23755-142">Las configuraciones del equilibrador de carga interno no son compatibles con SNAT.</span><span class="sxs-lookup"><span data-stu-id="23755-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="23755-143">En el contexto de Hola de este documento, SNAT hace referencia a traducción de direcciones en la red de origen de tooport enmascarado.</span><span class="sxs-lookup"><span data-stu-id="23755-143">In hello context of this document, SNAT refers tooport masquerading source  network address translation.</span></span>  <span data-ttu-id="23755-144">Esto aplica tooscenarios que una máquina virtual en un grupo de equilibradores de carga tiene dirección IP del tooreach Hola respectivos interno equilibrador de carga servidor front-end.</span><span class="sxs-lookup"><span data-stu-id="23755-144">This applies tooscenarios where a VM in a load balancer pool needs tooreach hello respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="23755-145">Este escenario no es compatible con el equilibrador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="23755-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="23755-146">Errores de conexión se producirán al flujo de hello es toohello de carga equilibrada VM que se originaron flujo Hola.</span><span class="sxs-lookup"><span data-stu-id="23755-146">Connection failures will occur when hello flow is load balanced toohello VM which originated hello flow.</span></span> <span data-ttu-id="23755-147">Debe usar un equilibrador de carga de estilo proxy para estos escenarios.</span><span class="sxs-lookup"><span data-stu-id="23755-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23755-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="23755-148">Next Steps</span></span>

[<span data-ttu-id="23755-149">Compatibilidad de Azure Resource Manager con Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="23755-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="23755-150">Introducción a la configuración de un equilibrador de carga accesible desde Internet</span><span class="sxs-lookup"><span data-stu-id="23755-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="23755-151">Introducción a la configuración de un equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="23755-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="23755-152">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="23755-152">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="23755-153">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="23755-153">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
