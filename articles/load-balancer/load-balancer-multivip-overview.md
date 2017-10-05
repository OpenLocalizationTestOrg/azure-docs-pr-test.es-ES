---
title: Varias IP virtuales para Azure Load Balancer | Microsoft Docs
description: "Información general de varias IP virtuales para Azure Load Balancer"
services: load-balancer
documentationcenter: na
author: chkuhtz
manager: narayan
editor: 
ms.assetid: 748e50cd-3087-4c2e-a9e1-ac0ecce4f869
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2016
ms.author: chkuhtz
ms.openlocfilehash: d9e88b859020be2a96a57a01e5624052ed134b64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="multiple-vips-for-azure-load-balancer"></a><span data-ttu-id="9f649-103">Varias IP virtuales para Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="9f649-103">Multiple VIPs for Azure Load Balancer</span></span>

<span data-ttu-id="9f649-104">Azure Load Balancer permite utilizar servicios de equilibrio de carga en varios puertos, varias direcciones IP, o en ambos.</span><span class="sxs-lookup"><span data-stu-id="9f649-104">Azure Load Balancer allows you to load balance services on multiple ports, multiple IP addresses, or both.</span></span> <span data-ttu-id="9f649-105">Puede usar las definiciones de equilibrador de carga públicas e internas para flujos de equilibrio de carga entre un conjunto de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9f649-105">You can use public and internal load balancer definitions to load balance flows across a set of VMs.</span></span>

<span data-ttu-id="9f649-106">En este artículo se describen los fundamentos de esta capacidad, los conceptos importantes y las restricciones.</span><span class="sxs-lookup"><span data-stu-id="9f649-106">This article describes the fundamentals of this ability, important concepts, and constraints.</span></span> <span data-ttu-id="9f649-107">Si solo desea exponer los servicios en una dirección IP, puede encontrar instrucciones simplificadas para configuraciones [públicas](load-balancer-get-started-internet-portal.md) o [internas](load-balancer-get-started-ilb-arm-portal.md) del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="9f649-107">If you only intend to expose services on one IP address, you can find simplified instructions for [public](load-balancer-get-started-internet-portal.md) or [internal](load-balancer-get-started-ilb-arm-portal.md) load balancer configurations.</span></span> <span data-ttu-id="9f649-108">Agregar varias direcciones IP virtuales es una acción incremental de la configuración de una única IP virtual.</span><span class="sxs-lookup"><span data-stu-id="9f649-108">Adding Multiple VIPs is incremental to a single VIP configuration.</span></span> <span data-ttu-id="9f649-109">Mediante los conceptos de este artículo, puede expandir una configuración simplificada en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="9f649-109">Using the concepts in this article, you can expand a simplified configuration at any time.</span></span>

<span data-ttu-id="9f649-110">Al definir un Azure Load Balancer, las configuraciones front-end y back-end están conectadas con reglas.</span><span class="sxs-lookup"><span data-stu-id="9f649-110">When you define an Azure Load Balancer, a frontend and a backend configuration are connected with rules.</span></span> <span data-ttu-id="9f649-111">El sondeo de estado a que hace referencia la regla se utiliza para determinar cómo se envían nuevos flujos a un nodo en el grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="9f649-111">The health probe referenced by the rule is used to determine how new flows are sent to a node in the backend pool.</span></span> <span data-ttu-id="9f649-112">El front-end se define mediante una IP Virtual (VIP), que es una tupla de 3 que consta de una dirección IP (pública o interna), un protocolo de transporte (UDP o TCP) y un número de puerto.</span><span class="sxs-lookup"><span data-stu-id="9f649-112">The frontend is defined by a Virtual IP (VIP), which is a 3-tuple comprised of an IP address (public or internal), a transport protocol (UDP or TCP), and a port number.</span></span> <span data-ttu-id="9f649-113">Una DIP es una dirección IP de un NIC virtual de Azure conectado a una máquina virtual en el grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="9f649-113">A DIP is an IP address on an Azure virtual NIC attached to a VM in the backend pool.</span></span>

<span data-ttu-id="9f649-114">La tabla siguiente contiene algunas configuraciones de front-end de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f649-114">The following table contains some example frontend configurations:</span></span>

