---
title: "ejemplos de configuración de enrutador de cliente aaaExpressRoute | Documentos de Microsoft"
description: "Esta página ofrece ejemplos de configuración de enrutamiento para enrutadores Cisco y Juniper."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: d6ea716f-d5ee-4a61-92b0-640d6e7d6974
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: b5faca0666bda6173e54abb0b6560d5f8bf8bfc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="router-configuration-samples-tooset-up-and-manage-nat"></a>Configuración del enrutador ejemplos tooset seguridad y administrar NAT
En esta página se proporcionan ejemplos de configuración de NAT para enrutadores Cisco serie ASA y Juniper serie SRX. Estos son ejemplos de toobe previsto únicamente carácter informativo y no puede usar tal cual. Puede trabajar con su proveedor toocome con configuraciones adecuadas para la red. 

> [!IMPORTANT]
> Los ejemplos en esta página están toobe previsto puramente para obtener instrucciones. Debe trabajar con el equipo de ventas / técnica de su proveedor y la red toocome equipo seguridad con configuraciones adecuadas toomeet sus necesidades. Microsoft no admitirá problemas relacionados con tooconfigurations enumerados en esta página. Debe ponerse en contacto con el fabricante del dispositivo para problemas de soporte técnico.
> 
> 

* Ejemplos de configuración de enrutador siguientes aplican tooAzure Public y Microsoft emparejamientos. No debe configurar NAT para emparejamiento privado de Azure. Si desea más información, consulte [Emparejamientos de ExpressRoute](expressroute-circuit-peerings.md) y [Requisitos de NAT de ExpressRoute](expressroute-nat.md).

* DEBE utilizar independiente de grupos de IP de NAT para conectividad toohello internet y ExpressRoute. Con hello misma IP de NAT de grupo a través de Hola internet y ExpressRoute dará como resultado el enrutamiento y la pérdida de conectividad asimétrica.


## <a name="cisco-asa-firewalls"></a>Firewalls de Cisco ASA
### <a name="pat-configuration-for-traffic-from-customer-network-toomicrosoft"></a>Configuración de PAT para el tráfico de tooMicrosoft de red de cliente
    object network MSFT-PAT
      range <SNAT-START-IP> <SNAT-END-IP>


    object-group network MSFT-Range
      network-object <IP> <Subnet_Mask>

    object-group network on-prem-range-1
      network-object <IP> <Subnet-Mask>

    object-group network on-prem-range-2
      network-object <IP> <Subnet-Mask>

    object-group network on-prem
      network-object object on-prem-range-1
      network-object object on-prem-range-2

    nat (outside,inside) source dynamic on-prem pat-pool MSFT-PAT destination static MSFT-Range MSFT-Range

### <a name="pat-configuration-for-traffic-from-microsoft-toocustomer-network"></a>Configuración de PAT para el tráfico de red de Microsoft toocustomer

**Interfaces y dirección:**

    Source Interface (where hello traffic enters hello ASA): inside
    Destination Interface (where hello traffic exits hello ASA): outside

**Configuración:**

Grupo NAT:

    object network outbound-PAT
        host <NAT-IP>

Servidor de destino:

    object network Customer-Network
        network-object <IP> <Subnet-Mask>

Grupo de objetos de direcciones IP de cliente

    object-group network MSFT-Network-1
        network-object <MSFT-IP> <Subnet-Mask>

    object-group network MSFT-PAT-Networks
        network-object object MSFT-Network-1

Comandos NAT:

    nat (inside,outside) source dynamic MSFT-PAT-Networks pat-pool outbound-PAT destination static Customer-Network Customer-Network


