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
# <a name="enable-communication-for-role-instances-in-azure"></a>Habilitar la comunicación para instancias de rol en Azure
Los roles de servicio en la nube se comunican a través de conexiones internas y externas. Las conexiones externas se denominan **puntos de conexión de entrada** mientras que conexiones internas se denominan **puntos de conexión internos**. Este tema se describe cómo hello toomodify [definición del servicio](cloud-services-model-and-package.md#csdef) toocreate extremos.

## <a name="input-endpoint"></a>Extremo de entrada
extremo de entrada de Hola se utiliza cuando se desea tooexpose un toohello puerto fuera. Especifique el tipo de protocolo de Hola y el puerto de hello del extremo de Hola que, a continuación, se aplica a ambos puertos externos e internos de hello para el punto de conexión de Hola. Si lo desea, puede especificar un puerto interno diferente para el punto de conexión de hello con hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) atributo.

extremo de entrada de Hello sirve Hola siguientes protocolos: **http, https, tcp y udp**.

toocreate un extremo de entrada, agregar hello **InputEndpoint** toohello de elemento secundarios **extremos** elemento de rol web o de trabajo.

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a>Extremo de entrada de instancia
Los extremos de entrada de instancia son los puntos de conexión de tooinput similar pero permite asignar puertos orientados al público específicos para cada instancia de rol individuales mediante el reenvío de puerto de equilibrador de carga de Hola. Puede especificar un único puerto público o un intervalo de puertos.

solo puede usar el extremo de entrada de instancia de Hello **tcp** o **udp** como protocolo de Hola.

toocreate un extremo de entrada de instancia, agregue hello **InstanceInputEndpoint** toohello de elemento secundarios **extremos** elemento de rol web o de trabajo.

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a>Extremo interno
Los extremos internos están disponibles para la comunicación entre instancias. puerto de Hello es opcional y si se omite, un puerto dinámico se asigna el punto de conexión de toohello. Además, puede usar un intervalo de puertos. Recuerde que hay un límite de cinco extremos internos por rol.

extremo interno de Hello sirve Hola siguientes protocolos: **http, tcp, udp, cualquier**.

toocreate un extremo de entrada interno, agregue hello **InternalEndpoint** toohello de elemento secundarios **extremos** elemento de rol web o de trabajo.

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