| <span data-ttu-id="9f649-115">IP virtual</span><span class="sxs-lookup"><span data-stu-id="9f649-115">VIP</span></span> | <span data-ttu-id="9f649-116">Dirección IP</span><span class="sxs-lookup"><span data-stu-id="9f649-116">IP address</span></span> | <span data-ttu-id="9f649-117">protocolo</span><span class="sxs-lookup"><span data-stu-id="9f649-117">protocol</span></span> | <span data-ttu-id="9f649-118">puerto</span><span class="sxs-lookup"><span data-stu-id="9f649-118">port</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9f649-119">1</span><span class="sxs-lookup"><span data-stu-id="9f649-119">1</span></span> |<span data-ttu-id="9f649-120">65.52.0.1</span><span class="sxs-lookup"><span data-stu-id="9f649-120">65.52.0.1</span></span> |<span data-ttu-id="9f649-121">TCP</span><span class="sxs-lookup"><span data-stu-id="9f649-121">TCP</span></span> |<span data-ttu-id="9f649-122">80</span><span class="sxs-lookup"><span data-stu-id="9f649-122">80</span></span> |
| <span data-ttu-id="9f649-123">2</span><span class="sxs-lookup"><span data-stu-id="9f649-123">2</span></span> |<span data-ttu-id="9f649-124">65.52.0.1</span><span class="sxs-lookup"><span data-stu-id="9f649-124">65.52.0.1</span></span> |<span data-ttu-id="9f649-125">TCP</span><span class="sxs-lookup"><span data-stu-id="9f649-125">TCP</span></span> |<span data-ttu-id="9f649-126">*8080*</span><span class="sxs-lookup"><span data-stu-id="9f649-126">*8080*</span></span> |
| <span data-ttu-id="9f649-127">3</span><span class="sxs-lookup"><span data-stu-id="9f649-127">3</span></span> |<span data-ttu-id="9f649-128">65.52.0.1</span><span class="sxs-lookup"><span data-stu-id="9f649-128">65.52.0.1</span></span> |<span data-ttu-id="9f649-129">*UDP*</span><span class="sxs-lookup"><span data-stu-id="9f649-129">*UDP*</span></span> |<span data-ttu-id="9f649-130">80</span><span class="sxs-lookup"><span data-stu-id="9f649-130">80</span></span> |
| <span data-ttu-id="9f649-131">4</span><span class="sxs-lookup"><span data-stu-id="9f649-131">4</span></span> |<span data-ttu-id="9f649-132">*65.52.0.2*</span><span class="sxs-lookup"><span data-stu-id="9f649-132">*65.52.0.2*</span></span> |<span data-ttu-id="9f649-133">TCP</span><span class="sxs-lookup"><span data-stu-id="9f649-133">TCP</span></span> |<span data-ttu-id="9f649-134">80</span><span class="sxs-lookup"><span data-stu-id="9f649-134">80</span></span> |

<span data-ttu-id="9f649-135">En la tabla se muestran cuatro front-end diferentes.</span><span class="sxs-lookup"><span data-stu-id="9f649-135">The table shows four different frontends.</span></span> <span data-ttu-id="9f649-136">Los front-end 1, 2 y 3 son una sola dirección IP virtual con varias reglas.</span><span class="sxs-lookup"><span data-stu-id="9f649-136">Frontends #1, #2 and #3 are a single VIP with multiple rules.</span></span> <span data-ttu-id="9f649-137">Se utiliza la misma dirección IP, pero el puerto o el protocolo es diferente para cada front-end.</span><span class="sxs-lookup"><span data-stu-id="9f649-137">The same IP address is used but the port or protocol is different for each frontend.</span></span> <span data-ttu-id="9f649-138">Los front-end 1 y 4 son un ejemplo de varias direcciones IP virtuales, donde se reutilizan el mismo protocolo front-end y el puerto a través de varias direcciones IP virtuales.</span><span class="sxs-lookup"><span data-stu-id="9f649-138">Frontends #1 and #4 are an example of Multiple VIPs, where the same frontend protocol and port are reused across multiple VIPs.</span></span>

<span data-ttu-id="9f649-139">Azure Load Balancer proporciona flexibilidad para definir las reglas de equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="9f649-139">Azure Load Balancer provides flexibility in defining the load balancing rules.</span></span> <span data-ttu-id="9f649-140">Una regla declara cómo se asigna una dirección y el puerto en el front-end a la dirección de destino y al puerto en el back-end.</span><span class="sxs-lookup"><span data-stu-id="9f649-140">A rule declares how an address and port on the frontend is mapped to the destination address and port on the backend.</span></span> <span data-ttu-id="9f649-141">El hecho de que los puertos back-end se reutilicen o no a través de las reglas depende del tipo de regla.</span><span class="sxs-lookup"><span data-stu-id="9f649-141">Whether or not backend ports are reused across rules depends on the type of the rule.</span></span> <span data-ttu-id="9f649-142">Cada tipo de regla tiene requisitos específicos que pueden afectar al diseño del sondeo y a la configuración del host.</span><span class="sxs-lookup"><span data-stu-id="9f649-142">Each type of rule has specific requirements that can affect host configuration and probe design.</span></span> <span data-ttu-id="9f649-143">Existen dos tipos de reglas:</span><span class="sxs-lookup"><span data-stu-id="9f649-143">There are two types of rules:</span></span>

