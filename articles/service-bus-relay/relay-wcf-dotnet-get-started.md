---
title: "aaaGet partió retransmisiones de WCF de retransmisión de Azure en .NET | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Azure retransmisión WCF retransmite tooconnect dos aplicaciones hospedadas en diferentes ubicaciones."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5493281a-c2e5-49f2-87ee-9d3ffb782c75
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: a652617fc2e9b7c8d62d39fa914f77df6e3a1771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-relay-wcf-relays-with-net"></a>¿Cómo toouse Azure retransmisión WCF las retransmisiones con .NET
Este artículo describe cómo toouse Hola servicio de retransmisión de Azure. ejemplos de Hello están escritas en C# y usar la API de Windows Communication Foundation (WCF) de hello con extensiones contenidas en hello ensamblado de Bus de servicio. Para obtener más información acerca de la retransmisión de Azure, vea hello [Introducción a Azure Relay](relay-what-is-it.md).

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a>¿Qué es Retransmisión de WCF?

Hello Azure [ *retransmisión de WCF* ](relay-what-is-it.md) servicio permite aplicaciones híbridas de toobuild que se ejecutan en un centro de datos de Azure y su propio entorno de empresa local. servicio de retransmisión de Hello facilita este proceso permitiéndole toosecurely exponer los servicios de Windows Communication Foundation (WCF) que residen dentro de una nube pública de la toohello de red empresas corporativas, sin tener tooopen una conexión de servidor de seguridad o requerir infraestructura de red corporativa de cambios intrusivo tooa.

![Conceptos del relé WCF](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

Retransmisión de Azure permite toohost los servicios WCF en el entorno empresarial existente. A continuación, puede delegar la escucha entrantes sesiones y solicitudes toothese WCF services toohello servicio de retransmisión de ejecución dentro de Azure. Esto permite tooexpose estos servicios tooapplication código se ejecuta en Azure, o los trabajadores toomobile o entornos de extranet de socio comercial. Retransmisión le permite controlar toosecurely quién puede acceder a estos servicios en un nivel específico. Proporciona una funcionalidad de la aplicación de forma eficaz y segura tooexpose y los datos de las soluciones empresariales existentes y aprovechar las ventajas del mismo desde la nube de Hola.

Este artículo describe cómo toouse toocreate de retransmisión de Azure en que un servicio web WCF, exponen de mediante un enlace de canal TCP, que implementa una conversación segura entre dos entidades.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-hello-service-bus-nuget-package"></a>Obtener el paquete de NuGet de Bus de servicio de Hola
Hola [paquete NuGet de Bus de servicio](https://www.nuget.org/packages/WindowsAzure.ServiceBus) es hello tooget de manera más fácil de hello API de Service Bus y tooconfigure la aplicación con todas las dependencias de Bus de servicio de Hola de. paquete de NuGet tooinstall hello en el proyecto, Hola siguientes:

1. En el Explorador de soluciones, haga clic con el botón derecho en **Referencias** y, a continuación, en **Administrar paquetes NuGet**.
2. La búsqueda de "Bus de servicio" y seleccione hello **Microsoft Azure Service Bus** elemento. Haga clic en **instalar** toocomplete Hola instalación y luego cierre Hola después el cuadro de diálogo:
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a>Exponga y consuma un servicio web SOAP con TCP
tooexpose un servicio web de SOAP de WCF existente para su uso externo, debe realizar los cambios toohello los enlaces de servicio y las direcciones. Esto podría precisar el archivo de configuración de tooyour de cambios o podría requerir cambios en el código, dependiendo de cómo se configurado y configura los servicios WCF. Tenga en cuenta que WCF permite toohave varios puntos de conexión de red sobre Hola mismo servicio, por lo que puede conservar Hola existente extremos internos al agregar extremos de retransmisión para external acceso en hello mismo tiempo.

En esta tarea, crear un servicio WCF simple y agregar un tooit de agente de escucha de retransmisión. Este ejercicio asume cierta familiaridad con Visual Studio y por lo tanto, no se recorre a través de todos los detalles de Hola de creación de un proyecto. En su lugar, se centra en el código de hello.

Antes de iniciar estos pasos, complete Hola siguiendo el procedimiento tooset del entorno:

1. En Visual Studio, cree una aplicación de consola que contiene dos proyectos, "Cliente" y "Servicio", dentro de la solución de Hola.
2. Agregar proyectos de tooboth de paquete de NuGet de Bus de servicio de Hola. Este paquete agrega todos los proyectos de tooyour de referencias de ensamblado necesarias Hola.

### <a name="how-toocreate-hello-service"></a>¿Cómo toocreate Hola servicio
En primer lugar, cree el propio servicio Hola. Los servicios WCF cuentan con al menos tres partes distintas:

* Definición de un contrato que describe qué mensajes se intercambian y qué operaciones están toobe invocada.
* Implementación de dicho contrato.
* Host que hospeda el servicio WCF de Hola y expone varios puntos de conexión.

ejemplos de código de Hello en esta sección solucionar cada uno de estos componentes.

contrato de Hello define una sola operación, `AddNumbers`, que suma dos números y devuelve el resultado de hello. Hola `IProblemSolverChannel` Hola cliente toomore de interfaz permite administrar fácilmente la duración de proxy de Hola. La creación de esta interfaz se considera una práctica recomendada. Es una buena idea tooput esta definición en un archivo separado del contrato para que se puede hacer referencia a ese archivo proyectos de la "Cliente" y el "Servicio", pero también puede copiar el código de hello en ambos proyectos.

```csharp
using System.ServiceModel;

[ServiceContract(Namespace = "urn:ps")]
interface IProblemSolver
{
    [OperationContract]
    int AddNumbers(int a, int b);
}

interface IProblemSolverChannel : IProblemSolver, IClientChannel {}
```

Con el contrato de hello en su lugar, implementación de hello es la siguiente:

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a>Configuración de un host de servicio mediante programación
Con el contrato de Hola y la implementación en su lugar, ahora puede hospedar el servicio de Hola. Hospedaje aparece dentro de un [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) de objetos, que se encarga de administrar instancias de servicio de Hola y hosts Hola extremos a los que realizar escuchas de mensajes. Hello siguiente código configura el servicio de hello con un extremo local normal y una apariencia de Hola de retransmisión extremo tooillustrate, unos junto a otros, de extremos internos y externos. Reemplace la cadena hello *espacio de nombres* por el nombre del espacio de nombres y *yourKey* con la clave SAS de Hola que obtuvo en el paso de instalación anterior de Hola.

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));

