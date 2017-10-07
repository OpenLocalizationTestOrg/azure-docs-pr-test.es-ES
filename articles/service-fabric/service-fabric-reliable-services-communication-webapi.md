---
title: "comunicación aaaService con hello ASP.NET Web API | Documentos de Microsoft"
description: "Obtenga información acerca de cómo la comunicación del servicio tooimplement paso a paso mediante el uso de Hola ASP.NET Web API con OWIN hospeda a sí mismo en hello confiable de servicios de API."
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
ms.date: 02/10/2017
ms.author: vturecek
redirect_url: /azure/service-fabric/service-fabric-reliable-services-communication-aspnetcore
ms.openlocfilehash: 3fb18fcb141ada0d79a0acda3dccbc7fb044346d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a>Introducción a los servicios de la API web de Microsoft Azure Service Fabric con autohospedaje OWIN
Azure Service Fabric aplica la potencia de hello en sus manos cuando decida cómo desea que su toocommunicate de servicios con los usuarios y entre sí. Este tutorial se centra en la implementación de la comunicación del servicio mediante la API web de ASP.NET con autohospedaje OWIN (Open Web Interface para .NET) en la API de Reliable Services de Service Fabric. Trataremos profundamente en hello API de comunicación acoplable de servicios de confianza. También vamos a usar API Web en un tooshow de ejemplo paso a paso, cómo tooset un detector de comunicación personalizada.

