---
title: Seguridad de red aaaAzure | Documentos de Microsoft
description: "Obtenga información acerca de los servicios informáticos en la nube que incluyen una amplia selección de instancias de proceso y servicios que se pueden escalar arriba y abajo automáticamente toomeet hello las necesidades de su aplicación o enterprise."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2017
ms.author: TomSh
ms.openlocfilehash: 7dae83bbe338a2727575447583a7fb773527dd59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security"></a>Azure Network Security

Somos conscientes de que la seguridad es trabajo en la nube de Hola y la importancia que tiene que buscar información precisa y oportuna sobre la seguridad de Azure. Uno de hello mejor motivos toouse Azure para las aplicaciones y servicios es tootake aprovechar la amplia gama de herramientas de seguridad y las capacidades de Azure. Estas herramientas y capacidades de ayudan que sea posible toocreate soluciones seguras en hello plataforma Windows Azure.

Microsoft Azure proporciona confidencialidad, integridad y disponibilidad para los datos del cliente, al mismo tiempo que hace posible una responsabilidad transparente. toohelp entender mejor colección Hola de controles de seguridad de red implementados en Microsoft Azure desde la perspectiva del cliente de hello, este artículo, "Seguridad de red de Azure", se escribe tooprovide información completa sobre seguridad de la red de Hola controles disponibles con Microsoft Azure.

Este documento está pensado tooinform acerca de la amplia gama de Hola de red controla que puede configurar la seguridad de hello tooenhance de implementar las soluciones de hello en Azure. Si está interesado en qué Microsoft does tejido de red toosecure Hola de Hola misma plataforma de Azure, consulte la sección de seguridad de Azure Hola Hola [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/azure-security).

## <a name="azure-platform"></a>Plataforma Azure

Azure es una plataforma de servicios en la nube pública que admite una amplia selección de sistemas operativos, lenguajes de programación, plataformas, herramientas, bases de datos y dispositivos.  Puede ejecutar contenedores de Linux con integración de Docker, compilar aplicaciones con JavaScript, Python, .NET, PHP, Java, Node.js y crear back-ends para dispositivos iOS, Android y Windows. Servicios de nube de Azure admiten Hola mismas tecnologías millones de desarrolladores y profesionales de TI ya se basan en y de confianza.

Al compilar en, o migrar los activos de TI a un proveedor de servicios de nube pública, está confiando en tooprotect de capacidades de la organización a las aplicaciones y datos con Hola controles hello y servicios que proporcionan una seguridad de hello toomanage de basados en la nube activos.

Diseño de la infraestructura de Azure de hello facility tooapplications para hospedar simultáneamente millones de clientes y proporciona una base de confianza en los que las empresas pueden satisfacer sus requisitos de seguridad. Además, Azure le proporciona una amplia colección de toocontrol de capacidad de hello y opciones de seguridad configurables usarlas para que puedan personalizar requisitos únicos Hola de seguridad toomeet de las implementaciones de su organización.

## <a name="abstract"></a>Descripción breve

Servicios en la nube pública de Microsoft ofrece servicios e infraestructura a gran escala, funcionalidades de calidad empresarial y numerosas opciones de conectividad híbrida. Puede elegir tooaccess estos servicios a través de Internet de Hola o con ExpressRoute de Azure, que proporciona conectividad de red privada. plataforma de Microsoft Azure Hola permite tooseamlessly ampliar la infraestructura en la nube de Hola y crear arquitecturas de varios niveles. Además, otros fabricantes pueden habilitar funcionalidades mejoradas mediante servicios de seguridad y dispositivos virtuales.

Los servicios de red de Azure permiten maximizar la flexibilidad, disponibilidad, resistencia, seguridad e integridad por diseño. Este documento proporciona detalles sobre las funciones de red Hola de Azure y obtener información acerca de cómo los clientes pueden usar toohelp de características de seguridad nativa de Azure protegen sus activos de información.

Hola dirigida audiencias para estas notas del producto incluyen:

- Administradores técnicos, administradores de red y desarrolladores que buscan soluciones de seguridad que estén disponibles y sean compatibles con Azure.

-   PYME o ejecutivos de proceso de negocio que desean tooget general Hola tecnologías de red de Azure y servicios que son relevantes en discusiones en torno a la seguridad de red en hello nube pública de Azure.

## <a name="azure-networking-big-picture"></a>Panorama general de las redes de Azure
Microsoft Azure incluye una sólida toosupport de infraestructura de red de su aplicación y los requisitos de conectividad de servicio. Conectividad de red es posible entre los recursos ubicados en Azure, entre locales y recursos y tooand de hello Internet y Azure hospedado de Azure.

![Panorama general de las redes de Azure](media/azure-network-security/azure-network-security-fig-1.png)

Hola [infraestructura de red de Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-networking-guidelines) permite toosecurely conectar otro tooeach de recursos de Azure con redes virtuales (redes virtuales). Una red virtual es una representación de su propia red en la nube de Hola. Una red virtual es lógico de aislamiento de red dedicada tooyour suscripción de hello nube de Azure. Puede conectar redes locales de redes virtuales tooyour.

Azure es compatible con dedicado de red de un vínculo WAN conectividad tooyour local y una red Virtual de Azure con [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction). vínculo de Hello entre Azure y el sitio utiliza una conexión dedicada que no pasa por hello Internet pública. Si su aplicación de Azure se ejecuta en varios centros de datos, puede usar [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) tooroute solicitudes procedentes de usuarios cambien en todas las instancias de la aplicación hello. También es posible distribuir tooservices de tráfico que no se ejecutan en Azure si son accesibles desde Internet Hola.

## <a name="enterprise-view-of-azure-networking-components"></a>Información empresarial sobre los componentes de red de Azure
Azure tiene muchos componentes de red que son relevantes toonetwork discusiones de seguridad. se describen estos componentes de red y centrarse en la seguridad de hello emite toothem relacionado.

> [!Note]
> No todos los aspectos de redes de Azure se describen, se explican los considera toobe esencial en planear y diseñar una infraestructura de red segura alrededor de los servicios y las aplicaciones que implemente en Azure.

En este documento, será Hola de portada después Azure capacidades empresariales de red:

-   Conectividad de red básica

-   Conectividad híbrida

-   Controles de seguridad

-   Validación de la red

### <a name="basic-network-connectivity"></a>Conectividad de red básica

