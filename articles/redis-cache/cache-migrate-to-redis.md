---
title: "aaaMigrate tooRedis de aplicaciones de servicio de caché administrado - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomigrate administra el servicio de caché y caché en rol de aplicaciones tooAzure caché en Redis"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 041f077b-8c8e-4d7c-a3fc-89d334ed70d6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/30/2017
ms.author: sdanie
ms.openlocfilehash: bd81722820acf0d2637828fbb6100c723aafeba5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-managed-cache-service-tooazure-redis-cache"></a>Migrar desde el servicio de caché administrado tooAzure caché en Redis
Migrar las aplicaciones que usan el servicio de caché administrado de Azure tooAzure caché en Redis se puede lograr con cambios mínimos tooyour aplicación, en función características del servicio de caché administrado de Hola usadas por la aplicación de almacenamiento en caché. Aunque Hola API no son exactamente Hola mismo son similares y gran parte del código existente que utiliza el servicio de caché administrado tooaccess una memoria caché se puede reutilizar con cambios mínimos. En este tema muestra cómo configuración de aplicación y toomake Hola necesarios cambia toomigrate su toouse de aplicaciones de servicio de caché administrado caché en Redis de Azure y muestra cómo algunas de las características de Hola de caché en Redis de Azure pueden ser usado tooimplement Hola funcionalidad de una memoria caché del servicio de caché administrado.

>[!NOTE]
>Managed Cache Service e In-Role Cache se [retiraron](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/) el 30 de noviembre de 2016. Si dispone de todas las implementaciones de caché en rol que desea toomigrate tooAzure caché en Redis, puede seguir los pasos de hello en este artículo.

## <a name="migration-steps"></a>Pasos de migración
Hola pasos es necesario toomigrate una toouse de aplicación de servicio de caché administrado caché en Redis de Azure.

* Asignar tooAzure de características de servicio de caché administrado caché en Redis
* Elegir una oferta de caché
* Creación de una caché
* Configurar a clientes de caché de Hola
  * Quitar la configuración del servicio de caché administrado de Hola
  * Configurar a un cliente de caché mediante Hola paquete de NuGet StackExchange.Redis
* Migración del código del Servicio de caché administrado
  * Conectarse mediante la clase ConnectionMultiplexer de hello de caché de toohello
  * Tipos de datos primitivos de acceso en la memoria caché de Hola
  * Trabajar con objetos de .NET en memoria caché de Hola
* Migrar el estado de sesión de ASP.NET y tooAzure caché en Redis de caché de resultados 

## <a name="map-managed-cache-service-features-tooazure-redis-cache"></a>Asignar tooAzure de características de servicio de caché administrado caché en Redis
El Servicio de caché administrado de Azure y Caché en Redis de Azure guardan ciertas semejanzas pero implementan algunas de sus características de formas diferentes. En esta sección se describe algunas de las diferencias de Hola y proporciona instrucciones sobre cómo implementar características de Hola de servicio de caché administrado en caché en Redis de Azure.

