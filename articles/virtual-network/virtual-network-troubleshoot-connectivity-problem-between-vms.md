---
title: "aaaTroubleshooting problemas de conectividad entre máquinas virtuales de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooTroubleshoot Hola problemas de conectividad entre máquinas virtuales de Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a><span data-ttu-id="151e6-103">Solución de problemas de conectividad entre máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="151e6-103">Troubleshooting connectivity problems between Azure VMs</span></span>

<span data-ttu-id="151e6-104">Es posible que experimente problemas de conectividad entre máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="151e6-104">You might experience connectivity problems between Azure VMs.</span></span> <span data-ttu-id="151e6-105">Este artículo proporciona toohelp de pasos de solución de problemas para resolver este problema.</span><span class="sxs-lookup"><span data-stu-id="151e6-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a><span data-ttu-id="151e6-106">Síntoma</span><span class="sxs-lookup"><span data-stu-id="151e6-106">Symptom</span></span>

<span data-ttu-id="151e6-107">Una VM de Azure no se puede conectar tooanother máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="151e6-107">An Azure VM cannot connect tooanother Azure VM.</span></span>

## <a name="troubleshooting-guidance"></a><span data-ttu-id="151e6-108">Guía de solución de problemas</span><span class="sxs-lookup"><span data-stu-id="151e6-108">Troubleshooting guidance</span></span> 

