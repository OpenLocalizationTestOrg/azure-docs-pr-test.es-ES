---
title: requisitos de aaaRouting de ExpressRoute de Azure | Documentos de Microsoft
description: "En eta página se especifican los requisitos detallados para configurar y administrar el enrutamiento en los circuitos de ExpressRoute."
documentationcenter: na
services: expressroute
author: osamazia
manager: ganesr
editor: 
ms.assetid: 5b382e79-fa3f-495a-a764-c5ff86af66a2
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: osamam
ms.openlocfilehash: dd50009974ae1a7156c52d4f714d8d97075f13ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-routing-requirements"></a>Requisitos de enrutamiento de ExpressRoute
tooconnect tooMicrosoft servicios en la nube mediante ExpressRoute, podrá necesita tooset y administrar el enrutamiento. Algunos proveedores de conectividad ofrecen la configuración y administración de enrutamiento como un servicio administrado. Póngase en contacto con su toosee de proveedor de conectividad si ofrece este servicio. Si no lo hacen, deben cumplir toohello según los requisitos:

Consulte toohello [circuitos y dominios de enrutamiento](expressroute-circuit-peerings.md) artículo para obtener una descripción del enrutamiento de hello las sesiones que necesitan toobe configuran en toofacilitate conectividad.

> [!NOTE]
> Microsoft no admite protocolos de redundancia de enrutador (por ejemplo, HSRP o VRRP) en configuraciones de alta disponibilidad. Confiamos en un par redundante de sesiones BGP por configuración entre pares para la alta disponibilidad.
> 
> 

## <a name="ip-addresses-used-for-peerings"></a>Direcciones IP usadas para emparejamientos
Necesita tooreserve unos cuantos bloques de IP direcciones tooconfigure enrutamiento entre la red y enrutadores de borde (MSEEs) de empresa de Microsoft. Esta sección proporciona una lista de requisitos y describe las reglas de hello en cuanto a cómo se deben adquirir y utilizar estas direcciones IP.

### <a name="ip-addresses-used-for-azure-private-peering"></a>Direcciones IP usadas para la configuración entre pares privados de Azure
Puede usar direcciones IP privadas o públicas emparejamientos de Hola de tooconfigure de direcciones IP. intervalo de direcciones de Hello usado para configurar las rutas no debe solaparse con direcciones intervalos utilizados toocreate redes virtuales en Azure. 

