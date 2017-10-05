---
title: "Obtención de tablas ARP: Resource Manager: Solución de problemas de Azure ExpressRoute | Microsoft Docs"
description: "En esta página se proporcionan instrucciones sobre cómo obtener tablas ARP para un circuito ExpressRoute"
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: 0a6bf1d5-6baf-44dd-87d3-1ebd2fd08bdc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: a65b1ba2998eae33b3e73bd2492fbbf025eb5946
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="getting-arp-tables-in-the-resource-manager-deployment-model"></a><span data-ttu-id="64bd4-103">Obtención de tablas ARP en el modelo de implementación de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="64bd4-103">Getting ARP tables in the Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="64bd4-104">PowerShell: administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="64bd4-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="64bd4-105">PowerShell: clásico</span><span class="sxs-lookup"><span data-stu-id="64bd4-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="64bd4-106">Este artículo le guía por los pasos necesarios para comprender las tablas ARP del circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="64bd4-106">This article walks you through the steps to learn the ARP tables for your ExpressRoute circuit.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="64bd4-107">Este documento está pensado para ayudarle a diagnosticar y corregir problemas sencillos.</span><span class="sxs-lookup"><span data-stu-id="64bd4-107">This document is intended to help you diagnose and fix simple issues.</span></span> <span data-ttu-id="64bd4-108">No pretende sustituir al soporte técnico de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="64bd4-108">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="64bd4-109">Si no puede resolver el problema siguiendo las instrucciones que se describen a continuación, abra una incidencia de soporte técnico dirigida al [soporte técnico de Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) .</span><span class="sxs-lookup"><span data-stu-id="64bd4-109">You must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are unable to solve the problem using the guidance described below.</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="64bd4-110">Protocolo de resolución de direcciones (ARP) y tablas ARP</span><span class="sxs-lookup"><span data-stu-id="64bd4-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="64bd4-111">El Protocolo de resolución de direcciones (ARP) es un protocolo de nivel 2 definido en [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="64bd4-111">Address Resolution Protocol (ARP) is a layer 2 protocol defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="64bd4-112">ARP se utiliza para asignar la dirección Ethernet (dirección MAC) con una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="64bd4-112">ARP is used to map the Ethernet address (MAC address) with an ip address.</span></span>

<span data-ttu-id="64bd4-113">La tabla ARP proporciona una asignación de la dirección IPv4 y la dirección MAC para un emparejamiento determinado.</span><span class="sxs-lookup"><span data-stu-id="64bd4-113">The ARP table provides a mapping of the ipv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="64bd4-114">La tabla ARP de un emparejamiento de circuito ExpressRoute proporciona la siguiente información para cada interfaz (principal y secundaria)</span><span class="sxs-lookup"><span data-stu-id="64bd4-114">The ARP table for an ExpressRoute circuit peering provides the following information for each interface (primary and secondary)</span></span>

1. <span data-ttu-id="64bd4-115">Asignación de la dirección IP de la interfaz del enrutador local a la dirección MAC</span><span class="sxs-lookup"><span data-stu-id="64bd4-115">Mapping of on-premises router interface ip address to the MAC address</span></span>
2. <span data-ttu-id="64bd4-116">Asignación de la dirección IP de la interfaz del enrutador de ExpressRoute a la dirección MAC</span><span class="sxs-lookup"><span data-stu-id="64bd4-116">Mapping of ExpressRoute router interface ip address to the MAC address</span></span>
3. <span data-ttu-id="64bd4-117">Antigüedad de la asignación</span><span class="sxs-lookup"><span data-stu-id="64bd4-117">Age of the mapping</span></span>

<span data-ttu-id="64bd4-118">Las tablas ARP pueden ayudar a validar la configuración de nivel 2 y a solucionar los problemas básicos de conectividad de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="64bd4-118">ARP tables can help validate layer 2 configuration and troubleshooting basic layer 2 connectivity issues.</span></span> 

<span data-ttu-id="64bd4-119">Ejemplo de tabla ARP:</span><span class="sxs-lookup"><span data-stu-id="64bd4-119">Example ARP table:</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


