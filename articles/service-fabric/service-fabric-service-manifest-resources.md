---
title: los extremos de servicio de Service Fabric aaaSpecifying | Documentos de Microsoft
description: "Cómo manifiesto toodescribe recursos de punto de conexión en un servicio, incluida la forma tooset extremos HTTPS"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: da36cbdb-6531-4dae-88e8-a311ab71520d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: subramar
ms.openlocfilehash: a4ebee353ce5cf86583673674246094f03f368be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="specify-resources-in-a-service-manifest"></a><span data-ttu-id="a393a-103">Especificación de los recursos en un manifiesto de servicio</span><span class="sxs-lookup"><span data-stu-id="a393a-103">Specify resources in a service manifest</span></span>
## <a name="overview"></a><span data-ttu-id="a393a-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a393a-104">Overview</span></span>
<span data-ttu-id="a393a-105">manifiesto del servicio Hola permite que los recursos utilizados por hello servicio toobe declarado o modificar sin cambiar el código de hello compilado.</span><span class="sxs-lookup"><span data-stu-id="a393a-105">hello service manifest allows resources that are used by hello service toobe declared/changed without changing hello compiled code.</span></span> <span data-ttu-id="a393a-106">Azure Service Fabric es compatible con la configuración de recursos de punto de conexión para servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="a393a-106">Azure Service Fabric supports configuration of endpoint resources for hello service.</span></span> <span data-ttu-id="a393a-107">Hola acceder a toohello los recursos que se especifican en el manifiesto del servicio Hola puede controlarse a través de hello SecurityGroup Hola manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="a393a-107">hello access toohello resources that are specified in hello service manifest can be controlled via hello SecurityGroup in hello application manifest.</span></span> <span data-ttu-id="a393a-108">declaración de Hola de recursos permite que estas toobe recursos cambió durante la implementación, lo que significa que el servicio de hello no necesita toointroduce un nuevo mecanismo de configuración.</span><span class="sxs-lookup"><span data-stu-id="a393a-108">hello declaration of resources allows these resources toobe changed at deployment time, meaning hello service doesn't need toointroduce a new configuration mechanism.</span></span> <span data-ttu-id="a393a-109">se instala con hello SDK del servicio de Fabric Hello definición de esquema de archivo de ServiceManifest.xml hello y herramientas demasiado*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="a393a-109">hello schema definition for hello ServiceManifest.xml file is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

## <a name="endpoints"></a><span data-ttu-id="a393a-110">Puntos de conexión</span><span class="sxs-lookup"><span data-stu-id="a393a-110">Endpoints</span></span>
<span data-ttu-id="a393a-111">Cuando un recurso de extremo se define en el manifiesto del servicio de hello, Service Fabric asigna puertos de intervalo de puertos de aplicación Hola reservado cuando un puerto no se especifica explícitamente.</span><span class="sxs-lookup"><span data-stu-id="a393a-111">When an endpoint resource is defined in hello service manifest, Service Fabric assigns ports from hello reserved application port range when a port isn't specified explicitly.</span></span> <span data-ttu-id="a393a-112">Por ejemplo, buscar en el punto de conexión de hello *ServiceEndpoint1* especificado en el fragmento de manifiesto de hello proporcionado después de este párrafo.</span><span class="sxs-lookup"><span data-stu-id="a393a-112">For example, look at hello endpoint *ServiceEndpoint1* specified in hello manifest snippet provided after this paragraph.</span></span> <span data-ttu-id="a393a-113">Además, los servicios también pueden solicitar un puerto específico en un recurso.</span><span class="sxs-lookup"><span data-stu-id="a393a-113">Additionally, services can also request a specific port in a resource.</span></span> <span data-ttu-id="a393a-114">Réplicas de servicio que se ejecutan en nodos de clúster diferente se pueden asignar a números de puerto diferente, mientras que las réplicas de un servicio que se ejecuta en Hola mismo puerto de Hola de recurso compartido de nodo.</span><span class="sxs-lookup"><span data-stu-id="a393a-114">Service replicas running on different cluster nodes can be assigned different port numbers, while replicas of a service running on hello same node share hello port.</span></span> <span data-ttu-id="a393a-115">réplicas de servicio de Hello, a continuación, pueden usar estos puertos según sea necesario para la replicación y la escucha de solicitudes de cliente.</span><span class="sxs-lookup"><span data-stu-id="a393a-115">hello service replicas can then use these ports as needed for replication and listening for client requests.</span></span>

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="a393a-116">Consulte demasiado[configurar servicios de confianza con estado](service-fabric-reliable-services-configuration.md) tooread más acerca de cómo hacer referencia a los puntos de conexión del archivo de configuración de paquete de configuración de hello (settings.xml).</span><span class="sxs-lookup"><span data-stu-id="a393a-116">Refer too[Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md) tooread more about referencing endpoints from hello config package settings file (settings.xml).</span></span>

