---
title: "Obtención de tablas ARP: Implementación clásica: Solución de problemas de Azure ExpressRoute | Microsoft Docs"
description: "Esta página proporciona instrucciones para obtener Hola ARP tablas por un circuito ExpressRoute."
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
ms.openlocfilehash: 2b01304a38fa0e0def27dbd7c391d7ad8bbdabff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-classic-deployment-model"></a><span data-ttu-id="f2371-103">Obtener tablas de ARP en el modelo de implementación clásica de Hola</span><span class="sxs-lookup"><span data-stu-id="f2371-103">Getting ARP tables in hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f2371-104">PowerShell: administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="f2371-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="f2371-105">PowerShell: clásico</span><span class="sxs-lookup"><span data-stu-id="f2371-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="f2371-106">En este artículo le guiará por los pasos de hello para la obtención de tablas de protocolo de resolución de direcciones (ARP) de hello para el circuito de ExpressRoute de Azure.</span><span class="sxs-lookup"><span data-stu-id="f2371-106">This article walks you through hello steps for getting hello Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2371-107">Este documento está previsto toohelp diagnosticar y corregir problemas sencillos.</span><span class="sxs-lookup"><span data-stu-id="f2371-107">This document is intended toohelp you diagnose and fix simple issues.</span></span> <span data-ttu-id="f2371-108">No está previsto toobe un sustituto de soporte técnico de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f2371-108">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="f2371-109">Si no puede resolver el problema de hello mediante el uso de instrucciones de hello, abra una solicitud de soporte técnico con [Microsoft Azure ayuda y soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="f2371-109">If you can't solve hello problem by using hello following guidance, open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="f2371-110">Protocolo de resolución de direcciones (ARP) y tablas ARP</span><span class="sxs-lookup"><span data-stu-id="f2371-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="f2371-111">ARP es un protocolo de nivel 2 que se define en [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="f2371-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="f2371-112">ARP es toomap usa una dirección IP de tooan de direcciones (dirección MAC) Ethernet.</span><span class="sxs-lookup"><span data-stu-id="f2371-112">ARP is used toomap an Ethernet address (MAC address) tooan IP address.</span></span>

<span data-ttu-id="f2371-113">Una tabla ARP proporciona una asignación de dirección IPv4 de Hola y dirección MAC para un emparejamiento determinado.</span><span class="sxs-lookup"><span data-stu-id="f2371-113">An ARP table provides a mapping of hello IPv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="f2371-114">Hola tabla ARP de un circuito de ExpressRoute emparejamiento proporciona Hola siguiente información para cada interfaz (principal y secundaria):</span><span class="sxs-lookup"><span data-stu-id="f2371-114">hello ARP table for an ExpressRoute circuit peering provides hello following information for each interface (primary and secondary):</span></span>

1. <span data-ttu-id="f2371-115">Asignación de una dirección local enrutador interfaz IP dirección tooa MAC</span><span class="sxs-lookup"><span data-stu-id="f2371-115">Mapping of an on-premises router interface IP address tooa MAC address</span></span>
2. <span data-ttu-id="f2371-116">Asignación de una ExpressRoute interfaz dirección IP del enrutador dirección tooa MAC</span><span class="sxs-lookup"><span data-stu-id="f2371-116">Mapping of an ExpressRoute router interface IP address tooa MAC address</span></span>
3. <span data-ttu-id="f2371-117">antigüedad de Hola de asignación de Hola</span><span class="sxs-lookup"><span data-stu-id="f2371-117">hello age of hello mapping</span></span>

<span data-ttu-id="f2371-118">Las tablas ARP pueden ayudar a validar la configuración de capa 2 y a solucionar los problemas básicos de conectividad de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="f2371-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span></span>

<span data-ttu-id="f2371-119">A continuación, se muestra un ejemplo de una tabla ARP:</span><span class="sxs-lookup"><span data-stu-id="f2371-119">Following is an example of an ARP table:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="f2371-120">Hola siguiente sección proporciona información acerca de cómo tooview Hola tablas de ARP que ven los enrutadores de borde de ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="f2371-120">hello following section provides information about how tooview hello ARP tables that are seen by hello ExpressRoute edge routers.</span></span>

## <a name="prerequisites-for-using-arp-tables"></a><span data-ttu-id="f2371-121">Requisitos previos para usar las tablas ARP</span><span class="sxs-lookup"><span data-stu-id="f2371-121">Prerequisites for using ARP tables</span></span>
<span data-ttu-id="f2371-122">Asegúrese de que tiene Hola siguientes antes de continuar:</span><span class="sxs-lookup"><span data-stu-id="f2371-122">Ensure that you have hello following before you continue:</span></span>

* <span data-ttu-id="f2371-123">Un circuito ExpressRoute válido configurado con al menos un emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="f2371-123">A valid ExpressRoute circuit that's configured with at least one peering.</span></span> <span data-ttu-id="f2371-124">circuito Hola debe configurarse totalmente por el proveedor de conectividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="f2371-124">hello circuit must be fully configured by hello connectivity provider.</span></span> <span data-ttu-id="f2371-125">Usted (o el proveedor de conectividad) debe configurar al menos uno de los emparejamientos de hello (Azure privada o Azure público o Microsoft) en este circuito.</span><span class="sxs-lookup"><span data-stu-id="f2371-125">You (or your connectivity provider) must configure at least one of hello peerings (Azure private, Azure public, or Microsoft) on this circuit.</span></span>
* <span data-ttu-id="f2371-126">Intervalos de direcciones IP que se usan para configurar los emparejamientos de hello (público privado y Azure, Azure y Microsoft).</span><span class="sxs-lookup"><span data-stu-id="f2371-126">IP address ranges that are used for configuring hello peerings (Azure private, Azure public, and Microsoft).</span></span> <span data-ttu-id="f2371-127">Revisar ejemplos de asignación de direcciones IP de Hola Hola [página requisitos de enrutamiento de ExpressRoute](expressroute-routing.md) tooget una descripción de cómo son las direcciones IP asignado toointerfaces en su aise y en el lado de ExpressRoute de Hola.</span><span class="sxs-lookup"><span data-stu-id="f2371-127">Review hello IP address assignment examples in hello [ExpressRoute routing requirements page](expressroute-routing.md) tooget an understanding of how IP addresses are mapped toointerfaces on your aise and on hello ExpressRoute side.</span></span> <span data-ttu-id="f2371-128">Para obtener información acerca de la configuración de emparejamiento de hello revisando hello [página de configuración de emparejamiento de ExpressRoute](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="f2371-128">You can get information about hello peering configuration by reviewing hello [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span></span>
* <span data-ttu-id="f2371-129">Información de su proveedor de equipo o conectividad de red acerca de las direcciones MAC de Hola de interfaces de Hola que se usan con estas direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="f2371-129">Information from your networking team or connectivity provider about hello MAC addresses of hello interfaces that are used with these IP addresses.</span></span>
* <span data-ttu-id="f2371-130">Hola módulo más reciente Windows PowerShell para Azure (versión 1.50 o posterior).</span><span class="sxs-lookup"><span data-stu-id="f2371-130">hello latest Windows PowerShell module for Azure (version 1.50 or later).</span></span>

## <a name="arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="f2371-131">Tablas ARP para el circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f2371-131">ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="f2371-132">Esta sección proporciona instrucciones sobre cómo tooview Hola ARP tablas para cada tipo de intercambio de tráfico mediante el uso de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2371-132">This section provides instructions about how tooview hello ARP tables for each type of peering by using PowerShell.</span></span> <span data-ttu-id="f2371-133">Antes de continuar, usted o el proveedor de conectividad debe tooconfigure Hola emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="f2371-133">Before you continue, either you or your connectivity provider needs tooconfigure hello peering.</span></span> <span data-ttu-id="f2371-134">Cada circuito tiene dos rutas de acceso (principal y secundaria).</span><span class="sxs-lookup"><span data-stu-id="f2371-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="f2371-135">Puede comprobar Hola tabla ARP para cada ruta de acceso de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="f2371-135">You can check hello ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="f2371-136">Tablas ARP para el emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="f2371-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="f2371-137">Hola siguiente cmdlet proporciona Hola ARP tablas para el emparejamiento privado Azure:</span><span class="sxs-lookup"><span data-stu-id="f2371-137">hello following cmdlet provides hello ARP tables for Azure private peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

<span data-ttu-id="f2371-138">Aquí te mostramos la salida de ejemplo para una de las rutas de acceso de hello:</span><span class="sxs-lookup"><span data-stu-id="f2371-138">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="f2371-139">Tablas ARP para el emparejamiento público de Azure:</span><span class="sxs-lookup"><span data-stu-id="f2371-139">ARP tables for Azure public peering:</span></span>
<span data-ttu-id="f2371-140">Hola siguiente cmdlet proporciona Hola ARP tablas para pares públicos de Azure:</span><span class="sxs-lookup"><span data-stu-id="f2371-140">hello following cmdlet provides hello ARP tables for Azure public peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

<span data-ttu-id="f2371-141">Aquí te mostramos la salida de ejemplo para una de las rutas de acceso de hello:</span><span class="sxs-lookup"><span data-stu-id="f2371-141">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="f2371-142">Aquí te mostramos la salida de ejemplo para una de las rutas de acceso de hello:</span><span class="sxs-lookup"><span data-stu-id="f2371-142">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="f2371-143">Tablas ARP para el emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="f2371-143">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="f2371-144">Hola siguiente cmdlet proporciona Hola ARP tablas para el emparejamiento de Microsoft:</span><span class="sxs-lookup"><span data-stu-id="f2371-144">hello following cmdlet provides hello ARP tables for Microsoft peering:</span></span>

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


<span data-ttu-id="f2371-145">Resultados del ejemplo se muestran a continuación para una de las rutas de acceso de hello:</span><span class="sxs-lookup"><span data-stu-id="f2371-145">Sample output is shown below for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a><span data-ttu-id="f2371-146">¿Cómo toouse esta información</span><span class="sxs-lookup"><span data-stu-id="f2371-146">How toouse this information</span></span>
<span data-ttu-id="f2371-147">Hola tabla ARP de un emparejamiento puede ser conectividad y la configuración de toovalidate usa capa 2.</span><span class="sxs-lookup"><span data-stu-id="f2371-147">hello ARP table of a peering can be used toovalidate Layer 2 configuration and connectivity.</span></span> <span data-ttu-id="f2371-148">En esta sección se proporciona información general sobre la apariencia de las tablas ARP en distintos escenarios.</span><span class="sxs-lookup"><span data-stu-id="f2371-148">This section provides an overview of how ARP tables look in different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a><span data-ttu-id="f2371-149">Tabla ARP cuando un circuito está en un estado operativo (esperado)</span><span class="sxs-lookup"><span data-stu-id="f2371-149">ARP table when a circuit is in an operational (expected) state</span></span>
* <span data-ttu-id="f2371-150">Hola tabla ARP tiene una entrada para el lado local de hello con una dirección IP y MAC válida y una entrada similar para hello side de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f2371-150">hello ARP table has an entry for hello on-premises side with a valid IP and MAC address, and a similar entry for hello Microsoft side.</span></span>
* <span data-ttu-id="f2371-151">último octeto de Hola de dirección IP de hello local siempre es un número impar.</span><span class="sxs-lookup"><span data-stu-id="f2371-151">hello last octet of hello on-premises IP address is always an odd number.</span></span>
* <span data-ttu-id="f2371-152">último octeto de Hola de hello dirección IP de Microsoft siempre es un número par.</span><span class="sxs-lookup"><span data-stu-id="f2371-152">hello last octet of hello Microsoft IP address is always an even number.</span></span>
* <span data-ttu-id="f2371-153">Hola la misma dirección MAC aparece en hello lado de Microsoft para todos los emparejamientos de tres (principal o secundario).</span><span class="sxs-lookup"><span data-stu-id="f2371-153">hello same MAC address appears on hello Microsoft side for all three peerings (primary/secondary).</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-hello-connectivity-provider-side-has-problems"></a><span data-ttu-id="f2371-154">Tabla de ARP cuando es local o al lado de proveedor de conectividad de hello tiene problemas</span><span class="sxs-lookup"><span data-stu-id="f2371-154">ARP table when it's on-premises or when hello connectivity-provider side has problems</span></span>
 <span data-ttu-id="f2371-155">Sólo una entrada aparece en la tabla ARP Hola.</span><span class="sxs-lookup"><span data-stu-id="f2371-155">Only one entry appears in hello ARP table.</span></span> <span data-ttu-id="f2371-156">Muestra la asignación de hello entre la dirección MAC de Hola y la dirección IP de Hola que se usa en hello side de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f2371-156">It shows hello mapping between hello MAC address and hello IP address that's used on hello Microsoft side.</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> <span data-ttu-id="f2371-157">Si experimenta un problema parecido a esto, abra un soporte solicitarla con su tooresolve de proveedor de conectividad.</span><span class="sxs-lookup"><span data-stu-id="f2371-157">If you experience an issue like this, open a support request with your connectivity provider tooresolve it.</span></span>
> 
> 

### <a name="arp-table-when-hello-microsoft-side-has-problems"></a><span data-ttu-id="f2371-158">Tabla de ARP cuando Hola side de Microsoft tiene problemas</span><span class="sxs-lookup"><span data-stu-id="f2371-158">ARP table when hello Microsoft side has problems</span></span>
* <span data-ttu-id="f2371-159">No verá una tabla de ARP que se muestra para un emparejamiento si hay problemas en hello side de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f2371-159">You will not see an ARP table shown for a peering if there are issues on hello Microsoft side.</span></span>
* <span data-ttu-id="f2371-160">Abra una solicitud de soporte con [Ayuda y soporte técnico de Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="f2371-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="f2371-161">Especifique que tiene un problema con la conectividad de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="f2371-161">Specify that you have an issue with Layer 2 connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2371-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f2371-162">Next steps</span></span>
* <span data-ttu-id="f2371-163">Validar las configuraciones de nivel 3 para el circuito ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="f2371-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span></span>
  * <span data-ttu-id="f2371-164">Obtiene un estado de Hola de ruta toodetermine resumen de sesiones de BGP.</span><span class="sxs-lookup"><span data-stu-id="f2371-164">Get a route summary toodetermine hello state of BGP sessions.</span></span>
  * <span data-ttu-id="f2371-165">Obtener un toodetermine de la tabla de ruta qué prefijos se anuncian a través de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f2371-165">Get a route table toodetermine which prefixes are advertised across ExpressRoute.</span></span>
* <span data-ttu-id="f2371-166">Validar la transferencia de datos revisando los bytes de entrada y de salida.</span><span class="sxs-lookup"><span data-stu-id="f2371-166">Validate data transfer by reviewing bytes in and out.</span></span>
* <span data-ttu-id="f2371-167">Si sigue teniendo problemas, abra una solicitud de soporte técnico en [Ayuda y soporte técnico de Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) .</span><span class="sxs-lookup"><span data-stu-id="f2371-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

