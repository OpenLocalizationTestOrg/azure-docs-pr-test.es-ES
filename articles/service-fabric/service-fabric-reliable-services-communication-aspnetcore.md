---
title: "comunicación aaaService con hello ASP.NET Core | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse ASP.NET principales en servicios de confianza y sin estado."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 8aa4668d-cbb6-4225-bd2d-ab5925a868f2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/02/2017
ms.author: vturecek
ms.openlocfilehash: 6e6a83ab04390150292f63de5d9b51d290284e50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a>ASP.NET Core en Reliable Services de Service Fabric

ASP.NET Core es un nuevo marco de código abierto multiplataforma para crear aplicaciones conectadas a Internet modernas y basadas en la nube, como aplicaciones web, aplicaciones de IoT y back-ends móviles. 

Este artículo es una toohosting guía detallada de los servicios básicos de ASP.NET en los servicios de confianza de tejido de servicio por hello **Microsoft.ServiceFabric.AspNetCore.** * el conjunto de paquetes de NuGet.

Para ver un tutorial introductorio sobre ASP.NET Core en Service Fabric e instrucciones para configurar el entorno de desarrollo, consulte [Creación de un front-end de servicio web para una aplicación mediante ASP.NET Core](service-fabric-add-a-web-frontend.md).

resto de Hola de este artículo se da por supuesto que ya está familiarizados con ASP.NET Core. Si no es así, se recomienda leer hello [Fundamentos de ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/index).

## <a name="aspnet-core-in-hello-service-fabric-environment"></a>ASP.NET Core en entorno de Service Fabric Hola

Si bien pueden ejecutar aplicaciones de ASP.NET Core en .NET Core o en hello en que completa de .NET Framework, servicios de Service Fabric actualmente solo puede ejecutarse Hola completa de .NET Framework. Esto significa que cuando se crea un servicio ASP.NET Core Service Fabric, todavía debe dirigir Hola completa de .NET Framework.

ASP.NET Core se puede utilizar de dos maneras diferentes en Service Fabric:
 - **Implementado como archivo ejecutable invitado**. Esto es principalmente toorun usa ASP.NET Core aplicaciones existentes en el tejido de servicio sin realizar ningún cambio en el código.
 - **Ejecutado dentro de una instancia de Reliable Services**. Esto permite una mejor integración con el tiempo de ejecución de hello Service Fabric y permite a los servicios con estado ASP.NET Core.

resto de Hola de este artículo explica cómo Hola toouse ASP.NET Core dentro de un servicio confiable mediante los componentes de integración de ASP.NET Core que se incluyen con hello SDK del servicio de Fabric. 

## <a name="service-fabric-service-hosting"></a>Hospedaje de servicios de Service Fabric

En Service Fabric, una o varias instancias o réplicas del servicio se ejecutan en un *proceso de host de servicio* (un archivo ejecutable que ejecuta el código del servicio). Es, como autor del servicio, el propietario el proceso de host del servicio de Hola y Service Fabric activa y supervisa automáticamente.

ASP.NET tradicional (arriba tooMVC 5) es tooIIS estrechamente acopladas a través de System.Web.dll. ASP.NET Core proporciona una separación entre el servidor web de Hola y de la aplicación web. Esto permite toobe de aplicaciones web portables entre diferentes servidores web y también permite toobe de servidores web *hospeda a sí mismo*, lo cual significa que puede iniciar un servidor web en su propio proceso, como proceso tooa lugar que pertenece a web dedicado software de servidor como IIS. 

En orden toocombine un servicio de Service Fabric y ASP.NET, ya sea como un ejecutable de invitado o en un servicio confiable, debe ser capaz de toostart ASP.NET dentro de su proceso de host de servicio. Núcleo de ASP.NET que se hospeda a sí mismo permite toodo esto.

## <a name="hosting-aspnet-core-in-a-reliable-service"></a>Hospedaje de ASP.NET Core en una instancia de Reliable Services
Normalmente, las aplicaciones de ASP.NET Core hospedadas por sí mismo crean un WebHost en el punto de entrada de una aplicación, como Hola `static void Main()` método `Program.cs`. En este caso, el ciclo de vida de Hola de hello WebHost es enlazado toohello ciclo de vida del proceso de Hola.

![Hospedaje de ASP.NET Core en un proceso][0]