También puede usar un intervalo de puertos.

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a>Roles de trabajo en comparación con los Roles web
Hay una pequeña diferencia entre los extremos cuando se trabaja con roles web y de trabajo. Hello rol web debe tener como mínimo un solo extremo de entrada con hello **HTTP** protocolo.

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after hello first InputEndPoint -->
</Endpoints>
```

## <a name="using-hello-net-sdk-tooaccess-an-endpoint"></a>Uso de hello .NET SDK tooaccess un punto de conexión
Hola biblioteca administrada de Azure proporciona métodos para toocommunicate de instancias de rol en tiempo de ejecución. Desde código que se ejecuta dentro de una instancia de rol, puede recuperar información acerca de la existencia de Hola de otras instancias de rol y sus puntos de conexión, así como información acerca de la instancia de rol actual de Hola.

> [!NOTE]
> Solo puede recuperar información sobre las instancias de rol que se ejecuten en el servicio en la nube y que definan, al menos, un extremo interno. Asimismo, no puede obtener datos sobre instancias de rol que se ejecuten en un servicio diferente.
> 
> 

Puede usar hello [instancias](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) instancias de tooretrieve las propiedades de un rol. En primer lugar utilice hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn un rol actual de toohello de referencia de instancia y, a continuación, usar hello [rol](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) tooreturn un rol de toohello de referencia de propiedad.

Cuando se conecta tooa instancia de rol mediante programación a través de hello .NET SDK, es información de punto de conexión de hello tooaccess es relativamente fácil. Por ejemplo, después de que ya se ha conectado tooa entorno de rol específico, puede obtener el puerto Hola de un extremo concreto con este código:

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

Hola **instancias** propiedad devuelve una colección de **RoleInstance** objetos. Esta colección siempre contiene la instancia actual de Hola. Si el rol de hello no define un extremo interno, colección de hello incluye instancia actual de hello, pero no otras instancias. número de Hola de instancias de rol de la colección de hello siempre será 1 en caso de hello donde no se define ningún extremo interno para el rol de Hola. Si el rol de hello define un extremo interno, sus instancias son reconocibles en tiempo de ejecución y número de Hola de instancias en la colección de hello corresponderá toohello número de instancias especificadas para el rol de hello en el archivo de configuración de servicio de Hola.

> [!NOTE]
> Hola biblioteca administrada de Azure no proporciona una manera de determinar el estado de Hola de otras instancias de rol, pero se pueden implementar estas evaluaciones de estado si el servicio necesita esta funcionalidad. Puede usar [diagnósticos de Azure](cloud-services-dotnet-diagnostics.md) tooobtain información sobre la ejecución de instancias de rol.
> 
> 

número de puerto de hello toodetermine para un extremo interno en una instancia de rol, puede usar hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) tooreturn propiedad direcciones de un objeto de diccionario que contiene los nombres de extremo y su correspondiente IP y puertos. Hola [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) propiedad devuelve la dirección IP de Hola y el puerto para un extremo especificado. Hola **PublicIPEndpoint** propiedad devuelve el puerto de Hola para un extremo con equilibrio de carga. parte de la dirección IP Hola de hello **PublicIPEndpoint** no se utiliza la propiedad.

Aquí tiene un ejemplo que itera las instancias de rol.

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

Este es un ejemplo de un rol de trabajo que obtiene el punto de conexión de hello expuesto a través de la definición de servicio de Hola y comienza a escuchar las conexiones.

> [!WARNING]
> Este código solo funcionará en un servicio implementado. Cuando se ejecuta en hello emulador de proceso de Azure, los elementos de configuración que crean los puntos de conexión directa de puerto de servicio (**InstanceInputEndpoint** elementos) se omiten.
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

## <a name="network-traffic-rules-toocontrol-role-communication"></a>Comunicación entre roles de toocontrol de reglas de tráfico de red
Después de definir extremos internos, puede agregar toocontrol de reglas (basadas en los extremos de Hola que ha creado) de tráfico de red cómo instancias de rol pueden comunicarse entre sí. Hello diagrama siguiente muestra algunos escenarios comunes para controlar la comunicación entre roles:

![Escenarios de reglas de tráfico de red](./media/cloud-services-enable-communication-role-instances/scenarios.png "Escenarios de reglas de tráfico de red")

Hello ejemplo de código siguiente muestra las definiciones de roles para los roles de Hola que se muestra en el diagrama anterior Hola. Cada definición de rol incluye, al menos, un extremo interno definido:

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
> Es posible que los extremos internos de tanto puertos asignados fijos como automáticos tengan restricciones de comunicación entre roles.
> 
> 

De forma predeterminada, después de define un extremo interno, la comunicación puede iniciarse desde cualquier extremo interno de toohello de rol de un rol sin restricciones. comunicación de toorestrict, debe agregar una **NetworkTrafficRules** elemento toohello **ServiceDefinition** elemento en el archivo de definición de servicio de Hola.

### <a name="scenario-1"></a>Escenario 1.
Sólo permitir el tráfico de red desde **WebRole1** demasiado**WorkerRole1**.

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

### <a name="scenario-2"></a>Escenario 2.
Solo permite el tráfico de red de **WebRole1** demasiado**WorkerRole1** y **WorkerRole2**.

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

### <a name="scenario-3"></a>Escenario 3.
Solo permite el tráfico de red de **WebRole1** demasiado**WorkerRole1**, y **WorkerRole1** demasiado**WorkerRole2**.

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

### <a name="scenario-4"></a>Escenario 4.
Solo permite el tráfico de red de **WebRole1** demasiado**WorkerRole1**, **WebRole1** demasiado**WorkerRole2**, y  **WorkerRole1** demasiado**WorkerRole2**.

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

Puede encontrar una referencia de esquema XML para los elementos de hello usado anteriormente [aquí](https://msdn.microsoft.com/library/azure/gg557551.aspx).

## <a name="next-steps"></a>Pasos siguientes
Más información sobre Hola servicio en la nube [modelo](cloud-services-model-and-package.md).

