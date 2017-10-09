---
title: "prácticas recomendadas de seguridad de red de aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de que algunas características clave de hello disponibles en Azure toohelp crean entornos de red segura"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: d169387a-1243-4867-a602-01d6f2d8a2a1
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: b851b2862428a8bd5e7525c85584fc1c14ffcabe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-cloud-services-and-network-security"></a>Servicios en la nube de Microsoft y seguridad de red
Servicios en la nube de Microsoft ofrece servicios e infraestructura a gran escala, funcionalidades de calidad empresarial y numerosas opciones de conectividad híbrida. Los clientes pueden elegir tooaccess estos servicios a través de Internet de Hola o con ExpressRoute de Azure, que proporciona conectividad de red privada. plataforma de Microsoft Azure Hola permite a los clientes tooseamlessly ampliar su infraestructura en la nube de Hola y crear arquitecturas de varios niveles. Además, otros fabricantes pueden habilitar funcionalidades mejoradas mediante servicios de seguridad y dispositivos virtuales. En este documento se proporciona una visión general de los problemas de seguridad y de arquitectura que los clientes deben tener en cuenta al usar Servicios en la nube de Microsoft con acceso a través de ExpressRoute. También se describe la creación de servicios más seguros en redes virtuales de Azure.

## <a name="fast-start"></a>Inicio rápido
Hola siguiendo el gráfico de lógica puede dirigir tooa ejemplo concreto acerca de hello muchas técnicas de seguridad disponibles con hello plataforma Windows Azure. Referencia rápida encontrar ejemplo de Hola que mejor se adapte a su caso. Para obtener una explicación ampliada, seguir leyendo a través de papel de Hola.
[![0]][0]

