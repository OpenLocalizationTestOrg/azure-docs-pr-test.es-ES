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
# <a name="router-configuration-samples-tooset-up-and-manage-routing"></a>Configuración del enrutador muestrea tooset seguridad y administrar el enrutamiento
Esta página ofrece ejemplos de configuración de enrutamiento e interfaces para enrutadores Cisco serie IOS-XE y Juniper serie MX. Estos son ejemplos de toobe previsto únicamente carácter informativo y no puede usar tal cual. Puede trabajar con su proveedor toocome con configuraciones adecuadas para la red. 

> [!IMPORTANT]
> Los ejemplos en esta página están toobe previsto puramente para obtener instrucciones. Debe trabajar con el equipo de ventas / técnica de su proveedor y la red toocome equipo seguridad con configuraciones adecuadas toomeet sus necesidades. Microsoft no admitirá problemas relacionados con tooconfigurations enumerados en esta página. Debe ponerse en contacto con el fabricante del dispositivo para problemas de soporte técnico.
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a>Configuración de MSS de MTU y TCP en las interfaces de enrutador
* Hola MTU de interfaz de ExpressRoute de hello es 1500, que es Hola habitual MTU de una interfaz Ethernet en un enrutador. A menos que el enrutador tenga una MTU diferentes de forma predeterminada, no es un valor sin necesidad de toospecify en la interfaz del enrutador Hola.
* A diferencia de una puerta de enlace de VPN de Azure, hello MSS de TCP para un circuito de ExpressRoute no es necesario toobe especificado.

Ejemplos de configuración de enrutador siguientes aplican tooall emparejamientos. Si desea más información, vea [Emparejamientos de ExpressRoute](expressroute-circuit-peerings.md) y [Requisitos de NAT de ExpressRoute](expressroute-routing.md).


## <a name="cisco-ios-xe-based-routers"></a>Enrutadores basados en Cisco IOS-XE
ejemplos de Hello en esta sección se aplican para ningún enrutador ejecutan familia del sistema operativo IOS XE Hola.

### <a name="1-configuring-interfaces-and-sub-interfaces"></a>1. Configuración de interfaces y subinterfaces
Se requieren una interfaz sub por emparejamiento en cada enrutador conectar tooMicrosoft. Una subinterfaz puede identificarse con un identificador de VLAN o un par apilado de identificadores de VLAN y una dirección IP.

**Definición de interfaz Dot1Q**

Este ejemplo proporciona la definición de interfaz subcarpetas de Hola para una interfaz secundaria con un único identificador de VLAN. Hola Id. de VLAN es exclusivo para cada emparejamiento. último octeto de la dirección IPv4 de Hello siempre será un número impar.

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

**Definición de interfaz QinQ**

Este ejemplo proporciona la definición de interfaz subcarpetas de Hola para una interfaz subcarpetas con dos identificadores de VLAN. Hola externa Id. de VLAN (s-etiqueta), si utiliza permanece igual Hola a través de todos los emparejamientos de Hola. interna de Hello Id. de VLAN (c-tag) es exclusivo para cada emparejamiento. último octeto de la dirección IPv4 de Hello siempre será un número impar.

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a>2. Configuración de sesiones eBGP
Debe configurar una sesión BGP con Microsoft para cada emparejamiento. ejemplo de Hola siguiente permite toosetup una sesión BGP con Microsoft. Si Hola dirección IPv4 que usan para la interfaz de sub era a.b.c.d, dirección IP de saludo del vecino BGP hello (Microsoft) será a.b.c.d+1. último octeto de Hola de dirección de IPv4 de vecino de hello BGP siempre será un número par.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a>3. Configurar toobe de prefijos anunciados en la sesión BGP Hola
Puede configurar su tooMicrosoft de enrutador tooadvertise seleccione prefijos. Puede hacerlo utilizando Hola el ejemplo siguiente.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a>4. Asignaciones de ruta
Puede usar las asignaciones de ruta y prefijo enumera los prefijos de toofilter que se propague a la red. Puede usar el ejemplo de Hola por debajo de la tarea de hello tooaccomplish. Asegúrese de que tiene el programa de instalación de listas de prefijos adecuado.

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


## <a name="juniper-mx-series-routers"></a>Enrutadores Juniper serie MX
ejemplos de Hello en esta sección se aplican para los enrutadores de la serie Juniper MX.

### <a name="1-configuring-interfaces-and-sub-interfaces"></a>1. Configuración de interfaces y subinterfaces

**Definición de interfaz Dot1Q**

Este ejemplo proporciona la definición de interfaz subcarpetas de Hola para una interfaz secundaria con un único identificador de VLAN. Hola Id. de VLAN es exclusivo para cada emparejamiento. último octeto de la dirección IPv4 de Hello siempre será un número impar.

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


**Definición de interfaz QinQ**

Este ejemplo proporciona la definición de interfaz subcarpetas de Hola para una interfaz subcarpetas con dos identificadores de VLAN. Hola externa Id. de VLAN (s-etiqueta), si utiliza permanece igual Hola a través de todos los emparejamientos de Hola. interna de Hello Id. de VLAN (c-tag) es exclusivo para cada emparejamiento. último octeto de la dirección IPv4 de Hello siempre será un número impar.

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

### <a name="2-setting-up-ebgp-sessions"></a>2. Configuración de sesiones eBGP
Debe configurar una sesión BGP con Microsoft para cada emparejamiento. ejemplo de Hola siguiente permite toosetup una sesión BGP con Microsoft. Si Hola dirección IPv4 que usan para la interfaz de sub era a.b.c.d, dirección IP de saludo del vecino BGP hello (Microsoft) será a.b.c.d+1. último octeto de Hola de dirección de IPv4 de vecino de hello BGP siempre será un número par.

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

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a>3. Configurar toobe de prefijos anunciados en la sesión BGP Hola
Puede configurar su tooMicrosoft de enrutador tooadvertise seleccione prefijos. Puede hacerlo utilizando Hola el ejemplo siguiente.

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


### <a name="4-route-maps"></a>4. Asignaciones de ruta
Puede usar las asignaciones de ruta y prefijo enumera los prefijos de toofilter que se propague a la red. Puede usar el ejemplo de Hola por debajo de la tarea de hello tooaccomplish. Asegúrese de que tiene el programa de instalación de listas de prefijos adecuado.

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

## <a name="next-steps"></a>Pasos siguientes
Vea hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md) para obtener más detalles.

