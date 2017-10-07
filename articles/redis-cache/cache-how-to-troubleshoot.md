---
title: "aaaHow tootroubleshoot caché en Redis de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se problemas comunes de tooresolve con caché en Redis de Azure."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 928b9b9c-d64f-4252-884f-af7ba8309af6
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: sdanie
ms.openlocfilehash: 4e736fce2b6d5200a2a8d802f3f1384b63458cab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-azure-redis-cache"></a>Cómo tootroubleshoot Redis de Azure almacenan en caché
Este artículo proporciona instrucciones para la solución Hola siguientes categorías de problemas de caché en Redis de Azure.

* [Solución de problemas de lado cliente](#client-side-troubleshooting) : esta sección proporcionan instrucciones acerca de cómo identificar y resolver problemas causados por la aplicación hello conectarse tooAzure caché en Redis.
* [Solución de problemas de lado de servidor](#server-side-troubleshooting) : esta sección proporcionan instrucciones acerca de cómo identificar y resolver problemas causados en hello lado de servidor de caché en Redis de Azure.
* [Las excepciones de tiempo de espera de StackExchange.Redis](#stackexchangeredis-timeout-exceptions) -esta sección proporciona información sobre cómo solucionar problemas al usar el cliente de StackExchange.Redis Hola.

> [!NOTE]
> Algunos de los pasos de esta guía de solución de problemas de Hola incluyen instrucciones toorun comandos de Redis y supervisar diversas métricas de rendimiento. Para obtener más información e instrucciones, consulte los artículos de Hola Hola [información adicional](#additional-information) sección.
> 
> 

## <a name="client-side-troubleshooting"></a>Solución de problemas de lado cliente
Esta sección describen los problemas que pudieran producirse debido a una condición en la aplicación de cliente de Hola.

* [Presión de memoria en el cliente de Hola](#memory-pressure-on-the-client)
* [Ráfagas de tráfico](#burst-of-traffic)
* [Uso elevado de la CPU del cliente](#high-client-cpu-usage)
* [Ancho de banda del lado cliente agotado](#client-side-bandwidth-exceeded)
* [Tamaño de solicitud/respuesta grande](#large-requestresponse-size)
* [¿Qué datos toomy problema en Redis?](#what-happened-to-my-data-in-redis)

### <a name="memory-pressure-on-hello-client"></a>Presión de memoria en el cliente de Hola
#### <a name="problem"></a>Problema
Presión de memoria en el equipo de cliente hello conduce a tooall tipos de problemas de rendimiento que pueden retrasar el procesamiento de datos enviado por la instancia de Redis Hola sin ningún retraso. Cuando se alcanza la presión de memoria, sistema de hello normalmente tiene datos de toopage de la memoria de toovirtual de memoria física que está en el disco. Esto *muchos errores de página* causas Hola significativamente sistema tooslow hacia abajo.

#### <a name="measurement"></a>Medición
1. Supervisar el uso de memoria en la máquina toomake seguro de que no supera la memoria disponible. 
2. Hola monitor `Page Faults/Sec` contador de rendimiento. La mayoría de los sistemas tendrá algunos errores de página, incluso durante el funcionamiento normal; por tanto, vigile los picos en este contador de rendimiento de errores de página que corresponden a tiempos de espera agotados.

#### <a name="resolution"></a>Resolución
Actualice a su cliente mayor tamaño de máquina virtual con más memoria tooa de cliente o profundizar en los consuption de memoria memoria tooreduce de patrones de uso.

### <a name="burst-of-traffic"></a>Ráfagas de tráfico
#### <a name="problem"></a>Problema
Ráfagas de tráfico se combinan con malo `ThreadPool` configuración puede provocar retrasos en el procesamiento de datos ya enviado por hello servidor Redis pero aún no se ha utilizado en el lado del cliente de Hola.

#### <a name="measurement"></a>Medición
Supervise cómo sus estadísticas de `ThreadPool` cambian a lo largo del tiempo mediante un código [como este](https://github.com/JonCole/SampleCode/blob/master/ThreadPoolMonitor/ThreadPoolLogger.cs). También puede mirar hello `TimeoutException` mensaje de StackExchange.Redis. Aquí tiene un ejemplo:

    System.TimeoutException: Timeout performing EVAL, inst: 8, mgr: Inactive, queue: 0, qu: 0, qs: 0, qc: 0, wr: 0, wq: 0, in: 64221, ar: 0, 
    IOCP: (Busy=6,Free=999,Min=2,Max=1000), WORKER: (Busy=7,Free=8184,Min=2,Max=8191)

Hola por encima del mensaje, hay varios problemas que le resulten interesantes:

1. Tenga en cuenta que en hello `IOCP` hello y sección `WORKER` sección tiene un `Busy` valor que es mayor que hello `Min` valor. Esto significa que es necesario justar la configuración de `ThreadPool` .
2. También puede ver `in: 64221`. Esto indica que 64211 bytes se han recibido en la capa de sockets de kernel Hola pero aún no haya leído todavía aplicación hello (p. ej. StackExchange.Redis). Normalmente, esto significa que la aplicación no está leyendo datos de red de hello tan rápidamente como servidor hello está enviando tooyou.

#### <a name="resolution"></a>Resolución
Configurar la [configuración de grupo de subprocesos](https://gist.github.com/JonCole/e65411214030f0d823cb) toomake seguro de que el grupo de subprocesos escalará rápidamente en escenarios de ráfaga.

### <a name="high-client-cpu-usage"></a>Uso elevado de la CPU del cliente
#### <a name="problem"></a>Problema
Uso elevado de CPU en el cliente de hello es una indicación de que no puede seguir sistema Hola trabajo Hola que se solicitó tooperform. Esto significa que el cliente hello producirán tooprocess una respuesta de Redis puntualmente aunque Redis envía respuesta Hola muy rápidamente.

#### <a name="measurement"></a>Medición
Hola Monitor uso de CPU del gran sistema a través de hello Portal de Azure u Hola asociado del contador de rendimiento. Tenga cuidado no toomonitor *proceso* CPU porque un solo proceso puede tener poca utilización de CPU en Hola mismo tiempo que la CPU del sistema general puede ser alto. Busque picos de uso de CPU que correspondan a tiempos de espera agotados. Como resultado de elevado de la CPU, también puede ver alto `in: XXX` valores en `TimeoutException` mensajes de error como se describe en hello [ráfaga de tráfico](#burst-of-traffic) sección.

> [!NOTE]
> StackExchange.Redis 1.1.603 y versiones posteriores incluyen hello `local-cpu` métrica en `TimeoutException` mensajes de error. Asegúrese de está utilizando la versión más reciente de Hola de hello [paquete de StackExchange.Redis NuGet](https://www.nuget.org/packages/StackExchange.Redis/). Hay errores constantemente está corregido en hello código toomake tootimeouts más sólida por lo que es importante disponer de la versión más reciente de Hola.
> 
> 

#### <a name="resolution"></a>Resolución
Actualizar tooa mayor tamaño de máquina virtual con más capacidad de CPU o investigar la causa de que los picos de CPU. 

### <a name="client-side-bandwidth-exceeded"></a>Ancho de banda del lado cliente agotado
#### <a name="problem"></a>Problema
Los equipos cliente con diferentes tamaños tienen limitaciones en el ancho de banda de red disponible. Si supera el cliente de Hola Hola ancho de banda disponible, datos no se procesarán en el lado del cliente de hello tan rápidamente como servidor hello es enviarlo. Esto puede provocar tootimeouts.

#### <a name="measurement"></a>Medición
Supervise cómo cambia el uso del ancho de banda a lo largo del tiempo mediante código [como este](https://github.com/JonCole/SampleCode/blob/master/BandWidthMonitor/BandwidthLogger.cs). Tenga en cuenta que este código puede no ejecutarse correctamente en algunos entornos con permisos restringidos (como sitios web de Azure).

#### <a name="resolution"></a>Resolución
Aumente el tamaño de la máquina virtual del cliente o reduzca el consumo del ancho de banda de red.

### <a name="large-requestresponse-size"></a>Tamaño de solicitud/respuesta grande
#### <a name="problem"></a>Problema
Una solicitud/respuesta grande puede provocar tiempos de espera agotados. Por ejemplo, suponga que el valor del tiempo de espera configurado en el cliente es de 1 segundo. La aplicación solicita dos claves (p. ej. 'A' y 'B') en hello vez (uso de Hola la misma conexión de red física). La mayoría de los clientes admiten "Canalización" de las solicitudes, por ejemplo, que ambas solicitudes 'A' y 'B' se envían en servidor de toohello de conexión de hello uno después de hello otros sin tener que esperar las respuestas de Hola. Hello servidor enviará las respuestas de Hola de nuevo en hello mismo orden. Si la respuesta 'A' es grande suficientemente lo puede comer la mayor parte del tiempo de espera de Hola para las solicitudes posteriores. 

Hola siguiente ejemplo muestra este escenario. En este escenario, solicitud 'A' y 'B' se envían rápidamente, servidor hello comienza a enviar las respuestas 'A' y 'B' rápidamente, pero debido a tiempos de transferencia de datos, 'B' atascar detrás de Hola otra solicitud y agota el tiempo, aunque el servidor de hello ha respondido rápidamente.

    |-------- 1 Second Timeout (A)----------|
    |-Request A-|
         |-------- 1 Second Timeout (B) ----------|
         |-Request B-|
                |- Read Response A --------|
                                           |- Read Response B-| (**TIMEOUT**)



#### <a name="measurement"></a>Medición
Se trata de un un toomeasure difícil. Básicamente tiene tooinstrument sus solicitudes grandes de tootrack de código de cliente y las respuestas. 

#### <a name="resolution"></a>Resolución
1. Redis está optimizado para un gran número de valores pequeños, en lugar de unos pocos valores grandes. Hola preferida solución es toobreak seguridad de los datos en los valores menores relacionados. Vea hello [¿qué es el intervalo de tamaño de hello valor ideal para redis? Is 100KB too large?](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ) (¿Cuál es el intervalo de tamaño de valor ideal para redis? ¿100 KB es demasiado grande?) para ver detalles de por qué se recomiendan valores más pequeños.
2. Aumentar tamaño de saludo de la máquina virtual (para el cliente y el servidor de caché de Redis), el tiempo para las respuestas más grandes de transferencia capacidades de tooget mayor ancho de banda, reducir los datos. Tenga en cuenta obtener más ancho de banda solo servidor de Hola o simplemente en hello cliente puede no ser suficiente. Medir el uso de ancho de banda y comparar toohello capacidades del tamaño de hello de la máquina virtual que tiene actualmente.
3. Aumentar el número de Hola de `ConnectionMultiplexer` objetos uso y las solicitudes de round robin a través conexiones diferentes.

### <a name="what-happened-toomy-data-in-redis"></a>¿Qué datos toomy problema en Redis?
#### <a name="problem"></a>Problema
Esperaba para determinados toobe de datos en la instancia de caché en Redis de Azure pero no parece que no existe toobe.

#### <a name="resolution"></a>Resolución
Vea [qué datos toomy problema en Redis?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md) con las posibles causas y resoluciones.

## <a name="server-side-troubleshooting"></a>Solución de problemas de lado servidor
Esta sección describen los problemas que pudieran producirse debido a una condición en el servidor de caché de Hola.

* [Presión de memoria en el servidor de Hola](#memory-pressure-on-the-server)
* [Uso elevado de la CPU/carga de servidor](#high-cpu-usage-server-load)
* [Ancho de banda del lado servidor agotado](#server-side-bandwidth-exceeded)

### <a name="memory-pressure-on-hello-server"></a>Presión de memoria en el servidor de Hola
#### <a name="problem"></a>Problema
Presión de memoria en el lado servidor hello conduce a tooall tipos de problemas de rendimiento que pueden retrasar el procesamiento de solicitudes. Cuando se alcanza la presión de memoria, sistema de hello normalmente tiene datos de toopage de la memoria de toovirtual de memoria física que está en el disco. Esto *muchos errores de página* causas Hola significativamente sistema tooslow hacia abajo. Hay varias causas posibles de esta presión de memoria: 

1. Capacidad de toofull de caché de Hola que haya rellenado con datos. 
2. Redis es ver la fragmentación de memoria alta - suelen deberse almacenar objetos grandes (Redis se optimiza para un objeto pequeño - vea hello [¿qué es el intervalo de tamaño de hello valor ideal para redis? Is 100KB too large?](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ) (¿Cuál es el intervalo de tamaño de valor ideal para redis? ¿100 KB es demasiado grande?) para ver detalles. 

#### <a name="measurement"></a>Medición
Redis expone dos métricas que pueden ayudarle a identificar este problema. en primer lugar es Hello `used_memory` y hello otro es `used_memory_rss`. [Estas métricas](cache-how-to-monitor.md#available-metrics-and-reporting-intervals) están disponibles en hello Portal de Azure o a través de hello [Redis información](http://redis.io/commands/info) comando.

#### <a name="resolution"></a>Resolución
Hay varios cambios posibles que puede hacer uso de memoria de toohelp mantener correcto:

1. [Configurar una directiva de memoria](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) y establecer tiempos de expiración de las claves. Tenga en cuenta que esto puede no ser suficiente si tiene fragmentación.
2. [Configurar un valor reservado maxmemory](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) que es lo suficientemente grande como toocompensate fragmentación de memoria.
3. Dividir los objetos grandes que están en la memoria caché en objetos relacionados más pequeños.
4. [Escala](cache-how-to-scale.md) tooa mayor tamaño de la caché.
5. Si usas un [caché premium con clúster de Redis habilitado](cache-how-to-premium-clustering.md) puede [aumentar el número de Hola de particiones](cache-how-to-premium-clustering.md#change-the-cluster-size-on-a-running-premium-cache).

### <a name="high-cpu-usage--server-load"></a>Uso elevado de la CPU/carga de servidor
#### <a name="problem"></a>Problema
Uso elevado de CPU puede significar que el lado del cliente de hello puede producir un error tooprocess una respuesta de Redis de manera oportuna aunque Redis envía respuesta Hola muy rápidamente.

#### <a name="measurement"></a>Medición
Hola Monitor uso de CPU del gran sistema a través de hello Portal de Azure u Hola asociado del contador de rendimiento. Tenga cuidado no toomonitor *proceso* CPU porque un solo proceso puede tener poca utilización de CPU en Hola mismo tiempo que la CPU del sistema general puede ser alto. Busque picos de uso de CPU que correspondan a tiempos de espera agotados.

#### <a name="resolution"></a>Resolución
[Escala](cache-how-to-scale.md) tooa mayor caché con más capacidad de CPU de nivel o investigar la causa de que los picos de CPU. 

### <a name="server-side-bandwidth-exceeded"></a>Ancho de banda del lado servidor agotado
#### <a name="problem"></a>Problema
Las instancias de memoria caché con diferentes tamaños tienen limitaciones en el ancho de banda de red disponible. Si el servidor de hello supera el ancho de banda disponible de hello, a continuación, datos no se enviará a toohello cliente lo más rápidamente. Esto puede provocar tootimeouts.

#### <a name="measurement"></a>Medición
Puede supervisar hello `Cache Read` métrica, que es la cantidad de Hola de los datos leídos de la caché de hello en Megabytes por segundo (MB/s) durante el intervalo de notificación especificado Hola. Este valor corresponde toohello de ancho de banda de red utilizado por esta memoria caché. Si desea tooset las alertas para los límites de ancho de banda de red de lado de servidor, puede crearlos mediante este `Cache Read` contador. Comparar sus lecturas con valores de hello en [esta tabla](cache-faq.md#cache-performance) para hello observado límites de ancho de banda para caché de distintos tamaños y niveles de precios.

#### <a name="resolution"></a>Resolución
Si es constantemente cerca Hola observado ancho de banda máximo para el tamaño de caché y de nivel de precios, considere la posibilidad de [escalado](cache-how-to-scale.md) tooa precios nivel o el tamaño que tiene el mayor ancho de banda de red, uso de valores de hello en [esta tabla](cache-faq.md#cache-performance) como guía.

## <a name="stackexchangeredis-timeout-exceptions"></a>Excepciones de tiempo de espera de StackExchange.Redis
StackExchange.Redis usa la opción de configuración `synctimeout` para operaciones sincrónicas, y tiene un valor predeterminado de 1000 ms. Si no se completa una llamada sincrónica en hello había estipulada tiempo, hello StackExchange.Redis cliente produce un toohello similar de error de tiempo de espera siguiente ejemplo.

    System.TimeoutException: Timeout performing MGET 2728cc84-58ae-406b-8ec8-3f962419f641, inst: 1,mgr: Inactive, queue: 73, qu=6, qs=67, qc=0, wr=1/1, in=0/0 IOCP: (Busy=6, Free=999, Min=2,Max=1000), WORKER (Busy=7,Free=8184,Min=2,Max=8191)


Este mensaje de error contiene las métricas que pueden ayudar a punto toohello causa y posible la resolución del problema de Hola. Hello tabla siguiente contiene detalles sobre las medidas de mensaje de error de Hola.

| Métrica del mensaje de error | Detalles |
| --- | --- |
| inst |En el último intervalo de tiempo hello: se han emitido 0 comandos |
| mgr |Administrador de socket de Hello está realizando `socket.select` lo que significa que está solicitando Hola OS tooindicate un socket que tiene algo toodo; básicamente: lector de hello no está leyendo activamente en red Hola porque no piense hay algo toodo |
| queue |Hay un total de 73 operaciones en curso. |
| qu |6 de las operaciones en curso de hello están en la cola sin enviar hello y aún no se han escrito toohello de red saliente |
| qs |se enviaron 67 de operaciones en curso de toohello servidor pero aún no está disponible una respuesta. Hola respuesta podría ser `Not yet sent by hello server` o`sent by hello server but not yet processed by hello client.` |
| qc |0 de operaciones en curso de hello ha visto respuestas pero no aún se marcaron como completa debido toowaiting en bucle de finalización de Hola |
| wr |Hay un sistema de escritura activa (es decir Hola 6 sin enviar solicitudes no se omiten) bytes/activewriters |
| bucear |No hay ningún lector active y cero bytes están disponible toobe leer en hello NIC bytes/activereaders |

### <a name="steps-tooinvestigate"></a>Tooinvestigate de pasos
1. Como práctica recomendada de asegurarse de que está usando Hola siguiente patrón tooconnect cuando se usa el cliente de StackExchange.Redis Hola.

    ```c#
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("cachename.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ````

    Para obtener más información, consulte [conectar caché toohello mediante StackExchange.Redis](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache).

1. Asegúrese de que la caché en Redis de Azure y la aplicación de cliente de Hola Hola misma región de Azure. Por ejemplo, podría estar obteniendo los tiempos de espera cuando la memoria caché está en este de EE. pero cliente hello es zona horaria del Pacífico occidental y solicitud de hello no se completa dentro de hello `synctimeout` intervalo o podría estar obteniendo los tiempos de espera cuando se está depurando en el equipo de desarrollo local. 
   
    Que se recomienda encarecidamente toohave caché de Hola y de cliente de hello en Hola mismo región de Azure. Si tiene un escenario que incluye las llamadas de región cruzada, debe establecer hello `synctimeout` el valor del intervalo tooa mayor que el intervalo de 1000 ms de saludo predeterminado mediante la inclusión de un `synctimeout` propiedad en la cadena de conexión de Hola. Hello en el ejemplo siguiente se muestra un fragmento de cadena de conexión de caché de StackExchange.Redis con un `synctimeout` de ms 2000.
   
        synctimeout=2000,cachename.redis.cache.windows.net,abortConnect=false,ssl=true,password=...
2. Asegúrese de está utilizando la versión más reciente de Hola de hello [paquete de StackExchange.Redis NuGet](https://www.nuget.org/packages/StackExchange.Redis/). Hay errores constantemente está corregido en hello código toomake tootimeouts más sólida por lo que es importante disponer de la versión más reciente de Hola.
3. Si hay solicitudes obtener sujetas a limitaciones de ancho de banda en el servidor de Hola o cliente, tardará más tiempo para ellos toocomplete y, por tanto, provocar tiempos de espera. toosee si el tiempo de espera vence toonetwork ancho de banda en el servidor de hello, consulte [superado el ancho de banda del lado servidor](#server-side-bandwidth-exceeded). toosee si el tiempo de espera vence tooclient ancho de banda de red, consulte [superado el ancho de banda del lado cliente](#client-side-bandwidth-exceeded).
4. ¿Se siente CPU se enlazan en el servidor de Hola o en el cliente de hello?
   
   * Compruebe si están obteniendo enlazados por CPU en el cliente que podría provocar Hola solicitud toonot pueden procesar en hello `synctimeout` intervalo, lo que produce un tiempo de espera. Mover tooa tamaño de cliente o distribuir la carga de hello puede ayudar a toocontrol esto. 
   * Compruebe si se va a obtener CPU enlazada Hola servidor mediante la supervisión de hello `CPU` [métrica de rendimiento de caché](cache-how-to-monitor.md#available-metrics-and-reporting-intervals). Solicitudes que entran en mientras Redis es el límite de CPU puede hacer que las solicitudes tootimeout. tooaddress Esto puede distribuir Hola la carga entre varias particiones en una caché premium, o actualizar tooa mayor tamaño o el nivel de precios. Para más información, consulte [Ancho de banda del lado servidor agotado](#server-side-bandwidth-exceeded).
5. ¿Existen comandos tarda mucho tiempo tooprocess en servidor hello? Comandos que tardan mucho tiempo tooprocess en el servidor de redis Hola de ejecución prolongada puede provocar tiempos de espera. Algunos ejemplos de comandos que tardan mucho en ejecutarse son `mget` con un gran número de claves, `keys *` o scripts de LUA mal escritos. Puede conectar tooyour instancia de caché en Redis de Azure con cliente de redis cli de Hola o usar hello [consola Redis](cache-configure.md#redis-console) ejecución hello y [SlowLog](http://redis.io/commands/slowlog) toosee de comando si hay solicitudes tardando más de lo esperado. El servidor de Redis y StackExchange.Redis están optimizados para muchas solicitudes pequeñas, en lugar de menos solicitudes de gran tamaño. Dividir los datos en fragmentos menores puede mejorar las cosas aquí. 
   
    Para obtener información sobre la conexión de punto de conexión de SSL de caché de Redis de Azure de toohello mediante la cli de redis y stunnel, vea hello [anuncio de proveedor de estado de sesión de ASP.NET para Redis versión preliminar](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) entrada de blog. Para más información, consulte [SlowLog](http://redis.io/commands/slowlog).
6. Una carga alta del servidor de Redis puede causar tiempos de espera agotados. Puede supervisar Hola de carga del servidor mediante la supervisión de hello `Redis Server Load` [métrica de rendimiento de caché](cache-how-to-monitor.md#available-metrics-and-reporting-intervals). Una carga del servidor de 100 (valor máximo) significa que ese servidor de redis Hola ha estado ocupado, sin tiempo de inactividad, procesamiento de solicitudes. toosee si algunas solicitudes ocupan todos de capacidad del servidor hello, ejecute hello SlowLog comando tal como se describe en el párrafo anterior Hola. Para más información, consulte [Uso elevado de la CPU/carga de servidor](#high-cpu-usage-server-load).
7. ¿Hubo cualquier otro evento de lado de cliente de Hola que podría haber causado un señalización visual de la red? Comprobar Hola cliente (web, rol de trabajo o una VM de Iaas) si se produjo un evento como número de Hola de instancias de cliente de ajuste de escala hacia arriba o hacia abajo, o implementar una nueva versión del cliente de Hola o escala automática está activada? En nuestras pruebas que hemos encontrado que escalado automático o escala hacia arriba o hacia abajo para hacer que se puede perder conectividad de red saliente durante varios segundos. Código de StackExchange.Redis es resistente toosuch eventos y se volverá a conectar. Durante este tiempo de reconexión las solicitudes en cola Hola pueden tiempo de espera.
8. ¿Hubo una solicitud grande anterior varias solicitudes pequeñas toohello caché en Redis que agotó el tiempo? Hola parámetro `qs` error Hola mensaje le indica cuántas solicitudes se enviaron desde el servidor de toohello de cliente de hello, pero aún no han procesado una respuesta. Este valor puede seguir creciendo, ya que StackExchange.Redis usa una sola conexión de TCP y solo puede leer una respuesta cada vez. Aunque la primera operación de hello agotó el tiempo de espera, no impide que los datos de Hola que se envían hacia y desde el servidor de Hola y otras solicitudes se bloquean hasta que esto está finalizado, provocando tiempos de espera. Una solución es la oportunidad de Hola de toominimize de tiempos de espera, asegurándose de que la memoria caché sea lo suficientemente grande como para la carga de trabajo y dividir los valores grandes en fragmentos más pequeños. Otra posible solución es toouse un grupo de `ConnectionMultiplexer` objetos en el cliente y elija Hola menos cargado `ConnectionMultiplexer` al enviar una solicitud nueva. Esto debe impedir que un tiempo de espera solo cause otro tiempo de espera de solicitudes tooalso.
9. Si utilizas `RedisSessionStateprovider`, asegúrese de tiempo de espera de reintento de hello ha establecido correctamente. `retrytimeoutInMilliseconds` debe ser superior a `operationTimeoutinMilliseonds`; de lo contrario, no se producirá ningún reintento. En el siguiente ejemplo de Hola `retrytimeoutInMilliseconds` se establece too3000. Para obtener más información, consulte [proveedor de estado de sesión de ASP.NET para caché en Redis de Azure](cache-aspnet-session-state-provider.md) y [cómo toouse Hola parámetros de configuración de proveedor de estado de sesión y proveedor de caché de resultados](https://github.com/Azure/aspnet-redis-providers/wiki/Configuration).

    <add
      name="AFRedisCacheSessionStateProvider"
      type="Microsoft.Web.Redis.RedisSessionStateProvider"
      host="enbwcache.redis.cache.windows.net"
      port="6380"
      accessKey="…"
      ssl="true"
      databaseId="0"
      applicationName="AFRedisCacheSessionState"
      connectionTimeoutInMilliseconds = "5000"
      operationTimeoutInMilliseconds = "1000"
      retryTimeoutInMilliseconds="3000" />


1. Compruebe el uso de memoria en el servidor de caché en Redis de Azure hello [supervisión](cache-how-to-monitor.md#available-metrics-and-reporting-intervals) `Used Memory RSS` y `Used Memory`. Si una directiva de expulsión en su lugar, se inicia Redis expulsar claves cuando `Used_Memory` alcanza Hola tamaño de caché. Idealmente, `Used Memory RSS` solo debe ser ligeramente mayor que `Used memory`. Una gran diferencia significa que no hay fragmentación de memoria (interna o externa). Cuando `Used Memory RSS` es menor que `Used Memory`, significa que se ha intercambiado la parte de la memoria caché de Hola por sistema operativo de Hola. Si esto ocurre, que puede esperar latencias importantes. Dado que Redis no tiene control sobre cómo sus asignaciones asignan páginas toomemory, alta `Used Memory RSS` resulta a menudo Hola de un pico en el uso de memoria. Cuando Redis libera memoria, memoria de Hola se le envía toohello asignador y asignador Hola puede o no puede conseguir hello toohello atrás de memoria del sistema. Puede haber una discrepancia entre hello `Used Memory` consumo de memoria y el valor devuelto por el sistema operativo de Hola. Es posible due toohello hechos memoria se ha utilizado y publicado por Redis, pero no le otorgó sistema back-toohello. toohelp mitigar los problemas de memoria puede llevar a cabo pasos de Hola.
   
   * Actualizar tamaño mayor de hello caché tooa para que no está ejecutando con las limitaciones de memoria en el sistema de Hola.
   * Establecer tiempos de expiración de claves de Hola para que los valores antiguos se desalojan de forma proactiva.
   * Hola Hola de monitor `used_memory_rss` métrica de caché. Cuando este valor aproxima a tamaño de hello de la memoria caché, es probable toostart aparece el problema de rendimiento. Distribuir datos de hello en varias particiones si usa una caché premium, o actualizar el tamaño de caché mayor tooa.
   
   Para obtener más información, consulte [presión de memoria en el servidor de hello](#memory-pressure-on-the-server).

## <a name="additional-information"></a>Información adicional
* [¿Qué oferta y tamaño de Caché en Redis debo utilizar?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)
* [¿Cómo puedo realicen pruebas comparativas y pruebas Hola de rendimiento de la memoria caché?](cache-faq.md#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* [¿Cómo puedo ejecutar comandos de Redis?](cache-faq.md#how-can-i-run-redis-commands)
* [Cómo toomonitor Redis de Azure almacenan en caché](cache-how-to-monitor.md)

