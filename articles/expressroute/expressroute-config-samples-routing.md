---
title: "ejemplos de configuración de enrutador de cliente aaaExpressRoute | Documentos de Microsoft"
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
ms.openlocfilehash: 5c91f24e6082e01c3e8df91b4fcfda46a6c29fa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="router-configuration-samples-tooset-up-and-manage-routing"></a><span data-ttu-id="2649b-103">Configuración del enrutador muestrea tooset seguridad y administrar el enrutamiento</span><span class="sxs-lookup"><span data-stu-id="2649b-103">Router configuration samples tooset up and manage routing</span></span>
<span data-ttu-id="2649b-104">Esta página ofrece ejemplos de configuración de enrutamiento e interfaces para enrutadores Cisco serie IOS-XE y Juniper serie MX.</span><span class="sxs-lookup"><span data-stu-id="2649b-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span></span> <span data-ttu-id="2649b-105">Estos son ejemplos de toobe previsto únicamente carácter informativo y no puede usar tal cual.</span><span class="sxs-lookup"><span data-stu-id="2649b-105">These are intended toobe samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="2649b-106">Puede trabajar con su proveedor toocome con configuraciones adecuadas para la red.</span><span class="sxs-lookup"><span data-stu-id="2649b-106">You can work with your vendor toocome up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2649b-107">Los ejemplos en esta página están toobe previsto puramente para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="2649b-107">Samples in this page are intended toobe purely for guidance.</span></span> <span data-ttu-id="2649b-108">Debe trabajar con el equipo de ventas / técnica de su proveedor y la red toocome equipo seguridad con configuraciones adecuadas toomeet sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="2649b-108">You must work with your vendor's sales / technical team and your networking team toocome up with appropriate configurations toomeet your needs.</span></span> <span data-ttu-id="2649b-109">Microsoft no admitirá problemas relacionados con tooconfigurations enumerados en esta página.</span><span class="sxs-lookup"><span data-stu-id="2649b-109">Microsoft will not support issues related tooconfigurations listed in this page.</span></span> <span data-ttu-id="2649b-110">Debe ponerse en contacto con el fabricante del dispositivo para problemas de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="2649b-110">You must contact your device vendor for support issues.</span></span>
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a><span data-ttu-id="2649b-111">Configuración de MSS de MTU y TCP en las interfaces de enrutador</span><span class="sxs-lookup"><span data-stu-id="2649b-111">MTU and TCP MSS settings on router interfaces</span></span>
* <span data-ttu-id="2649b-112">Hola MTU de interfaz de ExpressRoute de hello es 1500, que es Hola habitual MTU de una interfaz Ethernet en un enrutador.</span><span class="sxs-lookup"><span data-stu-id="2649b-112">hello MTU for hello ExpressRoute interface is 1500, which is hello typical default MTU for an Ethernet interface on a router.</span></span> <span data-ttu-id="2649b-113">A menos que el enrutador tenga una MTU diferentes de forma predeterminada, no es un valor sin necesidad de toospecify en la interfaz del enrutador Hola.</span><span class="sxs-lookup"><span data-stu-id="2649b-113">Unless your router has a different MTU by default, there is no need toospecify a value on hello router interface.</span></span>
* <span data-ttu-id="2649b-114">A diferencia de una puerta de enlace de VPN de Azure, hello MSS de TCP para un circuito de ExpressRoute no es necesario toobe especificado.</span><span class="sxs-lookup"><span data-stu-id="2649b-114">Unlike an Azure VPN Gateway, hello TCP MSS for an ExpressRoute circuit does not need toobe specified.</span></span>

<span data-ttu-id="2649b-115">Ejemplos de configuración de enrutador siguientes aplican tooall emparejamientos.</span><span class="sxs-lookup"><span data-stu-id="2649b-115">Router configuration samples below apply tooall peerings.</span></span> <span data-ttu-id="2649b-116">Si desea más información, vea [Emparejamientos de ExpressRoute](expressroute-circuit-peerings.md) y [Requisitos de NAT de ExpressRoute](expressroute-routing.md).</span><span class="sxs-lookup"><span data-stu-id="2649b-116">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span></span>


## <a name="cisco-ios-xe-based-routers"></a><span data-ttu-id="2649b-117">Enrutadores basados en Cisco IOS-XE</span><span class="sxs-lookup"><span data-stu-id="2649b-117">Cisco IOS-XE based routers</span></span>
<span data-ttu-id="2649b-118">ejemplos de Hello en esta sección se aplican para ningún enrutador ejecutan familia del sistema operativo IOS XE Hola.</span><span class="sxs-lookup"><span data-stu-id="2649b-118">hello samples in this section apply for any router running hello IOS-XE OS family.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="2649b-119">1. Configuración de interfaces y subinterfaces</span><span class="sxs-lookup"><span data-stu-id="2649b-119">1. Configuring interfaces and sub-interfaces</span></span>
<span data-ttu-id="2649b-120">Se requieren una interfaz sub por emparejamiento en cada enrutador conectar tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="2649b-120">You will require a sub interface per peering in every router you connect tooMicrosoft.</span></span> <span data-ttu-id="2649b-121">Una subinterfaz puede identificarse con un identificador de VLAN o un par apilado de identificadores de VLAN y una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="2649b-121">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span></span>

