---
title: "Obtención de tablas ARP: Resource Manager: Solución de problemas de Azure ExpressRoute | Microsoft Docs"
description: "Esta página proporciona instrucciones sobre la obtención Hola ARP tablas por un circuito ExpressRoute"
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
ms.openlocfilehash: c386b031814d40ef6ea3ce5e0eaaab9634470e8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-resource-manager-deployment-model"></a><span data-ttu-id="06330-103">Obtener tablas de ARP en el modelo de implementación del Administrador de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="06330-103">Getting ARP tables in hello Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="06330-104">PowerShell: administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="06330-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="06330-105">PowerShell: clásico</span><span class="sxs-lookup"><span data-stu-id="06330-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="06330-106">Este artículo le guiará a través de Hola Hola de toolearn pasos que ARP tablas para el circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="06330-106">This article walks you through hello steps toolearn hello ARP tables for your ExpressRoute circuit.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="06330-107">Este documento está previsto toohelp diagnosticar y corregir problemas sencillos.</span><span class="sxs-lookup"><span data-stu-id="06330-107">This document is intended toohelp you diagnose and fix simple issues.</span></span> <span data-ttu-id="06330-108">No está previsto toobe un sustituto de soporte técnico de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="06330-108">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="06330-109">Debe abrir una incidencia de soporte técnico con [soporte técnico de Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) si es un problema de hello toosolve no se puede utilizar la Guía de Hola se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="06330-109">You must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are unable toosolve hello problem using hello guidance described below.</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="06330-110">Protocolo de resolución de direcciones (ARP) y tablas ARP</span><span class="sxs-lookup"><span data-stu-id="06330-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="06330-111">El Protocolo de resolución de direcciones (ARP) es un protocolo de nivel 2 definido en [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="06330-111">Address Resolution Protocol (ARP) is a layer 2 protocol defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="06330-112">ARP es hello toomap usa la dirección Ethernet (dirección MAC) con una dirección ip.</span><span class="sxs-lookup"><span data-stu-id="06330-112">ARP is used toomap hello Ethernet address (MAC address) with an ip address.</span></span>

<span data-ttu-id="06330-113">Hola tabla ARP proporciona una asignación de dirección ipv4 de Hola y dirección MAC para un emparejamiento determinado.</span><span class="sxs-lookup"><span data-stu-id="06330-113">hello ARP table provides a mapping of hello ipv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="06330-114">Hola tabla ARP de un circuito de ExpressRoute emparejamiento proporciona Hola siguiente información para cada interfaz (principal y secundaria)</span><span class="sxs-lookup"><span data-stu-id="06330-114">hello ARP table for an ExpressRoute circuit peering provides hello following information for each interface (primary and secondary)</span></span>

1. <span data-ttu-id="06330-115">Asignación de dirección de MAC toohello dirección de ip de la interfaz de enrutador de locales</span><span class="sxs-lookup"><span data-stu-id="06330-115">Mapping of on-premises router interface ip address toohello MAC address</span></span>
2. <span data-ttu-id="06330-116">Asignación de dirección de MAC toohello dirección de ip de la interfaz de enrutador de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="06330-116">Mapping of ExpressRoute router interface ip address toohello MAC address</span></span>
3. <span data-ttu-id="06330-117">Antigüedad de asignación de Hola</span><span class="sxs-lookup"><span data-stu-id="06330-117">Age of hello mapping</span></span>

<span data-ttu-id="06330-118">Las tablas ARP pueden ayudar a validar la configuración de nivel 2 y a solucionar los problemas básicos de conectividad de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="06330-118">ARP tables can help validate layer 2 configuration and troubleshooting basic layer 2 connectivity issues.</span></span> 

<span data-ttu-id="06330-119">Ejemplo de tabla ARP:</span><span class="sxs-lookup"><span data-stu-id="06330-119">Example ARP table:</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


<span data-ttu-id="06330-120">Hello siguiente sección proporciona información sobre cómo puede ver Hola tablas ARP vistas por enrutadores de borde de ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="06330-120">hello following section provides information on how you can view hello ARP tables seen by hello ExpressRoute edge routers.</span></span> 

## <a name="prerequisites-for-learning-arp-tables"></a><span data-ttu-id="06330-121">Requisitos previos para comprender las tablas ARP</span><span class="sxs-lookup"><span data-stu-id="06330-121">Prerequisites for learning ARP tables</span></span>
<span data-ttu-id="06330-122">Asegúrese de que tiene Hola siguientes antes de que avanza más</span><span class="sxs-lookup"><span data-stu-id="06330-122">Ensure that you have hello following before you progress further</span></span>

* <span data-ttu-id="06330-123">Un circuito ExpressRoute válido configurado con al menos un emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="06330-123">A Valid ExpressRoute circuit configured with at least one peering.</span></span> <span data-ttu-id="06330-124">circuito Hola debe configurarse totalmente por el proveedor de conectividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="06330-124">hello circuit must be fully configured by hello connectivity provider.</span></span> <span data-ttu-id="06330-125">Usted (o el proveedor de conectividad) debe haber configurado al menos uno de los emparejamientos de hello (público privado y Azure, Azure y Microsoft) en este circuito.</span><span class="sxs-lookup"><span data-stu-id="06330-125">You (or your connectivity provider) must have configured at least one of hello peerings (Azure private, Azure public and Microsoft) on this circuit.</span></span>
* <span data-ttu-id="06330-126">Intervalos de direcciones IP que se usa para configurar los emparejamientos de hello (público privado y Azure, Azure y Microsoft).</span><span class="sxs-lookup"><span data-stu-id="06330-126">IP address ranges used for configuring hello peerings (Azure private, Azure public and Microsoft).</span></span> <span data-ttu-id="06330-127">Revisar ejemplos de asignación de direcciones de ip de Hola Hola [página requisitos de enrutamiento de ExpressRoute](expressroute-routing.md) tooget una descripción de cómo son las direcciones ip asignado toointerfaces en su lado y en hello lado de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="06330-127">Review hello ip address assignment examples in hello [ExpressRoute routing requirements page](expressroute-routing.md) tooget an understanding of how ip addresses are mapped toointerfaces on your side and on hello ExpressRoute side.</span></span> <span data-ttu-id="06330-128">Puede obtener información sobre la configuración de emparejamiento de hello revisando hello [página de configuración de emparejamiento de ExpressRoute](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="06330-128">You can get information on hello peering configuration by reviewing hello [ExpressRoute peering configuration page](expressroute-howto-routing-arm.md).</span></span>
* <span data-ttu-id="06330-129">Información del equipo de red de / proveedor de conectividad en direcciones MAC de Hola de interfaces que se utiliza con estas direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="06330-129">Information from your networking team / connectivity provider on hello MAC addresses of interfaces used with these IP addresses.</span></span>
* <span data-ttu-id="06330-130">Debe tener el módulo más reciente de PowerShell de Hola de Azure (versión 1,50 u otra más reciente).</span><span class="sxs-lookup"><span data-stu-id="06330-130">You must have hello latest PowerShell module for Azure (version 1.50 or newer).</span></span>

## <a name="getting-hello-arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="06330-131">Hola ARP la obtención de tablas para el circuito de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="06330-131">Getting hello ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="06330-132">Esta sección proporciona instrucciones sobre cómo puede ver Hola tablas de ARP por emparejamiento mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06330-132">This section provides instructions on how you can view hello ARP tables per peering using PowerShell.</span></span> <span data-ttu-id="06330-133">Usted o su proveedor de conectividad debe haber configurado Hola emparejamiento antes de ir aún más.</span><span class="sxs-lookup"><span data-stu-id="06330-133">You or your connectivity provider must have configured hello peering before progressing further.</span></span> <span data-ttu-id="06330-134">Cada circuito tiene dos rutas de acceso (principal y secundaria).</span><span class="sxs-lookup"><span data-stu-id="06330-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="06330-135">Puede comprobar Hola tabla ARP para cada ruta de acceso de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="06330-135">You can check hello ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="06330-136">Tablas ARP para el emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="06330-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="06330-137">Hola siguiente cmdlet proporciona Hola ARP tablas para el emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="06330-137">hello following cmdlet provides hello ARP tables for Azure private peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

<span data-ttu-id="06330-138">Resultados del ejemplo se muestran a continuación para una de las rutas de acceso de Hola</span><span class="sxs-lookup"><span data-stu-id="06330-138">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="06330-139">Tablas ARP para el emparejamiento público de Azure</span><span class="sxs-lookup"><span data-stu-id="06330-139">ARP tables for Azure public peering</span></span>
<span data-ttu-id="06330-140">Hola siguiente cmdlet proporciona tablas de hello ARP para pares públicos de Azure</span><span class="sxs-lookup"><span data-stu-id="06330-140">hello following cmdlet provides hello ARP tables for Azure public peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


<span data-ttu-id="06330-141">Resultados del ejemplo se muestran a continuación para una de las rutas de acceso de Hola</span><span class="sxs-lookup"><span data-stu-id="06330-141">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="06330-142">Tablas ARP para el emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="06330-142">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="06330-143">Hola siguiente cmdlet proporciona Hola ARP tablas para el emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="06330-143">hello following cmdlet provides hello ARP tables for Microsoft peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


<span data-ttu-id="06330-144">Resultados del ejemplo se muestran a continuación para una de las rutas de acceso de Hola</span><span class="sxs-lookup"><span data-stu-id="06330-144">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a><span data-ttu-id="06330-145">¿Cómo toouse esta información</span><span class="sxs-lookup"><span data-stu-id="06330-145">How toouse this information</span></span>
<span data-ttu-id="06330-146">Hello ARP de un emparejamiento se puede usar tabla toodetermine validar configuración de capa 2 y la conectividad.</span><span class="sxs-lookup"><span data-stu-id="06330-146">hello ARP table of a peering can be used toodetermine validate layer 2 configuration and connectivity.</span></span> <span data-ttu-id="06330-147">En esta sección se proporciona información general sobre la apariencia de las tablas ARP en distintos escenarios.</span><span class="sxs-lookup"><span data-stu-id="06330-147">This section provides an overview of how ARP tables will look under different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a><span data-ttu-id="06330-148">Tabla ARP cuando un circuito está en estado operativo (estado esperado)</span><span class="sxs-lookup"><span data-stu-id="06330-148">ARP table when a circuit is in operational state (expected state)</span></span>
* <span data-ttu-id="06330-149">Hola tabla ARP tendrá una entrada para el lado local de hello con una dirección IP válida y una dirección MAC y una entrada similar para hello side de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="06330-149">hello ARP table will have an entry for hello on-premises side with a valid IP address and MAC address and a similar entry for hello Microsoft side.</span></span> 
* <span data-ttu-id="06330-150">último octeto de Hola de dirección ip de hello local siempre será un número impar.</span><span class="sxs-lookup"><span data-stu-id="06330-150">hello last octet of hello on-premises ip address will always be an odd number.</span></span>
* <span data-ttu-id="06330-151">último octeto de Hola de hello dirección ip de Microsoft siempre será un número par.</span><span class="sxs-lookup"><span data-stu-id="06330-151">hello last octet of hello Microsoft ip address will always be an even number.</span></span>
* <span data-ttu-id="06330-152">Hola la misma dirección MAC aparecerán en hello lado de Microsoft para todos los emparejamientos de 3 (principales o secundarias).</span><span class="sxs-lookup"><span data-stu-id="06330-152">hello same MAC address will appear on hello Microsoft side for all 3 peerings (primary / secondary).</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a><span data-ttu-id="06330-153">Tabla ARP cuando el lado del proveedor de conectividad o local tiene problemas</span><span class="sxs-lookup"><span data-stu-id="06330-153">ARP table when on-premises / connectivity provider side has problems</span></span>
<span data-ttu-id="06330-154">Si hay problemas con hello local o proveedor de conectividad puede ver que cualquiera de las solo entradas aparecerán en hello ARP tabla u Hola local MAC dirección mostrará incompleta.</span><span class="sxs-lookup"><span data-stu-id="06330-154">If there are issues with hello on-premises or connectivity provider you may see that either only one entry will appear in hello ARP table or hello on-prem MAC address will show incomplete.</span></span> <span data-ttu-id="06330-155">Esto mostrará la asignación de Hola entre Hola dirección MAC y la dirección IP usada en hello side de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="06330-155">This will show hello mapping between hello MAC address and IP address used in hello Microsoft side.</span></span> 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

<span data-ttu-id="06330-156">o</span><span class="sxs-lookup"><span data-stu-id="06330-156">or</span></span>
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> <span data-ttu-id="06330-157">Abra una solicitud de soporte técnico con su toodebug de proveedor de conectividad tales problemas.</span><span class="sxs-lookup"><span data-stu-id="06330-157">Open a support request with your connectivity provider toodebug such issues.</span></span> <span data-ttu-id="06330-158">Si no dispone de hello tabla ARP direcciones IP de interfaces de hello asignan direcciones tooMAC, Hola revisión siguiente información:</span><span class="sxs-lookup"><span data-stu-id="06330-158">If hello ARP table does not have IP addresses of hello interfaces mapped tooMAC addresses, review hello following information:</span></span>
> 
> 1. <span data-ttu-id="06330-159">Si Hola primera asignará dirección IP de subred de hello /30 para hello vínculo entre Hola PR MSEE y MSEE se utiliza en la interfaz de Hola de MSEE de int</span><span class="sxs-lookup"><span data-stu-id="06330-159">If hello first IP address of hello /30 subnet assigned for hello link between hello MSEE-PR and MSEE is used on hello interface of MSEE-PR.</span></span> <span data-ttu-id="06330-160">Azure usa siempre la dirección IP de la segunda Hola para MSEEs.</span><span class="sxs-lookup"><span data-stu-id="06330-160">Azure always uses hello second IP address for MSEEs.</span></span>
> 2. <span data-ttu-id="06330-161">Compruebe si Hola cliente (C-Tag) y las etiquetas VLAN de servicio (S-Tag) coinciden con ambos en par MSEE PR y MSEE.</span><span class="sxs-lookup"><span data-stu-id="06330-161">Verify if hello customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a><span data-ttu-id="06330-162">Tabla ARP cuando el lado de Microsoft tiene problemas</span><span class="sxs-lookup"><span data-stu-id="06330-162">ARP table when Microsoft side has problems</span></span>
* <span data-ttu-id="06330-163">No verá una tabla de ARP que se muestra para un emparejamiento si hay problemas en hello side de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="06330-163">You will not see an ARP table shown for a peering if there are issues on hello Microsoft side.</span></span> 
* <span data-ttu-id="06330-164">Abra una incidencia de soporte técnico dirigida al [soporte técnico de Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="06330-164">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="06330-165">Especifique que tiene un problema con la conectividad de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="06330-165">Specify that you have an issue with layer 2 connectivity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="06330-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="06330-166">Next Steps</span></span>
* <span data-ttu-id="06330-167">Validar las configuraciones de nivel 3 para el circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="06330-167">Validate Layer 3 configurations for your ExpressRoute circuit</span></span>
  * <span data-ttu-id="06330-168">Obtener estado de hello toodetermine resumen de ruta de sesiones de BGP</span><span class="sxs-lookup"><span data-stu-id="06330-168">Get route summary toodetermine hello state of BGP sessions</span></span> 
  * <span data-ttu-id="06330-169">Obtener toodetermine de la tabla de ruta qué prefijos se anuncian a través de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="06330-169">Get route table toodetermine which prefixes are advertised across ExpressRoute</span></span>
* <span data-ttu-id="06330-170">Validar la transferencia de datos revisando los bytes de entrada y de salida</span><span class="sxs-lookup"><span data-stu-id="06330-170">Validate data transfer by reviewing bytes in / out</span></span>
* <span data-ttu-id="06330-171">Si sigue teniendo problemas, abra una incidencia de soporte técnico dirigida al [soporte técnico de Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) .</span><span class="sxs-lookup"><span data-stu-id="06330-171">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

