---
title: "Ejemplos de configuración de enrutadores de cliente ExpressRoute | Microsoft Docs"
description: "Esta página ofrece ejemplos de configuración de enrutador para enrutadores Cisco y Juniper."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 564826bc-017a-4683-a385-37c9fa814948
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: 032e584dc5abf59e9e3e8d80673b402f1fbf721b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="router-configuration-samples-to-set-up-and-manage-routing"></a><span data-ttu-id="34741-103">Ejemplos de configuración de enrutadores para configurar y administrar enrutamiento</span><span class="sxs-lookup"><span data-stu-id="34741-103">Router configuration samples to set up and manage routing</span></span>
<span data-ttu-id="34741-104">Esta página ofrece ejemplos de configuración de enrutamiento e interfaces para enrutadores Cisco serie IOS-XE y Juniper serie MX.</span><span class="sxs-lookup"><span data-stu-id="34741-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span></span> <span data-ttu-id="34741-105">Solo pretenden ser ejemplos de carácter informativo y no se deben usar tal cual.</span><span class="sxs-lookup"><span data-stu-id="34741-105">These are intended to be samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="34741-106">Puede trabajar con el proveedor para elaborar las configuraciones adecuadas para la red.</span><span class="sxs-lookup"><span data-stu-id="34741-106">You can work with your vendor to come up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="34741-107">Los ejemplos de esta página pretenden tener un carácter meramente informativo.</span><span class="sxs-lookup"><span data-stu-id="34741-107">Samples in this page are intended to be purely for guidance.</span></span> <span data-ttu-id="34741-108">Debe trabajar con los equipos técnico y de ventas del proveedor y su equipo de red para elaborar las configuraciones adecuadas que satisfagan sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="34741-108">You must work with your vendor's sales / technical team and your networking team to come up with appropriate configurations to meet your needs.</span></span> <span data-ttu-id="34741-109">Microsoft no dará soporte técnico en problemas relacionados con las configuraciones que aparecen en esta página.</span><span class="sxs-lookup"><span data-stu-id="34741-109">Microsoft will not support issues related to configurations listed in this page.</span></span> <span data-ttu-id="34741-110">Debe ponerse en contacto con el fabricante del dispositivo para problemas de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="34741-110">You must contact your device vendor for support issues.</span></span>
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a><span data-ttu-id="34741-111">Configuración de MSS de MTU y TCP en las interfaces de enrutador</span><span class="sxs-lookup"><span data-stu-id="34741-111">MTU and TCP MSS settings on router interfaces</span></span>
* <span data-ttu-id="34741-112">La MTU de la interfaz de ExpressRoute es 1500, que es la MTU predeterminada típica de una interfaz Ethernet en un enrutador.</span><span class="sxs-lookup"><span data-stu-id="34741-112">The MTU for the ExpressRoute interface is 1500, which is the typical default MTU for an Ethernet interface on a router.</span></span> <span data-ttu-id="34741-113">A menos que el enrutador tenga una MTU diferente de forma predeterminada, no es necesario especificar un valor en la interfaz del enrutador.</span><span class="sxs-lookup"><span data-stu-id="34741-113">Unless your router has a different MTU by default, there is no need to specify a value on the router interface.</span></span>
* <span data-ttu-id="34741-114">A diferencia de Azure VPN Gateway, no es necesario especificar el MSS de TCP para un circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="34741-114">Unlike an Azure VPN Gateway, the TCP MSS for an ExpressRoute circuit does not need to be specified.</span></span>

<span data-ttu-id="34741-115">Los ejemplos de configuración de enrutadores siguientes se aplican a todos los emparejamientos.</span><span class="sxs-lookup"><span data-stu-id="34741-115">Router configuration samples below apply to all peerings.</span></span> <span data-ttu-id="34741-116">Si desea más información, vea [Emparejamientos de ExpressRoute](expressroute-circuit-peerings.md) y [Requisitos de NAT de ExpressRoute](expressroute-routing.md).</span><span class="sxs-lookup"><span data-stu-id="34741-116">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span></span>


## <a name="cisco-ios-xe-based-routers"></a><span data-ttu-id="34741-117">Enrutadores basados en Cisco IOS-XE</span><span class="sxs-lookup"><span data-stu-id="34741-117">Cisco IOS-XE based routers</span></span>
<span data-ttu-id="34741-118">Los ejemplos en esta sección se aplican a cualquier enrutador que ejecute la familia del SO IOS-XE.</span><span class="sxs-lookup"><span data-stu-id="34741-118">The samples in this section apply for any router running the IOS-XE OS family.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="34741-119">1. Configuración de interfaces y subinterfaces</span><span class="sxs-lookup"><span data-stu-id="34741-119">1. Configuring interfaces and sub-interfaces</span></span>
<span data-ttu-id="34741-120">Necesitará una subinterfaz por emparejamiento en cada enrutador que conecte a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="34741-120">You will require a sub interface per peering in every router you connect to Microsoft.</span></span> <span data-ttu-id="34741-121">Una subinterfaz puede identificarse con un identificador de VLAN o un par apilado de identificadores de VLAN y una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="34741-121">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span></span>

