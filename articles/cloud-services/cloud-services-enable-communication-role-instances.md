---
title: "Comunicación para roles en Cloud Services | Microsoft Docs"
description: "Las instancias de rol de los servicios en la nube pueden tener definidos puntos de conexión (http, https, tcp y udp) que se comunican con el exterior o entre otras instancias de rol."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7008a083-acbe-4fb8-ae60-b837ef971ca1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: 8e171d56bb67c971337fa383014988074ec828b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="3f556-103">Habilitar la comunicación para instancias de rol en Azure</span><span class="sxs-lookup"><span data-stu-id="3f556-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="3f556-104">Los roles de servicio en la nube se comunican a través de conexiones internas y externas.</span><span class="sxs-lookup"><span data-stu-id="3f556-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="3f556-105">Las conexiones externas se denominan **puntos de conexión de entrada** mientras que conexiones internas se denominan **puntos de conexión internos**.</span><span class="sxs-lookup"><span data-stu-id="3f556-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="3f556-106">En este tema se describe cómo modificar la [definición de servicio](cloud-services-model-and-package.md#csdef) para crear puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="3f556-106">This topic describes how to modify the [service definition](cloud-services-model-and-package.md#csdef) to create endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="3f556-107">Extremo de entrada</span><span class="sxs-lookup"><span data-stu-id="3f556-107">Input endpoint</span></span>
<span data-ttu-id="3f556-108">Los extremos de entrada se usan para exponer un puerto al exterior.</span><span class="sxs-lookup"><span data-stu-id="3f556-108">The input endpoint is used when you want to expose a port to the outside.</span></span> <span data-ttu-id="3f556-109">Tiene que especificar el tipo de protocolo y el puerto del extremo que se aplicará a los puertos internos y externos del extremo.</span><span class="sxs-lookup"><span data-stu-id="3f556-109">You specify the protocol type and the port of the endpoint which then applies for both the external and internal ports for the endpoint.</span></span> <span data-ttu-id="3f556-110">Si lo desea, puede especificar un puerto interno diferente para el extremo mediante el atributo [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) .</span><span class="sxs-lookup"><span data-stu-id="3f556-110">If you want, you can specify a different internal port for the endpoint with the [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="3f556-111">El extremo de entrada puede usar los siguientes protocolos: **http, https, tcp y udp**.</span><span class="sxs-lookup"><span data-stu-id="3f556-111">The input endpoint can use the following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="3f556-112">Para crear un punto de conexión de entrada, agregue el elemento secundario **InputEndpoint** al elemento **Endpoints** de un rol web o de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3f556-112">To create an input endpoint, add the **InputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="3f556-113">Extremo de entrada de instancia</span><span class="sxs-lookup"><span data-stu-id="3f556-113">Instance input endpoint</span></span>
<span data-ttu-id="3f556-114">Los extremos de entrada de instancia son similares a los extremos de entrada, pero los primeros permiten asignar puertos específicos de acceso público a cada instancia de rol individual mediante el enrutamiento de puertos en el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="3f556-114">Instance input endpoints are similar to input endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on the load balancer.</span></span> <span data-ttu-id="3f556-115">Puede especificar un único puerto público o un intervalo de puertos.</span><span class="sxs-lookup"><span data-stu-id="3f556-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="3f556-116">Solo puede utilizar el punto de conexión de entrada de instancia como protocolo **tcp** o **udp**.</span><span class="sxs-lookup"><span data-stu-id="3f556-116">The instance input endpoint can only use **tcp** or **udp** as the protocol.</span></span>

<span data-ttu-id="3f556-117">Para crear un punto de conexión de entrada de instancia, agregue el elemento secundario **InstanceInputEndpoint** al elemento **Endpoints** del rol web o de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3f556-117">To create an instance input endpoint, add the **InstanceInputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="3f556-118">Extremo interno</span><span class="sxs-lookup"><span data-stu-id="3f556-118">Internal endpoint</span></span>
<span data-ttu-id="3f556-119">Los extremos internos están disponibles para la comunicación entre instancias.</span><span class="sxs-lookup"><span data-stu-id="3f556-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="3f556-120">El puerto es opcional y si se omite, se asigna un puerto dinámico al extremo.</span><span class="sxs-lookup"><span data-stu-id="3f556-120">The port is optional and if omitted, a dynamic port is assigned to the endpoint.</span></span> <span data-ttu-id="3f556-121">Además, puede usar un intervalo de puertos.</span><span class="sxs-lookup"><span data-stu-id="3f556-121">A port range can be used.</span></span> <span data-ttu-id="3f556-122">Recuerde que hay un límite de cinco extremos internos por rol.</span><span class="sxs-lookup"><span data-stu-id="3f556-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="3f556-123">El extremo interno puede usar los siguientes protocolos: **http, tcp, udp y any**.</span><span class="sxs-lookup"><span data-stu-id="3f556-123">The internal endpoint can use the following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="3f556-124">Para crear un punto de conexión de entrada interno, agregue el elemento secundario **InternalEndpoint** al elemento **Endpoints** de un rol web o de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3f556-124">To create an internal input endpoint, add the **InternalEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="3f556-125">También puede usar un intervalo de puertos.</span><span class="sxs-lookup"><span data-stu-id="3f556-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="3f556-126">Roles de trabajo en comparación con los Roles web</span><span class="sxs-lookup"><span data-stu-id="3f556-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="3f556-127">Hay una pequeña diferencia entre los extremos cuando se trabaja con roles web y de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3f556-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="3f556-128">El rol web debe tener como mínimo un extremo de entrada que use el protocolo **HTTP** .</span><span class="sxs-lookup"><span data-stu-id="3f556-128">The web role must have at minimum a single input endpoint using the **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after the first InputEndPoint -->
</Endpoints>
```

## <a name="using-the-net-sdk-to-access-an-endpoint"></a><span data-ttu-id="3f556-129">Uso del SDK de .NET para tener acceso a un extremo</span><span class="sxs-lookup"><span data-stu-id="3f556-129">Using the .NET SDK to access an endpoint</span></span>
<span data-ttu-id="3f556-130">La Biblioteca administrada de Azure proporciona métodos a las instancias de rol para que puedan comunicarse en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="3f556-130">The Azure Managed Library provides methods for role instances to communicate at runtime.</span></span> <span data-ttu-id="3f556-131">Mediante el código que se ejecuta en una instancia de rol, puede recuperar información sobre la existencia de otras instancias de rol y sus extremos, así como información sobre la instancia de rol actual.</span><span class="sxs-lookup"><span data-stu-id="3f556-131">From code running within a role instance, you can retrieve information about the existence of other role instances and their endpoints, as well as information about the current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="3f556-132">Solo puede recuperar información sobre las instancias de rol que se ejecuten en el servicio en la nube y que definan, al menos, un extremo interno.</span><span class="sxs-lookup"><span data-stu-id="3f556-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="3f556-133">Asimismo, no puede obtener datos sobre instancias de rol que se ejecuten en un servicio diferente.</span><span class="sxs-lookup"><span data-stu-id="3f556-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="3f556-134">Puede usar la propiedad [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) para recuperar las instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="3f556-134">You can use the [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property to retrieve instances of a role.</span></span> <span data-ttu-id="3f556-135">Primero, use el elemento [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) para devolver una referencia a la instancia de rol actual y, a continuación, use la propiedad [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) para devolver una referencia al propio rol.</span><span class="sxs-lookup"><span data-stu-id="3f556-135">First use the [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) to return a reference to the current role instance, and then use the [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property to return a reference to the role itself.</span></span>

<span data-ttu-id="3f556-136">Si se conecta a una instancia de rol mediante programación a través del SDK de .NET, le será relativamente fácil obtener acceso a la información del extremo.</span><span class="sxs-lookup"><span data-stu-id="3f556-136">When you connect to a role instance programmatically through the .NET SDK, it's relatively easy to access the endpoint information.</span></span> <span data-ttu-id="3f556-137">Por ejemplo, una vez se haya conectado a un entorno de rol específico, puede obtener el puerto de un extremo en concreto con este código:</span><span class="sxs-lookup"><span data-stu-id="3f556-137">For example, after you've already connected to a specific role environment, you can get the port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="3f556-138">La propiedad **Instances** devuelve una colección de objetos **RoleInstance**.</span><span class="sxs-lookup"><span data-stu-id="3f556-138">The **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="3f556-139">Tenga en cuenta que esta colección siempre contiene la instancia actual.</span><span class="sxs-lookup"><span data-stu-id="3f556-139">This collection always contains the current instance.</span></span> <span data-ttu-id="3f556-140">Si el rol no define un extremo interno, la colección incluirá la instancia actual, pero no otras instancias.</span><span class="sxs-lookup"><span data-stu-id="3f556-140">If the role does not define an internal endpoint, the collection includes the current instance but no other instances.</span></span> <span data-ttu-id="3f556-141">El número de instancias de rol presentes en la colección siempre será 1, si resulta que no se ha definido ningún extremo interno para el rol.</span><span class="sxs-lookup"><span data-stu-id="3f556-141">The number of role instances in the collection will always be 1 in the case where no internal endpoint is defined for the role.</span></span> <span data-ttu-id="3f556-142">Si el rol define un extremo interno, sus instancias serán reconocibles en tiempo de ejecución y el número de instancias de la colección se corresponderá con el número de instancias especificadas para el rol en el archivo de configuración de servicio.</span><span class="sxs-lookup"><span data-stu-id="3f556-142">If the role defines an internal endpoint, its instances are discoverable at runtime, and the number of instances in the collection will correspond to the number of instances specified for the role in the service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="3f556-143">La Biblioteca administrada de Azure no le proporciona una manera de determinar el estado de otras instancias de rol, pero siempre puede implementar estas evaluaciones de estado si el servicio necesita esta funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="3f556-143">The Azure Managed Library does not provide a means of determining the health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="3f556-144">Puede usar [Diagnósticos de Azure](cloud-services-dotnet-diagnostics.md) para obtener información acerca de las instancias de rol que se estén ejecutando.</span><span class="sxs-lookup"><span data-stu-id="3f556-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) to obtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="3f556-145">Para determinar el número de puerto de un extremo interno en una instancia de rol, puede usar la propiedad [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) para devolver un objeto Dictionary que contenga los nombres de extremo y sus direcciones IP y puertos correspondientes.</span><span class="sxs-lookup"><span data-stu-id="3f556-145">To determine the port number for an internal endpoint on a role instance, you can use the [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property to return a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="3f556-146">La propiedad [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) devuelve la dirección IP y el puerto de un extremo específico.</span><span class="sxs-lookup"><span data-stu-id="3f556-146">The [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns the IP address and port for a specified endpoint.</span></span> <span data-ttu-id="3f556-147">La propiedad **PublicIPEndpoint** devuelve el puerto de un extremo con equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="3f556-147">The **PublicIPEndpoint** property returns the port for a load balanced endpoint.</span></span> <span data-ttu-id="3f556-148">La parte de la dirección IP de la propiedad **PublicIPEndpoint** no se usa.</span><span class="sxs-lookup"><span data-stu-id="3f556-148">The IP address portion of the **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="3f556-149">Aquí tiene un ejemplo que itera las instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="3f556-149">Here is an example that iterates role instances.</span></span>

```csharp
foreach (RoleInstance roleInst in RoleEnvironment.CurrentRoleInstance.Role.Instances)
{
    Trace.WriteLine("Instance ID: " + roleInst.Id);
    foreach (RoleInstanceEndpoint roleInstEndpoint in roleInst.InstanceEndpoints.Values)
    {
        Trace.WriteLine("Instance endpoint IP address and port: " + roleInstEndpoint.IPEndpoint);
    }
}
```

<span data-ttu-id="3f556-150">Aquí tiene el ejemplo de un rol de trabajo que obtiene el extremo expuesto a través de la definición de servicio, y que inicia la escucha de conexiones.</span><span class="sxs-lookup"><span data-stu-id="3f556-150">Here is an example of a worker role that gets the endpoint exposed through the service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="3f556-151">Este código solo funcionará en un servicio implementado.</span><span class="sxs-lookup"><span data-stu-id="3f556-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="3f556-152">Cuando se ejecutan en el Emulador de procesos de Azure, los elementos de configuración de servicio que crean extremos de puerto directo (elementos**InstanceInputEndpoint** ) se ignoran.</span><span class="sxs-lookup"><span data-stu-id="3f556-152">When running in the Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
> 
> 

```csharp
using System;
using System.Diagnostics;
using System.Linq;
using System.Net;
using System.Net.Sockets;
using System.Threading;
using Microsoft.WindowsAzure;
using Microsoft.WindowsAzure.Diagnostics;
using Microsoft.WindowsAzure.ServiceRuntime;
using Microsoft.WindowsAzure.StorageClient;

namespace WorkerRole1
{
  public class WorkerRole : RoleEntryPoint
  {
    public override void Run()
    {
      try
      {
        // Initialize method-wide variables
        var epName = "Endpoint1";
        var roleInstance = RoleEnvironment.CurrentRoleInstance;

        // Identify direct communication port
        var myPublicEp = roleInstance.InstanceEndpoints[epName].PublicIPEndpoint;
        Trace.TraceInformation("IP:{0}, Port:{1}", myPublicEp.Address, myPublicEp.Port);

        // Identify public endpoint
        var myInternalEp = roleInstance.InstanceEndpoints[epName].IPEndpoint;

        // Create socket listener
        var listener = new Socket(
          myInternalEp.AddressFamily, SocketType.Stream, ProtocolType.Tcp);

        // Bind socket listener to internal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block the thread and wait for a client request
          Socket handler = listener.Accept();
          Trace.TraceInformation("Client request received.");

          // Define body of socket handler
          var handlerThread = new Thread(
            new ParameterizedThreadStart(h =>
            {
              var socket = h as Socket;
              Trace.TraceInformation("Local:{0} Remote{1}",
                socket.LocalEndPoint, socket.RemoteEndPoint);

              // Shut down and close socket
              socket.Shutdown(SocketShutdown.Both);
              socket.Close();
            }
          ));

          // Start socket handler on new thread
          handlerThread.Start(handler);
        }
      }
      catch (Exception e)
      {
        Trace.TraceError("Caught exception in run. Details: {0}", e);
      }
    }

    public override bool OnStart()
    {
      // Set the maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see the MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-to-control-role-communication"></a><span data-ttu-id="3f556-153">Reglas de tráfico de red para controlar la comunicación entre roles</span><span class="sxs-lookup"><span data-stu-id="3f556-153">Network traffic rules to control role communication</span></span>
<span data-ttu-id="3f556-154">Una vez definidos los extremos internos, puede agregar reglas de tráfico de red (basadas en los extremos que haya creado) para controlar el modo en que se comunican las instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="3f556-154">After you define internal endpoints, you can add network traffic rules (based on the endpoints that you created) to control how role instances can communicate with each other.</span></span> <span data-ttu-id="3f556-155">En el siguiente diagrama verá algunos escenarios comunes para controlar la comunicación entre roles:</span><span class="sxs-lookup"><span data-stu-id="3f556-155">The following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="3f556-156">![Escenarios de reglas de tráfico de red](./media/cloud-services-enable-communication-role-instances/scenarios.png "Escenarios de reglas de tráfico de red")</span><span class="sxs-lookup"><span data-stu-id="3f556-156">![Network Traffic Rules Scenarios](./media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="3f556-157">En el siguiente ejemplo de código verá las definiciones de rol de los roles que se mostraban en el diagrama anterior.</span><span class="sxs-lookup"><span data-stu-id="3f556-157">The following code example shows role definitions for the roles shown in the previous diagram.</span></span> <span data-ttu-id="3f556-158">Cada definición de rol incluye, al menos, un extremo interno definido:</span><span class="sxs-lookup"><span data-stu-id="3f556-158">Each role definition includes at least one internal endpoint defined:</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalTCP1" protocol="tcp" />
    </Endpoints>
  </WebRole>
  <WorkerRole name="WorkerRole1">
    <Endpoints>
      <InternalEndpoint name="InternalTCP2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
  <WorkerRole name="WorkerRole2">
    <Endpoints>
      <InternalEndpoint name="InternalTCP3" protocol="tcp" />
      <InternalEndpoint name="InternalTCP4" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

> [!NOTE]
> <span data-ttu-id="3f556-159">Es posible que los extremos internos de tanto puertos asignados fijos como automáticos tengan restricciones de comunicación entre roles.</span><span class="sxs-lookup"><span data-stu-id="3f556-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="3f556-160">De forma predeterminada, una vez definido el extremo interno, la comunicación puede fluir sin restricciones desde cualquier rol hasta el extremo interno de otro rol.</span><span class="sxs-lookup"><span data-stu-id="3f556-160">By default, after an internal endpoint is defined, communication can flow from any role to the internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="3f556-161">Para restringir la comunicación, debe agregar un elemento **NetworkTrafficRules** al elemento **ServiceDefinition** que se encuentra en el archivo de definición de servicio.</span><span class="sxs-lookup"><span data-stu-id="3f556-161">To restrict communication, you must add a **NetworkTrafficRules** element to the **ServiceDefinition** element in the service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="3f556-162">Escenario 1.</span><span class="sxs-lookup"><span data-stu-id="3f556-162">Scenario 1</span></span>
<span data-ttu-id="3f556-163">Permitir solo el tráfico de red de **WebRole1** a **WorkerRole1**.</span><span class="sxs-lookup"><span data-stu-id="3f556-163">Only allow network traffic from **WebRole1** to **WorkerRole1**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-2"></a><span data-ttu-id="3f556-164">Escenario 2.</span><span class="sxs-lookup"><span data-stu-id="3f556-164">Scenario 2</span></span>
<span data-ttu-id="3f556-165">Permitir solo el tráfico de red de **WebRole1** a **WorkerRole1** y **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="3f556-165">Only allows network traffic from **WebRole1** to **WorkerRole1** and **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-3"></a><span data-ttu-id="3f556-166">Escenario 3.</span><span class="sxs-lookup"><span data-stu-id="3f556-166">Scenario 3</span></span>
<span data-ttu-id="3f556-167">Permitir solo el tráfico de red de **WebRole1** a **WorkerRole1** y **WorkerRole1** a **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="3f556-167">Only allows network traffic from **WebRole1** to **WorkerRole1**, and **WorkerRole1** to **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-4"></a><span data-ttu-id="3f556-168">Escenario 4.</span><span class="sxs-lookup"><span data-stu-id="3f556-168">Scenario 4</span></span>
<span data-ttu-id="3f556-169">Permitir solo el tráfico de red de **WebRole1** a **WorkerRole1**, **WebRole1** a **WorkerRole2** y **WorkerRole1** a **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="3f556-169">Only allows network traffic from **WebRole1** to **WorkerRole1**, **WebRole1** to **WorkerRole2**, and **WorkerRole1** to **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP4" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

<span data-ttu-id="3f556-170">Puede encontrar una referencia del esquema XML de los elementos usados anteriormente [aquí](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f556-170">An XML schema reference for the elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f556-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3f556-171">Next steps</span></span>
<span data-ttu-id="3f556-172">Obtenga más información sobre el [modelo](cloud-services-model-and-package.md)del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="3f556-172">Read more about the Cloud Service [model](cloud-services-model-and-package.md).</span></span>

