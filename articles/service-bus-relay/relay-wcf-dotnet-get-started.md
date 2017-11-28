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
# <a name="how-toouse-azure-relay-wcf-relays-with-net"></a><span data-ttu-id="5c59b-103">¿Cómo toouse Azure retransmisión WCF las retransmisiones con .NET</span><span class="sxs-lookup"><span data-stu-id="5c59b-103">How toouse Azure Relay WCF relays with .NET</span></span>
<span data-ttu-id="5c59b-104">Este artículo describe cómo toouse Hola servicio de retransmisión de Azure.</span><span class="sxs-lookup"><span data-stu-id="5c59b-104">This article describes how toouse hello Azure Relay service.</span></span> <span data-ttu-id="5c59b-105">ejemplos de Hello están escritas en C# y usar la API de Windows Communication Foundation (WCF) de hello con extensiones contenidas en hello ensamblado de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="5c59b-105">hello samples are written in C# and use hello Windows Communication Foundation (WCF) API with extensions contained in hello Service Bus assembly.</span></span> <span data-ttu-id="5c59b-106">Para obtener más información acerca de la retransmisión de Azure, vea hello [Introducción a Azure Relay](relay-what-is-it.md).</span><span class="sxs-lookup"><span data-stu-id="5c59b-106">For more information about Azure relay, see hello [Azure Relay overview](relay-what-is-it.md).</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a><span data-ttu-id="5c59b-107">¿Qué es Retransmisión de WCF?</span><span class="sxs-lookup"><span data-stu-id="5c59b-107">What is WCF Relay?</span></span>

<span data-ttu-id="5c59b-108">Hello Azure [ *retransmisión de WCF* ](relay-what-is-it.md) servicio permite aplicaciones híbridas de toobuild que se ejecutan en un centro de datos de Azure y su propio entorno de empresa local.</span><span class="sxs-lookup"><span data-stu-id="5c59b-108">hello Azure [*WCF Relay*](relay-what-is-it.md) service enables you toobuild hybrid applications that run in both an Azure datacenter and your own on-premises enterprise environment.</span></span> <span data-ttu-id="5c59b-109">servicio de retransmisión de Hello facilita este proceso permitiéndole toosecurely exponer los servicios de Windows Communication Foundation (WCF) que residen dentro de una nube pública de la toohello de red empresas corporativas, sin tener tooopen una conexión de servidor de seguridad o requerir infraestructura de red corporativa de cambios intrusivo tooa.</span><span class="sxs-lookup"><span data-stu-id="5c59b-109">hello relay service facilitates this by enabling you toosecurely expose Windows Communication Foundation (WCF) services that reside within a corporate enterprise network toohello public cloud, without having tooopen a firewall connection, or requiring intrusive changes tooa corporate network infrastructure.</span></span>

