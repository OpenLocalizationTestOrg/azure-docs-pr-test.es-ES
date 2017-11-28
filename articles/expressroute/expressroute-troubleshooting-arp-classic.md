---
title: "Obtención de tablas ARP: Implementación clásica: Solución de problemas de Azure ExpressRoute | Microsoft Docs"
description: "En esta página se proporcionan instrucciones para obtener tablas ARP para un circuito ExpressRoute."
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: b5856acf-03c2-4933-8111-6ce12998d92a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: fcc847b7e30fd55ca759830e0254ab7542e7663e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="getting-arp-tables-in-the-classic-deployment-model"></a><span data-ttu-id="23272-103">Obtención de tablas ARP en el modelo de implementación clásica</span><span class="sxs-lookup"><span data-stu-id="23272-103">Getting ARP tables in the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="23272-104">PowerShell: administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="23272-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="23272-105">PowerShell: clásico</span><span class="sxs-lookup"><span data-stu-id="23272-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="23272-106">Este artículo le guiará a través de los pasos para obtener las tablas del Protocolo de resolución de direcciones (ARP) para su circuito Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="23272-106">This article walks you through the steps for getting the Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23272-107">Este documento está pensado para ayudarle a diagnosticar y corregir problemas sencillos.</span><span class="sxs-lookup"><span data-stu-id="23272-107">This document is intended to help you diagnose and fix simple issues.</span></span> <span data-ttu-id="23272-108">No pretende sustituir al soporte técnico de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="23272-108">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="23272-109">Si no puede solucionar el problema mediante las siguientes instrucciones, abra una solicitud de soporte técnico con [Ayuda y soporte técnico de Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="23272-109">If you can't solve the problem by using the following guidance, open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="23272-110">Protocolo de resolución de direcciones (ARP) y tablas ARP</span><span class="sxs-lookup"><span data-stu-id="23272-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="23272-111">ARP es un protocolo de nivel 2 que se define en [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="23272-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="23272-112">ARP se usa para asignar una dirección Ethernet (dirección MAC) a una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="23272-112">ARP is used to map an Ethernet address (MAC address) to an IP address.</span></span>

<span data-ttu-id="23272-113">Una tabla ARP proporciona una asignación de la dirección IPv4 y la dirección MAC para un emparejamiento determinado.</span><span class="sxs-lookup"><span data-stu-id="23272-113">An ARP table provides a mapping of the IPv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="23272-114">La tabla ARP de un emparejamiento de circuito ExpressRoute proporciona la siguiente información para cada interfaz (principal y secundaria):</span><span class="sxs-lookup"><span data-stu-id="23272-114">The ARP table for an ExpressRoute circuit peering provides the following information for each interface (primary and secondary):</span></span>

1. <span data-ttu-id="23272-115">Asignación de una dirección IP de la interfaz del enrutador local a la dirección MAC</span><span class="sxs-lookup"><span data-stu-id="23272-115">Mapping of an on-premises router interface IP address to a MAC address</span></span>
2. <span data-ttu-id="23272-116">Asignación de la dirección IP de la interfaz del enrutador de ExpressRoute a la dirección MAC</span><span class="sxs-lookup"><span data-stu-id="23272-116">Mapping of an ExpressRoute router interface IP address to a MAC address</span></span>
3. <span data-ttu-id="23272-117">La antigüedad de la asignación</span><span class="sxs-lookup"><span data-stu-id="23272-117">The age of the mapping</span></span>

<span data-ttu-id="23272-118">Las tablas ARP pueden ayudar a validar la configuración de capa 2 y a solucionar los problemas básicos de conectividad de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="23272-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span></span>

<span data-ttu-id="23272-119">A continuación, se muestra un ejemplo de una tabla ARP:</span><span class="sxs-lookup"><span data-stu-id="23272-119">Following is an example of an ARP table:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="23272-120">En la siguiente sección se proporciona información sobre cómo puede ver las tablas ARP que ven los enrutadores de borde de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="23272-120">The following section provides information about how to view the ARP tables that are seen by the ExpressRoute edge routers.</span></span>

## <a name="prerequisites-for-using-arp-tables"></a><span data-ttu-id="23272-121">Requisitos previos para usar las tablas ARP</span><span class="sxs-lookup"><span data-stu-id="23272-121">Prerequisites for using ARP tables</span></span>
<span data-ttu-id="23272-122">Asegúrese de que tiene lo siguiente antes de continuar:</span><span class="sxs-lookup"><span data-stu-id="23272-122">Ensure that you have the following before you continue:</span></span>

* <span data-ttu-id="23272-123">Un circuito ExpressRoute válido configurado con al menos un emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="23272-123">A valid ExpressRoute circuit that's configured with at least one peering.</span></span> <span data-ttu-id="23272-124">El circuito debe estar completamente configurado por el proveedor de conectividad.</span><span class="sxs-lookup"><span data-stu-id="23272-124">The circuit must be fully configured by the connectivity provider.</span></span> <span data-ttu-id="23272-125">Usted (o su proveedor de conectividad) debe configurar al menos uno de los emparejamientos (privado de Azure, público de Azure o Microsoft) en este circuito.</span><span class="sxs-lookup"><span data-stu-id="23272-125">You (or your connectivity provider) must configure at least one of the peerings (Azure private, Azure public, or Microsoft) on this circuit.</span></span>
* <span data-ttu-id="23272-126">Intervalos de direcciones IP que se usan para configurar los emparejamientos (privado de Azure, público de Azure y Microsoft).</span><span class="sxs-lookup"><span data-stu-id="23272-126">IP address ranges that are used for configuring the peerings (Azure private, Azure public, and Microsoft).</span></span> <span data-ttu-id="23272-127">Revise los ejemplos de asignación de dirección IP en [Requisitos de enrutamiento de ExpressRoute](expressroute-routing.md) para comprender cómo se asignan las direcciones IP a las interfaces en su sitio y el sitio de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="23272-127">Review the IP address assignment examples in the [ExpressRoute routing requirements page](expressroute-routing.md) to get an understanding of how IP addresses are mapped to interfaces on your aise and on the ExpressRoute side.</span></span> <span data-ttu-id="23272-128">Puede obtener información sobre la configuración de emparejamiento en la página [Creación y modificación del enrutamiento de un circuito ExpressRoute](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="23272-128">You can get information about the peering configuration by reviewing the [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span></span>
* <span data-ttu-id="23272-129">Información del equipo de red o del proveedor de conectividad sobre las direcciones MAC de las interfaces que se usan con estas direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="23272-129">Information from your networking team or connectivity provider about the MAC addresses of the interfaces that are used with these IP addresses.</span></span>
* <span data-ttu-id="23272-130">El módulo más reciente de Windows PowerShell para Azure (versión 1.50 o superior).</span><span class="sxs-lookup"><span data-stu-id="23272-130">The latest Windows PowerShell module for Azure (version 1.50 or later).</span></span>

## <a name="arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="23272-131">Tablas ARP para el circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="23272-131">ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="23272-132">En esta sección se proporcionan instrucciones sobre cómo ver las tablas ARP para cada tipo de emparejamiento mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23272-132">This section provides instructions about how to view the ARP tables for each type of peering by using PowerShell.</span></span> <span data-ttu-id="23272-133">Antes de continuar, usted o su proveedor de conectividad necesita configurar el emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="23272-133">Before you continue, either you or your connectivity provider needs to configure the peering.</span></span> <span data-ttu-id="23272-134">Cada circuito tiene dos rutas de acceso (principal y secundaria).</span><span class="sxs-lookup"><span data-stu-id="23272-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="23272-135">Puede comprobar en la tabla ARP cada ruta de acceso de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="23272-135">You can check the ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="23272-136">Tablas ARP para el emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="23272-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="23272-137">El siguiente cmdlet proporciona el emparejamiento privado de Azure para las tablas ARP:</span><span class="sxs-lookup"><span data-stu-id="23272-137">The following cmdlet provides the ARP tables for Azure private peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

<span data-ttu-id="23272-138">A continuación, se muestra el resultado de ejemplo de una de las rutas de acceso:</span><span class="sxs-lookup"><span data-stu-id="23272-138">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="23272-139">Tablas ARP para el emparejamiento público de Azure:</span><span class="sxs-lookup"><span data-stu-id="23272-139">ARP tables for Azure public peering:</span></span>
<span data-ttu-id="23272-140">El siguiente cmdlet proporciona las tablas ARP para el emparejamiento público de Azure:</span><span class="sxs-lookup"><span data-stu-id="23272-140">The following cmdlet provides the ARP tables for Azure public peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

<span data-ttu-id="23272-141">A continuación, se muestra el resultado de ejemplo de una de las rutas de acceso:</span><span class="sxs-lookup"><span data-stu-id="23272-141">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="23272-142">A continuación, se muestra el resultado de ejemplo de una de las rutas de acceso:</span><span class="sxs-lookup"><span data-stu-id="23272-142">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="23272-143">Tablas ARP para el emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="23272-143">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="23272-144">El siguiente cmdlet proporciona las tablas ARP para el emparejamiento de Microsoft:</span><span class="sxs-lookup"><span data-stu-id="23272-144">The following cmdlet provides the ARP tables for Microsoft peering:</span></span>

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


<span data-ttu-id="23272-145">A continuación se muestra el resultado de ejemplo de una de las rutas de acceso:</span><span class="sxs-lookup"><span data-stu-id="23272-145">Sample output is shown below for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-to-use-this-information"></a><span data-ttu-id="23272-146">Uso de esta información</span><span class="sxs-lookup"><span data-stu-id="23272-146">How to use this information</span></span>
<span data-ttu-id="23272-147">La tabla ARP de un emparejamiento se puede usar para validar la configuración y la conectividad de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="23272-147">The ARP table of a peering can be used to validate Layer 2 configuration and connectivity.</span></span> <span data-ttu-id="23272-148">En esta sección se proporciona información general sobre la apariencia de las tablas ARP en distintos escenarios.</span><span class="sxs-lookup"><span data-stu-id="23272-148">This section provides an overview of how ARP tables look in different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a><span data-ttu-id="23272-149">Tabla ARP cuando un circuito está en un estado operativo (esperado)</span><span class="sxs-lookup"><span data-stu-id="23272-149">ARP table when a circuit is in an operational (expected) state</span></span>
* <span data-ttu-id="23272-150">La tabla ARP tiene una entrada para el lado local con una dirección IP válida y la dirección MAC, y una entrada similar para el lado de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="23272-150">The ARP table has an entry for the on-premises side with a valid IP and MAC address, and a similar entry for the Microsoft side.</span></span>
* <span data-ttu-id="23272-151">El último octeto de la dirección IP local siempre será un número impar.</span><span class="sxs-lookup"><span data-stu-id="23272-151">The last octet of the on-premises IP address is always an odd number.</span></span>
* <span data-ttu-id="23272-152">El último octeto de la dirección IP de Microsoft siempre será un número par.</span><span class="sxs-lookup"><span data-stu-id="23272-152">The last octet of the Microsoft IP address is always an even number.</span></span>
* <span data-ttu-id="23272-153">La misma dirección MAC aparece en el lado de Microsoft para los tres emparejamientos (principales o secundarios).</span><span class="sxs-lookup"><span data-stu-id="23272-153">The same MAC address appears on the Microsoft side for all three peerings (primary/secondary).</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-the-connectivity-provider-side-has-problems"></a><span data-ttu-id="23272-154">Tabla ARP cuando es local o cuando el lado del proveedor de conectividad tiene problemas</span><span class="sxs-lookup"><span data-stu-id="23272-154">ARP table when it's on-premises or when the connectivity-provider side has problems</span></span>
 <span data-ttu-id="23272-155">Solo aparece una entrada en la tabla ARP.</span><span class="sxs-lookup"><span data-stu-id="23272-155">Only one entry appears in the ARP table.</span></span> <span data-ttu-id="23272-156">Muestra la asignación entre la dirección MAC y la dirección IP que se usa en el lado de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="23272-156">It shows the mapping between the MAC address and the IP address that's used on the Microsoft side.</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> <span data-ttu-id="23272-157">Si experimenta un problema como este, abra una solicitud de soporte con su proveedor de conectividad para resolverlo.</span><span class="sxs-lookup"><span data-stu-id="23272-157">If you experience an issue like this, open a support request with your connectivity provider to resolve it.</span></span>
> 
> 

### <a name="arp-table-when-the-microsoft-side-has-problems"></a><span data-ttu-id="23272-158">Tabla ARP cuando el lado de Microsoft tiene problemas</span><span class="sxs-lookup"><span data-stu-id="23272-158">ARP table when the Microsoft side has problems</span></span>
* <span data-ttu-id="23272-159">Cuando hay problemas en el lado de Microsoft, no verá una tabla ARP para un emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="23272-159">You will not see an ARP table shown for a peering if there are issues on the Microsoft side.</span></span>
* <span data-ttu-id="23272-160">Abra una solicitud de soporte con [Ayuda y soporte técnico de Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="23272-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="23272-161">Especifique que tiene un problema con la conectividad de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="23272-161">Specify that you have an issue with Layer 2 connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23272-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="23272-162">Next steps</span></span>
* <span data-ttu-id="23272-163">Validar las configuraciones de nivel 3 para el circuito ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="23272-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span></span>
  * <span data-ttu-id="23272-164">Obtenga un resumen de ruta para determinar el estado de las sesiones BGP.</span><span class="sxs-lookup"><span data-stu-id="23272-164">Get a route summary to determine the state of BGP sessions.</span></span>
  * <span data-ttu-id="23272-165">Obtenga una tabla de rutas para determinar qué prefijos se anuncian a través de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="23272-165">Get a route table to determine which prefixes are advertised across ExpressRoute.</span></span>
* <span data-ttu-id="23272-166">Validar la transferencia de datos revisando los bytes de entrada y de salida.</span><span class="sxs-lookup"><span data-stu-id="23272-166">Validate data transfer by reviewing bytes in and out.</span></span>
* <span data-ttu-id="23272-167">Si sigue teniendo problemas, abra una solicitud de soporte técnico en [Ayuda y soporte técnico de Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) .</span><span class="sxs-lookup"><span data-stu-id="23272-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

