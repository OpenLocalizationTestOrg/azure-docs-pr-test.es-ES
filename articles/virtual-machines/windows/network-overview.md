---
title: "aaaVirtual redes y máquinas virtuales de Windows en Azure | Documentos de Microsoft"
description: "Obtenga información sobre la red cuando se relaciona con los conceptos básicos de toohello de creación de máquinas virtuales de Windows en Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5493e9f7-7d45-4e98-be9a-657a53708746
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: e28a4782f9f6c69f6101e45dbb560ccd694a1e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-networks-and-windows-virtual-machines-in-azure"></a>Redes virtuales y máquinas virtuales Windows en Azure 

Cuando se crea una máquina virtual (VM) de Azure, es preciso crear una [red virtual](../../virtual-network/virtual-networks-overview.md) (VNet) o usar una red virtual existente. También debe toodecide cómo las máquinas virtuales son previsto toobe acceso en hello red virtual. Es importante demasiado[plan antes de crear recursos](../../virtual-network/virtual-network-vnet-plan-design-arm.md) y asegúrese de que comprende hello [límites de recursos de red](../../azure-subscription-service-limits.md#networking-limits).

Hola figura siguiente, las máquinas virtuales se representan como servidores web y servidores de base de datos. Cada conjunto de máquinas virtuales se asignan subredes tooseparate Hola red virtual.

![red virtual de Azure](./media/network-overview/vnetoverview.png)

Puede crear una red virtual antes de crear una máquina virtual o puede crear Hola red virtual al crear una máquina virtual. De igual forma, debe crear una red virtual usted mismo, o bien se puede crear automáticamente al crear una máquina virtual.

Crear estos recursos toosupport comunicación con una máquina virtual:

- Interfaces de red
- Direcciones IP
- Red virtual y subredes

Además toothose recursos básicos, también debería considerar estos recursos opcionales:

- Grupos de seguridad de red
- Equilibradores de carga 

## <a name="network-interfaces"></a>Interfaces de red

A [interfaz de red (NIC)](../../virtual-network/virtual-network-network-interface.md) es interconexión de hello entre una máquina virtual y una red virtual (VNet). Una máquina virtual debe tener al menos una NIC, pero puede tener más de uno, según el tamaño de Hola de hello VM que se crea. Para obtener información acerca de cuántas NIC admite cada tamaño de máquina virtual, consulte [Tamaños de las máquinas virtuales Linux en Azure](sizes.md). 

Si desea toocreate una máquina virtual con más de una NIC, debe crear Hola VM con al menos dos.  Después de su creación puede agregar NIC adicionales número toohello compatible con tamaño VM de hello, pero no se puede agregar tooa adicional de NIC virtual solo se creó con una, independientemente de cuántas NIC es compatible con hello tamaño de máquina virtual. 

Si Hola VM se agrega el conjunto de disponibilidad tooan, todas las máquinas virtuales en el conjunto de disponibilidad de hello deben tener uno o varios NIC. Las máquinas virtuales con más de un NIC no es necesario toohave Hola el mismo número de NIC, pero todas ellas deben tener al menos dos.

Cada tooa NIC conectada VM debe existir en Hola misma ubicación y suscripción como Hola máquina virtual. Cada NIC debe estar conectado tooa red virtual que existe en hello misma ubicación de Azure y la suscripción como Hola NIC. Después de crea una NIC, puede cambiar la subred de hello a que está conectado, pero no se puede cambiar Hola red virtual está conectado a.  Cada NIC conectada tooa que máquina virtual se asigna una dirección MAC que no cambia hasta que se elimine Hola máquina virtual.

Esta tabla enumeran los métodos de Hola que puede usar toocreate una interfaz de red.

| Método | Descripción |
| ------ | ----------- |
| Azure Portal | Cuando se crea una máquina virtual en hello portal de Azure, se crea automáticamente una interfaz de red automáticamente (no se puede usar una NIC crear por separado). portal de Hello crea una máquina virtual con solo una NIC. Si desea que una máquina virtual con más de una NIC toocreate, se debe crear con un método diferente. |
| [Azure PowerShell](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) | Use [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) con hello **PublicIpAddressId -** parámetro tooprovide Hola identificador de dirección IP pública Hola que creó anteriormente. |
| [CLI de Azure](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md) | Hola tooprovide un identificador de la dirección IP pública de Hola que aborda el uso creado anteriormente, [crear nic de red az](https://docs.microsoft.com/cli/azure/network/nic#create) con hello **--public-ip-address** parámetro. |
| [Plantilla](../../virtual-network/virtual-network-deploy-multinic-arm-template.md) | Use [Network Interface in a Virtual Network with Public IP Address](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet) (Interfaz de red en una red virtual con dirección IP pública) como guía para implementar una interfaz de red mediante una plantilla. |

## <a name="ip-addresses"></a>Direcciones IP 

Puede asignar estos tipos de [direcciones IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) tooa NIC en Azure:

- **Las direcciones IP públicas** -usa toocommunicate entrante y saliente (sin traducción de direcciones de red (NAT)) con hello Internet y otros recursos de Azure no conectados tooa red virtual. Asignar una tooa de dirección IP pública NIC es opcional. Las direcciones IP públicas tienen un cargo nominal y se puede usar un número máximo de ellas por suscripción.
- **Direcciones IP privadas** : se usan para la comunicación dentro de una red virtual, la red local y Hola Internet (con NAT). Debe asignar al menos un tooa de dirección IP privada virtual. toolearn más información acerca de NAT en Azure, lea [descripción de las conexiones salientes en Azure](../../load-balancer/load-balancer-outbound-connections.md).

Puede asignar tooVMs de direcciones IP públicas o equilibradores de carga a través de internet. Puede asignar tooVMs de direcciones IP privadas y equilibradores de carga interno. Asignar tooa de direcciones IP mediante una interfaz de red de máquina virtual.

Existen dos métodos en el que una dirección IP se asigna recursos tooa - dinámico o estático. método de asignación de Hello predeterminada es dinámico, donde no se asigna una dirección IP cuando se crea. En su lugar, se asigna una dirección IP de hello al crear una máquina virtual o iniciar una VM detenida. dirección IP de Hola se libera cuando detener o eliminar Hola máquina virtual. 

Hola tooensure dirección IP de Hola para hello VM permanece igual, puede establecer explícitamente el método de asignación de Hola toostatic. En este caso, se asigna de inmediato una dirección IP. Se libera cuando se elimina Hola VM o cambie su toodynamic de método de asignación.
    
Esta tabla enumeran los métodos de Hola que puede usar toocreate una dirección IP.

| Método | Descripción |
| ------ | ----------- |
| [Portal de Azure](../../virtual-network/virtual-network-deploy-static-pip-arm-portal.md) | De forma predeterminada, las direcciones IP públicas son dinámicas y Hola dirección asociada toothem puede cambiar cuando se detiene o elimina Hola máquina virtual. tooguarantee que Hola VM siempre utiliza Hola la misma dirección IP pública, cree una dirección IP pública estática. De forma predeterminada, el portal de Hola asigna una tooa de dirección IP privada NIC dinámica al crear una máquina virtual. Puede cambiar este toostatic después Hola que se crea la máquina virtual.|
| [Azure PowerShell](../../virtual-network/virtual-network-deploy-static-pip-arm-ps.md) | Usa [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) con hello **AllocationMethod -** parámetro como dinámico o estático. |
| [CLI de Azure](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md) | Usa [crear az red public-ip](https://docs.microsoft.com/cli/azure/network/public-ip#create) con hello **: método de asignación** parámetro como dinámico o estático. |
| [Plantilla](../../virtual-network/virtual-network-deploy-static-pip-arm-template.md) | Use [Network Interface in a Virtual Network with Public IP Address](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet) (Interfaz de red en una red virtual con dirección IP pública) como guía para implementar una dirección IP pública mediante una plantilla. |

Después de crear una dirección IP pública, se puede asociar a una máquina virtual mediante la asignación tooa NIC.

## <a name="virtual-network-and-subnets"></a>Red virtual y subredes

Una subred es un intervalo de direcciones IP en hello red virtual. Una red virtual se puede dividir en varias subredes para facilitar su organización o por motivos de seguridad. Cada NIC en una máquina virtual es subred tooone conectados en una red virtual. NIC conectado toosubnets (iguales o distintos) dentro de una red virtual pueden comunicarse entre sí sin ninguna configuración adicional.

Al configurar una red virtual, especifique topología hello, incluidas las subredes y los espacios de direcciones disponibles de Hola. Si hello red virtual es toobe conectado tooother redes virtuales o locales redes, debe seleccionar intervalos de direcciones que no se superponen. direcciones IP de Hello son privadas y no son accesibles desde Internet, lo cual era true solo para las direcciones IP de hello no enrutables como 10.0.0.0/8, 172.16.0.0/12 o 192.168.0.0/16 Hola. Ahora, Azure trata cualquier intervalo de direcciones como parte de hello privada VNet espacio de direcciones IP que solo sea accesible dentro de hello red virtual, en redes virtuales conectadas entre sí y desde la ubicación local. 

Si trabaja en una organización en la que otra persona es responsable de las redes internas hello, debe hablar a toothat persona antes de seleccionar el espacio de direcciones. Asegúrese de que no hay ninguna superposición y dígales espacio Hola desea toouse para que no intenten toouse Hola mismo intervalo de direcciones IP. 

De forma predeterminada, no hay ningún límite de seguridad entre subredes, por lo que las máquinas virtuales en cada una de estas subredes pueden hablar tooone otro. Sin embargo, puede configurar grupos de seguridad de red (NSG), que le permiten tooand de flujo de tráfico toocontrol Hola de subredes y tooand desde máquinas virtuales. 

Esta tabla enumeran los métodos de Hola que puede usar una red virtual toocreate y subredes.   

| Método | Descripción |
| ------ | ----------- |
| [Portal de Azure](../../virtual-network/virtual-networks-create-vnet-arm-pportal.md) | Si permites que Azure cree una red virtual cuando se crea una máquina virtual, el nombre de hello es una combinación de nombre de grupo de recursos de Hola que contiene Hola red virtual y **- red virtual**. espacio de direcciones de Hello es 10.0.0.0/24, nombre de subred requerida de hello es **predeterminado**, y el intervalo de direcciones de subred de hello es 10.0.0.0/24. |
| [Azure PowerShell](../../virtual-network/virtual-networks-create-vnet-arm-ps.md) | Usa [New-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetworkSubnetConfig) y [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetwork) toocreate una subred y una red virtual. También puede usar [AzureRmVirtualNetworkSubnetConfig agregar](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) tooadd un tooan de subred red virtual existente. |
| [CLI de Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md) | Hello hello red virtual y subred se crean en hello mismo tiempo. Proporcionar un **: nombre de la subred** parámetro demasiado[crear red virtual de red az](https://docs.microsoft.com/cli/azure/network/vnet#create) con el nombre de la subred de Hola. |
| [Plantilla](../../virtual-network/virtual-networks-create-vnet-arm-template-click.md) | Hola toocreate de manera más fácil una red virtual y subredes toodownload una plantilla existente, como [red Virtual con dos subredes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets)y modificarlo para sus necesidades. |

## <a name="network-security-groups"></a>Grupos de seguridad de red

A [grupo de seguridad de red (NSG)](../../virtual-network/virtual-networks-nsg.md) contiene una lista de reglas de lista de Control de acceso (ACL) que permiten o deniegan toosubnets de tráfico de red, NIC o ambos. Los NSG se pueden asociar con subredes o individuales NIC conectado tooa subred. Cuando un NSG está asociado a una subred, las reglas de ACL de hello aplican tooall hello las máquinas virtuales en esa subred. Además, el tráfico tooan NIC individual puede estar restringida por asociar un NSG directamente tooa NIC.

Contiene dos tipos de reglas: de entrada y de salida. prioridad de Hola para una regla debe ser único dentro de cada conjunto. Cada regla tiene propiedades de protocolo, intervalos de puertos de origen y destino, prefijos de direcciones, dirección de tráfico, prioridad y tipo de acceso. 

Todos los grupos de seguridad de red contienen un conjunto de reglas predeterminadas. no se puede eliminar las reglas predeterminadas de Hello, pero dado que se asignan prioridad más baja de hello, pueden reemplazarse por reglas de Hola que cree. 

Al asociar un tooa NSG NIC, reglas de acceso de red de Hola Hola NSG son NIC de toothat solo aplicada. Si un NSG está aplicada tooa único NIC en una VM de varias NIC, no afecta al tráfico toohello otras NIC. Puede asociar diferentes NSG tooa NIC (o máquina virtual, según el modelo de implementación de hello) y Hola subred que está enlazado una NIC o la máquina virtual. Se da prioridad basado en dirección Hola del tráfico.

Asegúrese de demasiado[plan](../../virtual-network/virtual-networks-nsg.md#planning) sus NSG al planear las máquinas virtuales y red virtual.

Esta tabla enumeran los métodos de Hola que puede usar toocreate un grupo de seguridad de red.

| Método | Descripción |
| ------ | ----------- |
| [Portal de Azure](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md) | Cuando se crea una máquina virtual en hello portal de Azure, se crea automáticamente un NSG y toohello asociado NIC Hola portal crea. nombre de Hola de hello NSG es una combinación del nombre de Hola de hello VM y **- nsg**. Este NSG contiene una regla de entrada con una prioridad de 1000, servicio conjunto tooRDP, tooTCP de conjunto de protocolo de hello, puerto configurado too3389 y acción establece tooAllow. Si desea tooallow cualquier toohello de tráfico entrante otras máquinas virtuales, debe agregar reglas adicionales toohello NSG. |
| [Azure PowerShell](../../virtual-network/virtual-networks-create-nsg-arm-ps.md) | Use [AzureRmNetworkSecurityRuleConfig New](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityRuleConfig) y proporcionar información de la regla de hello necesario. Use [New-AzureRmNetworkSecurityGroup](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityGroup) toocreate hello NSG. Use [AzureRmVirtualNetworkSubnetConfig conjunto](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/Set-AzureRmVirtualNetworkSubnetConfig) tooconfigure hello NSG para la subred de Hola. Use [AzureRmVirtualNetwork conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetwork) tooadd hello NSG toohello red virtual. |
| [CLI de Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md) | Use [crear az red nsg](https://docs.microsoft.com/cli/azure/network/nsg#create) tooinitially crear hello NSG. Use [crear regla de nsg de red az](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) tooadd reglas toohello NSG. Use [actualización de subred de red virtual de red az](https://docs.microsoft.com/en-us/cli/azure/network/vnet/subnet#update) subred toohello de tooadd hello NSG. |
| [Plantilla](../../virtual-network/virtual-networks-create-nsg-arm-template.md) | Use [Create a Network Security Group](https://github.com/Azure/azure-quickstart-templates/tree/master/101-security-group-create) (Creación de un grupo de seguridad de red) como guía para la implementación de un grupo de seguridad de red mediante una plantilla. |

## <a name="load-balancers"></a>Equilibradores de carga

[El equilibrador de carga Azure](../../load-balancer/load-balancer-overview.md) entrega tooyour aplicaciones de alta disponibilidad y rendimiento de red. Se puede configurar un equilibrador de carga demasiado[equilibrar el tráfico entrante de Internet](../../load-balancer/load-balancer-internet-overview.md) tooVMs o [equilibrar el tráfico entre máquinas virtuales en una red virtual](../../load-balancer/load-balancer-internal-overview.md). Un equilibrador de carga también puede equilibrar el tráfico entre equipos locales y máquinas virtuales en una red entre entornos o reenvíe el tráfico externo tooa máquina virtual específica.

Hola carga equilibrador mapas de tráfico entrante y saliente entre Hola dirección IP pública y puerto de equilibrador de carga de Hola y dirección IP privada de Hola y el puerto de hello máquina virtual.

Al crear un equilibrador de carga, también es preciso tener en cuenta estos elementos de configuración:

- **Configuración de IP de front-end**: un equilibrador de carga puede incluir una o varias direcciones IP de front-end, conocidas también como IP virtuales (VIP). Estas direcciones IP servir como entrada para el tráfico de Hola.
- **Grupo de direcciones de back-end** – se distribuye las direcciones IP que están asociadas a la carga de hello NIC toowhich.
- **Las reglas NAT** -define cómo el tráfico fluye a través de IP de front-end de Hola y distribuida toohello IP de back-end.
- **Reglas del equilibrador de carga** -asigna una determinada IP front-end y un conjunto de tooa de combinación de puerto de direcciones IP de back-end y combinación de puerto. Un solo equilibrador de carga puede tener varias reglas de equilibrio de carga. Cada regla tiene una combinación de una IP de front-end y un puerto y una IP de back-end asociados a las máquinas virtuales.
- **[Sondeos](../../load-balancer/load-balancer-custom-probe-overview.md)**  -Hola de monitores de mantenimiento de máquinas virtuales. Cuando un sondeo se produce un error toorespond, equilibrador de carga de hello deja de enviar toohello de las conexiones nuevas VM incorrecto. no se ven afectadas las conexiones existentes de Hola y las conexiones nuevas se envían toohealthy las máquinas virtuales.

Esta tabla enumeran los métodos de Hola que puede usar toocreate un equilibrador de carga a través de internet.

| Método | Descripción |
| ------ | ----------- |
| Azure Portal | Actualmente no se puede crear un equilibrador de carga de conexión a internet mediante Hola portal de Azure. |
| [Azure PowerShell](../../load-balancer/load-balancer-get-started-internet-arm-ps.md) | Hola tooprovide un identificador de la dirección IP pública de Hola que aborda el uso creado anteriormente, [New-AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) con hello **PublicIpAddress -** parámetro. Use [New-AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) toocreate configuración de Hola Hola back-end del grupo de direcciones. Use [New-AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) toocreate entrada reglas NAT asociadas con la configuración IP front-end Hola que ha creado. Use [New-AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) toocreate Hola sondeos que necesita. Use [AzureRmLoadBalancerRuleConfig New](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) configuración de equilibrador de carga de toocreate Hola. Use [AzureRmLoadBalancer New](/powershell/module/azurerm.network/new-azurermloadbalancer) equilibrador de carga de toocreate Hola.|
| [CLI de Azure](../../load-balancer/load-balancer-get-started-internet-arm-cli.md) | Use [crear az red lb](https://docs.microsoft.com/cli/azure/network/lb#create) configuración de equilibrador de carga inicial de toocreate Hola. Use [crear az red lb ip de front-end](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) tooadd Hola dirección IP pública que creó anteriormente. Use [crear az red lb grupo de direcciones](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) tooadd configuración de Hola Hola back-end del grupo de direcciones. Use [az red lb-regla nat entrante-crear](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) tooadd reglas NAT. Use [crear regla de carga equilibrada de red az](https://docs.microsoft.com/cli/azure/network/lb/rule#create) reglas del equilibrador de carga de tooadd Hola. Use [crear la prueba de carga equilibrada de red az](https://docs.microsoft.com/cli/azure/network/lb/probe#create) tooadd Hola sondeos. |
| [Plantilla](../../load-balancer/load-balancer-get-started-internet-arm-template.md) | Use [2 máquinas virtuales en un equilibrador de carga y configurar las reglas NAT en hello LB](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-natrules) como guía para implementar un equilibrador de carga mediante una plantilla. |
    
Esta tabla enumeran los métodos de Hola que puede usar toocreate un equilibrador de carga interno.

| Método | Descripción |
| ------ | ----------- |
| Azure Portal | Actualmente no se puede crear un equilibrador de carga interno mediante Hola portal de Azure. |
| [Azure PowerShell](../../load-balancer/load-balancer-get-started-ilb-arm-ps.md) | tooprovide una dirección IP privada en la subred de red de hello, use [New-AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) con hello **PrivateIpAddress -** parámetro. Use [New-AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) toocreate configuración de Hola Hola back-end del grupo de direcciones. Use [New-AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) toocreate entrada reglas NAT asociadas con la configuración IP front-end Hola que ha creado. Use [New-AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) toocreate Hola sondeos que necesita. Use [AzureRmLoadBalancerRuleConfig New](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) configuración de equilibrador de carga de toocreate Hola. Use [AzureRmLoadBalancer New](/powershell/module/azurerm.network/new-azurermloadbalancer) equilibrador de carga de toocreate Hola.|
| [CLI de Azure](../../load-balancer/load-balancer-get-started-ilb-arm-cli.md) | Hola de uso [crear az red lb](https://docs.microsoft.com/cli/azure/network/lb#create) configuración de equilibrador de carga inicial de comando toocreate Hola. toodefine Hola dirección IP privada, utilice [crear az red lb ip de front-end](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) con hello **--dirección de ip privada** parámetro. Use [crear az red lb grupo de direcciones](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) tooadd configuración de Hola Hola back-end del grupo de direcciones. Use [az red lb-regla nat entrante-crear](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) tooadd reglas NAT. Use [crear regla de carga equilibrada de red az](https://docs.microsoft.com/cli/azure/network/lb/rule#create) reglas del equilibrador de carga de tooadd Hola. Use [crear la prueba de carga equilibrada de red az](https://docs.microsoft.com/cli/azure/network/lb/probe#create) tooadd Hola sondeos.|
| [Plantilla](../../load-balancer/load-balancer-get-started-ilb-arm-template.md) | Use [2 máquinas virtuales en un equilibrador de carga y configurar las reglas NAT en hello LB](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer) como guía para implementar un equilibrador de carga mediante una plantilla. |

## <a name="vms"></a>Máquinas virtuales

Las máquinas virtuales pueden crearse en hello misma red virtual y se puede conectar tooeach otro uso de direcciones IP privada. Pueden conectarse incluso si están en subredes diferentes sin Hola necesidad tooconfigure una puerta de enlace o use direcciones IP públicas. tooput máquinas virtuales en una red virtual, crear Hola red virtual y, a continuación, a medida que cree cada máquina virtual, le asigna toohello red virtual y subred. Las máquinas virtuales adquieren su configuración de red durante la implementación o el inicio.  

A las máquinas virtuales se les asigna una dirección IP cuando se implementan. Si implementa varias máquinas virtuales en una red virtual o una subred, se les asignan direcciones IP cuando arrancan. Una dirección IP dinámica (DIP) es la dirección IP interna Hola asociado a una máquina virtual. Puede asignar un tooa DIP estática máquina virtual. Si asigna una DIP estática, considere la posibilidad de usar un tooavoid de subred específica reutilizar accidentalmente una DIP estática para otra máquina virtual.  

Si crea una máquina virtual y posteriormente desea toomigrate en una red virtual, no es un cambio de configuración simple. Debe volver a implementar Hola VM en hello red virtual. Hola tooredeploy de manera más fácil es toodelete Hola de máquina virtual, pero no los discos conectados tooit y, a continuación, volver a crear Hola VM mediante Hola discos originales en hello red virtual. 

Esta tabla enumeran los métodos de Hola que puede usar toocreate una máquina virtual en una red virtual.

| Método | Descripción |
| ------ | ----------- |
| [Portal de Azure](../virtual-machines-windows-hero-tutorial.md) | Usará Hola red la configuración predeterminada que se encontraba anteriormente mencionados toocreate una máquina virtual con una NIC único. toocreate una máquina virtual con varias NIC, debe usar un método diferente. |
| [Azure PowerShell](../virtual-machines-windows-ps-create.md) | Incluye el uso de Hola de [AzureRmVMNetworkInterface agregar](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooadd Hola NIC que creaste previamente toohello configuración de máquina virtual. |
| [Plantilla](ps-template.md) | Use [Very simple deployment of a Windows VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) (Implementación muy simple de una máquina virtual Windows) como guía para la implementación de una máquina virtual mediante una plantilla. |

## <a name="next-steps"></a>Pasos siguientes

- Obtenga información acerca de cómo tooconfigure [rutas definidas por el usuario y reenvío IP](../../virtual-network/virtual-networks-udr-overview.md). 
- Obtenga información acerca de cómo tooconfigure [las conexiones de red virtual tooVNet](../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).
- Obtenga información acerca de cómo demasiado[solucionar problemas de rutas](../../virtual-network/virtual-network-routes-troubleshoot-portal.md).