1. <span data-ttu-id="9f649-144">La regla predeterminada sin la reutilización de un puerto back-end</span><span class="sxs-lookup"><span data-stu-id="9f649-144">The default rule with no backend port reuse</span></span>
2. <span data-ttu-id="9f649-145">La regla de dirección IP flotante donde se reutilizan puertos back-end</span><span class="sxs-lookup"><span data-stu-id="9f649-145">The Floating IP rule where backend ports are reused</span></span>

<span data-ttu-id="9f649-146">Azure Load Balancer permite combinar ambos tipos de regla en la misma configuración de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="9f649-146">Azure Load Balancer allows you to mix both rule types on the same load balancer configuration.</span></span> <span data-ttu-id="9f649-147">El equilibrador de carga puede utilizarlos simultáneamente para una máquina virtual determinada, o cualquier combinación, siempre y cuando se cumplan las restricciones de la regla.</span><span class="sxs-lookup"><span data-stu-id="9f649-147">The load balancer can use them simultaneously for a given VM, or any combination, as long as you abide by the constraints of the rule.</span></span> <span data-ttu-id="9f649-148">El tipo de regla que elija depende de los requisitos de la aplicación y la complejidad de la compatibilidad con dicha configuración.</span><span class="sxs-lookup"><span data-stu-id="9f649-148">Which rule type you choose depends on the requirements of your application and the complexity of supporting that configuration.</span></span> <span data-ttu-id="9f649-149">Debe evaluar qué tipos de reglas son mejores para su escenario.</span><span class="sxs-lookup"><span data-stu-id="9f649-149">You should evaluate which rule types are best for your scenario.</span></span>

<span data-ttu-id="9f649-150">Se analizan aún más estos escenarios empezando con el comportamiento predeterminado.</span><span class="sxs-lookup"><span data-stu-id="9f649-150">We explore these scenarios further by starting with the default behavior.</span></span>

## <a name="rule-type-1-no-backend-port-reuse"></a><span data-ttu-id="9f649-151">Tipo de regla 1: No reutilización de puerto back-end</span><span class="sxs-lookup"><span data-stu-id="9f649-151">Rule type #1: No backend port reuse</span></span>

![Ilustración de varias IP virtuales](./media/load-balancer-multivip-overview/load-balancer-multivip.png)

<span data-ttu-id="9f649-153">En este escenario, las IP virtuales front-end están configuradas como sigue:</span><span class="sxs-lookup"><span data-stu-id="9f649-153">In this scenario, the frontend VIPs are configured as follows:</span></span>

| <span data-ttu-id="9f649-154">IP virtual</span><span class="sxs-lookup"><span data-stu-id="9f649-154">VIP</span></span> | <span data-ttu-id="9f649-155">Dirección IP</span><span class="sxs-lookup"><span data-stu-id="9f649-155">IP address</span></span> | <span data-ttu-id="9f649-156">protocolo</span><span class="sxs-lookup"><span data-stu-id="9f649-156">protocol</span></span> | <span data-ttu-id="9f649-157">puerto</span><span class="sxs-lookup"><span data-stu-id="9f649-157">port</span></span> |
| --- | --- | --- | --- |
| ![IP virtual](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) <span data-ttu-id="9f649-159">1</span><span class="sxs-lookup"><span data-stu-id="9f649-159">1</span></span> |<span data-ttu-id="9f649-160">65.52.0.1</span><span class="sxs-lookup"><span data-stu-id="9f649-160">65.52.0.1</span></span> |<span data-ttu-id="9f649-161">TCP</span><span class="sxs-lookup"><span data-stu-id="9f649-161">TCP</span></span> |<span data-ttu-id="9f649-162">80</span><span class="sxs-lookup"><span data-stu-id="9f649-162">80</span></span> |
| ![IP virtual](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) <span data-ttu-id="9f649-164">2</span><span class="sxs-lookup"><span data-stu-id="9f649-164">2</span></span> |<span data-ttu-id="9f649-165">*65.52.0.2*</span><span class="sxs-lookup"><span data-stu-id="9f649-165">*65.52.0.2*</span></span> |<span data-ttu-id="9f649-166">TCP</span><span class="sxs-lookup"><span data-stu-id="9f649-166">TCP</span></span> |<span data-ttu-id="9f649-167">80</span><span class="sxs-lookup"><span data-stu-id="9f649-167">80</span></span> |

<span data-ttu-id="9f649-168">La DIP es el destino del flujo de entrada.</span><span class="sxs-lookup"><span data-stu-id="9f649-168">The DIP is the destination of the inbound flow.</span></span> <span data-ttu-id="9f649-169">En el grupo back-end, cada máquina virtual expone el servicio deseado en un puerto único en una DIP.</span><span class="sxs-lookup"><span data-stu-id="9f649-169">In the backend pool, each VM exposes the desired service on a unique port on a DIP.</span></span> <span data-ttu-id="9f649-170">Este servicio está asociado con el front-end a través de una definición de regla.</span><span class="sxs-lookup"><span data-stu-id="9f649-170">This service is associated with the frontend through a rule definition.</span></span>

