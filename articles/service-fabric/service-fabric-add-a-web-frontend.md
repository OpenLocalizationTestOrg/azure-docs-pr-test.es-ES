---
title: "aaaCreate un front-end web para la aplicación de Azure Service Fabric mediante ASP.NET Core | Documentos de Microsoft"
description: "Exponer su web toohello de aplicación de Service Fabric mediante el uso de un proyecto de ASP.NET Core y la comunicación entre servicio a través de comunicación remota de servicio."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: 0c4454d6cac4c2e343bd6e93e56d3d2f0ebfc4ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a>Creación de un front-end de servicio web para una aplicación mediante ASP.NET Core
De forma predeterminada, servicios de Azure Service Fabric no proporcionan un sitio web toohello de interfaz pública. tooexpose los clientes tooHTTP de funcionalidad de la aplicación, deberá toocreate un sitio web tooact como un punto de entrada del proyecto y, a continuación, comunicarse desde ahí tooyour servicios individuales.

En este tutorial, se retomar donde se dejó en hello [crear su primera aplicación en Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial y agregar un servicio web de ASP.NET Core delante de servicio de contador con estado Hola. Si aún no lo ha hecho, debe revisar primero ese tutorial.

## <a name="set-up-your-environment-for-aspnet-core"></a>Configuración del entorno para ASP.NET Core

Necesita Visual Studio de 2017 toofollow junto con este tutorial. Cualquier edición servirá. 

 - [Instalación de Visual Studio 2017](https://www.visualstudio.com/)

las aplicaciones de ASP.NET Core Service Fabric toodevelop, debe tener Hola siguiendo las cargas de trabajo instalados:
 - **Desarrollo de Azure** (en *Web y nube*)
 - **ASP.NET y desarrollo web** (en *Web y nube*)
 - **Desarrollo multiplataforma de .NET Core** (en *Otros conjuntos de herramientas*)

>[!Note] 
>Hello herramientas de .NET Core para Visual Studio 2015 ya no se actualizan, no obstante, si todavía se usa Visual Studio 2015, necesita toohave [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) instalado.

## <a name="add-an-aspnet-core-service-tooyour-application"></a>Agregar una aplicación de ASP.NET Core servicio tooyour
Núcleo de ASP.NET es un marco de desarrollo web ligera y multiplataforma que puede usar la interfaz de usuario de web moderna toocreate y las API web. 

Vamos a agregar una aplicación existente de ASP.NET Web API proyecto tooour.

1. En el Explorador de soluciones, haga clic en **servicios** en Hola proyecto de aplicación y elija **Agregar > nuevo servicio de Fabric**.
   
    ![Agregar una nueva aplicación existente de tooan de servicio][vs-add-new-service]
2. En hello **crear un servicio** página, elija **ASP.NET Core** y asígnele un nombre.
   
    ![Elegir el servicio web ASP.NET en el cuadro de diálogo de hello nuevo servicio][vs-new-service-dialog]

3. página siguiente de Hello proporciona un conjunto de ASP.NET Core plantillas de proyecto. Tenga en cuenta que estos se Hola mismo opciones que vería si crea un proyecto de ASP.NET Core fuera de una aplicación de Service Fabric, con una pequeña cantidad de código adicional tooregister Hola servicio con el tiempo de ejecución de hello Service Fabric. Para este tutorial, elija **API Web**. Sin embargo, puede aplicar Hola mismo conceptos toobuilding una aplicación web completa.
   
    ![Elección del tipo de proyecto ASP.NET][vs-new-aspnet-project-dialog]
   
    Una vez creado el proyecto API web, tendrá dos servicios en la aplicación. Mientras continúa toobuild con la aplicación, puede agregar más servicios en hello exactamente igual. Cada uno puede tener versiones y actualizaciones independientes.

## <a name="run-hello-application"></a>Ejecutar la aplicación hello
tooget una idea de lo que hemos hecho, vamos a implementar la nueva aplicación de Hola y realice un vistazo en el comportamiento predeterminado de Hola que Hola plantilla API Web de ASP.NET Core proporciona.

1. Presione F5 en Visual Studio toodebug Hola app.
2. Cuando se completa la implementación, Visual Studio inicia una raíz de toohello del explorador de hello servicio ASP.NET Web API. plantilla de API Web de ASP.NET Core Hello no proporciona comportamiento predeterminado para la raíz de hello, por lo que debería ver un error 404 en explorador Hola.
3. Agregar `/api/values` toohello ubicación en el Explorador de Hola. Esto invoca hello `Get` método en hello ValuesController en la plantilla de la API Web de Hola. Devuelve respuesta predeterminada de hello proporcionada por la plantilla de hello: una matriz JSON que contiene dos cadenas:
   
    ![Valores predeterminados devueltos desde la plantilla API web de ASP.NET Core][browser-aspnet-template-values]
   
    Extremo de Hola de tutorial de hello, esta página mostrará valor más reciente del contador Hola de nuestro servicio con estado en lugar de hello cadenas predeterminadas.

## <a name="connect-hello-services"></a>Conectar servicios de Hola
Service Fabric proporciona una flexibilidad completa en el modo de comunicación con los servicios confiables. En una sola aplicación, podría tener servicios que son accesibles a través de TCP, servicios que son accesibles a través de una API de REST de HTTP y servicios que son accesibles a través de sockets web. Para obtener información sobre opciones de hello disponibles y los inconvenientes de hello, consulte [comunicarse con servicios](service-fabric-connect-and-communicate-with-services.md). En este tutorial, usamos [comunicación remota de servicio de Service Fabric](service-fabric-reliable-services-communication-remoting.md), proporcionado en hello SDK.

Hola enfoque de comunicación remota de servicio (modelada en llamadas a procedimiento remoto o RPC), se define una interfaz tooact como contrato público de hello para el servicio de Hola. A continuación, usar ese toogenerate interfaz una clase de proxy para interactuar con el servicio de Hola.

### <a name="create-hello-remoting-interface"></a>Crear la interfaz de comunicación remota de Hola
Empecemos creando Hola interfaz tooact como Hola contrato entre el servicio con estado de Hola y otros servicios, en este caso Hola proyecto web de ASP.NET Core. Esta interfaz debe estar compartida por todos los servicios que usan llamadas a RPC toomake, por lo que vamos a crear en su propio proyecto de biblioteca de clases.

1. En el Explorador de soluciones, haga clic con el botón derecho en la solución y seleccione **Agregue** > **Nuevo proyecto**.

2. Elija hello **Visual C#** entrada Hola dejado el panel de navegación y, a continuación, seleccione hello **biblioteca de clases** plantilla. Asegurarse de esa versión de .NET Framework Hola se establece demasiado**4.5.2**.
   
    ![Creación de un proyecto de interfaz para el servicio con estado][vs-add-class-library-project]

3. Instalar hello **Microsoft.ServiceFabric.Services.Remoting** paquete NuGet. Busque **Microsoft.ServiceFabric.Services.Remoting** en hello NuGet paquete Administrador e instalarlo para todos los proyectos de solución de Hola que usar el servicio de acceso remoto, incluidos:
   - proyecto de biblioteca de clases de Hola que contiene la interfaz de servicio de Hola
   - proyecto de servicio con estado Hola
   - Hola proyecto de servicio web de ASP.NET Core
   
    ![Agregando el paquete NuGet de servicios Hola][vs-services-nuget-package]

4. En la biblioteca de clases de hello, crear una interfaz con un único método, `GetCountAsync`, y extender la interfaz de Hola desde `Microsoft.ServiceFabric.Services.Remoting.IService`. interfaz de comunicación remota de Hello debe derivar de esta interfaz tooindicate que es una interfaz de comunicación remota de servicio.
   
    ```c#
    using Microsoft.ServiceFabric.Services.Remoting;
    using System.Threading.Tasks;
        
    ...

    namespace MyStatefulService.Interface
    {
        public interface ICounter: IService
        {
            Task<long> GetCountAsync();
        }
    }
    ```

### <a name="implement-hello-interface-in-your-stateful-service"></a>Implementar interfaz hello en el servicio con estado
Ahora que hemos definido interfaz hello, necesitamos tooimplement en servicio con estado Hola.

1. En el servicio con estado, agregue un proyecto de biblioteca de clases de toohello de referencia que contiene la interfaz de Hola.
   
    ![Agregar un proyecto de biblioteca de clases de toohello de referencia de servicio con estado Hola][vs-add-class-library-reference]
2. Busque Hola clase que hereda de `StatefulService`, como `MyStatefulService`y ampliarlo hello tooimplement `ICounter` interfaz.
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. Ahora implemente Hola único método que se define en hello `ICounter` interfaz, `GetCountAsync`.
   
    ```c#
    public async Task<long> GetCountAsync()
    {
        var myDictionary = 
            await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
   
        using (var tx = this.StateManager.CreateTransaction())
        {          
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            return result.HasValue ? result.Value : 0;
        }
    }
    ```

### <a name="expose-hello-stateful-service-using-a-service-remoting-listener"></a>Exponer Hola servicio con estado con un agente de escucha de comunicación remota de servicio
Con hello `ICounter` interfaz implementada, el paso final de hello es canal de comunicación de comunicación remota de servicio de tooopen Hola. Para los servicios con estado, Service Fabric proporciona un método reemplazable denominado " `CreateServiceReplicaListeners`". Con este método, puede especificar una o varias escuchas de comunicación, según tipo hello de comunicación que necesite tooenable para el servicio.

> [!NOTE]
> se llama a Hola método equivalente para abrir los servicios de toostateless de canal de comunicación `CreateServiceInstanceListeners`.

En este caso, reemplazamos Hola existente `CreateServiceReplicaListeners` método y proporcionar una instancia de `ServiceRemotingListener`, que crea un punto de conexión RPC que sea accesible desde los clientes a través de `ServiceProxy`.  

Hola `CreateServiceRemotingListener` método de extensión en hello `IService` interfaz permite tooeasily crear un `ServiceRemotingListener` con todos los valores predeterminados. toouse este método de extensión, asegúrese de tener hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` espacio de nombres importado. 

```c#
using Microsoft.ServiceFabric.Services.Remoting.Runtime;

...

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new List<ServiceReplicaListener>()
    {
        new ServiceReplicaListener(
            (context) =>
                this.CreateServiceRemotingListener(context))
    };
}
```


### <a name="use-hello-serviceproxy-class-toointeract-with-hello-service"></a>Utilizar hello ServiceProxy clase toointeract con el servicio de Hola
Nuestro servicio con estado ahora está listo tooreceive tráfico de otros servicios a través de RPC. Por lo que todo lo que sigue siendo consiste en Agregar Hola código toocommunicate con él de hello servicio web ASP.NET.

1. En el proyecto ASP.NET, agregue una biblioteca de clases de toohello de referencia que contiene Hola `ICounter` interfaz.

2. Antes de que se ha agregado hello **Microsoft.ServiceFabric.Services.Remoting** proyecto ASP.NET de toohello de paquete de NuGet. Este paquete proporciona hello `ServiceProxy` clase que usar toomake RPC llama toohello de servicio con estado. Asegúrese de que este paquete de NuGet está instalado en el proyecto de servicio web de ASP.NET Core Hola.

4. Hola **controladores** carpeta, abra hello `ValuesController` clase. Tenga en cuenta que hello `Get` método actualmente solo devuelve una matriz de cadenas codificadas de forma rígida de "value1" y "value2", que coincide con lo que vimos anteriormente en el Explorador de Hola. Reemplace esta implementación con hello siguiente código:
   
    ```c#
    using MyStatefulService.Interface;
    using Microsoft.ServiceFabric.Services.Client;
    using Microsoft.ServiceFabric.Services.Remoting.Client;
   
    ...

    [HttpGet]
    public async Task<IEnumerable<string>> Get()
    {
        ICounter counter =
            ServiceProxy.Create<ICounter>(new Uri("fabric:/MyApplication/MyStatefulService"), new ServicePartitionKey(0));
   
        long count = await counter.GetCountAsync();
   
        return new string[] { count.ToString() };
    }
    ```
   
    primera línea de código de Hello es clave Hola uno. toocreate Hola ICounter proxy toohello servicio con estado, deberá tooprovide dos piezas de información: nombre de servicio de Hola hello y el Id. de partición.
   
    Puede usar servicios con estado de partición tooscale dividiendo su estado en sectores de almacenamiento diferentes, en función de una clave que defina, por ejemplo, un identificador de cliente o un código postal. En nuestra aplicación trivial, servicio con estado de hello sólo tiene una partición, por lo que no importa la clave de Hola. Cualquier tecla proporcionada por usted llevará toohello misma partición. toolearn más información acerca de la creación de particiones de servicios, consulte [cómo toopartition servicios confiables de tejido de servicio](service-fabric-concepts-partitioning.md).
   
    nombre del servicio Hello es un URI de tejido de formulario de hello: /&lt;$application_name&gt;/&lt;service_name&gt;.
   
    Con estos dos fragmentos de información, Service Fabric puede identificar máquina Hola que se deben enviar las solicitudes. Hola `ServiceProxy` clase controla también perfectamente caso de hello donde se produce un error en la máquina de Hola que aloja la partición de servicio con estado de Hola y otra máquina debe ser promocionada tootake su lugar. Esta abstracción permite escribir Hola toodeal de código de cliente con otros servicios de proceso mucho más sencillas.
   
    Una vez que tenemos proxy hello, basta con invocar hello `GetCountAsync` método y devuelva su resultado.

5. Presione F5 nuevo toorun Hola modificó la aplicación. Como antes, Visual Studio inicia automáticamente Hola explorador toohello raíz Hola proyecto web. Agregar ruta de acceso de "api/valores" hello y debería ver el valor de contador actual de hello devuelto.
   
    ![valor de contador con estado de Hello muestra en el Explorador de Hola][browser-aspnet-counter-value]
   
    Actualice el Explorador de hello actualización del valor toosee Hola contador periódicamente.

## <a name="kestrel-and-weblistener"></a>Kestrel y WebListener

Hello predeterminada ASP.NET web server Core, conocido como Kestrel, es [no se admite actualmente para controlar el tráfico de internet directa](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel). Como resultado, hello plantilla de servicio sin estado ASP.NET Core Service Fabric usa [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) de forma predeterminada. 

toolearn más información sobre Kestrel y WebListener en servicios de Service Fabric, consulte demasiado[ASP.NET Core en servicios de Service Fabric confiable](service-fabric-reliable-services-communication-aspnetcore.md).

## <a name="connecting-tooa-reliable-actor-service"></a>Conexión de servicio de Actor confiable tooa
Este tutorial se centra en la incorporación de un front-end web que se comunica con un servicio con estado. Sin embargo, puede seguir una muy similar tooactors tootalk de modelo. Cuando se crea un proyecto de Reliable Actor, Visual Studio genera automáticamente un proyecto de interfaz. Puede usar ese toogenerate interfaz un proxy de actor en hello web proyecto toocommunicate con actor Hola. canal de comunicación de Hola se proporciona automáticamente. Así, no es necesario toodo cualquier cosa que es equivalente tooestablishing un `ServiceRemotingListener` como hizo para el servicio con estado de hello en este tutorial.

## <a name="how-web-services-work-on-your-local-cluster"></a>Cómo funcionan los servicios web en el clúster local
En general, puede implementar exactamente Hola mismo tejido de servicio aplicación tooa varias máquinas de clúster que se implementa en el clúster local y ser muy seguro que funciona según lo esperado. Esto es porque el clúster local es simplemente una configuración de cinco nodos que contrae tooa único equipo.

Cuando se trata de servicios de tooweb, sin embargo, hay un matiz de clave. Cuando el clúster se encuentra detrás de un equilibrador de carga, como ocurre en Azure, debe asegurarse de que los servicios web se implementan en todos los equipos desde el equilibrador de carga de hello simplemente operaciones por turnos de tráfico en los equipos de Hola. Para ello, establecer hello `InstanceCount` para hello servicio toohello valor especial "-1".

Por el contrario, cuando se ejecuta un servicio web localmente, necesita tooensure que solo una instancia del servicio de saludo se está ejecutando. En caso contrario, experimenta conflictos de varios procesos que están escuchando en hello misma ruta de acceso y el puerto. Como resultado, se debe establecer recuento de instancias de servicio web de hello demasiado "1" para implementaciones locales.

toolearn tooconfigure distintos valores de entorno diferente, vea [administrar parámetros de la aplicación para varios entornos](service-fabric-manage-multiple-environment-app-configuration.md).

## <a name="next-steps"></a>Pasos siguientes
Ahora que tiene un front-end web configurado para la aplicación con ASP.NET Core, obtenga más información sobre [ASP.NET Core en Reliable Services de Service Fabric](service-fabric-reliable-services-communication-aspnetcore.md) para una descripción detallada de cómo funciona ASP.NET Core con Service Fabric.

Después, [más información sobre la comunicación con servicios](service-fabric-connect-and-communicate-with-services.md) en general tooget a completar imagen de servicio cómo funciona la comunicación en Service Fabric.

Una vez que tenga una buena comprensión del funcionamiento de la comunicación del servicio, [crear un clúster de Azure e implementar la nube de toohello aplicación](service-fabric-cluster-creation-via-portal.md).

<!-- Image References -->

[vs-add-new-service]: ./media/service-fabric-add-a-web-frontend/vs-add-new-service.png
[vs-new-service-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-service-dialog.png
[vs-new-aspnet-project-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-aspnet-project-dialog.png
[browser-aspnet-template-values]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-template-values.png
[vs-add-class-library-project]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-project.png
[vs-add-class-library-reference]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-reference.png
[vs-services-nuget-package]: ./media/service-fabric-add-a-web-frontend/vs-services-nuget-package.png
[browser-aspnet-counter-value]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-counter-value.png
[vs-create-platform]: ./media/service-fabric-add-a-web-frontend/vs-create-platform.png


<!-- external links -->
[dotnetcore-install]: https://www.microsoft.com/net/core#windows
