---
title: "aaaHow tooUse caché en Redis de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooimprove Hola rendimiento de las aplicaciones de Azure con caché en Redis de Azure"
services: redis-cache,app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c502f74c-44de-4087-8303-1b1f43da12d5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 763d70c10972eec9a1885969e8da5bf1c4084727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache"></a>Cómo tooUse Redis de Azure almacenan en caché
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Esta guía le mostrará cómo tooget a usar **Azure Redis Cache**. Caché en Redis de Microsoft Azure se basa en código abierto populares de hello caché en Redis. Proporciona acceso a tooa dedicado Redis caché segura, administrada por Microsoft. Una caché creada con Azure Redis Cache es accesible desde cualquier aplicación dentro de Microsoft Azure.

Caché en Redis de Microsoft Azure está disponible en hello siguientes niveles:

* **Básico** – Nodo único. Varios tamaños de too53 GB.
* **Estándar**: principal/réplica de dos nodos. Varios tamaños de too53 GB. Contrato de nivel de servicio del 99,9 %.
* **Premium** : dos nodos principal/réplica con too10 particiones. Varios tamaños de 6 GB too530 GB. Todas las características del nivel Estándar y algunas otras características son compatibles con los [clústeres de Redis](cache-how-to-premium-clustering.md), la [persistencia de Redis](cache-how-to-premium-persistence.md) y [Azure Virtual Network](cache-how-to-premium-vnet.md). Contrato de nivel de servicio del 99,9 %.

Estos niveles difieren en las características y el precio. Para más información sobre los precios, consulte los [precios de caché][Cache Pricing Details].

Esta guía le mostrará cómo hello toouse [StackExchange.Redis] [ StackExchange.Redis] cliente mediante C\# código. Hello escenarios descritos se incluyen **crear y configurar una memoria caché**, **configurar clientes de caché**, y **agregando y quitando objetos de caché de hello**. Para más información sobre el uso de Azure Redis Cache, consulte [Pasos siguientes][Next Steps]. Para obtener un tutorial paso a paso de la creación una ASP.NET MVC de aplicación web con caché en Redis, vea [cómo toocreate una aplicación Web con caché en Redis](cache-web-app-howto.md).

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a>Introducción a Azure Redis Cache
Empezar a trabajar con Azure Redis Cache es fácil. tooget iniciado, hacer provisioning y configurar una memoria caché. A continuación, configure los clientes de caché de Hola por lo que puede tener acceso a la memoria caché de Hola. Después de configuran los clientes de caché de hello, puede empezar a trabajar con ellos.

* [Crear la memoria caché de Hola][Create hello cache]
* [Configurar a clientes de caché de Hola][Configure hello cache clients]

<a name="create-cache"></a>

## <a name="create-a-cache"></a>Creación de una caché
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a>tooaccess se crea en la memoria caché después de él
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

Para obtener más información acerca de cómo configurar la memoria caché, vea [cómo tooconfigure Azure Redis Cache](cache-configure.md).

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a>Configurar a clientes de caché de Hola
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

Una vez que el proyecto de cliente está configurado para almacenar en caché, puede usar técnicas de hello descritas en las siguientes secciones para trabajar con la memoria caché de Hola.

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a>Trabajo con cachés
pasos de Hello en esta sección describe cómo las tareas comunes de tooperform con memoria caché.