## <a name="example-specifying-an-http-endpoint-for-your-service"></a><span data-ttu-id="a393a-117">Ejemplo: Especificación de un punto de conexión HTTP para el servicio</span><span class="sxs-lookup"><span data-stu-id="a393a-117">Example: specifying an HTTP endpoint for your service</span></span>
<span data-ttu-id="a393a-118">Hello siguiente manifiesto de servicio define un recurso de punto de conexión TCP y los dos recursos de extremo HTTP de hello &lt;recursos&gt; elemento.</span><span class="sxs-lookup"><span data-stu-id="a393a-118">hello following service manifest defines one TCP endpoint resource and two HTTP endpoint resources in hello &lt;Resources&gt; element.</span></span>

<span data-ttu-id="a393a-119">Service Fabric hace ACL automáticamente en los puntos de conexión HTTP.</span><span class="sxs-lookup"><span data-stu-id="a393a-119">HTTP endpoints are automatically ACL'd by Service Fabric.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Stateful1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         This name must match hello string used in hello RegisterServiceType call in Program.cs. -->
    <StatefulServiceType ServiceTypeName="Stateful1Type" HasPersistedState="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <ExeHost>
        <Program>Stateful1.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port number on which to
           listen. Note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
      <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
      <Endpoint Name="ServiceEndpoint3" Protocol="https"/>

      <!-- This endpoint is used by hello replicator for replicating hello state of your service.
           This endpoint is configured through hello ReplicatorSettings config section in hello Settings.xml
           file under hello ConfigPackage. -->
      <Endpoint Name="ReplicatorEndpoint" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

## <a name="example-specifying-an-https-endpoint-for-your-service"></a><span data-ttu-id="a393a-120">Ejemplo: Especificación de un punto de conexión HTTPS para el servicio</span><span class="sxs-lookup"><span data-stu-id="a393a-120">Example: specifying an HTTPS endpoint for your service</span></span>
<span data-ttu-id="a393a-121">Hola protocolo HTTPS proporciona autenticación del servidor y también se utiliza para cifrar la comunicación entre cliente y servidor.</span><span class="sxs-lookup"><span data-stu-id="a393a-121">hello HTTPS protocol provides server authentication and is also used for encrypting client-server communication.</span></span> <span data-ttu-id="a393a-122">tooenable HTTPS en el servicio de Service Fabric, especificar el protocolo de Hola Hola *recursos -> extremos -> extremo* sección Hola del manifiesto de servicios, como se muestra anteriormente para el punto de conexión de hello *ServiceEndpoint3* .</span><span class="sxs-lookup"><span data-stu-id="a393a-122">tooenable HTTPS on your Service Fabric service, specify hello protocol in hello *Resources -> Endpoints -> Endpoint* section of hello service manifest, as shown earlier for hello endpoint *ServiceEndpoint3*.</span></span>

> [!NOTE]
> <span data-ttu-id="a393a-123">No se puede cambiar el protocolo de un servicio durante la actualización de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a393a-123">A service’s protocol cannot be changed during application upgrade.</span></span> <span data-ttu-id="a393a-124">Si se modifica en el transcurso, se tratará de un cambio brusco.</span><span class="sxs-lookup"><span data-stu-id="a393a-124">If it is changed during upgrade, it is a breaking change.</span></span>
> 
> 

<span data-ttu-id="a393a-125">Este es un ejemplo ApplicationManifest necesita tooset para HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a393a-125">Here is an example ApplicationManifest that you need tooset for HTTPS.</span></span> <span data-ttu-id="a393a-126">se debe proporcionar la huella digital de Hello para el certificado.</span><span class="sxs-lookup"><span data-stu-id="a393a-126">hello thumbprint for your certificate must be provided.</span></span> <span data-ttu-id="a393a-127">Hola EndpointRef es una referencia tooEndpointResource en ServiceManifest, para el que establece el protocolo HTTPS de Hola.</span><span class="sxs-lookup"><span data-stu-id="a393a-127">hello EndpointRef is a reference tooEndpointResource in ServiceManifest, for which you set hello HTTPS protocol.</span></span> <span data-ttu-id="a393a-128">Puede agregar más de un certificado EndpointCertificate.</span><span class="sxs-lookup"><span data-stu-id="a393a-128">You can add more than one EndpointCertificate.</span></span>  

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="Application1Type"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
    <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
    <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint3"/>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types when an instance of this
         application type is created. You can also create one or more instances of service type by using the
         Service Fabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Stateful1">
      <StatefulService ServiceTypeName="Stateful1Type" TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]" MinReplicaSetSize="[Stateful1_ ]">
        <UniformInt64Partition PartitionCount="[Stateful1_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
      </StatefulService>
    </Service>
  </DefaultServices>
  <Certificates>
    <EndpointCertificate Name="TestCert1" X509FindValue="FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF F0" X509StoreName="MY" />  
  </Certificates>