sh.AddServiceEndpoint(
   typeof (IProblemSolver), new NetTcpBinding(),
   "net.tcp://localhost:9358/solver");

sh.AddServiceEndpoint(
   typeof(IProblemSolver), new NetTcpRelayBinding(),
   ServiceBusEnvironment.CreateServiceUri("sb", "namespace", "solver"))
    .Behaviors.Add(new TransportClientEndpointBehavior {
          TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", "<yourKey>")});

sh.Open();

Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();

sh.Close();
```

En el ejemplo de Hola, cree dos extremos que se encuentran en hello misma implementación del contrato. Uno es local y el otro se proyecta a través de Azure Relay. Hola diferencia principal entre ellos consiste en enlaces de hello; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) para hello local y [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) para el extremo de retransmisión de Hola y direcciones de Hola. extremo local Hello tiene una dirección de red local con un puerto distinto. extremo de retransmisión Hello tiene una dirección de extremo formada por cadena hello `sb`, el nombre de espacio de nombres y ruta de acceso de Hola "solver." Esto da como resultado Hola URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifica el extremo de servicio de Hola como un extremo TCP de Bus de servicio (retransmisión) con un nombre completo de DNS externo. Si coloca código de hello reemplazando los marcadores de posición de hello en hello `Main` función de hello **servicio** aplicación, tendrá un servicio funcional. Si desea que su toolisten servicio exclusivamente en retransmisión hello, quite la declaración de punto de conexión local de Hola.

### <a name="configure-a-service-host-in-hello-appconfig-file"></a>Configurar un host de servicio en el archivo App.config de hello
También puede configurar el host de hello mediante el archivo App.config de hello. en este caso, el código de hospedaje de servicio de Hello aparece en el ejemplo siguiente se Hola.

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();
sh.Close();
```

Mueva las definiciones de extremo de Hello en el archivo App.config de hello. paquete de NuGet Hola ya ha agregado un intervalo del archivo App.config de definiciones toohello, que son extensiones de configuración de hello necesario para la retransmisión de Azure. Hola siguiente ejemplo, que es hello exacto equivalente de código anterior, hello, debería aparecer directamente bajo hello **system.serviceModel** elemento. Este ejemplo de código presupone que el espacio de nombres C# del proyecto tiene el nombre de **Service**.
Reemplace los marcadores de posición de hello con el nombre de espacio de nombres de retransmisión y la clave SAS.

```xml
<services>
    <service name="Service.ProblemSolver">
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpBinding"
                  address="net.tcp://localhost:9358/solver"/>
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpRelayBinding"
                  address="sb://<namespaceName>.servicebus.windows.net/solver"
                  behaviorConfiguration="sbTokenProvider"/>
    </service>
</services>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

Después de realizar estos cambios, Hola servicio se inicia como lo hacía anteriormente, pero con dos puntos de conexión activos: uno local y una escucha en la nube de Hola.

### <a name="create-hello-client"></a>Crear el cliente de Hola
#### <a name="configure-a-client-programmatically"></a>Configuración de un cliente mediante programación
servicio de hello tooconsume, puede construir un cliente WCF mediante un [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) objeto. El Bus de servicio usa un modelo basado en tokens de seguridad implementado mediante SAS. Hola [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) clase representa un proveedor de tokens de seguridad con métodos de fábrica integrados que devuelven algunos proveedores de tokens bien conocidos. Hello en el ejemplo siguiente se usa hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) adquisición de hello toohandle de método de token SAS adecuado de Hola. Hola nombre y la clave son los obtenidos de portal de hello, tal como se describe en la sección anterior de Hola.

Primero, referencia o copia hello `IProblemSolver` de contrato de código del servicio de hello en el proyecto de cliente.

A continuación, reemplace el código de hello en hello `Main` método del cliente de hello, vuelva a reemplazar texto de marcador de posición de hello con el espacio de nombres de retransmisión y la clave SAS.

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>(
    new NetTcpRelayBinding(),
    new EndpointAddress(ServiceBusEnvironment.CreateServiceUri("sb", "<namespaceName>", "solver")));

cf.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior
            { TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey","<yourKey>") });

using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

Ahora puede compilar el cliente de Hola y el servicio de hello, ejecutarlos (ejecución de servicio de hello en primer lugar) y cliente de hello llama Hola servicio e imprime **9**. Puede ejecutar Hola cliente y servidor en equipos diferentes, incluso a través de redes y comunicación de hello seguirán funcionando. También puede ejecutar el código de cliente de Hello en nube de Hola o localmente.

#### <a name="configure-a-client-in-hello-appconfig-file"></a>Configurar a un cliente en el archivo App.config de hello
Hola siguiente código muestra cómo el cliente de hello tooconfigure mediante Hola archivo App.config.

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

Mueva las definiciones de extremo de Hello en el archivo App.config de hello. el ejemplo siguiente, que es hello igual que el código de hello indicada anteriormente, Hello debe aparecer una directamente debajo de hello `<system.serviceModel>` elemento. En este caso, como antes, debe reemplazar los marcadores de posición de hello con el espacio de nombres de retransmisión y la clave SAS.

```xml
<client>
    <endpoint name="solver" contract="Service.IProblemSolver"
              binding="netTcpRelayBinding"
              address="sb://<namespaceName>.servicebus.windows.net/solver"
              behaviorConfiguration="sbTokenProvider"/>
</client>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que conoce los fundamentos de Hola de retransmisión de Azure, siga estas toolearn de vínculos más.

* [¿Qué es Relay de Azure?](relay-what-is-it.md)
* [Información general sobre la arquitectura de Azure Service Bus](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* Descargar ejemplos de Bus de servicio de [ejemplos Azure] [ Azure samples] o vea hello [descripción general de los ejemplos de Service Bus][overview of Service Bus samples].

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
