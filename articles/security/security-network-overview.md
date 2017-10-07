---
title: aaaNetwork conceptos de seguridad y los requisitos de Azure | Documentos de Microsoft
description: " Este artículo facilita toounderstand, lo que Microsoft Azure tiene toooffer en el área de Hola de seguridad de red. Proporcionamos explicaciones básicas de los conceptos centrales de seguridad de red y los requisitos y obtener información sobre qué Azure tiene toooffer en cada una de estas áreas. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: bedf411a-0781-47b9-9742-d524cf3dbfc1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: terrylan
ms.openlocfilehash: 87d336064b880ddcf90ae4fcb79b7823367682b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security-overview"></a>Azure Network Security Overview (Información general sobre Azure Network Security)
Microsoft Azure incluye una sólida toosupport de infraestructura de red de su aplicación y los requisitos de conectividad de servicio. Conectividad de red es posible entre los recursos ubicados en Azure, entre locales y recursos y tooand de hello Internet y Azure hospedado de Azure.

objetivo de Hola de este artículo es toomake resulta más sencillo para toounderstand, lo que Microsoft Azure tiene toooffer en el área de Hola de seguridad de red. Aquí ofrecemos una explicación básica de los conceptos y requisitos fundamentales de la seguridad de red. También se proporcionan información sobre qué Azure tiene toooffer en cada una de estas áreas, así como vínculos toohelp obtener una comprensión más profunda de las áreas de interés.

En este artículo de información general de seguridad de red de Azure se centra en hello siguientes áreas:

* Redes de Azure
* Control de acceso de red
* Protección del acceso remoto y la conectividad local
* Disponibilidad
* Resolución de nombres
* Arquitectura de red perimetral (DMZ)
* Detección de amenazas y supervisión


## <a name="azure-networking"></a>Redes de Azure
Las máquinas virtuales necesita conectividad de red. toosupport ese requisito, Azure requiere toobe de máquinas virtuales conectada tooan red Virtual de Azure. Red Virtual de Azure es una construcción lógica que se basa en el tejido de red físico de Azure Hola. Cada red virtual lógica de Azure está aislada de todas las demás redes virtuales de Azure. Esto ayuda a garantizar que el tráfico de red en sus implementaciones no es accesible tooother clientes de Microsoft Azure.

Más información:

* [Información general sobre redes virtuales](../virtual-network/virtual-networks-overview.md)


## <a name="network-access-control"></a>Control de acceso de red
Control de acceso de red es Hola para limitar el tooand de conectividad de dispositivos específicos o subredes de red Virtual de Azure. objetivo de Hola de control de acceso de red es tooyour de toolimit acceder a máquinas virtuales, los usuarios de tooapproved de servicios y dispositivos. Controles de acceso se basan en permitir o denegar decisiones para las conexiones tooand desde la máquina virtual o el servicio.

Azure admite varios tipos de controles de acceso de red, como:

* Control de capa de red
* Control de ruta y tunelización forzada
* Dispositivos de seguridad de red virtual

### <a name="network-layer-control"></a>Control de capa de red
Toda implementación segura requiere alguna medida de control del acceso a la red. objetivo de Hola de control de acceso de red es toorestrict sistemas necesarios de máquina virtual comunicación toohello y que se bloquean los demás intentos de comunicación.