Sin embargo, punto de entrada de aplicación Hola no es Hola lugar correcto toocreate un WebHost en un servicio confiable, porque sólo se utiliza el punto de entrada de aplicación Hola tooregister un servicio escriba con tiempo de ejecución de Service Fabric hello, de modo que pueden crear instancias de ese servicio tipo. Hola WebHost debe crearse en un servicio confiable propio. En el proceso de host de servicio de hello, instancias de servicio o réplicas pueden atravesar varios ciclos de vida. 

Una instancia de Reliable Services se representa mediante la clase de servicio derivada de `StatelessService` o `StatefulService`. pila de comunicación de Hola para un servicio se encuentra en un `ICommunicationListener` implementación en la clase de servicio. Hola `Microsoft.ServiceFabric.Services.AspNetCore.*` paquetes de NuGet contengan implementaciones de `ICommunicationListener` que iniciar y administrar Hola ASP.NET Core WebHost para Kestrel o WebListener en un servicio confiable.

![Hospedaje de ASP.NET Core en una instancia de Reliable Services][1]

## <a name="aspnet-core-icommunicationlisteners"></a>ICommunicationListeners en ASP.NET Core
Hola `ICommunicationListener` implementaciones de Kestrel y WebListener en hello `Microsoft.ServiceFabric.Services.AspNetCore.*` paquetes de NuGet tienen patrones de uso similar pero realizar el servidor web de tooeach específico de acciones ligeramente diferente. 

