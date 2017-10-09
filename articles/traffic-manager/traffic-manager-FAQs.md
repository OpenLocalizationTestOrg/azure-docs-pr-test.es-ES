---
title: "aaaAzure Traffic Manager - preguntas más frecuentes | Documentos de Microsoft"
description: "Este artículo ofrecen respuestas toofrequently preguntas más frecuentes acerca del Administrador de tráfico"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 75d5ff9a-f4b9-4b05-af32-700e7bdfea5a
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: kumud
ms.openlocfilehash: 5530d03b55bbf49a52002841e281e2cf5819c2b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-frequently-asked-questions-faq"></a>Preguntas más frecuentes (P+F) sobre Traffic Manager

## <a name="traffic-manager-basics"></a>Introducción a Traffic Manager

### <a name="what-ip-address-does-traffic-manager-use"></a>¿Qué dirección IP usa el Administrador de tráfico?

Como se explica en [cómo Traffic Manager funciona](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), Traffic Manager funciona en hello nivel de DNS. Envía las respuestas DNS servicio adecuado de toodirect clientes toohello punto de conexión. Los clientes, a continuación, conectarse toohello extremo de servicio directamente, no a través del Administrador de tráfico.

Por lo tanto, Traffic Manager no proporciona un punto de conexión o la dirección IP para los clientes tooconnect a. Por lo tanto, si desea una dirección IP estática para el servicio, que debe configurarse en el servicio de hello, no en el Administrador de tráfico.

### <a name="does-traffic-manager-support-sticky-sessions"></a>¿Admite Traffic Manager sesiones temporales?

Como se explica en [cómo Traffic Manager funciona](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), Traffic Manager funciona en hello nivel de DNS. Utiliza el punto de conexión DNS respuestas toodirect clientes toohello servicio adecuado. Los clientes conectarse toohello extremo de servicio directamente, no a través del Administrador de tráfico. Por lo tanto, el Administrador de tráfico no ve tráfico Hola HTTP entre el cliente de Hola y el servidor de Hola.

Además, dirección IP de origen Hola de consulta DNS de hello recibido por el Administrador de tráfico pertenece toohello recursiva servicio DNS, no el cliente de Hola. Por lo tanto, Traffic Manager no tiene manera tootrack individuales clientes y no puede implementar 'rápidas' sesiones. Esta limitación es el tráfico DNS según tooall comunes sistemas de administración y no es específico tooTraffic Manager.

### <a name="why-am-i-seeing-an-http-error-when-using-traffic-manager"></a>¿Por qué obtengo un error HTTP al utilizar Traffic Manager?

Como se explica en [cómo Traffic Manager funciona](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), Traffic Manager funciona en hello nivel de DNS. Utiliza el punto de conexión DNS respuestas toodirect clientes toohello servicio adecuado. Los clientes, a continuación, conectarse toohello extremo de servicio directamente, no a través del Administrador de tráfico. Traffic Manager no ve el tráfico HTTP que circula entre cliente y servidor. Por tanto, todos los errores HTTP que obtenga deben provenir de la aplicación. Para la aplicación hello cliente tooconnect toohello todos los pasos de resolución DNS están completos. Esto incluye ninguna interacción del Administrador de tráfico en el flujo de tráfico de aplicación Hola.

Investigación adicional, por tanto, debe centrarse en la aplicación hello.

encabezado de host de Hello HTTP enviado desde el explorador del cliente de hello es origen más común de Hola de problemas. Asegúrese de que aplicación hello es el encabezado de host correcto tooaccept configurado Hola Hola nombre de dominio que usa. Para los extremos que usan hello servicio de aplicaciones de Azure, consulte [configurar un nombre de dominio personalizado para una aplicación web en el servicio de aplicación de Azure con Traffic Manager](../app-service-web/web-sites-traffic-manager-custom-domain-name.md).

### <a name="what-is-hello-performance-impact-of-using-traffic-manager"></a>¿Cuál es el impacto de rendimiento de hello del uso de Traffic Manager?

Como se explica en [cómo Traffic Manager funciona](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), Traffic Manager funciona en hello nivel de DNS. Puesto que los clientes conectan directamente a los extremos de servicio de tooyour, no hay ningún impacto en el rendimiento que se produce cuando se usa Traffic Manager una vez establecida la conexión de Hola.