<span data-ttu-id="9f649-171">Se definen dos reglas:</span><span class="sxs-lookup"><span data-stu-id="9f649-171">We define two rules:</span></span>

| <span data-ttu-id="9f649-172">Regla</span><span class="sxs-lookup"><span data-stu-id="9f649-172">Rule</span></span> | <span data-ttu-id="9f649-173">Asignación de front-end</span><span class="sxs-lookup"><span data-stu-id="9f649-173">Map frontend</span></span> | <span data-ttu-id="9f649-174">Para grupo back-end</span><span class="sxs-lookup"><span data-stu-id="9f649-174">To backend pool</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9f649-175">1</span><span class="sxs-lookup"><span data-stu-id="9f649-175">1</span></span> |![IP virtual](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) <span data-ttu-id="9f649-177">VIP1:80</span><span class="sxs-lookup"><span data-stu-id="9f649-177">VIP1:80</span></span> |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) <span data-ttu-id="9f649-179">DIP1:80,</span><span class="sxs-lookup"><span data-stu-id="9f649-179">DIP1:80,</span></span> ![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) <span data-ttu-id="9f649-181">DIP2:80</span><span class="sxs-lookup"><span data-stu-id="9f649-181">DIP2:80</span></span> |
| <span data-ttu-id="9f649-182">2</span><span class="sxs-lookup"><span data-stu-id="9f649-182">2</span></span> |![IP virtual](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) <span data-ttu-id="9f649-184">VIP2:80</span><span class="sxs-lookup"><span data-stu-id="9f649-184">VIP2:80</span></span> |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) <span data-ttu-id="9f649-186">DIP1:81,</span><span class="sxs-lookup"><span data-stu-id="9f649-186">DIP1:81,</span></span> ![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) <span data-ttu-id="9f649-188">DIP2:81</span><span class="sxs-lookup"><span data-stu-id="9f649-188">DIP2:81</span></span> |

<span data-ttu-id="9f649-189">La asignación completa en Azure Load Balancer ahora se realiza como sigue:</span><span class="sxs-lookup"><span data-stu-id="9f649-189">The complete mapping in Azure Load Balancer is now as follows:</span></span>

| <span data-ttu-id="9f649-190">Regla</span><span class="sxs-lookup"><span data-stu-id="9f649-190">Rule</span></span> | <span data-ttu-id="9f649-191">Dirección IP de IP virtual</span><span class="sxs-lookup"><span data-stu-id="9f649-191">VIP IP address</span></span> | <span data-ttu-id="9f649-192">protocolo</span><span class="sxs-lookup"><span data-stu-id="9f649-192">protocol</span></span> | <span data-ttu-id="9f649-193">puerto</span><span class="sxs-lookup"><span data-stu-id="9f649-193">port</span></span> | <span data-ttu-id="9f649-194">Destino</span><span class="sxs-lookup"><span data-stu-id="9f649-194">Destination</span></span> | <span data-ttu-id="9f649-195">puerto</span><span class="sxs-lookup"><span data-stu-id="9f649-195">port</span></span> |
| --- | --- | --- | --- | --- | --- |
| ![Regla](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) <span data-ttu-id="9f649-197">1</span><span class="sxs-lookup"><span data-stu-id="9f649-197">1</span></span> |<span data-ttu-id="9f649-198">65.52.0.1</span><span class="sxs-lookup"><span data-stu-id="9f649-198">65.52.0.1</span></span> |<span data-ttu-id="9f649-199">TCP</span><span class="sxs-lookup"><span data-stu-id="9f649-199">TCP</span></span> |<span data-ttu-id="9f649-200">80</span><span class="sxs-lookup"><span data-stu-id="9f649-200">80</span></span> |<span data-ttu-id="9f649-201">Dirección IP de DIP</span><span class="sxs-lookup"><span data-stu-id="9f649-201">DIP IP Address</span></span> |<span data-ttu-id="9f649-202">80</span><span class="sxs-lookup"><span data-stu-id="9f649-202">80</span></span> |
| ![Regla](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) <span data-ttu-id="9f649-204">2</span><span class="sxs-lookup"><span data-stu-id="9f649-204">2</span></span> |<span data-ttu-id="9f649-205">65.52.0.2</span><span class="sxs-lookup"><span data-stu-id="9f649-205">65.52.0.2</span></span> |<span data-ttu-id="9f649-206">TCP</span><span class="sxs-lookup"><span data-stu-id="9f649-206">TCP</span></span> |<span data-ttu-id="9f649-207">80</span><span class="sxs-lookup"><span data-stu-id="9f649-207">80</span></span> |<span data-ttu-id="9f649-208">Dirección IP de DIP</span><span class="sxs-lookup"><span data-stu-id="9f649-208">DIP IP Address</span></span> |<span data-ttu-id="9f649-209">81</span><span class="sxs-lookup"><span data-stu-id="9f649-209">81</span></span> |