## <a name="juniper-srx-series-routers"></a>Enrutadores Juniper serie SRX
### <a name="1-create-redundant-ethernet-interfaces-for-hello-cluster"></a>1. Crear redundancia interfaces Ethernet para clúster Hola
    interfaces {
        reth0 {
            description "tooInternal Network";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 1;
            }
            unit 100 {
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
        reth1 {
            description "tooMicrosoft via Edge Router";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 2;
            }
            unit 100 {
                description "tooMicrosoft via Edge Router";
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
    }


### <a name="2-create-two-security-zones"></a>2. Creación de dos zonas de seguridad
* Zona de confianza para la red interna y Zona de no confianza para la red externa que soporta enrutadores de borde
* Asignar interfaces adecuadas toohello zonas
* Permitir que los servicios en interfaces de Hola

    security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }


### <a name="3-create-security-policies-between-zones"></a>3. Creación de directivas de seguridad entre zonas
    security {
        policies {
            from-zone Trust to-zone Untrust {
                policy allow-any {
                    match {
                        source-address any;
                        destination-address any;
                        application any;
                    }
                    then {
                        permit;
                    }
                }
            }
            from-zone Untrust to-zone Trust {
                policy allow-any {
                    match {
                        source-address any;
                        destination-address any;
                        application any;
                    }
                    then {
                        permit;
                    }
                }
            }
        }
    }


### <a name="4-configure-nat-policies"></a>4. Configuración de directivas de NAT
* Creación de dos grupos de NAT. Uno será tooNAT usado el tráfico saliente tooMicrosoft y otro de cliente de Microsoft toohello.
* Crear reglas de tráfico de tooNAT Hola respectivos
  
       security {
           nat {
               source {
                   pool SNAT-To-ExpressRoute {
                       routing-instance {
                           External-ExpressRoute;
                       }
                       address {
                           <NAT-IP-address/Subnet-mask>;
                       }
                   }
                   pool SNAT-From-ExpressRoute {
                       routing-instance {
                           Internal;
                       }
                       address {
                           <NAT-IP-address/Subnet-mask>;
                       }
                   }
                   rule-set Outbound_NAT {
                       from routing-instance Internal;
                       toorouting-instance External-ExpressRoute;
                       rule SNAT-Out {
                           match {
                               source-address 0.0.0.0/0;
                           }
                           then {
                               source-nat {
                                   pool {
                                       SNAT-To-ExpressRoute;
                                   }
                               }
                           }
                       }
                   }
                   rule-set Inbound-NAT {
                       from routing-instance External-ExpressRoute;
                       toorouting-instance Internal;
                       rule SNAT-In {
                           match {
                               source-address 0.0.0.0/0;
                           }
                           then {
                               source-nat {
                                   pool {
                                       SNAT-From-ExpressRoute;
                                   }
                               }
                           }
                       }
                   }
               }
           }
       }

### <a name="5-configure-bgp-tooadvertise-selective-prefixes-in-each-direction"></a>5. Configurar los prefijos BGP tooadvertise selectivos en cada dirección
Consulte toosamples en [ejemplos de configuración de enrutamiento ](expressroute-config-samples-routing.md) página.

### <a name="6-create-policies"></a>6. Creación de directivas
    routing-options {
                  autonomous-system <Customer-ASN>;
    }
    policy-options {
        prefix-list Microsoft-Prefixes {
            <IP-Address/Subnet-Mask;
            <IP-Address/Subnet-Mask;
        }
        prefix-list private-ranges {
            10.0.0.0/8;
            172.16.0.0/12;
            192.168.0.0/16;
            100.64.0.0/10;
        }
        policy-statement Advertise-NAT-Pools {
            from {
                protocol static;
                route-filter <NAT-Pool-Address/Subnet-mask> prefix-length-range /32-/32;
            }
            then accept;
        }
        policy-statement Accept-from-Microsoft {
            term 1 {
                from {
                    instance External-ExpressRoute;
                    prefix-list-filter Microsoft-Prefixes orlonger;
                }
                then accept;
            }
            term deny {
                then reject;
            }
        }
        policy-statement Accept-from-Internal {
            term no-private {
                from {
                    instance Internal;
                    prefix-list-filter private-ranges orlonger;
                }
                then reject;
            }
            term bgp {
                from {
                    instance Internal;
                    protocol bgp;
                }
                then accept;
            }
            term deny {
                then reject;
            }
        }
    }
    routing-instances {
        Internal {
            instance-type virtual-router;
            interface reth0.100;
            routing-options {
                static {
                    route <NAT-Pool-IP-Address/Subnet-mask> discard;
                }
                instance-import Accept-from-Microsoft;
            }
            protocols {
                bgp {
                    group customer {
                        export <Advertise-NAT-Pools>;
                        peer-as <Customer-ASN-1>;
                        neighbor <BGP-Neighbor-IP-Address>;
                    }
                }
            }
        }
        External-ExpressRoute {
            instance-type virtual-router;
            interface reth1.100;
            routing-options {
                static {
                    route <NAT-Pool-IP-Address/Subnet-mask> discard;
                }
                instance-import Accept-from-Internal;
            }
            protocols {
                bgp {
                    group edge-router {
                        export <Advertise-NAT-Pools>;
                        peer-as <Customer-Public-ASN>;
                        neighbor <BGP-Neighbor-IP-Address>;
                    }
                }
            }
        }
    }

## <a name="next-steps"></a>Pasos siguientes
Vea hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md) para obtener más detalles.

