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
# <a name="router-configuration-samples-tooset-up-and-manage-nat"></a><span data-ttu-id="3812d-103">Configuración del enrutador ejemplos tooset seguridad y administrar NAT</span><span class="sxs-lookup"><span data-stu-id="3812d-103">Router configuration samples tooset up and manage NAT</span></span>
<span data-ttu-id="3812d-104">En esta página se proporcionan ejemplos de configuración de NAT para enrutadores Cisco serie ASA y Juniper serie SRX.</span><span class="sxs-lookup"><span data-stu-id="3812d-104">This page provides NAT configuration samples for Cisco ASA and Juniper SRX series routers.</span></span> <span data-ttu-id="3812d-105">Estos son ejemplos de toobe previsto únicamente carácter informativo y no puede usar tal cual.</span><span class="sxs-lookup"><span data-stu-id="3812d-105">These are intended toobe samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="3812d-106">Puede trabajar con su proveedor toocome con configuraciones adecuadas para la red.</span><span class="sxs-lookup"><span data-stu-id="3812d-106">You can work with your vendor toocome up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3812d-107">Los ejemplos en esta página están toobe previsto puramente para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="3812d-107">Samples in this page are intended toobe purely for guidance.</span></span> <span data-ttu-id="3812d-108">Debe trabajar con el equipo de ventas / técnica de su proveedor y la red toocome equipo seguridad con configuraciones adecuadas toomeet sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="3812d-108">You must work with your vendor's sales / technical team and your networking team toocome up with appropriate configurations toomeet your needs.</span></span> <span data-ttu-id="3812d-109">Microsoft no admitirá problemas relacionados con tooconfigurations enumerados en esta página.</span><span class="sxs-lookup"><span data-stu-id="3812d-109">Microsoft will not support issues related tooconfigurations listed in this page.</span></span> <span data-ttu-id="3812d-110">Debe ponerse en contacto con el fabricante del dispositivo para problemas de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="3812d-110">You must contact your device vendor for support issues.</span></span>
> 
> 

* <span data-ttu-id="3812d-111">Ejemplos de configuración de enrutador siguientes aplican tooAzure Public y Microsoft emparejamientos.</span><span class="sxs-lookup"><span data-stu-id="3812d-111">Router configuration samples below apply tooAzure Public and Microsoft peerings.</span></span> <span data-ttu-id="3812d-112">No debe configurar NAT para emparejamiento privado de Azure.</span><span class="sxs-lookup"><span data-stu-id="3812d-112">You must not configure NAT for Azure private peering.</span></span> <span data-ttu-id="3812d-113">Si desea más información, consulte [Emparejamientos de ExpressRoute](expressroute-circuit-peerings.md) y [Requisitos de NAT de ExpressRoute](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="3812d-113">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute NAT requirements](expressroute-nat.md) for more details.</span></span>

* <span data-ttu-id="3812d-114">DEBE utilizar independiente de grupos de IP de NAT para conectividad toohello internet y ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3812d-114">You MUST use separate NAT IP pools for connectivity toohello internet and ExpressRoute.</span></span> <span data-ttu-id="3812d-115">Con hello misma IP de NAT de grupo a través de Hola internet y ExpressRoute dará como resultado el enrutamiento y la pérdida de conectividad asimétrica.</span><span class="sxs-lookup"><span data-stu-id="3812d-115">Using hello same NAT IP pool across hello internet and ExpressRoute will result in asymmetric routing and loss of connectivity.</span></span>


## <a name="cisco-asa-firewalls"></a><span data-ttu-id="3812d-116">Firewalls de Cisco ASA</span><span class="sxs-lookup"><span data-stu-id="3812d-116">Cisco ASA firewalls</span></span>
### <a name="pat-configuration-for-traffic-from-customer-network-toomicrosoft"></a><span data-ttu-id="3812d-117">Configuración de PAT para el tráfico de tooMicrosoft de red de cliente</span><span class="sxs-lookup"><span data-stu-id="3812d-117">PAT configuration for traffic from customer network tooMicrosoft</span></span>
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

### <a name="pat-configuration-for-traffic-from-microsoft-toocustomer-network"></a><span data-ttu-id="3812d-118">Configuración de PAT para el tráfico de red de Microsoft toocustomer</span><span class="sxs-lookup"><span data-stu-id="3812d-118">PAT configuration for traffic from Microsoft toocustomer network</span></span>

<span data-ttu-id="3812d-119">**Interfaces y dirección:**</span><span class="sxs-lookup"><span data-stu-id="3812d-119">**Interfaces and Direction:**</span></span>

    Source Interface (where hello traffic enters hello ASA): inside
    Destination Interface (where hello traffic exits hello ASA): outside

<span data-ttu-id="3812d-120">**Configuración:**</span><span class="sxs-lookup"><span data-stu-id="3812d-120">**Configuration:**</span></span>