<span data-ttu-id="9f649-210">Cada regla debe generar un flujo con una combinación única de dirección IP de destino y puerto de destino.</span><span class="sxs-lookup"><span data-stu-id="9f649-210">Each rule must produce a flow with a unique combination of destination IP address and destination port.</span></span> <span data-ttu-id="9f649-211">Al variar el puerto de destino del flujo, varias reglas pueden entregar flujos en la misma DIP en puertos diferentes.</span><span class="sxs-lookup"><span data-stu-id="9f649-211">By varying the destination port of the flow, multiple rules can deliver flows to the same DIP on different ports.</span></span>

<span data-ttu-id="9f649-212">Los sondeos de estado siempre se dirigen a la DIP de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9f649-212">Health probes are always directed to the DIP of a VM.</span></span> <span data-ttu-id="9f649-213">Debe asegurarse de que el sondeo refleja el estado de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9f649-213">You must ensure you that your probe reflects the health of the VM.</span></span>

## <a name="rule-type-2-backend-port-reuse-by-using-floating-ip"></a><span data-ttu-id="9f649-214">Tipo de regla 2: reutilización de puerto back-end mediante IP flotante</span><span class="sxs-lookup"><span data-stu-id="9f649-214">Rule type #2: backend port reuse by using Floating IP</span></span>

<span data-ttu-id="9f649-215">Azure Load Balancer proporciona la flexibilidad para reutilizar el puerto front-end en varias direcciones IP virtuales independientemente del tipo de regla que se utiliza.</span><span class="sxs-lookup"><span data-stu-id="9f649-215">Azure Load Balancer provides the flexibility to reuse the frontend port across multiple VIPs regardless of the rule type used.</span></span> <span data-ttu-id="9f649-216">Además, algunos escenarios de aplicación prefieren o requieren que varias instancias de la aplicación usen el mismo puerto en una sola máquina virtual en el grupo back-end.</span><span class="sxs-lookup"><span data-stu-id="9f649-216">Additionally, some application scenarios prefer or require the same port to be used by multiple application instances on a single VM in the backend pool.</span></span> <span data-ttu-id="9f649-217">Entre los ejemplos comunes de reutilización de puertos se incluyen la agrupación en clústeres para alta disponibilidad, dispositivos de red virtuales y la exposición de varios puntos de conexión TLS sin volver a cifrar.</span><span class="sxs-lookup"><span data-stu-id="9f649-217">Common examples of port reuse include clustering for high availability, network virtual appliances, and exposing multiple TLS endpoints without re-encryption.</span></span>

<span data-ttu-id="9f649-218">Si desea reutilizar el puerto back-end en varias reglas, debe habilitar la IP flotante en la definición de la regla.</span><span class="sxs-lookup"><span data-stu-id="9f649-218">If you want to reuse the backend port across multiple rules, you must enable Floating IP in the rule definition.</span></span>

<span data-ttu-id="9f649-219">La IP flotante es una parte de lo que se conoce como Direct Server Return (DSR).</span><span class="sxs-lookup"><span data-stu-id="9f649-219">Floating IP is a portion of what is known as Direct Server Return (DSR).</span></span> <span data-ttu-id="9f649-220">DSR consta de dos partes: una topología de flujo y un esquema de asignación de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="9f649-220">DSR consists of two parts: a flow topology and an IP address mapping scheme.</span></span> <span data-ttu-id="9f649-221">En un nivel de plataforma, Azure Load Balancer siempre funciona en una topología de flujo DSR independientemente de si la dirección IP flotante está habilitada o no.</span><span class="sxs-lookup"><span data-stu-id="9f649-221">At a platform level, Azure Load Balancer always operates in a DSR flow topology regardless of whether Floating IP is enabled or not.</span></span> <span data-ttu-id="9f649-222">Esto significa que la parte de salida de un flujo siempre se reescribe correctamente para que se dirija de nuevo al origen.</span><span class="sxs-lookup"><span data-stu-id="9f649-222">This means that the outbound part of a flow is always correctly rewritten to flow directly back to the origin.</span></span>

<span data-ttu-id="9f649-223">Con el tipo de regla predeterminada, Azure expone un esquema de asignación de direcciones IP de equilibrio de carga tradicional a efectos de facilitar el uso.</span><span class="sxs-lookup"><span data-stu-id="9f649-223">With the default rule type, Azure exposes a traditional load balancing IP address mapping scheme for ease of use.</span></span> <span data-ttu-id="9f649-224">Habilitar la dirección IP flotante cambia el esquema de asignación de direcciones IP para permitir una flexibilidad adicional, como se explica a continuación.</span><span class="sxs-lookup"><span data-stu-id="9f649-224">Enabling Floating IP changes the IP address mapping scheme to allow for additional flexibility as explained below.</span></span>

