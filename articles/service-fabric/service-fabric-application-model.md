---
title: modelo de aplicaciones de Service Fabric aaaAzure | Documentos de Microsoft
description: "¿Cómo toomodel y describir aplicaciones y servicios de Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 17a99380-5ed8-4ed9-b884-e9b827431b02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: 54c4d026e7d556be5f697d4a6f2ee886687e1c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="model-an-application-in-service-fabric"></a>Modelar una aplicación en Service Fabric
Este artículo proporciona información general sobre el modelo de aplicaciones de Azure Service Fabric de Hola y cómo toodefine una aplicación y el servicio a través de los archivos de manifiesto.

## <a name="understand-hello-application-model"></a>Entender el modelo de aplicación Hola
Una aplicación es una colección de servicios constituyentes que realizan una determinada función o funciones. Un servicio realiza una función completa e independiente, y puede iniciarse y ejecutarse independientemente de otros servicios.  Un servicio se compone de código, configuración y datos. Para cada servicio, código consta de los archivos binarios de hello ejecutable, configuración consta de configuración del servicio que se pueden cargar en tiempo de ejecución y datos están formados por toobe de datos estáticos arbitrario utilizado por el servicio de Hola. Cada componente de este modelo de aplicación jerárquico puede tener varias versiones y actualizarse independientemente.

![modelo de aplicaciones de Service Fabric Hola][appmodel-diagram]

Un tipo de aplicación es una categorización de una aplicación, que consta de un conjunto de tipos de servicio. Un tipo de servicio es una categorización de un servicio. categorización de Hello puede tener distintas configuraciones y configuraciones, pero Hola Hola core funcionalidad permanece igual. instancias de un servicio Hello son variaciones de configuración de servicio diferente de Hola de hello mismo tipo de servicio.  

Las clases (o "tipos") de aplicaciones y servicios se describen a través de archivos XML (manifiestos de aplicación y de servicio).  Hola manifiestos son plantillas de hello en el que las aplicaciones se pueden crear instancias del clúster de hello almacén de imágenes. se instala con hello SDK del servicio de Fabric Hello definición de esquema de archivo de ServiceManifest.xml y ApplicationManifest.xml de hello y herramientas demasiado*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

código de Hello de instancias de aplicación diferente que se ejecutan como procesos independientes, incluso cuando se hospedan en Hola mismo nodo de Service Fabric. Además, se puede administrar Hola ciclo de vida de cada instancia de la aplicación (por ejemplo, si se actualiza) por separado. Hello diagrama siguiente muestra cómo los tipos de aplicaciones se componen de tipos de servicio, que a su vez están compuestos de código, la configuración y paquetes de datos. diagrama de hello toosimplify, sólo paquetes de datos/config/código de hello para `ServiceType4` se muestran, aunque cada tipo de servicio podría incluir algunos o todos los tipos de paquetes.

![Tipos de aplicaciones de Service Fabric y tipos de servicio][cluster-imagestore-apptypes]

Dos archivos de manifiesto son servicios y aplicaciones usados toodescribe: Hola manifiesto del servicio y el manifiesto de aplicación. Los manifiestos se tratan detalladamente en las secciones siguientes de Hola.

Puede haber una o más instancias de un tipo de servicio activas en el clúster de Hola. Por ejemplo, las instancias de servicio con estado, o réplicas, logran alta confiabilidad mediante la replicación de estado entre las réplicas ubicadas en distintos nodos de clúster de Hola. Replicación básicamente proporciona redundancia para hello servicio toobe disponible incluso si se produce un error en un nodo en un clúster. A [particiones servicio](service-fabric-concepts-partitioning.md) más divide su estado (y su estado de toothat de patrones de acceso) en nodos de clúster de Hola.

Hello siguiente diagrama muestra hello relación entre las aplicaciones y las instancias de servicio, particiones y réplicas.

![Particiones y réplicas dentro de un servicio][cluster-application-instances]