| Características del Servicio de caché administrado | Compatibilidad con el Servicio de caché administrado | Compatibilidad con Caché en Redis de Azure |
| --- | --- | --- |
| Cachés con nombre |Una memoria caché predeterminada está configurada y en hello pueden configurarse ofertas estándar y Premium, la toonine adicional cachés con nombre si lo desea. |Las memorias caché de Redis de Azure tienen un número configurable de bases de datos (valor predeterminado de 16) que pueden ser utilizado tooimplement almacena en memoria caché en un toonamed funcionalidad similar. Para más información, consulte [What are Redis databases?](cache-faq.md#what-are-redis-databases) (¿Qué son las bases de datos de Redis?) y [Configuración predeterminada del servidor Redis](cache-configure.md#default-redis-server-configuration). |
| Alta disponibilidad |Proporciona alta disponibilidad para los elementos en caché de hello en hello ofertas estándar y Premium. Si los elementos se pierde debido a error tooa, copias de seguridad de elementos de hello en memoria caché de hello siguen estando disponibles. Escribe la caché secundaria toohello se realiza sincrónicamente. |Alta disponibilidad está disponible en hello ofertas estándar y Premium, que tienen una configuración de la réplica principal de dos nodos (cada partición en una caché Premium tiene un par de réplica principal). Escrituras toohello réplica se realizan de forma asincrónica. Para obtener más información, consulte [Precios de Azure Redis Cache](https://azure.microsoft.com/pricing/details/cache/). |
| Notificaciones |Permite que se producen notificaciones asincrónicas de los clientes tooreceive cuando una serie de operaciones de caché en una caché con nombre. |Aplicaciones cliente pueden utilizar Redis pub/sub o [las notificaciones de Keyspace](cache-configure.md#keyspace-notifications-advanced-settings) tooachieve un toonotifications funcionalidad similar. |
| Caché local |Almacena una copia de los objetos almacenados en caché localmente en el cliente de Hola para un acceso muy rápido. |Las aplicaciones cliente necesitaría tooimplement esta funcionalidad mediante un diccionario o una estructura de datos similar. |
| Directiva de expulsión |Ninguna o LRU. directiva predeterminada de Hello es LRU. |Caché en Redis de Azure admite las siguientes directivas de expulsión de hello: volatile-lru, lru allkeys, volátil aleatorio, allkeys aleatorio volátil-ttl, noeviction. directiva predeterminada de Hello es volatile-lru. Para obtener más información, consulte [Configuración de servidor predeterminada en Redis](cache-configure.md#default-redis-server-configuration). |
| Directiva de caducidad |Directiva de caducidad de Hello predeterminada es Absolute e intervalo de expiración de saludo predeterminado es de diez minutos. También hay directivas variable y Nunca. |De forma predeterminada no expiran los elementos en caché de hello, pero una expiración puede configurarse de forma por escritura mediante sobrecargas de conjunto de caché. Para obtener más información, consulte [agregar y recuperar objetos de caché de hello](cache-dotnet-how-to-use-azure-redis-cache.md#add-and-retrieve-objects-from-the-cache). |
| Regiones y etiquetado |Las regiones son subgrupos de elementos en caché. Las regiones admiten también anotación Hola de elementos almacenados en caché con cadenas descriptivas adicionales llamadas etiquetas. Las regiones admiten operaciones de búsqueda de tooperform de capacidad de hello en elementos etiquetados en dicha región. Todos los elementos dentro de una región se encuentran dentro de un único nodo del clúster de caché de Hola. |Una caché en Redis consta de un solo nodo (a menos que se habilite Redis clúster) por lo que no hay ningún concepto de Hola de regiones de servicio de caché administrado. Redis admite búsqueda y operaciones de caracteres comodín al recuperar las claves para que etiquetas descriptivas se pueden incrustar en los nombres de clave de Hola y usan elementos de hello tooretrieve más adelante. Para ver un ejemplo de la implementación de una solución de etiquetado con Redis, consulte [Implementing cache tagging with Redis](http://stackify.com/implementing-cache-tagging-redis/)(Implementación del etiquetado de caché con Redis). |
| Serialización |Caché administrada admite NetDataContractSerializer, BinaryFormatter y uso de Hola de serializadores personalizados. valor predeterminado de Hello es NetDataContractSerializer. |Es responsabilidad de Hola Hola aplicación tooserialize .NET de objetos de cliente antes de colocarlos en la memoria caché de hello, con la elección de Hola de serializador de hello seguridad toohello programador de aplicaciones de cliente. Para obtener más información y código de ejemplo, vea [trabajar con objetos de .NET en memoria caché de hello](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache). |
| Emulador de caché |El servicio de caché administrado ofrece un emulador de la memoria caché local. |Caché en Redis de Azure no tiene un emulador, pero puede [crear hello MSOpenTech de redis server.exe localmente](cache-faq.md#cache-emulator) tooprovide una experiencia con el emulador. |

## <a name="choose-a-cache-offering"></a>Elegir una oferta de caché
Caché en Redis de Microsoft Azure está disponible en hello siguientes niveles:

* **Básico** – Nodo único. Varios tamaños de too53 GB.
* **Estándar**: principal/réplica de dos nodos. Varios tamaños de too53 GB. Contrato de nivel de servicio del 99,9 %.
* **Premium** : dos nodos principal/réplica con too10 particiones. Varios tamaños de 6 GB too530 GB. Todas las características del nivel Estándar y algunas otras características son compatibles con los [clústeres de Redis](cache-how-to-premium-clustering.md), la [persistencia de Redis](cache-how-to-premium-persistence.md) y [Azure Virtual Network](cache-how-to-premium-vnet.md). Contrato de nivel de servicio del 99,9 %.

Estos niveles difieren en las características y el precio. Hello características se tratan más adelante en esta guía y para obtener más información sobre los precios, consulte [detalles de precios de caché](https://azure.microsoft.com/pricing/details/cache/).

Un punto de partida para la migración es toopick Hola tamaño que coincide con el tamaño de hello de la caché de servicio de caché administrado anterior y, a continuación, escalar hacia arriba o hacia abajo según los requisitos de saludo de la aplicación. Para obtener instrucciones sobre cómo elegir Hola derecho oferta de caché en Redis de Azure, vea [qué oferta de caché de Redis y tamaño debo usar?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).

## <a name="create-a-cache"></a>Creación de una caché
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="configure-hello-cache-clients"></a>Configurar a clientes de caché de Hola
Una vez creada y configurada la memoria caché de hello, paso siguiente hello es configuración de servicio de caché administrado de hello tooremove y agregar Hola Agregar configuración de caché en Redis de Azure de Hola y las referencias para que los clientes de caché pueden tener acceso a la memoria caché de Hola.

* Quitar la configuración del servicio de caché administrado de Hola
* Configurar a un cliente de caché mediante Hola paquete de NuGet StackExchange.Redis

### <a name="remove-hello-managed-cache-service-configuration"></a>Quitar la configuración del servicio de caché administrado de Hola
Antes de hello las aplicaciones cliente pueden configurarse para caché en Redis de Azure, configuración de servicio de caché administrado de hello existente y se deben quitar las referencias de ensamblado desinstalando paquete de NuGet del servicio de caché administrado de Hola.

Hola toouninstall paquete de NuGet del servicio de caché administrado, haga clic en proyecto de cliente de hello en **el Explorador de soluciones** y elija **administrar paquetes de NuGet**. Seleccione hello **paquetes instalados** nodo y tipo W**indowsAzure.Caching** en hello búsqueda instalado cuadro paquetes. Seleccione **Windows** **caché de Azure** (o **Windows** **Caching de Azure** según versión Hola de paquete de NuGet hello), haga clic en  **Desinstalar**y, a continuación, haga clic en **cerrar**.

![Desinstalar paquetes NuGet de Azure Managed Cache Service](./media/cache-migrate-to-redis/IC757666.jpg)

Desinstalar paquete de NuGet del servicio de caché administrado de hello quita ensamblados de servicio de caché administrado de Hola y las entradas del servicio de caché administrado de hello en hello app.config o web.config de la aplicación de cliente de Hola. Porque no se pueden quitar algunas opciones personalizadas cuando se desinstala el paquete de NuGet hello, abra web.config o app.config y asegúrese de que Hola siguientes elementos se quitan por completo.

Asegúrese de que hello `dataCacheClients` entrada se elimina de hello `configSections` elemento. No quite todo hello `configSections` elemento; simplemente quitar hello `dataCacheClients` entrada, si está presente.

```xml
<configSections>
  <!-- Existing sections omitted for clarity. -->
  <section name="dataCacheClients"type="Microsoft.ApplicationServer.Caching.DataCacheClientsSection, Microsoft.ApplicationServer.Caching.Core" allowLocation="true" allowDefinition="Everywhere"/>
</configSections>
```

Asegúrese de que hello `dataCacheClients` se quita la sección. Hola `dataCacheClients` sección será similar toohello siguiente ejemplo.

```xml
<dataCacheClients>
  <dataCacheClientname="default">
    <!--toouse hello in-role flavor of Azure Cache, set identifier toobe hello cache cluster role name -->
    <!--toouse hello Azure Managed Cache Service, set identifier toobe hello endpoint of hello cache cluster -->
    <autoDiscoverisEnabled="true"identifier="[Cache role name or Service Endpoint]"/>

    <!--<localCache isEnabled="true" sync="TimeoutBased" objectCount="100000" ttlValue="300" />-->
    <!--Use this section toospecify security settings for connecting tooyour cache. This section is not required if your cache is hosted on a role that is a part of your cloud service. -->
    <!--<securityProperties mode="Message" sslEnabled="true">
      <messageSecurity authorizationInfo="[Authentication Key]" />
    </securityProperties>-->
  </dataCacheClient>
</dataCacheClients>
```

Una vez que se quita la configuración del servicio de caché administrado de hello, puede configurar el cliente de caché de Hola tal y como se describe en los pasos de la sección de Hola.

### <a name="configure-a-cache-client-using-hello-stackexchangeredis-nuget-package"></a>Configurar a un cliente de caché mediante Hola paquete de NuGet StackExchange.Redis
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

## <a name="migrate-managed-cache-service-code"></a>Migración del código del Servicio de caché administrado
API de Hello para el cliente de caché de StackExchange.Redis Hola es toohello similar el servicio de caché administrado. Esta sección proporciona información general sobre las diferencias de Hola.

### <a name="connect-toohello-cache-using-hello-connectionmultiplexer-class"></a>Conectarse mediante la clase ConnectionMultiplexer de hello de caché de toohello
En el servicio de caché administrado, Hola administró caché de conexiones toohello `DataCacheFactory` y `DataCache` clases. En la caché en Redis de Azure, estas conexiones se administrarán hello `ConnectionMultiplexer` clase.

Agregue Hola siguientes mediante la instrucción toohello superior de cualquier archivo del que desea tooaccess Hola caché.

```c#
using StackExchange.Redis
```

Si no se resuelve este espacio de nombres, asegúrese de que ha agregado Hola paquete de StackExchange.Redis NuGet tal y como se describe en [configurar clientes de caché de hello](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).

> [!NOTE]
> Tenga en cuenta que el cliente hello StackExchange.Redis requiere .NET Framework 4 o posterior.
> 
> 

instancia del servicio Azure Redis Cache tooconnect tooan, llamada Hola estático `ConnectionMultiplexer.Connect` método y pase el extremo de Hola y la clave. Un enfoque toosharing una `ConnectionMultiplexer` las instancias de la aplicación es toohave una propiedad estática que devuelve una instancia conectada, similar toohello siguiente ejemplo. Esto proporciona una manera segura para subprocesos tooinitialize sólo un único conectado `ConnectionMultiplexer` instancia. En este ejemplo `abortConnect` es toofalse de conjunto, lo que significa que llamada Hola tendrá éxito aun cuando no se establece una memoria caché toohello de conexión. Una característica clave de `ConnectionMultiplexer` es que automáticamente restaurará la memoria caché de conectividad toohello una vez que el problema de red de Hola o por otros motivos se resuelven.

```c#
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
```

Hello extremo de la caché, las claves y los puertos pueden obtenerse de hello **caché en Redis** hoja para la instancia de caché. Para obtener más información, consulte [Propiedades de Caché en Redis](cache-configure.md#properties).

Una vez establecida la conexión de hello, devolver una base de datos de caché de referencia toohello Redis Hola llamada `ConnectionMultiplexer.GetDatabase` método. Devuelve el objeto de Hola de hello `GetDatabase` método es un objeto ligero de acceso directo y no es necesario toobe almacenado.

```c#
IDatabase cache = Connection.GetDatabase();

// Perform cache operations using hello cache object...
// Simple put of integral data types into hello cache
cache.StringSet("key1", "value");
cache.StringSet("key2", 25);

// Simple get of data types from hello cache
string key1 = cache.StringGet("key1");
int key2 = (int)cache.StringGet("key2");
```

cliente de StackExchange.Redis de Hello usa hello `RedisKey` y `RedisValue` tipos para tener acceso a elementos y almacenarlos en caché de Hola. Estos tipos se asignan a tipos de lenguajes más primitivos, como la cadena, y no suelen usarse directamente. Redis cadenas son Hola clase más básica del valor de Redis y pueden contener muchos tipos de datos, incluidas secuencias binarias serializadas, y aunque no puede usar tipo hello directamente, usará métodos que contienen `String` en nombre de Hola. Para los tipos de datos primitivos más almacenar y recuperar elementos de caché de hello utilizando hello `StringSet` y `StringGet` métodos, a menos que se va a almacenar colecciones u otros tipos de datos de Redis en memoria caché de Hola. 

`StringSet`y `StringGet` son muy similar toohello servicio de caché administrado `Put` y `Get` métodos, con la principal diferencia radica en que antes de establecer y obtener un objeto .NET en la memoria caché de Hola debe serializar en primer lugar. 

Al llamar a `StringGet`, si existe un objeto hello, se devuelve y si no es así, se devuelve null. En este caso puede recuperar el valor de Hola Hola deseado origen de datos y almacenar en memoria caché de Hola para su uso posterior. Esto se conoce como modelo de cache-aside Hola.

expiración de hello toospecify de un elemento en caché de hello, use hello `TimeSpan` parámetro de `StringSet`.

```c#
cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));
```

Caché en Redis de Azure puede trabajar con objetos .NET, así como con tipos de datos primitivos; sin embargo, antes de poder almacenar en caché un objeto .NET, se debe serializar. Esto es responsabilidad de hello del desarrollador de la aplicación hello. Esto proporciona flexibilidad de desarrollador de hello en la elección de Hola de serializador de Hola. Para obtener más información y código de ejemplo, vea [trabajar con objetos de .NET en memoria caché de hello](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).

## <a name="migrate-aspnet-session-state-and-output-caching-tooazure-redis-cache"></a>Migrar el estado de sesión de ASP.NET y tooAzure caché en Redis de caché de resultados
Caché en Redis de Azure cuenta con proveedores de estado de sesión ASP.NET y almacenamiento en caché de los resultados de las páginas. toomigrate la aplicación que utiliza las versiones de servicio de caché administrado de Hola de estos proveedores, quite primero hello las secciones existentes del archivo web.config y, a continuación, configurar versiones de caché en Redis de Azure de Hola de proveedores de Hola. Para obtener instrucciones sobre el uso de hello proveedores de ASP.NET de caché de Redis de Azure, consulte [proveedor de estado de sesión de ASP.NET para caché en Redis de Azure](cache-aspnet-session-state-provider.md) y [proveedor de caché de resultados de ASP.NET para caché en Redis de Azure](cache-aspnet-output-cache-provider.md).

## <a name="next-steps"></a>Pasos siguientes
Explorar hello [documentación de Azure Redis Cache](https://azure.microsoft.com/documentation/services/cache/) para tutoriales, ejemplos y vídeos entre otros.