<span data-ttu-id="9f649-225">En el siguiente diagrama, se ilustra esta configuración:</span><span class="sxs-lookup"><span data-stu-id="9f649-225">The following diagram illustrates this configuration:</span></span>

![Ilustración de varias IP virtuales](./media/load-balancer-multivip-overview/load-balancer-multivip-dsr.png)

<span data-ttu-id="9f649-227">En este escenario, cada máquina virtual del grupo back-end tiene tres interfaces de red:</span><span class="sxs-lookup"><span data-stu-id="9f649-227">For this scenario, every VM in the backend pool has three network interfaces:</span></span>

* <span data-ttu-id="9f649-228">DIP: una NIC virtual asociada a la máquina virtual (configuración IP del recurso NIC de Azure)</span><span class="sxs-lookup"><span data-stu-id="9f649-228">DIP: a Virtual NIC associated with the VM (IP configuration of Azure's NIC resource)</span></span>
* <span data-ttu-id="9f649-229">VIP1: una interfaz de bucle invertido en el SO invitado que se configura con la dirección IP de VIP1</span><span class="sxs-lookup"><span data-stu-id="9f649-229">VIP1: a loopback interface within guest OS that is configured with IP address of VIP1</span></span>
* <span data-ttu-id="9f649-230">VIP2: una interfaz de bucle invertido en el SO invitado que se configura con la dirección IP de VIP2</span><span class="sxs-lookup"><span data-stu-id="9f649-230">VIP2: a loopback interface within guest OS that is configured with IP address of VIP2</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f649-231">La configuración de las interfaces lógicas se ejecuta en el SO invitado.</span><span class="sxs-lookup"><span data-stu-id="9f649-231">The configuration of the logical interfaces is performed within the guest OS.</span></span> <span data-ttu-id="9f649-232">Esta configuración no se ejecuta ni administra en Azure.</span><span class="sxs-lookup"><span data-stu-id="9f649-232">This configuration is not performed or managed by Azure.</span></span> <span data-ttu-id="9f649-233">Sin esta configuración, las reglas no funcionarán.</span><span class="sxs-lookup"><span data-stu-id="9f649-233">Without this configuration, the rules will not function.</span></span> <span data-ttu-id="9f649-234">Las definiciones de sondeo de estado usan la DIP de la máquina virtual en lugar de la dirección IP virtual lógica.</span><span class="sxs-lookup"><span data-stu-id="9f649-234">Health probe definitions use the DIP of the VM rather than the logical VIP.</span></span> <span data-ttu-id="9f649-235">Por lo tanto, el servicio debe proporcionar las respuestas del sondeo en un puerto DIP que reflejen el estado del servicio ofrecido en la dirección IP virtual lógica.</span><span class="sxs-lookup"><span data-stu-id="9f649-235">Therefore, your service must provide probe responses on a DIP port that reflect the status of the service offered on the logical VIP.</span></span>

<span data-ttu-id="9f649-236">Se asume que la configuración front-end es la misma que en el escenario anterior:</span><span class="sxs-lookup"><span data-stu-id="9f649-236">Let's assume the same frontend configuration as in the previous scenario:</span></span>

| <span data-ttu-id="9f649-237">IP virtual</span><span class="sxs-lookup"><span data-stu-id="9f649-237">VIP</span></span> | <span data-ttu-id="9f649-238">Dirección IP</span><span class="sxs-lookup"><span data-stu-id="9f649-238">IP address</span></span> | <span data-ttu-id="9f649-239">protocolo</span><span class="sxs-lookup"><span data-stu-id="9f649-239">protocol</span></span> | <span data-ttu-id="9f649-240">puerto</span><span class="sxs-lookup"><span data-stu-id="9f649-240">port</span></span> |
| --- | --- | --- | --- |
| ![IP virtual](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) <span data-ttu-id="9f649-242">1</span><span class="sxs-lookup"><span data-stu-id="9f649-242">1</span></span> |<span data-ttu-id="9f649-243">65.52.0.1</span><span class="sxs-lookup"><span data-stu-id="9f649-243">65.52.0.1</span></span> |<span data-ttu-id="9f649-244">TCP</span><span class="sxs-lookup"><span data-stu-id="9f649-244">TCP</span></span> |<span data-ttu-id="9f649-245">80</span><span class="sxs-lookup"><span data-stu-id="9f649-245">80</span></span> |
| ![IP virtual](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) <span data-ttu-id="9f649-247">2</span><span class="sxs-lookup"><span data-stu-id="9f649-247">2</span></span> |<span data-ttu-id="9f649-248">*65.52.0.2*</span><span class="sxs-lookup"><span data-stu-id="9f649-248">*65.52.0.2*</span></span> |<span data-ttu-id="9f649-249">TCP</span><span class="sxs-lookup"><span data-stu-id="9f649-249">TCP</span></span> |<span data-ttu-id="9f649-250">80</span><span class="sxs-lookup"><span data-stu-id="9f649-250">80</span></span> |

<span data-ttu-id="9f649-251">Se definen dos reglas:</span><span class="sxs-lookup"><span data-stu-id="9f649-251">We define two rules:</span></span>

| <span data-ttu-id="9f649-252">Regla</span><span class="sxs-lookup"><span data-stu-id="9f649-252">Rule</span></span> | <span data-ttu-id="9f649-253">Asignación de front-end</span><span class="sxs-lookup"><span data-stu-id="9f649-253">Map frontend</span></span> | <span data-ttu-id="9f649-254">Para grupo back-end</span><span class="sxs-lookup"><span data-stu-id="9f649-254">To backend pool</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9f649-255">1</span><span class="sxs-lookup"><span data-stu-id="9f649-255">1</span></span> |![Regla](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) <span data-ttu-id="9f649-257">VIP1:80</span><span class="sxs-lookup"><span data-stu-id="9f649-257">VIP1:80</span></span> |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) <span data-ttu-id="9f649-259">VIP1:80 (en VM1 y VM2)</span><span class="sxs-lookup"><span data-stu-id="9f649-259">VIP1:80 (in VM1 and VM2)</span></span> |
| <span data-ttu-id="9f649-260">2</span><span class="sxs-lookup"><span data-stu-id="9f649-260">2</span></span> |![Regla](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) <span data-ttu-id="9f649-262">VIP2:80</span><span class="sxs-lookup"><span data-stu-id="9f649-262">VIP2:80</span></span> |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) <span data-ttu-id="9f649-264">VIP2:80 (en VM1 y VM2)</span><span class="sxs-lookup"><span data-stu-id="9f649-264">VIP2:80 (in VM1 and VM2)</span></span> |