## <a name="introduction-tooweb-api-in-service-fabric"></a>Introducción tooWeb API de Service Fabric
ASP.NET Web API es un marco eficaz y popular para la creación de HTTP APIs sobre Hola .NET Framework. Si no ya está familiarizado con el marco de trabajo de hello, consulte [Introducción a ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn más.

API Web en Service Fabric es Hola mismo ASP.NET Web API conocen y adoran. Hello diferencia radica en cómo se *host* una aplicación de API Web. No va a utilizar Microsoft Internet Information Services (IIS). toobetter comprender la diferencia de hello, vamos a dividirla en dos partes:

1. aplicación de API Web de Hello (incluidos los controladores y los modelos)
2. host de Hello (hello web server, normalmente IIS)

Una aplicación de la API web no cambia. No es distinta de las aplicaciones Web API que ha escrito en hello anterior, y debe ser toosimply pueda mover a través de la mayoría del código de aplicación. Pero si ha sido hospedaje en IIS, donde se hospeda la aplicación hello puede ser un poco diferente de lo que está acostumbrado. Antes de que obtenemos toohello parte de hospedaje, puede empezar con algo más conocidos: Hola aplicación Web API.

## <a name="create-hello-application"></a>Crear aplicación hello
Empiece por crear una nueva aplicación Service Fabric, con un servicio único sin estado en Visual Studio 2015.

Una plantilla de Visual Studio para un servicio sin estado mediante las API de Web es tooyou disponible. En este tutorial, crearemos desde cero un proyecto de API web que tenga como resultado lo que se obtendría si seleccionara esta plantilla.

Seleccione un toolearn de proyecto de servicio sin estado en blanco cómo toobuild un proyecto de Web API desde el principio o puede empezar con el servicio sin estado Hola plantilla API Web y basta con seguir el tutorial.  

Hola primer paso es toopull en algunos paquetes de NuGet para la API Web. paquete de Hello queremos toouse es Microsoft.AspNet.WebApi.OwinSelfHost. Este paquete incluye todos los paquetes de Web API necesarios de Hola y Hola *host* paquetes. Esto será importante más adelante.

Una vez instalados los paquetes de saludo, puede empezar a crear estructura de proyecto de API Web básica hello. Si ha utilizado la API Web, estructura de proyecto de hello deberá ser muy familiar. Empiece agregando un directorio `Controllers` y un controlador de valores sencillos:

**ValuesController.cs**

```csharp
using System.Collections.Generic;
using System.Web.Http;

namespace WebService.Controllers
{
    public class ValuesController : ApiController
    {
        // GET api/values 
        public IEnumerable<string> Get()
        {
            return new string[] { "value1", "value2" };
        }

        // GET api/values/5 
        public string Get(int id)
        {
            return "value";
        }

        // POST api/values 
        public void Post([FromBody]string value)
        {
        }

        // PUT api/values/5 
        public void Put(int id, [FromBody]string value)
        {
        }

        // DELETE api/values/5 
        public void Delete(int id)
        {
        }
    }
}

```

A continuación, agregue una clase de inicio Hola proyecto raíz tooregister Hola enrutamiento, los formateadores y cualquier otro programa de instalación de configuración. También es donde se conecta la API Web en toohello *host*, que se revisan de nuevo más tarde. 

**Startup.cs**

```csharp
using System.Web.Http;
using Owin;

namespace WebService
{
    public static class Startup
    {
        public static void ConfigureApp(IAppBuilder appBuilder)
        {
            // Configure Web API for self-host. 
            HttpConfiguration config = new HttpConfiguration();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            appBuilder.UseWebApi(config);
        }
    }
}
```

Esto es todo por parte de la aplicación de Hola. En este punto, hemos configurado solo hello Web API proyecto diseño básico. Hasta ahora, no debería buscar mucho diferente de proyectos API Web que ha escrito en los último Hola o de plantilla de API Web básica hello. La lógica de negocios va en controladores de Hola y modelos como de costumbre.

¿Ahora qué hacemos con el hospedaje para poder ejecutarlo en realidad?

## <a name="service-hosting"></a>Hospedaje de servicio
En Service Fabric, el servicio se ejecuta en un *proceso de host de servicio*(un archivo ejecutable que ejecuta el código del servicio). Al escribir un servicio mediante el uso de hello confiable de servicios de API, el proyecto de servicio solo compila tooan archivo ejecutable que registra el tipo de servicio y se ejecuta el código. Esto ocurre en la mayoría de los casos al escribir un servicio de Service Fabric en .NET. Cuando abra Program.cs en el proyecto de servicio sin estado hello, verá:

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric.Services.Runtime;

internal static class Program
{
    private static void Main()
    {
        try
        {
            ServiceRuntime.RegisterServiceAsync("WebServiceType",
                context => new WebService(context)).GetAwaiter().GetResult();

            ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(WebService).Name);

            // Prevents this host process from terminating so services keeps running. 
            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

Si se ve es sospechosamente como aplicación de consola de tooa de punto de entrada de hello, que es porque es.

Hola a más detalles sobre el proceso de host de servicio y registro del servicio están más allá del ámbito de Hola de este artículo. Pero es importante tooknow para ahora que *se ejecuta el código de servicio en su propio proceso*.

## <a name="self-host-web-api-with-an-owin-host"></a>Autohospedaje de la API web con un host OWIN
¿Dado que el código de aplicación de API Web se hospeda en su propio proceso, cómo enlazó, servidor web de tooa? Escriba [OWIN](http://owin.org/). OWIN es simplemente un contrato entre las aplicaciones web .NET y servidores web. Tradicionalmente cuando se usa ASP.NET (arriba tooMVC 5), aplicación web de hello es tooIIS estrechamente acopladas a través de System.Web. Sin embargo, la API Web implementa OWIN, por lo que puede escribir una aplicación web que se separa del servidor web de Hola que lo hospeda. Por este motivo, puede usar un servidor web OWIN de *autohospedaje* que puede iniciar en su propio proceso. Esto se adapta perfectamente con los modelos de hospedaje de Service Fabric de Hola que acabamos de describir.

En este artículo, vamos a usar Katana como host de hello OWIN para hello aplicación Web API. Katana es una implementación del host OWIN de código abierto basada en [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) y Hola Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).

> [!NOTE]
> más información acerca de Katana, vaya toohello toolearn [Katana sitio](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana). Para obtener una introducción rápida de cómo toouse Katana tooself host Web API, consulte [OWIN Use tooSelf Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).
> 
> 

## <a name="set-up-hello-web-server"></a>Configurar el servidor web de Hola
Hola confiable de servicios de API proporciona un punto de entrada de comunicación que se pueden conectar en pilas de comunicación que permiten a los usuarios y el servicio de toohello de tooconnect de clientes:

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

servidor web de Hello (y cualquier otra pila de comunicación que utilizar Hola futura, por ejemplo, WebSockets) deben usar hello ICommunicationListener interfaz toointegrate correctamente con el sistema de Hola. los motivos Hola serán más evidentes Hola siguiendo los pasos.

En primer lugar, cree una clase denominada OwinCommunicationListener que implemente ICommunicationListener:

**OwinCommunicationListener.cs**

```csharp
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;
using System;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        public void Abort()
        {
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
        }
    }
}
```

interfaz ICommunicationListener de Hello proporciona tres toomanage métodos un agente de escucha de comunicación para el servicio:

* *OpenAsync*. Empezar a escuchar las solicitudes.
* *CloseAsync*. Dejar de escuchar las solicitudes, finalizar las solicitudes en curso y cerrar correctamente.
* *Abort*. Cancelar todo y detener inmediatamente.

tooget iniciado, agregue los miembros de clase privada para el agente de escucha de cosas Hola tendrá toofunction. Estos se inicializarán a través del constructor de Hola y utilizar más adelante cuando configure Hola escuchando la dirección URL.

```csharp
internal class OwinCommunicationListener : ICommunicationListener
{
    private readonly ServiceEventSource eventSource;
    private readonly Action<IAppBuilder> startup;
    private readonly ServiceContext serviceContext;
    private readonly string endpointName;
    private readonly string appRoot;

    private IDisposable webApp;
    private string publishAddress;
    private string listeningAddress;

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
        : this(startup, serviceContext, eventSource, endpointName, null)
    {
    }

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
    {
        if (startup == null)
        {
            throw new ArgumentNullException(nameof(startup));
        }

        if (serviceContext == null)
        {
            throw new ArgumentNullException(nameof(serviceContext));
        }

        if (endpointName == null)
        {
            throw new ArgumentNullException(nameof(endpointName));
        }

        if (eventSource == null)
        {
            throw new ArgumentNullException(nameof(eventSource));
        }

        this.startup = startup;
        this.serviceContext = serviceContext;
        this.endpointName = endpointName;
        this.eventSource = eventSource;
        this.appRoot = appRoot;
    }


    ...

```

## <a name="implement-openasync"></a>Implementación de OpenAsync
tooset de servidor web de hello, necesita dos fragmentos de información:

* *Prefijo de ruta de acceso de dirección URL*. Aunque esto es opcional, es conveniente para tooset esta una copia de seguridad ahora para que puede hospedar varios servicios web con seguridad en la aplicación.
* *Un puerto*.

Antes de obtener un puerto de servidor web de hello, es importante que comprenda que Service Fabric proporciona una capa de aplicación que actúa como un búfer entre la aplicación y el sistema operativo subyacente Hola donde se ejecuta. Por lo tanto, Service Fabric proporciona una manera tooconfigure *extremos* para los servicios. Service Fabric garantiza que los puntos de conexión están disponibles para su toouse de servicio. De esta manera, no tiene tooconfigure a usted mismo en hello subyacente de entorno de sistema operativo. Fácilmente puede hospedar la aplicación de Service Fabric en diferentes entornos sin necesidad de toomake cualquier aplicación de tooyour de cambios. (Por ejemplo, puede hospedar Hola la misma aplicación en Azure o en su propio centro de datos.)

Configurar un extremo HTTP en PackageRoot\ServiceManifest.xml:

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

Este paso es importante porque el proceso de host del servicio de Hola se ejecuta con credenciales restringidas (servicio de red en Windows). Esto significa que el servicio no tendrá acceso tooset un extremo HTTP por sí mismo. Mediante la configuración de punto de conexión de hello, Service Fabric sabe tooset una lista de control de acceso apropiado de hello (ACL) para hello escuche en direcciones URL que Hola servicio. Service Fabric también proporciona un lugar estándar tooconfigure extremos.

De nuevo en OwinCommunicationListener.cs, puede iniciar la implementación de OpenAsync. Esto es donde se inicia el servidor de web de Hola. En primer lugar, obtener información de punto de conexión de Hola y crear dirección URL de Hola que escucha en el servicio de Hola. dirección URL de Hello será diferente dependiendo de si se utiliza el agente de escucha de hello en un servicio sin estado o un servicio con estado. Para un servicio con estado, el agente de escucha de hello debe toocreate un nombre único para cada réplica de servicio con estado realiza escuchas en dirección. Para los servicios sin estado, dirección de hello puede ser mucho más fácil. 

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
    var protocol = serviceEndpoint.Protocol;
    int port = serviceEndpoint.Port;

    if (this.serviceContext is StatefulServiceContext)
    {
        StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}{3}/{4}/{5}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/',
            statefulServiceContext.PartitionId,
            statefulServiceContext.ReplicaId,
            Guid.NewGuid());
    }
    else if (this.serviceContext is StatelessServiceContext)
    {
        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/');
    }
    else
    {
        throw new InvalidOperationException();
    }

    ...

```

Tenga en cuenta que "http://+" se utiliza aquí. Se trata de toomake seguro de que el servidor web Hola está escuchando en todas las direcciones disponibles, incluyendo localhost, el FQDN y la dirección IP del equipo Hola.

Hello OpenAsync implementación es uno de los motivos más importantes de hello ¿por qué servidor web de hello (o cualquier pila de comunicación) se implementa como un ICommunicationListener, en lugar de simplemente tener abre directamente desde `RunAsync()` en el servicio de Hola. valor devuelto de Hola de OpenAsync es dirección Hola Hola servidor web está escuchando en. Cuando esta dirección se devuelve toohello system, registra dirección Hola con servicio Hola. Tejido de servicio proporciona una API que permite a los clientes y otro servicios toothen solicitar esta dirección por nombre de servicio. Esto es importante porque la dirección de servicio de hello no es estático. Servicios se mueven en clúster de Hola para fines de disponibilidad y equilibrio de recursos. Este es el mecanismo de Hola que permite a los clientes hello tooresolve dirección para un servicio de escucha.

Con esto en mente, OpenAsync inicia el servidor web de Hola y devuelve la dirección de Hola que escuchan en. Tenga en cuenta que realiza escuchas en "http://+", pero antes de que OpenAsync devuelve la dirección de hello, Hola "+" se reemplaza con hello IP o FQDN del nodo de hello está actualmente en. dirección de Hello devuelto por este método es lo que está registrado con el sistema de Hola. También es lo que los clientes y otros servicios ven cuando solicitan la dirección de un servicio. Para los clientes toocorrectly conectar tooit, que necesitan una IP o FQDN real de dirección de Hola.

```csharp
    ...

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    try
    {
        this.eventSource.Message("Starting web server on " + this.listeningAddress);

        this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

        this.eventSource.Message("Listening on " + this.publishAddress);

        return Task.FromResult(this.publishAddress);
    }
    catch (Exception ex)
    {
        this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

Tenga en cuenta que esto hace referencia a clase de inicio de Hola que se pasó en toohello OwinCommunicationListener en el constructor de Hola. Saludos toobootstrap aplicación de API Web del servidor de web de hello usa esta instancia de inicio.

Hola `ServiceEventSource.Current.Message()` línea aparecerá en la ventana de eventos de diagnóstico de hello más adelante, al ejecutar ese servidor web de Hola Hola aplicación tooconfirm ha iniciado correctamente.

## <a name="implement-closeasync-and-abort"></a>Implementación de CloseAsync y Abort
Por último, implemente CloseAsync y anulación del servidor web de toostop Hola. servidor web de Hola se puede detener eliminando identificador de servidor de Hola que se creó durante la OpenAsync.

```csharp
public Task CloseAsync(CancellationToken cancellationToken)
{
    this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

    this.StopWebServer();

    return Task.FromResult(true);
}

public void Abort()
{
    this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

    this.StopWebServer();
}

private void StopWebServer()
{
    if (this.webApp != null)
    {
        try
        {
            this.webApp.Dispose();
        }
        catch (ObjectDisposedException)
        {
            // no-op
        }
    }
}
```

En este ejemplo de implementación, CloseAsync y Abort simplemente detendrán servidor web de Hola. Puede elegir un apagado más correctamente coordinado de servidor web de hello en CloseAsync tooperform. Por ejemplo, apagado Hola podría esperar toobe solicitudes sobre la marcha completada antes de devolver Hola.

## <a name="start-hello-web-server"></a>Inicie hello web server
Ahora está listo toocreate y devolver una instancia de servidor web de OwinCommunicationListener toostart Hola. Nuevo en hello clase de servicio (WebService.cs), invalidar hello `CreateServiceInstanceListeners()` método:

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                           .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                           .Select(endpoint => endpoint.Name);

    return endpoints.Select(endpoint => new ServiceInstanceListener(
        serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
}
```

Esto es donde Hola API Web *aplicación* y Hola OWIN *host* finalmente cumplir. host de Hello (OwinCommunicationListener) tiene una instancia del programa Hola a *aplicación* (API de Web) a través de la clase de inicio de Hola. Service Fabric administra su ciclo de vida. Normalmente este mismo patrón puede ser seguido de cualquier pila de comunicación.

## <a name="put-it-all-together"></a>Colocación de todo junto
En este ejemplo, no es necesario toodo cualquier dato de hello `RunAsync()` método, por lo que la invalidación de simplemente puede eliminarse.

implementación del servicio final de Hello debe ser muy simple. Solo necesita el agente de escucha de toocreate Hola comunicación:

```csharp
using System;
using System.Collections.Generic;
using System.Fabric;
using System.Fabric.Description;
using System.Linq;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace WebService
{
    internal sealed class WebService : StatelessService
    {
        public WebService(StatelessServiceContext context)
            : base(context)
        { }

        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
            var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                                   .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                                   .Select(endpoint => endpoint.Name);

            return endpoints.Select(endpoint => new ServiceInstanceListener(
                serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
        }
    }
}
```

Hola completa `OwinCommunicationListener` clase:

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        private readonly ServiceEventSource eventSource;
        private readonly Action<IAppBuilder> startup;
        private readonly ServiceContext serviceContext;
        private readonly string endpointName;
        private readonly string appRoot;

        private IDisposable webApp;
        private string publishAddress;
        private string listeningAddress;

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
            : this(startup, serviceContext, eventSource, endpointName, null)
        {
        }

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
        {
            if (startup == null)
            {
                throw new ArgumentNullException(nameof(startup));
            }

            if (serviceContext == null)
            {
                throw new ArgumentNullException(nameof(serviceContext));
            }

            if (endpointName == null)
            {
                throw new ArgumentNullException(nameof(endpointName));
            }

            if (eventSource == null)
            {
                throw new ArgumentNullException(nameof(eventSource));
            }

            this.startup = startup;
            this.serviceContext = serviceContext;
            this.endpointName = endpointName;
            this.eventSource = eventSource;
            this.appRoot = appRoot;
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
            var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
            var protocol = serviceEndpoint.Protocol;
            int port = serviceEndpoint.Port;

            if (this.serviceContext is StatefulServiceContext)
            {
                StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}{3}/{4}/{5}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/',
                    statefulServiceContext.PartitionId,
                    statefulServiceContext.ReplicaId,
                    Guid.NewGuid());
            }
            else if (this.serviceContext is StatelessServiceContext)
            {
                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/');
            }
            else
            {
                throw new InvalidOperationException();
            }

            this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

            try
            {
                this.eventSource.Message("Starting web server on " + this.listeningAddress);

                this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

                this.eventSource.Message("Listening on " + this.publishAddress);

                return Task.FromResult(this.publishAddress);
            }
            catch (Exception ex)
            {
                this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

                this.StopWebServer();

                throw;
            }
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
            this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

            this.StopWebServer();

            return Task.FromResult(true);
        }

        public void Abort()
        {
            this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

            this.StopWebServer();
        }

        private void StopWebServer()
        {
            if (this.webApp != null)
            {
                try
                {
                    this.webApp.Dispose();
                }
                catch (ObjectDisposedException)
                {
                    // no-op
                }
            }
        }
    }
}
```

Ahora que ha colocado todas las piezas de hello en su lugar, el proyecto debería parecerse a una aplicación de API Web típica con puntos de entrada de API de servicios de confianza y un host OWIN.

## <a name="run-and-connect-through-a-web-browser"></a>Ejecutar y conectarse a través de un explorador web
Si no lo ha hecho, [configure el entorno de desarrollo](service-fabric-get-started.md).

Ahora puede compilar e implementar su servicio. Presione **F5** en Visual Studio toobuild e implementar la aplicación hello. En la ventana de eventos de diagnóstico de hello, verá un mensaje que indica que el servidor web Hola abierto en http://localhost:8281 /.

> [!NOTE]
> Si ya se ha abierto el puerto de Hola por otro proceso en el equipo, verá un error aquí. Esto indica que no se pudo abrir ese agente de escucha de Hola. Si ese es el caso de hello, pruebe a usar un puerto diferente para la configuración de punto de conexión de hello en ServiceManifest.xml.
> 
> 

Una vez que se está ejecutando el servicio de hello, abra un explorador y navegue demasiado[http://localhost:8281/api/valores](http://localhost:8281/api/values) tootest lo.

## <a name="scale-it-out"></a>Escala horizontal
Ampliación de aplicaciones web sin estado normalmente significa agregar más máquinas y girando hello las aplicaciones web en ellos. Motor de orquestaciones del tejido de servicio puede hacerlo automáticamente cada vez que se agregan nuevos nodos clúster tooa. Al crear instancias de un servicio sin estado, puede especificar el número de Hola de instancias que desea toocreate. Service Fabric coloca ese número de instancias en nodos de clúster de Hola. Y se asegura de que no toocreate más de una instancia en cada nodo. También puede indicar al Service Fabric tooalways crear una instancia en cada nodo mediante la especificación de **-1** para recuento de instancias de Hola. Esto garantiza que, siempre que agregue nodos tooscale fuera del clúster, se creará una instancia del servicio sin estado en nodos nuevos de Hola. Este valor es una propiedad de instancia de servicio de hello, por lo que se establece cuando se crea una instancia de servicio. Puede hacerlo a través de PowerShell:

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

También puede hacerlo al definir un servicio predeterminado en un proyecto de servicio sin estado de Visual Studio:

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

Para obtener más información sobre cómo toocreate aplicación y las instancias del servicio, vea [implementar una aplicación](service-fabric-deploy-remove-applications.md).

## <a name="next-steps"></a>Pasos siguientes
[Depurar la aplicación de Service Fabric con Visual Studio](service-fabric-debugging-your-application.md)