> [!TIP]
> Puede ver el diseño de Hola de aplicaciones en un clúster con la herramienta de explorador de Service Fabric Hola disponible en http://&lt;yourclusteraddress&gt;: 19080/explorador. Para más información, vea [Visualización del clúster mediante Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
> 
> 

## <a name="describe-a-service"></a>Describir un servicio
manifiesto del servicio Hello mediante declaración define la versión y tipo de servicio de Hola. Especifica los metadatos de servicio, como el tipo de servicio, las propiedades de estado, las métricas de equilibrio de carga, archivos binarios del servicio y archivos de configuración.  Dicho de otro modo, se describen paquetes de código, configuración y datos de Hola que componen un toosupport de paquete de servicio uno o más tipos de servicio. Este es un ejemplo sencillo de manifiesto de servicio:

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

**Versión** atributos son cadenas no estructuradas y no analizar sistema Hola. Atributos de versión es tooversion usa cada componente para las actualizaciones.

**ServiceTypes** declara qué tipos de servicio admite **CodePackages** en este manifiesto. Cuando se crea una instancia de un servicio en uno de estos tipos de servicio, todos los paquetes de código declarados en este manifiesto se activan mediante la ejecución de sus puntos de entrada. procesos resultantes Hola son tipos de servicio de hello compatible de tooregister esperado en tiempo de ejecución. Tipos de servicio se declaran en el nivel de manifiesto de hello y no el nivel de paquete del código de hello. Por lo que cuando hay varios paquetes de código, se todos activan cada vez que el sistema de hello busca cualquiera de hello declarado los tipos de servicio.

**SetupEntryPoint** es un punto de entrada con privilegios que se ejecuta con hello mismo credenciales como Service Fabric (normalmente Hola *LocalSystem* cuenta) antes de cualquier otro punto de entrada. ejecutable de Hello especificado por **EntryPoint** suele ser host de servicio de ejecución prolongada de Hola. presencia de Hola de un punto de entrada del programa de instalación independiente evita tener host del servicio de hello toorun con privilegios altos durante largos períodos de tiempo. ejecutable de Hello especificado por **EntryPoint** se ejecuta después de **SetupEntryPoint** se cierra correctamente. Si alguna vez proceso Hola finaliza o se bloquea, el proceso resultante Hola se supervisa y se reinicia (nuevo a partir **SetupEntryPoint**).  

Escenarios típicos de uso **SetupEntryPoint** son cuando se ejecuta un archivo ejecutable antes de iniciar servicio de Hola o realizar una operación con privilegios elevados. Por ejemplo:

* Configurar e inicializar variables de entorno que Hola necesidades ejecutable del servicio. Esto no es ejecutables tooonly limitado escritos a través de los modelos de programación de Service Fabric Hola. Por ejemplo, npm.exe necesita algunas variables de entorno configuradas para implementar una aplicación node.js.
* Configuración del control de acceso mediante la instalación de certificados de seguridad.

Para obtener más información acerca de cómo hello tooconfigure **SetupEntryPoint** vea [configurar Directiva de Hola para un punto de entrada del programa de instalación de servicio](service-fabric-application-runas-security.md)

**EnvironmentVariables** proporciona una lista de variables de entorno que se establecen para este paquete de código. Variables de Environmentment pueden invalidarse en hello `ApplicationManifest.xml` tooprovide valores diferentes para distintas instancias de servicio. 

**DataPackage** declara una carpeta, denominada por hello **nombre** atributo, que contiene toobe arbitraria de datos estáticos que consume el proceso de hello en tiempo de ejecución.

