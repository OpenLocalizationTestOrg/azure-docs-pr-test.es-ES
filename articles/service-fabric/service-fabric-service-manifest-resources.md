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
# <a name="specify-resources-in-a-service-manifest"></a>Especificación de los recursos en un manifiesto de servicio
## <a name="overview"></a>Información general
manifiesto del servicio Hola permite que los recursos utilizados por hello servicio toobe declarado o modificar sin cambiar el código de hello compilado. Azure Service Fabric es compatible con la configuración de recursos de punto de conexión para servicio de Hola. Hola acceder a toohello los recursos que se especifican en el manifiesto del servicio Hola puede controlarse a través de hello SecurityGroup Hola manifiesto de aplicación. declaración de Hola de recursos permite que estas toobe recursos cambió durante la implementación, lo que significa que el servicio de hello no necesita toointroduce un nuevo mecanismo de configuración. se instala con hello SDK del servicio de Fabric Hello definición de esquema de archivo de ServiceManifest.xml hello y herramientas demasiado*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

## <a name="endpoints"></a>Puntos de conexión
Cuando un recurso de extremo se define en el manifiesto del servicio de hello, Service Fabric asigna puertos de intervalo de puertos de aplicación Hola reservado cuando un puerto no se especifica explícitamente. Por ejemplo, buscar en el punto de conexión de hello *ServiceEndpoint1* especificado en el fragmento de manifiesto de hello proporcionado después de este párrafo. Además, los servicios también pueden solicitar un puerto específico en un recurso. Réplicas de servicio que se ejecutan en nodos de clúster diferente se pueden asignar a números de puerto diferente, mientras que las réplicas de un servicio que se ejecuta en Hola mismo puerto de Hola de recurso compartido de nodo. réplicas de servicio de Hello, a continuación, pueden usar estos puertos según sea necesario para la replicación y la escucha de solicitudes de cliente.

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

Consulte demasiado[configurar servicios de confianza con estado](service-fabric-reliable-services-configuration.md) tooread más acerca de cómo hacer referencia a los puntos de conexión del archivo de configuración de paquete de configuración de hello (settings.xml).

## <a name="example-specifying-an-http-endpoint-for-your-service"></a>Ejemplo: Especificación de un punto de conexión HTTP para el servicio
Hello siguiente manifiesto de servicio define un recurso de punto de conexión TCP y los dos recursos de extremo HTTP de hello &lt;recursos&gt; elemento.

Service Fabric hace ACL automáticamente en los puntos de conexión HTTP.

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

## <a name="example-specifying-an-https-endpoint-for-your-service"></a>Ejemplo: Especificación de un punto de conexión HTTPS para el servicio
Hola protocolo HTTPS proporciona autenticación del servidor y también se utiliza para cifrar la comunicación entre cliente y servidor. tooenable HTTPS en el servicio de Service Fabric, especificar el protocolo de Hola Hola *recursos -> extremos -> extremo* sección Hola del manifiesto de servicios, como se muestra anteriormente para el punto de conexión de hello *ServiceEndpoint3* .

> [!NOTE]
> No se puede cambiar el protocolo de un servicio durante la actualización de la aplicación. Si se modifica en el transcurso, se tratará de un cambio brusco.
> 
> 

Este es un ejemplo ApplicationManifest necesita tooset para HTTPS. se debe proporcionar la huella digital de Hello para el certificado. Hola EndpointRef es una referencia tooEndpointResource en ServiceManifest, para el que establece el protocolo HTTPS de Hola. Puede agregar más de un certificado EndpointCertificate.  

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

## <a name="overriding-endpoints-in-servicemanifestxml"></a>Invalidación de Endpoints en ServiceManifest.xml

Hola ApplicationManifest agregue una sección de ResourceOverrides que será una sección de tooConfigOverrides relacionado. En esta sección puede especificar la invalidación de hello para la sección de puntos de conexión de hello en la sección de recursos de hello especificada en el manifiesto del servicio de Hola.

En orden toooverride extremo en ServiceManifest con cambio ApplicationParameters Hola ApplicationManifest como sigue:

Hola ServiceManifestImport sección Agregar una nueva sección "ResourceOverrides"

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

Hola que agregar parámetros a continuación:

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

Al implementar la aplicación hello ahora puede pasar estos valores como ApplicationParameters por ejemplo:

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

Nota: Si los valores de hello proporcionan para hello ApplicationParameters está vacía, volvamos toohello predeterminado valor proporcionado en hello ServiceManifest para hello correspondiente EndPointName.

Por ejemplo:

Si está en hello ServiceManifest especificado

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

Hola Port1 y valor de Protocol1 de parámetros de la aplicación es nulo o está vacío. puerto de Hello todavía se decide por ServiceFabric. Y Hola protocolo tcp.

Imagine que especifica un valor incorrecto. Supongamos que para el puerto ha especificado un valor de cadena "Foo" en lugar de un valor entero.  Nueva ServiceFabricApplication comando producirá un error: parámetro de invalidación de hello con el atributo de nombre 'ServiceEndpoint1' "Port1" en la sección 'ResourceOverrides' no es válido. valor de Hello especificado es "Foo" y necesario es 'int'.