* [Conectar toohello caché][Connect toohello cache]
* [Agregar y recuperar objetos de caché de Hola][Add and retrieve objects from hello cache]
* [Trabajar con objetos de .NET en memoria caché de Hola](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a>Conectar toohello caché
trabajo de tooprogrammatically con una memoria caché, tiene una memoria caché toohello de referencia. Agregar Hola después de la parte superior de toohello de cualquier archivo desde el que desea toouse hello StackExchange.Redis cliente tooaccess una caché en Redis de Azure.

    using StackExchange.Redis;

> [!NOTE]
> cliente de Hello StackExchange.Redis requiere .NET Framework 4 o posterior.
> 
> 

Hola toohello conexión caché en Redis de Azure está administrado por hello `ConnectionMultiplexer` clase. Esta clase se debe compartir y reutiliza a lo largo de la aplicación cliente y no es necesario toobe creado en cada operación. 

tooconnect tooan caché en Redis de Azure y devolver una instancia de un `ConnectionMultiplexer`, llamada Hola estático `Connect` método y pase Hola caché extremo y la clave. Usar clave Hola generado a partir de portal de Azure como parámetro de contraseña de Hola Hola.

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> Advertencia: nunca almacene credenciales en el código fuente. tookeep este sencillo ejemplo, estoy mostrarlos en código fuente de Hola. Vea [cómo las cadenas de la aplicación y el trabajo de las cadenas de conexión] [ How Application Strings and Connection Strings Work] para obtener información acerca de cómo toostore credenciales.
> 
> 

Si no desea toouse SSL, establezca `ssl=false` u omitir hello `ssl` parámetro.

> [!NOTE]
> puerto no SSL de Hello está deshabilitado de forma predeterminada para las nuevas cachés. Para obtener instrucciones acerca de cómo habilitar el puerto no SSL de hello, consulte [puertos de acceso](cache-configure.md#access-ports).
> 
> 

Un enfoque toosharing una `ConnectionMultiplexer` las instancias de la aplicación es toohave una propiedad estática que devuelve una instancia conectada, similar toohello siguiente ejemplo. Este enfoque proporciona una manera segura para subprocesos tooinitialize sólo un único conectado `ConnectionMultiplexer` instancia. En estos ejemplos `abortConnect` es toofalse de conjunto, lo que significa que la llamada de hello es correcta incluso si no se establece un toohello conexión caché en Redis de Azure. Una característica clave de `ConnectionMultiplexer` es que restaurará automáticamente caché de conectividad toohello una vez que el problema de red de Hola o por otros motivos se resuelven.

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

Para más información sobre las opciones de configuración de conexión avanzadas, consulte el artículo sobre el [modelo de configuración de StackExchange.Redis][StackExchange.Redis configuration model].

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

Una vez establecida la conexión de hello, devolver una base de datos de caché de referencia toohello redis Hola llamada `ConnectionMultiplexer.GetDatabase` método. Devuelve el objeto de Hola de hello `GetDatabase` método es un objeto ligero de acceso directo y no es necesario toobe almacenado.

    // Connection refers tooa property that returns a ConnectionMultiplexer
    // as shown in hello previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using hello cache object...
    // Simple put of integral data types into hello cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from hello cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

Las memorias caché de Redis de Azure tienen un número configurable de bases de datos (valor predeterminado de 16) que pueden ser datos de hello independiente toologically utilizados dentro de una caché de Redis. Para más información, consulte [What are Redis databases?](cache-faq.md#what-are-redis-databases) (¿Qué son las bases de datos de Redis?) y [Configuración predeterminada del servidor Redis](cache-configure.md#default-redis-server-configuration).

Ahora que sabe cómo caché de base de datos de instancia de caché en Redis de Azure de tooconnect tooan y devuelven una referencia toohello, echemos un vistazo a trabajar con la memoria caché de Hola.

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a>Agregar y recuperar objetos de caché de Hola
Los elementos se pueden almacenar en y recupera desde una memoria caché con hello `StringSet` y `StringGet` métodos.

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

Redis almacenes de mayoría de los datos como cadenas de Redis, sino que estas cadenas puede contener muchos tipos de datos, incluidos los datos binarios serializados, que se pueden usar al almacenar .NET objetos en memoria caché de Hola.

Al llamar a `StringGet`, si existe un objeto hello, se devuelve, y si no es así, `null` se devuelve. Si `null` se devuelve, puede recuperar el valor de Hola Hola deseado origen de datos y almacenar en memoria caché de Hola para su uso posterior. Este patrón de uso se conoce como modelo de cache-aside Hola.

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

También puede usar `RedisValue`, tal y como se muestra en el siguiente ejemplo de Hola. `RedisValue` tiene operadores implícitos para trabajar con tipos de datos enteros y puede ser útil si `null` es un valor esperado para un elemento almacenado en caché.


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


expiración de hello toospecify de un elemento en caché de hello, use hello `TimeSpan` parámetro de `StringSet`.

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a>Trabajar con objetos de .NET en memoria caché de Hola
Azure Redis Cache puede almacenar en caché objetos .NET así como tipos de datos primitivos, pero antes de poder almacenar en caché un objeto .NET, se debe serializar. Esta serialización de objetos .NET es responsabilidad de hello del desarrollador de la aplicación hello y le ofrece flexibilidad de desarrollador de hello en la elección de Hola de serializador de Hola.

Objetos de tooserialize de una manera sencilla es hello toouse `JsonConvert` métodos de serialización en [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) y serializar tooand de JSON. Hello en el ejemplo siguiente se muestra un get y set utilizando un `Employee` instancia del objeto.

    class Employee
    {
        public int Id { get; set; }
        public string Name { get; set; }

        public Employee(int EmployeeId, string Name)
        {
            this.Id = EmployeeId;
            this.Name = Name;
        }
    }

    // Store toocache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a>Pasos siguientes
Ahora que conoce los fundamentos de hello, siga estas toolearn de vínculos más información acerca de la caché en Redis de Azure.

* Desproteger Hola proveedores ASP.NET para caché en Redis de Azure.
  * [Proveedor de estado de sesión de Redis de Azure](cache-aspnet-session-state-provider.md)
  * [Proveedor de caché de resultados de ASP.NET de caché en Redis de Azure](cache-aspnet-output-cache-provider.md)
* [Habilitar los diagnósticos de caché](cache-how-to-monitor.md#enable-cache-diagnostics) para que pueda [monitor](cache-how-to-monitor.md) Hola estado de la memoria caché. Puede ver hello las métricas de hello portal de Azure y también pueden [descargar y revisar](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) mediante herramientas de Hola de su elección.
* Extraer del repositorio hello [documentación del cliente de caché de StackExchange.Redis][StackExchange.Redis cache client documentation].
  * Se puede obtener acceso a Azure Redis Cache desde numerosos clientes de Redis y lenguajes de desarrollo. Para más información, consulte [http://redis.io/clients][http://redis.io/clients].
* Azure Redis Cache puede utilizarse también con herramientas como Redsmin y Redis Desktop Manager y servicios de terceros.
  * Para obtener más información sobre Redsmin, consulte [cómo tooretrieve una conexión a Redis de Azure, de cadena y usarlo con Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].
  * Acceda e inspeccione los datos en Azure Redis Cache con una GUI mediante [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).
* Vea hello [redis] [ redis] documentación y obtener información acerca de [tipos de datos de redis] [ redis data types] y [una introducción de quince minutos tipos de datos de tooRedis][a fifteen minute introduction tooRedis data types].

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction tooAzure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project tooUse Azure Caching]: #prepare-vs
[Configure Your Application tooUse Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create hello cache]: #create-cache
[Configure hello cache]: #enable-caching
[Configure hello cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect toohello cache]: #connect-to-cache
[Add and retrieve objects from hello cache]: #add-object
[Specify hello expiration of an object in hello cache]: #specify-expiration
[Store ASP.NET session state in hello cache]: #store-session


<!-- IMAGES -->


[StackExchangeNuget]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-stackexchange-redis.png

[NuGetMenu]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-nuget-menu.png

[CacheProperties]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-properties.png

[ManageKeys]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-keys.png

[SessionStateNuGet]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-session-state-provider.png

[BrowseCaches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-browse-caches.png

[Caches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-caches.png







<!-- LINKS -->
[http://redis.io/clients]: http://redis.io/clients
[Develop in other languages for Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn690470.aspx
[How tooretrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How tooConfigure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set hello Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in hello cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate tooAzure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups toomanage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction tooRedis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/


