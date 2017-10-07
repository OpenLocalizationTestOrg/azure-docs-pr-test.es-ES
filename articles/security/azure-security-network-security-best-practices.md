---
title: "Prácticas recomendadas de seguridad de red aaaAzure | Documentos de Microsoft"
description: "Este artículo proporciona un conjunto de procedimientos recomendados de seguridad de la red con funcionalidades de Azure integradas."
services: security
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: TomShinder
ms.assetid: 7f6aa45f-138f-4fde-a611-aaf7e8fe56d1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: TomSh
ms.openlocfilehash: 5867dea358b4da65c65b3e52fcab7e687e981642
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security-best-practices"></a>Procedimientos recomendados de seguridad de la red de Azure
Microsoft Azure permite dispositivos de tooother conectados en red de máquinas virtuales y aparatos tooconnect situándolos en redes virtuales de Azure. Red Virtual de Azure es una construcción de red virtual que permite a tooconnect red virtual interfaz tarjetas tooa virtual tooallow basadas en TCP/IP comunicaciones de red entre dispositivos habilitados para red. Máquinas virtuales de Azure conectado tooan red Virtual de Azure están tooconnect puede toodevices en Hola misma Azure red Virtual, redes virtuales diferentes de Azure, en Internet de Hola o incluso en sus propias redes locales.

En este artículo veremos un conjunto de procedimientos recomendados de seguridad de la red de Azure. Estas prácticas recomendadas se derivan de nuestra experiencia con las redes Azure y experiencias de Hola de clientes como usted.

Para cada procedimiento recomendado, explicaremos:

* ¿Qué recomienda Hola
* ¿Por qué desea tooenable este procedimiento recomendado
* ¿Qué podría ser resultado de hello si no se recomienda tooenable Hola
* Procedimiento recomendado de las alternativas posibles toohello
* ¿Cómo puede obtener información práctica recomendada de hello tooenable

En este artículo de prácticas recomendadas de seguridad de red de Azure se basa en una opinión de consenso y capacidades de la plataforma Windows Azure y conjuntos de características, tal como aparecen en tiempo de Hola que se escribió este artículo. Las opiniones y las tecnologías que cambian con el tiempo y este artículo será esos cambios se actualizaron en un tooreflect de forma periódica.

Los procedimientos recomendados de seguridad de la red de Azure descritos en este artículo incluyen:

* Segmentación lógica de subredes
* Control del comportamiento de enrutamiento
* Habilitación de la tunelización forzada
* Uso de aplicaciones de red virtual
* Implementación de redes perimetrales para zonas de seguridad
* Evitar la exposición toohello Internet con vínculos WAN dedicados
* Optimización del rendimiento y el tiempo de actividad
* Uso del equilibrio de carga global
* Deshabilitar el acceso RDP tooAzure máquinas virtuales
* Habilitación de Azure Security Center
* Extensión de su centro de datos en Azure