<span data-ttu-id="64bd4-120">En la siguiente sección se proporciona información sobre cómo puede ver las tablas ARP que ven los enrutadores de borde de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="64bd4-120">The following section provides information on how you can view the ARP tables seen by the ExpressRoute edge routers.</span></span> 

## <a name="prerequisites-for-learning-arp-tables"></a><span data-ttu-id="64bd4-121">Requisitos previos para comprender las tablas ARP</span><span class="sxs-lookup"><span data-stu-id="64bd4-121">Prerequisites for learning ARP tables</span></span>
<span data-ttu-id="64bd4-122">Asegúrese de que cumple los siguientes requisitos previos antes de seguir adelante</span><span class="sxs-lookup"><span data-stu-id="64bd4-122">Ensure that you have the following before you progress further</span></span>

* <span data-ttu-id="64bd4-123">Un circuito ExpressRoute válido configurado con al menos un emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="64bd4-123">A Valid ExpressRoute circuit configured with at least one peering.</span></span> <span data-ttu-id="64bd4-124">El circuito debe estar completamente configurado por el proveedor de conectividad.</span><span class="sxs-lookup"><span data-stu-id="64bd4-124">The circuit must be fully configured by the connectivity provider.</span></span> <span data-ttu-id="64bd4-125">Usted (o su proveedor de conectividad) debe haber configurado al menos uno de los emparejamientos (privado de Azure, público de Azure y Microsoft) en este circuito.</span><span class="sxs-lookup"><span data-stu-id="64bd4-125">You (or your connectivity provider) must have configured at least one of the peerings (Azure private, Azure public and Microsoft) on this circuit.</span></span>
* <span data-ttu-id="64bd4-126">Intervalos de direcciones IP usados para configurar los emparejamientos (privado de Azure, público de Azure y Microsoft).</span><span class="sxs-lookup"><span data-stu-id="64bd4-126">IP address ranges used for configuring the peerings (Azure private, Azure public and Microsoft).</span></span> <span data-ttu-id="64bd4-127">Revise los ejemplos de asignación de dirección IP en [Requisitos de enrutamiento de ExpressRoute](expressroute-routing.md) para comprender cómo se asignan las direcciones IP a las interfaces en su sitio y el sitio de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="64bd4-127">Review the ip address assignment examples in the [ExpressRoute routing requirements page](expressroute-routing.md) to get an understanding of how ip addresses are mapped to interfaces on your side and on the ExpressRoute side.</span></span> <span data-ttu-id="64bd4-128">Puede obtener información sobre la configuración de emparejamiento en la página [Creación y modificación del enrutamiento de un circuito ExpressRoute](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="64bd4-128">You can get information on the peering configuration by reviewing the [ExpressRoute peering configuration page](expressroute-howto-routing-arm.md).</span></span>
* <span data-ttu-id="64bd4-129">Información del equipo de red o del proveedor de conectividad sobre las direcciones MAC de las interfaces usadas con estas direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="64bd4-129">Information from your networking team / connectivity provider on the MAC addresses of interfaces used with these IP addresses.</span></span>
* <span data-ttu-id="64bd4-130">Debe tener como mínimo el módulo más reciente de PowerShell para Azure (versión 1.50 o superior).</span><span class="sxs-lookup"><span data-stu-id="64bd4-130">You must have the latest PowerShell module for Azure (version 1.50 or newer).</span></span>

## <a name="getting-the-arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="64bd4-131">Obtención de las tablas ARP para el circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="64bd4-131">Getting the ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="64bd4-132">En esta sección se proporcionan instrucciones sobre cómo ver las tablas ARP por emparejamiento mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64bd4-132">This section provides instructions on how you can view the ARP tables per peering using PowerShell.</span></span> <span data-ttu-id="64bd4-133">Usted o su proveedor de conectividad deben haber configurado el emparejamiento antes de seguir adelante.</span><span class="sxs-lookup"><span data-stu-id="64bd4-133">You or your connectivity provider must have configured the peering before progressing further.</span></span> <span data-ttu-id="64bd4-134">Cada circuito tiene dos rutas de acceso (principal y secundaria).</span><span class="sxs-lookup"><span data-stu-id="64bd4-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="64bd4-135">Puede comprobar en la tabla ARP cada ruta de acceso de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="64bd4-135">You can check the ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="64bd4-136">Tablas ARP para el emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="64bd4-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="64bd4-137">El siguiente cmdlet proporciona el emparejamiento privado de Azure para las tablas ARP:</span><span class="sxs-lookup"><span data-stu-id="64bd4-137">The following cmdlet provides the ARP tables for Azure private peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

<span data-ttu-id="64bd4-138">A continuación se muestra el resultado de ejemplo de una de las rutas de acceso:</span><span class="sxs-lookup"><span data-stu-id="64bd4-138">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="64bd4-139">Tablas ARP para el emparejamiento público de Azure</span><span class="sxs-lookup"><span data-stu-id="64bd4-139">ARP tables for Azure public peering</span></span>
<span data-ttu-id="64bd4-140">El siguiente cmdlet proporciona las tablas ARP para el emparejamiento público de Azure:</span><span class="sxs-lookup"><span data-stu-id="64bd4-140">The following cmdlet provides the ARP tables for Azure public peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


<span data-ttu-id="64bd4-141">A continuación se muestra el resultado de ejemplo de una de las rutas de acceso:</span><span class="sxs-lookup"><span data-stu-id="64bd4-141">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="64bd4-142">Tablas ARP para el emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="64bd4-142">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="64bd4-143">El siguiente cmdlet proporciona las tablas ARP para el emparejamiento de Microsoft:</span><span class="sxs-lookup"><span data-stu-id="64bd4-143">The following cmdlet provides the ARP tables for Microsoft peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


<span data-ttu-id="64bd4-144">A continuación se muestra el resultado de ejemplo de una de las rutas de acceso:</span><span class="sxs-lookup"><span data-stu-id="64bd4-144">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-to-use-this-information"></a><span data-ttu-id="64bd4-145">Uso de esta información</span><span class="sxs-lookup"><span data-stu-id="64bd4-145">How to use this information</span></span>
<span data-ttu-id="64bd4-146">La tabla ARP de un emparejamiento se puede usar para determinar o validar la configuración y la conectividad de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="64bd4-146">The ARP table of a peering can be used to determine validate layer 2 configuration and connectivity.</span></span> <span data-ttu-id="64bd4-147">En esta sección se proporciona información general sobre la apariencia de las tablas ARP en distintos escenarios.</span><span class="sxs-lookup"><span data-stu-id="64bd4-147">This section provides an overview of how ARP tables will look under different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a><span data-ttu-id="64bd4-148">Tabla ARP cuando un circuito está en estado operativo (estado esperado)</span><span class="sxs-lookup"><span data-stu-id="64bd4-148">ARP table when a circuit is in operational state (expected state)</span></span>
* <span data-ttu-id="64bd4-149">La tabla ARP tendrá una entrada para el lado local con una dirección IP válida y la dirección MAC y una entrada similar para el lado de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="64bd4-149">The ARP table will have an entry for the on-premises side with a valid IP address and MAC address and a similar entry for the Microsoft side.</span></span> 
* <span data-ttu-id="64bd4-150">El último octeto de la dirección IP local siempre será un número impar.</span><span class="sxs-lookup"><span data-stu-id="64bd4-150">The last octet of the on-premises ip address will always be an odd number.</span></span>
* <span data-ttu-id="64bd4-151">El último octeto de la dirección IP de Microsoft siempre será un número par.</span><span class="sxs-lookup"><span data-stu-id="64bd4-151">The last octet of the Microsoft ip address will always be an even number.</span></span>
* <span data-ttu-id="64bd4-152">La misma dirección MAC aparecerá en el lado de Microsoft para los 3 emparejamientos (principales o secundarios).</span><span class="sxs-lookup"><span data-stu-id="64bd4-152">The same MAC address will appear on the Microsoft side for all 3 peerings (primary / secondary).</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a><span data-ttu-id="64bd4-153">Tabla ARP cuando el lado del proveedor de conectividad o local tiene problemas</span><span class="sxs-lookup"><span data-stu-id="64bd4-153">ARP table when on-premises / connectivity provider side has problems</span></span>
<span data-ttu-id="64bd4-154">Si hay problemas con el proveedor de conectividad o local, puede que vea que solo aparece una entrada en la tabla ARP o que la dirección MAC local se muestra incompleta.</span><span class="sxs-lookup"><span data-stu-id="64bd4-154">If there are issues with the on-premises or connectivity provider you may see that either only one entry will appear in the ARP table or the on-prem MAC address will show incomplete.</span></span> <span data-ttu-id="64bd4-155">En ella se mostrará la asignación entre la dirección MAC y la dirección IP usadas en el lado de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="64bd4-155">This will show the mapping between the MAC address and IP address used in the Microsoft side.</span></span> 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

<span data-ttu-id="64bd4-156">o</span><span class="sxs-lookup"><span data-stu-id="64bd4-156">or</span></span>
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> <span data-ttu-id="64bd4-157">Abra una solicitud de soporte técnico con su proveedor de conectividad para depurar tales problemas.</span><span class="sxs-lookup"><span data-stu-id="64bd4-157">Open a support request with your connectivity provider to debug such issues.</span></span> <span data-ttu-id="64bd4-158">Si la tabla ARP no tiene direcciones IP de las interfaces que se asignan a direcciones MAC, revise la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="64bd4-158">If the ARP table does not have IP addresses of the interfaces mapped to MAC addresses, review the following information:</span></span>
> 
> 1. <span data-ttu-id="64bd4-159">Si la primera dirección IP de la subred /30 asignada para el vínculo entre el MSEE-PR y MSEE se utiliza en la interfaz de MSEE-PR.</span><span class="sxs-lookup"><span data-stu-id="64bd4-159">If the first IP address of the /30 subnet assigned for the link between the MSEE-PR and MSEE is used on the interface of MSEE-PR.</span></span> <span data-ttu-id="64bd4-160">Azure usa siempre la segunda dirección IP para los MSEE.</span><span class="sxs-lookup"><span data-stu-id="64bd4-160">Azure always uses the second IP address for MSEEs.</span></span>
> 2. <span data-ttu-id="64bd4-161">Compruebe si las etiquetas VLAN de servicio (S-Tag) y el cliente (C-Tag) coinciden en el par MSEE PR y MSEE.</span><span class="sxs-lookup"><span data-stu-id="64bd4-161">Verify if the customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a><span data-ttu-id="64bd4-162">Tabla ARP cuando el lado de Microsoft tiene problemas</span><span class="sxs-lookup"><span data-stu-id="64bd4-162">ARP table when Microsoft side has problems</span></span>
* <span data-ttu-id="64bd4-163">Cuando hay problemas en el lado de Microsoft, no verá una tabla ARP para un emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="64bd4-163">You will not see an ARP table shown for a peering if there are issues on the Microsoft side.</span></span> 
* <span data-ttu-id="64bd4-164">Abra una incidencia de soporte técnico dirigida al [soporte técnico de Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="64bd4-164">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="64bd4-165">Especifique que tiene un problema con la conectividad de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="64bd4-165">Specify that you have an issue with layer 2 connectivity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="64bd4-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="64bd4-166">Next Steps</span></span>
* <span data-ttu-id="64bd4-167">Validar las configuraciones de nivel 3 para el circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="64bd4-167">Validate Layer 3 configurations for your ExpressRoute circuit</span></span>
  * <span data-ttu-id="64bd4-168">Obtener el resumen de ruta para determinar el estado de las sesiones BGP</span><span class="sxs-lookup"><span data-stu-id="64bd4-168">Get route summary to determine the state of BGP sessions</span></span> 
  * <span data-ttu-id="64bd4-169">Obtener la tabla de rutas para determinar qué prefijos se anuncian a través de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="64bd4-169">Get route table to determine which prefixes are advertised across ExpressRoute</span></span>
* <span data-ttu-id="64bd4-170">Validar la transferencia de datos revisando los bytes de entrada y de salida</span><span class="sxs-lookup"><span data-stu-id="64bd4-170">Validate data transfer by reviewing bytes in / out</span></span>
* <span data-ttu-id="64bd4-171">Si sigue teniendo problemas, abra una incidencia de soporte técnico dirigida al [soporte técnico de Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) .</span><span class="sxs-lookup"><span data-stu-id="64bd4-171">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