<span data-ttu-id="34741-122">**Definición de interfaz Dot1Q**</span><span class="sxs-lookup"><span data-stu-id="34741-122">**Dot1Q interface definition**</span></span>

<span data-ttu-id="34741-123">Este ejemplo ofrece la definición de subinterfaz de una subinterfaz con un solo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="34741-123">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="34741-124">El identificador de VLAN es único para cada emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="34741-124">The VLAN ID is unique per peering.</span></span> <span data-ttu-id="34741-125">El último octeto de la dirección IPv4 siempre será un número impar.</span><span class="sxs-lookup"><span data-stu-id="34741-125">The last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

<span data-ttu-id="34741-126">**Definición de interfaz QinQ**</span><span class="sxs-lookup"><span data-stu-id="34741-126">**QinQ interface definition**</span></span>

<span data-ttu-id="34741-127">Este ejemplo ofrece la definición de subinterfaz de una subinterfaz con dos identificadores de VLAN.</span><span class="sxs-lookup"><span data-stu-id="34741-127">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="34741-128">El identificador de VLAN externo (s-tag), si se usa, es el mismo en todos los emparejamientos.</span><span class="sxs-lookup"><span data-stu-id="34741-128">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span></span> <span data-ttu-id="34741-129">El identificador de VLAN interno (c-tag) es único para cada emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="34741-129">The inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="34741-130">El último octeto de la dirección IPv4 siempre será un número impar.</span><span class="sxs-lookup"><span data-stu-id="34741-130">The last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="34741-131">2. Configuración de sesiones eBGP</span><span class="sxs-lookup"><span data-stu-id="34741-131">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="34741-132">Debe configurar una sesión BGP con Microsoft para cada emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="34741-132">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="34741-133">En el siguiente ejemplo permite configurar una sesión BGP con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="34741-133">The sample below enables you to setup a BGP session with Microsoft.</span></span> <span data-ttu-id="34741-134">Si la dirección IPv4 usada para la subinterfaz fue a.b.c.d, la dirección IP del vecino BGP (Microsoft) será a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="34741-134">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="34741-135">El último octeto de la dirección IPv4 del vecino BGP siempre será un número par.</span><span class="sxs-lookup"><span data-stu-id="34741-135">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-to-be-advertised-over-the-bgp-session"></a><span data-ttu-id="34741-136">3. Configuración de prefijos para anunciarse a través de la sesión BGP</span><span class="sxs-lookup"><span data-stu-id="34741-136">3. Setting up prefixes to be advertised over the BGP session</span></span>
<span data-ttu-id="34741-137">Puede configurar el enrutador para anunciar prefijos seleccionados a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="34741-137">You can configure your router to advertise select prefixes to Microsoft.</span></span> <span data-ttu-id="34741-138">Puede hacerlo usando el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="34741-138">You can do so using the sample below.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a><span data-ttu-id="34741-139">4. Asignaciones de ruta</span><span class="sxs-lookup"><span data-stu-id="34741-139">4. Route maps</span></span>
<span data-ttu-id="34741-140">Puede usar asignaciones de ruta y listas de prefijo para filtrar prefijos propagados en la red.</span><span class="sxs-lookup"><span data-stu-id="34741-140">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span></span> <span data-ttu-id="34741-141">Puede usar el ejemplo siguiente para realizar la tarea.</span><span class="sxs-lookup"><span data-stu-id="34741-141">You can use the sample below to accomplish the task.</span></span> <span data-ttu-id="34741-142">Asegúrese de que tiene el programa de instalación de listas de prefijos adecuado.</span><span class="sxs-lookup"><span data-stu-id="34741-142">Ensure that you have appropriate prefix lists setup.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
      neighbor <IP#2_used_by_Azure> route-map <MS_Prefixes_Inbound> in
     exit-address-family
    !
    route-map <MS_Prefixes_Inbound> permit 10
     match ip address prefix-list <MS_Prefixes>
    !


## <a name="juniper-mx-series-routers"></a><span data-ttu-id="34741-143">Enrutadores Juniper serie MX</span><span class="sxs-lookup"><span data-stu-id="34741-143">Juniper MX series routers</span></span>
<span data-ttu-id="34741-144">Los ejemplos en esta sección se aplican a los enrutadores Juniper serie MX.</span><span class="sxs-lookup"><span data-stu-id="34741-144">The samples in this section apply for any Juniper MX series routers.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="34741-145">1. Configuración de interfaces y subinterfaces</span><span class="sxs-lookup"><span data-stu-id="34741-145">1. Configuring interfaces and sub-interfaces</span></span>

<span data-ttu-id="34741-146">**Definición de interfaz Dot1Q**</span><span class="sxs-lookup"><span data-stu-id="34741-146">**Dot1Q interface definition**</span></span>

