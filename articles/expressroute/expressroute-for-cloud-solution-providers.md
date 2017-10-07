---
title: aaaAzure ExpressRoute para proveedores de soluciones de nube | Documentos de Microsoft
description: "Este artículo proporciona información para los proveedores de servicios de nube que tooincorporate desea Azure ExpressRoute en sus ofertas y servicios."
documentationcenter: na
services: expressroute
author: richcar
manager: carmonm
editor: 
ms.assetid: f6c5f8ee-40ba-41a1-ae31-67669ca419a6
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: richcar
ms.openlocfilehash: 062ecbb5e461e4384b01c4ac478cab696b7ed398
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-for-cloud-solution-providers-csp"></a>ExpressRoute para proveedores de soluciones en la nube (CSP)
Microsoft ofrece servicios de Hyper-escala para distribuidores tradicionales y aprovisionamiento de distribuidores (CSP) toobe toorapidly capaz de nuevos servicios y soluciones para los clientes sin Hola necesitan tooinvest en el desarrollo de estos nuevos servicios. tooallow Hola proveedor de soluciones de nube (CSP) Hola capacidad toodirectly administrar estos nuevos servicios, Microsoft ofrece programas y las API que permiten Hola CSP toomanage recursos de Microsoft Azure en nombre de sus clientes. Uno de esos recursos es ExpressRoute. ExpressRoute permite Hola CSP tooconnect cliente recursos tooAzure los servicios existentes. ExpressRoute es un tooservices de vínculo de comunicaciones privadas de alta velocidad en Azure. 

ExpresRoute está formada por un par de circuitos para lograr alta disponibilidad tooa adjunto suscripciones de cliente único y no puede compartirse por varios clientes. Cada circuito debe terminar en un enrutador diferentes toomaintain Hola de alta disponibilidad.

> [!NOTE]
> Existen límites de ancho de banda y de conexión en ExpressRoute, lo que significa que las implementaciones grandes o complejas requerirán varios circuitos ExpressRoute para un único cliente.
> 
> 

Microsoft Azure proporciona a un creciente número de servicios que puede ofrecer la clientes tooyour.  toobest aprovechar las ventajas de estos servicios requieren el uso de hello ExpressRoute conexiones tooprovide alta velocidad baja latencia acceso toohello entorno de Microsoft Azure.