<span data-ttu-id="2649b-122">**Definición de interfaz Dot1Q**</span><span class="sxs-lookup"><span data-stu-id="2649b-122">**Dot1Q interface definition**</span></span>

<span data-ttu-id="2649b-123">Este ejemplo proporciona la definición de interfaz subcarpetas de Hola para una interfaz secundaria con un único identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="2649b-123">This sample provides hello sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="2649b-124">Hola Id. de VLAN es exclusivo para cada emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="2649b-124">hello VLAN ID is unique per peering.</span></span> <span data-ttu-id="2649b-125">último octeto de la dirección IPv4 de Hello siempre será un número impar.</span><span class="sxs-lookup"><span data-stu-id="2649b-125">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

<span data-ttu-id="2649b-126">**Definición de interfaz QinQ**</span><span class="sxs-lookup"><span data-stu-id="2649b-126">**QinQ interface definition**</span></span>

<span data-ttu-id="2649b-127">Este ejemplo proporciona la definición de interfaz subcarpetas de Hola para una interfaz subcarpetas con dos identificadores de VLAN.</span><span class="sxs-lookup"><span data-stu-id="2649b-127">This sample provides hello sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="2649b-128">Hola externa Id. de VLAN (s-etiqueta), si utiliza permanece igual Hola a través de todos los emparejamientos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2649b-128">hello outer VLAN ID (s-tag), if used remains hello same across all hello peerings.</span></span> <span data-ttu-id="2649b-129">interna de Hello Id. de VLAN (c-tag) es exclusivo para cada emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="2649b-129">hello inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="2649b-130">último octeto de la dirección IPv4 de Hello siempre será un número impar.</span><span class="sxs-lookup"><span data-stu-id="2649b-130">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="2649b-131">2. Configuración de sesiones eBGP</span><span class="sxs-lookup"><span data-stu-id="2649b-131">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="2649b-132">Debe configurar una sesión BGP con Microsoft para cada emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="2649b-132">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="2649b-133">ejemplo de Hola siguiente permite toosetup una sesión BGP con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2649b-133">hello sample below enables you toosetup a BGP session with Microsoft.</span></span> <span data-ttu-id="2649b-134">Si Hola dirección IPv4 que usan para la interfaz de sub era a.b.c.d, dirección IP de saludo del vecino BGP hello (Microsoft) será a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="2649b-134">If hello IPv4 address you used for your sub interface was a.b.c.d, hello IP address of hello BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="2649b-135">último octeto de Hola de dirección de IPv4 de vecino de hello BGP siempre será un número par.</span><span class="sxs-lookup"><span data-stu-id="2649b-135">hello last octet of hello BGP neighbor's IPv4 address will always be an even number.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a><span data-ttu-id="2649b-136">3. Configurar toobe de prefijos anunciados en la sesión BGP Hola</span><span class="sxs-lookup"><span data-stu-id="2649b-136">3. Setting up prefixes toobe advertised over hello BGP session</span></span>
<span data-ttu-id="2649b-137">Puede configurar su tooMicrosoft de enrutador tooadvertise seleccione prefijos.</span><span class="sxs-lookup"><span data-stu-id="2649b-137">You can configure your router tooadvertise select prefixes tooMicrosoft.</span></span> <span data-ttu-id="2649b-138">Puede hacerlo utilizando Hola el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="2649b-138">You can do so using hello sample below.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a><span data-ttu-id="2649b-139">4. Asignaciones de ruta</span><span class="sxs-lookup"><span data-stu-id="2649b-139">4. Route maps</span></span>
<span data-ttu-id="2649b-140">Puede usar las asignaciones de ruta y prefijo enumera los prefijos de toofilter que se propague a la red.</span><span class="sxs-lookup"><span data-stu-id="2649b-140">You can use route-maps and prefix lists toofilter prefixes propagated into your network.</span></span> <span data-ttu-id="2649b-141">Puede usar el ejemplo de Hola por debajo de la tarea de hello tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="2649b-141">You can use hello sample below tooaccomplish hello task.</span></span> <span data-ttu-id="2649b-142">Asegúrese de que tiene el programa de instalación de listas de prefijos adecuado.</span><span class="sxs-lookup"><span data-stu-id="2649b-142">Ensure that you have appropriate prefix lists setup.</span></span>

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


## <a name="juniper-mx-series-routers"></a><span data-ttu-id="2649b-143">Enrutadores Juniper serie MX</span><span class="sxs-lookup"><span data-stu-id="2649b-143">Juniper MX series routers</span></span>
<span data-ttu-id="2649b-144">ejemplos de Hello en esta sección se aplican para los enrutadores de la serie Juniper MX.</span><span class="sxs-lookup"><span data-stu-id="2649b-144">hello samples in this section apply for any Juniper MX series routers.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="2649b-145">1. Configuración de interfaces y subinterfaces</span><span class="sxs-lookup"><span data-stu-id="2649b-145">1. Configuring interfaces and sub-interfaces</span></span>

