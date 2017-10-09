---
title: "aaaHow tooconfigure Redis agrupación en clústeres para una caché en Redis de Azure Premium | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate y administrar instancias de caché en Redis de Azure de clústeres para el nivel Premium de Redis"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 62208eec-52ae-4713-b077-62659fd844ab
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 44d520facb9d1af145b69f1b58f082aabb655d4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-redis-clustering-for-a-premium-azure-redis-cache"></a>¿Cómo tooconfigure Redis agrupación en clústeres para una caché en Redis de Azure Premium
Caché en Redis de Azure tiene diferentes ofertas de caché, lo que proporciona flexibilidad en la elección de Hola de tamaño de caché y las características, incluidas las características de nivel Premium como de agrupación en clústeres, la persistencia y la compatibilidad de red virtual. Este artículo describe cómo tooconfigure agrupación en clústeres en una prima Redis de Azure caché de instancia.

Para obtener información sobre otras características de caché premium, consulte [nivel Premium de caché de Redis de Azure de introducción toohello](cache-premium-tier-intro.md).

## <a name="what-is-redis-cluster"></a>¿Qué es Clúster Redis?
Caché en Redis de Azure ofrece clúster de Redis como [implementado en Redis](http://redis.io/topics/cluster-tutorial). Con clúster de Redis, obtendrá Hola siguientes ventajas: 

* Hola tooautomatically capacidad dividir el conjunto de datos entre varios nodos. 
* Hola capacidad toocontinue operaciones cuando un subconjunto de nodos de hello es experimentando errores o no se puede toocommunicate con el resto de Hola de clúster de Hola. 
* Más rendimiento: rendimiento aumenta linealmente a medida que aumente el número de Hola de particiones. 
* Aumentar el tamaño de memoria: aumenta linealmente a medida que aumente el número de Hola de particiones.  

Para obtener información sobre el tamaño, el rendimiento y el ancho de banda con memorias caché premium, vea [¿Qué oferta y tamaño de Caché en Redis debo utilizar?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)

En Azure, se ofrece Redis clúster como un modelo de réplica principal donde cada partición tiene un par de réplica principal con la replicación donde se administra la replicación de Hola por el servicio de caché de Redis de Azure. 

## <a name="clustering"></a>Agrupación en clústeres
Agrupación en clústeres está habilitada en hello **nueva caché en Redis** hoja durante la creación de la memoria caché. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Agrupación en clústeres se configura en hello **Redis clúster** hoja.

![Agrupación en clústeres][redis-cache-clustering]

Puede tener hasta too10 particiones en clúster de Hola. Haga clic en **habilitado** y deslice el control deslizante de Hola o escriba un número entre 1 y 10 para **número de particiones** y haga clic en **Aceptar**.

Cada partición es un par de caché de la réplica principal administrado por Azure y tamaño total de Hola de caché de Hola se calcula multiplicando el número de Hola de particiones por tamaño de caché de hello seleccionado en el nivel de precios de Hola. 

![Agrupación en clústeres][redis-cache-clustering-selected]

Una vez que se crea una caché Hola conectarse tooit y usar simplemente como una memoria caché no agrupado y Redis distribuye los datos de Hola a lo largo de particiones de memoria caché de Hola. Si diagnósticos es [habilitado](cache-how-to-monitor.md#enable-cache-diagnostics), las métricas capturadas por separado para cada partición y puede ser [ver](cache-how-to-monitor.md) en hello caché en Redis hoja. 

> [!NOTE]
> 
> Hay algunas diferencias menores necesarias en la aplicación cliente cuando se configura la agrupación en clústeres. Para obtener más información, vea [¿necesito toomake cualquier toouse de aplicación de cliente de cambios toomy de agrupación en clústeres?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 

Para el código de ejemplo sobre cómo trabajar con la agrupación en clústeres con cliente de StackExchange.Redis hello, vea hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) parte de hello [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) ejemplo.

<a name="cluster-size"></a>

## <a name="change-hello-cluster-size-on-a-running-premium-cache"></a>Cambiar el tamaño de clúster de hello en un ejecución caché premium
tamaño del clúster de hello toochange en una ejecución premium almacenar en memoria caché con un clic habilitado, agrupación en clústeres **Redis tamaño del clúster** de hello **menú recursos**.

> [!NOTE]
> Mientras hello Azure Redis caché Premium nivel ha sido liberado tooGeneral disponibilidad, característica de tamaño de clúster Redis Hola está actualmente en vista previa.
> 
> 

![Tamaño del Clúster en Redis][redis-cache-redis-cluster-size]

tamaño de clúster de toochange hello, utilice el control deslizante de Hola o escriba un número entre 1 y 10 en hello **número de particiones** cuadro de texto y haga clic en **Aceptar** toosave.

> [!NOTE]
> Ajuste de escala en un clúster ejecuta hello [migrar](https://redis.io/commands/migrate) comando, que es un comando costoso, por lo que para minimizar el impacto, considere la posibilidad de realizar esta operación durante horas de poca actividad. Durante el proceso de migración de hello, verá un pico de carga del servidor. Ajuste de escala en un clúster tiene un valor largo proceso y cantidad de Hola de tiempo que se tarda depende Hola número de claves y el tamaño de los valores de hello asociados a esas claves.
> 
> 

## <a name="clustering-faq"></a>P+F de agrupación en clústeres
Hello lista siguiente contiene toocommonly respuestas preguntas más frecuentes acerca de los clústeres de caché en Redis de Azure.

* [¿Es necesario toomake cualquier toouse de aplicación de cliente de cambios toomy de agrupación en clústeres?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
* [¿Cómo se distribuyen las claves en un clúster?](#how-are-keys-distributed-in-a-cluster)
* [¿Cuál es el mayor tamaño de caché Hola que puedo crear?](#what-is-the-largest-cache-size-i-can-create)
* [¿Todos los clientes de Redis admiten la agrupación en clústeres?](#do-all-redis-clients-support-clustering)
* [¿Cómo conecto toomy caché cuando se habilita la agrupación en clústeres?](#how-do-i-connect-to-my-cache-when-clustering-is-enabled)
* [¿Puedo conectar directamente toohello particiones individuales de la memoria caché?](#can-i-directly-connect-to-the-individual-shards-of-my-cache)
* [¿Puedo configurar la agrupación en clústeres para una memoria caché creada anteriormente?](#can-i-configure-clustering-for-a-previously-created-cache)
* [¿Puedo configurar la agrupación en clústeres para una caché básica o estándar?](#can-i-configure-clustering-for-a-basic-or-standard-cache)
* [¿Puedo usar la agrupación en clústeres con proveedores de estado de sesión de ASP.NET de Redis y almacenamiento en caché de salida de hello?](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)
* [Estoy recibiendo excepciones MOVE al usar StackExchange.Redis y agrupaciones en clústeres, ¿qué debo hacer?](#i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do)

### <a name="do-i-need-toomake-any-changes-toomy-client-application-toouse-clustering"></a>¿Es necesario toomake cualquier toouse de aplicación de cliente de cambios toomy de agrupación en clústeres?
* Cuando la agrupación en clústeres está habilitada, solo está disponible la base de datos 0. Si la aplicación cliente usa varias bases de datos e intenta tooread escritura tooa base de datos o distinto de 0, hello siguiente excepción se produce. `Unhandled Exception: StackExchange.Redis.RedisConnectionException: ProtocolFailure on GET --->``StackExchange.Redis.RedisCommandException: Multiple databases are not supported on this server; cannot switch toodatabase: 6`
  
  Para obtener más información, consulte [Redis Cluster Specification - Implemented subset](http://redis.io/topics/cluster-spec#implemented-subset)(Especificación de clúster en Redis: subconjunto implementado).
* Si usa [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/), debe usar la versión 1.0.481 o posterior. Conectar toohello caché usando Hola mismo [puntos de conexión, los puertos y las claves](cache-configure.md#properties) que usar cuando se conecta la memoria caché de tooa que no tiene habilitado de agrupación en clústeres. Hola única diferencia es que todas las lecturas y escrituras deben hacerse toodatabase 0.
  
  * Otros clientes pueden tener requisitos diferentes. Vea [¿Todos los clientes de Redis admiten la agrupación en clústeres?](#do-all-redis-clients-support-clustering)
* Si la aplicación usa varias operaciones claves por lotes en un único comando, todas las claves deben estar ubicadas en hello misma partición. ¿las claves de toolocate en Hola la misma partición, vea [cómo se distribuyen las claves en un clúster?](#how-are-keys-distributed-in-a-cluster)
* Si está usando el proveedor de estado de sesión de ASP.NET de Redis, debe usar 2.0.1 o posterior. ¿Vea [puedo usar clústeres con proveedores de estado de sesión de ASP.NET de Redis y almacenamiento en caché de salida de hello?](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)

### <a name="how-are-keys-distributed-in-a-cluster"></a>¿Cómo se distribuyen las claves en un clúster?
Por hello Redis [modelo de distribución de claves](http://redis.io/topics/cluster-spec#keys-distribution-model) documentación: espacio de claves de Hola se divide en las ranuras de 16384. Cada clave se aplica un algoritmo hash y asigna tooone de estas zonas, que se distribuyen en hello nodos de clúster de Hola. Puede configurar qué parte de la clave de hello es tooensure con algoritmo hash que se encuentran varias claves en Hola misma partición mediante etiquetas de hash.

* Claves con una etiqueta de hash: si se incluye a cualquier parte de la clave de hello en `{` y `}`, se aplica un algoritmo hash sólo esa parte de la clave de Hola para fines de Hola de determinar la ranura de hash de Hola de una clave. Por ejemplo, hello siguientes 3 claves debería encontrarse en hello misma partición: `{key}1`, `{key}2`, y `{key}3` desde sólo hello `key` parte del nombre de Hola se aplica un algoritmo hash. Para obtener una lista completa de especificaciones de etiquetas hash de claves, consulte [Etiquetas hash de claves](http://redis.io/topics/cluster-spec#keys-hash-tags).
* Claves sin una etiqueta de hash: nombre de clave completo de Hola se utiliza para crear valores hash. Esto produce una distribución uniforme estadísticamente entre las particiones de Hola de caché de Hola.

Para optimizar el rendimiento y el rendimiento, se recomienda distribuir las claves de hello uniformemente. Si usa claves con una etiqueta de hash es que las claves de la aplicación hello responsabilidad tooensure Hola se distribuyen uniformemente.

Para obtener más información, consulte [Modelo de distribución de claves](http://redis.io/topics/cluster-spec#keys-distribution-model), [Particionamiento de datos de clúster Redis](http://redis.io/topics/cluster-tutorial#redis-cluster-data-sharding) y [Etiquetas hash de claves](http://redis.io/topics/cluster-spec#keys-hash-tags).

Para el código de ejemplo sobre cómo trabajar con la agrupación en clústeres y buscar las claves en hello mismo particionamiento con cliente de StackExchange.Redis hello, vea hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) parte de hello [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) ejemplo.

### <a name="what-is-hello-largest-cache-size-i-can-create"></a>¿Cuál es el mayor tamaño de caché Hola que puedo crear?
tamaño de caché premium más grande de Hello es 53 GB. Puede crear hasta particiones too10 ofrecerle un tamaño máximo de 530 GB. Si necesita un tamaño mayor, puede [solicitar más](mailto:wapteams@microsoft.com?subject=Redis%20Cache%20quota%20increase). Para obtener más información, consulte [Precios de Caché en Redis de Azure](https://azure.microsoft.com/pricing/details/cache/).

### <a name="do-all-redis-clients-support-clustering"></a>¿Todos los clientes de Redis admiten la agrupación en clústeres?
En hello no todos los clientes admiten la hora actual Redis agrupación en clústeres. StackExchange.Redis es uno de los que los admiten. Para obtener más información sobre otros clientes, consulte hello [jugando con clúster de hello](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) sección de hello [tutorial de clúster de Redis](http://redis.io/topics/cluster-tutorial).

> [!NOTE]
> Si está utilizando StackExchange.Redis como el cliente, asegúrese de que usa la versión más reciente de Hola de [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/) 1.0.481 o una versión posterior de agrupación en clústeres toowork correctamente. Si tiene problemas con las excepciones move, consulte la explicación sobre [excepciones move](#move-exceptions) para obtener más información.
> 
> 

### <a name="how-do-i-connect-toomy-cache-when-clustering-is-enabled"></a>¿Cómo conecto toomy caché cuando se habilita la agrupación en clústeres?
Puede conectarse tooyour caché usando Hola mismo [extremos](cache-configure.md#properties), [puertos](cache-configure.md#properties), y [claves](cache-configure.md#access-keys) que usar cuando se conecta la memoria caché de tooa que no tiene habilitado de agrupación en clústeres. Redis administra Hola agrupación en clústeres en hello back-end para que no tenga toomanage desde el cliente.

### <a name="can-i-directly-connect-toohello-individual-shards-of-my-cache"></a>¿Puedo conectar directamente toohello particiones individuales de la memoria caché?
Esto no se admite oficialmente. Dicho esto, cada partición consta de un par de caché principal/réplica que se conoce colectivamente como una instancia de caché. Puede conectar toothese instancias de caché mediante la utilidad de redis cli de Hola Hola [inestable](http://redis.io/download) rama del repositorio de Redis hello en GitHub. Esta versión implementa la compatibilidad básica cuando se inició con hello `-c` cambiar. Para obtener más información, consulte [jugando con clúster de hello](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) en [http://redis.io](http://redis.io) en hello [tutorial de clúster de Redis](http://redis.io/topics/cluster-tutorial).

Para no ssl, use Hola siga los comandos.

    Redis-cli.exe –h <<cachename>> -p 13000 (tooconnect tooinstance 0)
    Redis-cli.exe –h <<cachename>> -p 13001 (tooconnect tooinstance 1)
    Redis-cli.exe –h <<cachename>> -p 13002 (tooconnect tooinstance 2)
    ...
    Redis-cli.exe –h <<cachename>> -p 1300N (tooconnect tooinstance N)

Para ssl, reemplace `1300N` por `1500N`.

### <a name="can-i-configure-clustering-for-a-previously-created-cache"></a>¿Puedo configurar la agrupación en clústeres para una memoria caché creada anteriormente?
En este momento solo puede habilitar la agrupación en clústeres cuando cree una memoria caché. Puede cambiar el tamaño del clúster Hola después de que se crea una caché hello, pero no se puede agregar memoria caché premium de agrupación en clústeres tooa o quitar el clúster de una caché premium después de que se crea una caché Hola. Una caché premium con clústeres habilitado y solo una partición es diferente de una caché premium de hello mismo tamaño con ninguna agrupación en clústeres.

### <a name="can-i-configure-clustering-for-a-basic-or-standard-cache"></a>¿Puedo configurar la agrupación en clústeres para una caché básica o estándar?
La agrupación en clústeres solo está disponible para las memorias cachés premium.

### <a name="can-i-use-clustering-with-hello-redis-aspnet-session-state-and-output-caching-providers"></a>¿Puedo usar la agrupación en clústeres con proveedores de estado de sesión de ASP.NET de Redis y almacenamiento en caché de salida de hello?
* **Proveedor de caché de salida de Redis** : no se requieren cambios.
* **Proveedor de estado de sesión de Redis** -toouse agrupación en clústeres, debe usar [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 o superior o una excepción se produce. Este es un cambio importante. Para obtener más información, consulte [v2.0.0 Breaking Change Details](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details) (Detalles sobre cambios importantes de la versión 2.0.0).

<a name="move-exceptions"></a>

### <a name="i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do"></a>Estoy recibiendo excepciones MOVE al usar StackExchange.Redis y agrupaciones en clústeres, ¿qué debo hacer?
Si utiliza StackExchange.Redis y recibe `MOVE` excepciones al emplear agrupaciones en clústeres, asegúrese de que está utilizando la versión [1.1.603 de StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/) o posterior. Para obtener instrucciones acerca de cómo configurar su toouse de las aplicaciones de .NET StackExchange.Redis, consulte [configurar clientes de caché de hello](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).

## <a name="next-steps"></a>Pasos siguientes
Obtenga información acerca de cómo toouse premium más características de caché.

* [Nivel de introducción toohello Premium de caché de Redis de Azure](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-clustering]: ./media/cache-how-to-premium-clustering/redis-cache-clustering.png

[redis-cache-clustering-selected]: ./media/cache-how-to-premium-clustering/redis-cache-clustering-selected.png

[redis-cache-redis-cluster-size]: ./media/cache-how-to-premium-clustering/redis-cache-redis-cluster-size.png