[Ejemplo 1: Crear una red perimetral (también conocida como DMZ, zona desmilitarizada o subred filtrada) toohelp proteger las aplicaciones con grupos de seguridad de red (NSG).](#example-1-build-a-perimeter-network-to-help-protect-applications-with-nsgs)</br>
[Ejemplo 2: Crear un perímetro de red toohelp proteger las aplicaciones con un firewall y los NSG.](#example-2-build-a-perimeter-network-to-help-protect-applications-with-a-firewall-and-nsgs)</br>
[Ejemplo 3: Crear un perímetro de red toohelp proteger las redes con un firewall, la ruta definida por el usuario (UDR) y el NSG.](#example-3-build-a-perimeter-network-to-help-protect-networks-with-a-firewall-and-udr-and-nsg)</br>
[Ejemplo 4: Incorporación de una conexión híbrida con una red privada virtual (VPN) de dispositivo virtual de sitio a sitio.](#example-4-add-a-hybrid-connection-with-a-site-to-site-virtual-appliance-vpn)</br>
[Ejemplo 5: Incorporación de una conexión híbrida con una instancia de Azure VPN Gateway de sitio a sitio.](#example-5-add-a-hybrid-connection-with-a-site-to-site-azure-vpn-gateway)</br>
[Ejemplo 6: Incorporación de una conexión híbrida con ExpressRoute.](#example-6-add-a-hybrid-connection-with-expressroute)</br>
Ejemplos para agregar conexiones entre redes virtuales, la alta disponibilidad y el encadenamiento de servicios se agregarán toothis documento sobre Hola próximos meses.

## <a name="microsoft-compliance-and-infrastructure-protection"></a>Protección de infraestructura y cumplimiento normativo de Microsoft
las organizaciones toohelp cumplen nacionales, regionales, y los requisitos específicos del sector que rigen Hola recopilación y uso de datos de personas, Microsoft ofrece más de 40 certificaciones y certificados. Hola más completo conjunto de cualquier proveedor de servicios de nube.

Para obtener más información, consulte la información de compatibilidad de hello en hello [Microsoft Trust Center][TrustCenter].

Microsoft tiene un enfoque integral tooprotect infraestructura necesaria toorun hiperescala global servicios en la nube. Infraestructura de nube de Microsoft incluye hardware, software, redes y administrativos y personal de operaciones, además de centros de datos físico toohello.

![2]

Este enfoque proporciona una base más segura para los clientes toodeploy sus servicios en la nube de Microsoft Hola. paso siguiente Hello es para los clientes toodesign y crear un tooprotect de arquitectura de seguridad de estos servicios.

## <a name="traditional-security-architectures-and-perimeter-networks"></a>Arquitecturas de seguridad tradicionales y redes perimetrales
Aunque Microsoft invierte considerablemente en la protección de la infraestructura de nube de hello, los clientes también deben proteger sus servicios en la nube y los grupos de recursos. Un enfoque multicapa toosecurity proporciona mejor defensa de Hola. Una zona de seguridad de red perimetral protege los recursos de red internos de una red que no sea de confianza. Una red perimetral refiere toohello bordes o partes de la red de Hola que se colocan entre Internet Hola y Hola protegido enterprise infraestructura de TI.

En redes de empresa típica, infraestructura básica de Hola se enriquece mucho en los perímetros de hello, con varios niveles de dispositivos de seguridad. límite de Hola de cada capa consta de los dispositivos y los puntos de cumplimiento de directiva. Cada capa puede incluir una combinación de hello después de dispositivos de seguridad de red: firewalls, prevención de denegación de servicio (DoS), la detección de intrusiones o sistemas de protección (identificadores/IP) y los dispositivos VPN. Aplicación de directivas puede adoptar la forma de Hola de las directivas de firewall, listas de control de acceso (ACL) o el enrutamiento. Hola primera línea de defensa en red hello, aceptando directamente el tráfico entrante desde Internet, hello es una combinación de estos mecanismos tooblock ataques y tráfico dañino permitiendo solicitudes legítimas aún más en la red de Hola. Este tráfico enruta directamente tooresources en la red perimetral de Hola. Ese recurso puede, a continuación, "hablar" tooresources un poco más en red hello, tránsito siguiente límite de hello para la validación del primero. capa exterior Hola se denomina red perimetral de hello porque esta parte de la red de hello está expuesto toohello Internet, normalmente con alguna forma de protección en ambos lados. Hello en la ilustración siguiente se muestra un ejemplo de una red de perímetro de una única subred en una red corporativa, con dos de los límites de seguridad.

![3]

Hay muchas tooimplement arquitecturas utiliza una red perimetral. Estas arquitecturas pueden oscilar entre una red de perímetro de varias subredes de tooa de equilibrador de carga simple con diversos mecanismos en el tráfico de tooblock de cada límite y proteger capas más profundas de hello de la red corporativa de Hola. Cómo se crea la red perimetral de hello depende de necesidades específicas de Hola de organización de Hola y su tolerancia al riesgo general.

Como los clientes mueven sus nubes de toopublic de las cargas de trabajo, es crítico toosupport capacidades similares para arquitectura de la red perimetral en Azure toomeet cumplimiento y los requisitos de seguridad. En este documento se proporcionan instrucciones sobre cómo pueden crear los clientes un entorno de red seguro en Azure. Se centra en la red perimetral de hello, pero también incluye una explicación completa de muchos aspectos de seguridad de red. Hola después preguntas informan a este tema:

* ¿Cómo se puede crear una red perimetral en Azure?
* ¿Cuáles son algunas de la red perimetral de hello características de Azure disponibles toobuild Hola?
* ¿Cómo se pueden proteger las cargas de trabajo back-end?
* ¿Cómo son cargas de trabajo del toohello de controla las comunicaciones de Internet en Azure?
* ¿Cómo se pueden proteger redes locales de Hola de implementaciones en Azure?
* ¿Cuándo se deben usar las características de seguridad de Azure nativas frente a dispositivos o servicios de terceros?

Hola siguiente diagrama muestra los diferentes niveles de seguridad de que Azure proporciona toocustomers. Estos niveles son los modos nativo en hello plataforma Windows Azure propio y funciones definidas por el cliente:

![4]

Entrada de hello Internet, DDoS Azure ayuda a protegerse contra ataques a gran escala en Azure. Hola siguiente nivel es definido por el cliente direcciones IP públicas (extremos), que son utilizado toodetermine qué tráfico puede pasar a través de la red virtual de hello en la nube servicio toohello. El aislamiento de la red virtual de Azure nativa garantiza un aislamiento completo de todas las demás redes y que el tráfico solo fluya a través de los métodos y las rutas de acceso configurados por el usuario. Estas rutas de acceso y los métodos son capa siguiente de hello, donde los NSG, UDR y dispositivos de red virtual pueden ser usado toocreate seguridad límites tooprotect hello las implementaciones de aplicaciones en red Hola protegido.

Hola siguiente sección proporciona una visión general de redes virtuales de Azure. Los clientes crean estas redes virtuales, que son a las que están conectadas las cargas de trabajo implementadas. Las redes virtuales son Hola base de todas las características de seguridad de red de Hola que requieren tooestablish un perímetro de la red tooprotect de implementaciones de clientes en Azure.

## <a name="overview-of-azure-virtual-networks"></a>Información general sobre las redes virtuales de Azure
Antes de que el tráfico de Internet pueda obtener toohello redes virtuales de Azure, hay dos niveles de seguridad inherentes toohello plataforma Windows Azure:

1.    **Protección frente a DDoS**: protección frente a DDoS es una capa de hello Azure red físico que protege Hola plataforma Windows Azure propio frente a ataques basados en Internet a gran escala. Estos ataques usar varios nodos de "bot" en un toooverwhelm de intento de un servicio en Internet. Azure cuenta con una malla de protección frente a DDoS sólida en toda la conectividad de entrada, salida y entre regiones de Azure. Este nivel de protección DDoS no tiene ningún usuario puede configurar atributos y no es accesible toohello cliente. nivel de protección DDoS Hola protege Azure como una plataforma de ataques a gran escala, también supervisa tráfico región entre Azure y out-enlazado. Con dispositivos de red virtual en la red virtual de hello, capas adicionales de resistencia pueden configurarse por el cliente de hello contra un ataque de escala más pequeño que no viaje protección a nivel de plataforma Hola. Un ejemplo de DDoS en acción; Si una dirección IP con orientación de internet se atacadas por un ataque DDoS a gran escala, Azure podría detectar orígenes Hola de ataques de Hola y omitir Hola infractora tráfico antes de alcanzar el destino pretendido. En casi todos casos, hello atacada de punto de conexión no se ve afectado por ataques de Hola. En hello pocos casos en que un punto de conexión se ve afectado, ningún tipo de tráfico es tooother afectados los puntos de conexión, solo Hola atacada extremo. Por lo tanto, otros clientes y servicios no sufrirían impacto alguno de este ataque. Es fundamental toonote que Azure DDoS solo busca ataques a gran escala. Es posible que el servicio específico podría verse desbordo antes de que se superen los umbrales de protección a nivel de plataforma de Hola. Por ejemplo, un ataque de DDoS podría desconectar un sitio web de un solo servidor IIS A0 antes de que la protección frente a DDoS de nivel de plataforma de Azure registrara una amenaza.

2.  **Las direcciones IP públicas**: dirección IP pública direcciones (habilitadas a través de extremos de servicio, direcciones IP públicas, puerta de enlace de aplicaciones y otras características de Azure que presentan un recurso de tooyour internet enrutados público del toohello de dirección IP) permitan servicios en la nube o los grupos de recursos toohave las direcciones IP de Internet públicas y puertos expuestos. punto de conexión de Hello usa dirección interna de traducción de direcciones de red (NAT) tooroute tráfico toohello y el puerto en hello red virtual de Azure. Esta ruta de acceso es la forma principal de hello toopass tráfico externo en la red virtual de Hola. direcciones IP públicas de Hello son configurable toodetermine qué tráfico se pasa en, y cómo y dónde se traduce en toohello de red virtual.

Una vez que llega a tráfico de red virtual de Hola, hay muchas características que entran en juego. Redes virtuales de Azure se Hola base para los clientes tooattach sus cargas de trabajo y donde se aplica la seguridad de nivel de red básica. Es una red privada (una superposición de red virtual) en Azure para clientes con hello después de funciones y características:

* **Aislamiento del tráfico**: una red virtual es el límite de aislamiento de tráfico de hello en hello plataforma Windows Azure. Máquinas virtuales (VM) en una red virtual no se puede comunicar directamente tooVMs en una red virtual diferente, incluso si ambas redes virtuales se crean por Hola a mismo cliente. El aislamiento consiste en una propiedad fundamental que garantiza que las máquinas virtuales del cliente y la comunicación sigan siendo privadas en una red virtual.

>[!NOTE]
>El aislamiento del tráfico refiere solo tootraffic *entrada* toohello de red virtual. Por el tráfico saliente predeterminado de toohello de red virtual de hello internet está permitido, pero puede evitarse si lo desea mediante NSG.
>
>

* **Topología de niveles múltiples**: redes virtuales permiten a los clientes topología de niveles múltiples de toodefine asignar subredes y la designación de espacios de direcciones independientes para los distintos elementos o "capas" de sus cargas de trabajo. Estas agrupaciones lógicas y topologías habilitar Directiva de acceso diferente de toodefine de los clientes basada en tipos de cargas de trabajo de Hola y controlan los flujos de tráfico entre las capas de Hola.
* **Conectividad entre instalaciones locales**: los clientes pueden establecer conectividad entre instalaciones locales entre una red virtual y varios sitios locales u otras redes virtuales en Azure. tooconstruct una conexión, los clientes pueden usar intercambio de tráfico de red virtual, las puertas de enlace VPN de Azure, aparatos virtuales de red de terceros o ExpressRoute. Azure es compatible con VPN de sitio a sitio (S2S) mediante los protocolos estándar IPsec/IKE y conectividad privada de ExpressRoute.
* **NSG** permite a los clientes toocreate reglas (ACL) en el nivel de hello deseado de granularidad: subredes virtuales, máquinas virtuales individuales o interfaces de red. Los clientes pueden controlar el acceso permitir o denegar la comunicación entre las cargas de trabajo de hello en una red virtual, de los sistemas de redes del cliente a través de la conectividad entre entornos, o dirigir la comunicación de Internet.
* **UDR** y **el reenvío IP** permiten a los clientes vías de comunicación de hello toodefine entre los diferentes niveles en una red virtual. Los clientes pueden implementar un firewall, IDS/IPS y otros dispositivos virtuales y enrutar el tráfico de red a través de estos dispositivos de seguridad para la aplicación de directivas de límites de seguridad, auditoría e inspección.
* **Red aparatos virtuales** en hello Azure Marketplace: dispositivos de seguridad, como firewalls y equilibradores de carga, identificadores y direcciones IP están disponibles en Azure Marketplace de Hola y Hola Galería de imágenes de máquina virtual. Los clientes pueden implementar estas aplicaciones en sus redes virtuales y, específicamente, en su entorno de red seguro de seguridad límites (incluidas las subredes de la red perimetral hello) toocomplete un valor de varios niveles.

Con estas características y capacidades, un ejemplo de cómo podría crearse una arquitectura de la red perimetral en Azure es hello siguiente diagrama:

![5]

## <a name="perimeter-network-characteristics-and-requirements"></a>Características y requisitos de una red perimetral
red perimetral de Hello es Hola front-end de red de hello, interactúa directamente la comunicación de hello Internet. paquetes de saludo entrante deben fluyen a través de los dispositivos de seguridad de hello, como firewall de hello, identificadores y direcciones IP, antes de llegar a los servidores back-end de Hola. Paquetes de vinculado a Internet de las cargas de trabajo de hello también puedan fluir a través de dispositivos de seguridad de hello en la red perimetral de hello para la aplicación de directivas, inspección y auditoría fines, antes de abandonar la red Hola. Además, la red perimetral de Hola puede hospedar las puertas de enlace VPN entre entornos entre redes virtuales del cliente y redes locales.

### <a name="perimeter-network-characteristics"></a>Características de una red perimetral
Hace referencia a la ilustración anterior hello, algunas de las características de Hola de una red perimetral buena son las siguientes:

* Accesible desde Internet:
  * subred de red perimetral de Hello propio tiene conexión a Internet, comunicarse directamente con hello Internet.
  * Las direcciones IP públicas, VIP o extremos de servicio pasan dispositivos y la red front-end de toohello de tráfico de Internet.
  * El tráfico entrante desde Hola que Internet pasa a través de dispositivos de seguridad antes de otros recursos de red front-end de Hola.
  * Si está habilitada la seguridad de salida, el tráfico pasa a través de dispositivos de seguridad, como paso final de hello, antes de pasar toohello Internet.
* Red protegida:
  * No hay ninguna ruta de acceso directo de la infraestructura básica de hello Internet toohello.
  * Infraestructura básica de canales toohello debe recorrer a través de dispositivos de seguridad, como los NSG, firewalls o dispositivos VPN.
  * Otros dispositivos no deben cubrir la infraestructura básica de hello y de Internet.
  * Dispositivos de seguridad en ambas Hola orientado a Internet y red protegida Hola orientada hacia los límites de la red perimetral de hello (por ejemplo, hello dos firewall iconos que aparecen en la ilustración anterior hello) puede ser realmente un único dispositivo virtual con reglas diferenciados o interfaces para cada límite. Por ejemplo, un dispositivo físico, separado lógicamente, control de carga de Hola para los límites de la red perimetral de Hola.
* Otras prácticas y restricciones comunes:
  * Las cargas de trabajo no deben almacenar información crítica de la empresa.
  * Las implementaciones y las configuraciones de red de tooperimeter de acceso y las actualizaciones son administradores de tooonly limitado autorizado.

### <a name="perimeter-network-requirements"></a>Requisitos de red perimetral
tooenable estas características, siga estas instrucciones en tooimplement de requisitos de red virtual una red perimetral correcta:

* **Arquitectura de subred:** especificar Hola virtual red, que se dedica una subred completa como red de perímetro de hello, separadas de otras subredes Hola mismo red virtual. Esta separación garantiza tráfico Hola entre la red perimetral de Hola y otros flujos de niveles de subred interna o privada a través de un firewall o un dispositivo virtual de identificadores y direcciones IP.  Las rutas definidas por el usuario en límite de hello subredes son necesarios tooforward este dispositivo virtual de tráfico toohello.
* **NSG:** subred de red perimetral de hello propio deberían tooallow abierto de comunicación con hello Internet, pero que no significa que los clientes deben omitir los NSG. Siga comunes seguridad prácticas toominimize Hola red superficies expuestas toohello Internet. Bloquear intervalos de direcciones remotas de hello permitida implementaciones de hello tooaccess o protocolos de aplicación específica de Hola y puertos que están abiertos. Sin embargo, es posible que se den circunstancias en las que no sea posible realizar un bloqueo completo. Por ejemplo, si los clientes tienen un sitio Web externo en Azure, red perimetral de hello debe permitir las solicitudes web de Hola entrantes desde cualquier dirección IP pública, pero sólo se debe abrir los puertos de la aplicación web hello: TCP en el puerto 80 o TCP en el puerto 443.
* **Tabla de enrutamiento:** subred de red perimetral de hello propio debe ser capaz de toocommunicate toohello Internet directamente, pero no se debe permitir la comunicación directa tooand de back-end o local redes de hello sin pasar por un firewall o dispositivo de seguridad.
* **Configuración de dispositivo de seguridad:** tooroute e inspeccionar paquetes entre la red perimetral de Hola y el resto de Hola de redes de hello protegido, Hola dispositivos de seguridad como firewall, identificadores, y dispositivos de direcciones IP pueden ser de host múltiple. Pueden tener una NIC independiente para la red perimetral de Hola y subredes de back-end de Hola. Hola NIC de red perimetral de hello comunican directamente tooand de hello Internet, con hello NSG correspondientes y el perímetro de hello tabla de enrutamiento de red. NIC de Hola la conexión de subredes de back-end de toohello tienen más restringidos NSG y tablas de enrutamiento de subredes de back-end de hello correspondiente.
* **Funciones del dispositivo de seguridad:** dispositivos de seguridad de hello implementados en la red perimetral de hello suele realizan Hola siguiente funcionalidad:
  * Firewall: Imponer las reglas de firewall y directivas de control de acceso para las solicitudes entrantes de Hola.
  * Detección y prevención de amenazas: detectar y mitigar los ataques malintencionados de hello Internet.
  * Auditoría y registro: mantener registros detallados para auditoría y análisis.
  * Proxy inverso: Hola entrantes de redirigir las solicitudes toohello correspondientes servidores de back-end. Esta redirección implica la asignación y traducción de direcciones de destino de hello en los dispositivos de front-end de hello, normalmente los firewalls, direcciones de servidor back-end de toohello.
  * Proxy de reenvío: proporcionar NAT y realizar la auditoría para la comunicación que se inicializan desde la red virtual de hello toohello Internet.
  * Enrutador: Reenviar el tráfico entrante y entre subredes dentro de la red virtual de Hola.
  * Dispositivo VPN: actúa como Hola entre entornos puertas de enlace VPN para la conectividad entre entornos VPN entre redes de cliente locales y redes virtuales de Azure.
  * Servidor VPN: Aceptar clientes VPN que se conectan tooAzure las redes virtuales.

> [!TIP]
> Mantener Hola después independiente de dos grupos: usuarios de hello tooaccess Hola perimetral red seguridad hello y engranaje las personas autorización autorizados como administradores de desarrollo, implementación o las operaciones de la aplicación. Mantener estos grupos separados permite una separación de funciones y evita que una sola persona omita la seguridad de las aplicaciones y los controles de seguridad de red.
>
>

### <a name="questions-toobe-asked-when-building-network-boundaries"></a>Toobe de preguntas más frecuentes al compilar los límites de red
En esta sección, a menos que se menciona específicamente, Hola término "redes" hace referencia tooprivate Azure redes virtuales creadas por un administrador de la suscripción. término de Hello no hace referencia a redes físicas subyacentes de toohello dentro de Azure.

Además, redes virtuales de Azure son a menudo tooextend usa las redes locales tradicionales. Es posible tooincorporate sitio a sitio o híbrida ExpressRoute soluciones con arquitecturas de red perimetral de red. Este vínculo híbrido es una consideración importante a la hora de crear límites de seguridad de red.

Hello siguientes tres preguntas son tooanswer crítico cuando se crea una red con una red perimetral y varios de los límites de seguridad.

#### <a name="1-how-many-boundaries-are-needed"></a>1) ¿Cuántos límites se necesitan?
primer punto de decisión de Hello es toodecide cuántos de los límites de seguridad son necesarios en un escenario que nos ocupa:

* Un solo límite: uno en la red perimetral front-end de hello, entre la red virtual de Hola y Hola Internet.
* Los límites de dos: uno en el lado de Internet de la red perimetral de Hola Hola y otro entre la subred de la red perimetral hello y subredes de back-end de hello en Hola redes virtuales de Azure.
* Tres límites: uno en hello Internet lado de la red perimetral de hello, uno entre la red perimetral de Hola y subredes de back-end y otro entre subredes de back-end de Hola y red local de Hola.
* N límites: un número variable. Dependiendo de los requisitos de seguridad, no hay ningún toohello limitar el número de límites de seguridad que se pueden aplicar en una red determinada.

Hello número y tipo de los límites necesarios varían depende riesgo hello y tolerancia escenario específico de una empresa que se están implementando. Esta decisión suelen tomarla conjuntamente varios grupos de una organización, que a menudo incluye un equipo de riesgos y cumplimiento, un equipo de redes y plataformas, y un equipo de desarrollo de aplicaciones. Deben tener las personas con conocimientos de seguridad, datos de hello implicados y tecnologías de Hola que se va a usar un ejemplo en esta postura de seguridad adecuadas de decisión tooensure Hola para cada implementación.

> [!TIP]
> Usar Hola un número más pequeño de los límites que cumplen los requisitos de seguridad de Hola para una situación determinada. Con más de los límites, operaciones y solución de problemas pueden resultar más difícil, así como Hola administración sobrecarga que implica a la administración de hello varias directivas de límite con el tiempo. Sin embargo, unos límites insuficientes aumentan el riesgo. Saldo de Hola de búsqueda es crítica.
>
>

![6]

Hello en la ilustración anterior se muestra una vista de alto nivel de una red de límite de seguridad de tres. límites de Hola se encuentran entre la red perimetral de Hola y Hola Internet, hello Azure front-end y subredes privadas de back-end y Hola subred de back-end de Azure y red corporativa de hello en local.

#### <a name="2-where-are-hello-boundaries-located"></a>¿2), donde se encuentran los límites de hello?
Una vez que se decide número Hola de límites, donde tooimplement ellos es Hola siguiente punto de decisión. Generalmente, hay tres opciones:

* Uso de un servicio intermedio basado en Internet (por ejemplo, un firewall de aplicaciones web basado en la nube, que no se trata en este documento).
* Uso de características nativas o dispositivos virtuales de red en Azure.
* Uso de dispositivos físicos en la red local de Hola

Puramente redes de Azure, opciones de hello son características nativas de Azure (por ejemplo, los equilibradores de carga de Azure) o dispositivos de red virtual de Hola ecosistema de partners enriquecido de Azure (por ejemplo, los servidores de seguridad de punto de comprobación).

Si se necesita un límite entre Azure y una red local, dispositivos de seguridad de hello pueden residir en cualquier lado de conexión de hello (o ambos). Por lo tanto, una decisión debe realizarse en el equipo de seguridad de hello ubicación tooplace.

En la ilustración anterior hello, red de perímetro de Internet de Hola y límites de hello frente a back-end están incluidos completamente en Azure y deben ser características nativas de Azure o dispositivos de red virtual. Dispositivos de seguridad en Hola límite entre Azure (subred back-end) y podría ser la red corporativa de hello en hello parte de Azure o lado local de hello o incluso una combinación de dispositivos en ambos lados. Puede haber ventajas significativas y opción de tooeither desventajas que debe considerarse en serio.

Por ejemplo, usando el equipo de seguridad física existente en hello local de lado de la red tiene ventaja de Hola que no se necesita ningún icono de engranaje nuevo. Simplemente hay que volver a configurarlo. desventaja de Hello, sin embargo, es que todo el tráfico debe vuelva desde Azure toohello local red toobe visto por engranaje de seguridad de Hola. Tráfico de Azure en Azure, por tanto, podría producir una latencia elevada y afecta a la experiencia de usuario y de rendimiento de la aplicación, si se fuerza el back-toohello de red local para la aplicación de directiva de seguridad.

#### <a name="3-how-are-hello-boundaries-implemented"></a>¿(3) cómo se implementan los límites de hello?
Cada límite de seguridad probablemente tendrá requisitos de las funcionalidades diferentes (por ejemplo, identificadores y las reglas de firewall Hola lado de Internet de la red perimetral de hello, pero solo las ACL entre la red perimetral de Hola y subred back-end). Decidir qué dispositivo (o cuántos dispositivos) depende de toouse Hola requisitos de escenario y seguridad. En Hola pasos de la sección ejemplos 1, 2 y 3 describen algunas opciones que se pudieron utilizar. Revisión de las características de Azure red nativo de Hola y dispositivos Hola disponibles en Azure desde el ecosistema de partners de hello muestra hello gran número de opciones disponibles toosolve prácticamente cualquier escenario.

Otro punto de decisión de implementación de clave es cómo tooconnect Hola local red con Azure. ¿Debería utilizar hello Azure puerta de enlace virtual o un dispositivo virtual de red? Estas opciones se describen con más detalle en hello pasos de la sección (ejemplos 4, 5 y 6).

Además, podría ser necesario el tráfico entre redes virtuales dentro de Azure. Estos escenarios se agregarán en hello futuras.

Una vez que sepa respuestas hello toohello anterior preguntas, Hola [Fast Start](#fast-start) sección puede ayudarle a identificar qué ejemplos son más adecuadas para un escenario determinado.

## <a name="examples-building-security-boundaries-with-azure-virtual-networks"></a>Ejemplos: Creación de límites de seguridad con redes virtuales de Azure
### <a name="example-1-build-a-perimeter-network-toohelp-protect-applications-with-nsgs"></a>Ejemplo 1 compilación un toohelp de red perimetral proteger las aplicaciones con los NSG
[Hacer copia de inicio de tooFast](#fast-start) | [Detailed compilar las instrucciones de este ejemplo][Example1]

[![7]][7]

#### <a name="environment-description"></a>Descripción del entorno
En este ejemplo, hay una suscripción que contiene Hola recursos siguientes:

- Un único grupo de recursos
- Una red virtual solo en la nube con dos subredes: "FrontEnd" y "BackEnd"
- Un grupo de seguridad de red que está aplicada tooboth subredes
- Un servidor Windows que representa un servidor de aplicaciones web ("IIS01")
- Dos servidores Windows que representan servidores back-end de aplicaciones ("AppVM01", "AppVM02")
- Un servidor Windows que representa un servidor DNS ("DNS01")
- Una IP pública asociada con el servidor de web de aplicación Hola

Para las secuencias de comandos y una plantilla de Azure Resource Manager, vea hello [instrucciones de compilación][Example1].

#### <a name="nsg-description"></a>Descripción del grupo de seguridad de red
En este ejemplo, se crea un grupo de seguridad de red y se cargan después seis reglas.

> [!TIP]
> Por lo general, debe crear las reglas de "Permitir" específicas en primer lugar, seguida de hello más genérico "Denegar" las reglas. Hola prioridad determina qué reglas se evalúan primero. Una vez que el tráfico se encuentra la regla específica de tooapply tooa, no se evalúa ninguna otra regla. Se pueden aplicar reglas NSG en cualquiera Hola dirección entrante o saliente (desde la perspectiva de Hola de subred de hello).
>
>

Mediante declaración, se regeneran Hola siguiendo las reglas para el tráfico entrante:

1. Se permite el tráfico DNS interno (puerto 53).
2. Se permite el tráfico RDP (puerto 3389) de hello Internet tooany Máquina Virtual.
3. Se permite el tráfico HTTP (puerto 80) del servidor de hello Internet tooweb (IIS01).
4. Se permite cualquier tráfico (todos los puertos) del IIS01 tooAppVM1.
5. Se deniega todo (todos los puertos) el tráfico desde Hola Internet toohello toda la red virtual (tanto en las subredes).
6. Se deniega todo (todos los puertos) el tráfico de subred de back-end de toohello Hola subred front-end.

Con estas subredes de enlazado tooeach reglas, si una solicitud HTTP es entrante desde el servidor web de hello Internet toohello, ambas reglas 3 (permitir) y 5 (denegar) se aplicará. Sin embargo, dado que la regla 3 tiene una prioridad más alta, solo se aplicaría esta, y la regla 5 no entraría en juego. Por lo tanto solicitud HTTP de hello podría permitirse a toohello servidor de web. Si ese mismo tráfico tratara de servidor de hello DNS01 tooreach, regla 5 (denegar) sería Hola tooapply primera y tráfico de hello no estarían permitido toopass toohello server. Regla 6 (denegar) bloques Hola subred front-end de hablar de subred de back-end de toohello (excepto el tráfico permitido en las reglas 1 y 4). Este conjunto de reglas protege la red de back-end de hello en caso de que un atacante pone en peligro la aplicación web de hello en front-end de Hola. el atacante de Hola habría limitado acceso toohello back-end "protegido" red (solo tooresources expuesta en el servidor de hello AppVM01).

Hay una regla de salida predeterminada que permite el tráfico de salida toohello Internet. En este ejemplo, permitimos el tráfico saliente y no modificamos las reglas de salida. toolock hacia abajo el tráfico en ambas direcciones, enrutamiento definido por el usuario es necesario (vea el ejemplo 3).

#### <a name="conclusion"></a>Conclusión
En este ejemplo es una forma relativamente sencilla y directa de aislar la subred de back-end de Hola de tráfico entrante. Para obtener más información, vea hello [instrucciones de compilación][Example1]. Estas instrucciones incluyen lo siguiente:

* ¿Cómo toobuild este perímetro de la red con secuencias de comandos de PowerShell clásicos.
* ¿Cómo toobuild este perímetro de la red con una plantilla de Azure Resource Manager.
* Descripciones detalladas de cada comando de grupo de seguridad de red.
* Escenarios de flujo de tráfico detallados, que muestran cómo se permite o se deniega el tráfico en cada nivel.


### <a name="example-2-build-a-perimeter-network-toohelp-protect-applications-with-a-firewall-and-nsgs"></a>Ejemplo 2 compilación un toohelp de red perimetral proteger las aplicaciones con un firewall y los NSG
[Hacer copia de inicio de tooFast](#fast-start) | [Detailed compilar las instrucciones de este ejemplo][Example2]

[![8]][8]

#### <a name="environment-description"></a>Descripción del entorno
En este ejemplo, hay una suscripción que contiene Hola recursos siguientes:

* Un único grupo de recursos
* Una red virtual solo en la nube con dos subredes: "FrontEnd" y "BackEnd"
* Un grupo de seguridad de red que está aplicada tooboth subredes
* Un dispositivo de red virtual, en este caso un firewall, conectado subred front-end toohello
* Un servidor Windows que representa un servidor de aplicaciones web ("IIS01")
* Dos servidores Windows que representan servidores back-end de aplicaciones ("AppVM01", "AppVM02")
* Un servidor Windows que representa un servidor DNS ("DNS01")

Para las secuencias de comandos y una plantilla de Azure Resource Manager, vea hello [instrucciones de compilación][Example2].

#### <a name="nsg-description"></a>Descripción del grupo de seguridad de red
En este ejemplo, se crea un grupo de seguridad de red y se cargan después seis reglas.

> [!TIP]
> Por lo general, debe crear las reglas de "Permitir" específicas en primer lugar, seguida de hello más genérico "Denegar" las reglas. Hola prioridad determina qué reglas se evalúan primero. Una vez que el tráfico se encuentra la regla específica de tooapply tooa, no se evalúa ninguna otra regla. Se pueden aplicar reglas NSG en cualquiera Hola dirección entrante o saliente (desde la perspectiva de Hola de subred de hello).
>
>

Mediante declaración, se regeneran Hola siguiendo las reglas para el tráfico entrante:

1. Se permite el tráfico DNS interno (puerto 53).
2. Se permite el tráfico RDP (puerto 3389) de hello Internet tooany Máquina Virtual.
3. Se permite cualquier tráfico (todos los puertos) toohello red virtual dispositivo Internet (firewall).
4. Se permite cualquier tráfico (todos los puertos) del IIS01 tooAppVM1.
5. Se deniega todo (todos los puertos) el tráfico desde Hola Internet toohello toda la red virtual (tanto en las subredes).
6. Se deniega todo (todos los puertos) el tráfico de subred de back-end de toohello Hola subred front-end.

Con estas subredes de enlazado tooeach reglas, si una solicitud HTTP ha entrado Firewall toohello conectado Internet hello, ambas reglas 3 (permitir) y 5 (denegar) se aplicará. Sin embargo, dado que la regla 3 tiene una prioridad más alta, solo se aplicaría esta, y la regla 5 no entraría en juego. Por lo tanto solicitud Hola HTTP podría permitirse toohello firewall. Si ese mismo tráfico tratara de servidor de hello IIS01 tooreach, aunque se encuentre en la subred de front-end de hello, regla 5 aplicaría (denegar), y el tráfico de hello no estarían permitido toopass toohello server. Regla 6 (denegar) bloques Hola subred front-end de hablar de subred de back-end de toohello (excepto el tráfico permitido en las reglas 1 y 4). Este conjunto de reglas protege la red de back-end de hello en caso de que un atacante pone en peligro la aplicación web de hello en front-end de Hola. el atacante de Hola habría limitado acceso toohello back-end "protegido" red (solo tooresources expuesta en el servidor de hello AppVM01).

Hay una regla de salida predeterminada que permite el tráfico de salida toohello Internet. En este ejemplo, permitimos el tráfico saliente y no modificamos las reglas de salida. toolock hacia abajo el tráfico en ambas direcciones, enrutamiento definido por el usuario es necesario (vea el ejemplo 3).

#### <a name="firewall-rule-description"></a>Descripción de reglas de firewall
En el firewall de hello, se deben crear las reglas de reenvío. Dado que este ejemplo sólo las rutas de tráfico de Internet de entrada toohello servidor de seguridad y, a continuación, toohello web, solo uno de reenvío de red (NAT) de traducción de direcciones se necesita la regla.

regla de reenvío de Hello acepta cualquier dirección de origen de entrada que visita firewall Hola intentar tooreach HTTP (puerto 80 o 443 para HTTPS). Tiene envían fuera de la interfaz local del servidor de seguridad de Hola y redirigido toohello web server con la dirección IP de 10.0.1.5 Hola.

#### <a name="conclusion"></a>Conclusión
En este ejemplo es una forma relativamente sencilla de protección de su aplicación con un firewall y el aislamiento de la subred de back-end de Hola de tráfico entrante. Para obtener más información, vea hello [instrucciones de compilación][Example2]. Estas instrucciones incluyen lo siguiente:

* ¿Cómo toobuild este perímetro de la red con secuencias de comandos de PowerShell clásicos.
* ¿Cómo toobuild este ejemplo con una plantilla de Azure Resource Manager.
* Descripciones detalladas de cada comando de grupo de seguridad de red y regla de firewall.
* Escenarios de flujo de tráfico detallados, que muestran cómo se permite o se deniega el tráfico en cada nivel.

### <a name="example-3-build-a-perimeter-network-toohelp-protect-networks-with-a-firewall-and-udr-and-nsg"></a>Compilación de ejemplo 3 un toohelp de red perimetral proteger las redes con un firewall y UDR y NSG
[Hacer copia de inicio de tooFast](#fast-start) | [Detailed compilar las instrucciones de este ejemplo][Example3]

[![9]][9]

#### <a name="environment-description"></a>Descripción del entorno
En este ejemplo, hay una suscripción que contiene Hola recursos siguientes:

* Un único grupo de recursos
* Una red virtual con tres subredes: "SecNet", "FrontEnd" y "BackEnd"
* Un dispositivo de red virtual, en este caso un firewall, conectado toohello SecNet subred
* Un servidor Windows que representa un servidor de aplicaciones web ("IIS01")
* Dos servidores Windows que representan servidores back-end de aplicaciones ("AppVM01", "AppVM02")
* Un servidor Windows que representa un servidor DNS ("DNS01")

Para las secuencias de comandos y una plantilla de Azure Resource Manager, vea hello [instrucciones de compilación][Example3].

#### <a name="udr-description"></a>Descripción de UDR
De forma predeterminada, Hola siguiendo las rutas del sistema se define como:

        Effective routes :
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

Hola VNETLocal siempre es uno o más prefijos de dirección definida que componen la red virtual de Hola para esa red específica (es decir, cambia de red de toovirtual de red virtual, según cómo se defina cada red virtual específica). rutas de sistema de Hello restantes son estáticas y predeterminado según se indica en la tabla de Hola.

En este ejemplo, se crean dos tablas de enrutamiento, uno para las subredes de front-end y back-end de Hola. Cada tabla se carga con rutas estáticas adecuadas para hello dada la subred. En este ejemplo, cada tabla tiene tres rutas que dirigir todo el tráfico (0.0.0.0/0) a través de firewall de hello (del próximo salto = la dirección IP de dispositivo Virtual):

1. El tráfico de subred local con ningún próximo salto define tooallow subred local tráfico toobypass Hola firewall.
2. Tráfico de red virtual con un próximo salto definido como el firewall. Esta siguiente salto invalidaciones Hola regla predeterminada que permite tooroute de tráfico de red virtual local directamente.
3. Tráfico todas las restante (0/0) con un próximo salto se define como Hola firewall.

> [!TIP]
> No disponer de entrada de la subred local de hello en hello las comunicaciones de UDR saltos subred local.
>
> * ¡En nuestro ejemplo, es fundamental 10.0.1.0/24 que señala tooVNETLocal! Sin él, se producirá un error de paquete dejando servidor local de servidor Web (10.0.1.4) destinados a tooanother de hello 10.0.1.25 (por ejemplo) tal y como se enviarán toohello NVA. Hola NVA lo enviará subred toohello y subred Hola se volverá a enviar, toohello NVA en un bucle infinito.
> * las posibilidades de Hola de un bucle de enrutamiento son normalmente más altos en dispositivos con varias NIC que están conectados tooseparate subredes, que suele ser de dispositivos locales tradicionales.
>
>

Una vez que se crean tablas de enrutamiento de hello, deben ser subredes tootheir enlazado. Hola subred front-end de tabla de enrutamiento, una vez creada y enlazado toohello subred, sería este resultado:

        Effective routes :
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active

> [!NOTE]
> UDR ahora pueden subred de puerta de enlace de toohello aplicado qué hello ExpressRoute está conectado el circuito.
>
> En los ejemplos 3 y 4 se muestran ejemplos de cómo tooenable el perímetro de una red con ExpressRoute o conexión de red de sitio a sitio.
>
>

#### <a name="ip-forwarding-description"></a>Descripción de reenvío IP
El reenvío IP es un tooUDR de característica complementaria. El reenvío IP es una configuración en un dispositivo virtual que permite tooreceive el tráfico dirigido específicamente no toohello dispositivo y, a continuación, reenviar ese destino final de tooits de tráfico.

Por ejemplo, si AppVM01 realiza una solicitud enviada al servidor DNS01 toohello, UDR enrutaría este tráfico toohello firewall. Con el reenvío IP habilitada, tráfico de hello para el destino de hello DNS01 (10.0.2.4) es aceptado por dispositivo de hello (10.0.0.4) y, a continuación, reenvía el destino último tooits (10.0.2.4). Sin el reenvío IP habilitada en firewall de hello, tráfico no haría aceptado por dispositivo de Hola a pesar de la tabla de rutas Hola dispone firewall Hola salto siguiente Hola. toouse un dispositivo virtual, es fundamental tooremember tooenable IP reenvío junto con UDR.

#### <a name="nsg-description"></a>Descripción del grupo de seguridad de red
En este ejemplo, se crea un grupo de seguridad de red y se carga después con una única regla. Este grupo es, a continuación, enlazar sólo toohello front-end y back-end subredes (y no Hola SecNet). Mediante declaración se va a compilar Hola siguiente regla:

* Se deniega todo (todos los puertos) el tráfico desde Hola Internet toohello toda la red virtual (todas las subredes).

Aunque en este ejemplo se usan grupos de seguridad de red, su principal objetivo es constituir un segundo nivel de defensa frente a errores de configuración manual. Hello objetivo es tooblock todo el tráfico entrante de hello Internet tooeither Hola subredes front-end o back-end. Solo debe flujo de tráfico a través de firewall de hello SecNet subred toohello (y, a continuación, si procede, en las subredes de front-end o back-end de toohello). Además, con las reglas UDR de hello en su lugar, todo el tráfico que ha llegado en hello subredes front-end o back-end se dirigirá out toohello firewall (gracias tooUDR). firewall de Hola que vea este tráfico como un flujo asimétrico y reduciría el tráfico saliente Hola. Por lo tanto, hay tres niveles de seguridad que protege subredes hello:

* No hay ninguna dirección IP pública en ningún NIC de FrontEnd o BackEnd.
* NSG deniega el tráfico de Internet Hola.
* Hola firewall prohibir asimétrica el tráfico.

Un aspecto interesante sobre hello NSG en este ejemplo es que contiene solo una regla, que es toodeny Internet tráfico toohello toda red virtual, incluida la subred de seguridad de Hola. Sin embargo, puesto que hello que NSG solo está enlazado toohello front-end y back-end subredes, regla de hello no procesados en tráfico entrante toohello subred de seguridad. Como resultado, el tráfico fluye toohello subred de seguridad.

#### <a name="firewall-rules"></a>Reglas de firewall
En el firewall de hello, se deben crear las reglas de reenvío. Puesto que firewall de hello está bloqueando o reenvío todo el tráfico entrante, saliente y tráfico de red virtual dentro, se necesitan muchas reglas de firewall. Además, todo el tráfico entrante llega a la dirección IP pública de hello servicio de seguridad (en puertos diferentes), toobe procesados por firewall de Hola. Una práctica recomendada es flujos lógicos de Hola toodiagram antes de configurar subredes de Hola y reglas de firewall, tooavoid deben revisar más adelante. Hello siguiente ilustración es una vista lógica de reglas de firewall de hello en este ejemplo:

![10]

> [!NOTE]
> Según Hola que utiliza otros dispositivos de red Virtual, los puertos de administración de hello varían. En este ejemplo se hace referencia a un firewall Barracuda NextGen que usa los puertos 22, 801 y 807. Consulte Hola dispositivo proveedor documentación toofind Hola exacta puertos utilizados para la administración de dispositivos Hola usándola.
>
>

#### <a name="firewall-rules-description"></a>Descripción de reglas de firewall
Hola anterior diagrama lógico, subred de seguridad de hello no se muestra porque firewall hello es el único recurso al que hello en esa subred. diagrama de Hello es que muestra las reglas de firewall de Hola y cómo lógicamente permitir o denegación flujos de tráfico, no Hola enrutado ruta de acceso real. Además, puertos externos Hola seleccionados para hello tráfico de RDP son puertos rango superior (8014 – 8026) y se han seleccionado tooloosely alinear con hello última dos octetos de la dirección IP local de Hola para mejorar la legibilidad sea más fácil (por ejemplo, dirección de servidor local 10.0.1.4 está asociado con el puerto externo 8014). Sin embargo, podría usarse cualquier puerto superior que no planteara conflictos.

En este ejemplo, necesitamos siete tipos de reglas:

* Reglas externas (para el tráfico entrante):
  1. Regla de Firewall de administración: una regla de redireccionamiento de esta aplicación permite tráfico toopass toohello los puertos de administración del dispositivo de hello red virtual.
  2. Las reglas RDP (para cada servidor de Windows): estos cuatro reglas (uno para cada servidor) que admita la administración de hello servidores individuales a través de RDP. También se pueden contraer cuatro reglas RDP Hello en una regla, según las capacidades de hello de dispositivo virtual en la red de Hola que se va a usar.
  3. Las reglas de tráfico de aplicación: hay dos de estas reglas, Hola primero para el tráfico de web front-end de Hola y Hola en segundo lugar para el tráfico de back-end de hello (por ejemplo, la capa del toodata servidor web). configuración de Hola de estas reglas depende de la arquitectura de red de hello (donde se colocan los servidores) y flujos de tráfico (el tráfico de Hola de qué dirección fluye y qué puertos se usan).
     * primera regla de Hello permite que servidor de aplicaciones de hello aplicación real tráfico tooreach Hola. Mientras hello otras reglas de permiten la administración y seguridad, las reglas de tráfico de aplicación son los que permiten tooaccess de los usuarios o servicios externos aplicaciones Hola. En este ejemplo, hay un solo servidor web en el puerto 80. Por lo tanto una única aplicación regla de firewall redirige el tráfico entrante toohello externo IP, dirección IP interna de servidores de web de toohello. sesión de tráfico de Hello redirigido se traducirían a través de NAT toohello interno del servidor.
     * segunda regla de Hello es Hola regla de back-end tooallow hello web tootalk toohello AppVM01 servidor (pero no AppVM02) a través de cualquier puerto.
* Reglas internas (para el tráfico entre redes virtuales)
  1. Regla de salida tooInternet: esta regla permite el tráfico desde cualquier red toopass toohello seleccionado redes. Esta regla suele ser una regla predeterminada ya en firewall de hello, pero en un estado deshabilitado. Esta regla debe habilitarse para este ejemplo.
  2. Regla de DNS: esta regla permite sólo DNS (el puerto 53) tráfico toopass toohello servidor DNS. Para este entorno, se bloquea la mayor parte del tráfico de hello front-end toohello back-end. Esta regla permite específicamente DNS desde cualquier subred local.
  3. Regla de toosubnet de subred: esta regla es tooallow cualquier servidor en servidor de tooany de tooconnect de subred back-end de Hola de subred de front-end de hello (pero no Hola inversa).
* Regla para notificaciones de error (para el tráfico que no cumple alguna de hello anterior):
  1. Denegar todas las reglas de tráfico: esta regla de denegación siempre debe ser regla final de hello (en términos de prioridad) y, por lo tanto si un flujo de tráfico se produce un error toomatch cualquiera de hello anterior reglas se quita esta regla. Esta regla es la predeterminada y, por lo general, está establecida y activa. Ninguna modificación es normalmente necesarios toothis regla.

> [!TIP]
> En hello segunda aplicación de tráfico de regla, toosimplify en este ejemplo, cualquier puerto está permitido. En un escenario real, hello más específicos puertos e intervalos de direcciones deben ser la superficie expuesta a ataques hello tooreduce usadas de esta regla.
>
>

Una vez que se crean las reglas anteriores de hello, es importante tooreview prioridad Hola el tráfico de tooensure de cada regla se permitirá o denegará según sea necesario. En este ejemplo, reglas de hello están en orden de prioridad.

#### <a name="conclusion"></a>Conclusión
En este ejemplo es un valor más complejo pero completar de manera de proteger y el aislamiento de red de Hola de hello en los ejemplos anteriores. (Ejemplo 2 protege solo la aplicación hello y 1 en el ejemplo se aísla solo subredes). Este diseño permite supervisar el tráfico en ambas direcciones y protege hello no solo los servidores de aplicación entrantes pero aplica la directiva de seguridad de red para todos los servidores en esta red. Además, función usa un dispositivo de hello, reconocimiento y auditoría de tráfico completo será posible. Para obtener más información, vea hello [instrucciones de compilación][Example3]. Estas instrucciones incluyen lo siguiente:

* Cómo toobuild este perímetro de ejemplo de la red con los scripts de PowerShell clásicos.
* ¿Cómo toobuild este ejemplo con una plantilla de Azure Resource Manager.
* Descripciones detalladas de cada enrutamiento definido por el usuario, comando de grupo de seguridad de red y regla de firewall.
* Escenarios de flujo de tráfico detallados, que muestran cómo se permite o se deniega el tráfico en cada nivel.

### <a name="example-4-add-a-hybrid-connection-with-a-site-to-site-virtual-appliance-vpn"></a>Ejemplo 4: Incorporación de una conexión híbrida con una VPN de dispositivo virtual de sitio a sitio
[Hacer copia de inicio de tooFast](#fast-start) | Obtener las instrucciones de compilación disponible pronto

[![11]][11]

#### <a name="environment-description"></a>Descripción del entorno
Las redes híbridas con un dispositivo de red virtual (NVA) se pueden agregar tooany de tipos de red perimetral de hello descritos en los ejemplos 1, 2 o 3.

Como se muestra en la ilustración anterior hello, una conexión VPN a través de Internet (sitio a sitio) hello es tooconnect usado un tooan de red local red virtual de Azure a través de una NVA.

> [!NOTE]
> Si usas ExpressRoute con hello emparejamiento público de Azure opción habilitada, se debe crear una ruta estática. Esta ruta estática debe enrutar toohello dirección de IP de VPN de NVA corporativos de Internet y no a través de hello conexión ExpressRoute. Hola NAT requerido en hello Azure público el emparejamiento de ExpressRoute opción puede interrumpir la sesión VPN de Hola.
>
>

Una vez Hola VPN está en su lugar, Hola NVA es concentrador central de Hola para todas las subredes y redes. las reglas de reenvío de Hello firewall determinan qué tráfico se permiten flujos, se traducen a través de NAT, se redirigen o se quitan (incluso para los flujos de tráfico entre la red local de Hola y Azure).

Flujos de tráfico se deben considerar cuidadosamente, ya que se pueden optimizar o degradado por este patrón de diseño, función hello específico caso de uso.

Uso de entorno Hola creado en el ejemplo 3 y, a continuación, agregar una conexión de red híbrida VPN de sitio a sitio, produce Hola después de diseño:

[![12]][12]

enrutador local de Hola o cualquier otro dispositivo de red que sea compatible con la NVA para VPN, sería el cliente VPN de Hola. Este dispositivo físico sería responsable de iniciar y mantener la conexión de VPN de hello con su NVA.

Lógicamente toohello NVA, red Hola aspecto independiente cuatro "zonas de seguridad" con reglas de hello en hello NVA que se va a director principal de Hola de tráfico entre esas zonas:

![13]

#### <a name="conclusion"></a>Conclusión
Adición de Hola de una conexión de red de sitio a sitio VPN híbrida tooan red virtual de Azure puede ampliar la red local de hello en Azure de forma segura. Al usar una conexión VPN, se cifra el tráfico y los enruta a través de Internet de Hola. Hola NVA en este ejemplo proporciona una ubicación central tooenforce y administrar la directiva de seguridad de Hola. Para obtener más información, vea Hola detallada (próximamente) instrucciones de compilación. Estas instrucciones incluyen lo siguiente:

* Cómo toobuild red perimetral de este ejemplo con scripts de PowerShell.
* ¿Cómo toobuild este ejemplo con una plantilla de Azure Resource Manager.
* Escenarios de flujo de tráfico detallados, que muestran cómo fluye el tráfico en este diseño.

### <a name="example-5-add-a-hybrid-connection-with-a-site-to-site-azure-vpn-gateway"></a>Ejemplo 5: Incorporación de una conexión híbrida con una VPN de puerta de enlace de Azure de sitio a sitio
[Hacer copia de inicio de tooFast](#fast-start) | Obtener las instrucciones de compilación disponible pronto

[![14]][14]

#### <a name="environment-description"></a>Descripción del entorno
Las redes híbridas con una puerta de enlace de VPN de Azure se pueden agregar tipo de red de perímetro tooeither se describe en los ejemplos 1 o 2.

Como se muestra en hello anterior figura, una conexión VPN a través de Internet (sitio a sitio) hello es tooconnect usado un tooan de red local red virtual de Azure a través de una puerta de enlace VPN de Azure.

> [!NOTE]
> Si usas ExpressRoute con hello emparejamiento público de Azure opción habilitada, se debe crear una ruta estática. Esta ruta estática debe enrutar toohello dirección de IP de VPN de NVA corporativos de Internet y no a través de hello ExpressRoute WAN. Hola NAT requerido en hello Azure público el emparejamiento de ExpressRoute opción puede interrumpir la sesión VPN de Hola.
>
>

Hello en la ilustración siguiente se muestra hello dos extremos de la red de este ejemplo. En el primer borde hello, Hola NVA y NSG controlan los flujos de tráfico para redes de Azure dentro y entre Azure y Hola Internet. borde de segundo de Hello es hello Azure puerta de enlace VPN, que es un borde de red independiente y aislado entre local y Azure.

Flujos de tráfico se deben considerar cuidadosamente, ya que se pueden optimizar o degradado por este patrón de diseño, función hello específico caso de uso.

Utilizando el entorno de hello creado en el ejemplo 1 y, a continuación, agregar una conexión de red híbrida VPN de sitio a sitio, produce Hola después de diseño:

[![15]][15]

#### <a name="conclusion"></a>Conclusión
Adición de Hola de una conexión de red de sitio a sitio VPN híbrida tooan red virtual de Azure puede ampliar la red local de hello en Azure de forma segura. Con puerta de enlace de VPN nativo hello, el tráfico está cifrado IPSec y enruta a través de Internet de Hola. Además, usar puerta de enlace de VPN de Azure de hello puede proporcionar una opción de bajo costo (sin una licencia adicional de costo igual que con NVAs de terceros). Esta opción resulta más económica en el ejemplo 1, en el que no se usa ningún dispositivo virtual de red. Para obtener más información, vea Hola detallada (próximamente) instrucciones de compilación. Estas instrucciones incluyen lo siguiente:

* Cómo toobuild red perimetral de este ejemplo con scripts de PowerShell.
* ¿Cómo toobuild este ejemplo con una plantilla de Azure Resource Manager.
* Escenarios de flujo de tráfico detallados, que muestran cómo fluye el tráfico en este diseño.

### <a name="example-6-add-a-hybrid-connection-with-expressroute"></a>Ejemplo 6: Incorporación de una conexión híbrida con ExpressRoute.
[Hacer copia de inicio de tooFast](#fast-start) | Obtener las instrucciones de compilación disponible pronto

[![16]][16]

#### <a name="environment-description"></a>Descripción del entorno
Las redes híbridas mediante una conexión de intercambio de tráfico privado puede ser de ExpressRoute agregan tipo de red de perímetro tooeither se describe en los ejemplos 1 o 2.

Como se muestra en hello anterior figura, intercambio de tráfico privado ExpressRoute proporciona una conexión directa entre la red local y Hola red virtual de Azure. Tráfico transita solo red del proveedor de servicio de Hola y red de Microsoft Azure hello, nunca tocar Hola Internet.

> [!TIP]
> Usar ExpressRoute mantiene el tráfico de red corporativa desactivar Hola Internet. Además, se permiten los contratos de nivel de servicio del proveedor de ExpressRoute. Hola puerta de enlace de Azure puede pasar una too10 Gbps con ExpressRoute, mientras que con VPN de sitio a sitio, el rendimiento máximo de puerta de enlace de Azure de hello es 200 Mbps.
>
>

Tal como se muestra en hello siguiente diagrama, con este hello opción entorno ahora tiene dos extremos de la red. Hola NVA y NSG control flujos de tráfico para redes de Azure dentro y entre hello Internet, mientras que la puerta de enlace de hello es un borde de red independiente y aislado entre local y Azure y Azure.

Flujos de tráfico se deben considerar cuidadosamente, ya que se pueden optimizar o degradado por este patrón de diseño, función hello específico caso de uso.

Utilizando el entorno de hello creado en el ejemplo 1 y, a continuación, agregar una conexión de red híbrida de ExpressRoute, produce Hola después de diseño:

[![17]][17]

#### <a name="conclusion"></a>Conclusión
Adición de Hola de una conexión de red de emparejamiento de ExpressRoute privado puede ampliar la red local de hello en Azure de una latencia segura, inferior, superior realizar manera. Además, con hello nativo puerta de enlace de Azure, como en este ejemplo, proporciona una opción de bajo costo (no de licencia adicionales al igual que con NVAs de terceros). Para obtener más información, vea Hola detallada (próximamente) instrucciones de compilación. Estas instrucciones incluyen lo siguiente:

* Cómo toobuild red perimetral de este ejemplo con scripts de PowerShell.
* ¿Cómo toobuild este ejemplo con una plantilla de Azure Resource Manager.
* Escenarios de flujo de tráfico detallados, que muestran cómo fluye el tráfico en este diseño.

## <a name="references"></a>Referencias
### <a name="helpful-websites-and-documentation"></a>Documentación y sitios web útiles
* Acceder a Azure con Azure Resource Manager:
* Acceder a Azure con PowerShell: [https://docs.microsoft.com/powershell/azureps-cmdlets-docs/](/powershell/azure/overview)
* Documentación de redes virtuales: [https://docs.microsoft.com/azure/virtual-network/](https://docs.microsoft.com/azure/virtual-network/)
* Documentación del grupo de seguridad de red: [https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg](virtual-network/virtual-networks-nsg.md)
* Documentación del enrutamiento definido por el usuario: [https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview](virtual-network/virtual-networks-udr-overview.md)
* Puertas de enlace virtuales de Azure: [https://docs.microsoft.com/azure/vpn-gateway/](https://docs.microsoft.com/azure/vpn-gateway/)
* Redes VPN de sitio a sitio: [https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell](vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* Documentación de ExpressRoute (ser seguro toocheck secciones de "Introducción" y "How To" hello): [https://docs.microsoft.com/azure/expressroute/](https://docs.microsoft.com/azure/expressroute/)

<!--Image References-->
[0]: ./media/best-practices-network-security/flowchart.png "Diagrama de flujo de opciones de seguridad"
[2]: ./media/best-practices-network-security/azuresecurityfeatures.png "Características de seguridad de Azure"
[3]: ./media/best-practices-network-security/dmzcorporate.png "Red perimetral en una red corporativa"
[4]: ./media/best-practices-network-security/azuresecurityarchitecture.png "Arquitectura de seguridad de Azure"
[5]: ./media/best-practices-network-security/dmzazure.png "Red perimetral en una instancia de Azure Virtual Network"
[6]: ./media/best-practices-network-security/dmzhybrid.png "Red híbrida con tres límites de seguridad"
[7]: ./media/best-practices-network-security/example1design.png "Red perimetral de entrada con grupo de seguridad de red"
[8]: ./media/best-practices-network-security/example2design.png "Red perimetral de entrada con dispositivo virtual de red y grupo de seguridad de red"
[9]: ./media/best-practices-network-security/example3design.png "Red perimetral bidireccional con un dispositivo de red virtual, grupos de seguridad de red y enrutamiento definido por el usuario"
[10]: ./media/best-practices-network-security/example3firewalllogical.png "vista lógica de hello las reglas de Firewall"
[11]: ./media/best-practices-network-security/example3designoptions.png "Red perimetral con red híbrida conectada a un dispositivo virtual de red"
[12]: ./media/best-practices-network-security/example4designs2s.png "Red perimetral con un dispositivo virtual de red conectada mediante una VPN de sitio a sitio"
[13]: ./media/best-practices-network-security/example4networklogical.png "Red lógica desde la perspectiva del dispositivo virtual de red"
[14]: ./media/best-practices-network-security/example5designoptions.png "Red perimetral con puerta de enlace de Azure conectada a red híbrida de sitio a sitio"
[15]: ./media/best-practices-network-security/example5designs2s.png "Red perimetral con puerta de enlace de Azure mediante VPN de sitio a sitio"
[16]: ./media/best-practices-network-security/example6designoptions.png "Red perimetral con puerta de enlace de Azure conectada a red híbrida de ExpressRoute"
[17]: ./media/best-practices-network-security/example6designexpressroute.png "Red perimetral con puerta de enlace de Azure mediante una conexión de ExpressRoute"

<!--Link References-->
[TrustCenter]: https://azure.microsoft.com/support/trust-center/compliance/
[Example1]: ./virtual-network/virtual-networks-dmz-nsg.md
[Example2]: ./virtual-network/virtual-networks-dmz-nsg-fw-asm.md
[Example3]: ./virtual-network/virtual-networks-dmz-nsg-fw-udr-asm.md
[Example4]: ./virtual-network/virtual-networks-hybrid-s2s-nva-asm.md
[Example5]: ./virtual-network/virtual-networks-hybrid-s2s-agw-asm.md
[Example6]: ./virtual-network/virtual-networks-hybrid-expressroute-asm.md
[Example7]: ./virtual-network/virtual-networks-vnet2vnet-direct-asm.md
[Example8]: ./virtual-network/virtual-networks-vnet2vnet-transit-asm.md
