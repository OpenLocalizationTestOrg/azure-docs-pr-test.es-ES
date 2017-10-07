---
title: "ejemplos de caché en Redis aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Redis de Azure almacenan en caché"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1f8d210c-ee09-4fe2-b63f-1e69246a27d8
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 5cf9287b577758b5d880d1ca3928c1bee643a8ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-samples"></a>Ejemplos de Caché en Redis de Azure
En este tema se proporciona una lista de ejemplos de caché en Redis de Azure, que tratan escenarios como conectar caché tooa, leer y escribir datos tooand desde una memoria caché y usar proveedores de caché en Redis ASP.NET Hola. Algunos ejemplos de hello son proyectos descargables, y algunos proporcionan instrucciones paso a paso e incluyan fragmentos de código, pero no crear vínculo proyecto descargable tooa.

## <a name="hello-world-samples"></a>Ejemplos Hello world
ejemplos de Hello en esta sección muestran los conceptos básicos de Hola de conectar la instancia del servicio Azure Redis Cache tooan lectura y escritura y memoria caché de toohello de datos mediante una variedad de lenguajes y clientes de Redis.

Hola [Hola a todos](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) ejemplo muestra cómo tooperform varias operaciones mediante Hola de caché [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cliente. NET.

Este ejemplo lo siguiente:

* Uso de distintas opciones de conexión
* Leer y escribir objetos tooand de memoria caché de hello mediante operaciones sincrónicas y asincrónicas
* Usar Redis MGET/MSET comandos tooreturn valores de claves especificados
* Realización de operaciones transaccionales de Redis
* Trabajo con listas de Redis y conjuntos ordenados
* Almacenamiento de objetos de .NET con serializadores JsonConvert
* Usar Redis establece tooimplement etiquetado
* Trabajar con el Clúster en Redis

Para obtener más información, vea hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) consulte la documentación de github y los escenarios de uso más hello [StackExchange.Redis.Tests](https://github.com/StackExchange/StackExchange.Redis/tree/master/StackExchange.Redis.Tests) pruebas unitarias.

[Cómo toouse caché de Redis de Azure con Python](cache-python-get-started.md) muestra cómo se inició con caché en Redis de Azure con Python y hello tooget [redis copiar](https://github.com/andymccurdy/redis-py) cliente.

[Trabajar con objetos de .NET en memoria caché de hello](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache) muestra es una manera de tooserialize .NET objetos por lo que puede escribir tooand leerlos desde una instancia de caché en Redis de Azure. 

## <a name="use-redis-cache-as-a-scale-out-backplane-for-aspnet-signalr"></a>Uso de Caché en Redis como un backplane de escalado horizontal para ASP.NET SignalRen
Hola [usar caché en Redis como una escalada Backplane para ASP.NET SignalR](https://github.com/rustd/RedisSamples/tree/master/RedisAsSignalRBackplane) ejemplo muestra cómo puede usar caché en Redis de Azure como backplane de SignalR. Para obtener más información acerca de backplane, consulte [Escalado horizontal SignalR con Redis](http://www.asp.net/signalr/overview/performance/scaleout-with-redis).

## <a name="redis-cache-customer-query-sample"></a>Ejemplo de consulta de cliente de Caché en Redis
Este ejemplo compara el rendimiento entre el acceso a datos desde una memoria caché y el acceso a datos desde almacenamiento de persistencia. Este ejemplo tiene dos proyectos.

* [Demostración de cómo Caché en Redis puede mejorar el rendimiento almacenando datos en caché](https://github.com/rustd/RedisSamples/tree/master/RedisCacheCustomerQuerySample)
* [Valor de inicialización Hola base de datos y caché de demostración de hello](https://github.com/rustd/RedisSamples/tree/master/SeedCacheForCustomerQuerySample)

## <a name="aspnet-session-state-and-output-caching"></a>Estado de sesión de ASP.NET y almacenamiento en caché de resultados
Hola [toostore usar caché de Redis de Azure SessionState de ASP.NET y OutputCache](https://github.com/rustd/RedisSamples/tree/master/SessionState_OutputCaching) ejemplo muestra cómo se toouse Azure Redis Cache toostore sesión ASP.NET y el uso de memoria caché de resultados Hola SessionState y OutputCache proveedores para Redis.

## <a name="manage-azure-redis-cache-with-maml"></a>Administración de Caché en Redis de Azure con Azure MAML
Hola [administrar Azure Redis Cache mediante las bibliotecas de administración de Azure](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) ejemplo muestra cómo puede utilizar las bibliotecas de administración de Azure toomanage - (crear / actualizar / eliminar) la memoria caché. 

## <a name="custom-monitoring-sample"></a>Ejemplo de personalización de supervisión
Hola [datos de supervisión de caché de Redis de acceso](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) ejemplo muestra cómo tener acceso a datos de supervisión de la memoria caché Redis de Azure fuera Hola Portal de Azure.

## <a name="a-twitter-style-clone-written-using-php-and-redis"></a>Un clon de estilo Twitter escrito mediante PHP y Redis
Hola [Retwis](https://github.com/SyntaxC4-MSFT/retwis) ejemplo es hello Redis Hello World. Es un clon de redes sociales de Twitter estilo mínimo escrito mediante Redis y PHP con hello [Predis](https://github.com/nrk/predis) cliente. código fuente de Hello es diseñada toobe muy simple y en hello mismo tiempo tooshow diferentes estructuras de datos de Redis.

## <a name="bandwidth-monitor"></a>Supervisión del ancho de banda
Hola [monitor de ancho de banda](https://github.com/JonCole/SampleCode/tree/master/BandWidthMonitor) ejemplo permite toomonitor de ancho de banda de hello utilizado en el cliente de Hola. toomeasure Hola ancho de banda, ejecutar el ejemplo hello en el equipo de cliente de caché de Hola, realizar llamadas toohello caché y observar el ancho de banda de hello notificado por el ejemplo hello del monitor de ancho de banda.

