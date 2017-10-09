---
title: aaaGetting a trabajar con la seguridad de Microsoft Azure | Documentos de Microsoft
description: "Este artículo proporciona información general sobre las capacidades de seguridad de Microsoft Azure y consideraciones generales para las organizaciones que están migrando a su proveedor de nube tooa activos."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 8d8a0088-c85a-48e7-bd04-2bc7b78b0691
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: yurid
ms.openlocfilehash: c61dd99ffd0143bc7b165367dadadc977ffcf47b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-microsoft-azure-security"></a>Introducción a la seguridad de Microsoft Azure
Al compilar o migrar proveedor de nube de tooa de activos de TI, está confiando en tooprotect de capacidades de la organización sus aplicaciones y datos con los servicios de Hola y controles de Hola que proporcionan una seguridad de hello toomanage de sus activos en la nube.

Diseño de la infraestructura de Azure de hello facility tooapplications para hospedar simultáneamente millones de clientes y proporciona una base de confianza en los que las empresas pueden satisfacer sus necesidades de seguridad. Además, Azure le proporciona una amplia gama de toocontrol de capacidad de hello y opciones de seguridad configurables usarlas para que puedan personalizar requisitos únicos Hola de seguridad toomeet de las implementaciones.

En este artículo de información general sobre la seguridad de Azure, veremos:

* Servicios de Azure y características que puede usar toohelp protegen los servicios y los datos dentro de Azure.
* Cómo Microsoft protege hello toohelp de infraestructura de Azure protegen sus datos y aplicaciones.

## <a name="identity-and-access-management"></a>Administración de identidades y acceso
Es fundamental controlar la infraestructura de acceso tooIT, datos y aplicaciones. Microsoft Azure proporciona estas funcionalidades con servicios como Azure Active Directory (Azure AD) o Azure Storage, y admite numerosos estándares y API.

