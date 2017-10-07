---
title: aaaConnect y comunicarse con los servicios de Azure Service Fabric | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooresolve, conectarse y comunicarse con servicios de Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: msfussell
ms.assetid: 7d1052ec-2c9f-443d-8b99-b75c97266e6c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/9/2017
ms.author: vturecek
ms.openlocfilehash: b8b374a71d4c5d21f48a560a3a8c81b357fe418d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a>Conexión y comunicación con servicios en Service Fabric
En Service Fabric, un servicio se ejecuta en algún lugar en un clúster de Service Fabric que normalmente se distribuye entre varias máquinas virtuales. Se puede mover desde un solo lugar tooanother, ya sea por el propietario del servicio hello, o automáticamente por Service Fabric. Servicios no están vinculados estáticamente tooa una máquina determinada o la dirección.

Una aplicación de Service Fabric se compone, por lo general, de muchos servicios diferentes, donde cada uno de ellos realiza una tarea especializada. Estos servicios pueden comunicarse entre sí tooform una función completa, por ejemplo, de diferentes partes de la representación de una aplicación web. También hay aplicaciones que se conectan tooand comunican con los servicios de cliente. Este documento se describen cómo tooset la comunicación con y entre los servicios de Service Fabric.

Este vídeo de Microsoft Virtual Academy también explica la comunicación del servicio: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965">  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a>Traiga su propio protocolo
Service Fabric ayuda a administrar Hola del ciclo de vida de los servicios pero no efectúa ninguna decisión sobre lo que los servicios. Esto incluye la comunicación. Cuando se abre el servicio de Service Fabric, es decir, tooset de oportunidad de su servicio en un extremo para las solicitudes entrantes, mediante cualquier pila de comunicación o protocolo que desee. El servicio escuchará en una dirección **IP:port** normal mediante cualquier esquema de direccionamiento, como un URI. Varias instancias de servicio o réplicas pueden compartir un proceso de host, en cuyo caso que se necesita toouse distintos puertos o usar un mecanismo de uso compartido de puertos, como controlador de núcleo de http.sys hello en Windows. En ambos casos, cada instancia de servicio o réplica de un proceso de host debe ser direccionable de forma exclusiva.

![puntos de conexión de servicio][1]

## <a name="service-discovery-and-resolution"></a>Detección y resolución de servicios
En un sistema distribuido, pueden mover los servicios de tooanother de una máquina con el tiempo. Esto puede ocurrir por diversos motivos, incluidos el equilibrio, las actualizaciones, las conmutaciones por error o el escalado de recursos. Esto significa cambian de direcciones de extremo de servicio como servicio Hola mueve toonodes con direcciones IP diferentes y puede abrir en puertos diferentes si el servicio de hello usa un puerto seleccionado dinámicamente.

![Distribución de servicios][7]

Tejido de servicio proporciona una detección y la resolución que se llamó al servicio Hola Naming Service. Hello Naming Service mantiene una tabla que asigna los toohello direcciones de extremo que escuchan en instancias de servicio con nombre. Todas las instancias de servicio con nombre en Service Fabric tienen nombres únicos como URI como, por ejemplo, `"fabric:/MyApplication/MyService"`. nombre de Hello del servicio de hello no cambia con vida Hola Hola, es solo direcciones de extremo de Hola que pueden cambiar cuando mueve servicios. Esto es análogo toowebsites con direcciones URL constantes pero donde puede cambiar la dirección IP de Hola. Y tooDNS similar en web de hello, que se resuelve direcciones de tooIP de direcciones URL de sitios Web, Service Fabric tiene un registrador que se asigna la dirección del extremo de tootheir de nombres de servicio.

![puntos de conexión de servicio][2]

Resolver y conectar tooservices implica Hola siguiendo los pasos que se ejecute en un bucle:

