---
title: las redes aaaAzure | Documentos de Microsoft
description: "Obtenga información sobre servicios de redes y funcionalidades de Azure ."
services: networking
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: jdial
ms.openlocfilehash: 18945d139427f2e65138c0fd223e663fa46e9211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking"></a>Redes de Azure

Azure proporciona una variedad de funcionalidades de red que se pueden usar conjuntamente o por separado. Haga clic en cualquiera de hello después capacidades clave toolearn más información acerca de ellos:
- [Conectividad entre recursos de Azure](#connectivity): recursos de Azure conectarse juntos en una red virtual privada y segura en la nube de Hola.
- [Conectividad a Internet](#internet-connectivity): tooand de recursos de Azure se comunican a través de Internet de Hola.
- [Conectividad local](#on-premises-connectivity): conectarse a un recursos de tooAzure de red local a través de una red privada virtual (VPN) a través de Internet de hello, o a través de una conexión dedicada tooAzure.
- [Dirección del tráfico y equilibrio de carga](#load-balancing): tooservers de tráfico de equilibrio de carga en Hola la misma ubicación y dirigir el tráfico tooservers en diferentes ubicaciones.
- [Seguridad](#security): filtre el tráfico de red entre subredes de la red o máquinas virtuales individuales.
- [Enrutamiento](#routing): utilice el enrutamiento predeterminado o controle completamente el enrutamiento entre los recursos locales y de Azure.
- [Manejabilidad](#manageability): supervise y administre los recursos de red de Azure.
- [Herramientas de implementación y configuración](#tools): usar un portal basado en web o herramientas de línea de comandos multiplataforma toodeploy y configurar los recursos de red.

## <a name="Connectivity"></a>Conectividad entre recursos de Azure

Los recursos de Azure como Virtual Machines, Cloud Services, conjuntos de escalado de máquinas virtuales y Azure App Service Environment pueden comunicarse de forma privada entre sí a través de una red virtual de Azure. Una red virtual es un aislamiento lógico de hello nube de Azure dedicada tooyour [suscripción](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fnetworking%2ftoc.json). Puede implementar varias redes virtuales dentro de cada suscripción y [región](https://azure.microsoft.com/regions) de Azure. Cada red virtual está aislada de otras redes virtuales. Para cada red virtual, puede:

- Especificar un espacio de direcciones IP privado personalizado mediante direcciones públicas y privadas (RFC 1918). Azure asigna recursos conectados toohello red virtual una dirección IP privada del espacio de direcciones de Hola que asigna.
- Hola red virtual en una o varias subredes de segmento y asignar una parte de la subred tooeach espacio de direcciones IP Hola red virtual.
- Utilizar la resolución de nombres que proporciona Azure o especifique su propio servidor DNS para su uso por los recursos de conecta tooa red virtual.

más información acerca del servicio de red Virtual de Azure de hello, leer hello toolearn [información general de red Virtual](../virtual-network/virtual-networks-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo. Puede conectar redes virtuales tooeach otros, habilitar recursos conectados tooeither toocommunicate de red virtual entre sí a través de redes virtuales. Puede utilizar uno o ambos de hello después opciones tooconnect redes virtuales tooeach otros:

- **Emparejamiento:** habilita recursos conectado toodifferent redes virtuales de Azure en hello mismo toocommunicate de región de Azure entre sí. Hello ancho de banda y latencia de hello redes virtuales está Hola mismo como si fueron de los recursos de hello toohello conectado misma red virtual. toolearn más sobre el emparejamiento, leer hello [introducción de intercambio de tráfico de red Virtual](../virtual-network/virtual-network-peering-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.
- **Puerta de enlace VPN:** habilita recursos conexión toodifferent redes virtuales de Azure en diferentes regiones de Azure toocommunicate entre sí. El tráfico entre redes virtuales fluye a través de una instancia de Azure VPN Gateway. Ancho de banda entre redes virtuales es el ancho de banda limitado toohello de puerta de enlace de Hola. toolearn más acerca de cómo conectar redes virtuales con una puerta de enlace de VPN, leer hello [configurar una conexión de red virtual a red virtual entre las regiones](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.

## <a name="internet-connectivity"></a>Conectividad de Internet

Todos los recursos de Azure a conectado tooa red virtual tiene conectividad saliente toohello Internet de forma predeterminada. dirección IP privada de Hello del recurso de hello es la dirección de red de origen convierte la dirección IP pública de (SNAT) tooa Hola infraestructura de Azure. más información acerca de la conectividad saliente de Internet, leer hello toolearn [descripción de las conexiones salientes en Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.

toocommunicate entrante tooAzure recursos de Internet de Hola o toocommunicate toohello saliente Internet sin SNAT, un recurso debe asignarse a una dirección IP pública. más información acerca de las direcciones IP públicas, leer hello toolearn [direcciones IP públicas](../virtual-network/virtual-network-public-ip-address.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.

## <a name="on-premises-connectivity"></a>Conectividad local

Se puede acceder a los recursos de la red virtual de forma segura a través de una conexión VPN o de una conexión directa privada. toosend el tráfico de red entre su red virtual de Azure y la red local, debe crear una puerta de enlace de red virtual. Configurar tipo de hello toocreate Hola de puerta de enlace de conexión que desee, VPN o ExpressRoute.

Puede conectar su tooa de red local red virtual con cualquier combinación de hello siguientes opciones:

**Punto a sitio (VPN a través de SSTP)**

Hola la siguiente imagen muestra independiente toosite punto conexiones entre varios equipos y una red virtual:

![De punto a sitio](./media/networking-overview/point-to-site.png)

Esta conexión se establece entre un solo equipo y una red virtual. Este tipo de conexión es excelente si principiante con Azure, o para los desarrolladores, ya que requiere poca o ninguna red existente de tooyour de cambios. También es adecuada cuando se conecta desde una ubicación remota, como una conferencia o el domicilio. Conexiones de punto a sitio están acopladas a menudo con una conexión de sitio a sitio a través de hello misma puerta de enlace de red virtual. conexión de Hello utiliza la comunicación de tooprovide cifrado de protocolo de hello SSTP sobre Hola Internet entre el equipo de Hola y Hola red virtual. latencia de Hello una VPN de sitio a punto es imprevisible, ya que Hola tráfico que atraviesa Hola Internet.

**Sitio a sitio (túnel VPN de IPsec/IKE)**

![De sitio a sitio](./media/networking-overview/site-to-site.png)

Esta conexión se establece entre el dispositivo VPN local y una instancia de Azure VPN Gateway. Este tipo de conexión permite a cualquier recurso local que autorice tooaccess Hola red virtual. conexión de Hello es una VPN de IPSec/IKE que proporciona comunicación cifrada con respecto a Hola Internet entre el dispositivo local y la puerta de enlace de VPN de Azure de Hola. Puede conectar varios locales sitios toohello misma puerta de enlace VPN. Hola de-local dispositivo VPN en cada sitio debe tener una dirección IP pública de externo que no está detrás de un dispositivo NAT. latencia de Hola para una conexión de sitio a sitio es impredecible, puesto que Hola tráfico que atraviesa Hola Internet.

**ExpressRoute (conexión privada dedicada)**

![ExpressRoute](./media/networking-overview/expressroute.png)

Este tipo de conexión se establece entre la red y Azure, a través de un asociado de ExpressRoute. Esta conexión es privada. El tráfico no atraviesa Hola Internet. latencia de Hola para una conexión ExpressRoute es predecible, puesto que el tráfico no atraviesan Hola Internet. ExpressRoute puede combinarse con una conexión de sitio a sitio.

más información acerca de todas las opciones de conexión anterior de hello, leer hello toolearn [diagramas de topología de conexión](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.

## <a name="load-balancing"></a>Equilibrio de carga y dirección del tráfico

Microsoft Azure proporciona varios servicios para administrar cómo se distribuye el tráfico de red y se equilibra la carga. Puede usar cualquiera de hello después capacidades por separado o conjuntamente:

**Equilibrio de carga de DNS**

Hola el servicio Administrador de tráfico de Azure proporciona equilibrio de carga global de DNS. El Administrador de tráfico responde tooclients con la dirección IP de Hola de un punto de conexión correcto, basado en uno de hello siguiendo métodos de enrutamiento:
- **Geográfico:** los clientes se dirigen toospecific extremos (Azure, anidada o externo) en función de qué ubicación geográfica su consulta DNS se origina desde. Este método permite escenarios donde es importante conocer la región geográfica del cliente, así como el enrutamiento a partir de ella. Algunos ejemplos incluyen cumplir los mandatos de soberanía de datos, la localización del contenido y de la experiencia del usuario, y la medición del tráfico de otras regiones.
- **Rendimiento:** dirección IP de hello devuelve toohello cliente es Hola "más cercano" toohello. punto de conexión "más cercano" Hello no es necesariamente más cercano, medido por la distancia geográfica. En su lugar, este método determina el extremo más cercano de hello mediante la medición de latencia de red. El Administrador de tráfico mantiene una latencia tabla tootrack Hola ida y vuelta hora de Internet entre los intervalos de direcciones IP y cada centro de datos de Azure.
- **Prioridad:** tráfico es el punto de conexión de toohello dirigida primario (prioridad más alta). Si no hay ningún punto de conexión principal de hello, rutas de Traffic Manager Hola toohello segundo extremo de tráfico. Si ambos extremos de hello principales y secundarias no están disponibles, el tráfico de hello dirige toohello en tercer lugar, y así sucesivamente. Disponibilidad de punto de conexión de Hola se basa en el estado de hello configurado (habilitado o deshabilitado) y Hola supervisión continuada del extremo.
- **Método round-robin ponderado:** para cada consulta, Traffic Manager elegirá aleatoriamente un punto de conexión disponible. probabilidad de Hola de elegir un punto de conexión se basa en pesos Hola asignados tooall puntos de conexión disponibles. Usar Hola mismo peso a través de todos los resultados de los puntos de conexión en una distribución de tráfico incluso. Mediante valores ponderados mayores o menores en puntos de conexión concretos hace que esos toobe extremos devuelven mayor o menor frecuencia en las respuestas DNS de Hola.

Hola siguiente imagen muestra una solicitud para un tooa de aplicación dirigida web extremo de aplicación Web. Los puntos de conexión también pueden ser otros servicios de Azure como Virtual Machines y Cloud Services.

![Administrador de tráfico](./media/networking-overview/traffic-manager.png)

Hola cliente conecta directamente toothat extremo. Azure Traffic Manager detecta cuando un punto de conexión está en mal estado y, a continuación, redirige los clientes tooa diferentes, correcto punto de conexión. toolearn más acerca del Administrador de tráfico, leer hello [Introducción al administrador de tráfico de Azure](../traffic-manager/traffic-manager-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.

**Equilibrio de carga de la aplicación**

Hola servicio de puerta de enlace de aplicaciones de Azure proporciona el controlador de entrega de aplicaciones (ADC) como un servicio. Puerta de enlace de aplicaciones ofrece diversas capacidades de equilibrio de carga de nivel 7 (HTTP/HTTPS) para sus aplicaciones, incluso una aplicación web de firewall tooprotect sus aplicaciones web de amenazas y ataques. Puerta de enlace de aplicaciones también permite productividad de granja de servidores web toooptimize mediante la descarga de puerta de enlace de aplicaciones de toohello de finalización de SSL de la CPU. 

Otras capacidades de enrutamiento de nivel 7 incluyen la distribución de round robin de tráfico entrante, afinidad de sesión basado en cookies, enrutamiento basado en la ruta de acceso de direcciones URL y toohost de capacidad de hello varios sitios Web detrás de una puerta de enlace de aplicación único. Application Gateway puede configurarse como una puerta de enlace accesible desde Internet, una puerta de enlace solo para uso interno o una combinación de las dos. Application Gateway está completamente administrada por Azure, es escalable y tiene una elevada disponibilidad. Cuenta con un amplio conjunto de funcionalidades de diagnóstico y registro, lo que facilita su administración. más información acerca de la puerta de enlace de aplicaciones, leer hello toolearn [información general de la puerta de enlace de aplicaciones](../application-gateway/application-gateway-introduction.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.

Hello siguiente imagen muestra dirección URL de enrutamiento con puerta de enlace de aplicaciones basado en la ruta de acceso:

![Application Gateway](./media/networking-overview/application-gateway.png)

**Equilibrio de carga de red**

Hola equilibrador de carga de Azure proporciona gran rendimiento y baja latencia capa 4 equilibrio de carga para todos los protocolos TCP y UDP. Administra conexiones entrantes y salientes. Puede configurar los puntos de conexión de carga equilibrada públicos e internos. Puede definir reglas toomap entrada destinos de grupo de conexiones tooback-end utilizando HTTP y TCP sondeo de estado opciones toomanage disponibilidad del servicio. más información acerca de equilibrador de carga, leer hello toolearn [información general del equilibrador de carga](../load-balancer/load-balancer-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.

Hola siguiente imagen muestra una aplicación de varios nivel con conexión a Internet que utiliza los equilibradores de carga externos e internos:

![Equilibrador de carga](./media/networking-overview/load-balancer.png)

## <a name="security"></a>Seguridad

Puede filtrar tráfico tooand de recursos de Azure con hello siguientes opciones:

- **Red:** puede implementar toofilter de grupos (NSG) de seguridad de red de Azure entrante y saliente tráfico tooAzure recursos. Cada grupo de seguridad de red contiene una o varias reglas de entrada y salida. Cada regla especifica direcciones IP de origen de hello, direcciones IP de destino, puerto y protocolo que se filtra el tráfico con. Los NSG pueden subredes tooindividual aplicados y máquinas virtuales individuales. más información acerca de los NSG, leer hello toolearn [información general de grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.
- **Aplicación:** al usar una instancia de Application Gateway con el firewall de aplicación web, puede proteger las aplicaciones web de amenazas y ataques. Algunos ejemplos comunes son ataques de inyección de código SQL, scripting entre sitios y encabezados con formato incorrecto. La puerta de enlace de aplicaciones filtra este tráfico y le impide llegar a los servidores web. Es capaz de tooconfigure qué reglas desea que estén activados. directivas de negociación de SSL de Hello capacidad tooconfigure se proporciona tooallow determinada directivas toobe deshabilitado. más información acerca de firewall de aplicación web de hello, leer hello toolearn [firewall de aplicación Web](../application-gateway/application-gateway-web-application-firewall-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.

Si necesita capacidad de red no proporcionan Azure, o desea que las aplicaciones de red toouse use local, puede implementar productos de hello en máquinas virtuales y conectarlos tooyour red virtual. Hola [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances) contiene varias máquinas virtuales diferentes configuradas previamente con aplicaciones de red que utiliza actualmente. Estas máquinas virtuales preconfiguradas están tooas que normalmente se conoce virtual los dispositivos de red (NVA). Las aplicaciones virtuales de red están disponibles con aplicaciones como el firewall y la optimización de WAN.

## <a name="routing"></a>Enrutamiento

Azure crea de forma predeterminada las tablas de rutas que habilite recursos tooany conectado subred en cualquier toocommunicate de red virtual entre sí. Puede implementar uno o ambos de los siguientes tipos de rutas toooverride de Hola Hola Azure crea las rutas predeterminadas:
- **Definido por el usuario:** puede crear tablas de enrutamiento personalizadas con rutas que controlan donde el tráfico es enrutado toofor cada subred. más información acerca de las rutas definidas por el usuario, leer hello toolearn [rutas definidas por el usuario](../virtual-network/virtual-networks-udr-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.
- **Borde (BGP) de protocolo de puerta de enlace:** si se conecta a la red de red virtual tooyour local mediante una conexión de puerta de enlace de VPN de Azure o ExpressRoute, puede propagar tooyour de rutas BGP redes virtuales. BGP es frecuente en hello tooexchange enrutamiento y alcance de la información de Internet entre dos o más redes de protocolo de enrutamiento estándar Hola. Cuando se utiliza en el contexto de Hola de redes virtuales de Azure, BGP permite Hola puertas de enlace de VPN de Azure y los dispositivos VPN local, pares BGP llamado o vecinos, tooexchange "enruta" que informan sobre las puertas de enlace en la disponibilidad de Hola y accesibilidad de los prefijos toogo a través de las puertas de enlace de Hola o enrutadores implicados. BGP también puede habilitar el enrutamiento del tránsito entre varias redes mediante la propagación de las rutas de una puerta de enlace BGP aprende desde una BGP del mismo nivel tooall otros pares BGP. toolearn más información acerca de BGP, consulte hello [BGP con información general de las puertas de enlace VPN de Azure](../vpn-gateway/vpn-gateway-bgp-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.

## <a name="manageability"></a>Manejabilidad

Azure proporciona siguiente hello toomonitor de las herramientas y administración de redes:
- **Registros de actividad:** recursos de Azure todos los que los registros de actividad que proporcionan información acerca de las operaciones realizadas coloque, estado de las operaciones y quién inició la operación de Hola. más información acerca de los registros de actividad, leer hello toolearn [información general de registros de actividad](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.
- **Registros de diagnóstico:** periódico y eventos espontáneos se creados por los recursos de red y se registran en las cuentas de almacenamiento de Azure, enviar tooan concentrador de eventos de Azure o se envían tooAzure análisis de registros. Registros de diagnóstico proporcionan el estado de toohello una visión general de un recurso. Los registros de diagnóstico se proporcionan para Load Balancer (con conexión a Internet), los grupos de seguridad de red, las rutas y Application Gateway. más información acerca de los registros de diagnóstico, leer hello toolearn [información general de los registros de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.
- **Métricas:** las métricas son medidas de rendimiento y contadores recopilados durante un período de tiempo en los recursos. Las métricas pueden ser alertas tootrigger utilizados en función de umbrales. Las métricas están disponibles actualmente en Application Gateway. más información acerca de las métricas, leer hello toolearn [Introducción a las métricas](../monitoring-and-diagnostics/monitoring-overview-metrics.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.
- **Solución de problemas:** información para solucionar problemas es accesible directamente en hello portal de Azure. información de Hello ayuda a diagnosticar problemas comunes con ExpressRoute, puerta de enlace de VPN, puerta de enlace de aplicaciones, los registros de seguridad de red, rutas, DNS, equilibrador de carga y Traffic Manager.
- **Control de acceso basado en rol (RBAC):** controle quién puede crear y administrar recursos de red con el control de acceso basado en rol (RBAC). Obtener más información sobre RBAC leyendo hello [empezar a trabajar con RBAC](../active-directory/role-based-access-control-what-is.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo. 
- **Captura de paquetes:** Hola Monitor de red de Azure proporciona servicio Hola toorun capacidad capturar un paquete en una máquina virtual a través de una extensión de hello VM. La funcionalidad está disponible para máquinas virtuales Linux y Windows. más información acerca de la captura de paquetes, leer hello toolearn [información general de captura de paquetes](../network-watcher/network-watcher-packet-capture-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.
- **Comprobar los flujos de IP:** Monitor de red permite tooverify IP flujos entre una máquina virtual de Azure y un recurso remoto toodetermine si paquetes permitidos o denegados. Esta capacidad proporciona a los administradores la capacidad de hello tooquickly diagnosticar problemas de conectividad. toolearn más información acerca de cómo fluye tooverify IP, leer hello [flujo IP comprobar información general sobre](../network-watcher/network-watcher-ip-flow-verify-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.
- **Solucionar problemas de conectividad VPN:** Hola capacidad de VPN de solucionador de problemas del Monitor de red proporciona Hola capacidad tooquery una conexión o la puerta de enlace y comprobar el estado de Hola de recursos de Hola. más información sobre solución de problemas de las conexiones VPN, leer hello toolearn [información general de solución de problemas de conectividad VPN](../network-watcher/network-watcher-troubleshoot-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.
- **Ver la topología de red:** ver una representación gráfica de los recursos de red de hello en una red virtual con el Monitor de red. toolearn más acerca de cómo ver la topología de red, lea hello [información general de la topología](../network-watcher/network-watcher-topology-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.

## <a name="tools"></a>Herramientas de implementación y configuración

Puede implementar y configurar los recursos de red de Azure con cualquiera de hello siguientes herramientas:

- **Azure Portal:** una interfaz gráfica de usuario que se ejecuta en un explorador. Abra hello [portal de Azure](http://portal.azure.com).
- **Azure PowerShell:** herramientas de línea de comandos para la administración de Azure desde equipos Windows. Más información acerca de PowerShell de Azure por leer Hola [Introducción a Azure PowerShell](/powershell/azure/overview?view=azurermps-3.8.0?toc=%2fazure%2fnetworking%2ftoc.json) artículo.
- **Interfaz de la línea de comandos (CLI) de Azure:** herramientas de la línea de comandos para administrar Azure desde equipos Linux, macOS o Windows. Obtener más información sobre Hola CLI de Azure por leer hello [descripción general de CLI de Azure](/cli/azure/get-started-with-azure-cli?toc=%2fazure%2fnetworking%2ftoc.json) artículo.
- **Plantillas de administrador de recursos de Azure:** un archivo (en formato JSON) que define la infraestructura de Hola y la configuración de una solución de Azure. Mediante una plantilla, puede implementar la solución repetidamente a lo largo del ciclo de vida y tener la seguridad de que los recursos se implementan de forma coherente. más sobre la creación de plantillas, leen hello toolearn [las prácticas recomendadas para la creación de plantillas](../azure-resource-manager/resource-manager-template-best-practices.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo. Plantillas pueden implementarse con hello portal de Azure, CLI o PowerShell. tooget a trabajar con plantillas de forma inmediata, implemente uno de hello muchas plantillas preconfiguradas en hello [plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/?term=network) biblioteca. 

## <a name="pricing"></a>Precios

Algunos de hello Azure Servicios de red con un cargo, mientras que otras son libres. Hola de vista [red Virtual](https://azure.microsoft.com/pricing/details/virtual-network), [puerta de enlace VPN](https://azure.microsoft.com/pricing/details/vpn-gateway), [Application Gateway](https://azure.microsoft.com/en-us/pricing/details/application-gateway/), [equilibrador de carga](https://azure.microsoft.com/pricing/details/load-balancer), [delMonitordered](https://azure.microsoft.com/pricing/details/network-watcher), [DNS](https://azure.microsoft.com/pricing/details/dns), [Traffic Manager](https://azure.microsoft.com/pricing/details/traffic-manager) y [ExpressRoute](https://azure.microsoft.com/pricing/details/expressroute) precios páginas para obtener más información.

## <a name="next-steps"></a>Pasos siguientes

- Crear la red virtual de primera y conectar unos tooit de máquinas virtuales, siguiendo los pasos de Hola Hola [crear la primera red virtual](../virtual-network/virtual-network-get-started-vnet-subnet.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.
- Conectar su red virtual de equipo tooa siguiendo los pasos de Hola Hola [configurar una conexión punto a sitio](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.
- Servidores de toopublic de tráfico de Internet se equilibra la carga siguiendo los pasos de Hola Hola [crear un equilibrador de carga a través de Internet](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) artículo.