Ambos agentes de escucha de comunicación proporcionan un constructor que toma Hola argumentos siguientes:
 - **`ServiceContext serviceContext`**: Hola `ServiceContext` objeto que contiene información acerca de hello ejecutando el servicio.
 - **`string endpointName`**: nombre de Hola de un `Endpoint` configuración en ServiceManifest.xml. Esto es principalmente en qué se diferencian los agentes de escucha de comunicación de hello dos: WebListener **requiere** un `Endpoint` configuración, mientras que Kestrel no.
 - **`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: expresión lambda que se implementa para crear y devolver `IWebHost`. Esto le permite tooconfigure `IWebHost` Hola modo habitual en una aplicación de ASP.NET Core. lambda Hello proporciona una dirección URL que se genera para dependiendo de la integración de Service Fabric Hola opciones hello y use `Endpoint` configuración que proporcione. Que dirección URL, a continuación, se pueden modificar o utilizar como-es el servidor web de toostart Hola.

## <a name="service-fabric-integration-middleware"></a>Middleware de integración de Service Fabric
Hola `Microsoft.ServiceFabric.Services.AspNetCore` paquete de NuGet incluye hello `UseServiceFabricIntegration` método de extensión `IWebHostBuilder` que agrega middleware para Service Fabric. Este middleware configura Hola Kestrel o WebListener `ICommunicationListener` tooregister una dirección URL de servicio exclusiva con Hola servicio de nomenclatura de tejido de servicio y, a continuación, valida los clientes tooensure de solicitudes de cliente conectan toohello de servicio adecuado. Esto es necesario en un entorno de host compartido como Service Fabric, donde varias aplicaciones web pueden ejecutar en hello misma físico o máquina virtual pero no utilizan nombres de host único, tooprevent clientes conecten erróneamente toohello de servicio incorrecta. Este escenario se describe con más detalle en la sección siguiente Hola.

### <a name="a-case-of-mistaken-identity"></a>Un caso de identidad equivocada
Las réplicas de servicio, con independencia del protocolo, escuchan en una combinación IP:puerto única. Una vez que una réplica de servicio ha comenzado a escuchar en un punto de conexión de IP: Port, informa de que toohello de dirección de extremo tejido nomenclatura servicio donde se pueden detectar los clientes u otros servicios. Si los servicios utilizan puertos de la aplicación asigna dinámicamente, una réplica de servicio pueden utilizar casualmente Hola mismo punto de conexión de IP: Port de otro servicio que se encontraban previamente en Hola misma físico o máquina virtual. Esto puede hacer que un cliente toomistakely conectar toohello de servicio incorrecta. Esto puede ocurrir si se produce Hola sigue la secuencia de eventos:

 1. Un servicio A escucha en 10.0.0.1:30000 a través de HTTP. 
 2. El cliente resuelve el servicio A y obtiene la dirección 10.0.0.1:30000.
 3. Se desplaza tooa otro nodo del servicio.
 4. Servicio B se coloca en 10.0.0.1 y casualmente usa Hola mismo puerto 30000.
 5. Cliente intentará establecer tooconnect tooservice A con 10.0.0.1:30000 de direcciones almacenadas en caché.
 6. Cliente es ahora está conectado correctamente conectado tooservice B no que se dé cuenta toohello de servicio incorrecta.

Esto puede provocar errores en los momentos aleatorios que pueden ser difícil toodiagnose. 

### <a name="using-unique-service-urls"></a>Uso de direcciones URL de servicio únicas
Servicios de tooprevent, puede publicar un servicio de nombres con un identificador único de punto de conexión toohello y, a continuación, validar ese identificador único durante las solicitudes de cliente. Se trata de una acción cooperativa entre servicios en un entorno de confianza sin inquilinos hostiles. No proporciona autenticación de servicio segura en un entorno con inquilinos hostiles.

En un entorno de confianza, Hola middleware que se agrega de forma hello `UseServiceFabricIntegration` método anexa automáticamente una dirección de toohello de identificador único que se registra toohello servicio de nomenclatura y valida ese identificador en cada solicitud. Si no coincide con el identificador de hello, Hola middleware devuelve inmediatamente una respuesta HTTP 410 ya no existe.

Los servicios que utilizan un puerto asignado de forma dinámica deberían usar este middleware.

Los servicios que utilizan un puerto fijo único no tienen este problema en un entorno cooperativo. Un único puerto fijo se utiliza normalmente para servicios externo que necesitan un puerto bien conocido para tooconnect de las aplicaciones de cliente para. Por ejemplo, la mayoría de las aplicaciones web accesibles desde Internet usarán el puerto 80 o 443 para las conexiones del explorador web. En este caso, identificador único de hello no debe estar habilitada.

Hello siguiente diagrama muestra flujo de solicitud de hello con middleware de hello habilitado:

![Integración de ASP.NET Core de Service Fabric][2]

Kestrel y WebListener `ICommunicationListener` implementaciones utilizan este mecanismo Hola exactamente igual. Aunque WebListener internamente puede diferenciar las solicitudes basadas en rutas de acceso de dirección URL únicas subyacente hello *http.sys* característica, que es la funcionalidad de uso compartido de puerto *no* utilizado por hello WebListener `ICommunicationListener` implementación ya que se produciría en códigos de estado de error HTTP 503 y 404 de HTTP en el escenario de Hola se ha descrito anteriormente. A su vez hace muy difícil intención de hello toodetermine de los clientes de error de hello, como HTTP 503 y 404 de HTTP ya están tooindicate utilizada otros errores. Por lo tanto, Kestrel y WebListener `ICommunicationListener` implementaciones estandaricen middleware Hola proporcionada por hello `UseServiceFabricIntegration` método de extensión para que los clientes sólo necesitan tooperform un extremo de servicio vuelve a resolver acción en las respuestas HTTP 410.

## <a name="weblistener-in-reliable-services"></a>WebListener en Reliable Services
WebListener puede utilizarse en un servicio confiable mediante la importación de hello **Microsoft.ServiceFabric.AspNetCore.WebListener** paquete NuGet. Este paquete contiene `WebListenerCommunicationListener`, una implementación de `ICommunicationListener`, que le permita toocreate un WebHost de núcleo de ASP.NET dentro de un servicio confiable con WebListener como servidor web de Hola.

WebListener se basa en hello [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx). Esto utiliza hello *http.sys* controlador de kernel usado por IIS tooprocess HTTP solicita y enrutar tooprocesses ellas las aplicaciones web en ejecución. Esto permite que varios procesos en hello misma máquina física o virtual toohost las aplicaciones web de hello mismo puerto, eliminar la ambigüedad por una ruta de acceso de dirección URL única o un nombre de host. Estas características son útiles en Service Fabric para hospedar varios sitios Web en hello mismo clúster.

Hello siguiente diagrama ilustra cómo WebListener usa hello *http.sys* controladores de kernel de Windows para uso compartido de puertos:

![http.sys][3]

### <a name="weblistener-in-a-stateless-service"></a>WebListener en un servicio sin estado
toouse `WebListener` en un servicio sin estado, reemplace el método hello `CreateServiceInstanceListeners` método y devuelven un `WebListenerCommunicationListener` instancia:

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseWebListener()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build()))
    };
}
```