![Conceptos del relé WCF](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

<span data-ttu-id="5c59b-111">Retransmisión de Azure permite toohost los servicios WCF en el entorno empresarial existente.</span><span class="sxs-lookup"><span data-stu-id="5c59b-111">Azure Relay enables you toohost WCF services within your existing enterprise environment.</span></span> <span data-ttu-id="5c59b-112">A continuación, puede delegar la escucha entrantes sesiones y solicitudes toothese WCF services toohello servicio de retransmisión de ejecución dentro de Azure.</span><span class="sxs-lookup"><span data-stu-id="5c59b-112">You can then delegate listening for incoming sessions and requests toothese WCF services toohello relay service running within Azure.</span></span> <span data-ttu-id="5c59b-113">Esto permite tooexpose estos servicios tooapplication código se ejecuta en Azure, o los trabajadores toomobile o entornos de extranet de socio comercial.</span><span class="sxs-lookup"><span data-stu-id="5c59b-113">This enables you tooexpose these services tooapplication code running in Azure, or toomobile workers or extranet partner environments.</span></span> <span data-ttu-id="5c59b-114">Retransmisión le permite controlar toosecurely quién puede acceder a estos servicios en un nivel específico.</span><span class="sxs-lookup"><span data-stu-id="5c59b-114">Relay enables you toosecurely control who can access these services at a fine-grained level.</span></span> <span data-ttu-id="5c59b-115">Proporciona una funcionalidad de la aplicación de forma eficaz y segura tooexpose y los datos de las soluciones empresariales existentes y aprovechar las ventajas del mismo desde la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c59b-115">It provides a powerful and secure way tooexpose application functionality and data from your existing enterprise solutions and take advantage of it from hello cloud.</span></span>

<span data-ttu-id="5c59b-116">Este artículo describe cómo toouse toocreate de retransmisión de Azure en que un servicio web WCF, exponen de mediante un enlace de canal TCP, que implementa una conversación segura entre dos entidades.</span><span class="sxs-lookup"><span data-stu-id="5c59b-116">This article discusses how toouse Azure Relay toocreate a WCF web service, exposed using a TCP channel binding, that implements a secure conversation between two parties.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-hello-service-bus-nuget-package"></a><span data-ttu-id="5c59b-117">Obtener el paquete de NuGet de Bus de servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="5c59b-117">Get hello Service Bus NuGet package</span></span>
<span data-ttu-id="5c59b-118">Hola [paquete NuGet de Bus de servicio](https://www.nuget.org/packages/WindowsAzure.ServiceBus) es hello tooget de manera más fácil de hello API de Service Bus y tooconfigure la aplicación con todas las dependencias de Bus de servicio de Hola de.</span><span class="sxs-lookup"><span data-stu-id="5c59b-118">hello [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is hello easiest way tooget hello Service Bus API and tooconfigure your application with all of hello Service Bus dependencies.</span></span> <span data-ttu-id="5c59b-119">paquete de NuGet tooinstall hello en el proyecto, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="5c59b-119">tooinstall hello NuGet package in your project, do hello following:</span></span>

1. <span data-ttu-id="5c59b-120">En el Explorador de soluciones, haga clic con el botón derecho en **Referencias** y, a continuación, en **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5c59b-120">In Solution Explorer, right-click **References**, then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="5c59b-121">La búsqueda de "Bus de servicio" y seleccione hello **Microsoft Azure Service Bus** elemento.</span><span class="sxs-lookup"><span data-stu-id="5c59b-121">Search for "Service Bus" and select hello **Microsoft Azure Service Bus** item.</span></span> <span data-ttu-id="5c59b-122">Haga clic en **instalar** toocomplete Hola instalación y luego cierre Hola después el cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="5c59b-122">Click **Install** toocomplete hello installation, then close hello following dialog box:</span></span>
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a><span data-ttu-id="5c59b-123">Exponga y consuma un servicio web SOAP con TCP</span><span class="sxs-lookup"><span data-stu-id="5c59b-123">Expose and consume a SOAP web service with TCP</span></span>
<span data-ttu-id="5c59b-124">tooexpose un servicio web de SOAP de WCF existente para su uso externo, debe realizar los cambios toohello los enlaces de servicio y las direcciones.</span><span class="sxs-lookup"><span data-stu-id="5c59b-124">tooexpose an existing WCF SOAP web service for external consumption, you must make changes toohello service bindings and addresses.</span></span> <span data-ttu-id="5c59b-125">Esto podría precisar el archivo de configuración de tooyour de cambios o podría requerir cambios en el código, dependiendo de cómo se configurado y configura los servicios WCF.</span><span class="sxs-lookup"><span data-stu-id="5c59b-125">This may require changes tooyour configuration file or it could require code changes, depending on how you have set up and configured your WCF services.</span></span> <span data-ttu-id="5c59b-126">Tenga en cuenta que WCF permite toohave varios puntos de conexión de red sobre Hola mismo servicio, por lo que puede conservar Hola existente extremos internos al agregar extremos de retransmisión para external acceso en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="5c59b-126">Note that WCF allows you toohave multiple network endpoints over hello same service, so you can retain hello existing internal endpoints while adding relay endpoints for external access at hello same time.</span></span>

<span data-ttu-id="5c59b-127">En esta tarea, crear un servicio WCF simple y agregar un tooit de agente de escucha de retransmisión.</span><span class="sxs-lookup"><span data-stu-id="5c59b-127">In this task, you build a simple WCF service and add a relay listener tooit.</span></span> <span data-ttu-id="5c59b-128">Este ejercicio asume cierta familiaridad con Visual Studio y por lo tanto, no se recorre a través de todos los detalles de Hola de creación de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="5c59b-128">This exercise assumes some familiarity with Visual Studio, and therefore does not walk through all hello details of creating a project.</span></span> <span data-ttu-id="5c59b-129">En su lugar, se centra en el código de hello.</span><span class="sxs-lookup"><span data-stu-id="5c59b-129">Instead, it focuses on hello code.</span></span>

<span data-ttu-id="5c59b-130">Antes de iniciar estos pasos, complete Hola siguiendo el procedimiento tooset del entorno:</span><span class="sxs-lookup"><span data-stu-id="5c59b-130">Before starting these steps, complete hello following procedure tooset up your environment:</span></span>

1. <span data-ttu-id="5c59b-131">En Visual Studio, cree una aplicación de consola que contiene dos proyectos, "Cliente" y "Servicio", dentro de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c59b-131">Within Visual Studio, create a console application that contains two projects, "Client" and "Service", within hello solution.</span></span>
2. <span data-ttu-id="5c59b-132">Agregar proyectos de tooboth de paquete de NuGet de Bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c59b-132">Add hello Service Bus NuGet package tooboth projects.</span></span> <span data-ttu-id="5c59b-133">Este paquete agrega todos los proyectos de tooyour de referencias de ensamblado necesarias Hola.</span><span class="sxs-lookup"><span data-stu-id="5c59b-133">This package adds all hello necessary assembly references tooyour projects.</span></span>

### <a name="how-toocreate-hello-service"></a><span data-ttu-id="5c59b-134">¿Cómo toocreate Hola servicio</span><span class="sxs-lookup"><span data-stu-id="5c59b-134">How toocreate hello service</span></span>
<span data-ttu-id="5c59b-135">En primer lugar, cree el propio servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="5c59b-135">First, create hello service itself.</span></span> <span data-ttu-id="5c59b-136">Los servicios WCF cuentan con al menos tres partes distintas:</span><span class="sxs-lookup"><span data-stu-id="5c59b-136">Any WCF service consists of at least three distinct parts:</span></span>

* <span data-ttu-id="5c59b-137">Definición de un contrato que describe qué mensajes se intercambian y qué operaciones están toobe invocada.</span><span class="sxs-lookup"><span data-stu-id="5c59b-137">Definition of a contract that describes what messages are exchanged and what operations are toobe invoked.</span></span>
* <span data-ttu-id="5c59b-138">Implementación de dicho contrato.</span><span class="sxs-lookup"><span data-stu-id="5c59b-138">Implementation of that contract.</span></span>
* <span data-ttu-id="5c59b-139">Host que hospeda el servicio WCF de Hola y expone varios puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="5c59b-139">Host that hosts hello WCF service and exposes several endpoints.</span></span>

<span data-ttu-id="5c59b-140">ejemplos de código de Hello en esta sección solucionar cada uno de estos componentes.</span><span class="sxs-lookup"><span data-stu-id="5c59b-140">hello code examples in this section address each of these components.</span></span>

<span data-ttu-id="5c59b-141">contrato de Hello define una sola operación, `AddNumbers`, que suma dos números y devuelve el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="5c59b-141">hello contract defines a single operation, `AddNumbers`, that adds two numbers and returns hello result.</span></span> <span data-ttu-id="5c59b-142">Hola `IProblemSolverChannel` Hola cliente toomore de interfaz permite administrar fácilmente la duración de proxy de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c59b-142">hello `IProblemSolverChannel` interface enables hello client toomore easily manage hello proxy lifetime.</span></span> <span data-ttu-id="5c59b-143">La creación de esta interfaz se considera una práctica recomendada.</span><span class="sxs-lookup"><span data-stu-id="5c59b-143">Creating such an interface is considered a best practice.</span></span> <span data-ttu-id="5c59b-144">Es una buena idea tooput esta definición en un archivo separado del contrato para que se puede hacer referencia a ese archivo proyectos de la "Cliente" y el "Servicio", pero también puede copiar el código de hello en ambos proyectos.</span><span class="sxs-lookup"><span data-stu-id="5c59b-144">It's a good idea tooput this contract definition into a separate file so that you can reference that file from both your "Client" and "Service" projects, but you can also copy hello code into both projects.</span></span>

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

<span data-ttu-id="5c59b-145">Con el contrato de hello en su lugar, implementación de hello es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="5c59b-145">With hello contract in place, hello implementation is as follows:</span></span>

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a><span data-ttu-id="5c59b-146">Configuración de un host de servicio mediante programación</span><span class="sxs-lookup"><span data-stu-id="5c59b-146">Configure a service host programmatically</span></span>
<span data-ttu-id="5c59b-147">Con el contrato de Hola y la implementación en su lugar, ahora puede hospedar el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c59b-147">With hello contract and implementation in place, you can now host hello service.</span></span> <span data-ttu-id="5c59b-148">Hospedaje aparece dentro de un [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) de objetos, que se encarga de administrar instancias de servicio de Hola y hosts Hola extremos a los que realizar escuchas de mensajes.</span><span class="sxs-lookup"><span data-stu-id="5c59b-148">Hosting occurs inside a [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, which takes care of managing instances of hello service and hosts hello endpoints that listen for messages.</span></span> <span data-ttu-id="5c59b-149">Hello siguiente código configura el servicio de hello con un extremo local normal y una apariencia de Hola de retransmisión extremo tooillustrate, unos junto a otros, de extremos internos y externos.</span><span class="sxs-lookup"><span data-stu-id="5c59b-149">hello following code configures hello service with both a regular local endpoint and a relay endpoint tooillustrate hello appearance, side by side, of internal and external endpoints.</span></span> <span data-ttu-id="5c59b-150">Reemplace la cadena hello *espacio de nombres* por el nombre del espacio de nombres y *yourKey* con la clave SAS de Hola que obtuvo en el paso de instalación anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c59b-150">Replace hello string *namespace* with your namespace name and *yourKey* with hello SAS key that you obtained in hello previous setup step.</span></span>

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

<span data-ttu-id="5c59b-151">En el ejemplo de Hola, cree dos extremos que se encuentran en hello misma implementación del contrato.</span><span class="sxs-lookup"><span data-stu-id="5c59b-151">In hello example, you create two endpoints that are on hello same contract implementation.</span></span> <span data-ttu-id="5c59b-152">Uno es local y el otro se proyecta a través de Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="5c59b-152">One is local and one is projected through Azure Relay.</span></span> <span data-ttu-id="5c59b-153">Hola diferencia principal entre ellos consiste en enlaces de hello; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) para hello local y [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) para el extremo de retransmisión de Hola y direcciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c59b-153">hello key differences between them are hello bindings; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) for hello local one and [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) for hello relay endpoint and hello addresses.</span></span> <span data-ttu-id="5c59b-154">extremo local Hello tiene una dirección de red local con un puerto distinto.</span><span class="sxs-lookup"><span data-stu-id="5c59b-154">hello local endpoint has a local network address with a distinct port.</span></span> <span data-ttu-id="5c59b-155">extremo de retransmisión Hello tiene una dirección de extremo formada por cadena hello `sb`, el nombre de espacio de nombres y ruta de acceso de Hola "solver."</span><span class="sxs-lookup"><span data-stu-id="5c59b-155">hello relay endpoint has an endpoint address composed of hello string `sb`, your namespace name, and hello path "solver."</span></span> <span data-ttu-id="5c59b-156">Esto da como resultado Hola URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifica el extremo de servicio de Hola como un extremo TCP de Bus de servicio (retransmisión) con un nombre completo de DNS externo.</span><span class="sxs-lookup"><span data-stu-id="5c59b-156">This results in hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifying hello service endpoint as a Service Bus (relay) TCP endpoint with a fully qualified external DNS name.</span></span> <span data-ttu-id="5c59b-157">Si coloca código de hello reemplazando los marcadores de posición de hello en hello `Main` función de hello **servicio** aplicación, tendrá un servicio funcional.</span><span class="sxs-lookup"><span data-stu-id="5c59b-157">If you place hello code replacing hello placeholders into hello `Main` function of hello **Service** application, you will have a functional service.</span></span> <span data-ttu-id="5c59b-158">Si desea que su toolisten servicio exclusivamente en retransmisión hello, quite la declaración de punto de conexión local de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c59b-158">If you want your service toolisten exclusively on hello relay, remove hello local endpoint declaration.</span></span>

### <a name="configure-a-service-host-in-hello-appconfig-file"></a><span data-ttu-id="5c59b-159">Configurar un host de servicio en el archivo App.config de hello</span><span class="sxs-lookup"><span data-stu-id="5c59b-159">Configure a service host in hello App.config file</span></span>
<span data-ttu-id="5c59b-160">También puede configurar el host de hello mediante el archivo App.config de hello.</span><span class="sxs-lookup"><span data-stu-id="5c59b-160">You can also configure hello host using hello App.config file.</span></span> <span data-ttu-id="5c59b-161">en este caso, el código de hospedaje de servicio de Hello aparece en el ejemplo siguiente se Hola.</span><span class="sxs-lookup"><span data-stu-id="5c59b-161">hello service hosting code in this case appears in hello next example.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();
sh.Close();
```

<span data-ttu-id="5c59b-162">Mueva las definiciones de extremo de Hello en el archivo App.config de hello.</span><span class="sxs-lookup"><span data-stu-id="5c59b-162">hello endpoint definitions move into hello App.config file.</span></span> <span data-ttu-id="5c59b-163">paquete de NuGet Hola ya ha agregado un intervalo del archivo App.config de definiciones toohello, que son extensiones de configuración de hello necesario para la retransmisión de Azure.</span><span class="sxs-lookup"><span data-stu-id="5c59b-163">hello NuGet package has already added a range of definitions toohello App.config file, which are hello required configuration extensions for Azure Relay.</span></span> <span data-ttu-id="5c59b-164">Hola siguiente ejemplo, que es hello exacto equivalente de código anterior, hello, debería aparecer directamente bajo hello **system.serviceModel** elemento.</span><span class="sxs-lookup"><span data-stu-id="5c59b-164">hello following example, which is hello exact equivalent of hello previous code, should appear directly beneath hello **system.serviceModel** element.</span></span> <span data-ttu-id="5c59b-165">Este ejemplo de código presupone que el espacio de nombres C# del proyecto tiene el nombre de **Service**.</span><span class="sxs-lookup"><span data-stu-id="5c59b-165">This code example assumes that your project C# namespace is named **Service**.</span></span>
<span data-ttu-id="5c59b-166">Reemplace los marcadores de posición de hello con el nombre de espacio de nombres de retransmisión y la clave SAS.</span><span class="sxs-lookup"><span data-stu-id="5c59b-166">Replace hello placeholders with your relay namespace name and SAS key.</span></span>

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

<span data-ttu-id="5c59b-167">Después de realizar estos cambios, Hola servicio se inicia como lo hacía anteriormente, pero con dos puntos de conexión activos: uno local y una escucha en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c59b-167">After you make these changes, hello service starts as it did before, but with two live endpoints: one local and one listening in hello cloud.</span></span>

### <a name="create-hello-client"></a><span data-ttu-id="5c59b-168">Crear el cliente de Hola</span><span class="sxs-lookup"><span data-stu-id="5c59b-168">Create hello client</span></span>
#### <a name="configure-a-client-programmatically"></a><span data-ttu-id="5c59b-169">Configuración de un cliente mediante programación</span><span class="sxs-lookup"><span data-stu-id="5c59b-169">Configure a client programmatically</span></span>
<span data-ttu-id="5c59b-170">servicio de hello tooconsume, puede construir un cliente WCF mediante un [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) objeto.</span><span class="sxs-lookup"><span data-stu-id="5c59b-170">tooconsume hello service, you can construct a WCF client using a [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) object.</span></span> <span data-ttu-id="5c59b-171">El Bus de servicio usa un modelo basado en tokens de seguridad implementado mediante SAS.</span><span class="sxs-lookup"><span data-stu-id="5c59b-171">Service Bus uses a token-based security model implemented using SAS.</span></span> <span data-ttu-id="5c59b-172">Hola [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) clase representa un proveedor de tokens de seguridad con métodos de fábrica integrados que devuelven algunos proveedores de tokens bien conocidos.</span><span class="sxs-lookup"><span data-stu-id="5c59b-172">hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) class represents a security token provider with built-in factory methods that return some well-known token providers.</span></span> <span data-ttu-id="5c59b-173">Hello en el ejemplo siguiente se usa hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) adquisición de hello toohandle de método de token SAS adecuado de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c59b-173">hello following example uses hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method toohandle hello acquisition of hello appropriate SAS token.</span></span> <span data-ttu-id="5c59b-174">Hola nombre y la clave son los obtenidos de portal de hello, tal como se describe en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c59b-174">hello name and key are those obtained from hello portal as described in hello previous section.</span></span>

<span data-ttu-id="5c59b-175">Primero, referencia o copia hello `IProblemSolver` de contrato de código del servicio de hello en el proyecto de cliente.</span><span class="sxs-lookup"><span data-stu-id="5c59b-175">First, reference or copy hello `IProblemSolver` contract code from hello service into your client project.</span></span>

<span data-ttu-id="5c59b-176">A continuación, reemplace el código de hello en hello `Main` método del cliente de hello, vuelva a reemplazar texto de marcador de posición de hello con el espacio de nombres de retransmisión y la clave SAS.</span><span class="sxs-lookup"><span data-stu-id="5c59b-176">Then, replace hello code in hello `Main` method of hello client, again replacing hello placeholder text with your relay namespace and SAS key.</span></span>

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

<span data-ttu-id="5c59b-177">Ahora puede compilar el cliente de Hola y el servicio de hello, ejecutarlos (ejecución de servicio de hello en primer lugar) y cliente de hello llama Hola servicio e imprime **9**.</span><span class="sxs-lookup"><span data-stu-id="5c59b-177">You can now build hello client and hello service, run them (run hello service first), and hello client calls hello service and prints **9**.</span></span> <span data-ttu-id="5c59b-178">Puede ejecutar Hola cliente y servidor en equipos diferentes, incluso a través de redes y comunicación de hello seguirán funcionando.</span><span class="sxs-lookup"><span data-stu-id="5c59b-178">You can run hello client and server on different machines, even across networks, and hello communication will still work.</span></span> <span data-ttu-id="5c59b-179">También puede ejecutar el código de cliente de Hello en nube de Hola o localmente.</span><span class="sxs-lookup"><span data-stu-id="5c59b-179">hello client code can also run in hello cloud or locally.</span></span>

#### <a name="configure-a-client-in-hello-appconfig-file"></a><span data-ttu-id="5c59b-180">Configurar a un cliente en el archivo App.config de hello</span><span class="sxs-lookup"><span data-stu-id="5c59b-180">Configure a client in hello App.config file</span></span>
<span data-ttu-id="5c59b-181">Hola siguiente código muestra cómo el cliente de hello tooconfigure mediante Hola archivo App.config.</span><span class="sxs-lookup"><span data-stu-id="5c59b-181">hello following code shows how tooconfigure hello client using hello App.config file.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="5c59b-182">Mueva las definiciones de extremo de Hello en el archivo App.config de hello.</span><span class="sxs-lookup"><span data-stu-id="5c59b-182">hello endpoint definitions move into hello App.config file.</span></span> <span data-ttu-id="5c59b-183">el ejemplo siguiente, que es hello igual que el código de hello indicada anteriormente, Hello debe aparecer una directamente debajo de hello `<system.serviceModel>` elemento.</span><span class="sxs-lookup"><span data-stu-id="5c59b-183">hello following example, which is hello same as hello code listed previously, should appear directly beneath hello `<system.serviceModel>` element.</span></span> <span data-ttu-id="5c59b-184">En este caso, como antes, debe reemplazar los marcadores de posición de hello con el espacio de nombres de retransmisión y la clave SAS.</span><span class="sxs-lookup"><span data-stu-id="5c59b-184">Here, as before, you must replace hello placeholders with your relay namespace and SAS key.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5c59b-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5c59b-185">Next steps</span></span>
<span data-ttu-id="5c59b-186">Ahora que conoce los fundamentos de Hola de retransmisión de Azure, siga estas toolearn de vínculos más.</span><span class="sxs-lookup"><span data-stu-id="5c59b-186">Now that you've learned hello basics of Azure Relay, follow these links toolearn more.</span></span>

* [<span data-ttu-id="5c59b-187">¿Qué es Relay de Azure?</span><span class="sxs-lookup"><span data-stu-id="5c59b-187">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="5c59b-188">Información general sobre la arquitectura de Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="5c59b-188">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* <span data-ttu-id="5c59b-189">Descargar ejemplos de Bus de servicio de [ejemplos Azure] [ Azure samples] o vea hello [descripción general de los ejemplos de Service Bus][overview of Service Bus samples].</span><span class="sxs-lookup"><span data-stu-id="5c59b-189">Download Service Bus samples from [Azure samples][Azure samples] or see hello [overview of Service Bus samples][overview of Service Bus samples].</span></span>

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
