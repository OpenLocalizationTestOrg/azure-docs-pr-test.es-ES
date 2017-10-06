---
title: "una red Virtual para una caché en Redis de Azure Premium aaaConfigure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate y administrar la compatibilidad con red Virtual para las instancias de caché en Redis de Azure de nivel Premium"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 8b1e43a0-a70e-41e6-8994-0ac246d8bf7f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: sdanie
ms.openlocfilehash: fab715f4d9365ee4c2f8b89d2e2e58768c25b671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-virtual-network-support-for-a-premium-azure-redis-cache"></a>Cómo tooconfigure admite la red Virtual para una caché de Redis de Azure Premium
Caché en Redis de Azure tiene diferentes ofertas de caché, lo que proporciona flexibilidad en la elección de Hola de tamaño de caché y las características, incluidas las características de nivel Premium como de agrupación en clústeres, la persistencia y la compatibilidad de red virtual. Una red virtual es una red privada en la nube de Hola. Cuando una instancia de caché en Redis de Azure se configura con una red virtual, no es direccionable de forma pública y solo puede tener acceso desde máquinas virtuales y las aplicaciones dentro de hello red virtual. Este artículo describe cómo son compatibles con tooconfigure de red virtual para una instancia de caché en Redis de Azure premium.

> [!NOTE]
> Azure Redis Cache admite redes virtuales clásicas y de Resource Manager.
> 
> 

Para obtener información sobre otras características de caché premium, consulte [nivel Premium de caché de Redis de Azure de introducción toohello](cache-premium-tier-intro.md).