<span data-ttu-id="34741-147">Este ejemplo ofrece la definición de subinterfaz de una subinterfaz con un solo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="34741-147">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="34741-148">El identificador de VLAN es único para cada emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="34741-148">The VLAN ID is unique per peering.</span></span> <span data-ttu-id="34741-149">El último octeto de la dirección IPv4 siempre será un número impar.</span><span class="sxs-lookup"><span data-stu-id="34741-149">The last octet of your IPv4 address will always be an odd number.</span></span>

    interfaces {
        vlan-tagging;
        <Interface_Number> {
            unit <Number> {
                vlan-id <VLAN_ID>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }
            }
        }
    }


<span data-ttu-id="34741-150">**Definición de interfaz QinQ**</span><span class="sxs-lookup"><span data-stu-id="34741-150">**QinQ interface definition**</span></span>

<span data-ttu-id="34741-151">Este ejemplo ofrece la definición de subinterfaz de una subinterfaz con dos identificadores de VLAN.</span><span class="sxs-lookup"><span data-stu-id="34741-151">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="34741-152">El identificador de VLAN externo (s-tag), si se usa, es el mismo en todos los emparejamientos.</span><span class="sxs-lookup"><span data-stu-id="34741-152">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span></span> <span data-ttu-id="34741-153">El identificador de VLAN interno (c-tag) es único para cada emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="34741-153">The inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="34741-154">El último octeto de la dirección IPv4 siempre será un número impar.</span><span class="sxs-lookup"><span data-stu-id="34741-154">The last octet of your IPv4 address will always be an odd number.</span></span>

    interfaces {
        <Interface_Number> {
            flexible-vlan-tagging;
            unit <Number> {
                vlan-tags outer <S-tag> inner <C-tag>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }                           
            }                               
        }                                   
    }                           

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="34741-155">2. Configuración de sesiones eBGP</span><span class="sxs-lookup"><span data-stu-id="34741-155">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="34741-156">Debe configurar una sesión BGP con Microsoft para cada emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="34741-156">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="34741-157">En el siguiente ejemplo permite configurar una sesión BGP con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="34741-157">The sample below enables you to setup a BGP session with Microsoft.</span></span> <span data-ttu-id="34741-158">Si la dirección IPv4 usada para la subinterfaz fue a.b.c.d, la dirección IP del vecino BGP (Microsoft) será a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="34741-158">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="34741-159">El último octeto de la dirección IPv4 del vecino BGP siempre será un número par.</span><span class="sxs-lookup"><span data-stu-id="34741-159">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span></span>

    routing-options {
        autonomous-system <Customer_ASN>;
    }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

### <a name="3-setting-up-prefixes-to-be-advertised-over-the-bgp-session"></a><span data-ttu-id="34741-160">3. Configuración de prefijos para anunciarse a través de la sesión BGP</span><span class="sxs-lookup"><span data-stu-id="34741-160">3. Setting up prefixes to be advertised over the BGP session</span></span>
<span data-ttu-id="34741-161">Puede configurar el enrutador para anunciar prefijos seleccionados a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="34741-161">You can configure your router to advertise select prefixes to Microsoft.</span></span> <span data-ttu-id="34741-162">Puede hacerlo usando el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="34741-162">You can do so using the sample below.</span></span>

    policy-options {
        policy-statement <Policy_Name> {
            term 1 {
                from protocol OSPF;
        route-filter <Prefix_to_be_advertised/Subnet_Mask> exact;
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }


### <a name="4-route-maps"></a><span data-ttu-id="34741-163">4. Asignaciones de ruta</span><span class="sxs-lookup"><span data-stu-id="34741-163">4. Route maps</span></span>
<span data-ttu-id="34741-164">Puede usar asignaciones de ruta y listas de prefijo para filtrar prefijos propagados en la red.</span><span class="sxs-lookup"><span data-stu-id="34741-164">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span></span> <span data-ttu-id="34741-165">Puede usar el ejemplo siguiente para realizar la tarea.</span><span class="sxs-lookup"><span data-stu-id="34741-165">You can use the sample below to accomplish the task.</span></span> <span data-ttu-id="34741-166">Asegúrese de que tiene el programa de instalación de listas de prefijos adecuado.</span><span class="sxs-lookup"><span data-stu-id="34741-166">Ensure that you have appropriate prefix lists setup.</span></span>

    policy-options {
        prefix-list MS_Prefixes {
            <IP_Prefix_1/Subnet_Mask>;
            <IP_Prefix_2/Subnet_Mask>;
        }
        policy-statement <MS_Prefixes_Inbound> {
            term 1 {
                from {
        prefix-list MS_Prefixes;
                }
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                import <MS_Prefixes_Inbound>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

## <a name="next-steps"></a><span data-ttu-id="34741-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="34741-167">Next Steps</span></span>
<span data-ttu-id="34741-168">Consulte [P+F de ExpressRoute](expressroute-faqs.md) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="34741-168">See the [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