* **Resolver**: punto de conexión Hola Get que ha publicado un servicio de Hola Naming Service.
* **Conectar**: conectar toohello servicio sobre cualquier protocolo que se usa en ese punto de conexión.
* **Vuelva a intentar**: un intento de conexión puede producir un error de una serie de motivos, por ejemplo, si el servicio de Hola se mueve desde la dirección de extremo de hello última hora Hola se resolvió. En ese caso, Hola anterior resolución y conectar pasos deben toobe vuelve a intentar y este ciclo se repite hasta que la conexión de Hola se realiza correctamente.

## <a name="connecting-tooother-services"></a>Conectar servicios tooother
Servicios que se conectan tooeach sí dentro de un clúster por lo general puede acceder directamente a los puntos de conexión de Hola de otros servicios porque los nodos de hello en un clúster están en hello misma red local. toomake es más fácil tooconnect entre servicios, Service Fabric proporciona servicios adicionales que usan Hola Naming Service. Un servicio DNS y un servicio de proxy inverso.


### <a name="dns-service"></a>Servicio DNS
Dado que muchos servicios, especialmente en los servicios en contenedores, pueden tener un nombre de dirección URL existente, tooresolve capaz de estos mediante Hola protocolo DNS estándar (en lugar de protocolo del servicio de nomenclatura de hello) es muy prácticos, especialmente en aplicaciones "Levantar y mover" escenarios. Esto es exactamente qué servicio DNS Hola. Permite toomap DNS nombres tooa nombre del servicio y, por tanto, resolver direcciones IP del extremo. 

Como se muestra en hello siguiente diagrama, Hola servicio DNS, en ejecución en el clúster de Service Fabric hello, asigna nombres de tooservice de nombres DNS que, a continuación, se resuelven utilizando Hola Naming Service tooreturn Hola extremo direcciones tooconnect a. nombre DNS de Hello para el servicio de Hola se proporciona en tiempo de Hola de creación. 

![puntos de conexión de servicio][9]

Para obtener más detalles sobre cómo ver hello toouse servicio DNS [servicio DNS en Azure Service Fabric](service-fabric-dnsservice.md) artículo.

### <a name="reverse-proxy-service"></a>Servicio de proxy inverso
servicios en clúster de Hola que expone extremos HTTP incluidos HTTPS de direcciones de proxy inverso de Hola. proxy inverso Hola simplifica considerablemente la llamada a otros servicios y sus métodos debido a un determinado formato de URI e identificadores resolver hello, conectar, Hola a pasos de reintento necesarios para toocommunicate de un servicio con el uso de otro servicio de nomenclatura. En otras palabras, se oculta Hola servicio de escribir el nombre del usuario al llamar a otros servicios haciendo esto tan sencillo como llamar a una dirección URL.

![puntos de conexión de servicio][10]

Para obtener más detalles sobre cómo toouse Hola invertir el servicio de proxy, consulte [proxy en Azure Service Fabric inverso](service-fabric-reverseproxy.md) artículo.

## <a name="connections-from-external-clients"></a>Conexiones desde clientes externos
Servicios que se conectan tooeach sí dentro de un clúster por lo general puede acceder directamente a los puntos de conexión de Hola de otros servicios porque los nodos de hello en un clúster están en hello misma red local. Sin embargo, en algunos entornos, un clúster puede estar detrás de un equilibrador de carga que enruta el tráfico de entrada externo a través de un conjunto limitado de puertos. En estos casos, los servicios todavía pueden comunicarse entre sí y resolver direcciones mediante Hola Naming Service, pero realizar pasos adicionales deben ser tomada tooallow los clientes externos tooconnect tooservices.

## <a name="service-fabric-in-azure"></a>Service Fabric en Azure
Un clúster de Service Fabric en Azure se coloca detrás de un equilibrador de carga de Azure. Todos los clústeres de toohello de tráfico externo deben pasar a través del equilibrador de carga de Hola. Hello equilibrador de carga automáticamente reenviará el tráfico entrante en un tooa determinado puerto aleatorio *nodo* cuya Hola abrir el mismo puerto. Hello equilibrador de carga de Azure solo conoce puertos abiertos en hello *nodos*, no conozca puertos abiertos individuo *services*.

