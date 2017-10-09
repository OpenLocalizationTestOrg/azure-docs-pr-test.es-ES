---
title: aaaCommunication para los Roles de servicios en la nube | Documentos de Microsoft
description: "Instancias de rol de servicios en la nube pueden tener puntos de conexión (http, https, tcp y udp) definidas para ellos que se comunican con hello fuera o entre otras instancias de rol."
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
ms.openlocfilehash: 1fb39215ceb8a3f0381ef5e108c1149de115ff8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="44c22-103">Habilitar la comunicación para instancias de rol en Azure</span><span class="sxs-lookup"><span data-stu-id="44c22-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="44c22-104">Los roles de servicio en la nube se comunican a través de conexiones internas y externas.</span><span class="sxs-lookup"><span data-stu-id="44c22-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="44c22-105">Las conexiones externas se denominan **puntos de conexión de entrada** mientras que conexiones internas se denominan **puntos de conexión internos**.</span><span class="sxs-lookup"><span data-stu-id="44c22-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="44c22-106">Este tema se describe cómo hello toomodify [definición del servicio](cloud-services-model-and-package.md#csdef) toocreate extremos.</span><span class="sxs-lookup"><span data-stu-id="44c22-106">This topic describes how toomodify hello [service definition](cloud-services-model-and-package.md#csdef) toocreate endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="44c22-107">Extremo de entrada</span><span class="sxs-lookup"><span data-stu-id="44c22-107">Input endpoint</span></span>
<span data-ttu-id="44c22-108">extremo de entrada de Hola se utiliza cuando se desea tooexpose un toohello puerto fuera.</span><span class="sxs-lookup"><span data-stu-id="44c22-108">hello input endpoint is used when you want tooexpose a port toohello outside.</span></span> <span data-ttu-id="44c22-109">Especifique el tipo de protocolo de Hola y el puerto de hello del extremo de Hola que, a continuación, se aplica a ambos puertos externos e internos de hello para el punto de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="44c22-109">You specify hello protocol type and hello port of hello endpoint which then applies for both hello external and internal ports for hello endpoint.</span></span> <span data-ttu-id="44c22-110">Si lo desea, puede especificar un puerto interno diferente para el punto de conexión de hello con hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) atributo.</span><span class="sxs-lookup"><span data-stu-id="44c22-110">If you want, you can specify a different internal port for hello endpoint with hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="44c22-111">extremo de entrada de Hello sirve Hola siguientes protocolos: **http, https, tcp y udp**.</span><span class="sxs-lookup"><span data-stu-id="44c22-111">hello input endpoint can use hello following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="44c22-112">toocreate un extremo de entrada, agregar hello **InputEndpoint** toohello de elemento secundarios **extremos** elemento de rol web o de trabajo.</span><span class="sxs-lookup"><span data-stu-id="44c22-112">toocreate an input endpoint, add hello **InputEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="44c22-113">Extremo de entrada de instancia</span><span class="sxs-lookup"><span data-stu-id="44c22-113">Instance input endpoint</span></span>
<span data-ttu-id="44c22-114">Los extremos de entrada de instancia son los puntos de conexión de tooinput similar pero permite asignar puertos orientados al público específicos para cada instancia de rol individuales mediante el reenvío de puerto de equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="44c22-114">Instance input endpoints are similar tooinput endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on hello load balancer.</span></span> <span data-ttu-id="44c22-115">Puede especificar un único puerto público o un intervalo de puertos.</span><span class="sxs-lookup"><span data-stu-id="44c22-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="44c22-116">solo puede usar el extremo de entrada de instancia de Hello **tcp** o **udp** como protocolo de Hola.</span><span class="sxs-lookup"><span data-stu-id="44c22-116">hello instance input endpoint can only use **tcp** or **udp** as hello protocol.</span></span>