### <a name="weblistener-in-a-stateful-service"></a>WebListener en un servicio con estado

`WebListenerCommunicationListener`actualmente no está diseñado para su uso en servicios con estado vencimiento toocomplications con hello subyacente *http.sys* característica de uso compartido de puerto. Para obtener más información, vea Hola pasos de la sección de asignación de puerto dinámico con WebListener. Para los servicios con estado, Kestrel es hello recomendada servidor web.

### <a name="endpoint-configuration"></a>Configuración del punto de conexión

Un `Endpoint` configuración es necesaria para los servidores web que utilizan la API de servidor HTTP de Windows, incluidos los WebListener Hola. Servidores Web que utilizan la API de servidor HTTP de Windows hello en primer lugar deben reservar su dirección URL con *http.sys* (Esto se consigue normalmente con hello [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) herramienta). Esta acción requiere privilegios elevados de los que sus servicios carecen de forma predeterminada. Hola "http" o "https" opciones de hello `Protocol` propiedad de hello `Endpoint` configuración de *ServiceManifest.xml* se utilizan específicamente tooinstruct Hola Service Fabric en tiempo de ejecución tooregister una dirección URL con *http.sys* en su nombre mediante hello [ *carácter comodín fuerte* ](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) prefijo de dirección URL.

Por ejemplo, tooreserve `http://+:80` para un servicio, hello configuración siguiente debe usarse en ServiceManifest.xml:

```xml
<ServiceManifest ... >
    ...
    <Resources>
        <Endpoints>
            <Endpoint Name="ServiceEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>

</ServiceManifest>
```

Y se debe pasar el nombre del extremo de hello toohello `WebListenerCommunicationListener` constructor:

```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     return new WebHostBuilder()
         .UseWebListener()
         .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
         .UseUrls(url)
         .Build();
 })
```

#### <a name="use-weblistener-with-a-static-port"></a>Uso de WebListener con un puerto estático
toouse un puerto estático con WebListener, especifique el número de puerto de Hola Hola `Endpoint` configuración:

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a>Uso de WebListener con un puerto dinámico
toouse un puerto asignado dinámicamente con WebListener, omitir hello `Port` propiedad Hola `Endpoint` configuración:

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

Tenga en cuenta que un puerto dinámico asignado por una configuración `Endpoint` proporciona solo un puerto *por cada proceso de host*. Hello actual Service Fabric modelo de hospedaje permite varios toobe de instancias o réplicas de servicio hospedado en hello mismo proceso, lo que significa que cada uno de ellos compartirán Hola mismo número de puerto cuando se asignan a través de hello `Endpoint` configuración. Varias instancias de WebListener pueden compartir un puerto mediante subyacente hello *http.sys* puertos de característica, pero que no es compatible con `WebListenerCommunicationListener` debido a las complicaciones de toohello incluye las solicitudes de cliente. Para el uso de puertos dinámicos, Kestrel es hello recomendada servidor web.

## <a name="kestrel-in-reliable-services"></a>Kestrel en Reliable Services
Kestrel puede utilizarse en un servicio confiable mediante la importación de hello **Microsoft.ServiceFabric.AspNetCore.Kestrel** paquete NuGet. Este paquete contiene `KestrelCommunicationListener`, una implementación de `ICommunicationListener`, que le permita toocreate un WebHost de núcleo de ASP.NET dentro de un servicio confiable con Kestrel como servidor web de Hola.

Kestrel es un servidor web multiplataforma para ASP.NET Core basado en libuv, una biblioteca de E/S asincrónica multiplataforma. A diferencia de WebListener, Kestrel no utiliza un administrador centralizado de puntos de conexión como *http.sys*. Y, a diferencia de WebListener, Kestrel no es compatible con el uso compartido de puertos entre varios procesos. Cada instancia de Kestrel debe usar un puerto único.

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a>Kestrel en un servicio sin estado
toouse `Kestrel` en un servicio sin estado, reemplace el método hello `CreateServiceInstanceListeners` método y devuelven un `KestrelCommunicationListener` instancia:

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

### <a name="kestrel-in-a-stateful-service"></a>Kestrel en un servicio con estado
toouse `Kestrel` en un servicio con estado, reemplace el método hello `CreateServiceReplicaListeners` método y devuelven un `KestrelCommunicationListener` instancia:

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new ServiceReplicaListener[]
    {
        new ServiceReplicaListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                         services => services
                             .AddSingleton<StatefulServiceContext>(serviceContext)
                             .AddSingleton<IReliableStateManager>(this.StateManager))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