<span data-ttu-id="9f649-265">En la tabla siguiente se muestra la asignación completa en el equilibrador de carga:</span><span class="sxs-lookup"><span data-stu-id="9f649-265">The following table shows the complete mapping in the load balancer:</span></span>

| <span data-ttu-id="9f649-266">Regla</span><span class="sxs-lookup"><span data-stu-id="9f649-266">Rule</span></span> | <span data-ttu-id="9f649-267">Dirección IP de IP virtual</span><span class="sxs-lookup"><span data-stu-id="9f649-267">VIP IP address</span></span> | <span data-ttu-id="9f649-268">protocolo</span><span class="sxs-lookup"><span data-stu-id="9f649-268">protocol</span></span> | <span data-ttu-id="9f649-269">puerto</span><span class="sxs-lookup"><span data-stu-id="9f649-269">port</span></span> | <span data-ttu-id="9f649-270">Destino</span><span class="sxs-lookup"><span data-stu-id="9f649-270">Destination</span></span> | <span data-ttu-id="9f649-271">puerto</span><span class="sxs-lookup"><span data-stu-id="9f649-271">port</span></span> |
| --- | --- | --- | --- | --- | --- |
| ![IP virtual](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) <span data-ttu-id="9f649-273">1</span><span class="sxs-lookup"><span data-stu-id="9f649-273">1</span></span> |<span data-ttu-id="9f649-274">65.52.0.1</span><span class="sxs-lookup"><span data-stu-id="9f649-274">65.52.0.1</span></span> |<span data-ttu-id="9f649-275">TCP</span><span class="sxs-lookup"><span data-stu-id="9f649-275">TCP</span></span> |<span data-ttu-id="9f649-276">80</span><span class="sxs-lookup"><span data-stu-id="9f649-276">80</span></span> |<span data-ttu-id="9f649-277">igual que la dirección VIP (65.52.0.1)</span><span class="sxs-lookup"><span data-stu-id="9f649-277">same as VIP (65.52.0.1)</span></span> |<span data-ttu-id="9f649-278">igual que la dirección VIP (80)</span><span class="sxs-lookup"><span data-stu-id="9f649-278">same as VIP (80)</span></span> |
| ![IP virtual](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) <span data-ttu-id="9f649-280">2</span><span class="sxs-lookup"><span data-stu-id="9f649-280">2</span></span> |<span data-ttu-id="9f649-281">65.52.0.2</span><span class="sxs-lookup"><span data-stu-id="9f649-281">65.52.0.2</span></span> |<span data-ttu-id="9f649-282">TCP</span><span class="sxs-lookup"><span data-stu-id="9f649-282">TCP</span></span> |<span data-ttu-id="9f649-283">80</span><span class="sxs-lookup"><span data-stu-id="9f649-283">80</span></span> |<span data-ttu-id="9f649-284">igual que la dirección VIP (65.52.0.2)</span><span class="sxs-lookup"><span data-stu-id="9f649-284">same as VIP (65.52.0.2)</span></span> |<span data-ttu-id="9f649-285">igual que la dirección VIP (80)</span><span class="sxs-lookup"><span data-stu-id="9f649-285">same as VIP (80)</span></span> |