1. [<span data-ttu-id="151e6-109">Compruebe si está mal configurado NIC</span><span class="sxs-lookup"><span data-stu-id="151e6-109">Check if NIC is misconfigured</span></span>](#step-1-check-if-nic-is-misconfigured)
2. [<span data-ttu-id="151e6-110">Compruebe si el tráfico de red está bloqueado por NSG o UDR</span><span class="sxs-lookup"><span data-stu-id="151e6-110">Check if network traffic is blocked by NSG or UDR</span></span>](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [<span data-ttu-id="151e6-111">Compruebe si el tráfico de red está bloqueado por firewall de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="151e6-111">Check if network traffic is blocked by VM firewall</span></span>](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [<span data-ttu-id="151e6-112">Compruebe si VM aplicación o servicio está escuchando en el puerto de Hola</span><span class="sxs-lookup"><span data-stu-id="151e6-112">Check whether VM app or service is listening on hello port</span></span>](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [<span data-ttu-id="151e6-113">Compruebe si el problema de hello está provocado por SNAT</span><span class="sxs-lookup"><span data-stu-id="151e6-113">Check whether hello problem is caused by SNAT</span></span>](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [<span data-ttu-id="151e6-114">Compruebe si se bloquea el tráfico a una ACL para Hola VM clásico</span><span class="sxs-lookup"><span data-stu-id="151e6-114">Check whether traffic is blocked by ACLs for hello classic VM</span></span>](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [<span data-ttu-id="151e6-115">Compruebe si se crea el extremo de Hola para Hola VM clásico</span><span class="sxs-lookup"><span data-stu-id="151e6-115">Check whether hello endpoint is created for hello classic VM</span></span>](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [<span data-ttu-id="151e6-116">No se puede tooconnect tooa recurso compartido de red VM</span><span class="sxs-lookup"><span data-stu-id="151e6-116">Unable tooconnect tooa VM network share</span></span>](#step-8-unable-to-connect-to-a-vm-network-share)
9. [<span data-ttu-id="151e6-117">Conectividad de red virtual entre redes</span><span class="sxs-lookup"><span data-stu-id="151e6-117">Inter-Vnet connectivity</span></span>](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a><span data-ttu-id="151e6-118">Pasos para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="151e6-118">Troubleshooting steps</span></span>

<span data-ttu-id="151e6-119">Siga estos pasos tootroubleshoot problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="151e6-119">Follow these steps tootroubleshoot hello problem.</span></span> <span data-ttu-id="151e6-120">Compruebe si se ha resuelto el problema de hello después de cada paso.</span><span class="sxs-lookup"><span data-stu-id="151e6-120">Check whether hello problem is resolved after each step.</span></span> 

### <a name="step-1-check-if-nic-is-misconfigured"></a><span data-ttu-id="151e6-121">Paso 1: Comprobar si NIC está mal configurado</span><span class="sxs-lookup"><span data-stu-id="151e6-121">Step 1: Check if NIC is misconfigured</span></span>

<span data-ttu-id="151e6-122">Siga [cómo tooreset interfaz de red de VM en Windows Azure](../virtual-machines/windows/reset-network-interface.md).</span><span class="sxs-lookup"><span data-stu-id="151e6-122">Follow [How tooreset network interface for Azure Windows VM](../virtual-machines/windows/reset-network-interface.md).</span></span> 

<span data-ttu-id="151e6-123">Si el problema de Hola se produce después de modificar la interfaz de red (NIC) de hello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="151e6-123">If hello problem occurs after you modify hello network interface (NIC), follow these steps:</span></span>

<span data-ttu-id="151e6-124">**Máquinas virtuales de NIC de operaciones**</span><span class="sxs-lookup"><span data-stu-id="151e6-124">**Mulit-NIC VMs**</span></span>

1. <span data-ttu-id="151e6-125">Agregue una NIC.</span><span class="sxs-lookup"><span data-stu-id="151e6-125">Add a NIC.</span></span>
2. <span data-ttu-id="151e6-126">Solucionar problemas de Hola Hola incorrecta NIC o quitar incorrecta NIC.</span><span class="sxs-lookup"><span data-stu-id="151e6-126">Fix hello problems in hello bad NIC or remove bad NIC.</span></span>  <span data-ttu-id="151e6-127">A continuación, volver a añadir NIC de Hola.</span><span class="sxs-lookup"><span data-stu-id="151e6-127">Then readd hello NIC.</span></span>

<span data-ttu-id="151e6-128">Para obtener más información, consulte [tooor de interfaces de red de agregar quitar de máquinas virtuales](virtual-network-network-interface-vm.md).</span><span class="sxs-lookup"><span data-stu-id="151e6-128">For more information, see [Add network interfaces tooor remove from virtual machines](virtual-network-network-interface-vm.md).</span></span>

<span data-ttu-id="151e6-129">**Máquina virtual con una única NIC**</span><span class="sxs-lookup"><span data-stu-id="151e6-129">**Single-NIC VM**</span></span> 

- [<span data-ttu-id="151e6-130">Nueva implementación de la máquina virtual en Windows</span><span class="sxs-lookup"><span data-stu-id="151e6-130">Redeploy Windows VM</span></span>](../virtual-machines/windows/redeploy-to-new-node.md)
- [<span data-ttu-id="151e6-131">Nueva implementación de la máquina virtual de Linux</span><span class="sxs-lookup"><span data-stu-id="151e6-131">Redeploy Linux VM</span></span>](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a><span data-ttu-id="151e6-132">Paso 2: Comprobar si el tráfico de red está bloqueado por NSG o UDR</span><span class="sxs-lookup"><span data-stu-id="151e6-132">Step 2: Check if network traffic is blocked by NSG or UDR</span></span>

<span data-ttu-id="151e6-133">Utilizar [comprobar de flujo de IP de Monitor de red](../network-watcher/network-watcher-ip-flow-verify-overview.md) y [registro de flujo de NSG](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify si hay un grupo de seguridad de red o la ruta definida por el usuario que está interfiriendo con el flujo de tráfico.</span><span class="sxs-lookup"><span data-stu-id="151e6-133">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span>

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a><span data-ttu-id="151e6-134">Paso 3: Comprobar si el tráfico de red está bloqueado por firewall de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="151e6-134">Step 3: Check if network traffic is blocked by VM firewall</span></span>

<span data-ttu-id="151e6-135">Deshabilitar firewall de hello y, a continuación, el resultado de hello de pruebas.</span><span class="sxs-lookup"><span data-stu-id="151e6-135">Disable hello firewall, and then test hello result.</span></span> <span data-ttu-id="151e6-136">Si se resuelve el problema de hello, validar la configuración de hello en firewall de Hola y volver a habilitar.</span><span class="sxs-lookup"><span data-stu-id="151e6-136">If hello problem is resolved, validate hello settings in hello firewall and re-enable.</span></span>

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a><span data-ttu-id="151e6-137">Paso 4: Comprobar si VM aplicación o servicio está escuchando en el puerto de Hola</span><span class="sxs-lookup"><span data-stu-id="151e6-137">Step 4: Check whether VM app or service is listening on hello port</span></span>

<span data-ttu-id="151e6-138">Puede usar uno de hello siguiendo métodos toocheck si la aplicación de la máquina virtual o un servicio está escuchando en el puerto de Hola</span><span class="sxs-lookup"><span data-stu-id="151e6-138">You can use one of hello following methods toocheck whether VM Application or Service is listening on hello port</span></span>

- <span data-ttu-id="151e6-139">Ejecute hello después comandos toocheck si Hola servidor está escuchando en ese puerto.</span><span class="sxs-lookup"><span data-stu-id="151e6-139">Run hello following commands toocheck whether hello server is listening on that port.</span></span>

<span data-ttu-id="151e6-140">**Máquina virtual Windows**</span><span class="sxs-lookup"><span data-stu-id="151e6-140">**Windows VM**</span></span>

    netstat –ano

<span data-ttu-id="151e6-141">**Máquina virtual Linux**</span><span class="sxs-lookup"><span data-stu-id="151e6-141">**Linux VM**</span></span>

    netstat -l

- <span data-ttu-id="151e6-142">Ejecute hello **Telnet** comando hello puerto de máquina virtual tooitself tootest Hola.</span><span class="sxs-lookup"><span data-stu-id="151e6-142">Run hello **Telnet** command on hello VM tooitself tootest hello port.</span></span> <span data-ttu-id="151e6-143">Si se produce un error en la prueba de hello, aplicación o servicio no está toolisten configurado en el puerto de Hola.</span><span class="sxs-lookup"><span data-stu-id="151e6-143">If hello test fails, application or service is not configured toolisten on hello port.</span></span>

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a><span data-ttu-id="151e6-144">Paso 5: Comprobar si el problema de hello está provocado por SNAT</span><span class="sxs-lookup"><span data-stu-id="151e6-144">Step 5: Check whether hello problem is caused by SNAT</span></span>

<span data-ttu-id="151e6-145">En algunos escenarios, hello VM se coloca detrás de una solución de equilibrio de carga que tiene una dependencia de recursos fuera de Azure.</span><span class="sxs-lookup"><span data-stu-id="151e6-145">In some scenarios, hello VM is placed behind a Load balance solution that has a dependency on resources outside of Azure.</span></span> <span data-ttu-id="151e6-146">En estos casos, si tiene problemas de conexión intermitentes, problema de hello puede deberse a [agotamiento de puertos SNAT](../load-balancer/load-balancer-outbound-connections.md).</span><span class="sxs-lookup"><span data-stu-id="151e6-146">In these scenarios, if you experience intermittent connection problems, hello problem may be caused by [SNAT port exhaustion](../load-balancer/load-balancer-outbound-connections.md).</span></span> <span data-ttu-id="151e6-147">problema de hello tooresolve, crear una dirección VIP (o ILPIP para clásico) para cada máquina virtual que está detrás de equilibrador de carga de Hola y proteger con NSG o ACL.</span><span class="sxs-lookup"><span data-stu-id="151e6-147">tooresolve hello issue, create a VIP (or ILPIP for classic) for each VM that is behind hello Load balancer and secure with NSG or ACL.</span></span> 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a><span data-ttu-id="151e6-148">Paso 6: Comprobación de si se bloquea el tráfico a una ACL para Hola VM clásico</span><span class="sxs-lookup"><span data-stu-id="151e6-148">Step 6: Check whether traffic is blocked by ACLs for hello classic VM</span></span>

<span data-ttu-id="151e6-149">Una ACL proporciona Hola capacidad tooselectively permitir o denegar el tráfico para un punto de conexión de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="151e6-149">An ACL provides hello ability tooselectively permit or deny traffic for a virtual machine endpoint.</span></span> <span data-ttu-id="151e6-150">Para obtener más información, consulte [administrar Hola ACL en un punto de conexión](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span><span class="sxs-lookup"><span data-stu-id="151e6-150">For more information, see [Manage hello ACL on an endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a><span data-ttu-id="151e6-151">Paso 7: Comprobación de si se crea el punto de conexión de Hola Hola VM clásico</span><span class="sxs-lookup"><span data-stu-id="151e6-151">Step 7: Check whether hello endpoint is created for hello classic VM</span></span>

<span data-ttu-id="151e6-152">Todas las máquinas virtuales que cree en Azure mediante el modelo de implementación clásica de hello pueden comunicarse automáticamente a través de un canal de red privada con otras máquinas virtuales en hello que mismo servicio o de red virtual en la nube.</span><span class="sxs-lookup"><span data-stu-id="151e6-152">All VMs that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="151e6-153">Sin embargo, los equipos en otras redes virtuales requieren máquina virtual del tooa de tráfico de los puntos de conexión toodirect Hola red de entrada.</span><span class="sxs-lookup"><span data-stu-id="151e6-153">However, computers on other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="151e6-154">Para obtener más información, consulte [cómo tooset extremos](../virtual-machines/windows/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="151e6-154">For more information, see [How tooset up endpoints](../virtual-machines/windows/classic/setup-endpoints.md).</span></span>

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a><span data-ttu-id="151e6-155">Paso 8: Recurso compartido de red no se puede tooconnect tooa VM</span><span class="sxs-lookup"><span data-stu-id="151e6-155">Step 8: Unable tooconnect tooa VM network share</span></span>

<span data-ttu-id="151e6-156">Si es que no se puede tooconnect tooa recurso compartido de red VM, problema de hello puede deberse a que las NIC no está disponible en hello VM.</span><span class="sxs-lookup"><span data-stu-id="151e6-156">If you are unable tooconnect tooa VM network share, hello problem can be caused by unavailable NICs in hello VM.</span></span> <span data-ttu-id="151e6-157">toodelete Hola NIC no está disponible, vea [cómo toodelete Hola NIC no está disponible](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span><span class="sxs-lookup"><span data-stu-id="151e6-157">toodelete hello unavailable NICs, see [How toodelete hello unavailable NICs](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span></span>

### <a name="step-9-inter-vnet-connectivity"></a><span data-ttu-id="151e6-158">Paso 9: La conectividad de red virtual entre redes</span><span class="sxs-lookup"><span data-stu-id="151e6-158">Step 9: Inter-Vnet connectivity</span></span>

<span data-ttu-id="151e6-159">Utilizar [comprobar de flujo de IP de Monitor de red](../network-watcher/network-watcher-ip-flow-verify-overview.md) y [registro de flujo de NSG](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify si hay un grupo de seguridad de red o la ruta definida por el usuario que está interfiriendo con el flujo de tráfico.</span><span class="sxs-lookup"><span data-stu-id="151e6-159">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span> <span data-ttu-id="151e6-160">También puede validar la configuración de red virtual entre [aquí](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span><span class="sxs-lookup"><span data-stu-id="151e6-160">You can also validate your Inter-Vnet configuration [here](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span></span>

### <a name="need-help-contact-support"></a><span data-ttu-id="151e6-161">¿Necesita ayuda?</span><span class="sxs-lookup"><span data-stu-id="151e6-161">Need help?</span></span> <span data-ttu-id="151e6-162">Póngase en contacto con el servicio de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="151e6-162">Contact support.</span></span>
<span data-ttu-id="151e6-163">Si aún necesita ayuda, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget rápidamente para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="151e6-163">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
