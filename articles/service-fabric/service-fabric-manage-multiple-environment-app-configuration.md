---
title: aaaManage varios entornos de Service Fabric | Documentos de Microsoft
description: "Aplicaciones de Service Fabric se pueden ejecutar en clústeres que varían en tamaño desde una toothousands de máquina de máquinas. En algunos casos, le interesará tooconfigure la aplicación de forma diferente para los distintos entornos. Este artículo se trata cómo toodefine parámetros de aplicación diferente por cada entorno."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: mikkelhegn
ms.openlocfilehash: 2b3327e0e1a3bbd35a50835e720619f308b1b501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a>Administración de los parámetros de la aplicación en varios entornos
Puede crear clústeres de Azure Service Fabric mediante en cualquier parte de una toomany miles de máquinas. Aunque los archivos binarios de aplicación pueden ejecutar sin modificaciones a través de este amplio espectro de entornos, a menudo desea tooconfigure Hola aplicación de manera diferente, según número Hola de máquinas que vaya a implementar.

A modo de ejemplo simple, considere `InstanceCount` en un servicio sin estado. Cuando se ejecutan las aplicaciones en Azure, se suele preferir tooset este valor especiales del parámetro toohello "-1". Esta configuración garantiza que el servicio se ejecuta en cada nodo de clúster de hello (o todos los nodos de tipo de nodo de hello si ha configurado una restricción de selección de ubicación). Sin embargo, esta configuración no es adecuada para un clúster único equipo ya que no puede tener varios procesos escuchando en hello mismo punto de conexión en un único equipo. En su lugar, normalmente establece `InstanceCount` demasiado "1".

## <a name="specifying-environment-specific-parameters"></a>Especificación de parámetros concretos del entorno
problema de configuración de Hello solución toothis es un conjunto de servicios predeterminados con parámetros y los archivos de parámetros de aplicación que rellenan los valores de parámetro para un entorno determinado. Servicios predeterminados y los parámetros de la aplicación están configurados en la aplicación hello y manifiestos de servicio. se instala con hello SDK del servicio de Fabric Hello definición de esquema para archivos de ServiceManifest.xml y ApplicationManifest.xml de Hola y herramientas demasiado*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

### <a name="default-services"></a>Servicios predeterminados
Las aplicaciones de Service Fabric constan de una colección de instancias de servicio. Aunque es posible que toocreate una aplicación vacía y, a continuación, crear todas las instancias de servicio de forma dinámica, la mayoría de las aplicaciones tiene un conjunto de servicios básicos que siempre se debe crear cuando se crea una instancia de aplicación hello. Se trata de tooas que se hace referencia "servicios predeterminados". Cuando se especifican en el manifiesto de aplicación Hola, con marcadores de posición para la configuración de cada entorno incluido entre corchetes:

```xml
  <DefaultServices>
      <Service Name="Stateful1">
          <StatefulService
              ServiceTypeName="Stateful1Type"
              TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
              MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

              <UniformInt64Partition
                  PartitionCount="[Stateful1_PartitionCount]"
                  LowKey="-9223372036854775808"
                  HighKey="9223372036854775807"
              />
        </StatefulService>
    </Service>
  </DefaultServices>
```

Cada uno de los parámetros con nombre de hello debe definirse dentro de elemento de parámetros de Hola Hola del manifiesto de aplicación:

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

DefaultValue (atributo) Hola especifica Hola valor toobe utilizado en ausencia de Hola de un parámetro más específica para un entorno determinado.

> [!NOTE]
> No todos los parámetros de instancias de servicio son adecuados para la configuración de cada entorno. En el ejemplo de Hola anterior, Hola LowKey y valores HighKey esquema de partición del servicio de Hola se definen explícitamente para todas las instancias del servicio de hello puesto que el intervalo de partición de hello es una función de dominio de datos de hello, no el entorno de Hola.
> 
> 

### <a name="per-environment-service-configuration-settings"></a>Opciones de configuración del servicio de cada entorno
Hola [modelo de aplicaciones de Service Fabric](service-fabric-application-model.md) permite tooinclude paquetes de configuración que contienen pares clave-valor personalizados que son legibles en tiempo de ejecución de servicios. valores de Hello de estas opciones también se pueden diferenciar entorno especificando un `ConfigOverride` en el manifiesto de aplicación Hola.

Suponga que tiene Hola después de la configuración en hello Config\Settings.xml archivo para hello `Stateful1` servicio:

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
toooverride este valor para un par de entorno o aplicación específica, cree un `ConfigOverride` al importar Hola manifiesto del servicio en el manifiesto de aplicación Hola.