<span data-ttu-id="9f649-286">El destino del flujo de entrada es la dirección IP virtual en la interfaz de bucle invertido en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9f649-286">The destination of the inbound flow is the VIP address on the loopback interface in the VM.</span></span> <span data-ttu-id="9f649-287">Cada regla debe generar un flujo con una combinación única de dirección IP de destino y puerto de destino.</span><span class="sxs-lookup"><span data-stu-id="9f649-287">Each rule must produce a flow with a unique combination of destination IP address and destination port.</span></span> <span data-ttu-id="9f649-288">Al variar la dirección IP de destino del flujo, se puede reutilizar el puerto en la misma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9f649-288">By varying the destination IP address of the flow, port reuse is possible on the same VM.</span></span> <span data-ttu-id="9f649-289">El servicio se expone al equilibrador de carga enlazándolo con la dirección IP de la IP virtual y al puerto de la interfaz de bucle invertido correspondiente.</span><span class="sxs-lookup"><span data-stu-id="9f649-289">Your service is exposed to the load balancer by binding it to the VIP’s IP address and port of the respective loopback interface.</span></span>

<span data-ttu-id="9f649-290">Observe que este ejemplo no cambia el puerto de destino.</span><span class="sxs-lookup"><span data-stu-id="9f649-290">Notice that this example does not change the destination port.</span></span> <span data-ttu-id="9f649-291">Aunque se trata de un escenario de IP flotante, Azure Load Balancer también admite la definición de una regla para volver a escribir el puerto de destino back-end y para que sea diferente del puerto de destino front-end.</span><span class="sxs-lookup"><span data-stu-id="9f649-291">Even though this is a Floating IP scenario, Azure Load Balancer also supports defining a rule to rewrite the backend destination port and to make it different from the frontend destination port.</span></span>

<span data-ttu-id="9f649-292">El tipo de regla de dirección IP flotante es el fundamento de varios modelos de configuración del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="9f649-292">The Floating IP rule type is the foundation of several load balancer configuration patterns.</span></span> <span data-ttu-id="9f649-293">Un ejemplo que está disponible actualmente es la configuración [SQL AlwaysOn con varios agentes de escucha](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) .</span><span class="sxs-lookup"><span data-stu-id="9f649-293">One example that is currently available is the [SQL AlwaysOn with Multiple Listeners](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) configuration.</span></span> <span data-ttu-id="9f649-294">Con el tiempo, se documentarán varios de estos escenarios.</span><span class="sxs-lookup"><span data-stu-id="9f649-294">Over time, we will document more of these scenarios.</span></span>

## <a name="limitations"></a><span data-ttu-id="9f649-295">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="9f649-295">Limitations</span></span>

* <span data-ttu-id="9f649-296">Solo se admiten varias configuraciones de IP virtual con máquinas virtuales de IaaS.</span><span class="sxs-lookup"><span data-stu-id="9f649-296">Multiple VIP configurations are only supported with IaaS VMs.</span></span>
* <span data-ttu-id="9f649-297">Con la regla de dirección IP flotante, la aplicación debe utilizar la DIP para los flujos salientes.</span><span class="sxs-lookup"><span data-stu-id="9f649-297">With the Floating IP rule, your application must use the DIP for outbound flows.</span></span> <span data-ttu-id="9f649-298">Si la aplicación se enlaza a la dirección IP virtual configurada en la interfaz de bucle invertido en el sistema operativo invitado, a continuación, SNAT no está disponible para volver a escribir el flujo de salida y, por tanto, se produce un error en el flujo.</span><span class="sxs-lookup"><span data-stu-id="9f649-298">If your application binds to the VIP address configured on the loopback interface in the guest OS, then SNAT is not available to rewrite the outbound flow and the flow fails.</span></span>
* <span data-ttu-id="9f649-299">Las direcciones IP públicas repercuten en la facturación.</span><span class="sxs-lookup"><span data-stu-id="9f649-299">Public IP addresses have an effect on billing.</span></span> <span data-ttu-id="9f649-300">Para obtener más información, vea [Precios de las direcciones IP](https://azure.microsoft.com/pricing/details/ip-addresses/)</span><span class="sxs-lookup"><span data-stu-id="9f649-300">For more information, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/)</span></span>
* <span data-ttu-id="9f649-301">Se aplican los límites de suscripción.</span><span class="sxs-lookup"><span data-stu-id="9f649-301">Subscription limits apply.</span></span> <span data-ttu-id="9f649-302">Para más información, vea los [límites de servicio](../azure-subscription-service-limits.md#networking-limits) .</span><span class="sxs-lookup"><span data-stu-id="9f649-302">For more information, see [Service limits](../azure-subscription-service-limits.md#networking-limits) for details.</span></span>