Dado que Traffic Manager se integra con aplicaciones de nivel de DNS de hello, que requiere una toobe de búsqueda DNS adicional insertada Hola cadena de resolución DNS. impacto de Hola de Traffic Manager en el tiempo de resolución DNS es mínimo. Traffic Manager usa una red global de servidores de nombres y utiliza [difusión por proximidad](https://en.wikipedia.org/wiki/Anycast) las consultas DNS de red tooensure siempre son toohello enrutado servidor de nombre disponible más cercano. Además, el almacenamiento en caché de las respuestas DNS significa que latencia Hola DNS adicional que se incurre con el Administrador de tráfico aplica únicamente a tooa parte de las sesiones.

rutas de método de rendimiento de Hello tráfico toohello de extremo disponible más cercano. Hello resultado neto es que hello impacto en el rendimiento general asociado a este método debería ser mínimo. Algún aumento en la latencia de DNS se debe desplazar por extremo inferior de la toohello de latencia de red.

### <a name="what-application-protocols-can-i-use-with-traffic-manager"></a>¿Qué protocolos de aplicación puedo usar con el Administrador de tráfico?

Como se explica en [cómo Traffic Manager funciona](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), Traffic Manager funciona en hello nivel de DNS. Una vez completada la búsqueda DNS de hello, los clientes conectarse toohello extremo de la aplicación directamente, no a través del Administrador de tráfico. Por lo tanto, conexión Hola puede usar cualquier protocolo de aplicación. Si se selecciona TCP como Hola supervisión, el Administrador de tráfico del protocolo se puede realizar el seguimiento de estado de punto de conexión sin usando cualquier protocolo de aplicación. Si decide que el mantenimiento de hello toohave verificado mediante un protocolo de aplicación, el punto de conexión de hello necesita toobe toorespond capaz de tooeither HTTP o HTTPS GET solicitudes.

### <a name="can-i-use-traffic-manager-with-a-naked-domain-name"></a>¿Puedo usar Traffic Manager con un nombre de dominio desnudo?

No. estándares DNS de Hello no permiten CNAME tooco-existe con otros registros DNS de hello el mismo nombre. vértice Hello (o raíz) de una zona DNS siempre contiene dos registros DNS existentes; Hola hello y SOA autoritativos registros NS. Esto significa que no se puede crear un registro CNAME en vértice de la zona de hello sin infringir los estándares DNS Hola.

El Administrador de tráfico requiere un nombre DNS de personal de CNAME DNS toomap registros Hola. Por ejemplo, asignar www.contoso.com toohello Traffic Manager perfil DNS nombre contoso.trafficmanager.net. Además, Hola perfil de Traffic Manager devuelve un segundo tooindicate de CNAME DNS qué extremo Hola cliente debe conectarse.

toowork resolver este problema, se recomienda utilizar un tráfico de toodirect de redirección HTTP de hello naked dominio nombre tooa otra dirección URL, que, a continuación, se puede utilizar el Administrador de tráfico. Por ejemplo, hello dominio naked 'contoso.com' puede redirigir a los usuarios toohello CNAME 'www.contoso.com' que apunta toohello nombre DNS de Traffic Manager.

En nuestra cola de trabajos pendientes de características realizamos un seguimiento de los dominios vacíos que son totalmente compatibles con el Administrador de tráfico. Puede dar su apoyo a esta solicitud de característica [votando por ella en nuestro sitio de comentarios de la comunidad](https://feedback.azure.com/forums/217313-networking/suggestions/5485350-support-apex-naked-domains-more-seamlessly).

### <a name="does-traffic-manager-consider-hello-client-subnet-address-when-handling-dns-queries"></a>¿Traffic Manager considere la posibilidad de dirección de subred de cliente hello cuando se administran las consultas DNS? 
No, actualmente Traffic Manager tiene en cuenta solo Hola dirección IP de origen de consulta DNS Hola recibe, que es normalmente la dirección IP de Hola de resolución DNS de hello, al realizar búsquedas para los métodos de enrutamiento geográfico y el rendimiento.  
En concreto, [7871 RFC – subred del cliente en las consultas DNS](https://tools.ietf.org/html/rfc7871) que proporciona un [mecanismo de extensión para DNS (EDNS0)](https://tools.ietf.org/html/rfc2671) que puede pasar en la dirección de subred de cliente de Hola de resoluciones que admiten servidores de tooDNS es no admite actualmente en el Administrador de tráfico. Puede dar su apoyo a esta solicitud de característica a través del [sitio de comentarios de la comunidad](https://feedback.azure.com/forums/217313-networking).


### <a name="what-is-dns-ttl-and-how-does-it-impact-my-users"></a>¿Qué es el TTL de DNS y cómo afecta a mis usuarios?

Cuando una consulta DNS aterriza en Traffic Manager, establece un valor en respuesta Hola llamado time-to-live (TTL). Este valor, cuya unidad es en segundos, indica a tooDNS resoluciones en un nivel inferior en el tiempo toocache esta respuesta. Mientras no se garantiza que las resoluciones DNS toocache este resultado, el almacenamiento en caché se les permite toorespond tooany las consultas posteriores desactivar la memoria caché de hello en lugar de pasar los servidores DNS del Administrador de tooTraffic. Esto afecta a las respuestas de hello como sigue:
- un TTL más alto reduce el número de Hola de consultas que llegará a Hola servidores DNS de Traffic Manager, lo que pueden reducir el costo de Hola para un cliente ya que el número de consultas que se atienden es un uso facturable.
- un valor de TTL más alto puede reducir potencialmente Hola tarda toodo una búsqueda de DNS.
- un valor de TTL más alto también significa que los datos no reflejan la información más reciente sobre Hola mantenimiento que Traffic Manager ha obtenido a través de los agentes de búsqueda.

### <a name="how-high-or-low-can-i-set-hello-ttl-for-traffic-manager-responses"></a>¿Cómo alta o baja puedo establecer Hola TTL para las respuestas de Traffic Manager?

Puede establecer, en un nivel por perfil, Hola toobe TTL de DNS como mínimo es 0 segundos y tan alto como 2.147.483.647 segundos (Hola máximo del intervalo compatible con [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt )). Un valor de TTL de 0 significa que siguen en la cadena solucionadores DNS no almacenan en caché las respuestas de consulta y todas las consultas son espera servidores DNS del Administrador de tráfico de hello tooreach para la resolución.

## <a name="traffic-manager-geographic-traffic-routing-method"></a>Método de enrutamiento del tráfico geográfico de Traffic Manager

### <a name="what-are-some-use-cases-where-geographic-routing-is-useful"></a>¿En qué casos de uso el enrutamiento geográfico resulta útil? 
Tipo de enrutamiento geográfico puede usarse en cualquier escenario donde un cliente de Azure necesita toodistinguish a sus usuarios en función de las regiones geográficas. Por ejemplo, mediante el método de enrutamiento de tráfico geográfica hello, puede proporcionar a los usuarios en determinadas regiones una experiencia de usuario diferente que los de otras regiones. Otro ejemplo es cumplir los mandatos de soberanía de datos locales que requieren que los usuarios de una región específica sean atendidos solo por puntos de conexión de dicha región.

### <a name="what-are-hello-regions-that-are-supported-by-traffic-manager-for-geographic-routing"></a>¿Qué regiones de Hola que son compatibles con el Administrador de tráfico para el enrutamiento geográfica? 
jerarquía de país o región de Hola que será utilizado por el Administrador de tráfico puede encontrarse [aquí](traffic-manager-geographic-regions.md). Aunque esta página se mantiene actualizada con los cambios, puede recuperar mediante programación Hola la misma información mediante el uso de hello [API de REST de Azure Traffic Manager](https://docs.microsoft.com/rest/api/trafficmanager/). 

### <a name="how-does-traffic-manager-determine-where-a-user-is-querying-from"></a>¿Cómo determina Traffic Manager desde dónde consulta un usuario? 
Traffic Manager busca en la dirección IP de origen de Hola de consulta de hello (Esto es más probable es que una resolución DNS local haciendo Hola consultar en nombre de usuario de hello) y utiliza una ubicación de hello toodetermine interna del mapa de tooregion IP. Esta asignación se actualiza en un tooaccount constantemente cambios en hello internet. 

### <a name="is-it-guaranteed-that-traffic-manager-can-correctly-determine-hello-exact-geographic-location-of-hello-user-in-every-case"></a>¿Se garantiza que Traffic Manager correctamente puede determinar la ubicación geográfica exacta de Hola de usuario de hello en todos los casos?
No, Traffic Manager no puede garantizar esa región geográfica Hola se infiere de dirección IP de origen Hola de una consulta DNS siempre corresponderá ubicación del usuario toohello debido toohello siguientes motivos: 

- En primer lugar, como se describe en preguntas más frecuentes de hello anterior, Hola vemos es el de una resolución DNS realizando la búsqueda de hello en nombre de usuario de Hola de dirección IP de origen. Mientras la ubicación geográfica de Hola de resolución DNS de hello es un buen proxy para ubicación geográfica de saludo del usuario de hello, también puede ser diferente dependiendo de consumo de hello del servicio de resolución DNS de Hola y Hola específico servicio de resolución DNS que ha elegido un cliente toouse. Por ejemplo, un cliente que se encuentra en Malasia podría especificar en uso de la configuración de su dispositivo seleccionado de un servicio de resolución DNS podría obtener cuyo servidor DNS en Singapur toohandle resoluciones de consulta de Hola para ese usuario o dispositivo. En que el caso, el Administrador de tráfico solo puede ver IP Hola la resolución de direcciones corresponde toohello ubicación Singapur. Consulte también Hola anteriores preguntas más frecuentes con respecto a la dirección de subred de cliente se admiten en esta página.

- En segundo lugar, el Administrador de tráfico usa una asignación interna toodo hello toogeographic región traducción de direcciones IP. Mientras se valida y se actualiza esta asignación en una tooincrease continuamente su precisión y la cuenta de hello evolucionando la naturaleza de Hola internet, todavía hay posibilidad de Hola que nuestra información no es una representación exacta de la ubicación geográfica de Hola de todos los direcciones IP de Hola.


###  <a name="does-an-endpoint-need-toobe-physically-located-in-hello-same-region-as-hello-one-it-is-configured-with-for-geographic-routing"></a>¿Una toobe de necesidad de punto de conexión ubicado físicamente en Hola misma región que Hola uno que está configurado con para enrutamiento geográfica? 
No, ubicación de Hola de punto de conexión de hello impone ninguna restricción en la que regiones pueden estar asignada tooit. Por ejemplo, un punto de conexión en la región de centro de EE. UU. Azure puede tener todos los usuarios de la India dirige tooit.

### <a name="can-i-assign-geographic-regions-tooendpoints-in-a-profile-that-is-not-configured-toodo-geographic-routing"></a>¿Se puede asignar la región geográfica tooendpoints en un perfil que no está configurado toodo geográfica enrutamiento? 

Sí, si el método de enrutamiento de Hola de un perfil no es geográfico, puede usar hello [API de REST de Azure Traffic Manager](https://docs.microsoft.com/rest/api/trafficmanager/) tooassign tooendpoints de las regiones geográficas en ese perfil. En caso de hello de perfiles de tipo de enrutamiento no geográficos, se omite esta configuración. Si cambia este perfil toogeographic enrutamiento tipo en un momento posterior, Traffic Manager puede usar esas asignaciones.


### <a name="why-am-i-getting-an-error-when-i-try-toochange-hello-routing-method-of-an-existing-profile-toogeographic"></a>¿Por qué recibo un error cuando intento método de enrutamiento de hello toochange de un tooGeographic de perfil existente?

Todos los extremos de hello en un perfil con el enrutamiento geográfico necesitan toohave al menos una región asignada tooit. tooconvert un tipo de enrutamiento de toogeographic de perfil existente, primero debe tooassociate las regiones geográficas tooall sus puntos de conexión con hello [API de REST de Azure Traffic Manager](https://docs.microsoft.com/rest/api/trafficmanager/) antes de cambiar Hola enrutamiento escriba toogeographic. Si mediante el portal, eliminar los puntos de conexión de hello, cambiar método de enrutamiento de Hola de hello toogeographic de perfil y, a continuación, agregar extremos de hello junto con su asignación de región geográfica. 


###  <a name="why-is-it-strongly-recommended-that-customers-create-nested-profiles-instead-of-endpoints-under-a-profile-with-geographic-routing-enabled"></a>¿Por qué se recomienda encarecidamente que los clientes creen perfiles anidados en lugar de puntos de conexión en un perfil con el enrutamiento geográfico habilitado? 

Una región puede asignarse tooonly un punto de conexión dentro de un perfil si su utilizando el tipo de enrutamiento geográfico. Si ese punto de conexión no es un tipo anidado con una tooit de perfil conectado secundarios, si ese extremo va mal, Traffic Manager continúa toosend tráfico tooit desde alternativa Hola de no enviar que todo el tráfico no es mejor. El Administrador de tráfico no no extremo tooanother de conmutación por error, incluso cuando región Hola asignada es "principal" de región de hello asignado extremo toohello que fue incorrecto (por ejemplo, si un punto de conexión que tiene la región España va mal, que haremos tooanother de conmutación por error no punto de conexión que tiene Hola región Europa asignado tooit). Esto se hace tooensure que la configuración de Traffic Manager aspectos Hola fronteras geográficas que un cliente tiene en su perfil. beneficio de hello tooget de tooanother el punto de conexión cuando sale mal un punto de conexión de la conmutación por error, se recomienda que las regiones geográficas asignarse toonested perfiles con varios puntos de conexión dentro de ella en lugar de extremos individuales. De este modo, si un punto de conexión Hola anidado secundarios perfil se produce un error, el tráfico posible punto de conexión de conmutación por error tooanother dentro de hello mismo anidar perfil secundario.

### <a name="are-there-any-restrictions-on-hello-api-version-that-supports-this-routing-type"></a>¿Existen restricciones en la versión de Hola API que admite este tipo de enrutamiento?

Sí, pero solo versión de API de 2017-03-01 y admite más reciente Hola geográfica tipo de enrutamiento. Las versiones anteriores de API no pueden ser toocreated usa perfiles del tipo de enrutamiento geográfico o asignar tooendpoints de las regiones geográficas. Si una versión anterior de la API es tooretrieve usa los perfiles de una suscripción de Azure, no se devuelve ningún perfil de tipo de enrutamiento geográfico. Además, al usar las versiones anteriores de la API, cualquier perfil devuelto que tenga puntos de conexión con una asignación de región geográfica no muestra su asignación de región geográfica.



## <a name="traffic-manager-endpoints"></a>Puntos de conexión del Administrador de tráfico

### <a name="can-i-use-traffic-manager-with-endpoints-from-multiple-subscriptions"></a>¿Puedo usar el Administrador de tráfico con puntos de conexión de varias suscripciones?

No se pueden usar puntos de conexión de varias suscripciones con Azure Web Apps. Azure Web Apps requiere que cualquier nombre de dominio personalizado usado con Web Apps se use únicamente en una suscripción. No es posible toouse las aplicaciones Web desde varias suscripciones con hello mismo nombre de dominio.

Para otros tipos de punto de conexión, es posible toouse Traffic Manager con puntos de conexión de más de una suscripción. En el Administrador de recursos, los puntos de conexión de cualquier suscripción pueden agregarse tooTraffic Manager, como persona Hola configuración de perfil de Traffic Manager de hello tiene el punto de conexión de acceso de lectura toohello. Estos permisos pueden concederse mediante la funcionalidad de [control de acceso basado en rol (RBAC) de Azure Resource Manager](../active-directory/role-based-access-control-configure.md).


### <a name="can-i-use-traffic-manager-with-cloud-service-staging-slots"></a>¿Puedo usar Traffic Manager con espacios de ensayo de servicio en la nube?

Sí. Los espacios de ensayo de servicio en la nube se pueden configurar en Traffic Manager como puntos de conexión externos. Comprobaciones de mantenimiento todavía se cobrará a velocidad de hello extremos de Azure. Porque Hola tipo de extremo externo está en uso, servicio de cambios toohello subyacente no se recogen automáticamente. Con extremos externos, Traffic Manager no puede detectar cuándo Hola servicio en la nube se detiene o elimina. Por lo tanto, Hola Traffic Manager continúa facturación para las comprobaciones de mantenimiento hasta que el punto de conexión de hello esté deshabilitado o eliminado.

### <a name="does-traffic-manager-support-ipv6-endpoints"></a>¿Admite el Administrador de tráfico puntos de conexión IPv6?

Traffic Manager no proporciona actualmente servidores de nombres que admitan direcciones IPv6. Sin embargo, todavía puede utilizarse Traffic Manager por clientes de IPv6 que se conectan a puntos de conexión de tooIPv6. No hace que un cliente DNS solicita directamente tooTraffic Manager. En su lugar, cliente hello usa un servicio DNS recursivas. Un cliente de solo IPv6 envía solicitudes de servicio DNS recursivas toohello a través de IPv6. A continuación, el servicio de recursiva de Hola debe ser servidores de nombres de Traffic Manager pueda toocontact Hola con IPv4.

Administrador de tráfico responde con el nombre DNS de Hola de punto de conexión de Hola. punto de conexión de toosupport IPv6, AAAA de DNS registrar señalador toohello de nombre DNS de hello extremo IPv6 dirección debe existir. Las comprobaciones de estado de Traffic Manager solo admiten direcciones IPv4. servicio Hello necesita extremo tooexpose IPv4 en hello mismo nombre DNS.

### <a name="can-i-use-traffic-manager-with-more-than-one-web-app-in-hello-same-region"></a>¿Puedo usar Traffic Manager con más de una aplicación Web en hello misma región?

Traffic Manager suele ser usado toodirect tráfico tooapplications implementado en regiones diferentes. Sin embargo, también se puede utilizar en una aplicación tiene más de una implementación en hello misma región. Hello extremos de Azure Traffic Manager no permite más de un extremo de aplicación Web de hello mismo toobe de región de Azure agrega toohello mismo perfil de Traffic Manager.

##  <a name="traffic-manager-endpoint-monitoring"></a>Supervisión de puntos de conexión de Traffic Manager

### <a name="is-traffic-manager-resilient-tooazure-region-failures"></a>¿Es Traffic Manager resistente tooAzure errores de región?

Traffic Manager es un componente clave de entrega de Hola de aplicaciones de alta disponibilidad en Azure.
toodeliver alta disponibilidad, el Administrador de tráfico debe tener un excepcionalmente alto nivel de disponibilidad y ser resistentes tooregional error.

De forma predeterminada, los componentes de Traffic Manager son resistentes tooa error completo de cualquier región de Azure. Esta resistencia aplica a los componentes de Traffic Manager tooall: servidores de nombres DNS de hello, API de hello, capa de almacenamiento de Hola y servicio de supervisión de extremos de Hola.

En el caso poco probable de Hola de una interrupción de toda una región de Azure, Traffic Manager suele ser toofunction toocontinue esperado. Las aplicaciones implementadas en varias regiones de Azure pueden basarse en la instancia disponible tooan de Traffic Manager toodirect tráfico de su aplicación.

### <a name="how-does-hello-choice-of-resource-group-location-affect-traffic-manager"></a>¿Cómo afecta elección Hola de ubicación del grupo de recursos Traffic Manager?

El Administrador de tráfico es servicio global individual. No es regional. elección de Hola de ubicación del grupo de recursos no hace ningún perfil de administrador de tooTraffic diferencia implementado en ese grupo de recursos.

Administrador de recursos de Azure requiere que todos los recursos grupos toospecify una ubicación, lo que determina la ubicación predeterminada de Hola para recursos implementados en ese grupo de recursos. Cuando se crea un perfil de Traffic Manager, se crea en un grupo de recursos. Todos los perfiles de Traffic Manager usar **global** como su ubicación, invalida Hola configuración predeterminada del grupo de recursos.

### <a name="how-do-i-determine-hello-current-health-of-each-endpoint"></a>¿Cómo se determina el estado actual de Hola de cada punto de conexión?

Hola supervisar el estado de cada punto de conexión actual, en suma toohello perfil general, se muestra en hello portal de Azure. Esta información también está disponible a través de control del tráfico de Hola [API de REST](https://msdn.microsoft.com/library/azure/mt163667.aspx), [cmdlets de PowerShell](https://msdn.microsoft.com/library/mt125941.aspx), y [multiplataforma Azure CLI](../cli-install-nodejs.md).

Azure no proporciona información histórica sobre el punto de conexión anterior Hola o mantenimiento de alertas de tooraise de capacidad sobre el estado de tooendpoint de cambios.

### <a name="can-i-monitor-https-endpoints"></a>¿Puedo supervisar puntos de conexión HTTPS?

Sí. El Administrador de tráfico admite el sondeo a través de HTTPS. Configurar **HTTPS** como protocolo de hello en configuración de supervisión de Hola.

Traffic Manager no puede proporcionar ninguna validación de certificado, incluidos:

* No se validan certificados del servidor
* No se admiten certificados del servidor de SNI
* No se admiten certificados de cliente

### <a name="can-i-use-traffic-manager-even-if-my-application-does-not-have-support-for-http-or-https"></a>¿Puedo usar Traffic Manager incluso si mi aplicación no tiene compatibilidad para HTTP o HTTPS?

Sí. Puede especificar TCP que puede iniciar una conexión TCP y esperar una respuesta desde el punto de conexión de Hola Hola protocolo y el Administrador de tráfico de supervisión. Si el punto de conexión de hello responde toohello solicitud de conexión con una conexión de hello tooestablish de respuesta, en tiempo de espera de hello período, a continuación, en ese punto de conexión se marca con un estado correcto.

### <a name="what-specific-responses-are-required-from-hello-endpoint-when-using-tcp-monitoring"></a>¿Qué respuestas específicas son necesarias desde el punto de conexión de hello cuando se usa TCP supervisión?

Cuando se usa la supervisión de TCP, se inicia el Administrador de tráfico un protocolo de enlace TCP de tres vías enviando un SYN solicitar tooendpoint en Hola puerto especificado. A continuación, espera durante un período de tiempo (según lo especificado en la configuración de tiempo de espera de hello) para una respuesta desde el punto de conexión de Hola. Si responde de punto de conexión de hello toohello SYN solicitud con una respuesta SYN ACK en período de tiempo de espera de hello especificado en configuración de supervisión de hello, ese punto de conexión se considera correcta. Si no se recibe respuesta SYN ACK hello, Hola Traffic Manager restablece conexión Hola responde con un RST.

### <a name="how-fast-does-traffic-manager-move-my-users-away-from-an-unhealthy-endpoint"></a>¿Con qué rapidez Traffic Manager mueve mis usuarios de un punto de conexión incorrecto?

Traffic Manager proporciona varias opciones de configuración que le permitirá comportamiento de conmutación por error de hello toocontrol de su perfil de Traffic Manager como se indica a continuación:
- puede especificar que Hola Traffic Manager sondeos Hola extremos con más frecuencia estableciendo Hola intervalo de sondeo en 10 segundos. Esto garantiza que cualquier punto de conexión que vaya a ser incorrecto se detecte lo antes posible. 
- puede especificar cuánto tiempo de espera toowait antes de una solicitud de comprobación de mantenimiento (valor de tiempo de espera mínimo es 5 s).
- puede especificar cuántos errores pueden producir antes de que el punto de conexión de hello está marcado como incorrecto. Este valor puede ser mínimo es 0, en qué punto de conexión de hello mayúsculas se muestra como incorrecto en cuanto se produce un error Hola comprobación de mantenimiento del primero. Sin embargo, con valor mínimo de Hola de 0 para el número de hello tolerado de errores puede provocar tooendpoints que se interrumpa la rotación debido tooany problemas transitorios que pueden producirse en tiempo de presentación de sondeo.
- puede especificar Hola time-to-live (TTL) de hello toobe de respuesta DNS como mínimo es 0. Si lo hace, significa que las resoluciones DNS no pueden almacenar en caché respuesta hello y cada nueva consulta obtiene una respuesta que incorpora la información de estado más reciente de Hola que Hola Traffic Manager tiene.

Mediante estas opciones, Traffic Manager puede proporcionar las conmutaciones por error menos de 10 segundos después de un punto de conexión poner incorrecto y se realiza una consulta DNS frente a perfil de hello correspondiente.

### <a name="how-can-i-specify-different-monitoring-settings-for-different-endpoints-in-a-profile"></a>¿Cómo puedo especificar diferentes opciones de supervisión para los diferentes puntos de conexión de un perfil?

La configuración de supervisión de Traffic Manager se encuentra en el nivel de perfil. Si necesita toouse un valor diferente de supervisión para un solo punto de conexión, es posible debido a ese punto de conexión como un [anidados perfil](traffic-manager-nested-profiles.md) cuya configuración de supervisión es diferentes de perfil de hello primario.

### <a name="what-host-header-do-endpoint-health-checks-use"></a>¿Qué encabezado host se utiliza en las comprobaciones de estado de punto de conexión?

Traffic Manager usa encabezados de host en las comprobaciones de estado HTTP y HTTPS. encabezado de host de Hello utilizada por el Administrador de tráfico es nombre Hola de destino de punto de conexión de hello configurado en el perfil de Hola. no se puede especificar el valor de Hello utilizado en el encabezado de host de Hola por separado de propiedad de destino de Hola.

### <a name="what-are-hello-ip-addresses-from-which-hello-health-checks-originate"></a>¿Cuáles son las direcciones IP Hola desde el que el estado de hello comprueba se originan?

Hello lista siguiente contiene las direcciones IP Hola desde el que el estado de Traffic Manager comprueba pueden originarse. Puede usar este tooensure de lista que se permiten las conexiones entrantes de estas direcciones IP en hello extremos toocheck su estado de mantenimiento.

* 40.68.30.66
* 40.68.31.178
* 137.135.80.149
* 137.135.82.249
* 23.96.236.252
* 65.52.217.19
* 40.87.147.10
* 40.87.151.34
* 13.75.124.254
* 13.75.127.63
* 52.172.155.168
* 52.172.158.37
* 104.215.91.84
* 13.75.153.124
* 13.84.222.37
* 23.101.191.199
* 23.96.213.12
* 137.135.46.163
* 137.135.47.215
* 191.232.208.52
* 191.232.214.62
* 13.75.152.253
* 104.41.187.209
* 104.41.190.203

### <a name="how-many-health-checks-toomy-endpoint-can-i-expect-from-traffic-manager"></a>¿Punto de conexión del toomy de comprobaciones de mantenimiento cuántos puedo esperar de Traffic Manager?

número de Hola de mantenimiento de Traffic Manager comprueba alcanzar su punto de conexión depende de la siguiente Hola:
- Hola valor que haya establecido para el intervalo de supervisión de hello (intervalo menor significa más solicitudes de aterrizaje en el punto de conexión en cualquier período de tiempo determinado).
- número de Hola de ubicaciones desde donde hello las comprobaciones de mantenimiento originan (direcciones IP de Hola desde donde puede esperar estas comprobaciones se muestra en hello anterior preguntas más frecuentes).

## <a name="traffic-manager-nested-profiles"></a>Perfiles anidados de Traffic Manager

### <a name="how-do-i-configure-nested-profiles"></a>¿Cómo se configuran los perfiles anidados?

Perfiles del Administrador de tráfico anidados pueden configurarse con ambos hello Azure Resource Manager y Hola clásico API de REST de Azure, cmdlets de PowerShell de Azure y los comandos de CLI de Azure de multiplataforma. También se admiten a través del nuevo portal de Azure Hola. No se admiten en el portal clásico de Hola.

### <a name="how-many-layers-of-nesting-does-traffic-manger-support"></a>¿Cuántas capas de anidamiento admite el Administrador de tráfico?

Puede anidar perfiles de too10 niveles de profundidad. No se permiten "bucles".

### <a name="can-i-mix-other-endpoint-types-with-nested-child-profiles-in-hello-same-traffic-manager-profile"></a>¿Puedo combinar otros tipos de punto de conexión con perfiles secundarios anidados en Hola mismo perfil de Traffic Manager?

Sí. No hay ninguna restricción en el modo de combinar puntos de conexión de diferentes tipos dentro de un perfil.

### <a name="how-does-hello-billing-model-apply-for-nested-profiles"></a>¿Cómo se aplican el modelo de facturación de hello Nested perfiles de?

El uso de perfiles anidados no afecta de forma negativa a los precios.

La facturación de Traffic Manager tiene dos componentes: comprobaciones de estado del punto de conexión y millones de consultas DNS.

* Comprobaciones de estado del punto de conexión: cuando un perfil secundario se configura como punto de conexión de un perfil primario no se aplica ningún cargo. Supervisión de extremos de hello en el perfil de hello hijo se factura en hello forma habitual.
* Consultas de DNS: cada consulta se cuenta una sola vez. Una consulta en un perfil principal que devuelve un punto de conexión de un perfil secundario se cuenta contra Hola primario para el perfil únicamente.

Para obtener información detallada, vea hello [Traffic Manager página de precios](https://azure.microsoft.com/pricing/details/traffic-manager/).

### <a name="is-there-a-performance-impact-for-nested-profiles"></a>¿Se ve afectado el rendimiento por el uso de perfiles anidados?

No. No hay ningún efecto sobre el rendimiento derivado del uso de perfiles anidados.

servidores de nombres del Administrador de tráfico de Hello atraviesan jerarquía de perfil de hello internamente cuando se procesa cada consulta DNS. Un perfil DNS consulta tooa principal puede recibir una respuesta DNS con un punto de conexión de un perfil secundario. Se usará un único registro CNAME tanto si usa un solo perfil como si usa perfiles anidados. Un registro CNAME para cada perfil en la jerarquía de hello no hay ninguna necesidad de toocreate.

### <a name="how-does-traffic-manager-compute-hello-health-of-a-nested-endpoint-in-a-parent-profile"></a>¿Cómo Traffic Manager calcular estado de Hola de un punto de conexión anidada en un perfil principal?

perfil de Hello primario no realiza comprobaciones de estado secundario Hola directamente. En su lugar, estado de Hola de puntos de conexión del perfil de hello secundario son hello toocalculate usado el estado general del perfil de hello secundarios. Esta información se propaga el estado de Hola Hola anidado perfil jerarquía toodetermine de punto de conexión de hello anidado. perfil principal de Hola usa este toodetermine de mantenimiento agregado independientemente de si el tráfico de hello puede ser dirigido toohello secundarios.

Hello tabla siguiente describe el comportamiento de Hola de Traffic Manager comprobaciones de mantenimiento para un punto de conexión anidada.

| Estado de supervisión de perfiles secundarios | Estado de supervisión de extremos principales | Notas |
| --- | --- | --- |
| Deshabilitado. perfil de Hello secundario se ha deshabilitado. |Stopped |estado del extremo Hola primario se detiene, no se ha deshabilitado. Hola estado deshabilitado se reserva para indicar que ha deshabilitado el extremo de hello en perfil de hello primario. |
| Degradado. Al menos un punto de conexión de perfil secundario se encuentra en estado Degradado. |Online: número de Hola de extremos en línea en el perfil de hello secundario es al menos Hola valor de MinChildEndpoints.<BR>CheckingEndpoint: número de Hola de extremos en línea y CheckingEndpoint en perfil de hello secundario es al menos Hola valor de MinChildEndpoints.<BR>Degradado: en caso contrario. |El tráfico es enrutado tooan extremo de estado CheckingEndpoint. Si MinChildEndpoints se establece demasiado alto, el punto de conexión de hello siempre está degradado. |
| En línea. Al menos un punto de conexión de perfil secundario se encuentra en estado En línea. Ningún extremo está en estado degradado Hola. |Consulte más arriba. | |
| CheckingEndpoints. Al menos un punto de conexión de perfil secundario es "CheckingEndpoint". Ningún punto de conexión está "En línea" o "Degradado". |Igual que el anterior. | |
| Inactivo. Todos los puntos de conexión de perfil secundario están en estado "Deshabilitado" o "Detenido", o bien se trata de un perfil sin ningún punto de conexión. |Stopped | |

## <a name="next-steps"></a>Pasos siguientes:
- Obtenga más información sobre la [supervisión del punto de conexión y la conmutación por error automática](../traffic-manager/traffic-manager-monitoring.md)del Administrador de tráfico.
- Obtenga más información sobre los [métodos de enrutamiento del tráfico](../traffic-manager/traffic-manager-routing-methods.md) de Traffic Manager.