<span data-ttu-id="2649b-146">**Definición de interfaz Dot1Q**</span><span class="sxs-lookup"><span data-stu-id="2649b-146">**Dot1Q interface definition**</span></span>

<span data-ttu-id="2649b-147">Este ejemplo proporciona la definición de interfaz subcarpetas de Hola para una interfaz secundaria con un único identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="2649b-147">This sample provides hello sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="2649b-148">Hola Id. de VLAN es exclusivo para cada emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="2649b-148">hello VLAN ID is unique per peering.</span></span> <span data-ttu-id="2649b-149">último octeto de la dirección IPv4 de Hello siempre será un número impar.</span><span class="sxs-lookup"><span data-stu-id="2649b-149">hello last octet of your IPv4 address will always be an odd number.</span></span>

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


<span data-ttu-id="2649b-150">**Definición de interfaz QinQ**</span><span class="sxs-lookup"><span data-stu-id="2649b-150">**QinQ interface definition**</span></span>

<span data-ttu-id="2649b-151">Este ejemplo proporciona la definición de interfaz subcarpetas de Hola para una interfaz subcarpetas con dos identificadores de VLAN.</span><span class="sxs-lookup"><span data-stu-id="2649b-151">This sample provides hello sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="2649b-152">Hola externa Id. de VLAN (s-etiqueta), si utiliza permanece igual Hola a través de todos los emparejamientos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2649b-152">hello outer VLAN ID (s-tag), if used remains hello same across all hello peerings.</span></span> <span data-ttu-id="2649b-153">interna de Hello Id. de VLAN (c-tag) es exclusivo para cada emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="2649b-153">hello inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="2649b-154">último octeto de la dirección IPv4 de Hello siempre será un número impar.</span><span class="sxs-lookup"><span data-stu-id="2649b-154">hello last octet of your IPv4 address will always be an odd number.</span></span>

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

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="2649b-155">2. Configuración de sesiones eBGP</span><span class="sxs-lookup"><span data-stu-id="2649b-155">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="2649b-156">Debe configurar una sesión BGP con Microsoft para cada emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="2649b-156">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="2649b-157">ejemplo de Hola siguiente permite toosetup una sesión BGP con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2649b-157">hello sample below enables you toosetup a BGP session with Microsoft.</span></span> <span data-ttu-id="2649b-158">Si Hola dirección IPv4 que usan para la interfaz de sub era a.b.c.d, dirección IP de saludo del vecino BGP hello (Microsoft) será a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="2649b-158">If hello IPv4 address you used for your sub interface was a.b.c.d, hello IP address of hello BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="2649b-159">último octeto de Hola de dirección de IPv4 de vecino de hello BGP siempre será un número par.</span><span class="sxs-lookup"><span data-stu-id="2649b-159">hello last octet of hello BGP neighbor's IPv4 address will always be an even number.</span></span>

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

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a><span data-ttu-id="2649b-160">3. Configurar toobe de prefijos anunciados en la sesión BGP Hola</span><span class="sxs-lookup"><span data-stu-id="2649b-160">3. Setting up prefixes toobe advertised over hello BGP session</span></span>
<span data-ttu-id="2649b-161">Puede configurar su tooMicrosoft de enrutador tooadvertise seleccione prefijos.</span><span class="sxs-lookup"><span data-stu-id="2649b-161">You can configure your router tooadvertise select prefixes tooMicrosoft.</span></span> <span data-ttu-id="2649b-162">Puede hacerlo utilizando Hola el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="2649b-162">You can do so using hello sample below.</span></span>

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


### <a name="4-route-maps"></a><span data-ttu-id="2649b-163">4. Asignaciones de ruta</span><span class="sxs-lookup"><span data-stu-id="2649b-163">4. Route maps</span></span>
<span data-ttu-id="2649b-164">Puede usar las asignaciones de ruta y prefijo enumera los prefijos de toofilter que se propague a la red.</span><span class="sxs-lookup"><span data-stu-id="2649b-164">You can use route-maps and prefix lists toofilter prefixes propagated into your network.</span></span> <span data-ttu-id="2649b-165">Puede usar el ejemplo de Hola por debajo de la tarea de hello tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="2649b-165">You can use hello sample below tooaccomplish hello task.</span></span> <span data-ttu-id="2649b-166">Asegúrese de que tiene el programa de instalación de listas de prefijos adecuado.</span><span class="sxs-lookup"><span data-stu-id="2649b-166">Ensure that you have appropriate prefix lists setup.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2649b-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2649b-167">Next Steps</span></span>
<span data-ttu-id="2649b-168">Vea hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="2649b-168">See hello [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