Hola [red Virtual de Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) habilita el servicio toosecurely conectar otro tooeach de recursos de Azure con redes virtuales (VNet). Una red virtual es una representación de su propia red en la nube de Hola. Una red virtual es un aislamiento lógico de hello Azure red infraestructura dedicada tooyour suscripción. También puede conectar redes virtuales tooeach otros y tooyour redes mediante VPN de sitio a sitio local y dedicado [vínculos WAN](https://docs.microsoft.com/azure/expressroute/expressroute-introduction).

![Conectividad de red básica](media/azure-network-security/azure-network-security-fig-2.png)

Con hello comprender que usan servidores toohost de máquinas virtuales en Azure, pregunta hello es cómo conectan los tooa red en esas máquinas virtuales. Hello respuesta es que las máquinas virtuales conectan tooan [red Virtual de Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview).

Redes virtuales de Azure son como Hola virtual redes se usa en local con sus propias soluciones de plataforma de virtualización, como Microsoft Hyper-V o VMware.

#### <a name="intra-vnet-connectivity"></a>Conectividad entre redes virtuales

Puede conectar redes virtuales tooeach otros, habilitar recursos conectados tooeither toocommunicate de red virtual entre sí a través de redes virtuales. Puede utilizar uno o ambos de hello después opciones tooconnect redes virtuales tooeach otros:

- **Emparejamiento:** habilita recursos conectado toodifferent redes virtuales de Azure en hello mismo toocommunicate de ubicación de Azure entre sí. Hello ancho de banda y latencia de hello red virtual está Hola mismo como si fueron de los recursos de hello toohello conectado misma red virtual. leer toolearn más sobre el emparejamiento, [intercambio de tráfico de red Virtual](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

 ![Emparejamiento](media/azure-network-security/azure-network-security-fig-3.png)

- **Conexión de red virtual a red virtual:** habilita recursos conectado toodifferent red virtual de Azure en hello mismas o diferentes ubicaciones de Azure. A diferencia del emparejamiento, el ancho de banda es limitado entre las redes virtuales porque el tráfico debe pasar a través de una instancia de Azure VPN Gateway.

![Conexión de red virtual a red virtual](media/azure-network-security/azure-network-security-fig-4.png)


toolearn más acerca de cómo conectar redes virtuales con una conexión de red virtual a red virtual, leer hello [configurar un artículo de la conexión de red virtual a red virtual](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal?toc=%2fazure%2fvirtual-network%2ftoc.json).

#### <a name="azure-virtual-network-capabilities"></a>Funcionalidades de Azure Virtual Network:

Como puede ver, una red Virtual de Azure proporciona máquinas virtuales tooconnect toohello red para que puedan conectarse a recursos de red de tooother de forma segura. Sin embargo, la conectividad básica es principio simplemente Hola. Hello siguientes capacidades de servicio de red Virtual de Azure hello exponen las características de seguridad de red Virtual de Azure hello:

-   Aislamiento

-   Conectividad de Internet

-   Conectividad de recursos de Azure

-   Conectividad de red virtual

-   Conectividad local

-   Filtrado de tráfico

-   Enrutamiento

**Aislamiento**

Las redes virtuales están completamente [aisladas](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) entre sí. Puede crear redes virtuales independientes para el desarrollo, pruebas y producción que use Hola igual [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) bloques de direcciones. Por el contrario, puede crear varias redes virtuales que usan diferentes bloques de direcciones CIDR y que conectan redes entre sí. También puede segmentar una red virtual en varias subredes.

Azure proporciona resolución de nombres interna para las máquinas virtuales y [servicios en la nube](https://azure.microsoft.com/services/cloud-services/) instancias de rol conectado tooa red virtual. Opcionalmente puede configurar una red virtual toouse sus propios servidores DNS, en lugar de utilizar la resolución de nombres interna Azure.

Puede implementar varias redes virtuales dentro de cada [suscripción](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology?toc=%2fazure%2fvirtual-network%2ftoc.json) y [región](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology?toc=%2fazure%2fvirtual-network%2ftoc.json) de Azure. Cada red virtual está aislada de otras redes virtuales. Para cada red virtual, puede:

-   Especificar un espacio de direcciones IP privado personalizado mediante direcciones públicas y privadas (RFC 1918). Azure asigna recursos conectados toohello red virtual una dirección IP privada del espacio de direcciones de hello, asignar.

-   Hola red virtual en una o varias subredes de segmento y asignar una parte de la subred tooeach espacio de direcciones IP Hola red virtual.

-   Utilizar la resolución de nombres que proporciona Azure o especifique su propio servidor DNS para su uso por los recursos de conecta tooa red virtual. más información acerca de la resolución de nombres en redes virtuales, leer hello toolearn [la resolución de nombres para máquinas virtuales y servicios en la nube](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances).

**Conectividad de Internet**

Todos los [máquinas virtuales (VM) de Azure](https://docs.microsoft.com/azure/virtual-machines/windows/) e instancias de rol de servicios de nube conectado tooa red virtual tiene acceso a toohello Internet, de forma predeterminada. También puede habilitar recursos de toospecific de acceso de entrada, según sea necesario. (VM) e instancias de rol de servicios de nube conectado tooa red virtual tiene acceso a toohello Internet, de forma predeterminada. También puede habilitar recursos de toospecific de acceso de entrada, según sea necesario.

Todos los recursos de tooa conectado red virtual tiene conectividad saliente toohello Internet de forma predeterminada. dirección IP privada de Hello del recurso de hello es la dirección de red de origen convierte la dirección IP pública de (SNAT) tooa Hola infraestructura de Azure. Puede cambiar conectividad de hello predeterminado mediante la implementación de enrutamiento personalizado y filtrado de tráfico. más información acerca de la conectividad saliente de Internet, leer hello toolearn [descripción de las conexiones salientes en Azure](https://docs.microsoft.com/azure/load-balancer/load-balancer-outbound-connections?toc=%2fazure%2fvirtual-network%2ftoc.json).

toocommunicate entrante tooAzure recursos de Internet de Hola o toocommunicate toohello saliente Internet sin SNAT, un recurso debe asignarse a una dirección IP pública. más información acerca de las direcciones IP públicas, leer hello toolearn [direcciones IP públicas](https://docs.microsoft.com/azure/virtual-network/virtual-network-public-ip-address).

**Conectividad de recursos de Azure**

[Recursos de Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) como servicios en la nube y máquinas virtuales pueden estar conectado toohello misma red virtual. los recursos de Hello pueden conectarse tooeach otro uso privado de direcciones IP, incluso si están en subredes diferentes. Azure proporciona el enrutamiento predeterminado entre subredes, las redes virtuales y redes locales, por lo que no tiene tooconfigure y administrar rutas.

Puede conectar varios recursos de Azure tooa red virtual, como máquinas virtuales (VM), servicios en la nube, entornos del servicio de aplicación y conjuntos de escalas de máquina Virtual. Máquinas virtuales conectan tooa subred dentro de una red virtual a través de una interfaz de red (NIC). más información sobre los NIC, leer hello toolearn [interfaces de red](https://docs.microsoft.com/azure/virtual-network/virtual-network-network-interface).

**Conectividad de red virtual**

[Redes virtuales](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) puede ser tooeach conectado otros, habilitar recursos conectado tooany toocommunicate de red virtual con cualquier recurso de cualquier otra red virtual.

Puede conectar redes virtuales tooeach otros, habilitar recursos conectados tooeither toocommunicate de red virtual entre sí a través de redes virtuales. Puede utilizar uno o ambos de hello después opciones tooconnect redes virtuales tooeach otros:

- **Emparejamiento:** habilita recursos conectado toodifferent redes virtuales de Azure en hello mismo toocommunicate de ubicación de Azure entre sí. Hello ancho de banda y latencia de hello redes virtuales se Hola igual que si los recursos de hello estaban conectado toohello mismo VNet.toolearn más sobre el emparejamiento, leer hello [intercambio de tráfico de red Virtual](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

- **Conexión de red virtual a red virtual:** habilita recursos conectado toodifferent red virtual de Azure en hello mismas o diferentes ubicaciones de Azure. A diferencia del emparejamiento, el ancho de banda es limitado entre las redes virtuales porque el tráfico debe pasar a través de una instancia de Azure VPN Gateway. toolearn más acerca de cómo conectar redes virtuales con una conexión de red virtual a red virtual. toolearn leer más, hello [configurar una conexión de red virtual a red virtual](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal?toc=%2fazure%2fvirtual-network%2ftoc.json) .

**Conectividad local**

Se pueden conectar redes virtuales demasiado[local](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) redes a través de conexiones de red privada entre la red y Azure, o a través de una conexión de VPN de sitio a sitio a través de Internet de Hola.

Puede conectar su tooa de red local red virtual con cualquier combinación de hello siguientes opciones:

- **Red privada virtual (VPN) de Point-to-site:** entre una sola red de tooyour conectado de PC y Hola red virtual. Este tipo de conexión es excelente si principiante con Azure, o para los desarrolladores, ya que requiere poca o ninguna red existente de tooyour de cambios. conexión Hola utiliza la comunicación de tooprovide cifrado de protocolo de hello SSTP sobre Hola Internet entre Hola PC y Hola red virtual. latencia Hola una VPN de sitio a punto es impredecible desde Hola tráfico que atraviesa Hola Internet.

- **VPN de sitio a sitio:** se establece entre el dispositivo VPN y una instancia de Azure VPN Gateway. Este tipo de conexión permite a cualquier recurso local autorizar tooaccess una red virtual. conexión de Hello es una VPN de IPsec/IKE que proporciona comunicación cifrada con respecto a Hola Internet entre el dispositivo local y la puerta de enlace de VPN de Azure de Hola. latencia de Hola para una conexión de sitio a sitio es impredecible desde Hola tráfico que atraviesa Hola Internet.

- **Azure ExpressRoute:** establecida entre la red y Azure, a través de un asociado de ExpressRoute. Esta conexión es privada. El tráfico no atraviesa Hola Internet. latencia de Hola para una conexión ExpressRoute es predecible, puesto que el tráfico no atraviesan Hola Internet. más información acerca de todas las opciones de conexión anterior de hello, leer hello toolearn [diagramas de topología de conexión](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%2fazure%2fvirtual-network%2ftoc.json).

**Filtrado de tráfico**

El [tráfico de red](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) de entrada y salida de las instancias de rol de Cloud Services y máquinas virtuales se puede filtrar por dirección IP y puerto de origen, dirección IP y puerto de destino, y por protocolo.

Puede filtrar el tráfico de red entre subredes con uno o ambos de hello siguientes opciones:

- **Grupos de seguridad (NSG) de red:** cada NSG puede contener varias reglas de seguridad entrante y saliente que le permiten tráfico de toofilter por dirección IP de origen y destino, puerto y protocolo. Puede aplicar un tooeach NSG NIC en una máquina virtual. También puede aplicar una subred de toohello NSG una NIC u otros recursos de Azure, está conectado a. más información acerca de los NSG, leer hello toolearn [grupos de seguridad de red](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg).

- **Aplicaciones de red virtual:** una aplicación de red virtual es una máquina virtual que ejecuta software que realiza una función de red, como un firewall. Ver una lista de NVAs disponibles en hello Azure Marketplace. Los dispositivos virtuales de red también están disponibles para proporcionar la optimización de la WAN y otras funciones de tráfico de red. Los dispositivos virtuales de red normalmente se usan con rutas BGP o definidas por el usuario. También puede utilizar un tráfico de toofilter NVA entre redes virtuales.

**Enrutamiento**

Opcionalmente, puede invalidar el enrutamiento predeterminado de Azure mediante la configuración de sus propias rutas, o mediante el uso de rutas BGP a través de una puerta de enlace de red.

Azure crea tablas de rutas que habilite recursos tooany conectado subred en cualquier toocommunicate de red virtual entre sí, de forma predeterminada. Puede implementar uno o ambos Hola después opciones toooverride hello Azure crea las rutas predeterminadas:

- **Las rutas definidas por el usuario:** puede crear tablas de enrutamiento personalizadas con rutas que controlan donde el tráfico es enrutado toofor cada subred. más información acerca de las rutas definidas por el usuario, leer hello toolearn [rutas definidas por el usuario](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview).

- **Las rutas BGP:** si se conecta a la red de red virtual tooyour local mediante una conexión de puerta de enlace de VPN de Azure o ExpressRoute, puede propagar tooyour de rutas BGP redes virtuales.

### <a name="hybrid-internet-connectivity-connect-tooan-on-premises-network"></a>Conectividad a internet híbrido: conectar la red local de tooan
Puede conectar su tooa de red local red virtual con cualquier combinación de hello siguientes opciones:

-   Conectividad de Internet

-   VPN de punto a sitio (VPN P2S)

-   VPN de sitio a sitio (VPN S2S)

-   ExpressRoute

#### <a name="internet-connectivity"></a>Conectividad de Internet

Como sugiere su nombre, conectividad a Internet hace que las cargas de trabajo accesible desde Internet, Hola manteniendo exponer tooworkloads diferentes extremos públicos que se encuentran dentro de la red virtual de Hola. Estas cargas de trabajo podrían exponerse mediante [equilibrador de carga a través de Internet](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview) o simplemente asignando una IP pública de direcciones toohello máquina virtual. De esta manera, es posible que para cualquier cosa en hello Internet toobe pueda tooreach esa máquina virtual, proporcionan un firewall de host, [grupos de seguridad (NSG) de red](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg), y [rutas definidas por el usuario](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) permitir que toohappen.

En este escenario, podría exponer una aplicación que necesite toobe pública toohello Internet y ser capaz de tooconnect tooit de en cualquier lugar, o desde ubicaciones específicas según la configuración de Hola de las cargas de trabajo.

#### <a name="point-to-site-vpn-or-site-to-site-vpn"></a>VPN de punto a sitio o de sitio a sitio
Estos dos pertenecen a Hola misma categoría. Necesitan la puerta de enlace VPN de red virtual toohave y se puede conectar tooit mediante un cliente de VPN para la estación de trabajo como parte del programa Hola [configuraciónPoint-to-Site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) o puede configurar el entorno local [dispositivo VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) toobe capaz tooterminate una VPN de sitio a sitio. De esta manera, dispositivos locales pueden conectarse tooresources dentro de hello red virtual.

Una configuración de punto a sitio (P2S) le permite crear una conexión segura en una red virtual de la tooa de equipos cliente individuales. P2S es una conexión VPN sobre SSTP (Protocolo de túnel de sockets seguros).

![VPN de punto a sitio](media/azure-network-security/azure-network-security-fig-5.png)

Conexiones de punto a sitio son útiles cuando desea tooconnect tooyour red virtual desde una ubicación remota, como desde casa o un centro de conferencias, o si solo tiene unos pocos clientes que precisan de red virtual de tooconnect tooa.

Las conexiones P2S no requieren un dispositivo VPN ni una dirección IP pública. Establecer conexión de VPN de Hola desde el equipo cliente de Hola. Por lo tanto, P2S no se recomienda forma tooconnect tooAzure por si necesita una conexión persistente de muchos dispositivos locales y equipos tooyour red de Azure.

![VPN de sitio a sitio](media/azure-network-security/azure-network-security-fig-6.png)

> [!Note]
> Para obtener más información acerca de las conexiones punto a sitio, vea hello [Point-to-Site FA v preguntas](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-classic-azure-portal).

Una conexión de puerta de enlace VPN de sitio a sitio es tooconnect utilizado en sus instalaciones de red tooan red virtual de Azure a través de un túnel VPN de IPsec/IKE (IKEv1 o IKEv2).

Este tipo de conexión requiere una VPN dispositivo situado en local que tiene un tooit de dirección asignada de IP pública con orientación externa. Esta conexión tiene lugar en Hola Internet y le permite demasiado "tunelizar" información dentro de un vínculo entre la red y Azure cifrado. La VPN de sitio a sitio es una tecnología segura y madura que empresas de todos los tamaños han implementado durante décadas. El cifrado del túnel se realiza con el [modo de túnel IPsec](https://technet.microsoft.com/library/cc786385.aspx).

Mientras VPN de sitio a sitio es una tecnología de confianza, confiable y establecida, tráfico de túnel de hello atravesar Hola Internet. Además, el ancho de banda es relativamente limitada tooa máximo de aproximadamente 200 Mbps.

Si necesita un nivel de seguridad o de rendimiento excepcional para las conexiones entre locales, se recomienda utilizar Azure ExpressRoute para su conectividad. ExpressRoute es un vínculo de WAN dedicada entre su ubicación local o un proveedor de hospedaje de Exchange. Porque se trata de una conexión de telecomunicaciones, los datos no se transmiten a través de Internet de Hola y es, por tanto, no se expone toohello posibles riesgos inherentes a las comunicaciones de Internet.

> [!Note]
> Para más información acerca de las puertas de enlace VPN, consulte [Acerca de VPN Gateway](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).

#### <a name="dedicated-wan-link"></a>Vínculo WAN dedicado
Microsoft Azure ExpressRoute le permite ampliar sus redes locales en hello Azure a través de una conexión privada dedicada que se realiza mediante un proveedor de conectividad.

Las conexiones ExpressRoute no pasan por hello Internet pública. Esto permite toooffer las conexiones de ExpressRoute, más confiabilidad, velocidades más rápidas, latencias más bajas y mayor seguridad que las típicas conexiones a través de Internet de Hola.

![ Vínculo WAN dedicado](media/azure-network-security/azure-network-security-fig-7.png)

> [!Note]
> Para obtener información acerca de cómo tooconnect su tooMicrosoft de red con ExpressRoute, consulte [modelos de conectividad de ExpressRoute](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) y [información general técnica de ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction).

Como con opciones de VPN de sitio a sitio de hello, ExpressRoute también le permite tooresources tooconnect que no son necesariamente solo una red virtual. De hecho, función hello SKU, puede conectar redes virtuales too10. Si tienes hello [complemento premium](https://docs.microsoft.com/azure/expressroute/expressroute-faqs), las conexiones tooup too100 las redes virtuales son posibles, según el ancho de banda. más información sobre lo que estos tipos de apariencia de las conexiones, como, leer toolearn [diagramas de topología de conexión](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%2fazure%2fvirtual-network%2ftoc.json).

### <a name="security-controls"></a>Controles de seguridad
Una instancia de Azure Virtual Network proporciona una red lógica y segura que está aislada de otras redes virtuales y es compatible con muchos controles de seguridad que se usan en las redes locales. Los clientes crear su propia estructura, utilizando: subredes, utilice su propio intervalo de direcciones IP privadas, configurar tablas de rutas, grupos de seguridad de red de control de acceso (ACL) de listas, puertas de enlace y aparatos virtuales toorun sus cargas de trabajo en la nube de Hola.

siguiente Hola es controles de seguridad que puede usar en las redes virtuales de Azure:

-   Controles de acceso a la red

-   Rutas definidas por el usuario

-   Aplicación de seguridad de red

-   Application Gateway

-   Firewall de aplicaciones web de Azure

-   Control de disponibilidad de red

#### <a name="network-access-controls"></a>Controles de acceso a la red
Aunque Hola red Virtual de Azure (VNet) es la piedra angular de hello del modelo de red de Azure y proporciona aislamiento y protección, Hola [grupos de seguridad de red (NSG)](https://blogs.msdn.microsoft.com/igorpag/2016/05/14/azure-network-security-groups-nsg-best-practices-and-lessons-learned/) son Hola principal de la herramienta que use tooenforce y controlar el tráfico de red reglas de Hola a nivel de red.

![ Controles de acceso a la red](media/azure-network-security/azure-network-security-fig-8.png)


Puede controlar el acceso permitir o denegar la comunicación entre las cargas de trabajo de hello en una red virtual, de los sistemas de redes del cliente a través de la conectividad entre entornos, o dirigir la comunicación de Internet.

En el diagrama de hello, redes virtuales y los NSG residen en una capa específica de la pila de seguridad general Azure hello, donde los NSG, UDR y dispositivos de red virtual pueden ser usado toocreate seguridad límites tooprotect hello las implementaciones de aplicaciones en red Hola protegido.

Los NSG utilizan un tráfico de tooevaluate de tupla de 5 (y se utilizan en las reglas de Hola que configure para hello NSG):

-   [Dirección IP de origen y destino](https://support.microsoft.com/help/969029/the-functionality-for-source-ip-address-selection-in-windows-server-2008-and-in-windows-vista-differs-from-the-corresponding-functionality-in-earlier-versions-of-windows)

-   [Puerto de origen y destino](https://technet.microsoft.com/library/dd197515)

-   Protocolo: [Protocolo de control de transmisión (TCP)](https://technet.microsoft.com/library/cc940037.aspx) o [Protocolo de datagramas de usuario (UDP)](https://technet.microsoft.com/library/cc940034.aspx)

Esto significa que puede controlar el acceso entre una sola máquina virtual y un grupo de máquinas virtuales o una sola tooanother de máquina virtual única máquina virtual, o entre subredes enteras. De nuevo, tenga en cuenta que esto es simplemente un filtrado de paquetes con estado, no una inspección de paquetes completa. No hay ninguna validación de protocolo ni funcionalidad IDS o IPS de nivel de red en un grupo de seguridad de red.

Un grupo de seguridad de red incluye algunas reglas integradas que debe tener en cuenta. Dichos componentes son:

-   **Permitir todo el tráfico dentro de una red virtual específica:** todas las máquinas virtuales en hello misma red Virtual de Azure pueden comunicarse entre sí.

-   **Permitir tooinbound de equilibrio de carga de Azure:** esta regla permite el tráfico procedente de cualquier dirección de destino de origen dirección tooany hello Azure equilibrador de carga.

-   **Denegar todo el tráfico entrante:** esta regla bloquea todo el tráfico de origen de hello Internet que haya permitido explícitamente.

-   **Permitir todo el tráfico a salida toohello Internet:** esta regla permite que las máquinas virtuales tooinitiate conexiones toohello Internet. Si no desea que estas conexiones iniciadas, necesita toocreate un tooblock de regla esas conexiones o aplicar la tunelización forzada.

#### <a name="system-routes-and-user-defined-routes"></a>Rutas de sistema y rutas definidas por el usuario

Cuando se agrega la red virtual de máquinas virtuales (VM) tooa (VNet) en Azure, verá que hello las máquinas virtuales están capaz de toocommunicate entre sí a través de la red hello, automáticamente. No es necesario toospecify una puerta de enlace, incluso aunque hello las máquinas virtuales están en subredes diferentes.

Hello mismo sirve para la comunicación de hello las máquinas virtuales toohello Internet pública y la red local de tooyour incluso cuando el propietario de una conexión híbrida de Azure tooyour centro de datos está presente.

![Rutas del sistema](media/azure-network-security/azure-network-security-fig-9.png)

Este flujo de comunicación es posible porque Azure utiliza una serie de sistema rutas toodefine cómo fluye el tráfico IP. Las rutas del sistema controlan el flujo de Hola de comunicación en hello los escenarios siguientes:

-   Desde Hola misma subred.

-   Desde un tooanother de subred dentro de una red virtual.

-   Desde máquinas virtuales toohello Internet.

-   Desde una red virtual tooanother red virtual a través de una puerta de enlace VPN.

-   Desde una red virtual a través de intercambio de tráfico de red virtual de red virtual tooanother ([encadenamiento de servicios](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview)).

-   Desde una red de en entornos de red virtual tooyour a través de una puerta de enlace VPN.

Muchas empresas tienen seguridad estricta y directivas de requisitos de cumplimiento que requieren inspección local de todos los tooenforce de paquetes de red específicos. Azure proporciona un mecanismo denominado [tunelización forzada](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-forced-tunneling) que enruta el tráfico procedente de hello local tooon de máquinas virtuales mediante la creación de una ruta personalizada o por [protocolo de puerta de enlace de borde (BGP)](https://docs.microsoft.com/windows-server/remote/remote-access/bgp/border-gateway-protocol-bgp) anuncios a través de ExpressRoute o VPN.

La tunelización forzada en Azure se configura a través de rutas definidas por el usuario (UDR) de redes virtuales. Redirigir el tráfico tooan local de sitio se expresa como una puerta de enlace de VPN de Azure de toohello de ruta predeterminada.

Hello siguiente sección enumeran hello las limitaciones actuales de la tabla de enrutamiento de Hola y rutas para una red Virtual de Azure:

-   Cada subred de la red virtual tiene una tabla de enrutamiento del sistema integrada. tabla de enrutamiento de sistema de Hello tiene Hola los tres grupos de rutas siguientes:

 -  **Las rutas de red virtual locales:** directamente toohello máquinas virtuales de destino en hello misma red virtual

 - **En las rutas locales:** toohello puerta de enlace de VPN de Azure

 -  **Ruta predeterminada:** toohello directamente Internet. Se quitan los paquetes destinados toohello las direcciones IP privadas no cubiertas por las rutas de hello dos anteriores.

-   Con la versión de Hola de rutas definidas por el usuario, puede crear un tooadd de tabla de enrutamiento una ruta predeterminada y, a continuación, asociar Hola enrutamiento tabla tooyour red virtual subred tooenable forzado túnel en esas subredes.

-   Deberá tooset un sitio denominado"predeterminado" entre la red virtual de hello entre entornos sitios locales toohello conectado.

-   La tunelización forzada debe asociarse a una red virtual que tiene una puerta de enlace de VPN de enrutamiento dinámico (no una puerta de enlace estática).

- La tunelización forzada de ExpressRoute no se configura mediante este mecanismo, pero en su lugar, se habilita de forma anunciando una ruta predeterminada a través de hello BGP de ExpressRoute sesiones de emparejamiento.

> [!Note]
> Para obtener más información, vea hello [documentación de ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) para obtener más información.

#### <a name="network-security-appliances"></a>Aplicaciones de seguridad de red
Mientras que los grupos de seguridad de red y las rutas definidas por el usuario pueden proporcionar un cierto grado de seguridad de red en hello las capas de red y el transporte de hello [modelo OSI](https://en.wikipedia.org/wiki/OSI_model), va toobe situaciones donde desea o necesita tooenable seguridad en los niveles superiores de la pila de red de Hola. En tales situaciones, se recomienda implementar aplicaciones de seguridad de la red virtual proporcionadas por asociados de Azure.

![Aplicaciones de seguridad de red](./media/azure-network-security/azure-network-security-fig-10.png)

Dispositivos de seguridad de red de Azure mejoran la seguridad de red virtual y las funciones de red y están disponibles en muchos proveedores a través de hello [Azure Marketplace](https://azuremarketplace.microsoft.com). Estos dispositivos de seguridad virtual pueden ser implementado tooprovide:

-   Firewalls de alta disponibilidad

-   Prevención de intrusiones

-   Detección de intrusiones

-   Firewalls de aplicaciones web (WAF)

-   Optimización de WAN

-   Enrutamiento

-   Equilibrio de carga

-   VPN

-   Administración de certificados

-   Active Directory

-   Autenticación multifactor

#### <a name="application-gateway"></a>puerta de enlace de aplicaciones

[Microsoft Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) es una aplicación virtual dedicada que proporciona un controlador de entrega de aplicaciones (ADC) como servicio.

 ![Application Gateway](./media/azure-network-security/azure-network-security-fig-11.png)

Puerta de enlace de aplicaciones permite disponibilidad y rendimiento de granja de servidores web toooptimize mediante la descarga de CPU intensivo SSL terminación toohello aplicación puerta de enlace (descarga de SSL). También proporciona otras funcionalidades de enrutamiento de capa 7 entre las que se incluyen:

-   Distribución round robin del tráfico entrante

-   Afinidad de sesión basada en cookies

-   Enrutamiento basado en URL

-   Capacidad toohost varios sitios Web detrás de una sola puerta de enlace de aplicaciones


A [firewall de aplicación web (WAFS)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) también se proporciona como parte de la puerta de enlace de aplicaciones de Hola. Esto proporciona protección de aplicaciones tooweb vulnerabilidades de web y vulnerabilidades de seguridad comunes. Application Gateway se puede configurar como una puerta de enlace orientada a Internet, una puerta de enlace solo para uso interno o una combinación de las dos.

El WAF de Application Gateway se puede ejecutar en modo de detección o de prevención. Un caso de uso común es para los administradores toorun en tráfico tooobserve en modo de detección para patrones malintencionados. Una vez que se detectan posibles vulnerabilidades, activar el modo de tooprevention bloquea el tráfico entrante sospechoso.

 ![Application Gateway](./media/azure-network-security/azure-network-security-fig-12.png)

Además, WAFS de puerta de enlace de aplicaciones le ayuda a supervisar las aplicaciones web contra los ataques mediante un registro WAFS en tiempo real que se integran con [Monitor Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) y [Azure Security Center](https://azure.microsoft.com/services/security-center/) tootrack WAFS alertas y supervisar las tendencias con facilidad.

registro de Hello JSON con formato va directamente cuenta de almacenamiento del cliente toohello. Tiene un control total sobre estos registros y puede aplicar sus propias directivas de retención.

También puede usar estos registros en su propio sistema de análisis con [Integración de registro de Azure](https://aka.ms/AzLog). Registros de WAFS también se integran con [Operations Management Suite (OMS)](https://www.microsoft.com/cloud-platform/operations-management-suite) por lo que puede usar análisis de registros OMS tooexecute sofisticadas consultas específicas.

#### <a name="azure-web-application-firewall-waf"></a>Firewall de aplicaciones web (WAF) de Azure

Las aplicaciones Web son cada vez más destinos de ataques malintencionados que aprovecha las vulnerabilidades conocidas comunes, como la inyección de código SQL, ataques de scripting entre sitios y otros ataques que aparecen en hello [arriba OWASP 10](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project). Evitar estos ataques en la aplicación hello requiere mantenimiento riguroso, aplicación de revisiones y la supervisión en varias capas de la topología de la aplicación hello.

 ![Firewall de aplicaciones web (WAF) de Azure](./media/azure-network-security/azure-network-security-fig-13.png)

Un [firewall de aplicaciones web (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) centralizado puede proteger frente a ataques web y simplifica la administración de seguridad sin necesidad de realizar ningún cambio en las aplicaciones.

Una solución WAFS también puedan reaccionar de amenaza para la seguridad tooa más rápido por una vulnerabilidad conocida en una ubicación central en comparación con la protección de cada una de las aplicaciones web individuales de la aplicación de revisiones. Puertas de enlace de aplicaciones existentes pueden ser puerta de enlace de la aplicación de firewall habilitado de tooa convertido web aplicación fácilmente.

#### <a name="network-availability-controls"></a>Controles de disponibilidad de red

No hay tráfico de red de distintas opciones toodistribute con Microsoft Azure. Estas opciones funcionan de manera diferente, ya que disponen de un conjunto de características distintas y son compatibles con escenarios distintos. Cada una se puede usar por separado, pero también se pueden combinar.

A continuación se Hola controles de disponibilidad de red:

-   Azure Load Balancer

-   Application Gateway

-   Traffic Manager

**Azure Load balancer**

Entrega tooyour aplicaciones de alta disponibilidad y rendimiento de red. Se trata de un equilibrador de carga de nivel 4 (TCP y UDP) que distribuye el tráfico entrante entre las instancias de servicio correctas de los servicios que se definen en un conjunto de carga equilibrada.

 ![Azure Load Balancer](media/azure-network-security/azure-network-security-fig-14.png)


Azure Load Balancer puede configurarse para lo siguiente:

-   La carga de máquinas de toovirtual de Internet entrantes de equilibrar el tráfico. Esta configuración se conoce como " [equilibrio de carga con conexión a Internet](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview)".

-   Equilibrar la carga del tráfico entre máquinas virtuales de una red virtual, entre máquinas virtuales de servicios en la nube o entre equipos locales y máquinas virtuales de una red virtual entre entornos locales. Esta configuración se conoce como " [equilibrio de carga interno](https://docs.microsoft.com/azure/load-balancer/load-balancer-internal-overview)".

-   Máquina virtual específica a reenvíe el tráfico externo tooa.

Todos los recursos de nube de hello necesitan una toobe de dirección IP pública accesible desde Internet Hola. infraestructura de nube de Hello en Azure usa direcciones IP no enrutables para sus recursos. Azure utiliza traducción de direcciones de red (NAT) con toohello de toocommunicate de direcciones IP pública Internet.

 **Application Gateway**

 Puerta de enlace de aplicaciones funciona a nivel de aplicación Hola (nivel 7 en la pila de referencia de hello OSI red). Actúa como un servicio de proxy inverso, finalizando la conexión de cliente de Hola y los puntos de conexión tooback-end se envían solicitudes.

 **Traffic manager**

Microsoft Azure Traffic Manager permite distribución de hello toocontrol del tráfico de usuario para los extremos de servicio en distintos centros de datos. Entre los puntos de conexión de servicio compatibles con Traffic Manager, se incluyen máquinas virtuales de Azure, Web Apps y servicios en la nube. También puede utilizar el Administrador de tráfico con puntos de conexión externos, que no forman parte de Azure.

El Administrador de tráfico usa Hola toodirect cliente solicita toohello extremo más adecuado en función de sistema de nombres de dominio (DNS) un [método de enrutamiento del tráfico](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) y estado de Hola de extremos de Hola. Traffic Manager proporciona una gama de enrutamiento del tráfico necesidades de distintas aplicaciones de métodos toosuit, estado del extremo [supervisión](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring)y la conmutación automática por error. El Administrador de tráfico es resistente toofailure, incluidos los errores de Hola de toda una región de Azure.

Azure Traffic Manager permite distribución de hello toocontrol de tráfico a través de los extremos de la aplicación. Un punto de conexión es cualquier servicio accesible desde Internet hospedado dentro o fuera de Azure.

Traffic Manager ofrece dos ventajas principales:

-   Distribución del tráfico según tooone de varias [métodos de enrutamiento del tráfico](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods).

-   La [supervisión continua del estado de los puntos de conexión](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring) y la conmutación automática por error en caso de error en estos.

Cuando un cliente intenta tooconnect tooa servicio, primero debe resolver nombre DNS de Hola Hola tooan IP de dirección de servicio. cliente de Hello, a continuación, conecta el servicio hello tooaccess de toothat IP direcciones. Los extremos en función de reglas de hello del método de enrutamiento del tráfico de hello del servicio de administrador de tráfico usa DNS toodirect clientes toospecific. Los clientes conectarse directamente extremo toohello seleccionado. Traffic Manager no es un proxy ni una puerta de enlace. El Administrador de tráfico no ve tráfico Hola pasar entre el cliente de Hola y el servicio de Hola.

### <a name="azure-network-validation"></a>Validación de la red de Azure

Validación de la red de Azure es tooensure que Hola red de Azure funciona tal y como está configurado y se puede realizar la validación mediante Hola servicios y características disponibles toomonitor Hola red. Con el Monitor de red de Azure, puede tener acceso a una gran cantidad de registro y capacidades de diagnóstico que permite a con visión toounderstand el rendimiento de la red y el estado. Estas funcionalidades son accesibles a través del portal, Power Shell, CLI, API de Rest y SDK.

Seguridad operativa de Azure hace referencia toohello servicios, los controles y características disponibles toousers para proteger sus datos, aplicaciones y otros activos de Microsoft Azure. Seguridad operativa de Azure se basa en un marco que incorpora el conocimiento de hello adquirido a través de una varias funciones que son único tooMicrosoft, incluidos Hola del ciclo de vida de desarrollo seguridad de Microsoft (SDL), Hola centro de respuesta de seguridad de Microsoft programa y conocimiento profundo del panorama de amenazas de seguridad de ciberseguridad de Hola.

-   [Azure Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

-   [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro)

-   [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

-   [Azure Network Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)

-   [Azure Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)

-   Administrador de recursos de Azure

#### <a name="azure-resource-manager"></a>Azure Resource Manager

personas de Hola y procesos que operan Microsoft Azure quizás son característica de seguridad más importante de Hola de plataforma de Hola. Esta sección describe las características de la infraestructura global de los centros de datos de Microsoft que le ayudan a mejorar y mantener la seguridad, la continuidad y la privacidad.

infraestructura de Hola para su aplicación normalmente se compone de muchos componentes, puede ser una máquina virtual, cuenta de almacenamiento y red virtual, o una aplicación web, base de datos, servidor de base de datos y servicios de terceros. Estos componentes no se ven como entidades independientes, sino como partes de una sola entidad relacionadas e interdependientes. Desea toodeploy, administrar y supervisar como un grupo. Administrador de recursos de Azure permite toowork con recursos de hello en la solución como un grupo.

Puede implementar, actualizar o eliminar todos los recursos de hello para la solución en una única operación coordinada. Para realizar la implementación se usa una plantilla, que puede funcionar en distintos entornos, como producción, pruebas y ensayo. Administrador de recursos proporciona seguridad, auditoría y etiquetado características toohelp administrar sus recursos después de la implementación.

**ventajas de Hola de usar el Administrador de recursos**

Administrador de recursos ofrece varias ventajas:

-   Puede implementar, administrar y supervisar todos los recursos de hello para la solución como un grupo, en lugar de controlar estos recursos individualmente.

-   Repetidamente, puede implementar la solución a lo largo del ciclo de vida de desarrollo de Hola y estar seguro de que los recursos se implementan en un estado coherente.

-   Puede administrar la infraestructura mediante plantillas declarativas en lugar de scripts.

-   Puede definir las dependencias de hello entre los recursos, por lo que se implementan en el orden correcto de Hola.

-   Puede aplicar tooall servicios de control de acceso en el grupo de recursos porque el Control de acceso basado en roles (RBAC) se integra de forma nativa en plataforma de administración de Hola.

-   Puede aplicar etiquetas tooresources toologically organizar todos los recursos de hello en su suscripción.

-   Puede aclarar la facturación de su organización viendo los costos de un grupo de recursos que compartan la misma etiqueta.

> [!Note]
> Administrador de recursos proporciona un nuevo toodeploy de manera y administrar sus soluciones. Si ha usado Hola modelo de implementación anterior y desea toolearn acerca de los cambios de hello, consulte [Administrador de recursos de la descripción y la implementación clásica](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model).

## <a name="azure-network-logging-and-monitoring"></a>Registro y supervisión de red de Azure

Azure ofrece muchos toomonitor de herramientas, evitar, detectar y responder a eventos de seguridad de toonetwork. Algunos de hello más eficaces herramientas disponibles tooyou en esta área son:

-   Network Watcher

-   Supervisión en el nivel de recursos de red

-   Log Analytics

### <a name="network-watcher"></a>Network Watcher

[Monitor de red](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) -basadas en escenarios de supervisión se proporciona con características de hello en Monitor de red. Este servicio incluye captura de paquetes, próximo salto, comprobación de flujo de IP, vista de grupos de seguridad y registros de flujo de NSG. Supervisión del nivel de escenario, proporciona una vista de tooend de final de los recursos de red en la supervisión de recursos de red de tooindividual de contraste.

 ![Network Watcher](./media/azure-network-security/azure-network-security-fig-15.png)

Monitor de red es un servicio regional que permite toomonitor y diagnosticar condiciones en un nivel de escenario de red, hacia y desde Azure. Diagnóstico de red y herramientas de visualización disponibles con Monitor de red ayudan a comprender, diagnosticar y obtener red tooyour de visión en Azure.

Monitor de red tiene actualmente Hola siguientes capacidades:

#### <a name="topology"></a>Topología

La [topología](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) devuelve un gráfico de recursos de red de una red virtual. gráfico de Hola traza la interconexión Hola entre conectividad de red tooend de hello recursos toorepresent Hola final. En el portal de hello, topología devuelve objetos de recursos de hello en según la función de red virtual. relaciones de Hola se representan mediante líneas entre recursos de hello fuera de la región de Monitor de red de hello, aunque en recursos de hello grupo no se mostrará. recursos de Hola devueltos en la vista de hello portal son un subconjunto de los componentes de red de Hola que se representan. lista completa de Hola de toosee de recursos de red, puede usar [PowerShell](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-powershell) o [REST](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-rest).

Como los recursos se devuelven conexión Hola entre los se modelan en dos relaciones.

- **Contención**: Virtual Network contiene un subconjunto que incluye una NIC.

- **Asociación**: una NIC está asociada a una máquina virtual.

#### <a name="variable-packet-capture"></a>Captura de paquetes variable

Monitor de red [captura de paquetes variable](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) permite toocreate paquete captura sesiones tootrack tráfico tooand desde una máquina virtual. Captura de paquetes le ayuda a anomalías red toodiagnose reactivamente y proactivity. Otros usos incluyen la recopilación de estadísticas de red, obtenga información sobre las intrusiones de red, toodebug cliente-servidor las comunicaciones y mucho más.

La captura de paquetes es una extensión de máquina virtual que se inicia de forma remota a través de Network Watcher. Esta capacidad facilita la carga de Hola de ejecutar manualmente una captura de paquetes en la máquina virtual de hello deseado, que permite ahorrar tiempo. Captura de paquetes puede realizarse a través del portal de hello, PowerShell, CLI o API de REST. Un ejemplo de cómo se puede activar la captura de paquetes es con las alertas de la máquina virtual.

#### <a name="ip-flow-verify"></a>Comprobación de flujo de IP

[Compruebe los flujos IP](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) comprueba si un paquete se permite o deniega tooor desde una máquina virtual basada en la información de tupla de 5. Esta información está formada por la dirección, el protocolo, la dirección IP local, la dirección IP remota, el puerto local y el puerto remoto. Si el paquete de saludo ha sido denegado por un grupo de seguridad, se devuelve el nombre de Hola de regla de Hola que deniega el paquete de saludo. Aunque puede elegir cualquier dirección IP de origen o destino, esta característica ayuda a los administradores diagnosticar rápidamente problemas de conectividad de o toohello internet y desde o entorno local de toohello.

La comprobación de flujos de IP tiene como destino una interfaz de red de una máquina virtual. Flujo de tráfico, a continuación, se comprueba en función de hello configurado tooor de configuración de esa interfaz de red. Esta capacidad es útil para confirmar si una regla en un grupo de seguridad de red está bloqueando tooor de tráfico de entrada o salida de una máquina virtual.

#### <a name="next-hop"></a>Próximo salto

Determina hello [próximo salto](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) para los paquetes que se enrutan en hello tejido de red de Azure, lo que permite toodiagnose cualquier mal configurado rutas definidas por el usuario. El tráfico de una máquina virtual se envía un destino tooa basándose en rutas efectivas Hola asociadas con una NIC. Próximo salto obtiene tipo hello de próximo salto y la dirección IP de un paquete desde una máquina virtual específica y la NIC. Esto ayuda a toodetermine si hello paquete se está dirigido toohello destino o se holed de tráfico de Hola que se va a negro.

Próximo salto también devuelve la tabla de rutas de hello asociada de próximo salto Hola. Al consultar un próximo salto si Hola ruta se define como una ruta definida por el usuario, se devolverá esa ruta. De lo contrario, la funcionalidad devolverá "Ruta de sistema".

#### <a name="security-group-view"></a>Vista de grupo de seguridad

Obtiene las reglas de seguridad eficaz y aplicada de Hola que se aplican en una máquina virtual. Los grupos de seguridad de red pueden asociarse a un nivel de subred o a un nivel de NIC. Cuando se asocia a un nivel de subred, se aplican a instancias de máquina virtual de tooall hello en la subred de Hola. Red [vista de grupo de seguridad](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) devuelve todas las reglas que están asociadas en un nivel de formación y la subred para una máquina virtual que proporciona una visión general de configuración de Hola y Hola configurado NSG. Además, las reglas de seguridad eficaz Hola se devuelven para cada una de las NICs hello en una máquina virtual. Con la vista de grupos de seguridad de red, se puede evaluar una máquina virtual en busca de vulnerabilidades de red, como puertos abiertos. También puede validar si el grupo de seguridad de red está funcionando según lo previsto en función de un [configurado de comparación entre Hola y Hola reglas de seguridad eficaz](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-auditing-powershell).

#### <a name="nsg-flow-logging"></a>Registro de flujo de NSG

 Registros de flujo para los grupos de seguridad de red permiten toocapture registros tootraffic relacionados que se permitirán o denegarán según las reglas de seguridad de hello en el grupo de Hola. flujo de Hola se define mediante una información de tupla de 5: dirección IP de origen, dirección IP de destino, puerto de origen, puerto de destino y protocolo.

[Registros de flujo de grupo de seguridad de red](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) son una característica del Monitor de red que permite tooview información sobre el tráfico IP de entrada y de salida a través de un grupo de seguridad de red.

#### <a name="virtual-network-gateway-and-connection-troubleshooting"></a>Solución de problemas de puerta de enlace de Virtual Network y de conexión

Monitor de red proporciona muchas de las capacidades en lo referente a toounderstanding los recursos de red en Azure. Una de estas funcionalidades es la solución de problemas de recursos. Se puede llamar a la [solución de problemas de recursos](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) mediante PowerShell, la CLI o la API de REST. Cuando se llama, Monitor de red inspecciona el estado de saludo de una puerta de enlace de red Virtual o una conexión y devuelve sus conclusiones.

En esta sección le guiará por las tareas de administración diferente de Hola que están actualmente disponibles para solucionar problemas de recursos.

-   [Solución de problemas de una puerta de enlace de Virtual Network](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)

-   [Solución de problemas de una conexión](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)

#### <a name="network-subscription-limits"></a>Límites de suscripción de red

[Los límites de suscripción de red](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) proporcionan los detalles de uso de Hola de cada uno de los recursos de red de hello en una suscripción en una región con el número máximo de Hola de recursos disponibles.

#### <a name="configuring-diagnostics-log"></a>Configuración del registro de diagnóstico

Network Watcher proporciona una vista de los [registros de diagnóstico](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview). Esta vista contiene todos los recursos de las redes que admiten el registro de diagnóstico. Desde esta vista, puede habilitar y deshabilitar los recursos de red de forma cómoda y rápida.

### <a name="network-resource-level-monitoring"></a>Supervisión en el nivel de recursos de red

Hola siguientes características está disponible para la supervisión de nivel de recurso:

#### <a name="audit-log"></a>Registro de auditoría

Se registran las operaciones realizadas como parte de la configuración de Hola de redes. Estos registros de auditoría es esencial tooestablish cumplimientos distintos. Estos registros pueden verse en el portal de Azure de Hola o recuperan mediante herramientas de Microsoft como Power BI o herramientas de terceros. Los registros de auditoría están disponibles a través del portal de hello, PowerShell, CLI y API de Rest.

> [!Note]
> Para más información sobre los registros de auditoría, consulte [Operaciones de auditoría con Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-audit).
Hay registros de auditoría disponibles para las operaciones realizadas en todos los recursos de red.


#### <a name="metrics"></a>Métricas

Las métricas son medidas de rendimiento y contadores recopilados durante un período de tiempo. Las métricas están disponibles actualmente para Application Gateway. Las métricas pueden ser alertas tootrigger utilizados en función de umbral. Azure puerta de enlace de aplicaciones de forma predeterminada se supervisa el estado de Hola de todos los recursos de su grupo back-end y se quita automáticamente cualquier recurso que se considera incorrecto del grupo de Hola. Puerta de enlace de aplicación continúa instancias toomonitor hello en mal estado y se agregan hacer copia de grupo de back-end de toohello correcto una vez que estén disponibles y responden toohealth sondeos. Puerta de enlace de aplicación envía Hola sondeos de estado con hello mismo puerto que se define en la configuración de HTTP de back-end de Hola. Esta configuración garantiza que sondeo Hola está probando Hola mismo número de puerto que los clientes sería utilizar back-end de tooconnect toohello.

> [!Note]
> Vea [puerta de enlace de Application Diagnostics](https://docs.microsoft.com/azure/application-gateway/application-gateway-probe-overview) tooview cómo las métricas pueden ser utilizados toocreate alertas.

#### <a name="diagnostic-logs"></a>Registros de diagnóstico

Eventos periódicos y espontáneos son creados por los recursos de red y se registra en las cuentas de almacenamiento, enviadas tooan concentrador de eventos o análisis de registros. Estos registros proporcionan información sobre el estado de saludo de un recurso. Estos registros se pueden ver en herramientas como Power BI y Log Analytics. toolearn cómo tooview registros de diagnóstico, visite [análisis de registros](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-networking-analytics).

Los registros de diagnóstico están disponibles para el [equilibrador de carga](https://docs.microsoft.com/azure/load-balancer/load-balancer-monitor-log), los [grupos de seguridad de red](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log), las rutas y [Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics).

Network Watcher proporciona una vista de los registros de diagnóstico. Esta vista contiene todos los recursos de las redes que admiten el registro de diagnóstico. Desde esta vista, puede habilitar y deshabilitar los recursos de red de forma cómoda y rápida.

### <a name="log-analytics"></a>Log Analytics

[Análisis de registros](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) es un servicio en [Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) que supervisa su toomaintain de entornos de nube y locales su disponibilidad y el rendimiento. Recopila los datos generados por los recursos en los entornos de nube y locales y de otros análisis de tooprovide herramientas supervisión a través de varios orígenes.

Análisis de registros ofrecen Hola siguientes soluciones para supervisar las redes:

-   Network Performance Monitor (NPM) (monitor de rendimiento de red)

-   Azure Application Gateway Analytics

-   Azure Network Security Group Analytics

#### <a name="network-performance-monitor-npm"></a>Network Performance Monitor (NPM) (monitor de rendimiento de red)
Hola [Monitor de rendimiento de red](https://docs.microsoft.com/azure/log-analytics/log-analytics-network-performance-monitor) solución de administración es una solución que supervisa el estado de hello, la disponibilidad y la comunicación de redes de supervisión de red.

Es utilizado toomonitor conectividad entre:

-   nube pública y entorno local

-   centros de datos y ubicaciones de usuario (sucursales)

-   subredes que hospedan distintos niveles de una aplicación de varios niveles.


#### <a name="azure-application-gateway-analytics-in-log-analytics"></a>Azure Application Gateway Analytics en Log Analytics

Hola siguiendo los registros es compatibles con las puertas de enlace de la aplicación:

-   ApplicationGatewayAccessLog

-   ApplicationGatewayPerformanceLog

-   ApplicationGatewayFirewallLog

Hola siguiendo las métricas se admite para las puertas de enlace de la aplicación:

-   Rendimiento de 5 minutos

#### <a name="azure-network-security-group-analytics-in-log-analytics"></a>Azure Network Security Group Analytics en Log Analytics

Hello siguientes los registros son compatibles para [grupos de seguridad de red](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log):

- **NetworkSecurityGroupEvent:** contiene entradas para lo NSG son reglas tooVMs aplicados y roles de una instancia en función de la dirección MAC. estado de Hola para que estas reglas se recopila cada 60 segundos.

- **NetworkSecurityGroupRuleCounter:** contiene entradas para el número de veces cada NSG de regla se aplica toodeny o permitir el tráfico.

## <a name="next-steps"></a>Pasos siguientes
Obtener más información acerca de la seguridad con la lectura de algunos de nuestros detallados temas de seguridad:

-   [Análisis del registro para grupos de seguridad de red (NSG)](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log)

-   [Redes innovaciones esa interrupción de unidad hello en la nube](https://azure.microsoft.com/blog/networking-innovations-that-drive-the-cloud-disruption/)

-   [SONiC: Hola software de conmutador que alimenta Hola Microsoft Cloud Global de red](https://azure.microsoft.com/blog/sonic-the-networking-switch-software-that-powers-the-microsoft-global-cloud/)

-   [Cómo crea Microsoft su red global rápida y confiable](https://azure.microsoft.com/blog/how-microsoft-builds-its-fast-and-reliable-global-network/)

-   [Impulso de la innovación en la red](https://azure.microsoft.com/blog/lighting-up-network-innovation/)