</ApplicationManifest>
```

## <a name="overriding-endpoints-in-servicemanifestxml"></a><span data-ttu-id="a393a-129">Invalidación de Endpoints en ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="a393a-129">Overriding Endpoints in ServiceManifest.xml</span></span>

<span data-ttu-id="a393a-130">Hola ApplicationManifest agregue una sección de ResourceOverrides que será una sección de tooConfigOverrides relacionado.</span><span class="sxs-lookup"><span data-stu-id="a393a-130">In hello ApplicationManifest add a ResourceOverrides section which will be a sibling tooConfigOverrides section.</span></span> <span data-ttu-id="a393a-131">En esta sección puede especificar la invalidación de hello para la sección de puntos de conexión de hello en la sección de recursos de hello especificada en el manifiesto del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="a393a-131">In this section you can specify hello override for hello Endpoints section in hello resources section specified in hello Service manifest.</span></span>

<span data-ttu-id="a393a-132">En orden toooverride extremo en ServiceManifest con cambio ApplicationParameters Hola ApplicationManifest como sigue:</span><span class="sxs-lookup"><span data-stu-id="a393a-132">In order toooverride EndPoint in ServiceManifest using ApplicationParameters change hello ApplicationManifest as following:</span></span>

<span data-ttu-id="a393a-133">Hola ServiceManifestImport sección Agregar una nueva sección "ResourceOverrides"</span><span class="sxs-lookup"><span data-stu-id="a393a-133">In hello ServiceManifestImport section add a new section "ResourceOverrides"</span></span>

```xml
<ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <ResourceOverrides>
      <Endpoints>
        <Endpoint Name="ServiceEndpoint" Port="[Port]" Protocol="[Protocol]" Type="[Type]" />
        <Endpoint Name="ServiceEndpoint1" Port="[Port1]" Protocol="[Protocol1] "/>
      </Endpoints>
    </ResourceOverrides>
        <Policies>
           <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint"/>
        </Policies>
  </ServiceManifestImport>
```

<span data-ttu-id="a393a-134">Hola que agregar parámetros a continuación:</span><span class="sxs-lookup"><span data-stu-id="a393a-134">In hello Parameters add below:</span></span>

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

<span data-ttu-id="a393a-135">Al implementar la aplicación hello ahora puede pasar estos valores como ApplicationParameters por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a393a-135">While deploying hello application now you can pass in these values as ApplicationParameters for example:</span></span>

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

<span data-ttu-id="a393a-136">Nota: Si los valores de hello proporcionan para hello ApplicationParameters está vacía, volvamos toohello predeterminado valor proporcionado en hello ServiceManifest para hello correspondiente EndPointName.</span><span class="sxs-lookup"><span data-stu-id="a393a-136">Note: If hello values provide for hello ApplicationParameters is empty we go back toohello default value provided in hello ServiceManifest for hello corresponding EndPointName.</span></span>

<span data-ttu-id="a393a-137">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a393a-137">For example:</span></span>

<span data-ttu-id="a393a-138">Si está en hello ServiceManifest especificado</span><span class="sxs-lookup"><span data-stu-id="a393a-138">If in hello ServiceManifest you specified</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

<span data-ttu-id="a393a-139">Hola Port1 y valor de Protocol1 de parámetros de la aplicación es nulo o está vacío.</span><span class="sxs-lookup"><span data-stu-id="a393a-139">And hello Port1 and Protocol1 value for Application parameters is null or empty.</span></span> <span data-ttu-id="a393a-140">puerto de Hello todavía se decide por ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="a393a-140">hello port is still decided by ServiceFabric.</span></span> <span data-ttu-id="a393a-141">Y Hola protocolo tcp.</span><span class="sxs-lookup"><span data-stu-id="a393a-141">And hello Protocol will tcp.</span></span>

<span data-ttu-id="a393a-142">Imagine que especifica un valor incorrecto.</span><span class="sxs-lookup"><span data-stu-id="a393a-142">Suppose you specify a wrong value.</span></span> <span data-ttu-id="a393a-143">Supongamos que para el puerto ha especificado un valor de cadena "Foo" en lugar de un valor entero.  Nueva ServiceFabricApplication comando producirá un error: parámetro de invalidación de hello con el atributo de nombre 'ServiceEndpoint1' "Port1" en la sección 'ResourceOverrides' no es válido.</span><span class="sxs-lookup"><span data-stu-id="a393a-143">Like for Port you specified a string value "Foo" instead of an int.  New-ServiceFabricApplication command will fail with an error : hello override parameter with name 'ServiceEndpoint1' attribute 'Port1' in section 'ResourceOverrides' is invalid.</span></span> <span data-ttu-id="a393a-144">valor de Hello especificado es "Foo" y necesario es 'int'.</span><span class="sxs-lookup"><span data-stu-id="a393a-144">hello value specified is 'Foo' and required is 'int'.</span></span>