<span data-ttu-id="3812d-121">Grupo NAT:</span><span class="sxs-lookup"><span data-stu-id="3812d-121">NAT Pool:</span></span>

    object network outbound-PAT
        host <NAT-IP>

<span data-ttu-id="3812d-122">Servidor de destino:</span><span class="sxs-lookup"><span data-stu-id="3812d-122">Target Server:</span></span>

    object network Customer-Network
        network-object <IP> <Subnet-Mask>

<span data-ttu-id="3812d-123">Grupo de objetos de direcciones IP de cliente</span><span class="sxs-lookup"><span data-stu-id="3812d-123">Object Group for Customer IP Addresses</span></span>

    object-group network MSFT-Network-1
        network-object <MSFT-IP> <Subnet-Mask>

    object-group network MSFT-PAT-Networks
        network-object object MSFT-Network-1

<span data-ttu-id="3812d-124">Comandos NAT:</span><span class="sxs-lookup"><span data-stu-id="3812d-124">NAT Commands:</span></span>

    nat (inside,outside) source dynamic MSFT-PAT-Networks pat-pool outbound-PAT destination static Customer-Network Customer-Network


## <a name="juniper-srx-series-routers"></a><span data-ttu-id="3812d-125">Enrutadores Juniper serie SRX</span><span class="sxs-lookup"><span data-stu-id="3812d-125">Juniper SRX series routers</span></span>
### <a name="1-create-redundant-ethernet-interfaces-for-hello-cluster"></a><span data-ttu-id="3812d-126">1. Crear redundancia interfaces Ethernet para clúster Hola</span><span class="sxs-lookup"><span data-stu-id="3812d-126">1. Create redundant Ethernet interfaces for hello cluster</span></span>
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


### <a name="2-create-two-security-zones"></a><span data-ttu-id="3812d-127">2. Creación de dos zonas de seguridad</span><span class="sxs-lookup"><span data-stu-id="3812d-127">2. Create two security zones</span></span>
* <span data-ttu-id="3812d-128">Zona de confianza para la red interna y Zona de no confianza para la red externa que soporta enrutadores de borde</span><span class="sxs-lookup"><span data-stu-id="3812d-128">Trust Zone for internal network and Untrust Zone for external network facing Edge Routers</span></span>
* <span data-ttu-id="3812d-129">Asignar interfaces adecuadas toohello zonas</span><span class="sxs-lookup"><span data-stu-id="3812d-129">Assign appropriate interfaces toohello zones</span></span>
* <span data-ttu-id="3812d-130">Permitir que los servicios en interfaces de Hola</span><span class="sxs-lookup"><span data-stu-id="3812d-130">Allow services on hello interfaces</span></span>

    <span data-ttu-id="3812d-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span><span class="sxs-lookup"><span data-stu-id="3812d-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span></span>


### <a name="3-create-security-policies-between-zones"></a><span data-ttu-id="3812d-132">3. Creación de directivas de seguridad entre zonas</span><span class="sxs-lookup"><span data-stu-id="3812d-132">3. Create security policies between zones</span></span>
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


### <a name="4-configure-nat-policies"></a><span data-ttu-id="3812d-133">4. Configuración de directivas de NAT</span><span class="sxs-lookup"><span data-stu-id="3812d-133">4. Configure NAT policies</span></span>
* <span data-ttu-id="3812d-134">Creación de dos grupos de NAT.</span><span class="sxs-lookup"><span data-stu-id="3812d-134">Create two NAT pools.</span></span> <span data-ttu-id="3812d-135">Uno será tooNAT usado el tráfico saliente tooMicrosoft y otro de cliente de Microsoft toohello.</span><span class="sxs-lookup"><span data-stu-id="3812d-135">One will be used tooNAT traffic outbound tooMicrosoft and other from Microsoft toohello customer.</span></span>
* <span data-ttu-id="3812d-136">Crear reglas de tráfico de tooNAT Hola respectivos</span><span class="sxs-lookup"><span data-stu-id="3812d-136">Create rules tooNAT hello respective traffic</span></span>
  
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

### <a name="5-configure-bgp-tooadvertise-selective-prefixes-in-each-direction"></a><span data-ttu-id="3812d-137">5. Configurar los prefijos BGP tooadvertise selectivos en cada dirección</span><span class="sxs-lookup"><span data-stu-id="3812d-137">5. Configure BGP tooadvertise selective prefixes in each direction</span></span>
<span data-ttu-id="3812d-138">Consulte toosamples en [ejemplos de configuración de enrutamiento ](expressroute-config-samples-routing.md) página.</span><span class="sxs-lookup"><span data-stu-id="3812d-138">Refer toosamples in [Routing configuration samples ](expressroute-config-samples-routing.md) page.</span></span>

### <a name="6-create-policies"></a><span data-ttu-id="3812d-139">6. Creación de directivas</span><span class="sxs-lookup"><span data-stu-id="3812d-139">6. Create policies</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="3812d-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3812d-140">Next steps</span></span>
<span data-ttu-id="3812d-141">Vea hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="3812d-141">See hello [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