## <a name="why-vnet"></a>¿Por qué una red virtual?
[Red Virtual de Azure (VNet)](https://azure.microsoft.com/services/virtual-network/) implementación ofrece seguridad mejorada y aislamiento para la caché en Redis de Azure, así como las subredes, las directivas de control de acceso, y otra características toofurther restringir el acceso.

## <a name="virtual-network-support"></a>Compatibilidad con redes virtuales
Compatibilidad de red virtual está configurado en hello **nueva caché en Redis** hoja durante la creación de la memoria caché. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Una vez haya seleccionado un elevado nivel de precios, puede configurar la integración de red virtual Redis seleccionando una red virtual que se encuentra en hello misma suscripción y ubicación que la memoria caché. toouse una red virtual nueva, cree primero siguiendo los pasos de hello en [crear una red virtual con el portal de Azure hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) o [crear una red virtual (clásica) mediante el uso de hello portal de Azure](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) y, a continuación, devolver toohello **Nueva caché en Redis** toocreate hoja y configure la caché premium.

Hola tooconfigure red virtual para la caché de nuevo, haga clic en **red Virtual** en hello **nueva caché en Redis** hoja y seleccione Hola deseada red virtual de la lista desplegable de Hola.

![Red virtual][redis-cache-vnet]

Seleccione Hola subred deseada de hello **subred** lista desplegable lista y especificar Hola deseado **dirección IP estática**. Si usas un clásico Hola de red virtual **dirección IP estática** campo es opcional y si no se especifica ninguno, se elige una de la subred de hello seleccionado.

> [!IMPORTANT]
> Al implementar un tooa de caché en Redis de Azure Resource Manager VNet, caché Hola debe estar en una subred dedicada que no contiene ningún otro recurso excepto instancias de caché en Redis de Azure. Si se realiza un intento de toodeploy un tooa de caché en Redis de Azure Resource Manager VNet tooa subred que contiene otros recursos, la implementación de hello produce un error.
> 
> 

![Red virtual][redis-cache-vnet-ip]

> [!IMPORTANT]
> Azure reserva algunas direcciones IP dentro de cada subred y estas direcciones no se pueden usar. Hello primeros y últimas direcciones IP de subredes de hello están reservadas para la conformidad con el protocolo, junto con tres direcciones más utilizadas para los servicios de Azure. Para más información, consulte [¿Hay alguna restricción en el uso de direcciones IP dentro de estas subredes?](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)
> 
> En suma toohello direcciones IP que usa la infraestructura de red virtual de Azure hello, cada Redis instancia en la subred de direcciones IP hello usa dos por partición y una dirección IP adicional para el equilibrador de carga de Hola. Una memoria caché no clúster se considera toohave una partición.
> 
> 

Después de crea la memoria caché de hello, puede ver configuración Hola Hola red virtual haciendo clic en **red Virtual** de hello **menú recursos**.

![Red virtual][redis-cache-vnet-info]

tooconnect tooyour Redis de Azure, instancia de caché cuando se usa una red virtual, especifique el nombre de host de hello de la memoria caché en la cadena de conexión de hello tal y como se muestra en el siguiente ejemplo de Hola:

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5premium.redis.cache.windows.net,abortConnect=false,ssl=true,password=password");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

## <a name="azure-redis-cache-vnet-faq"></a>Preguntas frecuentes sobre la red virtual de Caché en Redis de Azure
Hola lista siguiente contiene toocommonly respuestas preguntas más frecuentes sobre la escala de hello Azure Redis Cache.

* [¿Cuáles son algunos de los problemas comunes de configuración incorrecta con Caché en Redis de Azure y las redes virtuales?](#what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets)
* [¿Cómo se puede comprobar que la memoria caché funciona una red virtual?](#how-can-i-verify-that-my-cache-is-working-in-a-vnet)
* [¿Se pueden usar redes virtuales con una memoria caché Basic o Estándar?](#can-i-use-vnets-with-a-standard-or-basic-cache)
* [¿Por qué se produce un error al crear una caché en Redis en algunas subredes, pero no en otras?](#why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others)
* [¿Cuáles son los requisitos de espacio de dirección de subred de hello?](#what-are-the-subnet-address-space-requirements)
* [¿Funcionarán todas las características al alojar una caché en una red virtual?](#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)

## <a name="what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets"></a>¿Cuáles son algunos de los problemas comunes de configuración incorrecta con Caché en Redis de Azure y las redes virtuales?
Cuando la caché en Redis de Azure se hospeda en una red virtual, se usan puertos Hola Hola las tablas siguientes. 

>[!IMPORTANT]
>Si se bloquean los puertos de hello en hello las tablas siguientes, caché hello no funcionen correctamente. Con uno o varios de estos puertos que están bloqueados es el problema más común de una configuración incorrecta de hello cuando se usa la caché en Redis de Azure en una red virtual.
> 
> 

- [Requisitos de puerto de salida](#outbound-port-requirements)
- [Requisitos de puerto de entrada](#inbound-port-requirements)

### <a name="outbound-port-requirements"></a>Requisitos de puerto de salida

Existen siete requisitos de puerto de salida.

- Si lo desea, todos los toohello de las conexiones salientes internet puede realizarse a través de un cliente auditoría el dispositivo local.
- Tres de los puertos de hello enrutan puntos de conexión de tráfico tooAzure servicio almacenamiento de Azure y DNS de Azure.
- Hola restantes intervalos de puertos y para la comunicación interna de subred de Redis. No es necesaria ninguna regla de NSG para las comunicaciones internas de la subred de Redis.

| Puertos | Dirección | Protocolo de transporte | Propósito | IP local | Dirección IP remota |
| --- | --- | --- | --- | --- | --- |
| 80, 443 |Salida |TCP |Dependencias de Redis en Almacenamiento de Azure/PKI (Internet) | (Subred de Redis) |* |
| 53 |Salida |TCP/UDP |Dependencias de Redis en DNS (Internet y red virtual) | (Subred de Redis) |* |
| 8443 |Salida |TCP |Comunicaciones internas en Redis | (Subred de Redis) | (Subred de Redis) |
| 10221-10231 |Salida |TCP |Comunicaciones internas en Redis | (Subred de Redis) | (Subred de Redis) |
| 20226 |Salida |TCP |Comunicaciones internas en Redis | (Subred de Redis) |(Subred de Redis) |
| 13000-13999 |Salida |TCP |Comunicaciones internas en Redis | (Subred de Redis) |(Subred de Redis) |
| 15000-15999 |Salida |TCP |Comunicaciones internas en Redis | (Subred de Redis) |(Subred de Redis) |


### <a name="inbound-port-requirements"></a>Requisitos de puerto de entrada

Existen ocho requisitos de intervalo de puertos de entrada. Las solicitudes entrantes en estos intervalos son entrante desde otros servicios hospedados en hello misma red virtual o interna toohello las comunicaciones de subred de Redis.

| Puertos | Dirección | Protocolo de transporte | Propósito | IP local | Dirección IP remota |
| --- | --- | --- | --- | --- | --- |
| 6379, 6380 |Entrada |TCP |TooRedis de comunicación de cliente, equilibrio de carga de Azure | (Subred de Redis) |Virtual Network, Azure Load Balancer |
| 8443 |Entrada |TCP |Comunicaciones internas en Redis | (Subred de Redis) |(Subred de Redis) |
| 8500 |Entrada |TCP/UDP |Equilibrio de carga de Azure | (Subred de Redis) |Azure Load Balancer |
| 10221-10231 |Entrada |TCP |Comunicaciones internas en Redis | (Subred de Redis) |(Subred de Redis), Azure Load Balancer |
| 13000-13999 |Entrada |TCP |TooRedis de comunicación de cliente clústeres de equilibrio de carga de Azure | (Subred de Redis) |Virtual Network, Azure Load Balancer |
| 15000-15999 |Entrada |TCP |Equilibrio de carga de clústeres, Azure de tooRedis de comunicación de cliente | (Subred de Redis) |Virtual Network, Azure Load Balancer |
| 16001 |Entrada |TCP/UDP |Equilibrio de carga de Azure | (Subred de Redis) |Azure Load Balancer |
| 20226 |Entrada |TCP |Comunicaciones internas en Redis | (Subred de Redis) |(Subred de Redis) |

### <a name="additional-vnet-network-connectivity-requirements"></a>Requisitos adicionales de conectividad de red virtual

Existen requisitos de conectividad de red para entornos para una Caché en Redis de Azure que no pueden cumplirse inicialmente en una red virtual. Caché en Redis de Azure requiere que todos Hola después elementos toofunction correctamente cuando se utiliza en una red virtual.

* Red saliente conectividad tooAzure extremos de almacenamiento en todo el mundo. Esto incluye los puntos de conexión que se encuentra en hello misma región que la instancia de caché en Redis de Azure de hello, así como los extremos de almacenamiento que se encuentra en **otros** regiones de Azure. Extremos de almacenamiento de Azure resolver en hello siguiendo los dominios DNS: *table.core.windows.net*, *blob.core.windows.net*, *queue.core.windows.net*y *file.core.windows.net*. 
* Salida conectividad de red demasiado*ocsp.msocsp.com*, *mscrl.microsoft.com*, y *crl.microsoft.com*. Esta conectividad es la funcionalidad SSL toosupport necesarios.
* configuración de DNS de Hola de red virtual de hello debe ser capaz de resolver todos los puntos de conexión de Hola y dominios que se menciona en Hola puntos anteriores. Estos requisitos de DNS pueden cumplirse asegurándose de una infraestructura DNS válida se configuran y se mantienen para la red virtual de Hola.
* Toohello de conectividad de red saliente después de extremos de supervisión de Azure, que resolver en hello siguiendo los dominios DNS: shoebox2 black.shoebox2.metrics.nsatc.net, Norte-prod2.prod2.metrics.nsatc.net, azglobal-black.azglobal.metrics.nsatc.net, shoebox2-red.shoebox2.metrics.nsatc.net, este-prod2.prod2.metrics.nsatc.net, azglobal-red.azglobal.metrics.nsatc.net.

### <a name="how-can-i-verify-that-my-cache-is-working-in-a-vnet"></a>¿Cómo se puede comprobar que la memoria caché funciona una red virtual?

>[!IMPORTANT]
>Cuando se conecta la instancia del servicio Azure Redis Cache tooan que se hospeda en una red virtual, la memoria caché los clientes deben estar en Hola misma red virtual, incluidas las aplicaciones de prueba o herramientas de diagnóstico de hacer ping.
>
>

Después de configuran los requisitos de puerto de hello tal y como se describe en la sección anterior de hello, puede comprobar que la memoria caché funciona mediante la realización de hello pasos.

- [Reiniciar](cache-administration.md#reboot) todos Hola nodos de caché. Si todos los de hello necesarios no se puede alcanzar las dependencias de caché (como se documenta en [requisitos del puerto de entrada](cache-how-to-premium-vnet.md#inbound-port-requirements) y [requisitos de puerto de salida](cache-how-to-premium-vnet.md#outbound-port-requirements)), caché hello no será capaz de toorestart correctamente.
- Una vez que los nodos de la memoria caché de hello reiniciar (como indica el estado de la caché de Hola Hola portal de Azure), puede realizar Hola siguientes pruebas:
  - hacer ping Hola extremo de la caché (mediante el puerto 6380) desde un equipo que esté dentro de hello misma red virtual como hello en caché, con [tcping](https://www.elifulkerson.com/projects/tcping.php). Por ejemplo:
    
    `tcping.exe contosocache.redis.cache.windows.net 6380`
    
    Si hello `tcping` herramienta notifica que Hola puerto está abierto, Hola caché está disponible para la conexión de los clientes en hello red virtual.

  - Tootest de otra manera es toocreate un cliente de caché de prueba (que podría ser una sencilla aplicación de consola mediante StackExchange.Redis) que se conecta toohello caché agrega y recupera algunos elementos de caché de Hola. Instalar la aplicación de cliente de ejemplo de Hola en una máquina virtual que se encuentra en Hola misma red virtual como memoria caché de Hola y ejecútelo en caché de tooverify conectividad toohello.


### <a name="can-i-use-vnets-with-a-standard-or-basic-cache"></a>¿Se pueden usar redes virtuales con una memoria caché Basic o Estándar?
Las redes virtuales solo se pueden usar con memorias caché Premium.

### <a name="why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others"></a>¿Por qué se produce un error al crear una caché en Redis en algunas subredes, pero no en otras?
Si va a implementar un tooa de caché en Redis de Azure Resource Manager VNet, caché Hola debe estar en una subred dedicada que no contenga ningún otro tipo de recurso. Si se realiza un intento de toodeploy se produce un error en una subred VNet el Administrador de recursos que contiene otros recursos, la implementación de Hola tooa de Azure Redis Cache. Debe eliminar los recursos existentes dentro de la subred de Hola Hola antes de poder crear una nueva caché de Redis.

Puede implementar varios tipos de recursos tooa clásico red virtual siempre que tengan suficiente IP direcciones disponibles.

### <a name="what-are-hello-subnet-address-space-requirements"></a>¿Cuáles son los requisitos de espacio de dirección de subred de hello?
Azure reserva algunas direcciones IP dentro de cada subred y estas direcciones no se pueden usar. Hello primeros y últimas direcciones IP de subredes de hello están reservadas para la conformidad con el protocolo, junto con tres direcciones más utilizadas para los servicios de Azure. Para más información, consulte [¿Hay alguna restricción en el uso de direcciones IP dentro de estas subredes?](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)

En suma toohello direcciones IP que usa la infraestructura de red virtual de Azure hello, cada Redis instancia en la subred de direcciones IP hello usa dos por partición y una dirección IP adicional para el equilibrador de carga de Hola. Una memoria caché no clúster se considera toohave una partición.

### <a name="do-all-cache-features-work-when-hosting-a-cache-in-a-vnet"></a>¿Funcionarán todas las características al alojar una caché en una red virtual?
Cuando la memoria caché forma parte de una red virtual, solo los clientes de hello red virtual pueden tener acceso a memoria caché de Hola. Como resultado, hello siguientes características de administración de memoria caché no funcionan en este momento.

* Consola de Redis: como consola de Redis se ejecuta en el explorador local, que se encuentra fuera de la red virtual de hello, no puede conectar tooyour caché.

## <a name="use-expressroute-with-azure-redis-cache"></a>Uso de ExpressRoute con Caché en Redis de Azure
Los clientes pueden conectarse un [ExpressRoute de Azure](https://azure.microsoft.com/services/expressroute/) infraestructura de red virtual de circuito tootheir, lo que extender su tooAzure de red local. 

De forma predeterminada, un circuito ExpressRoute recién creado no realiza la tunelización forzada (anuncio de una ruta predeterminada, 0.0.0.0/0) en una red virtual. Como resultado, se permite conectividad saliente de Internet directamente desde la red virtual de Hola y las aplicaciones cliente son tooother tooconnect capaz de Azure extremos incluidos caché en Redis de Azure.

Sin embargo, una configuración de cliente común es toouse tunelización forzada (anunciar una ruta predeterminada) lo que fuerza la salida Internet tráfico tooinstead flujo local. Este flujo de tráfico de conectividad con caché en Redis de Azure interrumpe si el tráfico de salida de hello es, a continuación, bloquea local que hello instancia de caché en Redis de Azure no sea capaz de toocommunicate con sus dependencias.

solución de Hello es toodefine uno (o más) definido por el usuario rutas (UDRs) en la subred Hola que contiene Hola caché en Redis de Azure. Un UDR define las rutas de subred específica que se respetará en lugar de la ruta predeterminada de Hola.

Si es posible, se recomienda hello toouse siguiente configuración:

* configuración de ExpressRoute de Hello anuncia 0.0.0.0/0 y de forma predeterminada force túneles todo el tráfico saliente en local.
* Hello UDR aplica toohello subred que contiene Hola caché en Redis de Azure define 0.0.0.0/0 con una ruta de trabajo para toohello de tráfico de TCP/IP internet pública; Por ejemplo por establecer Hola del próximo salto too'Internet de tipo '.

Hola efecto combinado de estos pasos es que el nivel de subred de hello UDR tiene precedencia sobre hello ExpressRoute forzado túnel, lo que garantiza el acceso a Internet saliente desde Hola caché en Redis de Azure.

Instancia de caché en Redis de Azure tooan conexión desde una aplicación local mediante ExpressRoute no es un escenario de uso típico debido a motivos de tooperformance (para obtener el mejor rendimiento de caché en Redis de Azure, los clientes deben estar en hello misma región que Hola caché en Redis de Azure).

>[!IMPORTANT] 
>Hola rutas definidas en un UDR **debe** ser lo suficientemente específica como tootake prioridad sobre las rutas anunciadas por la configuración de ExpressRoute de Hola. Hello en el ejemplo siguiente se usa el intervalo de direcciones de hello amplia 0.0.0.0/0 y por lo tanto puede potencialmente accidentalmente reemplazarse por anuncios de rutas con intervalos de direcciones más específicos.

>[!WARNING]  
>Caché en Redis de Azure no es compatible con configuraciones de ExpressRoute que **incorrectamente entre-anunciar rutas de hello pública emparejamiento toohello privada emparejamiento ruta de acceso**. Las configuraciones de ExpressRoute con el emparejamiento público configurado reciben anuncios de ruta de Microsoft para un amplio conjunto de intervalos de direcciones IP de Microsoft Azure. Si estos intervalos de direcciones se publicita entre incorrectamente en la ruta de intercambio de tráfico privado hello, resultado de hello es que todos los paquetes de red saliente de la subred de la instancia de caché en Redis de Azure de hello red de local del cliente tooa incorrectamente un túnel forzado infraestructura. Este flujo de red interrumpe Azure Redis Cache. problema de Hello solución toothis es toostop rutas de entre anuncios de Hola pública emparejamiento toohello privada emparejamiento ruta de acceso.


Se puede encontrar información de contexto sobre las rutas definidas por el usuario en esta [información general](../virtual-network/virtual-networks-udr-overview.md).

Para más información sobre ExpressRoute, consulte [Información técnica sobre ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="next-steps"></a>Pasos siguientes
Obtenga información acerca de cómo toouse premium más características de caché.

* [Nivel de introducción toohello Premium de caché de Redis de Azure](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-vnet]: ./media/cache-how-to-premium-vnet/redis-cache-vnet.png

[redis-cache-vnet-ip]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-ip.png

[redis-cache-vnet-info]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-info.png