## <a name="logically-segment-subnets"></a>Segmentación lógica de subredes
[Redes virtuales de Azure](https://azure.microsoft.com/documentation/services/virtual-network/) son similares LAN tooa en su red local. Hello idea que subyace a una red Virtual de Azure es que se crea una único privada red dirección IP basada en el espacio en el que puede colocar todos los [máquinas virtuales de Azure](https://azure.microsoft.com/services/virtual-machines/). Hola privados espacios de direcciones IP disponibles están en hello (10.0.0.0/8), de la clase A clase B (172.16.0.0/12) y la clase C de intervalos (192.168.0.0/16).

Toowhat similar local, debe tener más de espacio de direcciones de toosegment hello en subredes. Puede usar [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) según las subredes principios toocreate las subredes.

Enrutamiento entre subredes realizará automáticamente y no es necesario toomanually configurar tablas de enrutamiento. Sin embargo, la configuración predeterminada de hello es que no hay ningún control de acceso de red entre las subredes de hello que crear en hello red Virtual de Azure. En los controles de acceso de orden toocreate red entre subredes, necesitará tooput algo entre subredes Hola.

Una de estas cosas Hola usar tooaccomplish esta tarea es un [grupo de seguridad de red](../virtual-network/virtual-networks-nsg.md) (NSG). Los NSG son la inspección de paquetes con estado simple dispositivos que usan Hola 5-tupla (Hola IP de origen, puerto de origen, dirección IP de destino, puerto de destino y el protocolo de capa 4) enfocan toocreate permitir/denegar reglas para el tráfico de red. Puede permitir o denegar el tráfico tooand desde la dirección IP única, tooand desde varias direcciones IP o incluso tooand de subredes enteras.

Con los NSG de control de acceso de red entre subredes permite tooput recursos que pertenecen toohello misma zona de seguridad o una función de sus propias subredes. Por ejemplo, imagine una aplicación sencilla de 3 niveles con un nivel de web, un nivel lógico de aplicación y un nivel de base de datos. Coloque las máquinas virtuales que pertenecen tooeach de estos niveles en sus propias subredes. A continuación, use los NSG toocontrol tráfico entre subredes hello:

* Máquinas virtuales de nivel de Web solo se pueden iniciar máquinas de lógica de aplicación de las conexiones toohello y solo se pueden aceptar conexiones de Internet de Hola
* Máquinas virtuales de lógica de aplicación sólo se pueden iniciar conexiones con el nivel de base de datos y solo se pueden aceptar conexiones de nivel de web Hola
* Máquinas virtuales de nivel de base de datos no se puede iniciar la conexión con cualquier elemento fuera de su propia subred y solo se pueden aceptar conexiones de capa de lógica de aplicación Hola

toolearn más acerca de los grupos de seguridad de red y cómo puede usarlos toologically segmento las redes virtuales de Azure, lea el artículo de hello [¿qué es un grupo de seguridad de red](../virtual-network/virtual-networks-nsg.md) (NSG).

## <a name="control-routing-behavior"></a>Control del comportamiento de enrutamiento
Cuando se coloca una máquina virtual en una red Virtual de Azure, observará que la máquina virtual Hola puede conectarse tooany otra máquina virtual en Hola misma red Virtual de Azure, incluso si hello otras máquinas virtuales están en subredes diferentes. motivo de Hello ¿por qué esto es posible es que hay una colección de rutas de sistema que están habilitadas de forma predeterminada que permiten a este tipo de comunicación. Estas rutas predeterminadas permiten a las máquinas virtuales de hello misma red Virtual de Azure tooinitiate las conexiones entre sí y con hello Internet (para comunicaciones salientes a toohello Internet solo).

Mientras que las rutas de sistema de hello predeterminadas son útiles para muchos escenarios de implementación, hay veces que desee toocustomize configuración de enrutamiento de Hola para las implementaciones. Estas personalizaciones le permitirá tooconfigure Hola siguiente salto dirección tooreach destinos concretos.

Se recomienda configurar rutas definidas por el usuario al implementar una aplicación de seguridad de la red virtual; en otro procedimiento recomendado, más adelante, se tratará este tema.

> [!NOTE]
> Rutas definidas por el usuario no son necesarias y las rutas de sistema de hello predeterminadas funcionará en la mayoría de las instancias.
>
>

Puede aprender más acerca de rutas definidas por el usuario y cómo tooconfigure usarlas, lea el artículo de hello [¿qué son rutas definidas por el usuario y el reenvío IP](../virtual-network/virtual-networks-udr-overview.md).

## <a name="enable-forced-tunneling"></a>Habilitación de la tunelización forzada
toobetter comprender la tunelización forzada, resulta útil toounderstand qué "división de túnel" es.
ejemplo de Hola a más comunes de túnel dividido se ve con conexiones VPN. Imagine que establecer una conexión VPN de la red corporativa de hotel sala tooyour. Esta conexión permite tooconnect tooresources en su red corporativa y vaya tooresources de todas las comunicaciones de la red corporativa a través de túnel VPN de Hola.

¿Qué ocurre cuando se desea tooconnect tooresources en hello Internet? Cuando se habilita el túnel dividido, estas conexiones ir directamente a toohello Internet y no a través de hello VPN de túnel. Tenga en cuenta este toobe un riesgo potencial de algunos expertos en seguridad y, por tanto, se recomienda que se deshabilite el túnel dividido y todas las conexiones, los destinados a Hola Internet y los destinados a recursos corporativos, vaya a través del túnel VPN de Hola. ventaja de Hola de hacerlo es que toohello conexiones Internet, a continuación, se convierten obligatoriamente a través de dispositivos de seguridad de red corporativa de hello, que no sería el caso de hello si había conectado de cliente VPN de hello toohello Internet fuera de túnel VPN de Hola.

Ahora vamos a hacer esto encenderlo toovirtual máquinas de red Virtual de Azure. las rutas predeterminadas de Hola para una red Virtual de Azure permite que las máquinas virtuales tooinitiate tráfico toohello Internet. Esto demasiado puede representar un riesgo de seguridad, que pudieron aumentar la superficie expuesta a ataques Hola de una máquina virtual de estas conexiones salientes y ser usadas por atacantes.
Por este motivo, se recomienda habilitar la tunelización forzada en las máquinas virtuales cuando tiene conectividad entre locales entre la red virtual de Azure y su red local. Hablaremos acerca de conectividad entre entornos locales más adelante en este documento de procedimientos recomendados de redes de Azure.

Si no tiene una conexión entre entornos, asegúrese de que sacar partido de los grupos de seguridad de red (descrito anteriormente) o Azure tooprevent conexiones salientes toohello Internet desde su Virtual de Azure de red virtual seguridad aparatos (descrito a continuación) Máquinas.

Obtenga más información sobre toolearn tunelización forzada y cómo tooenable, lea el artículo de hello [configurar tunelización forzada mediante PowerShell y el Administrador de recursos de Azure](../vpn-gateway/vpn-gateway-forced-tunneling-rm.md).

## <a name="use-virtual-network-appliances"></a>Uso de aplicaciones de red virtual
Mientras que los grupos de seguridad de red y usuario definido el enrutamiento pueden proporcionar un cierto grado de seguridad de red en hello las capas de red y el transporte de hello [modelo OSI](https://en.wikipedia.org/wiki/OSI_model), va toobe situaciones en la que desea o necesita tooenable seguridad en los niveles altos de pila de Hola. En tales situaciones, se recomienda implementar aplicaciones de seguridad de la red virtual proporcionadas por asociados de Azure.

Las aplicaciones de seguridad de la red de Azure pueden proporcionar niveles de seguridad mucho mejores que los proporcionados por los controles de nivel de red. Algunas de las capacidades de seguridad de red Hola proporcionadas por dispositivos de seguridad de red virtual son:

* Firewalls
* Detección y prevención de intrusiones
* Administración de vulnerabilidades
* Control de aplicaciones
* Detección de anomalías basadas en la red
* Filtrado de web
* Antivirus
* Protección de redes de robots (botnets)

Si necesita un nivel de seguridad de la red mayor que el que se puede obtener con los controles de acceso al nivel de red, se recomienda investigar e implementar aplicaciones de seguridad de la red virtual de Azure.

toolearn acerca de los dispositivos de seguridad de red virtual de Azure están disponibles y sus capacidades, visite hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) y busque "seguridad" y "seguridad de la red".

## <a name="deploy-dmzs-for-security-zoning"></a>Implementación de redes perimetrales para zonas de seguridad
Una red Perimetral o "red perimetral" es físico o segmento de red lógica que está diseñado tooprovide una capa adicional de seguridad entre los activos y Hola Internet. propósito de Hola de hello DMZ es tooplace especializado dispositivos de control de acceso a redes en borde de Hola de red de hello red Perimetral para que se permita solo el tráfico deseado más allá de los dispositivos de seguridad de red de Hola y en la red Virtual de Azure.

DMZ es útiles porque puede Centrar la administración de control de acceso de red, supervisión, registros e informes en dispositivos de hello en el perímetro de saludo de la red Virtual de Azure. Aquí normalmente habilitaría la prevención DDoS, los sistemas de prevención y detección de intrusiones (IDS/IPS), las reglas y directivas de firewall, el filtrado web, el antimalware de la red, etc. dispositivos de seguridad de red de Hola se colocan entre Hola Internet y la red Virtual de Azure y tienen una interfaz en ambas redes.

Aunque se trata de diseño básico de Hola de una red Perimetral, hay muchos distintos diseños de red Perimetral, como opuesta, alojada tri, host múltiple y otros.

Se recomienda que considere la posibilidad de implementar un nivel de red Perimetral tooenhance Hola de seguridad de red para los recursos de Azure para todas las implementaciones de alta seguridad.

más información acerca de DMZ y cómo toodeploy en Azure, lea el artículo de hello toolearn [servicios de nube de Microsoft y seguridad de red](../best-practices-network-security.md).

## <a name="avoid-exposure-toohello-internet-with-dedicated-wan-links"></a>Evitar la exposición toohello Internet con vínculos WAN dedicados
Muchas organizaciones han elegido la ruta de TI híbrida Hola. En TI híbrida, algunos de los activos de información de la compañía de hello son en Azure, mientras que otros usuarios permanecen en local. En muchos casos, algunos componentes de un servicio se ejecutan en Azure, mientras que otros componentes siguen siendo locales.

En entornos híbridos de hello escenario de TI, normalmente hay algún tipo de conectividad entre entornos. Esto entre entornos conectividad permite Hola empresa tooconnect su tooAzure de redes locales redes virtuales. Hay dos soluciones de conectividad entre locales:

* VPN de sitio a sitio
* ExpressRoute

[VPN de sitio a sitio](../vpn-gateway/vpn-gateway-site-to-site-create.md) representa una conexión privada virtual entre su red local y una red virtual de Azure. Esta conexión tiene lugar en Hola Internet y le permite demasiado "tunelizar" información dentro de un vínculo entre la red y Azure cifrado. La VPN de sitio a sitio es una tecnología segura y madura que empresas de todos los tamaños han implementado durante décadas. El cifrado del túnel se realiza con el [modo de túnel IPsec](https://technet.microsoft.com/library/cc786385.aspx).

Mientras VPN de sitio a sitio es una tecnología de confianza, confiable y establecida, tráfico de túnel de hello atravesar Hola Internet. Además, el ancho de banda es relativamente limitada tooa máximo de sobre (200 Mbps).

Si necesita un nivel de seguridad o de rendimiento excepcional para las conexiones entre locales, se recomienda utilizar Azure ExpressRoute para su conectividad. ExpressRoute es un vínculo de WAN dedicada entre su ubicación local o un proveedor de hospedaje de Exchange. Porque se trata de una conexión de telecomunicaciones, los datos no se transmiten a través de Internet de Hola y es, por tanto, no se expone toohello posibles riesgos inherentes a las comunicaciones de Internet.

toolearn más acerca del funcionamiento de ExpressRoute de Azure y cómo toodeploy, por favor, lea el artículo de hello [información general técnica de ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="optimize-uptime-and-performance"></a>Optimización del rendimiento y el tiempo de actividad
Confidencialidad, integridad y disponibilidad (CIA) comprenden tres Hola del modelo de seguridad más influyente de hoy en día. Confidencialidad es acerca del cifrado y la privacidad, la integridad es asegurarse de que personal no autorizado no cambian los datos y disponibilidad consiste en asegurarse de que las personas autorizadas son tooaccess capaz de obtener información de hello que están autorizados tooaccess. Un error en cualquiera de estas áreas representa una posible infracción de seguridad.

La disponibilidad puede referirse al tiempo de actividad y el rendimiento. Si un servicio está inactivo, no puede accederse a la información. Si el rendimiento es tan bajo como datos de hello toomake inutilizables, a continuación, podemos consideramos Hola datos toobe inaccesible. Por lo tanto, desde una perspectiva de seguridad, necesitamos toodo cualquier podemos toomake que nuestros servicios tengan tiempo de actividad óptimo y el rendimiento.
Un método eficaz y popular usa tooenhance disponibilidad y el rendimiento es toouse equilibrio de carga. El equilibrio de carga es un método para distribuir el tráfico de la red entre los servidores que forman parte de un servicio. Por ejemplo, si tiene servidores web front-end como parte de su servicio, puede usar Equilibrio de carga tráfico de hello toodistribute entre los servidores web front-end varios.

Esta distribución del tráfico de aumenta la disponibilidad ya que si uno de los servidores web Hola deja de estar disponible, equilibrador de carga de hello dejará de enviar toothat el tráfico de servidor y los servidores de toohello de tráfico de redireccionamiento que aún estén en línea. Equilibrio de carga también mejora el rendimiento, porque hello procesador, la red y la sobrecarga de memoria para servir solicitudes se distribuye entre todos los servidores de equilibrio de carga de Hola

Se recomienda usar el equilibrio de carga siempre que se pueda y, según sea adecuado para los servicios. También se abordará idoneidad en hello las secciones siguientes.
En el nivel de red Virtual de Azure hello, Azure proporciona, con tres primarias opciones de equilibrio de carga:

* Equilibrio de carga basado en HTTP
* Equilibrio de carga externo
* Equilibrio de carga interno

## <a name="http-based-load-balancing"></a>Equilibrio de carga basado en HTTP
Equilibrio de carga basado en HTTP envergadura ninguna decisión sobre qué conexiones toosend del servidor mediante las características del protocolo de hello HTTP. Azure tiene un equilibrador de carga HTTP que pasa el nombre de Hola de puerta de enlace de aplicaciones.

Se recomienda usar la Puerta de enlace de aplicaciones de Azure cuando hay:

* Las aplicaciones que requieren las solicitudes de hello mismo tooreach de sesión de usuario o cliente Hola misma máquina virtual de back-end. Ejemplos de esto serían las aplicaciones de carro de la compra y los servidores de correo web.
* Aplicaciones que desean toofree granjas de servidores web de terminación SSL sobrecarga aprovechando las ventajas de la puerta de enlace de aplicaciones [descarga SSL](https://f5.com/glossary/ssl-offloading) característica.
* Las aplicaciones, como una red de entrega de contenido, que requieren varias solicitudes HTTP en hello mismo toobe de conexión de TCP de larga ejecución enrutar o servidores de back-end de toodifferent con equilibrio de carga.

toolearn más información acerca de cómo funciona la puerta de enlace de aplicaciones de Azure y cómo se pueden utilizar en las implementaciones, lea el artículo de hello [información general sobre la puerta de enlace de aplicaciones](../application-gateway/application-gateway-introduction.md).

## <a name="external-load-balancing"></a>Equilibrio de carga externo
Equilibrio de carga externo tiene lugar cuando las conexiones entrantes de Internet Hola carga equilibrada entre los servidores que se encuentran en una red Virtual de Azure. equilibrador de carga externo de Azure de Hello puede proporcionar esta capacidad y se recomienda que se usa cuando no requieren sesiones permanentes de Hola o la descarga de SSL.

En cambio basado en tooHTTP equilibrio de carga, Hola equilibrador de carga externo usa información en capas de red y el transporte de Hola de hello OSI modelo toomake sus decisiones de red en qué conexión del saldo tooload servidor a.

Recomendamos que use el equilibrio de carga externo siempre que tenga [aplicaciones sin estado](http://whatis.techtarget.com/definition/stateless-app) Aceptar solicitudes entrantes de hello Internet.

toolearn más información acerca de cómo funciona la Hola equilibrador de carga externo de Azure y cómo implementarla, lea el artículo de hello [empezar a crear un equilibrador de carga con conexión a Internet en el Administrador de recursos con PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md).

## <a name="internal-load-balancing"></a>Equilibrio de carga interno
Equilibrio de carga interno es tooexternal similar el equilibrio de carga y utiliza Hola mismo mecanismo tooload equilibrar conexiones toohello servidores detrás de ellos. Hello la única diferencia es que equilibrador de carga de hello en este caso acepta conexiones desde máquinas virtuales que no están en Internet Hola. En la mayoría de los casos, las conexiones de Hola que se aceptan para equilibrio de carga se inicien por dispositivos de red Virtual de Azure.

Se recomienda que realice para escenarios que puede beneficiarse de esta funcionalidad, como cuando se necesitan tooload equilibrar conexiones tooSQL servidores o servidores web interna de equilibrio de carga interna.

toolearn más información acerca de cómo funciona el equilibrio de carga interno de Azure y cómo implementarla, lea el artículo de hello [empezar a crear un equilibrador de carga interno mediante PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md#update-an-existing-load-balancer).

## <a name="use-global-load-balancing"></a>Uso del equilibrio de carga global
Hace posible de la informática en nube pública toodeploy distribuida globalmente las aplicaciones que tienen componentes que se encuentran en los centros de datos distribuidas por todo el mundo de Hola. Esto es posible en Microsoft Azure debido presencia de tooAzure centro de datos global. Por el contrario las tecnologías de equilibrio de carga de toohello se ha mencionado anteriormente, equilibrio de carga global hace posible toomake servicios disponibles incluso cuando todo centros de datos podrían estar disponible.

Puede obtener este tipo de equilibrio de carga global en Azure mediante [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/). Hace que el Administrador de tráfico está equilibrado de posibles tooload servicios de tooyour las conexiones basan en ubicación de hello del usuario de Hola.

Por ejemplo, si usuario Hola realiza un servicio de tooyour de solicitud de hello Europa, conexión hello es dirigido tooyour servicios que están ubicados en un centro de datos de Europa. Esta parte del Administrador de tráfico global de equilibrio de carga ayuda a tooimprove rendimiento dado conectarse toohello más cercano de centro de datos es más rápida que la conexión toodatacenters que están lejos.

En el lado de la disponibilidad de hello, equilibrio de carga global se asegura de que el servicio está disponible incluso si todo un centro de datos debe estar disponible.

Por ejemplo, si un centro de datos de Azure debe estar disponible debido a motivos de tooenvironmental o vencimiento toooutages (por ejemplo, errores de red regional), las conexiones de servicio tooyour sería vuelve a enrutar toohello más cercano de centro de datos en línea. Este equilibrio de carga global se logra al aprovechar las directivas DNS que se pueden crear en el Administrador de tráfico.

Se recomienda usar el Administrador de tráfico para cualquier solución de nube que desarrolle que tiene un ámbito ampliamente distribuido en varias regiones y requiere el nivel más alto de Hola de tiempo de actividad posible.

toolearn más sobre Azure Traffic Manager y cómo toodeploy, lea el artículo de hello [¿qué es el Administrador de tráfico](../traffic-manager/traffic-manager-overview.md).

## <a name="disable-rdpssh-access-tooazure-virtual-machines"></a>Deshabilitar el acceso RDP/SSH tooAzure máquinas virtuales
Es posible tooreach máquinas virtuales de Azure con hello [protocolo de escritorio remoto](https://en.wikipedia.org/wiki/Remote_Desktop_Protocol) (RDP) hello y [Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell) protocolos (SSH). Estos protocolos que sea posible toomanage las máquinas virtuales desde ubicaciones remotas y son estándar para calcular el centro de datos.

posible problema de seguridad Hola con el uso de estos protocolos a través de Internet de hello es que los atacantes pueden usar distintas [por fuerza bruta](https://en.wikipedia.org/wiki/Brute-force_attack) técnicas toogain acceso tooAzure máquinas virtuales. Una vez que los atacantes Hola obtienen acceso, pueden usar la máquina virtual como un punto de inicio para poner en peligro otros equipos de la red Virtual de Azure o incluso ataques dispositivos de red fuera de Azure.

Por este motivo, le recomendamos que deshabilite directa RDP y SSH acceso tooyour máquinas virtuales de Azure de hello Internet. Una vez directa RDP y SSH tener acceso desde Hola que Internet está deshabilitada, tiene otras opciones que puede usar estas máquinas virtuales tooaccess para la administración remota:

* VPN de punto a sitio
* VPN de sitio a sitio
* ExpressRoute

[VPN de punto a sitio](../vpn-gateway/vpn-gateway-point-to-site-create.md) es otro término para una conexión cliente/servidor de VPN con acceso remoto. Una VPN de punto a sitio permite un tooan de tooconnect de usuario única red Virtual de Azure a través de Internet de Hola. Después de que se establezca la conexión de punto a sitio Hola, usuario de hello será capaz de toouse RDP o SSH tooconnect tooany máquinas virtuales ubicadas en hello red Virtual de Azure que Hola usuario conectado toovia point-to-site VPN. Esto se da por supuesto que el usuario hello es tooreach autorizado esas máquinas virtuales.

Point-to-site VPN es más seguro que las conexiones directas de RDP o SSH porque el usuario de hello tiene tooauthenticate dos veces para que conecta tooa virtual machine. En primer lugar, Hola tooauthenticate de necesidades del usuario (y autorizar) conexión de tooestablish Hola point-to-site VPN; en segundo lugar, Hola tooauthenticate de necesidades del usuario (y autorizar) sesión RDP o SSH hello tooestablish.

A [VPN de sitio a sitio](../vpn-gateway/vpn-gateway-site-to-site-create.md) se conecta a una red de tooanother de toda la red a través de Internet de Hola. Puede usar un tooconnect VPN de sitio a sitio en su tooan de red local red Virtual de Azure. Si implementa una VPN de sitio a sitio, los usuarios de su red local será capaz de tooconnect toovirtual máquinas de la red Virtual de Azure mediante el uso de hello RDP o protocolo SSH en Hola conexión de VPN de sitio a sitio y no requiere tooallow directo RDP o SSH tener acceso a través de Internet de Hola.

También puede utilizar un toohello similar de un vínculo WAN dedicado tooprovide funcionalidad VPN de sitio a sitio. Hola principales diferencias son 1. vínculo WAN dedicado de Hello no atraviesan Hola Internet y 2. Los vínculos WAN dedicados suelen ser más estables y eficaces. Azure proporciona una solución de un vínculo WAN dedicado en forma de Hola de [ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).

## <a name="enable-azure-security-center"></a>Habilitación de Azure Security Center
Centro de seguridad de Azure le ayuda a evitar, detectar y responder toothreats y proporciona que mayor visibilidad en y control sobre, seguridad de Hola de los recursos de Azure. Proporciona administración de directivas y supervisión de la seguridad integrada en las suscripciones de Azure, ayuda a detectar las amenazas que podrían pasar desapercibidas y funciona con un amplio ecosistema de soluciones de seguridad.

Azure Security Center le ayuda a optimizar y controlar la seguridad de la red al:

* Proporcionar recomendaciones de seguridad de la red
* Supervisión del estado de saludo de la configuración de seguridad de red
* Las alertas toonetwork según las amenazas tanto en los niveles de red y de punto de conexión de Hola

Recomendamos encarecidamente habilitar Azure Security Center para todas las implementaciones de Azure.

más información sobre el centro de seguridad de Azure y cómo tooenable para las implementaciones, lea el artículo de hello toolearn [Introducción tooAzure centro de seguridad](../security-center/security-center-intro.md).

## <a name="securely-extend-your-datacenter-into-azure"></a>Extensión de su centro de datos en Azure de forma segura
TI de las empresas muchas organizaciones buscan tooexpand en nube de hello en lugar de crecimiento de sus centros de datos local. Este aumento representa una extensión de la infraestructura de TI existente en la nube pública de Hola. Aprovechando las ventajas de entre entornos opciones de conectividad, es posible tootreat las redes virtuales de Azure como simplemente otra subred en sus instalaciones en la infraestructura de red.

Sin embargo, hay muchas tareas de planificación y los problemas de diseño que necesitan toobe atienden primero. Esto es especialmente importante en el área de Hola de seguridad de red. Uno de hello mejores formas toounderstand cómo tratar este tipo de diseño es toosee un ejemplo.

Microsoft ha creado hello [diagrama de arquitectura de referencia de extensión de centro de datos](https://gallery.technet.microsoft.com/Datacenter-extension-687b1d84#content) y admitir toohelp colateral comprender cuál sería una extensión de centro de datos de este tipo. Esto proporciona una implementación de referencia de ejemplo que puede utilizar tooplan y diseñar una nube de toohello de extensión de centro de datos empresarial seguro. Se recomienda que revise este tooget documento una idea de los componentes clave de Hola de una solución segura.

toolearn más información acerca de cómo toosecurely ampliar su centro de datos en Azure, vea el vídeo de hello [tooMicrosoft de ampliar su centro de datos Azure](https://www.youtube.com/watch?v=Th1oQQCb2KA).