## <a name="microsoft-azure-management"></a>Administración de Microsoft Azure
Microsoft ofrece CSP API toomanage las suscripciones de cliente de Azure de hello permitiendo la integración mediante programación con sus propios sistemas de administración de servicio. Las funcionalidades de administración compatibles se explican [aquí](https://msdn.microsoft.com/library/partnercenter/dn974944.aspx).

## <a name="microsoft-azure-resource-management"></a>Administración de recursos de Microsoft Azure
Función hello contrato que tiene con su cliente determinarán cómo se administrarán suscripción Hola. Hola CSP puede administrar directamente la creación de hello y mantenimiento de recursos o un cliente de hello puede mantener el control de hello suscripción de Microsoft Azure y crear Hola recursos de Azure que necesitan. Si el cliente administra la creación de hello de recursos en su suscripción de Microsoft Azure usará uno de dos modelos: modelo de "Conectar a través" o "Direct-To" modelo. Estos modelos se describen en detalle en las secciones siguientes de Hola.  

### <a name="connect-through-model"></a>Modelo Conexión a través
![texto alternativo](./media/expressroute-for-cloud-solution-providers/connect-through.png)  

En hello conectarse mediante modelo Hola CSP crea una conexión directa entre el centro de datos y suscripción de Azure de su cliente. conexión directa de Hola se realiza mediante ExpressRoute, conectar la red con Azure. A continuación, el cliente conecta a red tooyour. Este escenario requiere que ese cliente hello atraviesa Hola CSP red tooaccess servicios de Azure. 

Si el cliente tiene otras suscripciones de Azure no administrados por Hola se, usarían Hola Internet pública o sus propios servicios de conexión privada tooconnect toothose aprovisionados en la suscripción de CSP no Hola. 

Para administrar los servicios de Azure de CSP, se supone que Hola CSP tiene una identidad de cliente establecida previamente almacenar que, a continuación, se replicará en Azure Active Directory para la administración de su suscripción de CSP mediante Administrate-On-Behalf-Of (AOBO). Impulsores clave para este escenario incluyen donde un asociado determinado o un proveedor de servicios tiene una relación establecida con el cliente de Hola, cliente hello está consumiendo servicios de proveedor actualmente o socio de hello tiene un tooprovide deseo una combinación de hospedado por el proveedor soluciones hospedadas en Azure tooprovide flexibilidad y la dirección del cliente desafíos y que no se puede satisfacer mediante CSP independiente. Este modelo se muestra en la **figura**siguiente.

![texto alternativo](./media/expressroute-for-cloud-solution-providers/connect-through-model.png)

### <a name="connect-toomodel"></a>Toomodel conectar
![texto alternativo](./media/expressroute-for-cloud-solution-providers/connect-to.png)

Hola toomodel conectar, el proveedor de servicios de hello crea una conexión directa entre el centro de datos de sus clientes y CSP hello aprovisionado suscripción de Azure mediante ExpressRoute a través de hello del cliente (customer) red.

> [!NOTE]
> Para ExpressRoute cliente hello ¿necesita toocreate y mantener el circuito de ExpressRoute de Hola.  
> 
> 

Este escenario de conectividad requiere que ese cliente Hola se conecta directamente a través de un tooaccess de red de cliente suscripción a Azure administrada por el CSP, mediante una conexión de red directa que se creó, posee y administra total o parcialmente por el cliente de Hola. Para estos clientes se supone que proveedor hello no tiene actualmente un almacén de identidades de cliente establecido y proveedor de hello ayudaría a clientes de hello en la replicación de su almacén de identidad actual en Azure Active Directory para la administración de sus suscripción a través de AOBO. Impulsores clave para este escenario incluyen donde un asociado determinado o un proveedor de servicios tiene una relación establecida con el cliente de Hola, cliente hello está consumiendo servicios de proveedor actualmente o socio de hello tiene un servicio de tooprovide desea que solo se basa en Soluciones hospedadas en Azure sin Hola necesitan para un centro de datos de proveedor existente o una infraestructura de.

![texto alternativo](./media/expressroute-for-cloud-solution-providers/connect-to-model.png)

Hello elegir entre estas dos opciones dependen de las necesidades del cliente y la actual necesita tooprovide Azure servicios. detalles de Hola de estos modelos y Hola asociado el control de acceso basado en roles, redes, y los patrones de diseño de identidad se tratan detalladamente en hello siguientes vínculos:

* **Control de acceso basado en rol (RBAC)** : RBAC se basa en Azure Active Directory.  Para más información sobre RBAC en Azure, consulte [este artículo](../active-directory/role-based-access-control-configure.md).
* **Redes** – portadas Hola distintos temas de las redes de Microsoft Azure.
* **Azure Active Directory (AAD)** – AAD proporciona Hola de identity management for 3rd aplicaciones SaaS y Microsoft Azure. Para más información sobre Azure AD, consulte [este artículo](https://azure.microsoft.com/documentation/services/active-directory/).  

## <a name="network-speeds"></a>Velocidades de red
ExpressRoute es compatible con velocidades de red de 50 Mb/s too10Gb/s. Esto permite a los clientes toopurchase cantidad de Hola de ancho de banda de red necesario para su entorno único.

> [!NOTE]
> Ancho de banda de red se puede aumentar según sea necesario sin interrumpir las comunicaciones, pero tooreduce velocidad de la red de hello requiere destruir el circuito de Hola y volver a crearla en velocidad de red más baja de Hola.  
> 
> 

ExpressRoute admite la conexión de Hola de circuito ExpressRoute de varias redes virtuales tooa único para una mejor utilización de las conexiones de alta velocidad de Hola. Un circuito ExpressRoute único se puede compartir entre varias suscripciones de Azure propiedad Hola mismo cliente.

## <a name="configuring-expressroute"></a>Configuración de ExpressRoute
ExpressRoute puede ser configurado toosupport tres tipos de tráfico ([dominios de enrutamiento](#ExpressRoute-routing-domains)) a través de un circuito ExpressRoute único. Este tráfico se divide entre emparejamiento de Microsoft, pares públicos de Azure y pares privados. Puede seleccionar uno o todos los tipos de toobe de tráfico que se envían a través de un circuito ExpressRoute único o usar varios circuitos ExpressRoute según tamaño Hola de circuito de ExpressRoute de Hola y aislamiento requeridos por el cliente. postura de seguridad de Hello del cliente no se permita pública tráfico y tootraverse de tráfico privado sobre Hola mismo circuito.

### <a name="connect-through-model"></a>Modelo Conexión a través
En un Hola conectar a través de la configuración será responsable de todo Hola redes tooconnect Fundamentos sus suscripciones de toohello de recursos de centro de datos de los clientes que se hospedan en Azure. Cada uno de su cliente que desea toouse las capacidades de Azure tendrán que necesita su propia conexión ExpressRoute, que serán administrada por Hola se. Hello utilizará Hola mismo cliente de hello métodos utilizaría el circuito de ExpressRoute de tooprocure Hola. Hello seguirá Hola mismos pasos que se describen en el artículo hello [flujos de trabajo de ExpressRoute](expressroute-workflows.md) de aprovisionamiento del circuito y Estados del circuito. Hola, a continuación, configurará Hola protocolo de puerta de enlace de borde (BGP) rutas toocontrol Hola tráfico que fluye entre la red local de Hola y red virtual de Azure.

### <a name="connect-toomodel"></a>Toomodel conectar
En un tooconfiguration connect, su cliente ya tiene un tooAzure de conexión existente o se iniciará un proveedor de servicios de internet de conexión toohello vincular ExpressRoute desde el centro de datos del cliente tooAzure directamente, en lugar de su centro de datos. proceso de aprovisionamiento de hello toobegin, su cliente seguirá Hola pasos tal como se describió en modelo de hello conectar a través. Una vez que se ha establecido el circuito de hello su cliente necesitará tooconfigure Hola enrutadores locales toobe tooaccess capaz de su red y redes virtuales de Azure.

Puede ayudar a configurar la conexión de Hola y configurar Hola enruta los recursos de hello tooallow en su toocommunicate datacenter(s) recursos del cliente hello en el centro de datos o con recursos de hello hospedados en Azure.

## <a name="expressroute-routing-domains"></a>Dominios de enrutamiento de ExpressRoute
ExpressRoute ofrece tres dominios de enrutamiento: público, privado y emparejamiento de Microsoft. Cada uno de los dominios de enrutamiento Hola se configuran con enrutadores idénticos en la configuración activo / activo para alta disponibilidad. Para ver más detalles sobre los dominios de enrutamiento de ExpressRoute, consulte [este artículo](expressroute-circuit-peerings.md).

Puede definir las rutas personalizadas filtros tooallow solo Hola vías desea tooallow o necesita. Para obtener más información o toosee toomake estos cambios ven artículo: [crear y modificar el enrutamiento de un circuito de ExpressRoute mediante PowerShell](expressroute-howto-routing-classic.md) para obtener más información acerca de los filtros de enrutamientos.

> [!NOTE]
> Para Microsoft y emparejamiento público conectividad aunque debe ser una dirección IP pública pertenece a clientes de Hola o CSP y debe cumplir las reglas de tooall definido. Para obtener más información, vea hello [requisitos previos de ExpressRoute](expressroute-prerequisites.md) página.  
> 
> 

## <a name="routing"></a>Enrutamiento
ExpressRoute conecta toohello Azure redes a través de puerta de enlace de red Virtual Azure Hola. Las puertas de enlace de red proporcionan enrutamiento para las redes virtuales de Azure.

Crear redes virtuales de Azure, también crea una tabla de enrutamiento predeterminada para el tráfico de toodirect de red virtual de Hola de subredes de Hola de red virtual de Hola. Si la tabla de rutas predeterminadas de hello no es suficiente para la solución de saludo personalizado rutas se pueden crear dispositivos de toocustom de tráfico saliente tooroute o tooblock enruta toospecific subredes o redes externas.

### <a name="default-routing"></a>Enrutamiento predeterminado
tabla de rutas predeterminadas de Hello incluye Hola siguiendo rutas:

* Enrutamiento dentro de una subred
* Subred de subred dentro de la red virtual de Hola
* toohello Internet
* Entre redes virtuales mediante un puerta de enlace de VPN
* Entre una red virtual y una red local mediante una puerta de enlace de VPN o ExpressRoute

![texto alternativo](./media/expressroute-for-cloud-solution-providers/default-routing.png)  

### <a name="user-defined-routing-udr"></a>Enrutamiento definido por el usuario (UDR)
Las rutas definidas por el usuario permiten había asignado de hello control de tráfico de salida de hello subred tooother subredes de red virtual de Hola o con uno de Hola otras puertas de enlace predefinidos (ExpressRoute; internet o VPN). tabla de enrutamiento de sistema Hola predeterminado puede reemplazarse con una tabla de enrutamiento definidas por el usuario que reemplaza la tabla de enrutamiento de hello predeterminada con las rutas personalizadas. Con el enrutamiento de definido por el usuario, los clientes pueden crear tooappliances rutas específicas, como firewalls o dispositivos de detección de intrusiones o bloquear el acceso toospecific subredes de subred Hola ruta definida por el usuario de Hola de hospedaje. Para ver información general sobre las rutas definidas por el usuario, lea [este artículo](../virtual-network/virtual-networks-udr-overview.md). 

## <a name="security"></a>Seguridad
Dependiendo de qué modelo está en uso, conectar mediante Connect-tooor, su cliente define las directivas de seguridad de hello en su red virtual o proporciona requisitos de directiva de seguridad de hello toohello CSP toodefine tootheir las redes virtuales. Hola siguiendo criterios de seguridad se puede definir:

1. **Aislamiento de cliente** : hello plataforma Windows Azure proporciona aislamiento de cliente mediante el almacenamiento de información de Id. de cliente y de red virtual en una base de datos segura, que es usado tooencapsulate tráfico de cada cliente en un túnel GRE.
2. **Grupo de seguridad (NSG) de red** son las reglas para definir el tráfico permitido dentro y fuera de las subredes de hello en redes virtuales en Azure. De forma predeterminada, hello NSG contienen bloquea el tráfico de tooblock de reglas de red virtual de hello Internet toohello y reglas de permiso para el tráfico dentro de una red virtual. Para más información sobre los grupos de seguridad de red, consulte [este artículo](https://azure.microsoft.com/blog/network-security-groups/).
3. **Túnel forzado** : se trata de un tooredirect opción internet enlazado tráfico originado en Azure toobe redirigida sobre toohello de conexión de ExpressRoute de hello en el centro de datos local. Para más información acerca de Túnel forzado, consulte [este artículo](expressroute-routing.md#advertising-default-routes).  
4. **Cifrado** : aunque circuitos ExpressRoute de hello son tooa dedicado específicas del cliente, no hay posibilidad de Hola que Hola proveedor de red podría superarse, permitiendo el tráfico de paquetes de tooexamine un intruso. Esta posibilidad, un cliente o CSP puede cifrar el tráfico a través de tooaddress Hola conexión mediante la definición de las directivas de modo de túnel de IPSec para todo el tráfico que fluye entre hello en recursos locales y recursos de Azure (consulte toohello modo opcional de túnel IPSec para el cliente 1 en la figura 5: seguridad de ExpressRoute, más arriba). segunda opción de Hello sería toouse un dispositivo de firewall en cada extremo Hola de hello circuito de ExpressRoute. Esto requerirá parte 3ª adicional de firewall toobe de máquinas virtuales y los dispositivos instalado en el tráfico de hello tooencrypt de extremos a través del circuito de ExpressRoute de Hola.

![texto alternativo](./media/expressroute-for-cloud-solution-providers/expressroute-security.png)  

## <a name="next-steps"></a>Pasos siguientes
Hola servicio de proveedor de soluciones de nube proporciona una tooincrease de manera los clientes de tooyour valor sin Hola necesitan para compras de infraestructura y capacidad costosas, manteniendo su posición como proveedor de hello Subcontratando principal. Perfecta integración con Microsoft Azure puede realizarse a través de hello CSP API, lo que le toointegrate de administración de Microsoft Azure de los marcos de administración existente.  

Puede encontrar información adicional en hello siguientes vínculos:

[Programa Proveedor de soluciones en la nube de Microsoft](https://partner.microsoft.com/en-US/Solutions/cloud-reseller-overview).  
[Obtener lista tootransact como un proveedor de soluciones de nube](https://partner.microsoft.com/en-us/solutions/cloud-reseller-pre-launch).  
[Recursos de Proveedor de soluciones en la nube de Microsoft](https://partner.microsoft.com/en-us/solutions/cloud-reseller-resources).