<span data-ttu-id="44c22-117">toocreate un extremo de entrada de instancia, agregue hello **InstanceInputEndpoint** toohello de elemento secundarios **extremos** elemento de rol web o de trabajo.</span><span class="sxs-lookup"><span data-stu-id="44c22-117">toocreate an instance input endpoint, add hello **InstanceInputEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="44c22-118">Extremo interno</span><span class="sxs-lookup"><span data-stu-id="44c22-118">Internal endpoint</span></span>
<span data-ttu-id="44c22-119">Los extremos internos están disponibles para la comunicación entre instancias.</span><span class="sxs-lookup"><span data-stu-id="44c22-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="44c22-120">puerto de Hello es opcional y si se omite, un puerto dinámico se asigna el punto de conexión de toohello.</span><span class="sxs-lookup"><span data-stu-id="44c22-120">hello port is optional and if omitted, a dynamic port is assigned toohello endpoint.</span></span> <span data-ttu-id="44c22-121">Además, puede usar un intervalo de puertos.</span><span class="sxs-lookup"><span data-stu-id="44c22-121">A port range can be used.</span></span> <span data-ttu-id="44c22-122">Recuerde que hay un límite de cinco extremos internos por rol.</span><span class="sxs-lookup"><span data-stu-id="44c22-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="44c22-123">extremo interno de Hello sirve Hola siguientes protocolos: **http, tcp, udp, cualquier**.</span><span class="sxs-lookup"><span data-stu-id="44c22-123">hello internal endpoint can use hello following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="44c22-124">toocreate un extremo de entrada interno, agregue hello **InternalEndpoint** toohello de elemento secundarios **extremos** elemento de rol web o de trabajo.</span><span class="sxs-lookup"><span data-stu-id="44c22-124">toocreate an internal input endpoint, add hello **InternalEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="44c22-125">También puede usar un intervalo de puertos.</span><span class="sxs-lookup"><span data-stu-id="44c22-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="44c22-126">Roles de trabajo en comparación con los Roles web</span><span class="sxs-lookup"><span data-stu-id="44c22-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="44c22-127">Hay una pequeña diferencia entre los extremos cuando se trabaja con roles web y de trabajo.</span><span class="sxs-lookup"><span data-stu-id="44c22-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="44c22-128">Hello rol web debe tener como mínimo un solo extremo de entrada con hello **HTTP** protocolo.</span><span class="sxs-lookup"><span data-stu-id="44c22-128">hello web role must have at minimum a single input endpoint using hello **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after hello first InputEndPoint -->
</Endpoints>
```

## <a name="using-hello-net-sdk-tooaccess-an-endpoint"></a><span data-ttu-id="44c22-129">Uso de hello .NET SDK tooaccess un punto de conexión</span><span class="sxs-lookup"><span data-stu-id="44c22-129">Using hello .NET SDK tooaccess an endpoint</span></span>
<span data-ttu-id="44c22-130">Hola biblioteca administrada de Azure proporciona métodos para toocommunicate de instancias de rol en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="44c22-130">hello Azure Managed Library provides methods for role instances toocommunicate at runtime.</span></span> <span data-ttu-id="44c22-131">Desde código que se ejecuta dentro de una instancia de rol, puede recuperar información acerca de la existencia de Hola de otras instancias de rol y sus puntos de conexión, así como información acerca de la instancia de rol actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="44c22-131">From code running within a role instance, you can retrieve information about hello existence of other role instances and their endpoints, as well as information about hello current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="44c22-132">Solo puede recuperar información sobre las instancias de rol que se ejecuten en el servicio en la nube y que definan, al menos, un extremo interno.</span><span class="sxs-lookup"><span data-stu-id="44c22-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="44c22-133">Asimismo, no puede obtener datos sobre instancias de rol que se ejecuten en un servicio diferente.</span><span class="sxs-lookup"><span data-stu-id="44c22-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="44c22-134">Puede usar hello [instancias](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) instancias de tooretrieve las propiedades de un rol.</span><span class="sxs-lookup"><span data-stu-id="44c22-134">You can use hello [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property tooretrieve instances of a role.</span></span> <span data-ttu-id="44c22-135">En primer lugar utilice hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn un rol actual de toohello de referencia de instancia y, a continuación, usar hello [rol](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) tooreturn un rol de toohello de referencia de propiedad.</span><span class="sxs-lookup"><span data-stu-id="44c22-135">First use hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn a reference toohello current role instance, and then use hello [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property tooreturn a reference toohello role itself.</span></span>

<span data-ttu-id="44c22-136">Cuando se conecta tooa instancia de rol mediante programación a través de hello .NET SDK, es información de punto de conexión de hello tooaccess es relativamente fácil.</span><span class="sxs-lookup"><span data-stu-id="44c22-136">When you connect tooa role instance programmatically through hello .NET SDK, it's relatively easy tooaccess hello endpoint information.</span></span> <span data-ttu-id="44c22-137">Por ejemplo, después de que ya se ha conectado tooa entorno de rol específico, puede obtener el puerto Hola de un extremo concreto con este código:</span><span class="sxs-lookup"><span data-stu-id="44c22-137">For example, after you've already connected tooa specific role environment, you can get hello port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="44c22-138">Hola **instancias** propiedad devuelve una colección de **RoleInstance** objetos.</span><span class="sxs-lookup"><span data-stu-id="44c22-138">hello **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="44c22-139">Esta colección siempre contiene la instancia actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="44c22-139">This collection always contains hello current instance.</span></span> <span data-ttu-id="44c22-140">Si el rol de hello no define un extremo interno, colección de hello incluye instancia actual de hello, pero no otras instancias.</span><span class="sxs-lookup"><span data-stu-id="44c22-140">If hello role does not define an internal endpoint, hello collection includes hello current instance but no other instances.</span></span> <span data-ttu-id="44c22-141">número de Hola de instancias de rol de la colección de hello siempre será 1 en caso de hello donde no se define ningún extremo interno para el rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="44c22-141">hello number of role instances in hello collection will always be 1 in hello case where no internal endpoint is defined for hello role.</span></span> <span data-ttu-id="44c22-142">Si el rol de hello define un extremo interno, sus instancias son reconocibles en tiempo de ejecución y número de Hola de instancias en la colección de hello corresponderá toohello número de instancias especificadas para el rol de hello en el archivo de configuración de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="44c22-142">If hello role defines an internal endpoint, its instances are discoverable at runtime, and hello number of instances in hello collection will correspond toohello number of instances specified for hello role in hello service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="44c22-143">Hola biblioteca administrada de Azure no proporciona una manera de determinar el estado de Hola de otras instancias de rol, pero se pueden implementar estas evaluaciones de estado si el servicio necesita esta funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="44c22-143">hello Azure Managed Library does not provide a means of determining hello health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="44c22-144">Puede usar [diagnósticos de Azure](cloud-services-dotnet-diagnostics.md) tooobtain información sobre la ejecución de instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="44c22-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) tooobtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="44c22-145">número de puerto de hello toodetermine para un extremo interno en una instancia de rol, puede usar hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) tooreturn propiedad direcciones de un objeto de diccionario que contiene los nombres de extremo y su correspondiente IP y puertos.</span><span class="sxs-lookup"><span data-stu-id="44c22-145">toodetermine hello port number for an internal endpoint on a role instance, you can use hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property tooreturn a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="44c22-146">Hola [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) propiedad devuelve la dirección IP de Hola y el puerto para un extremo especificado.</span><span class="sxs-lookup"><span data-stu-id="44c22-146">hello [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns hello IP address and port for a specified endpoint.</span></span> <span data-ttu-id="44c22-147">Hola **PublicIPEndpoint** propiedad devuelve el puerto de Hola para un extremo con equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="44c22-147">hello **PublicIPEndpoint** property returns hello port for a load balanced endpoint.</span></span> <span data-ttu-id="44c22-148">parte de la dirección IP Hola de hello **PublicIPEndpoint** no se utiliza la propiedad.</span><span class="sxs-lookup"><span data-stu-id="44c22-148">hello IP address portion of hello **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="44c22-149">Aquí tiene un ejemplo que itera las instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="44c22-149">Here is an example that iterates role instances.</span></span>

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

<span data-ttu-id="44c22-150">Este es un ejemplo de un rol de trabajo que obtiene el punto de conexión de hello expuesto a través de la definición de servicio de Hola y comienza a escuchar las conexiones.</span><span class="sxs-lookup"><span data-stu-id="44c22-150">Here is an example of a worker role that gets hello endpoint exposed through hello service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="44c22-151">Este código solo funcionará en un servicio implementado.</span><span class="sxs-lookup"><span data-stu-id="44c22-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="44c22-152">Cuando se ejecuta en hello emulador de proceso de Azure, los elementos de configuración que crean los puntos de conexión directa de puerto de servicio (**InstanceInputEndpoint** elementos) se omiten.</span><span class="sxs-lookup"><span data-stu-id="44c22-152">When running in hello Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
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

        // Bind socket listener toointernal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block hello thread and wait for a client request
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
      // Set hello maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-toocontrol-role-communication"></a><span data-ttu-id="44c22-153">Comunicación entre roles de toocontrol de reglas de tráfico de red</span><span class="sxs-lookup"><span data-stu-id="44c22-153">Network traffic rules toocontrol role communication</span></span>
<span data-ttu-id="44c22-154">Después de definir extremos internos, puede agregar toocontrol de reglas (basadas en los extremos de Hola que ha creado) de tráfico de red cómo instancias de rol pueden comunicarse entre sí.</span><span class="sxs-lookup"><span data-stu-id="44c22-154">After you define internal endpoints, you can add network traffic rules (based on hello endpoints that you created) toocontrol how role instances can communicate with each other.</span></span> <span data-ttu-id="44c22-155">Hello diagrama siguiente muestra algunos escenarios comunes para controlar la comunicación entre roles:</span><span class="sxs-lookup"><span data-stu-id="44c22-155">hello following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="44c22-156">![Escenarios de reglas de tráfico de red](./media/cloud-services-enable-communication-role-instances/scenarios.png "Escenarios de reglas de tráfico de red")</span><span class="sxs-lookup"><span data-stu-id="44c22-156">![Network Traffic Rules Scenarios](./media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="44c22-157">Hello ejemplo de código siguiente muestra las definiciones de roles para los roles de Hola que se muestra en el diagrama anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="44c22-157">hello following code example shows role definitions for hello roles shown in hello previous diagram.</span></span> <span data-ttu-id="44c22-158">Cada definición de rol incluye, al menos, un extremo interno definido:</span><span class="sxs-lookup"><span data-stu-id="44c22-158">Each role definition includes at least one internal endpoint defined:</span></span>

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
> <span data-ttu-id="44c22-159">Es posible que los extremos internos de tanto puertos asignados fijos como automáticos tengan restricciones de comunicación entre roles.</span><span class="sxs-lookup"><span data-stu-id="44c22-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="44c22-160">De forma predeterminada, después de define un extremo interno, la comunicación puede iniciarse desde cualquier extremo interno de toohello de rol de un rol sin restricciones.</span><span class="sxs-lookup"><span data-stu-id="44c22-160">By default, after an internal endpoint is defined, communication can flow from any role toohello internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="44c22-161">comunicación de toorestrict, debe agregar una **NetworkTrafficRules** elemento toohello **ServiceDefinition** elemento en el archivo de definición de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="44c22-161">toorestrict communication, you must add a **NetworkTrafficRules** element toohello **ServiceDefinition** element in hello service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="44c22-162">Escenario 1.</span><span class="sxs-lookup"><span data-stu-id="44c22-162">Scenario 1</span></span>
<span data-ttu-id="44c22-163">Sólo permitir el tráfico de red desde **WebRole1** demasiado**WorkerRole1**.</span><span class="sxs-lookup"><span data-stu-id="44c22-163">Only allow network traffic from **WebRole1** too**WorkerRole1**.</span></span>

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

### <a name="scenario-2"></a><span data-ttu-id="44c22-164">Escenario 2.</span><span class="sxs-lookup"><span data-stu-id="44c22-164">Scenario 2</span></span>
<span data-ttu-id="44c22-165">Solo permite el tráfico de red de **WebRole1** demasiado**WorkerRole1** y **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="44c22-165">Only allows network traffic from **WebRole1** too**WorkerRole1** and **WorkerRole2**.</span></span>

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

### <a name="scenario-3"></a><span data-ttu-id="44c22-166">Escenario 3.</span><span class="sxs-lookup"><span data-stu-id="44c22-166">Scenario 3</span></span>
<span data-ttu-id="44c22-167">Solo permite el tráfico de red de **WebRole1** demasiado**WorkerRole1**, y **WorkerRole1** demasiado**WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="44c22-167">Only allows network traffic from **WebRole1** too**WorkerRole1**, and **WorkerRole1** too**WorkerRole2**.</span></span>

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

### <a name="scenario-4"></a><span data-ttu-id="44c22-168">Escenario 4.</span><span class="sxs-lookup"><span data-stu-id="44c22-168">Scenario 4</span></span>
<span data-ttu-id="44c22-169">Solo permite el tráfico de red de **WebRole1** demasiado**WorkerRole1**, **WebRole1** demasiado**WorkerRole2**, y  **WorkerRole1** demasiado**WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="44c22-169">Only allows network traffic from **WebRole1** too**WorkerRole1**, **WebRole1** too**WorkerRole2**, and **WorkerRole1** too**WorkerRole2**.</span></span>

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

<span data-ttu-id="44c22-170">Puede encontrar una referencia de esquema XML para los elementos de hello usado anteriormente [aquí](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span><span class="sxs-lookup"><span data-stu-id="44c22-170">An XML schema reference for hello elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="44c22-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="44c22-171">Next steps</span></span>
<span data-ttu-id="44c22-172">Más información sobre Hola servicio en la nube [modelo](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="44c22-172">Read more about hello Cloud Service [model](cloud-services-model-and-package.md).</span></span>