En este ejemplo, una instancia de singleton de `IReliableStateManager` se proporciona el contenedor de inyección de dependencia de toohello WebHost. Esto no es estrictamente necesaria, pero le permite toouse `IReliableStateManager` y colecciones confiable en los métodos de acción de controlador MVC.

Tenga en cuenta que un `Endpoint` nombre de configuración es **no** proporciona demasiado`KestrelCommunicationListener` en un servicio con estado. Esto se explica con más detalle en los pasos de la sección de Hola.

### <a name="endpoint-configuration"></a>Configuración del punto de conexión
Un `Endpoint` configuración no es necesario toouse Kestrel. 

Kestrel es un servidor web independiente simple; a diferencia de WebListener (o HttpListener), no es necesario un `Endpoint` configuración de *ServiceManifest.xml* ya no requiere toostarting anterior del registro de dirección URL. 

#### <a name="use-kestrel-with-a-static-port"></a>Uso de Kestrel con un puerto estático
Se puede configurar un puerto estático en hello `Endpoint` configuración de ServiceManifest.xml para su uso con Kestrel. Aunque esto no es estrictamente necesario, ofrece dos ventajas potenciales:
 1. Si el puerto de hello no se encuentra en el intervalo de puertos de aplicación Hola, se abre a través de firewall de sistema operativo de Hola por Service Fabric.
 2. Hola tooyou dirección URL proporcionada a través de `KestrelCommunicationListener` usará este puerto.

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

Si un `Endpoint` está configurado, se debe pasar su nombre a hello `KestrelCommunicationListener` constructor: 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

Si un `Endpoint` no se utiliza la configuración, se omite el nombre de Hola Hola `KestrelCommunicationListener` constructor. En este caso, se utilizará un puerto dinámico. Vea la siguiente sección de Hola para obtener más información.

#### <a name="use-kestrel-with-a-dynamic-port"></a>Uso de Kestrel con un puerto dinámico
Kestrel no se puede usar la asignación de puerto automática de Hola de hello `Endpoint` configuración en ServiceManifest.xml, porque la asignación automática de puerto de un `Endpoint` configuración asigna un puerto único por *el proceso de host* , y un proceso de host solo puede contener varias instancias de Kestrel. Puesto que Kestrel no admite el uso compartido de puertos, esto no funciona porque cada instancia de Kestrel debe abrirse en un puerto único.

asignación de puertos dinámicos de toouse con Kestrel, simplemente omite hello `Endpoint` configuración en ServiceManifest.xml por completo y no pasan un toohello de nombre de punto de conexión `KestrelCommunicationListener` constructor:

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

En esta configuración, `KestrelCommunicationListener` seleccionará automáticamente un puerto no utilizado de intervalo de puertos de aplicación Hola.

## <a name="scenarios-and-configurations"></a>Escenarios y configuraciones
En esta sección Hola los escenarios siguientes se describe y proporciona Hola recomienda combinación de servidor web, configuración de puerto, opciones de integración de Service Fabric y diversas configuraciones tooachieve un servicio que funciona correctamente:
 - Servicio sin estado de ASP.NET Core expuesto al exterior
 - Servicio sin estado de ASP.NET Core solo interno
 - Servicio con estado de ASP.NET Core solo interno

Un **expone externamente** servicio es aquel que expone un extremo accesible desde fuera de clúster de hello, normalmente a través de un equilibrador de carga.

Un **solo para uso interno** servicio es aquella cuyo extremo solo es accesible desde dentro de clúster de Hola.

> [!NOTE]
> Servicio con estado extremos por lo general no se debe expone toohello Internet. Clústeres que se encuentran detrás de los equilibradores de carga que no son conscientes de la resolución del servicio de Service Fabric, como Hola equilibrador de carga de Azure, se pueden servicios con estado no se puede tooexpose porque equilibrador de carga de hello no ser capaz de toolocate y enrutar el tráfico toohello réplica de servicio con estado adecuado. 

### <a name="externally-exposed-aspnet-core-stateless-services"></a>Servicios sin estado de ASP.NET Core expuestos al exterior
WebListener es hello recomendada servidor web para los servicios front-end que exponen los extremos HTTP externos, orientado a Internet en Windows. Proporciona mejor protección frente a ataques y admite características incompatibles con Kestrel, como la autenticación de Windows y el uso compartido de puertos. 