* Debe reservar una subred /29 o dos subredes /30 para las interfaces de enrutamiento.
* pueden ser subredes Hola que se usan para el enrutamiento de direcciones IP privadas o las direcciones IP públicas.
* subredes de Hello no deben estar en conflicto con intervalo de hello reservado por el cliente de Hola para su uso en la nube de Microsoft de Hola.
* Si se usa una subred /29, se dividirá en dos /30 subredes. 
  * Hola primero/30 subred se usa para el vínculo principal de Hola y Hola /30 segunda subred se usa para el vínculo secundario Hola.
  * Para cada una de las subredes de hello /30, debe usar la primera dirección IP Hola de subred de hello /30 en el enrutador. Microsoft usa la segunda dirección IP Hola de hello /30 subred tooset una sesión de BGP.
  * Debe configurar las sesiones de BGP para nuestro [SLA de disponibilidad](https://azure.microsoft.com/support/legal/sla/) toobe válido.  

#### <a name="example-for-private-peering"></a>Ejemplo de configuración entre pares privados
Si elige toouse a.b.c.d/29 tooset de emparejamiento de hello, se dividirá en dos /30 subredes. En el ejemplo de Hola a continuación, veremos cómo se usa la subred de a.b.c.d/29 Hola. 

a.b.c.d/29 será división tooa.b.c.d/30 y a.b.c.d+4/30 y pasa por tooMicrosoft a través de hello las API de aprovisionamiento. Usarás a.b.c.d+1 Hola VRF IP para hello PE principal y Microsoft consumirá a.b.c.d+2 como Hola VRF IP para Hola MSEE principal. Usarás a.b.c.d+5 hello VRF IP para hello secundaria PE y Microsoft usará a.b.c.d+6 como Hola VRF IP para Hola MSEE secundaria.

Considere un caso donde seleccionar 192.168.100.128/29 tooset de intercambio de tráfico privado. 192.168.100.128/29 incluye direcciones de 192.168.100.128 too192.168.100.135, entre los que:

* 192.168.100.128/30 asignará toolink1, con el proveedor mediante 192.168.100.129 y Microsoft mediante 192.168.100.130.
* 192.168.100.132/30 asignará toolink2, con el proveedor mediante 192.168.100.133 y Microsoft mediante 192.168.100.134.

### <a name="ip-addresses-used-for-azure-public-and-microsoft-peering"></a>Direcciones IP usadas para la configuración de pares públicos de Azure y de Microsoft
Debe usar direcciones IP públicas perteneciente al usuario para configurar las sesiones BGP de Hola. Microsoft debe ser propiedad de hello tooverify capaz de direcciones IP de Hola a través de enrutamiento de los registros de Internet y registros de enrutamiento de Internet. 

* Debe usar un único/29 subred o dos /30 subredes tooset seguridad Hola BGP emparejamiento para cada emparejamiento por circuito de ExpressRoute (si tiene más de uno). 
* Si se usa una subred /29, se dividirá en dos /30 subredes. 
  * Hola primero/30 subred se usará para el vínculo principal de Hola y Hola /30 segunda subred se usa para el vínculo secundario Hola.
  * Para cada una de las subredes de hello /30, debe usar la primera dirección IP Hola de subred de hello /30 en el enrutador. Microsoft usa la segunda dirección IP Hola de hello /30 subred tooset una sesión de BGP.
  * Debe configurar las sesiones de BGP para nuestro [SLA de disponibilidad](https://azure.microsoft.com/support/legal/sla/) toobe válido.

## <a name="public-ip-address-requirement"></a>Requisitos de las direcciones IP públicas

### <a name="private-peering"></a>Emparejamiento privado
Puede elegir toouse las direcciones IPv4 públicas o privadas para el nivel privado. Proporcionamos un aislamiento completo del tráfico para que no sea posible que se solapen las direcciones con otros clientes en caso de un emparejamiento privado. Estas direcciones no son tooInternet anunciado. 


### <a name="public-peering"></a>Emparejamiento público
Hello Azure ruta de acceso de interconexión pública permite tooconnect tooall servicios hospedados en Azure a través de sus direcciones IP públicas. Se incluyen servicios enumerados en hello [ExpessRoute preguntas más frecuentes sobre](expressroute-faqs.md) y los servicios hospedados por ISV en Microsoft Azure. Servicios de conectividad tooMicrosoft Azure en público emparejamiento siempre se inicia desde la red en la red de Microsoft de Hola. Debe usar direcciones IP públicas para hello tráfico tooMicrosoft destino de red.

### <a name="microsoft-peering"></a>Emparejamiento de Microsoft
ruta de acceso de emparejamiento de Microsoft Hello le permite conectarse tooMicrosoft los servicios de nube que no se admiten a través de hello Azure ruta de acceso de interconexión pública. lista de Hello de servicios incluye servicios de Office 365, como Exchange Online, SharePoint Online, Skype empresarial y Dynamics 365. Microsoft admite una conectividad bidireccional en el emparejamiento de Microsoft de Hola. Servicios en la nube el tráfico destinado tooMicrosoft deben usar direcciones IPv4 públicas válidas antes de que entren en red de Microsoft de Hola.

Asegúrese de que la dirección IP y como número tooyou registrado en uno de hello siguientes está registros:

* [ARIN](https://www.arin.net/)
* [APNIC](https://www.apnic.net/)
* [AFRINIC](https://www.afrinic.net/)
* [LACNIC](http://www.lacnic.net/)
* [RIPENCC](https://www.ripe.net/)
* [RADB](http://www.radb.net/)
* [ALTDB](http://altdb.net/)

> [!IMPORTANT]
> Dirección IP pública direcciones anuncian tooMicrosoft a través de ExpressRoute no puede ser anunciado toohello Internet. Esto puede interrumpir los servicios de Microsoft tooother de conectividad. Sin embargo, las direcciones IP públicas utilizadas por los servidores de la red que se comunican con los puntos de conexión de Office 365 dentro de Microsoft pueden anunciarse en ExpressRoute. 
> 
> 

## <a name="dynamic-route-exchange"></a>Cambio de ruta dinámica
El cambio de enrutamiento se realizará sobre el protocolo eBGP. Se establecen sesiones de BGP entre MSEEs hello y los enrutadores. La autenticación de sesiones de BGP no es un requisito. Si es necesario, se puede configurar un hash MD5. Vea hello [configurar enrutamiento](expressroute-howto-routing-classic.md) y [Circuit flujos de trabajo de aprovisionamiento y Estados de circuito](expressroute-workflows.md) para obtener información acerca de cómo configurar las sesiones BGP.

## <a name="autonomous-system-numbers"></a>Números de sistema autónomo
Microsoft usará AS 12076 para la configuración entre pares públicos de Azure, privados de Azure y de Microsoft. Te hemos reservado ASN de 65515 too65520 para uso interno. Se admiten números AS de 16 y 32 bits.

No hay requisitos con respecto a la simetría de la transferencia de datos. rutas de acceso hacia delante y valor devuelto de Hello pueden atravesar pares de enrutador diferente. Las rutas idénticas deben anunciarse desde cualquiera de los lados en los distintos pares de circuito que le pertenezcan. Métricas de ruta no son necesario toobe idéntico.

## <a name="route-aggregation-and-prefix-limits"></a>Límites de agregación y prefijo de ruta
Se admiten hasta too4000 prefijos anuncian toous a través de hello Azure intercambio de tráfico privado. Esto puede aumentar la too10, 000 prefijos si está habilitado el complemento de hello ExpressRoute premium. Se aceptan prefijos de too200 por cada sesión de BGP pública de Azure e emparejamiento de Microsoft. 

sesión BGP Hola se quitará si número Hola de prefijos supera el límite de Hola. Aceptamos rutas predeterminadas en hello emparejamiento vínculo privado solo. Proveedor debe filtrar ruta predeterminada y direcciones IP privadas (RFC 1918) de hello pública de Azure y las rutas de acceso de emparejamiento de Microsoft. 

## <a name="transit-routing-and-cross-region-routing"></a>Enrutamiento de tránsito y enrutamiento entre regiones
ExpressRoute no puede configurarse como los enrutadores de tránsito. Tendrá toorely en el proveedor de conectividad de servicios de enrutamiento de tránsito.

## <a name="advertising-default-routes"></a>Anuncio de rutas predeterminadas
Las rutas predeterminadas solo se permiten en sesiones de configuración de pares privados de Azure. En tal caso, se enrutará todo el tráfico de red de tooyour de hello redes virtuales asociadas. Anunciar rutas predeterminadas en el intercambio de tráfico privado dará como resultado de ruta de acceso de internet de Hola de Azure está bloqueando. Debe confiar en el tráfico de tooroute contorno corporativo desde y toohello internet para los servicios hospedados en Azure. 

 tooenable conectividad tooother Azure servicios y los servicios de infraestructura, debe asegurarse de que uno de los siguientes elementos de hello es en su lugar:

* Pares públicos de Azure está habilitado tooroute tráfico toopublic extremos
* Utilice conectividad a internet tooallow enrutamiento definido por el usuario para cada conexión a Internet que necesite subred.

> [!NOTE]
> El anuncio de rutas predeterminadas interrumpirá la activación de la licencia de Windows y de otras máquinas virtuales. Siga las instrucciones [aquí](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx) toowork resolver este problema.
> 
> 

## <a name="bgp"></a>Soporte técnico para las comunidades de BGP
Esta sección proporciona información general de cómo se usarán las comunidades de BGP con ExpressRoute. Microsoft anunciará rutas hello pública y las rutas de acceso de emparejamiento de Microsoft con rutas etiquetadas con valores de la Comunidad adecuada. Hola motivo para hacerlo y Hola detalles en la Comunidad de valores se describen a continuación. Microsoft, sin embargo, no harán honor a cualquiera de las Comunidades valores etiquetados tooroutes anunciados tooMicrosoft.

Si va a conectar tooMicrosoft a través de ExpressRoute en cualquier ubicación de emparejamiento de uno dentro de una región geopolíticas, tendrán servicios de nube de Microsoft access tooall en todas las regiones dentro del límite de hello geopolíticos. 

Por ejemplo, si tooMicrosoft en Ámsterdam conectado a través de ExpressRoute, tendrá que Servicios de nube de Microsoft access tooall hospedados en Europa del Norte y Europa occidental. 

Consulte toohello [ExpressRoute asociados y las ubicaciones de emparejamiento](expressroute-locations.md) página para obtener una lista detallada de las regiones geopolíticas y regiones de Azure asociadas, ubicaciones de emparejamiento de ExpressRoute correspondiente.

Puede comprar más de un circuito ExpressRoute por región geopolítica. Tener varias conexiones ofrece ventajas significativas en la alta disponibilidad due toogeo redundancia. En situaciones en las que hay varios circuitos ExpressRoute, usted recibirá Hola que anuncia el mismo conjunto de prefijos de Microsoft en el emparejamiento público de Hola y rutas de acceso de emparejamiento de Microsoft. Esto significa que tendrá varias rutas de acceso desde su red a Microsoft. Esto puede producir potencialmente deficiente toobe decisiones enrutamiento realizada dentro de la red. Como resultado, puede experimentar conectividad deficiente experiencias toodifferent servicios. Puede basarse en hello Comunidad valores toomake adecuado enrutamiento decisiones toooffer [toousers enrutamiento óptimo](expressroute-optimize-routing.md).

| **Región de Microsoft Azure** | **Valor de comunidad de BGP** |
| --- | --- |
| **Norteamérica** | |
| Este de EE. UU. |12076:51004 |
| Este de EE. UU. 2 |12076:51005 |
| Oeste de EE. UU. |12076:51006 |
| Oeste de EE. UU. 2 |12076:51026 |
| Centro occidental de EE.UU. |12076:51027 |
| Centro-Norte de EE. UU |12076:51007 |
| Centro-Sur de EE. UU |12076:51008 |
| Central EE. UU.: |12076:51009 |
| Centro de Canadá |12076:51020 |
| Este de Canadá |12076:51021 |
| **Sudamérica** | |
| Sur de Brasil |12076:51014 |
| **Europa** | |
| Europa del Norte |12076:51003 |
| Europa occidental |12076:51002 |
| Sur del Reino Unido 2 | 12076:51024 |
| Oeste de Reino Unido | 12076:51025 |
| **Asia Pacífico** | |
| Asia oriental |12076:51010 |
| Sudeste asiático |12076:51011 |
| **Japón** | |
| Este de Japón |12076:51012 |
| Oeste de Japón |12076:51013 |
| **Australia** | |
| Australia Oriental |12076:51015 |
| Sudeste de Australia |12076:51016 |
| **India** | |
| Sur de India |12076:51019 |
| India occidental |12076:51018 |
| India central |12076:51017 |
| **Corea** | |
| Corea del Sur |12076:51028 |
| Corea Central |12076:51029 |

Todas las rutas anunciadas de Microsoft se etiqueta con el valor de la Comunidad adecuada de Hola. 

> [!IMPORTANT]
> Los prefijos globales se etiquetarán con un valor adecuado de comunidad y se anunciarán solo cuando esté habilitado el complemento premium de ExpressRoute.
> 
> 

Además toohello anterior, Microsoft se también etiquetar prefijos basados en servicio de Hola que pertenecen. Esto aplica solo toohello Microsoft emparejamiento. tabla de Hello siguiente proporciona una asignación del valor de comunidad de tooBGP de servicio.

| **Servicio** | **Valor de comunidad de BGP** |
| --- | --- |
| Exchange Online |12076:5010 |
| SharePoint Online |12076:5020 |
| Skype Empresarial Online |12076:5030 |
| Dynamics 365 |12076:5040 |
| Otros servicios en línea de Office 365 |12076:5100 |

> [!NOTE]
> Microsoft no admite los valores de la Comunidad BGP que establezca en hello las rutas anunciadas tooMicrosoft.
> 
> 

### <a name="bgp-community-support-in-national-clouds-preview"></a>Compatibilidad con la comunidad de BGP en nubes nacionales (versión preliminar)

| **Nubes nacionales Región de Azure**| **Valor de comunidad de BGP** |
| --- | --- |
| **Gobierno de Estados Unidos** |  |
| Gobierno de EE. UU.: Arizona | 12076:51106 |
| Gobierno de EE. UU. - Iowa | 12076:51109 |
| Gobierno de EE. UU. - Virginia | 12076:51105 |
| Gobierno de EE. UU.: Texas | 12076:51108 |
| Departamento de Defensa de EE. UU. Centro | 12076:51209 |
| Departamento de Defensa de EE. UU. Este | 12076:51205 |


| **Servicios en nubes nacionales** | **Valor de comunidad de BGP** |
| --- | --- |
| **Gobierno de Estados Unidos** |  |
| Exchange Online |12076:5110 |
| SharePoint Online |12076:5120 |
| Skype Empresarial Online |12076:5130 |
| Dynamics 365 |12076:5140 |
| Otros servicios en línea de Office 365 |12076:5200 |

## <a name="next-steps"></a>Pasos siguientes
* Configure su conexión ExpressRoute.
  
  * [Crear un circuito de ExpressRoute para el modelo de implementación clásica de hello](expressroute-howto-circuit-classic.md) o [crear y modificar un circuito de ExpressRoute con el Administrador de recursos de Azure](expressroute-howto-circuit-arm.md)
  * [Configurar el enrutamiento para el modelo de implementación clásica de hello](expressroute-howto-routing-classic.md) o [configurar el enrutamiento para el modelo de implementación del Administrador de recursos de Hola](expressroute-howto-routing-arm.md)
  * [Vincular un tooan de red virtual clásica circuito de ExpressRoute](expressroute-howto-linkvnet-classic.md) o [vincular un circuito de ExpressRoute de tooan de VNet el Administrador de recursos](expressroute-howto-linkvnet-arm.md)