[Azure AD](../active-directory/active-directory-whatis.md) es un repositorio de identidades y un motor que proporciona autenticación, autorización y control de acceso para usuarios, grupos y objetos de una organización. Azure AD también ofrece a los desarrolladores una administración de identidad de toointegrate de manera eficaz en sus aplicaciones. Protocolos estándar del sector como [SAML 2.0](https://en.wikipedia.org/wiki/SAML_2.0), [WS-Federation](https://msdn.microsoft.com/library/bb498017.aspx) y [OpenID Connect](http://openid.net/connect/) hacen posible el inicio de sesión en plataformas como .NET, Java, Node.js y PHP.

Hola basado en REST API de Graph permite a los desarrolladores tooread y escritura toohello directory desde cualquier plataforma. Gracias a la compatibilidad con [OAuth 2.0](http://oauth.net/2/), los desarrolladores pueden compilar aplicaciones móviles y web que se integran con las API web de Microsoft y de terceros, así como crear API web seguras propias. Hay bibliotecas de cliente de código abierto disponibles para .NET, la Tienda Windows, iOS y Android, así como otras bibliotecas en fase de desarrollo.

### <a name="how-azure-enables-identity-and-access-management"></a>Cómo habilita Azure la administración de identidades y acceso
Azure AD se puede usar como un directorio en la nube independiente para su organización, o bien como una solución integrada con su Active Directory local existente. Algunas características de integración incluyen la sincronización de directorios y el inicio de sesión único (SSO). Estos ampliación el alcance de hello sus identidades local existente en la nube de Hola y mejoran la experiencia de administrador y del usuario de Hola.

Otras capacidades de administración de identidades y acceso incluyen:

* Azure permite AD [SSO](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) tooSaaS aplicaciones, independientemente de dónde se hospedan. Algunas aplicaciones están federadas con Azure AD y otras usan SSO con contraseña. Las aplicaciones federadas también pueden admitir el aprovisionamiento de usuarios y almacén de contraseñas.
* Acceso toodata en [el almacenamiento de Azure](https://azure.microsoft.com/services/storage/) se controla mediante la autenticación. Cada cuenta de almacenamiento tiene una clave principal ([clave de la cuenta de almacenamiento](https://msdn.microsoft.com/library/azure/ee460785.aspx), o SAK) y una clave secreta secundaria (firma de acceso compartido de Hola o SAS).
* Azure AD proporciona identidad como servicio a través de la federación (mediante los [Servicios de federación de Active Directory](../active-directory/fundamentals-identity.md)), sincronización y replicación de directorios locales.
* [La autenticación multifactor Azure](../multi-factor-authentication/multi-factor-authentication.md) es servicio de la autenticación multifactor de Hola que requiere inicios de sesión de los usuarios tooverify mediante el uso de una aplicación móvil, una llamada de teléfono o un mensaje de texto. Se puede utilizar con los recursos de Azure AD toohelp seguras en entornos con el servidor de la autenticación multifactor Azure hello y también con aplicaciones personalizadas o directorios que usan Hola SDK.
* [Servicios de dominio de Azure AD](https://azure.microsoft.com/services/active-directory-ds/) le permite unir máquinas virtuales de Azure tooa dominio sin necesidad de implementar controladores de dominio. Puede iniciar sesión en las máquinas virtuales toothese con sus credenciales corporativas de Active Directory y administrar las máquinas virtuales Unidos a un dominio mediante líneas de base de seguridad de directiva de grupo tooenforce en todas las máquinas virtuales de Azure.
* [Azure B2C Directory Active](https://azure.microsoft.com/services/active-directory-b2c/) proporciona un servicio de administración de identidad global de alta disponibilidad para las aplicaciones orientadas al consumidor que escala toohundreds de millones de identidades. Se puede integrar en plataformas móviles y web. Los consumidores pueden iniciar sesión en tooall las aplicaciones a través de experiencias personalizables mediante sus cuentas sociales existentes o crear nuevas credenciales.

## <a name="data-access-control-and-encryption"></a>Control de acceso de datos y cifrado
Microsoft utiliza principios de Hola de separación de obligaciones y [privilegios mínimos](https://en.wikipedia.org/wiki/Principle_of_least_privilege) a lo largo de las operaciones de Azure. Toodata acceso por el personal de soporte técnico de Azure requiere el permiso explícito y se concede de forma "just-in-time" que se registran y auditar, a continuación, revoca tras la finalización de contratación de Hola.

Azure también proporciona varias funcionalidades para proteger los datos en tránsito y en reposo. Por ejemplo, cifrado de datos, archivos, aplicaciones, servicios, comunicaciones y unidades. Puede cifrar la información antes de colocarla en Azure y también almacenar las claves en sus centros de datos locales.

![Microsoft Antimalware en Azure](./media/azure-security-getting-started/sec-azgsfig1.PNG)

### <a name="azure-encryption-technologies"></a>Tecnologías de cifrado de Azure
Puede recopilar detalles en el entorno de acceso administrativo tooyour suscripción mediante el uso de [informes de Azure AD](../active-directory/active-directory-reporting-audit-events.md). Puede configurar [Cifrado de unidad BitLocker](https://technet.microsoft.com/library/cc732774.aspx) en los discos duros virtuales que contienen información confidencial en Azure.

Otras funciones de Azure que te ayudará a tookeep que proteger los datos incluyen:

* Los desarrolladores de aplicaciones pueden crear el cifrado en las aplicaciones de Hola que implementan en Azure mediante el uso de Windows hello [CryptoAPI](https://msdn.microsoft.com/library/ms867086.aspx) y .NET Framework.
* Controlar totalmente las claves de hello con cifrado en el cliente para el almacenamiento de blobs de Azure. servicio de almacenamiento de Hello nunca ve las claves de hello y no es capaz de descifrar los datos de Hola.
* [Azure Rights Management (Azure RMS)](https://technet.microsoft.com/library/jj585026.aspx) (con hello [RMS SDK](https://msdn.microsoft.com/library/dn758244.aspx)) proporciona el archivo y la prevención de pérdida de datos y el cifrado de nivel de datos mediante la administración basada en directivas de acceso.
* Azure es compatible con el [cifrado de nivel de tabla y columna (TDE/CLE)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/12/recommendations-for-using-cell-level-encryption-in-azure-sql-database.aspx) en máquinas virtuales de SQL Server y admite servidores de administración de claves locales de terceros en centros de datos.
* Claves de la cuenta de almacenamiento, firmas de acceso compartido, certificados de administración y otras claves son único tooeach inquilino de Azure.
* Azure [StorSimple](http://www.microsoft.com/server-cloud/products/storsimple/overview.aspx) almacenamiento híbrido cifra los datos a través de un par de claves pública/privada 128 bits antes de cargarlo tooAzure almacenamiento.
* Azure admite y utiliza numerosos mecanismos de cifrado, como SSL/TLS, IPsec y AES, dependiendo de los transportes, contenedores y tipos de datos de Hola.

## <a name="virtualization"></a>Virtualización
Hola plataforma Windows Azure usa un entorno virtualizado. Instancias de usuario funcionan como máquinas virtuales independientes que no tiene el servidor de acceso tooa host físico, y este aislamiento se aplica mediante físico [niveles de privilegios de procesador (anillo 0/anillo 3)](https://en.wikipedia.org/wiki/Protection_ring).

Anillo 0 es hello más con privilegios y 3 es hello menos. SO invitado de Hola se ejecuta en un 1 de anillo con menos privilegios, y las aplicaciones se ejecutan Hola 3 de anillo con privilegios mínimos. Esta virtualización de los recursos físicos provoca una separación clara de tooa entre SO invitado e hipervisor, resultante de separación de seguridad adicional entre dos Hola.

Hola hipervisor Azure actúa como un micro-kernel y pasa todas las solicitudes de acceso de hardware del host de toohello de máquinas virtuales de invitado para su procesamiento mediante una interfaz de memoria compartida denominada VMBus. Esto impide que los usuarios obtengan sistema toohello de acceso de lectura/escritura/ejecución sin procesar y reduce el riesgo de Hola de uso compartido de recursos del sistema.

![Microsoft Antimalware en Azure](./media/azure-security-getting-started/sec-azgsfig2.PNG)

### <a name="how-azure-implements-virtualization"></a>Cómo implementa Azure la virtualización
Azure usa un firewall de hipervisor (filtro de paquetes) que se implementa en el hipervisor de Hola y configura un agente de controlador de tejido. Esto ayuda a proteger los inquilinos contra accesos no autorizados. De forma predeterminada, todo el tráfico se bloquea cuando se crea una máquina virtual y, a continuación, el agente de controlador de tejido de hello configura tooadd de filtro de paquetes de saludo *reglas y las excepciones* tooallow tráfico autorizado.

Existen dos categorías de reglas que se programan aquí:

* **Reglas de configuración de la máquina o la infraestructura**: de forma predeterminada, se bloquea toda la comunicación. No existe es excepciones tooallow toosend de una máquina virtual y recibir tráfico DHCP y DNS. Máquinas virtuales también pueden enviar tráfico toohello "public" internet y enviar tráfico tooother máquinas virtuales de clúster de Hola y el servidor de activación de SO Hola. lista de máquinas virtuales de Hola de destinos salientes permitidas no incluye subredes de enrutador de Azure, volver a administración de Azure final y otras propiedades de Microsoft.
* **Archivo de configuración de rol**: define Hola listas de Control de acceso (ACL) entrantes en función de modelo de servicio del inquilino de Hola. Por ejemplo, si un inquilino tiene un front-end Web en el puerto 80 en un determinado equipo virtual, a continuación, Azure abre tooall de puerto 80 TCP direcciones IP si va a configurar un punto de conexión en hello [modelo de implementación clásica Azure](../azure-resource-manager/resource-manager-deployment-model.md). Si máquina virtual de Hola tiene un rol de final o de trabajo espera que se ejecuta, a continuación, abre el rol trabajador de hello solo máquina virtual de toohello dentro de Hola mismo inquilino.

## <a name="isolation"></a>Aislamiento
Otro requisito de seguridad importante en la nube es tooprevent de separación no autorizada y no intencionales transferencia de información entre las implementaciones en una arquitectura de varios inquilinos compartida.

Azure implementa el [control de acceso de red](https://azure.microsoft.com/blog/network-isolation-options-for-machines-in-windows-azure-virtual-networks/) y la segregación mediante aislamiento de VLAN, listas ACL, equilibradores de carga y filtros IP. Restringe el tráfico externo entrantes tooports y protocolos en las máquinas virtuales que definen. Azure implementa tooprevent suplantada filtrando el tráfico de red y restringir los componentes de la plataforma tootrusted tráfico entrante y saliente. Se implementan directivas de flujo de tráfico en los dispositivos de protección de límites que deniegan el tráfico de forma predeterminada.

![Microsoft Antimalware en Azure](./media/azure-security-getting-started/sec-azgsfig3.PNG)

Traducción de direcciones de red (NAT) se utiliza tooseparate el tráfico de red interno de tráfico externo. El tráfico interno no es enrutable externamente. Las [direcciones IP virtuales](http://blogs.msdn.com/b/cloud_solution_architect/archive/2014/11/08/vips-dips-and-pips-in-microsoft-azure.aspx) que sean enrutables externamente se traducen en [direcciones IP dinámicas internas](http://blogs.msdn.com/b/cloud_solution_architect/archive/2014/11/08/vips-dips-and-pips-in-microsoft-azure.aspx) que solo se pueden enrutar en Azure.

Máquinas virtuales de tráfico externo tooAzure pasa a través de las ACL en los enrutadores, equilibradores de carga y conmutadores de capa 3. Solo se permiten determinados protocolos conocidos. Las ACL están en lugar toolimit tráfico procedentes de máquinas virtuales invitadas VLAN tooother usadas para la administración. Además, se filtra el tráfico a través de filtros IP en el tráfico de hello límites más de Hola de sistema operativo del host en ambas capas de red y de vínculo de datos.

### <a name="how-azure-implements-isolation"></a>Cómo implementa Azure el aislamiento
Hola controlador de tejido de Azure es responsable de asignar recursos de infraestructura tootenant cargas de trabajo y administra las comunicaciones unidireccionales desde equipos de toovirtual de host de Hola. Hola hipervisor Azure exige la memoria y separación del proceso entre máquinas virtuales y lo enruta forma segura los inquilinos tooguest SO de tráfico de red. Azure también implementa el aislamiento de inquilinos, el almacenamiento y las redes virtuales.

* Cada inquilino de Azure AD está aislado de forma lógica mediante límites de seguridad.
* Las cuentas de almacenamiento de Azure son suscripción tooeach único y acceso debe ser autenticado mediante una clave de cuenta de almacenamiento.
* Las redes virtuales están aisladas de forma lógica mediante una combinación de direcciones IP privadas únicas, firewalls y listas ACL de IP. Equilibradores de carga enrutan los de inquilinos de tráfico toohello adecuado en función de las definiciones de extremo.

## <a name="virtual-networks-and-firewalls"></a>Redes virtuales y firewalls
Hola [redes virtuales y distribuidas](http://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx) en la Ayuda de Azure, asegúrese de que el tráfico de red privada está aislado físicamente del tráfico de otras redes virtuales de Azure.

![Microsoft Antimalware en Azure](./media/azure-security-getting-started/sec-azgsfig4.PNG)

Su suscripción puede contener varias redes privadas aisladas (e incluir firewall, equilibrio de carga y traducción de direcciones de red).

Azure proporciona tres niveles principales de segregación de red en cada Azure toologically segregar tráfico del clúster. [Redes de área local virtuales](https://azure.microsoft.com/services/virtual-network/) (VLAN) se utilizan tooseparate el tráfico del cliente del resto de Hola de hello red de Azure. Toohello de acceso a red de Azure desde el clúster fuera de Hola está restringido a través de equilibradores de carga.

Tooand de tráfico de red de máquinas virtuales debe pasar a través de conmutador virtual de hipervisor de Hola. componente de filtro IP de Hello en SO raíz de hello aísla Hola raíz virtual machine desde máquinas virtuales de invitado de Hola y Hola invitado virtual máquinas entre sí. Realiza el filtrado de comunicación entre los nodos y Hola un inquilino toorestrict del tráfico de red pública de Internet (basado en la configuración del servicio del cliente de hello), mantiene los separados de otros inquilinos.

filtro IP de Hello ayuda a evitar máquinas virtuales de invitado desde:

* Generen tráfico falsificado
* Recibir tráfico no dirigirse a toothem.
* Dirige el tráfico tooprotected extremos de la infraestructura.
* Envíen o reciban tráfico de difusión inadecuado

Puede colocar las máquinas virtuales en [Azure Virtual Networks](https://azure.microsoft.com/documentation/services/virtual-network/). Estas redes virtuales son similares redes toohello configurar en entornos locales, que son suelen estar asociadas a un conmutador virtual. Máquinas virtuales conectadas toohello misma red virtual puede comunicarse entre sí sin ninguna configuración adicional. También puede configurar subredes diferentes dentro de la red virtual.

Puede usar Hola siga comunicaciones seguras de toohelp de tecnologías de red Virtual de Azure en la red virtual:

* [**Grupos de seguridad de red (NSG)**](../virtual-network/virtual-networks-nsg.md) Puede usar un tooone de tráfico NSG toocontrol o más instancias de máquina virtual en la red virtual. Un grupo de seguridad de red contiene reglas de control de acceso que permitan o denieguen el tráfico según la dirección del tráfico, el protocolo, la dirección de origen y el puerto, y la dirección de destino y el puerto.
* [**Enrutamiento definido por el usuario**](../virtual-network/virtual-networks-udr-overview.md) Puede controlar Hola enrutamiento de paquetes a través de un dispositivo virtual mediante la creación de rutas definidas por el usuario que especifican el próximo salto para los paquetes que fluyen de dispositivo de seguridad de red virtual de tooa subred específica toogo tooa de Hola.
* [**Reenvío de IP**](../virtual-network/virtual-networks-udr-overview.md) Un dispositivo de seguridad de red virtual debe ser capaz de tooreceive el tráfico entrante que no sea tooitself rellena. tooallow un tráfico de máquinas virtuales tooreceive direccionado tooother destinos, habilitar el reenvío IP para la máquina virtual de Hola.
* [**Tunelización forzada**](../vpn-gateway/vpn-gateway-about-forced-tunneling.md). La tunelización forzada permite redirigir o "forzar" todo el tráfico vinculado a Internet generado por las máquinas virtuales en una ubicación de red virtual tooyour atrás local a través de un túnel VPN de sitio a sitio para inspección y auditoría
* [**Listas ACL de puntos de conexión**](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Puede controlar qué equipos se permiten las conexiones entrantes de la máquina virtual de hello Internet tooa en la red virtual mediante la definición de las ACL de extremo.
* [**Soluciones de seguridad de red de asociados**](https://azure.microsoft.com/marketplace/). Hay una serie de soluciones de seguridad de red asociado que se pueden acceder desde hello Azure Marketplace.

### <a name="how-azure-implements-virtual-networks-and-firewalls"></a>Cómo implementa Azure las redes virtuales y los firewalls
Azure implementa firewalls de filtrado de paquetes en todas las máquinas virtuales host e invitadas de forma predeterminada. Imágenes de sistema operativo Windows de hello Azure Marketplace también tienen Firewall de Windows habilitado de forma predeterminada. Equilibradores de carga en el perímetro de Hola de comunicaciones de control de redes de Azure orientados al público en función de las ACL de IP administradas por los administradores del cliente.

Si Azure mueve los datos del cliente como parte de las operaciones normales o durante un desastre, lo hace a través de canales de comunicaciones privados y cifrados. Otras capacidades de empleados por Azure toouse de firewalls y redes virtuales son:

* **Firewall de host nativo**: Azure Service Fabric y Azure Storage se ejecutan en un sistema operativo nativo que no tiene ningún hipervisor. Por lo tanto, el firewall de windows hello está configurado con las dos conjuntos anterior Hola de reglas. Almacenamiento ejecuta rendimiento toooptimize nativo.
* **Firewall de host**: firewall de host de hello es tooprotect Hola sistema operativo del host que ejecuta Hola hipervisor. reglas de Hola único controlador de Service Fabric hello tooallow programados y sistema operativo del host de tootalk toohello de cuadros de salto en un puerto específico. Hello otras excepciones son tooallow respuesta DHCP y DNS respuestas. Azure usa un archivo de configuración de máquina que tiene Hola plantilla de reglas de firewall para el sistema operativo del host Hola. el propio host Hola está protegido frente a ataques externos mediante una Windows firewall configurado toopermit únicamente la comunicación de orígenes conocidos y autenticados.
* **Firewall de invitado**: replica las reglas de hello en el filtro de paquetes de conmutador de máquina virtual de hello pero programados en software diferente (como parte de Firewall de Windows hello de SO invitado de hello). firewall de máquina virtual de Hello invitado puede ser configurado toorestrict tooor de comunicaciones de la máquina virtual de hello invitado, aunque se permita una comunicación de Hola por las configuraciones en el host de hello filtro IP. Por ejemplo, puede decidir toouse Hola invitado virtual machine firewall toorestrict comunicación entre dos de sus redes virtuales que se han configurado tooconnect tooone otro.
* **Firewall de almacenamiento (FW)**: firewall de hello en front-end de almacenamiento de hello filtra toobe tráfico únicamente en los puertos 80/443 y otros puertos de utilidad es necesario. firewall de Hello en hello almacenamiento back-end restringe toocome comunicaciones sólo desde los servidores front-end de almacenamiento.
* **La puerta de enlace de red virtual**: Hola [puerta de enlace de red Virtual Azure](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) actúa como puerta de enlace de hello entre entornos conecta las cargas de trabajo en la red Virtual de Azure tooyour sitios locales. Es necesario tooconnect sitios tooon local a través de [túneles VPN de sitio a sitio de IPsec](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md), o a través [ExpressRoute](../expressroute/expressroute-introduction.md) circuitos. Para los túneles VPN de IPsec/IKE, puertas de enlace de hello realizan protocolos de enlace de IKE y establecer túneles de VPN de S2S de IPsec de hello entre redes virtuales de Hola y sitios locales. Las puertas de enlace de red virtual también terminan las [VPN de punto a sitio](../vpn-gateway/vpn-gateway-point-to-site-create.md).

## <a name="secure-remote-access"></a>Acceso remoto seguro
Datos almacenados en la nube de hello deben tener suficientes medidas de seguridad habilitados tooprevent vulnerabilidades y mantener la confidencialidad e integridad en tránsito. Esto incluye controles de red que se enlazan con los mecanismos de administración de acceso e identidades auditables basados en las directivas de una organización.

Tecnología cifrada integrada permite comunicaciones de tooencrypt dentro y entre las implementaciones, entre las regiones de Azure y de los centros de datos locales de tooon Azure. Toovirtual de acceso de administrador de equipos a través de [sesiones de escritorio remoto](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), [Windows PowerShell en remoto](http://blogs.technet.com/b/heyscriptingguy/archive/2013/09/07/weekend-scripter-remoting-the-cloud-with-windows-azure-and-powershell.aspx), y hello portal de Azure está siempre cifrado.

toosecurely ampliar sus instalaciones datacenter toohello en la nube, Azure proporciona ambos [VPN de sitio a sitio](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md) y [point-to-site VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md), además de vínculos dedicados con [ExpressRoute](../expressroute/expressroute-introduction.md)(tooAzure de conexiones se cifran las redes virtuales a través de VPN).

### <a name="how-azure-implements-secure-remote-access"></a>Cómo implementa Azure el acceso remoto seguro
Siempre se debe autenticar las conexiones toohello portal de Azure y requieren SSL/TLS. Puede configurar certificados tooenable segura de administración. Los protocolos seguros estándar del sector [SSTP](https://technet.microsoft.com/magazine/2007.06.cableguy.aspx) e [IPsec](https://en.wikipedia.org/wiki/IPsec) son totalmente compatibles.

[Azure ExpressRoute](../expressroute/expressroute-introduction.md) permite crear conexiones privadas entre los centros de datos de Azure y la infraestructura de su entorno local o de un entorno de ubicación compartida. Las conexiones ExpressRoute no pasan por hello Internet pública. Ofrecen más confiabilidad, velocidades más rápidas, latencias más bajas y mayor seguridad que los vínculos típicos basados en Internet. En algunos casos, el uso de conexiones de ExpressRoute para transferir datos entre ubicaciones locales y Azure también puede aportar beneficios económicos importantes.

## <a name="logging-and-monitoring"></a>Registro y supervisión
Azure proporciona autenticado el registro de eventos relativas a la seguridad que generan una pista de auditoría, y es tootampering toobe resistente a ingeniería. Esto incluye información del sistema, como registros de eventos de seguridad en las máquinas virtuales de infraestructura de Azure y Azure AD. Supervisión de eventos de seguridad incluye la recopilación de eventos, como los cambios en las direcciones IP del servidor DHCP o DNS; intento de acceso tooports, protocolos o direcciones IP que están bloqueadas por diseño; cambios en la configuración de firewall o la directiva de seguridad; creación de cuenta o grupo; y procesos inesperados o en la instalación del controlador.

![Microsoft Antimalware en Azure](./media/azure-security-getting-started/sec-azgsfig5.PNG)

La grabación de registros de auditoría de accesos de usuario con privilegios y actividades, intentos de acceso autorizados y no autorizados, excepciones del sistema e información de eventos de seguridad se conservan durante un período de tiempo establecido. retención de Hola de los registros es a su entera discreción como configurar la recopilación de registros y los requisitos de retención tooyour propio.

### <a name="how-azure-implements-logging-and-monitoring"></a>Cómo implementa Azure el registro y la supervisión
Azure implementa compute de tooeach de agentes de agentes de administración (MA) y Monitor de seguridad de Azure (ASM), almacenamiento o el nodo de fabric bajo la administración sean nativo o virtual. Cada agente de administración es la cuenta de almacenamiento configurado tooauthenticate tooa servicio equipo con un certificado obtenido del almacén de certificados de Azure de Hola y reenviar preconfigurado y diagnóstico y la cuenta de almacenamiento de toohello de datos de evento. Estos agentes no son las máquinas virtuales de implementada toocustomers.

Administradores de Azure tener acceso a los registros a través de un portal web para los registros de toohello acceso autenticado y controlada. Un administrador puede analizar, filtrar, correlacionar y analizar los registros. cuentas de almacenamiento de equipo de servicio de Azure de Hola para registros están protegidos frente a toohelp de acceso de administrador directo evitar ante la manipulación del registro.

Microsoft recopila registros de dispositivos de red mediante Protocolo de Syslog de Hola y de servidores de host mediante servicios de recopilación de auditorías (ACS) de Microsoft. Estos registros se colocan en una base de datos de registros desde la que se generan alertas para eventos sospechosos. Administrador de Hello puede tener acceso y analizar estos registros.

[Diagnósticos de Azure](https://msdn.microsoft.com/library/azure/gg433048.aspx) es una característica de Azure que permite los datos de diagnóstico de toocollect desde una aplicación que se ejecuta en Azure. Se trata de datos de diagnóstico para depurar y solucionar problemas, medir el rendimiento, supervisar el uso de los recursos, analizar el tráfico y planificar la capacidad y realizar auditorías. Después de recopilan datos de diagnóstico de hello, puede ser transferido tooan cuenta de almacenamiento de Azure para su persistencia. Las transferencias pueden se programadas o a petición.

## <a name="threat-mitigation"></a>Mitigación de amenazas
En suma tooisolation, cifrado y el filtrado, Azure emplea a una serie de mecanismos de mitigación de amenazas e infraestructura tooprotect de procesos y servicios. Se incluyen los controles internos y tecnologías que se usan toodetect y corregir avanzadas amenazas como DDoS, un aumento de privilegios y Hola [OWASP los 10](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project).

controles de seguridad de Hola y procesos de administración de riesgos Microsoft tiene en toosecure lugar reducir su infraestructura de nube Hola a riesgo de incidentes de seguridad. Hola un incidente caso, equipo de administración de incidentes de seguridad (SIM) hello en el equipo de Microsoft Online Services de seguridad y cumplimiento (OSSC) de hello es toorespond listo en cualquier momento.

### <a name="how-azure-implements-threat-mitigation"></a>Cómo implementa Azure la mitigación de amenazas
Azure tiene controles de seguridad de mitigación de amenazas de tooimplement de contexto y los clientes toohelp mitigar amenazas potenciales en sus entornos. Hello lista siguiente resume las capacidades de mitigación de amenazas Hola que ofrece Azure:

* [Azure Anti-Malware](azure-security-antimalware.md) está habilitado de forma predeterminada en todos los servidores de infraestructura. Opcionalmente, puede habilitarlo en sus propias máquinas virtuales.
* Microsoft mantiene continuo de supervisión a través de servidores, redes y aplicaciones amenazas toodetect y evitar vulnerabilidades de seguridad. Alertas automatizadas notificar a los administradores de los comportamientos anómalos, lo que les tootake de acción correctiva en amenazas internas y externas.
* Puede implementar soluciones de seguridad de terceros dentro de sus suscripciones, como pueden ser los firewalls de aplicaciones web de [Barracuda](https://techlib.barracuda.com/ng54/deployonazure).
* Microsoft enfoque toopenetration pruebas incluyan "[formación de equipos de Red](http://download.microsoft.com/download/C/1/9/C1990DBA-502F-4C2A-848D-392B93D9B9C3/Microsoft_Enterprise_Cloud_Red_Teaming.pdf)," que permite a los profesionales de seguridad de Microsoft para atacar a sistemas de producción en directo (que no sea de clientes) en Azure tootest defensas contra reales, avanzadas , amenazas persistentes.
* Sistemas de implementación integrada administración Hola distribución e instalación de revisiones de seguridad a través de hello plataforma Windows Azure.

## <a name="next-steps"></a>Pasos siguientes
[Centro de confianza de Azure](https://azure.microsoft.com/support/trust-center/)

[Blog del equipo de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/)

[Centro de respuesta de seguridad de Microsoft](https://technet.microsoft.com/library/dn440717.aspx)

[Blog de Active Directory](http://blogs.technet.com/b/ad/)