Kestrel no se admite como servidor perimetral (orientado a Internet) en este momento. Se debe usar un servidor proxy inverso, como IIS o Nginx Hola a toohandle el tráfico de red pública de Internet.
 
Cuando toohello expuesto Internet, un servicio sin estado debe usar un punto de conexión conocido y estable que sea accesible a través de un equilibrador de carga. Se trata de dirección URL de hello proporcionará toousers de la aplicación. se recomienda Hola siguiente configuración:

|  |  | **Notas** |
| --- | --- | --- |
| Servidor web | WebListener | Si el servicio de hello es sólo tooa expuesto red de confianza, este tipo de una intranet, se puede usar Kestrel. En caso contrario, WebListener es opción Hola preferido. |
| Configuración de puerto | estática | Un puerto estático conocido debe configurarse en hello `Endpoints` configuración de ServiceManifest.xml, como 80 para HTTP o 443 para HTTPS. |
| ServiceFabricIntegrationOptions | None | Hola `ServiceFabricIntegrationOptions.None` opción se debe usar al configurar el middleware de integración de Service Fabric para que el servicio de hello no intenta toovalidate las solicitudes entrantes de un identificador único. Los usuarios externos de la aplicación no podrá saber información de identificación única hello usa Hola middleware. |
| Recuento de instancias | -1 | En casos de uso habitual, recuento de instancias de hello configuración debe establecerse demasiado "-1" para que una instancia está disponible en todos los nodos que reciben tráfico de un equilibrador de carga. |

Si varios servicios externamente expuestos compartan Hola al mismo conjunto de nodos, se debe usar una ruta de acceso de dirección URL único pero estable. Esto puede realizarse mediante la modificación de la dirección URL de hello proporcionada al configurar IWebHost. Tenga en cuenta que esto se aplica solo tooWebListener.

 ```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     url += "/MyUniqueServicePath";
 
     return new WebHostBuilder()
         .UseWebListener()
         ...
         .UseUrls(url)
         .Build();
 })
 ```

### <a name="internal-only-stateless-aspnet-core-service"></a>Servicio sin estado de ASP.NET Core solo interno
Los servicios sin estado que solo se llaman desde dentro de clúster de hello deberían utilizar direcciones URL únicas y asignan dinámicamente puertos tooensure cooperación entre varios servicios. se recomienda Hola siguiente configuración:

|  |  | **Notas** |
| --- | --- | --- |
| Servidor web | Kestrel | Aunque WebListener puede utilizarse para los servicios sin estado internos, Kestrel es Hola recomienda server tooallow varios tooshare de instancias de servicio un host.  |
| Configuración de puerto | asignado de forma dinámica | Varias réplicas de un servicio con estado pueden compartir un proceso de host o un sistema operativo host y, por tanto, necesitarán puertos únicos. |
| ServiceFabricIntegrationOptions | UseUniqueServiceUrl | Con la asignación de puertos dinámicos, esta configuración impide problema Hola equivocado de la identidad que se ha descrito anteriormente. |
| InstanceCount | cualquiera | configuración del número de instancia Hola puede establecerse servicio Hola de tooany valor toooperate necesarios. |

### <a name="internal-only-stateful-aspnet-core-service"></a>Servicio con estado de ASP.NET Core solo interno
Los servicios con estado que se llaman solo desde dentro de clúster de hello deben usar puertos asignados dinámicamente tooensure cooperación entre varios servicios. se recomienda Hola siguiente configuración:

|  |  | **Notas** |
| --- | --- | --- |
| Servidor web | Kestrel | Hola `WebListenerCommunicationListener` no está diseñado para su uso por los servicios con estado en el que las réplicas comparten un proceso de host. |
| Configuración de puerto | asignado de forma dinámica | Varias réplicas de un servicio con estado pueden compartir un proceso de host o un sistema operativo host y, por tanto, necesitarán puertos únicos. |
| ServiceFabricIntegrationOptions | UseUniqueServiceUrl | Con la asignación de puertos dinámicos, esta configuración impide problema Hola equivocado de la identidad que se ha descrito anteriormente. |

## <a name="next-steps"></a>Pasos siguientes
[Depurar la aplicación de Service Fabric con Visual Studio](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