Si necesita control de acceso de nivel de red básica (basado en la dirección IP y Hola TCP o protocolos UDP), a continuación, puede usar grupos de seguridad de red. Un grupo de seguridad de red (NSG) es un básico firewall de filtrado de paquetes con estado y permite toocontrol acceso tomando como base un [5-tupla](https://www.techopedia.com/definition/28190/5-tuple). Los NSG no proporcionan inspección de nivel de aplicación ni controles de acceso autenticados.

Más información:

* [Grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md)

### <a name="route-control-and-forced-tunneling"></a>Control de ruta y tunelización forzada
comportamiento de enrutamiento toocontrol de Hello capacidad en las redes virtuales de Azure es una función de control de seguridad y el acceso de red críticos. Si el enrutamiento está configurado incorrectamente, aplicaciones y servicios hospedados en la máquina virtual pueden conectar dispositivos de toounauthorized incluidos sistemas perteneciente y usada por los atacantes potenciales.

Las redes de Azure es compatible con comportamiento de enrutamiento de hello capacidad toocustomize hello para el tráfico de red en las redes virtuales de Azure. Esto le permite tooalter Hola predeterminada enrutamiento entradas de la tabla en la red Virtual de Azure. El control del comportamiento de enrutamiento ayuda a garantizar que todo el tráfico procedente de un determinado dispositivo o grupo de dispositivos entra o sale de la red virtual a través de una ubicación específica.

Por ejemplo, suponga que tiene un dispositivo de seguridad de red virtual en la red virtual de Azure. Desea toomake seguro de que todos los tooand de tráfico de red Virtual de Azure pasa ese dispositivo de seguridad virtual. Para ello, puede configurar [rutas definidas por el usuario](../virtual-network/virtual-networks-udr-overview.md) en Azure.

[La tunelización forzada](https://www.petri.com/azure-forced-tunneling) es un mecanismo que puede utilizar tooensure que los servicios no están permitidas tooinitiate una toodevices de conexión en hello Internet. Tenga en cuenta que esto es diferente de acepta las conexiones entrantes y, a continuación, responde toothem. Servidores web front-end requieren toorespond toorequests desde hosts de Internet y, por lo que se permite el tráfico de origen de Internet entrante toothese servidores web y hello web se permiten toorespond.

Lo que no desee tooallow es un tooinitiate de servidor web front-end una solicitud saliente. Estas solicitudes pueden representar un riesgo de seguridad porque estas conexiones pudieron ser utilizado toodownload malware. Incluso si desea que estos front-end tooinitiate servidores saliente solicita toohello Internet, quizás quiera tooforce les toogo a través de sus instalaciones de servidores proxy web, por lo que puede aprovechar la dirección URL de filtrado y registro.

En su lugar, sería aconsejable toouse forzado tooprevent túnel esto. Cuando se habilita la tunelización forzada, todas las conexiones toohello Internet se convierten obligatoriamente a través de la puerta de enlace local. Puede configurar la tunelización forzada aprovechando las rutas definidas por el usuario.

Más información:

* [¿Qué son las rutas definidas por el usuario y el reenvío IP?](../virtual-network/virtual-networks-udr-overview.md)

### <a name="virtual-network-security-appliances"></a>Dispositivos de seguridad de red virtual
Mientras que los grupos de seguridad de red, rutas definidas por el usuario y la tunelización forzada proporcionan un nivel de seguridad en los niveles de red y el transporte de Hola de hello [modelo OSI](https://en.wikipedia.org/wiki/OSI_model), puede haber ocasiones cuando desee tooenable seguridad en niveles superiores de red de Hola.

Por ejemplo, sus requisitos de seguridad podrían incluir:

* Autenticación y autorización antes de permitir el acceso tooyour aplicación
* Detección de intrusiones y respuesta a estas
* Inspección de la capa de aplicación para comprobar la existencia de protocolos de alto nivel
* Filtrado para direcciones URL
* Antimalware y antivirus de nivel de red
* Protección contra robots
* Control de acceso a las aplicaciones
* Protección frente a DDoS adicional (por encima de Hola de protección que proporciona DDoS de hello Azure fabric propio)

Puede tener acceso a estas características de seguridad de red mejoradas mediante el uso de una solución de socio de Azure. Puede encontrar Hola soluciones de seguridad de red de asociado de Azure más recientes visitando hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) y busque "seguridad" y "seguridad de red".

## <a name="secure-remote-access-and-cross-premises-connectivity"></a>Acceso remoto seguro y conectividad entre entornos
El programa de instalación, configuración y administración de los recursos de Azure debe toobe realizar de forma remota. Además, puede que desee toodeploy [TI híbrida](http://social.technet.microsoft.com/wiki/contents/articles/18120.hybrid-cloud-infrastructure-design-considerations.aspx) soluciones que tienen componentes locales y en hello nube pública de Azure. Estos escenarios requieren acceso remoto seguro.

Las redes de Azure admite Hola acceso remoto seguro a los escenarios siguientes:

* Conectar estaciones de trabajo individuales tooan red Virtual de Azure
* Conectar su tooan de red local red Virtual de Azure con una VPN
* Conectar su tooan de red local red Virtual de Azure con un vínculo WAN dedicado
* Conectar redes virtuales de Azure tooeach otros

### <a name="connect-individual-workstations-tooan-azure-virtual-network"></a>Conectar estaciones de trabajo individuales tooan red Virtual de Azure
Puede haber ocasiones cuando se desea tooenable individuales a los desarrolladores u operaciones personal toomanage máquinas virtuales y servicios de Azure. Por ejemplo, necesita tener acceso a la máquina virtual de tooa en una red Virtual de Azure y la directiva de seguridad no permite el acceso remoto de RDP o SSH tooindividual las máquinas virtuales. En este caso, puede usar una conexión VPN de punto a sitio.

Hola conexión VPN usa Hola point-to-site [VPN SSTP](https://technet.microsoft.com/library/cc731352.aspx) protocolo tooenable tooset una conexión privada y segura entre usuarios de Hola y Hola red Virtual de Azure. Una vez establecida la conexión VPN de hello, usuario Hola será capaz de tooRDP o SSH a través de VPN de hello vincular en cualquier máquina virtual en hello (suponiendo que hello usuario pueda autenticar y está autorizado) de red Virtual de Azure.

Más información:

* [Configurar una tooa de conexión de punto a sitio de red Virtual mediante PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

### <a name="connect-your-on-premises-network-tooan-azure-virtual-network-with-a-vpn"></a>Conectar su red local tooan red Virtual de Azure con una VPN
Puede que desee tooconnect su toda la red corporativa o determinadas partes de él, tooan red Virtual de Azure. Esto es habitual en escenarios de TI híbridos donde las empresas [amplían su centro de datos local a Azure](https://gallery.technet.microsoft.com/Datacenter-extension-687b1d84). En muchos casos, las empresas hospedarán partes de un servicio en Azure y partes en el entorno local, como cuando una solución incluye servidores web front-end en Azure y bases de datos de back-end en local. Estos tipos de conexiones "entre locales" también hacen que la administración de recursos ubicados en Azure sea más segura y permiten escenarios como la ampliación de controladores de dominio de Active Directory a Azure.

Una manera de tooaccomplish es toouse una [VPN de sitio a sitio](https://www.techopedia.com/definition/30747/site-to-site-vpn). Hola diferencia entre una VPN de sitio a sitio y una VPN de sitio a punto es que una VPN de punto a sitio se conecta un tooan de dispositivo única red Virtual de Azure, mientras una VPN de sitio a sitio se conecta a una red Virtual de Azure tooan de toda la red (por ejemplo, la red local) . VPN de sitio a sitio tooan red Virtual de Azure usan el protocolo VPN para el modo el altamente seguro túnel IPsec Hola.

Más información:

* [Crear un administrador de recursos de VNet con una conexión de VPN de sitio a sitio mediante Hola Portal de Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [Planeamiento y diseño de puerta de enlace de VPN](../vpn-gateway/vpn-gateway-plan-design.md)

### <a name="connect-your-on-premises-network-tooan-azure-virtual-network-with-a-dedicated-wan-link"></a>Conectar su red Virtual de Azure tooan de red local con un vínculo WAN dedicado
Las conexiones VPN de punto a sitio y de sitio a sitio son eficaces para permitir la conectividad entre locales. Sin embargo, algunas organizaciones tenerlos en cuenta hello toohave siguientes desventajas:

* Las conexiones VPN mover datos a través de Internet de hello: Esto expone estos problemas de seguridad de las conexiones toopotential involucrados en el movimiento de datos desde una red pública. Además, no se puede garantizar la confiabilidad y disponibilidad de las conexiones a Internet.
* Las conexiones de VPN tooAzure redes virtuales se puede considerar ancho de banda restringido para algunas aplicaciones y propósitos, como se max out a aproximadamente 200 Mbps.

Las organizaciones que necesitan Hola nivel más alto de seguridad y la disponibilidad de sus conexiones entre entornos normalmente utilizar vínculos WAN dedicados tooconnect tooremote sitios. Azure proporciona que Hola capacidad toouse un vínculo WAN dedicado que se puede usar tooconnect su tooan de red local red Virtual de Azure. Para ello se utiliza ExpressRoute de Azure.

Más información:

* [Información técnica de ExpressRoute](../expressroute/expressroute-introduction.md)

### <a name="connect-azure-virtual-networks-tooeach-other"></a>Conectar redes virtuales de Azure tooEach otros
Es posible que se toouse varias redes virtuales de Azure para sus implementaciones. Hay muchas razones para hacer esto. Uno de los motivos de hello puede ser toosimplify administración; otro podría darse por motivos de seguridad. Independientemente de la motivación de Hola o análisis razonado para poner los recursos en diferentes redes virtuales de Azure, puede haber ocasiones desee recursos en cada uno de hello tooconnect de redes entre sí.

Una opción sería para los servicios en una red Virtual de Azure tooconnect tooservices en otra red Virtual de Azure "bucle atrás" a través de Internet de Hola. conexión de Hello podría iniciar en una red Virtual de Azure, vaya a través de Internet de hello y, a continuación, vuelven a estar toohello destino red Virtual de Azure. Esta opción expone Hola conexión toohello seguridad problemas inherentes tooany comunicación basada en Internet.

Una mejor opción podría ser toocreate un Virtual de Azure VPN de sitio a sitio de red de Virtual de red en Azure. Esta red Virtual de Virtual de Azure de red en Azure VPN de sitio a sitio usa Hola mismo [el modo de túnel IPsec](https://technet.microsoft.com/library/cc786385.aspx) protocolo como conexión de VPN de sitio a sitio Hola entre entornos mencionado anteriormente.

ventaja de Hola de usar un Virtual de Azure VPN de sitio a sitio de red de Virtual de red en Azure es que se establece la conexión de VPN de hello sobre Hola tejido de red de Azure en lugar de conectarse a través de Internet de Hola. Esto proporciona que un nivel adicional de seguridad comparó toosite-to-site VPN que se conectan a través de Internet de Hola.

Más información:

* [Configuración de una conexión entre dos redes virtuales mediante Azure Resource Manager y PowerShell](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

## <a name="availability"></a>Disponibilidad
La disponibilidad es un componente clave de cualquier programa de seguridad. Si no puede acceder a sus usuarios y sistemas lo que necesita tooaccess sobre Hola de red, hello puede considerarse como servicio en peligro. Azure tiene ese Hola de compatibilidad después de mecanismos de alta disponibilidad de las tecnologías de red:

* Equilibrio de carga basado en HTTP
* Equilibrio de carga de nivel de red
* Equilibrio de carga global

Equilibrio de carga es un mecanismo diseñado tooequally distribuir conexiones entre varios dispositivos. objetivos de Hola de equilibrio de carga son:

* Aumentar la disponibilidad: aunque cargar equilibrar conexiones entre varios dispositivos, uno o varios de los dispositivos de hello pueden estar disponible y servicios de Hola que se ejecutan en hello restantes dispositivos conectados a Internet pueden continuar contenido de hello tooserve del servicio de Hola
* Aumentar el rendimiento: al cargar las conexiones de saldo en varios dispositivos, un único dispositivo no tiene el procesador de hello tootake de llamadas. En su lugar, las peticiones de memoria y procesamiento de Hola para servir contenido Hola se reparte entre varios dispositivos.

### <a name="http-based-load-balancing"></a>Equilibrio de carga basado en HTTP
Organizaciones que ejecutan servicios basados en web a menudo deseo toohave un equilibrador de carga basado en HTTP delante de esos toohelp de servicios web garantizar niveles adecuados de rendimiento y alta disponibilidad. En cambio tootraditional basados en red equilibradores de carga, hello las decisiones de equilibrio de carga tomadas por equilibradores de carga basado en HTTP se basan las características del protocolo de hello HTTP, no en los protocolos de capa de transporte y de red de Hola.

tooprovide, basado en HTTP equilibrio de carga para los servicios basados en web, Azure proporciona Hola puerta de enlace de aplicaciones de Azure. Hola admite la puerta de enlace de aplicaciones de Azure:

* Basado en HTTP equilibrio de carga: decisiones de equilibrio de carga se realizan en función de protocolo toohello especiales características HTTP
* Afinidad de sesión basado en cookies: esta funcionalidad se asegura que establecen conexiones permanece intacta entre servidor y cliente hello tooone de servidores de hello detrás de ese equilibrador de carga. Esto asegura la estabilidad de las transacciones.
* Descarga SSL: cuando se establece una conexión de cliente con equilibrio de carga de hello, que la sesión entre el cliente de Hola y el equilibrador de carga de hello está cifrada con hello HTTPS (SSL /) protocolo. Sin embargo, en el rendimiento de orden tooincrease, tiene Hola opción toohave Hola conexión entre el equilibrador de carga de Hola y el servidor de web Hola detrás de protocolo de HTTP (sin cifrar) de Hola de uso equilibrador de carga de Hola. Se trata de tooas que se hace referencia "descarga SSL" porque Hola servidores detrás de equilibrador de carga de hello no sufran sobrecarga del procesador Hola relacionada con el cifrado y, por tanto, deben ser capaz de tooservice solicitudes más rápidamente.
* Enrutamiento contenido basado en dirección URL: esta característica hace posible que las decisiones de toomake de equilibrador de carga de hello en donde las conexiones de tooforward basan en dirección URL de destino de Hola. Este método proporciona mucha más flexibilidad que las soluciones que toman decisiones sobre el equilibrio de carga según las direcciones IP.

Más información:

* [Introducción a Puerta de enlace de aplicaciones](../application-gateway/application-gateway-introduction.md)

### <a name="network-level-load-balancing"></a>Equilibrio de carga de nivel de red
En cambio basado en tooHTTP equilibrio de carga, equilibrio de carga de nivel de red hace que cargar Equilibrio decisiones basadas en direcciones números IP y puerto (TCP o UDP).
Puede obtener beneficios de Hola de nivel equilibrio de carga en Azure mediante el uso de hello equilibrador de carga de Azure. Algunas características claves de hello equilibrador de carga de Azure incluyen:

* Equilibrio de carga de nivel de red basado en la dirección IP y el número de puerto.
* Compatibilidad con cualquier protocolo de capa de aplicación.
* Equilibra la carga de máquinas virtuales de tooAzure e instancias de rol de servicios de nube
* Puede utilizarse en aplicaciones y máquinas virtuales accesibles desde Internet (equilibrio de carga externo) y no accesibles desde Internet (equilibrio de carga interno).
* Extremo de supervisión, que es usado toodetermine si alguno de los servicios de hello detrás de equilibrador de carga de hello ya no esté disponible

Más información:

* [Equilibrador de carga accesible desde Internet entre varias máquinas virtuales o servicios](../load-balancer/load-balancer-internet-overview.md)
* [Información general sobre el equilibrador de carga interno](../load-balancer/load-balancer-internal-overview.md)

### <a name="global-load-balancing"></a>Equilibrio de carga global
Algunas organizaciones desearán máximo nivel de disponibilidad de hello posibles. Una manera de tooreach que este objetivo es toohost aplicaciones en todo el mundo distribuido centros de datos. Cuando una aplicación está hospedada en centros de datos situados a lo largo de Hola a todos, es posible para un toobecome toda la región geopolíticos disponible y aún tiene aplicación hello y en ejecución.

Además toohello ventajas de disponibilidad que obtendrá al hospedar aplicaciones en los centros de datos distribuidos globalmente, también puede obtener ventajas de rendimiento. Estas ventajas de rendimiento se pueden obtener mediante un mecanismo que dirige las solicitudes de centro de datos de la toohello de servicio de Hola que está más cerca de dispositivo toohello que está realizando la solicitud de Hola.

El equilibrio de carga global puede proporcionarle ambas ventajas. En Azure, puede obtener beneficios de hello global de equilibrio de carga mediante el Administrador de tráfico de Azure.

Más información:

* [¿Qué es el Administrador de tráfico?](../traffic-manager/traffic-manager-overview.md)


## <a name="name-resolution"></a>Resolución de nombres
La resolución de nombres es una función crítica para todos los servicios hospedados en Azure. Desde la perspectiva de seguridad, riesgo en función de la resolución de nombre de hello puede provocar las solicitudes de tooan atacante redirección desde el sitio del atacante de tooan sitios. Proteger la resolución de nombres es un requisito de todos los servicios hospedados en la nube.

Hay dos tipos de resolución de nombres que debe tooaddress:

* Resolución de nombres interna: la resolución de nombres interna la usan los servicios en las redes virtuales de Azure, las redes locales o ambas. Los nombres usados para la resolución de nombres interna no son accesibles a través de Internet Hola. Para lograr una seguridad óptima, es importante que el esquema de resolución de nombre interno no es accesible tooexternal a los usuarios.
* Resolución de nombres externa: la resolución de nombres externa la utilizan las personas y los dispositivos fuera de las redes locales y virtuales de Azure. Estos son los nombres de Hola que sean visible toohello Internet y servicios en la nube de toodirect usa conexión tooyour.

Para la resolución de nombres interna, tiene dos opciones:

* Un servidor DNS de red virtual de Azure: cuando se crea una nueva red virtual de Azure, un servidor DNS se crea automáticamente. Este servidor DNS puede resolver nombres de Hola de máquinas de hello ubicados en esa red Virtual de Azure. Este servidor DNS no es configurable y está administrado por el Administrador de tejido de Azure hello, lo que una solución de resolución de nombre seguro.
* Traer su propio servidor DNS: tiene la opción de Hola de colocar un servidor DNS de su propia elección de la red Virtual de Azure. Este servidor DNS podría ser que un Active Directory integrado servidor DNS o una solución de servidor DNS dedicada proporcionada por un asociado de Azure, que puede obtener de hello Azure Marketplace.

Más información:

* [Información general sobre redes virtuales](../virtual-network/virtual-networks-overview.md)
* [Administración de servidores DNS usados por una red virtual](../virtual-network/virtual-network-manage-network.md#dns-servers)

Para la resolución DNS externa, tiene dos opciones:

* Hospedar su propio servidor DNS externo en el entorno local
* Hospedar su propio servidor DNS externo con un proveedor de servicios

Muchas organizaciones de gran tamaño hospedarán sus propios servidores DNS en el entorno local. Puede hacerlo porque tienen Hola redes experiencia y presencia global toodo así.

En la mayoría de los casos, es mejor toohost la resolución de nombres DNS de servicios con un proveedor de servicios. Estos proveedores de servicios tienen experiencia en red hello y presencia global tooensure muy alta disponibilidad para los servicios de resolución de nombres. La disponibilidad es esencial para servicios de DNS, ya que si la resolución de nombres de servicios producirá un error, nadie puede tooreach capaz de servicios de Internet.

Azure ofrece una alta disponibilidad y rendimiento de solución DNS externo en forma de Hola de DNS de Azure. Esta solución de resolución de nombres externa aprovecha la infraestructura de DNS de Azure en todo el mundo Hola. Le permite toohost su dominio en Azure mediante Hola mismas credenciales, API, herramientas y facturación como los servicios de Azure. Como parte de Azure, también hereda los controles de seguridad segura de hello integrados en la plataforma de Hola.

Más información:

* [Introducción a DNS de Azure](../dns/dns-overview.md)

## <a name="dmz-architecture"></a>Arquitectura de red perimetral (DMZ)
Muchas organizaciones empresariales usan DMZ toosegment su toocreate una franja de redes entre Hola Internet y sus servicios. parte de la red Perimetral de Hola de red de Hola se considera una zona de seguridad baja y no activos de gran valor se colocan en ese segmento de red. Normalmente verá los dispositivos de seguridad de red que tienen una interfaz de red en el segmento de red Perimetral de Hola y otra red tooa conectado de la interfaz de red que tiene máquinas virtuales y servicios que acepten las conexiones entrantes de hello Internet.

Hay una serie de variaciones de diseño de la red Perimetral y Hola decisión toodeploy una red Perimetral y, a continuación, ¿qué tipo de red Perimetral toouse si decide toouse uno, se basa en los requisitos de seguridad de red.

Más información:

* [Servicios en la nube de Microsoft y seguridad de red](../best-practices-network-security.md)


## <a name="monitoring-and-threat-detection"></a>Detección de amenazas y supervisión

Azure proporciona capacidades toohelp en esta área clave con temprano detección, supervisión y Hola capacidad toocollect y revisión de tráfico de red.

### <a name="azure-network-watcher"></a>Azure Network Watcher
Monitor de red de Azure incluye un gran número de funciones que ayuda a solucionar el problema, así como proporcionar un nuevo conjunto completo de herramientas tooassist con identificación de hello problemas de seguridad.

[Vista de grupo de seguridad ](/network-watcher/network-watcher-security-group-view-overview.md) ayuda con el cumplimiento de seguridad y auditoría de las máquinas virtuales y puede ser usado tooperform auditorías mediante programación comparar las directivas de las líneas de base de hello definidas por las reglas de tooeffective de organización para cada una de las máquinas virtuales. Esto puede ayudarle a identificar cualquier cambio en la configuración.

[Captura de paquetes](/network-watcher/network-watcher-packet-capture-overview.md) permite toocapture tooand de tráfico de red de la máquina virtual de Hola. Además de ayudar al permitir que las estadísticas de red toocollect y a solucionar el problema de aplicación Hola captura de paquetes de problemas puede ser muy valiosa en investigación de Hola de intrusiones de red. También puede utilizar esta funcionalidad junto con funciones de Azure capturas de red de toostart en respuesta toospecific Azure alertas.

Para obtener más información sobre el Monitor de red de Azure y cómo probar algunas de las funcionalidades de hello en los laboratorios de toostart Eche un vistazo a hello [información general sobre supervisión de Monitor de red de Azure](/network-watcher/network-watcher-monitoring-overview.md)

>[!NOTE]
Monitor de red de Azure aún está en vista previa pública por lo que puede no haber Hola mismo nivel de disponibilidad y confiabilidad son servicios que son en general la versión de disponibilidad. Puede que algunas características no se admitan, que tengan funcionalidades limitadas y que no estén disponibles en todas las ubicaciones de Azure. Para hello más las notificaciones de actualización de disponibilidad y estado de este servicio, consulte hello [página actualizaciones de Azure](https://azure.microsoft.com/updates/?product=network-watcher)

### <a name="azure-security-center"></a>Azure Security Center
Centro de seguridad le ayuda a evitar, detectar y responder toothreats y proporciona que mayor visibilidad en y control sobre, seguridad de Hola de los recursos de Azure. Proporciona administración de directivas y supervisión de la seguridad integrada en las suscripciones de Azure, ayuda a detectar las amenazas que podrían pasar desapercibidas y funciona con un amplio conjunto de soluciones de seguridad.

Azure Security Center le ayuda a optimizar y controlar la seguridad de la red al:

* Proporcionar recomendaciones de seguridad de la red
* Supervisión del estado de saludo de la configuración de seguridad de red
* Las alertas toonetwork según las amenazas tanto en los niveles de red y de punto de conexión de Hola

Más información:

* [Introducción tooAzure centro de seguridad](../security-center/security-center-intro.md)


### <a name="logging"></a>Registro
El registro en el nivel de red es una función clave en cualquier escenario de seguridad de red. En Azure, puede registrar información obtenida de nivel de red de grupos de seguridad de red tooget registrar información. Con el registro de NSG, obtiene información de:

* [Registros de actividad](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) : estos registros son tooview usado todas las operaciones envían tooyour Azure suscripciones. Estos registros están habilitados de forma predeterminada y se pueden usar en hello portal de Azure. Anteriormente se les llamaba "Registros de auditoría" o "Registros operativos".
* Los registros de eventos: estos registros proporcionan información sobre las reglas NSG que se aplicaron.
* Registros de contador: estos registros permiten saber cuántas veces en cada regla NSG fue toodeny aplicado o permitan el tráfico.

También puede usar [Microsoft Power BI](https://powerbi.microsoft.com/what-is-power-bi/), una visualización de datos eficaz herramienta tooview y analizar estos registros.

Más información:

* [Análisis del registro para grupos de seguridad de red (NSG)](../virtual-network/virtual-network-nsg-manage-log.md)
