---
title: Red Virtual aaaAzure | Documentos de Microsoft
description: "Más información sobre las características y conceptos de Azure Virtual Network."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9633de4b-a867-4ddf-be3c-a332edf02e24
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/23/2017
ms.author: jdial
ms.openlocfilehash: 55ae6a131d882ad893aeffcaa4127bc47beda552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-network"></a>Red virtual

Hola habilita de servicio de red Virtual de Azure toosecurely conectar otro tooeach de recursos de Azure con redes virtuales (redes virtuales). Una red virtual es una representación de su propia red en la nube de Hola. Una red virtual es un aislamiento lógico de hello nube de Azure dedicada tooyour suscripción. También puede conectar la red local de tooyour de redes virtuales. Hola siguiente muestra algunas de las funcionalidades de Hola de hello servicio de red Virtual de Azure:

![Diagrama de red](./media/virtual-networks-overview/virtual-network-overview.png)

toolearn más información acerca de hello siguiendo las capacidades de red Virtual de Azure, haga clic en la capacidad de hello:
- **[Aislamiento:](#isolation)** las redes virtuales están completamente aisladas entre sí. Puede crear redes virtuales independientes para el desarrollo, pruebas y producción ese Hola use bloques de direcciones CIDR mismo. Por el contrario, puede crear varias redes virtuales que usan diferentes bloques de direcciones CIDR y que conectan redes entre sí. También puede segmentar una red virtual en varias subredes. Azure proporciona resolución de nombres interna para las máquinas virtuales y las instancias de rol de servicios de nube conectado tooa red virtual. Opcionalmente puede configurar una red virtual toouse sus propios servidores DNS, en lugar de utilizar la resolución de nombres interna Azure.
- **[Conectividad a Internet:](#internet)**  instancias de rol de todas las máquinas virtuales (VM) de Azure y servicios en la nube conectado tooa red virtual tiene acceso a toohello Internet, de forma predeterminada. También puede habilitar recursos de toospecific de acceso de entrada, según sea necesario.
- **[Conectividad de los recursos de Azure:](#within-vnet)**  recursos de Azure como servicios en la nube y máquinas virtuales pueden ser toohello conectado misma red virtual. los recursos de Hello pueden conectarse tooeach otro uso privado de direcciones IP, incluso si están en subredes diferentes. Azure proporciona el enrutamiento predeterminado entre subredes, las redes virtuales y redes locales, por lo que no tiene tooconfigure y administrar rutas.
- **[Conectividad de red virtual:](#connect-vnets)**  redes virtuales pueden ser conectado tooeach otros, habilitar recursos conectado tooany toocommunicate de red virtual con cualquier recurso de cualquier otra red virtual.
- **[Conectividad local:](#connect-on-premises)**  redes virtuales pueden ser redes de local tooon conectado a través de conexiones de red privada entre la red y Azure, o a través de una conexión de VPN de sitio a sitio a través de Internet de Hola.
- **[Filtrado de tráfico:](#filtering)** el tráfico de red de entrada y salida de las instancias de rol de Cloud Services y máquinas virtuales se puede filtrar por dirección IP y puerto de origen, dirección IP y puerto de destino, y por protocolo.
- **[Enrutamiento:](#routing)** opcionalmente, puede invalidar el enrutamiento predeterminado de Azure mediante la configuración de sus propias rutas, o mediante el uso de rutas BGP a través de una puerta de enlace de red.

## <a name = "isolation"></a>Aislamiento de red y segmentación

Puede implementar varias redes virtuales dentro de cada [suscripción](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) y [región](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#region) de Azure. Cada red virtual está aislada de otras redes virtuales. Para cada red virtual, puede:
- Especificar un espacio de direcciones IP privado personalizado mediante direcciones públicas y privadas (RFC 1918). Azure asigna recursos conectados toohello red virtual una dirección IP privada del espacio de direcciones de Hola que asigna.
- Hola red virtual en una o varias subredes de segmento y asignar una parte de la subred tooeach espacio de direcciones IP Hola red virtual.
- Utilizar la resolución de nombres que proporciona Azure o especifique su propio servidor DNS para su uso por los recursos de conecta tooa red virtual. más información acerca de la resolución de nombres en redes virtuales, leer hello toolearn [la resolución de nombres para máquinas virtuales y servicios en la nube](virtual-networks-name-resolution-for-vms-and-role-instances.md) artículo.

## <a name = "internet"></a>Conectar toohello Internet
Todos los recursos de tooa conectado red virtual tiene conectividad saliente toohello Internet de forma predeterminada. dirección IP privada de Hello del recurso de hello es la dirección de red de origen convierte la dirección IP pública de (SNAT) tooa Hola infraestructura de Azure. más información acerca de la conectividad saliente de Internet, leer hello toolearn [descripción de las conexiones salientes en Azure](..\load-balancer\load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json#standalone-vm-with-no-instance-level-public-ip-address) artículo. Puede cambiar conectividad de hello predeterminado mediante la implementación de enrutamiento personalizado y filtrado de tráfico.

toocommunicate entrante tooAzure recursos de Internet de Hola o toocommunicate toohello saliente Internet sin SNAT, un recurso debe asignarse a una dirección IP pública. más información acerca de las direcciones IP públicas, leer hello toolearn [direcciones IP públicas](virtual-network-public-ip-address.md) artículo.

## <a name="within-vnet"></a>Conexión de recursos de Azure
Puede conectar varios recursos de Azure tooa red virtual, como máquinas virtuales (VM), servicios en la nube, entornos del servicio de aplicación y conjuntos de escalas de máquina Virtual. Máquinas virtuales conectan tooa subred dentro de una red virtual a través de una interfaz de red (NIC). más información sobre los NIC, leer hello toolearn [interfaces de red](virtual-network-network-interface.md) artículo.

## <a name="connect-vnets"></a>Conexión de redes virtuales

Puede conectar redes virtuales tooeach otros, habilitar recursos conectados tooeither toocommunicate de red virtual entre sí a través de redes virtuales. Puede utilizar uno o ambos de hello después opciones tooconnect redes virtuales tooeach otros:
- **Emparejamiento:** habilita recursos conectado toodifferent redes virtuales de Azure en hello mismo toocommunicate de ubicación de Azure entre sí. Hello ancho de banda y latencia de hello redes virtuales está Hola mismo como si fueron de los recursos de hello toohello conectado misma red virtual. toolearn más sobre el emparejamiento, leer hello [intercambio de tráfico de red Virtual](virtual-network-peering-overview.md) artículo.
- **Conexión de red virtual a red virtual:** habilita recursos conectado toodifferent red virtual de Azure en hello mismas o diferentes ubicaciones de Azure. A diferencia del emparejamiento, el ancho de banda es limitado entre las redes virtuales porque el tráfico debe pasar a través de una instancia de Azure VPN Gateway. toolearn más acerca de cómo conectar redes virtuales con una conexión de red virtual a red virtual, leer hello [configurar una conexión de red virtual a red virtual](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo.

## <a name="connect-on-premises"></a>Conectar la red local de tooan

Puede conectar su tooa de red local red virtual con cualquier combinación de hello siguientes opciones:
- **Red privada virtual (VPN) de Point-to-site:** entre una sola red de tooyour conectado de PC y Hola red virtual. Este tipo de conexión es excelente si principiante con Azure, o para los desarrolladores, ya que requiere poca o ninguna red existente de tooyour de cambios. conexión Hola utiliza la comunicación de tooprovide cifrado de protocolo de hello SSTP sobre Hola Internet entre Hola PC y Hola red virtual. latencia de Hello una VPN de sitio a punto es imprevisible, ya que Hola tráfico que atraviesa Hola Internet.
- **VPN de sitio a sitio:** se establece entre el dispositivo VPN y una instancia de Azure VPN Gateway. Este tipo de conexión permite a cualquier recurso local autorizar tooaccess una red virtual. conexión de Hello es una VPN de IPSec/IKE que proporciona comunicación cifrada con respecto a Hola Internet entre el dispositivo local y la puerta de enlace de VPN de Azure de Hola. latencia de Hola para una conexión de sitio a sitio es impredecible, puesto que Hola tráfico que atraviesa Hola Internet.
- **Azure ExpressRoute:** establecida entre la red y Azure, a través de un asociado de ExpressRoute. Esta conexión es privada. El tráfico no atraviesa Hola Internet. latencia de Hola para una conexión ExpressRoute es predecible, puesto que el tráfico no atraviesan Hola Internet.

más información acerca de todas las opciones de conexión anterior de hello, leer hello toolearn [diagramas de topología de conexión](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#diagrams) artículo.

## <a name="filtering"></a>Filtrado del tráfico de red
Puede filtrar el tráfico de red entre subredes con uno o ambos de hello siguientes opciones:
- **Grupos de seguridad (NSG) de red:** cada NSG puede contener varias reglas de seguridad entrante y saliente que le permiten tráfico de toofilter por dirección IP de origen y destino, puerto y protocolo. Puede aplicar un tooeach NSG NIC en una máquina virtual. También puede aplicar una subred de toohello NSG una NIC u otros recursos de Azure, está conectado a. más información acerca de los NSG, leer hello toolearn [grupos de seguridad de red](virtual-networks-nsg.md) artículo.
- **Dispositivos virtuales de red (NVA):** un dispositivo virtual de red es una máquina virtual que ejecuta software que realiza una función de red, como un firewall. Ver una lista de NVAs disponibles en hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances). Los dispositivos virtuales de red también están disponibles para proporcionar la optimización de la WAN y otras funciones de tráfico de red. Los dispositivos virtuales de red normalmente se usan con rutas BGP o definidas por el usuario. También puede utilizar un tráfico de toofilter NVA entre redes virtuales.

## <a name="routing"></a>Redirección del tráfico de red

Azure crea tablas de rutas que habilite recursos tooany conectado subred en cualquier toocommunicate de red virtual entre sí, de forma predeterminada. Puede implementar uno o ambos Hola después opciones toooverride hello Azure crea las rutas predeterminadas:
- **Las rutas definidas por el usuario:** puede crear tablas de enrutamiento personalizadas con rutas que controlan donde el tráfico es enrutado toofor cada subred. más información acerca de las rutas definidas por el usuario, leer hello toolearn [rutas definidas por el usuario](virtual-networks-udr-overview.md) artículo.
- **Las rutas BGP:** si se conecta a la red de red virtual tooyour local mediante una conexión de puerta de enlace de VPN de Azure o ExpressRoute, puede propagar tooyour de rutas BGP redes virtuales.

## <a name="pricing"></a>Precios

No hay ningún cargo por redes virtuales, subredes, tablas de rutas o grupos de seguridad de red. El uso del ancho de banda saliente de Internet, las direcciones IP públicas, el emparejamiento de redes virtuales, puertas de enlace VPN y ExpressRoute tienen sus propias estructuras de precios. Hola de vista [red Virtual](https://azure.microsoft.com/pricing/details/virtual-network), [puerta de enlace VPN](https://azure.microsoft.com/pricing/details/vpn-gateway), y [ExpressRoute](https://azure.microsoft.com/pricing/details/expressroute) precios páginas para obtener más información.

## <a name="faq"></a>P+F

tooreview preguntas más frecuentes acerca de la red Virtual, vea hello [P+F de red Virtual](virtual-networks-faq.md) artículo.


## <a name="next-steps"></a>Pasos siguientes

- Crear la red virtual de primera y conectar unos tooit de máquinas virtuales, siguiendo los pasos de Hola Hola [crear la primera red virtual](virtual-network-get-started-vnet-subnet.md) artículo.
- Crear una red virtual de sitio de punto de conexión tooa siguiendo los pasos de Hola Hola [configurar una conexión punto a sitio](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo.
- Obtener información sobre algunas de hello otra clave [capacidades de red](../networking/networking-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) de Azure.