![Topología de equilibrador de carga de Azure y Service Fabric][3]

Por ejemplo, en orden tooaccept externo el tráfico en el puerto **80**, debe configurarse Hola siguientes cosas:

1. Escriba un servicio que escuche en el puerto 80. Configurar el puerto 80 en ServiceManifest.xml del servicio de Hola y abrir un agente de escucha en el servicio de hello, por ejemplo, un servidor web hospedado por sí mismo.

    ```xml
    <Resources>
        <Endpoints>
            <Endpoint Name="WebEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>
    ```
    ```csharp
        class HttpCommunicationListener : ICommunicationListener
        {
            ...

            public Task<string> OpenAsync(CancellationToken cancellationToken)
            {
                EndpointResourceDescription endpoint =
                    serviceContext.CodePackageActivationContext.GetEndpoint("WebEndpoint");

                string uriPrefix = $"{endpoint.Protocol}://+:{endpoint.Port}/myapp/";

                this.httpListener = new HttpListener();
                this.httpListener.Prefixes.Add(uriPrefix);
                this.httpListener.Start();

                string publishUri = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
                return Task.FromResult(publishUri);
            }

            ...
        }

        class WebService : StatelessService
        {
            ...

            protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
            {
                return new[] { new ServiceInstanceListener(context => new HttpCommunicationListener(context))};
            }

            ...
        }
    ```
    ```java
        class HttpCommunicationlistener implements CommunicationListener {
            ...

            @Override
            public CompletableFuture<String> openAsync(CancellationToken arg0) {
                EndpointResourceDescription endpoint =
                    this.serviceContext.getCodePackageActivationContext().getEndpoint("WebEndpoint");
                try {
                    HttpServer server = com.sun.net.httpserver.HttpServer.create(new InetSocketAddress(endpoint.getPort()), 0);
                    server.start();

                    String publishUri = String.format("http://%s:%d/",
                        this.serviceContext.getNodeContext().getIpAddressOrFQDN(), endpoint.getPort());
                    return CompletableFuture.completedFuture(publishUri);
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            }

            ...
        }

        class WebService extends StatelessService {
            ...

            @Override
            protected List<ServiceInstanceListener> createServiceInstanceListeners() {
                <ServiceInstanceListener> listeners = new ArrayList<ServiceInstanceListener>();
                listeners.add(new ServiceInstanceListener((context) -> new HttpCommunicationlistener(context)));
                return listeners;       
            }

            ...
        }
    ```
2. Crear un clúster de Service Fabric en Azure y especifique el puerto **80** como un puerto de extremo personalizado para el tipo de nodo de Hola que va a hospedar el servicio de Hola. Si tiene más de un tipo de nodo, puede configurar un *restricción de emplazamiento* en hello tooensure de servicio sólo se ejecuta en el tipo de nodo de Hola que tiene abierto el puerto de extremo personalizado de Hola.

    ![Apertura de un puerto en un tipo de nodo][4]
3. Una vez que se haya creado el clúster de hello, configure Hola equilibrador de carga de Azure en el tráfico de tooforward de grupo de recursos del clúster de hello en el puerto 80. Al crear un clúster a través de hello portal de Azure, esto se configura automáticamente para cada puerto de extremo personalizado que se configuró.

    ![Reenviar el tráfico en hello equilibrador de carga de Azure][5]
4. Hola utiliza el equilibrador de carga Azure un toodetermine sondeo si o no toosend tráfico tooa de nodo concreto. Hola sondeo comprueba periódicamente un punto de conexión en cada toodetermine de nodo o no está respondiendo nodo Hola. Si el sondeo de hello no tooreceive una respuesta después de un número determinado de veces, equilibrador de carga de hello deja de enviar nodo toothat de tráfico. Al crear un clúster a través de hello portal de Azure, un sondeo se configura automáticamente para cada puerto de extremo personalizado que se configuró.

    ![Reenviar el tráfico en hello equilibrador de carga de Azure][8]

