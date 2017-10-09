---
title: "preguntas frecuentes de caché de Redis aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de hello respuestas toocommon preguntas, los patrones y prácticas recomendadas para caché en Redis de Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c2c52b7d-b2d1-433a-b635-c20180e5cab2
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 2c6ed2f65f755bd08f04857b7af31f520cf4f158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-faq"></a>P+F de Azure Redis Cache
Obtenga información acerca de hello respuestas toocommon preguntas, los patrones y prácticas recomendadas para caché en Redis de Azure.

## <a name="what-if-my-question-isnt-answered-here"></a>Mi pregunta no está respondida aquí. ¿Qué debo hacer?
Si su pregunta no aparece aquí, háganoslo saber y lo ayudaremos a encontrar una respuesta.

* Puede publicar una pregunta en los comentarios de Hola final Hola de estas preguntas más frecuentes y ponerse en contacto con el equipo de la memoria caché de Azure de Hola y otros miembros de la Comunidad sobre este artículo.
* tooreach un público más amplio, puede publicar una pregunta en hello [foro de MSDN de caché de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurecache) y ponerse en contacto con el equipo de la memoria caché de Azure de Hola y otros miembros de la Comunidad de Hola.
* Si desea toomake una solicitud de característica, puede enviar sus solicitudes e ideas demasiado[voz de usuario de caché de Redis de Azure](https://feedback.azure.com/forums/169382-cache).
* También puede enviar un correo electrónico toous en [Azure caché externo comentarios](mailto:azurecache@microsoft.com).

## <a name="azure-redis-cache-basics"></a>Conceptos básicos de Azure Redis Cache
Hola preguntas más frecuentes en esta sección se abordan algunos de los conceptos básicos de Hola de caché en Redis de Azure.

* [¿Qué es Caché en Redis de Azure?](#what-is-azure-redis-cache)
* [Introducción a Azure Redis Cache](#how-can-i-get-started-with-azure-redis-cache)

Hola siguientes preguntas y respuestas cubren los conceptos básicos y preguntas acerca de la caché en Redis de Azure y se responden en uno de Hola otras secciones de preguntas más frecuentes.

* [¿Qué oferta y tamaño de Caché en Redis debo utilizar?](#what-redis-cache-offering-and-size-should-i-use)
* [¿Qué clientes de Caché en Redis puedo usar?](#what-redis-cache-clients-can-i-use)
* [¿Hay un emulador local para Azure Redis Cache?](#is-there-a-local-emulator-for-azure-redis-cache)
* [¿Cómo se supervisa el estado de Hola y el rendimiento de la memoria caché?](#how-do-i-monitor-the-health-and-performance-of-my-cache)

## <a name="planning-faqs"></a>Preguntas más frecuentes de planeación
* [¿Qué oferta y tamaño de Caché en Redis debo utilizar?](#what-redis-cache-offering-and-size-should-i-use)
* [Rendimiento de Azure Redis Cache](#azure-redis-cache-performance)
* [¿En qué región debo buscar mi caché?](#in-what-region-should-i-locate-my-cache)
* [¿Cómo me facturan por Azure Redis Cache?](#how-am-i-billed-for-azure-redis-cache)
* [¿Puedo utilizar Azure Redis Cache con la nube de Azure Government, la nube de China de Azure o Microsoft Azure Alemania?](#can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany)

## <a name="development-faqs"></a>Preguntas más frecuentes de desarrollo
* [¿Qué opciones de configuración de StackExchange.Redis Hola se hacer?](#what-do-the-stackexchangeredis-configuration-options-do)
* [¿Qué clientes de Caché en Redis puedo usar?](#what-redis-cache-clients-can-i-use)
* [¿Hay un emulador local para Azure Redis Cache?](#is-there-a-local-emulator-for-azure-redis-cache)
* [¿Cómo puedo ejecutar comandos de Redis?](#how-can-i-run-redis-commands)
* [¿Por qué no caché en Redis de Azure tiene una referencia de biblioteca de clases MSDN como parte de Hola otros servicios de Azure?](#why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-the-other-azure-services)
* [¿Puedo usar Azure Redis Cache como caché de la sesión PHP?](#can-i-use-azure-redis-cache-as-a-php-session-cache)
* [¿Cuáles son las bases de datos de Redis?](#what-are-redis-databases)

## <a name="security-faqs"></a>Preguntas más frecuentes de seguridad
* [¿Cuándo se puede habilitar el puerto de sin SSL de Hola para conectar tooRedis?](#when-should-i-enable-the-non-ssl-port-for-connecting-to-redis)

## <a name="production-faqs"></a>Preguntas más frecuentes de producción
* [¿Cuáles son algunas prácticas recomendadas de producción?](#what-are-some-production-best-practices)
* [¿Cuáles son algunas de las consideraciones de hello cuando utilice comandos de Redis comunes?](#what-are-some-of-the-considerations-when-using-common-redis-commands)
* [¿Cómo puedo realicen pruebas comparativas y pruebas Hola de rendimiento de la memoria caché?](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* [Detalles importantes sobre el crecimiento del grupo de subprocesos](#important-details-about-threadpool-growth)
* [Habilitar tooget de servidor de catálogo global más rendimiento del cliente de hello al usar StackExchange.Redis](#enable-server-gc-to-get-more-throughput-on-the-client-when-using-stackexchangeredis)
* [Consideraciones sobre rendimiento de las conexiones](#performance-considerations-around-connections)

## <a name="monitoring-and-troubleshooting-faqs"></a>Preguntas más frecuentes de supervisión y solución de problemas
Hola preguntas más frecuentes en esta sección cubren habituales de supervisión y solución de problemas de preguntas. Para obtener más información sobre la supervisión y solución de problemas de las instancias de caché en Redis de Azure, consulte [cómo toomonitor Redis de Azure almacenan en caché](cache-how-to-monitor.md) y [cómo tootroubleshoot Redis de Azure almacenan en caché](cache-how-to-troubleshoot.md).

* [¿Cómo se supervisa el estado de Hola y el rendimiento de la memoria caché?](#how-do-i-monitor-the-health-and-performance-of-my-cache)
* [¿Por qué estoy viendo los tiempos de expiración?](#why-am-i-seeing-timeouts)
* [¿Por qué se desconecta mi cliente de caché de hello?](#why-was-my-client-disconnected-from-the-cache)

## <a name="prior-cache-offering-faqs"></a>Preguntas más frecuentes de la oferta de caché anterior
* [¿Qué oferta de caché de Azure es adecuada para mí?](#which-azure-cache-offering-is-right-for-me)

### <a name="what-is-azure-redis-cache"></a>¿Qué es Azure Redis Cache?
Caché en Redis de Azure se basa en código de abierto populares hello [caché en Redis](http://redis.io). Proporciona acceso a tooa dedicado Redis caché segura, administrada por Microsoft y es accesible desde cualquier aplicación en Azure. Para obtener información más detallada, vea hello [Azure Redis Cache](https://azure.microsoft.com/services/cache/) página del producto en Azure.com.

### <a name="how-can-i-get-started-with-azure-redis-cache"></a>Introducción a Azure Redis Cache
Hay varias maneras de empezar a utilizar Azure Redis Cache.

* Puede consultar uno de los tutoriales disponibles para [.NET](cache-dotnet-how-to-use-azure-redis-cache.md), [ASP.NET](cache-web-app-howto.md), [Java](cache-java-get-started.md), [Node.js](cache-nodejs-get-started.md) y [Python](cache-python-get-started.md).
* Puede ver [cómo tooBuild alto rendimiento aplicaciones utilizando Microsoft Azure Redis Cache](https://azure.microsoft.com/documentation/videos/how-to-build-high-performance-apps-using-microsoft-azure-cache/).
* Puede consultar documentación del cliente de Hola para los clientes de Hola que coincide con el lenguaje de desarrollo de Hola de su toosee proyecto cómo toouse Redis. Hay muchos clientes de Redis que pueden utilizarse con Azure Redis Cache. Para ver una lista de clientes de Redis, consulte [http://redis.io/clients](http://redis.io/clients).

Si no tiene una cuenta de Azure, siga estos pasos:

* [Abrir una cuenta de Azure gratis](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero). Obtenga créditos que pueden ser utilizado tootry out servicios de Azure de pago. Incluso después de que se agoten los créditos hello, puede mantener la cuenta de hello y usar características y servicios de Azure gratuitos.
* [Activar los beneficios de suscripción a Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero). Su suscripción a MSDN le proporciona créditos todos los meses que puede usar para servicios de Azure de pago.

<a name="cache-size"></a>

### <a name="what-redis-cache-offering-and-size-should-i-use"></a>¿Qué oferta y tamaño de Caché en Redis debo utilizar?
Cada oferta de Azure Redis Cache proporciona diferentes niveles de **tamaño**, **ancho de banda**, **alta disponibilidad** y opciones del **Acuerdo de Nivel de Servicio**.

Consideraciones para elegir una oferta de caché son las siguientes de Hola.

* **Memoria**: niveles de básico y estándar de hello ofrecen 250 MB: 53 GB. nivel de Hello Premium ofrece hasta too530 GB. Para obtener más información, consulte [Precios de Azure Redis Cache](https://azure.microsoft.com/pricing/details/cache/).
* **Rendimiento de red**: si tiene una carga de trabajo que requiere un alto rendimiento, nivel de hello Premium ofrece más ancho de banda en comparación con tooStandard o Basic. También dentro de cada nivel, las memorias caché de mayor tamaño tienen más ancho de banda debido a Hola subyacente de la máquina virtual que hospeda la caché de Hola. Vea hello [a partir de tabla](#cache-performance) para obtener más información.
* **Rendimiento**: nivel Premium de hello ofrece un rendimiento máximo disponible de Hola. Si el cliente o servidor de caché de hello alcanza el límite de ancho de banda de hello, puede recibir los tiempos de espera en el lado del cliente de Hola. Para obtener más información, vea hello en la tabla siguiente.
* **Alta disponibilidad/SLA**: caché en Redis de Azure garantiza que una memoria caché estándar o Premium está disponible al menos un 99,9% de tiempo de Hola. toolearn más información sobre nuestro SLA, consulte [precios de caché de Redis de Azure](https://azure.microsoft.com/support/legal/sla/cache/v1_0/). Hola SLA solo cubre los puntos de conexión de conectividad toohello memoria caché. Hola SLA no cubre la protección contra la pérdida de datos. Se recomienda usar la característica de persistencia de datos de Redis hello en resistencia de hello Premium capa tooincrease contra la pérdida de datos.
* **Persistencia de los datos de Redis**: nivel Premium de hello permite toopersist datos de la caché de hello en una cuenta de almacenamiento de Azure. En una caché básico o estándar, todos los datos de Hola se almacena en memoria. Si existen problemas con la infraestructura subyacente, podría producirse una pérdida de los datos. Se recomienda usar la característica de persistencia de datos de Redis hello en resistencia de hello Premium capa tooincrease contra la pérdida de datos. Azure Redis Cache ofrece opciones de RDB y AOF (próximamente) en la persistencia de Redis. Para obtener más información, consulte [cómo persistencia tooconfigure para una caché de Redis de Azure Premium](cache-how-to-premium-persistence.md).
* **Redis clúster**: toocreate almacena en caché mayor de 53 GB o tooshard datos en varios nodos de Redis, puede utilizar clústeres de Redis, que está disponible en el nivel de hello Premium. Cada nodo consta de un par de caché principal/réplica para alta disponibilidad. Para obtener más información, consulte [cómo tooconfigure agrupación en clústeres para una caché en Redis de Azure Premium](cache-how-to-premium-clustering.md).
* **Mejorado aislamiento de red y seguridad**: implementación de la red Virtual de Azure (VNET) proporciona seguridad mejorada y aislamiento para la caché en Redis de Azure, así como las subredes, las directivas de control de acceso, y otra características toofurther restringir el acceso. Para obtener más información, consulte [cómo son compatibles con tooconfigure red Virtual para una caché de Redis de Azure Premium](cache-how-to-premium-vnet.md).
* **Configurar Redis**: Hola estándar y los niveles de Premium, puede configurar Redis para las notificaciones de Keyspace.
* **Número máximo de conexiones de cliente**: nivel de hello Premium ofrece número máximo de Hola de clientes que se pueden conectar tooRedis, con un número mayor de conexiones para memorias caché con tamaño mayor. Para obtener más información, consulte [Precios de Azure Redis Cache](https://azure.microsoft.com/pricing/details/cache/).
* **Dedicado Core para servidor Redis**: en el nivel Premium de hello, todos los tamaños de caché tienen un núcleo dedicado para Redis. En los niveles básico o estándar de hello, Hola tamaño C1 y superior tenga un núcleo dedicado para el servidor de Redis.
* **Redis es de subproceso único** , por tanto tener dos o más núcleos no proporciona una ventaja adicional sobre tener solo dos núcleos, pero las máquinas virtuales de mayor tamaño suelen tener más ancho de banda que las de menor tamaño. Si el cliente o servidor de caché de hello alcanza el límite de ancho de banda de hello, recibirá los tiempos de espera en el lado del cliente de Hola.
* **Mejoras de rendimiento**: memorias caché en el nivel Premium de Hola se implementan en hardware con procesadores rápidos disponibles actualmente, lo que proporciona una mejor toohello comparados básico o estándar nivel de rendimiento. Las cachés de nivel Premium tienen un mayor rendimiento y latencias más bajas.

<a name="cache-performance"></a>

### <a name="azure-redis-cache-performance"></a>Rendimiento de Azure Redis Cache
Hello siguiente tabla muestran valores de ancho de banda máximo de hello observados durante la comprobación de diversos tamaños de Standard y Premium se almacena en caché mediante `redis-benchmark.exe` desde una VM de Iaas con el punto de conexión de hello Azure Redis Cache. 

>[!NOTE] 
>Estos valores no se garantizan y no hay ningún SLA para estos números, sino que deben ser los habituales. Se puede cargar su propio tamaño de caché correcto de aplicación toodetermine hello para la aplicación de prueba.
>
>

En esta tabla, podemos sacar Hola siguientes conclusiones:

* Rendimiento de cachés de Hola Hola mismo tamaño es más alto en Hola nivel Premium como nivel estándar toohello comparados. Por ejemplo, con un 6 GB de memoria caché, rendimiento de P1 es 180.000 RPS como too49 comparados, 000 para C3.
* Con Redis agrupación en clústeres, el rendimiento aumenta linealmente a medida que aumente el número de Hola de particiones (nodos) en clúster de Hola. Por ejemplo, si crea un clúster P4 de 10 particiones, rendimiento disponible hello es 400.000 * 10 = 4 millones RPS.
* El rendimiento para los tamaños de clave más grandes es más alto en el nivel Premium de hello como toohello comparado nivel estándar.

| Plan de tarifa  | Tamaño | Núcleos de CPU | Ancho de banda disponible | Tamaño del valor de 1 kB |
| --- | --- | --- | --- | --- |
| **Tamaños de caché estándar** | | |**Megabits por segundo (Mb/s) o Megabytes por segundo (MB/s)** |**Solicitudes por segundo (RPS)** |
| C0 |250 MB |Compartido |5 / 0.625 |600 |
| C1 |1 GB |1 |100 / 12.5 |12,200 |
| C2 |2,5 GB |2 |200 / 25 |24,000 |
| C3 |6 GB |4 |400 / 50 |49,000 |
| C4 |13 GB |2 |500 / 62.5 |61,000 |
| C5 |26 GB |4 |1,000 / 125 |115,000 |
| C6 |53 GB |8 |2,000 / 250 |150 000 |
| **Tamaños de caché Premium** | |**Núcleos de CPU por partición** | **Megabits por segundo (Mb/s) o Megabytes por segundo (MB/s)** |**Solicitudes por segundo (RPS), por partición** |
| P1 |6 GB |2 |1,500 / 187.5 |180,000 |
| P2 |13 GB |4 |3,000 / 375 |360,000 |
| P3 |26 GB |4 |3,000 / 375 |360,000 |
| P4 |53 GB |8 |6,000 / 750 |400.000 |

Para obtener instrucciones acerca de cómo descargar Hola Redis herramientas como `redis-benchmark.exe`, vea hello [¿cómo se puede ejecutar comandos de Redis?](#cache-commands) sección.

<a name="cache-region"></a>

### <a name="in-what-region-should-i-locate-my-cache"></a>¿En qué región debo buscar mi caché?
Para obtener el mejor rendimiento y latencia más baja, busque el servicio Azure Redis Cache Hola misma región que la aplicación de cliente de caché.

<a name="cache-billing"></a>

### <a name="how-am-i-billed-for-azure-redis-cache"></a>¿Cómo me facturan por Azure Redis Cache?
Los precios de Azure Redis Cache están [aquí](https://azure.microsoft.com/pricing/details/cache/). página de precios de Hello muestra precio como una tarifa por hora. Las memorias caché se facturan según una por minuto de tiempo de Hola Hola caché se crea hasta el tiempo de Hola que se elimina una memoria caché. No hay ninguna opción para detener o pausar facturación Hola de una memoria caché.

### <a name="can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany"></a>¿Puedo utilizar Azure Redis Cache con la nube de Azure Government, la nube de China de Azure o Microsoft Azure Alemania?
Sí, Azure Redis Cache está disponible en la nube de Azure Government, la nube de China de Azure y Microsoft Azure Alemania. direcciones URL de Hola para acceder y administrar caché en Redis de Azure son diferentes en esas nubes en comparación con la nube pública de Azure. 

| Nube   | Sufijo DNS para Redis            |
|---------|---------------------------------|
| Público  | *.redis.cache.windows.net       |
| Gobierno de EE. UU.  | *.redis.cache.usgovcloudapi.net |
| Alemania | *.redis.cache.cloudapi.de       |
| China   | *.redis.cache.chinacloudapi.cn  |

Para obtener más información sobre las consideraciones al usar caché en Redis de Azure con otras nubes, vea Hola siguientes vínculos.

- [Bases de datos de Azure Government - Azure Redis Cache](../azure-government/documentation-government-services-database.md#azure-redis-cache)
- [Nube de China de Azure - Azure Redis Cache](https://www.azure.cn/documentation/services/redis-cache/)
- [Microsoft Azure Alemania](https://azure.microsoft.com/overview/clouds/germany/)

Para obtener información sobre el uso de caché en Redis de Azure con PowerShell en la nube de la administración pública de Azure y Azure China en la nube, Microsoft Azure en Alemania, consulte [cómo tooconnect tooother nubes - PowerShell caché Redis de Azure](cache-howto-manage-redis-cache-powershell.md#how-to-connect-to-other-clouds).

<a name="cache-configuration"></a>

### <a name="what-do-hello-stackexchangeredis-configuration-options-do"></a>¿Qué opciones de configuración de StackExchange.Redis Hola se hacer?
StackExchange.Redis tiene muchas opciones. Esta sección trata sobre algunos de los parámetros comunes de Hola. Para obtener más información acerca de las opciones de StackExchange.Redis, consulte [Configuración de StackExchange.Redis](https://stackexchange.github.io/StackExchange.Redis/Configuration).

| ConfigurationOptions | Descripción | Recomendación |
| --- | --- | --- |
| AbortOnConnectFail |Cuando se establece tootrue, conexión hello no volverá a conectarse después de un error de red. |Establecer toofalse y deje que StackExchange.Redis volver a conectar automáticamente. |
| ConnectRetry |conectarse Hola número de veces que los intentos de conexión de toorepeat durante inicial. |Vea Hola después de notas para obtener instrucciones. |
| ConnectTimeout |Tiempo de espera en milisegundos para operaciones de conexión. |Vea Hola después de notas para obtener instrucciones. |

Valores predeterminados de Hola de cliente hello suelen ser suficientes. Puede ajustar opciones de hello en función de la carga de trabajo.

* **Reintentos**
  * Para ConnectRetry y ConnectTimeout, instrucciones generales de hello es toofail rápido y vuelva a intentarlo. Esta guía se basa en la carga de trabajo y la cantidad de tiempo en el promedio de toma de su tooissue cliente un comando de Redis y recibir una respuesta.
  * Permita que StackExchange.Redis se vuelva a conectar automáticamente en lugar de comprobar el estado de conexión y volver a conectarse. **Procure no utilizar hello ConnectionMultiplexer.IsConnected propiedad**.
  * Snowballing - a veces puede encontrarse con un problema donde están reintentando y Hola reintenta la bola de nieve y nunca se recupera. Si se produce snowballing, considere la posibilidad de usar un algoritmo de reintento de retroceso exponencial tal y como se describe en [vuelva a intentar instrucciones generales](../best-practices-retry-general.md) publicados por el grupo de Microsoft Patterns & Practices Hola.
* **Valores de tiempo de expiración**
  * Tenga en cuenta la carga de trabajo y establecer valores de hello en consecuencia. Si va a almacenar los valores grandes, establecer el valor más alto de tooa de tiempo de espera de Hola.
  * Establecer `AbortOnConnectFail` toofalse y deje que StackExchange.Redis volver a conectar automáticamente.
  * Usar una única instancia de ConnectionMultiplexer para la aplicación hello. Puede usar un toocreate LazyConnection una sola instancia devuelto por una propiedad de conexión, como se muestra en [conectarse mediante la clase ConnectionMultiplexer de hello de caché de toohello](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache).
  * Conjunto hello `ConnectionMultiplexer.ClientName` propiedad tooan instancia único nombre de la aplicación con fines de diagnóstico.
  * Use varias instancias `ConnectionMultiplexer` para cargas de trabajo personalizadas.
      * Puede seguir este modelo si tiene una carga variable en la aplicación. Por ejemplo:
      * Puede tener un multiplexor para tratar con claves grandes.
      * Puede tener un multiplexor para tratar con claves pequeñas.
      * Puede establecer distintos valores para los tiempos de expiración de la conexión así como lógica de reintento para cada ConnectionMultiplexer que use.
      * Conjunto hello `ClientName` propiedad en cada toohelp multiplexor con diagnósticos.
      * Esta guía puede provocar la latencia de toomore simplificado por `ConnectionMultiplexer`.

### <a name="what-redis-cache-clients-can-i-use"></a>¿Qué clientes de Caché en Redis puedo usar?
Una de las grandes virtudes de Hola de Redis es que hay muchos clientes admiten muchos lenguajes de desarrollo diferentes. Para obtener una lista de clientes, consulte [Redis clients](http://redis.io/clients)(Clientes de Redis). Para ver los tutoriales que abarcan varios idiomas diferentes y los clientes, consulte [cómo toouse Redis de Azure almacenan en caché](cache-dotnet-how-to-use-azure-redis-cache.md) y haga clic en el idioma de hello deseado del selector de idioma de hello en parte superior de hello del artículo de Hola.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<a name="cache-emulator"></a>

### <a name="is-there-a-local-emulator-for-azure-redis-cache"></a>¿Hay un emulador local para Azure Redis Cache?
No hay ningún emulador local para caché en Redis de Azure, pero puede ejecutar versión MSOpenTech de Hola de redis server.exe de hello [Redis herramientas de línea de comandos](https://github.com/MSOpenTech/redis/releases/) en local del equipo y conectar tooit tooget una caché local del tooa experiencia similar emulador de Windows, como se muestra en el siguiente ejemplo de Hola:

    private static Lazy<ConnectionMultiplexer>
          lazyConnection = new Lazy<ConnectionMultiplexer>
        (() =>
        {
            // Connect tooa locally running instance of Redis toosimulate a local cache emulator experience.
            return ConnectionMultiplexer.Connect("127.0.0.1:6379");
        });

        public static ConnectionMultiplexer Connection
        {
            get
            {
                return lazyConnection.Value;
            }
        }


Opcionalmente, puede configurar un [redis.conf](http://redis.io/topics/config) toomore archivo coinciden estrechamente con hello [configuración de caché predeterminada](cache-configure.md#default-redis-server-configuration) de su caché de Redis en línea de Azure si lo desea.

<a name="cache-commands"></a>

### <a name="how-can-i-run-redis-commands"></a>¿Cómo puedo ejecutar comandos de Redis?
Puede usar cualquiera de los comandos de hello enumerados en [comandos de Redis](http://redis.io/commands#) excepto los comandos de hello enumerados en [Redis comandos no admitidos en caché en Redis de Azure](cache-configure.md#redis-commands-not-supported-in-azure-redis-cache). Tiene varios comandos de Redis toorun de opciones.

* Si tiene una caché Standard o Premium, puede ejecutar comandos de Redis mediante hello [Redis consola](cache-configure.md#redis-console). consola de Redis Hola proporciona un toorun de forma segura comandos de Redis en hello portal de Azure.
* También puede utilizar herramientas de línea de comandos de Redis Hola. toouse, realizar Hola lo siguiente:
* Descargar hello [Redis herramientas de línea de comandos](https://github.com/MSOpenTech/redis/releases/).
* Conectar toohello caché mediante `redis-cli.exe`. Pase el extremo de la caché de hello con conmutador -h de Hola y la clave de Hola se mediante - a como se muestra en el siguiente ejemplo de Hola:
* `redis-cli -h <your cache="" name="">
  .redis.cache.windows.net -a <key>
  `

> [!NOTE]
> Hello herramientas de línea de comandos de Redis no funcionan con hello puerto SSL, pero puede utilizar una herramienta como `stunnel` toosecurely conectar puerto SSL de hello herramientas toohello según las instrucciones de hello en hello [anuncio de proveedor de estado de sesión de ASP.NET para Versión preliminar de Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) entrada de blog.
>
>

<a name="cache-reference"></a>

### <a name="why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-hello-other-azure-services"></a>¿Por qué no caché en Redis de Azure tiene una referencia de biblioteca de clases MSDN como parte de Hola otros servicios de Azure?
Caché en Redis de Microsoft Azure se basa en código abierto populares de hello caché en Redis y pueden tener acceso a una amplia variedad de [clientes de Redis](http://redis.io/clients) para muchos lenguajes de programación. Cada cliente tiene su propia API que hace llama toohello Redis caché instancia mediante [comandos de Redis](http://redis.io/commands).

Dado que cada cliente es diferente, no hay no una referencia de clase centralizada en MSDN; cada cliente mantiene su propia documentación de referencia. Documentación de referencia de toohello de Además, hay varios tutoriales que muestra cómo se inicia tooget con caché en Redis de Azure con distintos idiomas y los clientes de caché. tooaccess estos tutoriales, vea [cómo toouse Redis de Azure almacenan en caché](cache-dotnet-how-to-use-azure-redis-cache.md) y haga clic en el idioma de hello deseado del selector de idioma de hello en parte superior de hello del artículo de Hola.

### <a name="can-i-use-azure-redis-cache-as-a-php-session-cache"></a>¿Puedo usar Azure Redis Cache como caché de la sesión PHP?
Sí, toouse caché en Redis de Azure como una memoria caché la sesión PHP, especifique la instancia Azure Redis Cache tooyour de cadena de conexión de hello en `session.save_path`.

> [!IMPORTANT]
> Al usar caché en Redis de Azure como una memoria caché de sesión PHP, debe URL codificar caché toohello de hello seguridad clave tooconnect usado, como se muestra en el siguiente ejemplo de Hola:
>
> `session.save_path = "tcp://mycache.redis.cache.windows.net:6379?auth=<url encoded primary or secondary key here>";`
>
> Si Hola clave no está codificada de dirección URL, recibirá una excepción con un mensaje como:`Failed tooparse session.save_path`
>
>

Para obtener más información sobre el uso de caché en Redis como una memoria caché de sesión PHP con cliente de PhpRedis hello, consulte [controlador de sesión de PHP](https://github.com/phpredis/phpredis#php-session-handler).

### <a name="what-are-redis-databases"></a>¿Cuáles son las bases de datos de Redis?

Bases de datos de Redis son simplemente una separación lógica de datos dentro de hello misma instancia de Redis. memoria caché de Hola se comparte entre todas las bases de datos de Hola y el consumo de memoria real de una base de datos depende de hello claves/valores almacenados en esa base de datos. Por ejemplo, una caché C6 tiene 53 GB de memoria. Puede elegir tooput todos los 53 GB en una base de datos o puede dividirlo entre varias bases de datos. 

> [!NOTE]
> Cuando se utiliza una instancia Premium de Azure Redis Cache con clústeres habilitados, solo está disponible la base de datos 0. Esta limitación es una limitación de Redis intrínseca y no es específico tooAzure caché en Redis. Para obtener más información, vea [¿necesito toomake cualquier toouse de aplicación de cliente de cambios toomy de agrupación en clústeres?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 


<a name="cache-ssl"></a>

### <a name="when-should-i-enable-hello-non-ssl-port-for-connecting-tooredis"></a>¿Cuándo se puede habilitar el puerto de sin SSL de Hola para conectar tooRedis?
El servidor Redis no admite SSL de forma nativa, pero sí Azure Redis Cache. Si se va a conectar tooAzure caché en Redis y el cliente admite SSL, como StackExchange.Redis, a continuación, debe usar SSL.

>[!NOTE]
>puerto no SSL de Hello está deshabilitado de forma predeterminada para las nuevas instancias de caché en Redis de Azure. Si el cliente no es compatible con SSL, debe habilitar puerto no SSL de hello siguiendo las instrucciones de Hola Hola [acceso a puertos](cache-configure.md#access-ports) sección de hello [configurar una memoria caché en Redis de Azure](cache-configure.md) artículo.
>
>

Redis herramientas como `redis-cli` no funcionan con hello puerto SSL, pero puede utilizar una herramienta como `stunnel` toosecurely conectar puerto SSL de hello herramientas toohello según las instrucciones de hello en hello [anunciar un proveedor de estado de sesión de ASP.NET para la versión de vista previa de Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) entrada de blog.

Para obtener instrucciones acerca de cómo descargar Hola Redis herramientas, vea hello [¿cómo se puede ejecutar comandos de Redis?](#cache-commands) sección.

### <a name="what-are-some-production-best-practices"></a>¿Cuáles son algunas prácticas recomendadas de producción?
* [Prácticas recomendadas de StackExchange.Redis](#stackexchangeredis-best-practices)
* [Configuración y conceptos](#configuration-and-concepts)
* [Pruebas de rendimiento](#performance-testing)

#### <a name="stackexchangeredis-best-practices"></a>Prácticas recomendadas de StackExchange.Redis
* Establecer `AbortConnect` toofalse, a continuación, dejar hello ConnectionMultiplexer volver a conectar automáticamente. [Haga clic aquí para obtener información detallada](https://gist.github.com/JonCole/36ba6f60c274e89014dd#file-se-redis-setabortconnecttofalse-md).
* Reutilizar Hola ConnectionMultiplexer: no cree uno nuevo para cada solicitud. Hola `Lazy<ConnectionMultiplexer>` patrón [se muestra aquí](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache) se recomienda.
* Redis funciona mejor con valores más pequeños, por lo que puede cortar los datos más grandes en varias claves. En [esta discusión de Redis](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ), 100 kB se considera "grande". Lea [este artículo](https://gist.github.com/JonCole/db0e90bedeb3fc4823c2#large-requestresponse-size) para ver un problema de ejemplo que puede deberse a valores grandes.
* Configurar la [configuración de grupo de subprocesos](#important-details-about-threadpool-growth) tooavoid tiempos de espera.
* Utilice al menos Hola connectTimeout predeterminado de 5 segundos. Este intervalo daría StackExchange.Redis suficiente tiempo toore-establecer conexión hello, en el caso de una señalización visual de la red.
* Tenga en cuenta los costos de rendimiento Hola asociados con diferentes operaciones que se está ejecutando. Por ejemplo, hello `KEYS` comando es una operación o (n) y debe evitarse. Hola [redis.io sitio](http://redis.io/commands/) tiene detalles de la complejidad del tiempo de Hola para cada operación que admite. Haga clic en cada complejidad de hello toosee de comando para cada operación.

#### <a name="configuration-and-concepts"></a>Configuración y conceptos
* Use el nivel Estándar o Premium en sistemas de producción. Hola nivel básico es un sistema de nodo único con ninguna replicación de datos y ningún SLA. Además, utilice al menos una caché de C1. Las cachés C0 se usan normalmente en escenarios de desarrollo o pruebas sencillos.
* Recuerde que Redis es un almacén de datos **en memoria** . Lea [este artículo](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md) para ser consciente de los escenarios donde puede producirse la pérdida de datos.
* Desarrollar el sistema, que puede controlar señales de conexión [toopatching y conmutación por error de vencimiento](https://gist.github.com/JonCole/317fe03805d5802e31cfa37e646e419d#file-azureredis-patchingexplained-md).

#### <a name="performance-testing"></a>Pruebas de rendimiento
* Iniciar mediante `redis-benchmark.exe` tooget una idea de rendimiento posibles antes de escribir sus propias pruebas de rendimiento. Dado que `redis-benchmark` no admite SSL, debe [habilitar el puerto de hello no SSL a través del portal de Azure de hello](cache-configure.md#access-ports) antes de ejecutar pruebas de Hola. ¿Para obtener ejemplos, vea [cómo puedo realicen pruebas comparativas y pruebas Hola de rendimiento de la memoria caché?](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* Hola client VM utilizado para realizar pruebas debe ser Hola misma región que la instancia de caché de Redis.
* Se recomienda usar Dv2 Series de máquinas virtuales para su cliente ya que tienen hardware mejor y deben proporcionar los mejores resultados Hola.
* Asegúrese de que el cliente de VM que elija tiene al menos tanta capacidad informática y el ancho de banda como memoria caché de Hola que se va a probar.
* Habilitar VRSS en el equipo de cliente hello si se encuentra en Windows. [Haga clic aquí para obtener información detallada](https://technet.microsoft.com/library/dn383582.aspx).
* Las instancias de Redis de nivel Premium tienen mejor latencia de red y rendimiento porque se ejecutan en un hardware mejor de CPU y red.

<a name="cache-redis-commands"></a>

### <a name="what-are-some-of-hello-considerations-when-using-common-redis-commands"></a>¿Cuáles son algunas de las consideraciones de hello cuando utilice comandos de Redis comunes?
* No se deben ejecutar determinados comandos de Redis que toman un toocomplete mucho tiempo, no se conoce el impacto de Hola de estos comandos.
  * Por ejemplo, no ejecute hello [claves](http://redis.io/commands/keys) comando en producción mientras los cambios pueden tardar un tooreturn mucho tiempo según el número de Hola de claves. Redis es un servidor de un único subproceso y procesa los comandos uno a la vez. Si tiene otros comandos que se ejecutaron después de las claves, estos no se procesan hasta que Redis procesa los comandos de las claves de Hola. Hola [redis.io sitio](http://redis.io/commands/) tiene detalles de la complejidad del tiempo de Hola para cada operación que admite. Haga clic en cada complejidad de hello toosee de comando para cada operación.
* Tamaños de clave: ¿debo usar claves/valores pequeños o claves/valores grandes? En general, depende del escenario de Hola. Si su escenario requiere que las claves más largas, puede ajustar Hola ConnectionTimeout y vuelva a intentar valores y ajustar la lógica de reintento. Desde una perspectiva del servidor Redis, los valores menores se observan toohave un mejor rendimiento.
* Estas consideraciones no significan que no se puede almacenar valores mayores en Redis; debe ser consciente de hello siguientes consideraciones. Las latencias serán mayores. Si tiene un conjunto de datos mayor y otro que es más pequeño, puede usar varias instancias de ConnectionMultiplexer, cada una configurada con un conjunto diferente de valores de tiempo de espera e inténtelo de nuevo, como se describe en hello anterior [qué Hola Opciones de configuración de StackExchange.Redis es](#cache-configuration) sección.

<a name="cache-benchmarking"></a>

### <a name="how-can-i-benchmark-and-test-hello-performance-of-my-cache"></a>¿Cómo puedo realicen pruebas comparativas y pruebas Hola de rendimiento de la memoria caché?
* [Habilitar los diagnósticos de caché](cache-how-to-monitor.md#enable-cache-diagnostics) para que pueda [monitor](cache-how-to-monitor.md) Hola estado de la memoria caché. Puede ver hello las métricas de hello portal de Azure y también pueden [descargar y revisar](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) mediante herramientas de Hola de su elección.
* Puede usar pruebas de redis benchmark.exe tooload el servidor de Redis.
* Asegúrese de cliente de prueba de carga de Hola y de caché en Redis Hola Hola misma región.
* Usar redis cli.exe y supervisar caché hello mediante comandos de información de Hola.
* Si la carga está causando la fragmentación de memoria alta, se debe escalar tooa mayor tamaño de la caché.
* Para obtener instrucciones acerca de cómo descargar Hola Redis herramientas, vea hello [¿cómo se puede ejecutar comandos de Redis?](#cache-commands) sección.

Hello comandos siguientes proporcionan un ejemplo del uso de redis benchmark.exe. Para obtener resultados precisos, ejecutar estos comandos desde una máquina virtual en hello misma región que la memoria caché.

* Pruebe solicitudes SET con canalización con una carga útil de 1000

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t SET -n 1000000 -d 1024 -P 50`
* Pruebe solicitudes GET con canalización con una carga útil de 1000.
  Nota: Ejecutar prueba de conjunto de hello mostrado anteriormente primera caché toopopulate

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t GET -n 1000000 -d 1024 -P 50`

<a name="threadpool"></a>

### <a name="important-details-about-threadpool-growth"></a>Detalles importantes sobre el crecimiento del grupo de subprocesos
Hola ThreadPool CLR tiene dos tipos de subprocesos: "Trabajo" y "Puerto de terminación de E/S" (también conocido como IOCP) subprocesos.

* Los subprocesos de trabajo se utilizan para aspectos como el procesamiento de métodos `Task.Run(…)` o `ThreadPool.QueueUserWorkItem(…)`. Estos subprocesos también se usan distintos componentes en hello CLR cuando trabajo necesita toohappen en un subproceso en segundo plano.
* IOCP subprocesos se utilizan cuando se produce de E/S asincrónica (por ejemplo, leyendo desde la red de hello).

grupo de subprocesos de Hello ofrece nuevos subprocesos de trabajo o subprocesos de finalización de E/S a petición (sin límite) hasta que se alcanza el valor de "Mínimo" hello para cada tipo de subproceso. De forma predeterminada, el número mínimo de Hola de subprocesos se establece toohello número de procesadores en un sistema.

Una vez número de Hola de existente (ocupado) subprocesos aciertos Hola "" número mínimo de subprocesos, Hola ThreadPool limitar tasa de hello en el que inserta el nuevo subproceso tooone de subprocesos por 500 milisegundos. Normalmente, si su sistema obtiene una ráfaga de trabajo que necesita un subproceso IOCP, ese trabajo se procesará muy rápidamente. Sin embargo, si ráfaga de Hola de trabajo es superior a Hola configurada la opción "Mínima", habrá cierto retraso en el procesamiento de algunas de las tareas de hello cuando hello ThreadPool espera por una de estas dos cosas toohappen.

1. Un subproceso existente se convierte en disponible tooprocess Hola trabajo.
2. Ningún subproceso existente queda libra durante 500 ms, por lo que se crea un nuevo subproceso.

Básicamente, significa que cuando Hola número de subprocesos ocupados es mayor que los subprocesos de Min, va a pagar es probable que un retraso de 500 ms antes de procesa el tráfico de red por la aplicación hello. Además, es importante toonote que, cuando una existente subproceso permanece inactivo durante más de 15 segundos (según lo que recuerdo), se limpian y puede repetir este ciclo de crecimiento y contracción.

Si examinamos un mensaje de error de ejemplo de StackExchange.Redis (compilación 1.0.450 o posterior), verá que ahora se imprimen estadísticas del grupo de subprocesos (consulte a continuación los detalles de trabajo e IOCP).

    System.TimeoutException: Timeout performing GET MyKey, inst: 2, mgr: Inactive,
    queue: 6, qu: 0, qs: 6, qc: 0, wr: 0, wq: 0, in: 0, ar: 0,
    IOCP: (Busy=6,Free=994,Min=4,Max=1000),
    WORKER: (Busy=3,Free=997,Min=4,Max=1000)

En el ejemplo anterior de hello, puede ver que para el subproceso IOCP hay 6 subprocesos ocupados y sistema de hello es configurado tooallow 4 mínimo de subprocesos. En este caso, el cliente de hello habría visto probablemente dos retrasos de 500 ms. porque 6 > 4.

Tenga en cuenta que StackExchange.Redis puede alcanzar los tiempos de espera si se limita el crecimiento de los subprocesos de trabajo o de IOCP.

### <a name="recommendation"></a>Recomendación
Dada esta información, recomendamos encarecidamente que los clientes establecen valor de configuración mínima de Hola para toosomething de subprocesos de trabajo y IOCP mayor que el valor predeterminado de Hola. No podemos dar instrucciones única en lo que este valor debe ser porque Hola valor derecho para una aplicación es demasiado alta o baja para otra aplicación. Esta configuración también puede afectar el rendimiento de Hola de otras partes de aplicaciones complicadas, por lo que cada cliente necesita ajustar toofine que necesita este tootheir de configuración específico. Un buen punto de partida es 200 o 300, y luego probar y ajustar según sea necesario.

¿Cómo tooconfigure esta configuración:

* En ASP.NET, use hello ["minIoThreads" configuración] [ "minIoThreads" configuration setting] en hello `<processModel>` elemento de configuración en el archivo web.config. Si se ejecutan dentro de sitios Web de Azure, esta configuración no se expone a través de opciones de configuración de Hola. Sin embargo, aún debe ser capaz de tooconfigure esta configuración mediante programación (ver abajo) desde el método Application_Start en global.asax.cs.

  > [!NOTE] 
  > Hello valor especificado en este elemento de configuración es un *por núcleo* configuración. Por ejemplo, si tiene una máquina de 4 núcleos y desea que su toobe de configuración de minIOThreads 200 en tiempo de ejecución, usaría `<processModel minIoThreads="50"/>`.
  >

* Fuera de ASP.NET, use hello [ThreadPool.SetMinThreads(...) ](https://msdn.microsoft.com/library/system.threading.threadpool.setminthreads.aspx) API.

<a name="server-gc"></a>

### <a name="enable-server-gc-tooget-more-throughput-on-hello-client-when-using-stackexchangeredis"></a>Habilitar tooget de servidor de catálogo global más rendimiento del cliente de hello al usar StackExchange.Redis
Habilitar el Recolector de servidor puede optimizar el cliente de Hola y proporcionar un mejor rendimiento y la capacidad de StackExchange.Redis. Para obtener más información sobre el servidor de catálogo global y cómo tooenable, vea Hola siguientes artículos:

* [tooenable servidor GC](https://msdn.microsoft.com/library/ms229357.aspx)
* [Fundamentos de la recolección de elementos no utilizados](https://msdn.microsoft.com/library/ee787088.aspx)
* [Recolección de elementos no utilizados y rendimiento](https://msdn.microsoft.com/library/ee851764.aspx)


### <a name="performance-considerations-around-connections"></a>Consideraciones sobre rendimiento de las conexiones

Cada plan de tarifa tiene distintos límites para las conexiones de cliente, memoria y ancho de banda. Aunque cada tamaño de caché permite *hasta* un cierto número de conexiones, cada tooRedis de conexión tiene sobrecarga asociado. Un ejemplo de dicha sobrecarga podría ser el uso de memoria y CPU como resultado del cifrado TLS/SSL. límite máximo de conexiones de Hola para un tamaño de caché especificado supone una caché con poca carga. Si carga de sobrecarga de conexión *más* carga de las operaciones de cliente supera la capacidad para el sistema de Hola, caché Hola puede experimentar problemas de capacidad, incluso si no ha superado el límite de conexiones de hello para el tamaño actual de la caché de Hola.

Para obtener más información acerca de los límites de diferentes conexiones de Hola para cada nivel, consulte [precios de Azure Redis Cache](https://azure.microsoft.com/pricing/details/cache/). Para más información sobre las conexiones y otras configuraciones predeterminadas, consulte [Configuración predeterminada del servidor Redis](cache-configure.md#default-redis-server-configuration).

<a name="cache-monitor"></a>

### <a name="how-do-i-monitor-hello-health-and-performance-of-my-cache"></a>¿Cómo se supervisa el estado de Hola y el rendimiento de la memoria caché?
Se pueden supervisar instancias de Microsoft Azure Redis Cache en hello [portal de Azure](https://portal.azure.com). Puede ver las métricas, anclar gráficos de métricas toohello panel de inicio, personalizar el intervalo de fecha y hora de Hola de gráficos de supervisión, agregar y quitar métricas de los gráficos de Hola y establecer alertas cuando se cumplen determinadas condiciones. Para obtener más información, consulte [Supervisión de Azure Redis Cache](cache-how-to-monitor.md).

Hola caché en Redis **menú recursos** también contiene varias herramientas para supervisar y solucionar sus cachés.

* En **Diagnosticar y solucionar problemas** se proporciona información sobre los problemas comunes y las estrategias para resolverlos.
* **estado de los recursos** supervisa el recurso e indica si se ejecuta del modo previsto. Para obtener más información acerca de hello servicio de mantenimiento de recursos de Azure, consulte [información general de mantenimiento de recursos de Azure](../resource-health/resource-health-overview.md).
* **Nueva solicitud de soporte técnico** proporciona opciones tooopen una solicitud de soporte técnico de la memoria caché.

Estas herramientas permiten toomonitor Hola estado de las instancias de caché en Redis de Azure y ayudan a administrar las aplicaciones de almacenamiento en caché. Para obtener más información, vea la sección "Compatibilidad y configuración de solución de problemas" de Hola de [cómo tooconfigure Redis de Azure almacenan en caché](cache-configure.md).

<a name="cache-timeouts"></a>

### <a name="why-am-i-seeing-timeouts"></a>¿Por qué estoy viendo los tiempos de expiración?
Los tiempos de espera se producen en cliente hello que usar tootalk tooRedis. Cuando se envía un comando toohello Redis server, comando hello está puesto en la cola y servidor Redis finalmente recoge comando hello y lo ejecuta. Sin embargo cliente hello puede tiempo de espera durante este proceso y si lo hace una excepción se produce en hello llamando a lado. Para más información sobre la solución de problemas de tiempo de espera, consulte [Solución de problemas del lado cliente](cache-how-to-troubleshoot.md#client-side-troubleshooting) y [Excepciones de tiempo de espera de StackExchange.Redis](cache-how-to-troubleshoot.md#stackexchangeredis-timeout-exceptions).

<a name="cache-disconnect"></a>

### <a name="why-was-my-client-disconnected-from-hello-cache"></a>¿Por qué se desconecta mi cliente de caché de hello?
los siguientes Hola son alguna razón común para una desconexión de la memoria caché.

* Causas de cliente
  * se volvió a implementar la aplicación de cliente de Hola.
  * aplicación de cliente de Hello realiza una operación de escalado.
    * En caso de hello de servicios en la nube o aplicaciones Web, esto puede deberse tooauto la escala.
  * nivel de red de Hello en hello cliente cambia.
  * Se produjeron errores transitorios en cliente de Hola o en nodos de la red entre el cliente de Hola y el servidor de Hola Hola.
  * se alcanzó el límite del umbral de ancho de banda de Hola.
  * Las operaciones de la CPU tardó demasiado toocomplete.
* Causas de servidor
  * En hello oferta de caché standard, Hola servicio de caché de Redis de Azure inicia una conmutación por error de nodo secundario de hello nodo principal toohello.
  * Azure revisión instancia Hola donde se implementó la memoria caché de Hola
    * Esto puede servir para actualizaciones del servidor de Redis o para el mantenimiento general de máquinas virtuales.

### <a name="which-azure-cache-offering-is-right-for-me"></a>¿Qué oferta de caché de Azure es adecuada para mí?
> [!IMPORTANT]
> Según el [anuncio](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/) del año pasado, Azure Managed Cache Service y el servicio Azure In-Role Cache **se retiraron** el 30 de noviembre de 2016. Nuestra recomendación es toouse [Azure Redis Cache](https://azure.microsoft.com/services/cache/). Para obtener información sobre la migración, consulte [migrar desde el servicio de caché administrado tooAzure caché en Redis](cache-migrate-to-redis.md).
>
>

### <a name="azure-redis-cache"></a>Azure Redis Cache
Caché en Redis de Azure está generalmente disponible en tamaños de too53 GB y tiene un SLA del 99,9% de disponibilidad. Hola nueva [nivel premium](cache-premium-tier-intro.md) ofrece tamaños too530 GB y compatibilidad con los clústeres, la red virtual y persistencia, con un SLA del 99,9%.

Azure Redis caché proporciona clientes Hola capacidad toouse una caché de Redis segura y dedicada, administrada por Microsoft. Con esta oferta, dispone de conjunto de características enriquecidas de tooleverage Hola y el ecosistema de Redis y confiable de hospedaje y supervisión de Microsoft.

A diferencia de las memorias caché tradicionales que solo tratan con pares clave-valor, Redis es popular por sus tipos de datos de gran rendimiento. Redis también admite la ejecución de operaciones atómicas en estos tipos, como anexar la cadena de tooa; incrementar el valor de hello en un hash; Insertar lista tooa; calcular la intersección de conjuntos, unión y diferencia; o un miembro de hello obtener con la mayor puntuación en un conjunto ordenado. Otras características incluyen compatibilidad con transacciones, pub/sub, scripting Lua, claves con un número limitado período de vida y configuración configuración toomake Redis comportarse más como una caché tradicional.

Éxito de tooRedis de otro aspecto clave es su ecosistema de código abierto vibrante y Hola alrededor de ella. Esto se refleja en conjunto diverso de Hola de clientes de Redis disponibles a través de varios idiomas. Este ecosistema y la amplia gama de clientes permiten toobe de caché en Redis de Azure usa casi cualquier carga de trabajo que cree en Azure.

Para obtener más información acerca de cómo empezar a usar caché en Redis de Azure, consulte [cómo tooUse Redis de Azure almacenan en caché](cache-dotnet-how-to-use-azure-redis-cache.md) y [documentación de Azure Redis Cache](index.md).

### <a name="managed-cache-service"></a>Managed Cache service
[Managed Cache Service se retiró el 30 de noviembre de 2016.](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)

tooview archivado documentación, vea [archivados documentación del servicio de caché administrado](https://msdn.microsoft.com/library/azure/dn386094.aspx).

### <a name="in-role-cache"></a>Caché en rol
[In-Role Cache se retiró el 30 de noviembre de 2016.](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)

tooview archivado documentación, vea [archivados documentación de caché en rol](https://msdn.microsoft.com/library/azure/dn386103.aspx).

["minIoThreads" configuration setting]: https://msdn.microsoft.com/library/vstudio/7w2sway1(v=vs.100).aspx