```xml
  <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
Este parámetro se puede configurar después por entorno, tal como se mostró anteriormente. Para ello, debe declarar en la sección de parámetros de Hola Hola del manifiesto de aplicación y especificando valores específicos del entorno en los archivos de parámetros de aplicación Hola.

> [!NOTE]
> En caso de hello de valores de configuración de servicio, hay tres lugares donde se puede establecer el valor de Hola de una clave: paquete de configuración de servicio de hello, el manifiesto de aplicación de Hola y el archivo de parámetros de aplicación Hola. Service Fabric se siempre elija Hola parámetro archivo de aplicación en primer lugar (si se especifica), a continuación, Hola manifiesto de aplicación y finalmente Hola paquete de configuración de.
> 
> 

### <a name="setting-and-using-environment-variables"></a>Establecimiento y uso de variables de entorno 
Puede especificar y establecer variables de entorno en el archivo de ServiceManifest.xml de hello y, a continuación, invalidar estas opciones en el archivo ApplicationManifest.xml de hello en por instancia.
ejemplo de Hola siguiente muestra dos variables de entorno, uno con un valor establecido y se reemplaza de hello otro. Puede utilizar valores de variables de entorno tooset Hola misma forma que estos se utilizan para las invalidaciones de configuración de parámetros de aplicación.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```
las variables de entorno de toooverride Hola Hola ApplicationManifest.xml, paquete de código de referencia Hola Hola ServiceManifest con hello `EnvironmentOverrides` elemento.

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 Una vez que se crea con el nombre de instancia del servicio de Hola puede tener acceso a las variables de entorno de Hola desde el código. Por ejemplo, en C# puede hacer siguiente Hola

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a>Variables de entorno de Service Fabric
Service Fabric tiene variables de entorno integradas que se establecen para cada instancia del servicio. Hello lista completa de variables de entorno se a continuación, donde hello los en negrita son Hola que va a utilizar en su servicio, Hola otro es utilizado por el tiempo de ejecución de Service Fabric. 

* Fabric_ApplicationHostId
* Fabric_ApplicationHostType
* Fabric_ApplicationId
* **Fabric_ApplicationName**
* Fabric_CodePackageInstanceId
* **Fabric_CodePackageName**
* **Fabric_Endpoint_[SuNombreDeServicio]TypeEndpoint**
* **Fabric_Folder_App_Log**
* **Fabric_Folder_App_Temp**
* **Fabric_Folder_App_Work**
* **Fabric_Folder_Application**
* Fabric_NodeId
* **Fabric_NodeIPOrFQDN**
* **Fabric_NodeName**
* Fabric_RuntimeConnectionAddress
* Fabric_ServicePackageInstanceId
* Fabric_ServicePackageName
* Fabric_ServicePackageVersionInstance
* FabricPackageFileName

Hola belows de código muestra cómo toolist Hola variables de entorno de Service Fabric
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
Hello siguientes son ejemplos de variables de entorno para un tipo de aplicación denominado `GuestExe.Application` con un tipo de servicio llamado `FrontEndService` cuando se ejecuta en el equipo de desarrollo local.

* **Fabric_ApplicationName = fabric:/GuestExe.Application**
* **Fabric_CodePackageName = Code**
* **Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**
* **Fabric_NodeIPOrFQDN = localhost**
* **Fabric_NodeName = _Node_2**

### <a name="application-parameter-files"></a>Archivos de parámetros de la aplicación
proyecto de aplicación de Service Fabric Hola puede incluir uno o varios archivos de parámetro de la aplicación. Cada uno de ellos define valores específicos de Hola para los parámetros de Hola que se definen en el manifiesto de aplicación Hola:

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="3" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
De forma predeterminada, una aplicación nueva incluye tres archivos de parámetros de aplicación, denominados Local.1Node.xml, Local.5Node.xml y Cloud.xml:

![Archivos de parámetros de la aplicación en el Explorador de soluciones][app-parameters-solution-explorer]

toocreate un archivo de parámetros, simplemente copie y pegue uno ya existente y asígnele un nombre nuevo.

## <a name="identifying-environment-specific-parameters-during-deployment"></a>Identificación de parámetros específicos del entorno durante la implementación
Durante la implementación, deberá toochoose Hola parámetro apropiado archivo tooapply con la aplicación. Puede hacerlo a través del cuadro de diálogo de publicación de hello en Visual Studio o PowerShell.

### <a name="deploy-from-visual-studio"></a>Implementación desde Visual Studio
Puede elegir entre lista Hola de archivos de parámetros disponibles cuando se publica la aplicación en Visual Studio.

![Elija un archivo de parámetros en el cuadro de diálogo de hello publicar][publishdialog]

### <a name="deploy-from-powershell"></a>Implementación a partir de PowerShell
Hola `Deploy-FabricApplication.ps1` script de PowerShell incluido en la plantilla de proyecto de aplicación Hola acepta un perfil de publicación como un parámetro y hello PublishProfile contiene un archivo de parámetros de referencia toohello aplicación.

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de algunos de los conceptos básicos de Hola que se describen en este tema, vea hello [Introducción técnica a Service Fabric](service-fabric-technical-overview.md). Para obtener más información sobre otras funcionalidades de administración de aplicaciones disponibles en Visual Studio, vea [Administración de aplicaciones de Service Fabric en Visual Studio](service-fabric-manage-application-in-visual-studio.md).

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