Es importante tooremember que hello equilibrador de carga de Azure y sondeo Hola solo conocen hello *nodos*, no Hola *servicios* ejecutan en nodos de Hola. Hola equilibrador de carga de Azure siempre enviará tráfico toonodes que respondan toohello sondeo, por lo que debe tener cuidado tooensure servicios están disponibles en los nodos de Hola que se pueda toorespond toohello sondeo.

## <a name="reliable-services-built-in-communication-api-options"></a>Reliable Services: opciones de API de comunicación integradas
Hola servicios confiables framework incluye varias opciones de comunicación pregenerado. Decisión de Hello sobre los cuales uno adaptará mejor a los depende de elección de Hola de hello programación modelo, marco de comunicación de Hola y Hola lenguaje de programación que los servicios se escriben en.

* **Ningún protocolo específico:** si no tiene una opción determinada del marco de comunicación, pero desea tooget algo activos y en funcionamiento rápidamente, Hola opción ideal para usted es [comunicación remota de servicio](service-fabric-reliable-services-communication-remoting.md), lo que permite llamadas a procedimiento remoto fuertemente tipado para servicios de confianza y actores confiable. Esto es más fácil de hello y tooget de forma más rápida a trabajar con comunicación del servicio. La comunicación remota de servicio controla la resolución de direcciones, la conexión, los reintentos y el control de errores del servicio. Esto está disponible para aplicaciones de C# y Java.
* **HTTP**: para una comunicación independiente del lenguaje, HTTP proporciona una opción estándar con las herramientas y los servidores HTTP disponibles en muchos lenguajes diferentes, compatibles todos ellos con Service Fabric. Los servicios pueden usar cualquier pila HTTP disponible, incluida la [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) para aplicaciones de C#. Los clientes escritos en C# pueden aprovechar hello `ICommunicationClient` y `ServicePartitionClient` clases, mientras que para Java, usar hello `CommunicationClient` y `FabricServicePartitionClient` clases, [para la resolución de servicio, las conexiones HTTP y bucles de reintento](service-fabric-reliable-services-communication.md).
* **WCF**: Si tienes código existente que usa WCF como el marco de comunicación, puede usar hello `WcfCommunicationListener` para el lado del servidor de Hola y `WcfCommunicationClient` y `ServicePartitionClient` clases para cliente de Hola. Pero esto solo está disponible para las aplicaciones de C# en clústeres basados en Windows. Para obtener más información, consulte el artículo [implementación basada en WCF de pila de comunicación de hello](service-fabric-reliable-services-communication-wcf.md).

## <a name="using-custom-protocols-and-other-communication-frameworks"></a>Uso de protocolos personalizados y otros marcos de comunicación
Los servicios pueden usar cualquier protocolo o marco de comunicación, ya sea un protocolo binario personalizado sobre sockets de TCP o eventos de streaming a través de [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) o [IoT Hub de Azure](https://azure.microsoft.com/services/iot-hub/). Service Fabric proporciona comunicación las API que se puede conectar la pila de comunicación en, mientras todos los Hola trabajar toodiscover y conectar se abstrae del usuario. Consulte este artículo sobre hello [modelo de comunicación de servicio confiable](service-fabric-reliable-services-communication.md) para obtener más detalles.

## <a name="next-steps"></a>Pasos siguientes
Aprender más acerca de conceptos de Hola y de API disponibles en hello [modelo de comunicación de servicios de confianza](service-fabric-reliable-services-communication.md), a continuación, empezar a trabajar rápidamente con [comunicación remota de servicio](service-fabric-reliable-services-communication-remoting.md) o visite toolearn detallada de cómo toowrite un agente de escucha de comunicación con [API Web con OWIN autohospedaje](service-fabric-reliable-services-communication-webapi.md).

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