**ConfigPackage** declara una carpeta, denominada por hello **nombre** atributo, que contiene un *Settings.xml* archivo. archivo de configuración de Hello contiene secciones de los valores de par de clave y valor, definido por el usuario que lee el proceso de hello en tiempo de ejecución. Durante una actualización, si solo hello **ConfigPackage** **versión** ha cambiado, a continuación, Hola ejecutando el proceso no se reinicia. En su lugar, una devolución de llamada notifica al proceso de Hola que han cambiado los valores de configuración para que pueden volver a cargar dinámicamente. Este es un ejemplo de archivo *Settings.xml* :

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> Un manifiesto de servicio puede contener varios paquetes de código, configuración y datos, pudiendo tener cada uno de ellos varias versiones de forma independiente.
> 
> 

<!--
For more information about other features supported by service manifests, refer toohello following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a>Describir una aplicación
manifiesto de aplicación Hola describe mediante declaración versión y tipo de aplicación Hola. Especifica metadatos de composición de servicios como nombres estables, esquema de particiones, recuento de instancias/factor de replicación, directiva de seguridad y aislamiento, restricciones de ubicación, reemplazos de configuración y tipos de servicio constituyentes. También se describen los dominios de equilibrio de carga de Hello en que se coloca la aplicación hello.

Por lo tanto, un manifiesto de aplicación describe los elementos en el nivel de aplicación de Hola y hace referencia a uno o más servicio manifiestos toocompose un tipo de aplicación. Este es un ejemplo sencillo de manifiesto de aplicación:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ApplicationManifest
      ApplicationTypeName="MyApplicationType"
      ApplicationTypeVersion="AppManifestVersion1"
      xmlns="http://schemas.microsoft.com/2011/01/fabric"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example application manifest</Description>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="MyServiceManifest" ServiceManifestVersion="SvcManifestVersion1"/>
    <ConfigOverrides/>
    <EnvironmentOverrides CodePackageRef="MyCode"/>
  </ServiceManifestImport>
  <DefaultServices>
     <Service Name="MyService">
         <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
             <SingletonPartition/>
         </StatelessService>
     </Service>
  </DefaultServices>
</ApplicationManifest>
```

Al igual que los manifiestos de servicio, **versión** atributos son cadenas no estructuradas y no están analizados por sistema Hola. Atributos de versión también es utilizado tooversion cada componente para las actualizaciones.

**ServiceManifestImport** contiene manifiestos de tooservice de referencias que componen este tipo de aplicación. Los manifiestos de servicio importados determinan qué tipos de servicio son válidos dentro de este tipo de aplicación. Dentro de hello ServiceManifestImport, se invalidan los valores de configuración en Settings.xml y entorno de variables en archivos de ServiceManifest.xml. 


**DefaultServices** declara instancias de servicio que se crean automáticamente cada vez que se crea una instancia de una aplicación en este tipo de aplicación. Los servicios predeterminados son simplemente una comodidad y se comportan como servicios normales en todos los aspectos después de su creación. Se actualizan junto con todos los demás servicios en la instancia de la aplicación hello y también se pueden quitar.

> [!NOTE]
> Un manifiesto de aplicación puede contener varias importaciones y servicios predeterminados del manifiesto de servicio. Cada importación del manifiesto de servicio puede tener varias versiones independientemente.
> 
> 

toolearn toomaintain otra aplicación y los parámetros de servicio para entornos individuales, vea [administrar parámetros de la aplicación para varios entornos](service-fabric-manage-multiple-environment-app-configuration.md).

<!--
For more information about other features supported by application manifests, refer toohello following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a>Pasos siguientes
[Empaquetar una aplicación](service-fabric-package-apps.md) y asegúrese de está listo toodeploy.

[Implementar y quitar aplicaciones] [ 10] describe cómo toouse instancias de la aplicación de toomanage de PowerShell.

[Administrar parámetros de la aplicación para varios entornos] [ 11] describe cómo tooconfigure parámetros y variables de entorno para las instancias de aplicación diferente.

[Configurar directivas de seguridad para la aplicación] [ 12] describe cómo toorun servicios con acceso de toorestrict de directivas de seguridad.

Los [Modelos de hospedaje de aplicaciones][13] describen la relación entre las réplicas o las instancias de un servicio implementado y el proceso de host de servicio.

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
