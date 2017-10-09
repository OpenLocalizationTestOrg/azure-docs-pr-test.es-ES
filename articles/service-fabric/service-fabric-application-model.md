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
# <a name="model-an-application-in-service-fabric"></a><span data-ttu-id="c6aff-103">Modelar una aplicación en Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c6aff-103">Model an application in Service Fabric</span></span>
<span data-ttu-id="c6aff-104">Este artículo proporciona información general sobre el modelo de aplicaciones de Azure Service Fabric de Hola y cómo toodefine una aplicación y el servicio a través de los archivos de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="c6aff-104">This article provides an overview of hello Azure Service Fabric application model and how toodefine an application and service via manifest files.</span></span>

## <a name="understand-hello-application-model"></a><span data-ttu-id="c6aff-105">Entender el modelo de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="c6aff-105">Understand hello application model</span></span>
<span data-ttu-id="c6aff-106">Una aplicación es una colección de servicios constituyentes que realizan una determinada función o funciones.</span><span class="sxs-lookup"><span data-stu-id="c6aff-106">An application is a collection of constituent services that perform a certain function or functions.</span></span> <span data-ttu-id="c6aff-107">Un servicio realiza una función completa e independiente, y puede iniciarse y ejecutarse independientemente de otros servicios.</span><span class="sxs-lookup"><span data-stu-id="c6aff-107">A service performs a complete and standalone function and can start and run independently of other services.</span></span>  <span data-ttu-id="c6aff-108">Un servicio se compone de código, configuración y datos.</span><span class="sxs-lookup"><span data-stu-id="c6aff-108">A service is composed of code, configuration, and data.</span></span> <span data-ttu-id="c6aff-109">Para cada servicio, código consta de los archivos binarios de hello ejecutable, configuración consta de configuración del servicio que se pueden cargar en tiempo de ejecución y datos están formados por toobe de datos estáticos arbitrario utilizado por el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6aff-109">For each service, code consists of hello executable binaries, configuration consists of service settings that can be loaded at run time, and data consists of arbitrary static data toobe consumed by hello service.</span></span> <span data-ttu-id="c6aff-110">Cada componente de este modelo de aplicación jerárquico puede tener varias versiones y actualizarse independientemente.</span><span class="sxs-lookup"><span data-stu-id="c6aff-110">Each component in this hierarchical application model can be versioned and upgraded independently.</span></span>

![modelo de aplicaciones de Service Fabric Hola][appmodel-diagram]

<span data-ttu-id="c6aff-112">Un tipo de aplicación es una categorización de una aplicación, que consta de un conjunto de tipos de servicio.</span><span class="sxs-lookup"><span data-stu-id="c6aff-112">An application type is a categorization of an application and consists of a bundle of service types.</span></span> <span data-ttu-id="c6aff-113">Un tipo de servicio es una categorización de un servicio.</span><span class="sxs-lookup"><span data-stu-id="c6aff-113">A service type is a categorization of a service.</span></span> <span data-ttu-id="c6aff-114">categorización de Hello puede tener distintas configuraciones y configuraciones, pero Hola Hola core funcionalidad permanece igual.</span><span class="sxs-lookup"><span data-stu-id="c6aff-114">hello categorization can have different settings and configurations, but hello core functionality remains hello same.</span></span> <span data-ttu-id="c6aff-115">instancias de un servicio Hello son variaciones de configuración de servicio diferente de Hola de hello mismo tipo de servicio.</span><span class="sxs-lookup"><span data-stu-id="c6aff-115">hello instances of a service are hello different service configuration variations of hello same service type.</span></span>  

<span data-ttu-id="c6aff-116">Las clases (o "tipos") de aplicaciones y servicios se describen a través de archivos XML (manifiestos de aplicación y de servicio).</span><span class="sxs-lookup"><span data-stu-id="c6aff-116">Classes (or "types") of applications and services are described through XML files (application manifests and service manifests).</span></span>  <span data-ttu-id="c6aff-117">Hola manifiestos son plantillas de hello en el que las aplicaciones se pueden crear instancias del clúster de hello almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="c6aff-117">hello manifests are hello templates against which applications can be instantiated from hello cluster's image store.</span></span> <span data-ttu-id="c6aff-118">se instala con hello SDK del servicio de Fabric Hello definición de esquema de archivo de ServiceManifest.xml y ApplicationManifest.xml de hello y herramientas demasiado*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="c6aff-118">hello schema definition for hello ServiceManifest.xml and ApplicationManifest.xml file is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

<span data-ttu-id="c6aff-119">código de Hello de instancias de aplicación diferente que se ejecutan como procesos independientes, incluso cuando se hospedan en Hola mismo nodo de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c6aff-119">hello code for different application instances run as separate processes even when hosted by hello same Service Fabric node.</span></span> <span data-ttu-id="c6aff-120">Además, se puede administrar Hola ciclo de vida de cada instancia de la aplicación (por ejemplo, si se actualiza) por separado.</span><span class="sxs-lookup"><span data-stu-id="c6aff-120">Furthermore, hello lifecycle of each application instance can be managed (for example, upgraded) independently.</span></span> <span data-ttu-id="c6aff-121">Hello diagrama siguiente muestra cómo los tipos de aplicaciones se componen de tipos de servicio, que a su vez están compuestos de código, la configuración y paquetes de datos.</span><span class="sxs-lookup"><span data-stu-id="c6aff-121">hello following diagram shows how application types are composed of service types, which in turn are composed of code, configuration, and data packages.</span></span> <span data-ttu-id="c6aff-122">diagrama de hello toosimplify, sólo paquetes de datos/config/código de hello para `ServiceType4` se muestran, aunque cada tipo de servicio podría incluir algunos o todos los tipos de paquetes.</span><span class="sxs-lookup"><span data-stu-id="c6aff-122">toosimplify hello diagram, only hello code/config/data packages for `ServiceType4` are shown, though each service type would include some or all those package types.</span></span>

![Tipos de aplicaciones de Service Fabric y tipos de servicio][cluster-imagestore-apptypes]

<span data-ttu-id="c6aff-124">Dos archivos de manifiesto son servicios y aplicaciones usados toodescribe: Hola manifiesto del servicio y el manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c6aff-124">Two different manifest files are used toodescribe applications and services: hello service manifest and application manifest.</span></span> <span data-ttu-id="c6aff-125">Los manifiestos se tratan detalladamente en las secciones siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6aff-125">Manifests are covered in detail in hello following sections.</span></span>

<span data-ttu-id="c6aff-126">Puede haber una o más instancias de un tipo de servicio activas en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6aff-126">There can be one or more instances of a service type active in hello cluster.</span></span> <span data-ttu-id="c6aff-127">Por ejemplo, las instancias de servicio con estado, o réplicas, logran alta confiabilidad mediante la replicación de estado entre las réplicas ubicadas en distintos nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6aff-127">For example, stateful service instances, or replicas, achieve high reliability by replicating state between replicas located on different nodes in hello cluster.</span></span> <span data-ttu-id="c6aff-128">Replicación básicamente proporciona redundancia para hello servicio toobe disponible incluso si se produce un error en un nodo en un clúster.</span><span class="sxs-lookup"><span data-stu-id="c6aff-128">Replication essentially provides redundancy for hello service toobe available even if one node in a cluster fails.</span></span> <span data-ttu-id="c6aff-129">A [particiones servicio](service-fabric-concepts-partitioning.md) más divide su estado (y su estado de toothat de patrones de acceso) en nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6aff-129">A [partitioned service](service-fabric-concepts-partitioning.md) further divides its state (and access patterns toothat state) across nodes in hello cluster.</span></span>

<span data-ttu-id="c6aff-130">Hello siguiente diagrama muestra hello relación entre las aplicaciones y las instancias de servicio, particiones y réplicas.</span><span class="sxs-lookup"><span data-stu-id="c6aff-130">hello following diagram shows hello relationship between applications and service instances, partitions, and replicas.</span></span>

![Particiones y réplicas dentro de un servicio][cluster-application-instances]

> [!TIP]
> <span data-ttu-id="c6aff-132">Puede ver el diseño de Hola de aplicaciones en un clúster con la herramienta de explorador de Service Fabric Hola disponible en http://&lt;yourclusteraddress&gt;: 19080/explorador.</span><span class="sxs-lookup"><span data-stu-id="c6aff-132">You can view hello layout of applications in a cluster using hello Service Fabric Explorer tool available at http://&lt;yourclusteraddress&gt;:19080/Explorer.</span></span> <span data-ttu-id="c6aff-133">Para más información, vea [Visualización del clúster mediante Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="c6aff-133">For more information, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
> 
> 

## <a name="describe-a-service"></a><span data-ttu-id="c6aff-134">Describir un servicio</span><span class="sxs-lookup"><span data-stu-id="c6aff-134">Describe a service</span></span>
<span data-ttu-id="c6aff-135">manifiesto del servicio Hello mediante declaración define la versión y tipo de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6aff-135">hello service manifest declaratively defines hello service type and version.</span></span> <span data-ttu-id="c6aff-136">Especifica los metadatos de servicio, como el tipo de servicio, las propiedades de estado, las métricas de equilibrio de carga, archivos binarios del servicio y archivos de configuración.</span><span class="sxs-lookup"><span data-stu-id="c6aff-136">It specifies service metadata such as service type, health properties, load-balancing metrics, service binaries, and configuration files.</span></span>  <span data-ttu-id="c6aff-137">Dicho de otro modo, se describen paquetes de código, configuración y datos de Hola que componen un toosupport de paquete de servicio uno o más tipos de servicio.</span><span class="sxs-lookup"><span data-stu-id="c6aff-137">Put another way, it describes hello code, configuration, and data packages that compose a service package toosupport one or more service types.</span></span> <span data-ttu-id="c6aff-138">Este es un ejemplo sencillo de manifiesto de servicio:</span><span class="sxs-lookup"><span data-stu-id="c6aff-138">Here is a simple example service manifest:</span></span>

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

<span data-ttu-id="c6aff-139">**Versión** atributos son cadenas no estructuradas y no analizar sistema Hola.</span><span class="sxs-lookup"><span data-stu-id="c6aff-139">**Version** attributes are unstructured strings and not parsed by hello system.</span></span> <span data-ttu-id="c6aff-140">Atributos de versión es tooversion usa cada componente para las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="c6aff-140">Version attributes are used tooversion each component for upgrades.</span></span>

<span data-ttu-id="c6aff-141">**ServiceTypes** declara qué tipos de servicio admite **CodePackages** en este manifiesto.</span><span class="sxs-lookup"><span data-stu-id="c6aff-141">**ServiceTypes** declares what service types are supported by **CodePackages** in this manifest.</span></span> <span data-ttu-id="c6aff-142">Cuando se crea una instancia de un servicio en uno de estos tipos de servicio, todos los paquetes de código declarados en este manifiesto se activan mediante la ejecución de sus puntos de entrada.</span><span class="sxs-lookup"><span data-stu-id="c6aff-142">When a service is instantiated against one of these service types, all code packages declared in this manifest are activated by running their entry points.</span></span> <span data-ttu-id="c6aff-143">procesos resultantes Hola son tipos de servicio de hello compatible de tooregister esperado en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="c6aff-143">hello resulting processes are expected tooregister hello supported service types at run time.</span></span> <span data-ttu-id="c6aff-144">Tipos de servicio se declaran en el nivel de manifiesto de hello y no el nivel de paquete del código de hello.</span><span class="sxs-lookup"><span data-stu-id="c6aff-144">Service types are declared at hello manifest level and not hello code package level.</span></span> <span data-ttu-id="c6aff-145">Por lo que cuando hay varios paquetes de código, se todos activan cada vez que el sistema de hello busca cualquiera de hello declarado los tipos de servicio.</span><span class="sxs-lookup"><span data-stu-id="c6aff-145">So when there are multiple code packages, they are all activated whenever hello system looks for any one of hello declared service types.</span></span>

<span data-ttu-id="c6aff-146">**SetupEntryPoint** es un punto de entrada con privilegios que se ejecuta con hello mismo credenciales como Service Fabric (normalmente Hola *LocalSystem* cuenta) antes de cualquier otro punto de entrada.</span><span class="sxs-lookup"><span data-stu-id="c6aff-146">**SetupEntryPoint** is a privileged entry point that runs with hello same credentials as Service Fabric (typically hello *LocalSystem* account) before any other entry point.</span></span> <span data-ttu-id="c6aff-147">ejecutable de Hello especificado por **EntryPoint** suele ser host de servicio de ejecución prolongada de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6aff-147">hello executable specified by **EntryPoint** is typically hello long-running service host.</span></span> <span data-ttu-id="c6aff-148">presencia de Hola de un punto de entrada del programa de instalación independiente evita tener host del servicio de hello toorun con privilegios altos durante largos períodos de tiempo.</span><span class="sxs-lookup"><span data-stu-id="c6aff-148">hello presence of a separate setup entry point avoids having toorun hello service host with high privileges for extended periods of time.</span></span> <span data-ttu-id="c6aff-149">ejecutable de Hello especificado por **EntryPoint** se ejecuta después de **SetupEntryPoint** se cierra correctamente.</span><span class="sxs-lookup"><span data-stu-id="c6aff-149">hello executable specified by **EntryPoint** is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="c6aff-150">Si alguna vez proceso Hola finaliza o se bloquea, el proceso resultante Hola se supervisa y se reinicia (nuevo a partir **SetupEntryPoint**).</span><span class="sxs-lookup"><span data-stu-id="c6aff-150">If hello process ever terminates or crashes, hello resulting process is monitored and restarted (beginning again with **SetupEntryPoint**).</span></span>  

<span data-ttu-id="c6aff-151">Escenarios típicos de uso **SetupEntryPoint** son cuando se ejecuta un archivo ejecutable antes de iniciar servicio de Hola o realizar una operación con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="c6aff-151">Typical scenarios for using **SetupEntryPoint** are when you run an executable before hello service starts or you perform an operation with elevated privileges.</span></span> <span data-ttu-id="c6aff-152">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c6aff-152">For example:</span></span>

* <span data-ttu-id="c6aff-153">Configurar e inicializar variables de entorno que Hola necesidades ejecutable del servicio.</span><span class="sxs-lookup"><span data-stu-id="c6aff-153">Setting up and initializing environment variables that hello service executable needs.</span></span> <span data-ttu-id="c6aff-154">Esto no es ejecutables tooonly limitado escritos a través de los modelos de programación de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="c6aff-154">This is not limited tooonly executables written via hello Service Fabric programming models.</span></span> <span data-ttu-id="c6aff-155">Por ejemplo, npm.exe necesita algunas variables de entorno configuradas para implementar una aplicación node.js.</span><span class="sxs-lookup"><span data-stu-id="c6aff-155">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="c6aff-156">Configuración del control de acceso mediante la instalación de certificados de seguridad.</span><span class="sxs-lookup"><span data-stu-id="c6aff-156">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="c6aff-157">Para obtener más información acerca de cómo hello tooconfigure **SetupEntryPoint** vea [configurar Directiva de Hola para un punto de entrada del programa de instalación de servicio](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="c6aff-157">For more details on how tooconfigure hello **SetupEntryPoint** see [Configure hello policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<span data-ttu-id="c6aff-158">**EnvironmentVariables** proporciona una lista de variables de entorno que se establecen para este paquete de código.</span><span class="sxs-lookup"><span data-stu-id="c6aff-158">**EnvironmentVariables** provides a list of environment variables that are set for this code package.</span></span> <span data-ttu-id="c6aff-159">Variables de Environmentment pueden invalidarse en hello `ApplicationManifest.xml` tooprovide valores diferentes para distintas instancias de servicio.</span><span class="sxs-lookup"><span data-stu-id="c6aff-159">Environmentment variables can be overridden in hello `ApplicationManifest.xml` tooprovide different values for different service instances.</span></span> 

<span data-ttu-id="c6aff-160">**DataPackage** declara una carpeta, denominada por hello **nombre** atributo, que contiene toobe arbitraria de datos estáticos que consume el proceso de hello en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="c6aff-160">**DataPackage** declares a folder, named by hello **Name** attribute, that contains arbitrary static data toobe consumed by hello process at run time.</span></span>

<span data-ttu-id="c6aff-161">**ConfigPackage** declara una carpeta, denominada por hello **nombre** atributo, que contiene un *Settings.xml* archivo.</span><span class="sxs-lookup"><span data-stu-id="c6aff-161">**ConfigPackage** declares a folder, named by hello **Name** attribute, that contains a *Settings.xml* file.</span></span> <span data-ttu-id="c6aff-162">archivo de configuración de Hello contiene secciones de los valores de par de clave y valor, definido por el usuario que lee el proceso de hello en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="c6aff-162">hello settings file contains sections of user-defined, key-value pair settings that hello process reads back at run time.</span></span> <span data-ttu-id="c6aff-163">Durante una actualización, si solo hello **ConfigPackage** **versión** ha cambiado, a continuación, Hola ejecutando el proceso no se reinicia.</span><span class="sxs-lookup"><span data-stu-id="c6aff-163">During an upgrade, if only hello **ConfigPackage** **version** has changed, then hello running process is not restarted.</span></span> <span data-ttu-id="c6aff-164">En su lugar, una devolución de llamada notifica al proceso de Hola que han cambiado los valores de configuración para que pueden volver a cargar dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="c6aff-164">Instead, a callback notifies hello process that configuration settings have changed so they can be reloaded dynamically.</span></span> <span data-ttu-id="c6aff-165">Este es un ejemplo de archivo *Settings.xml* :</span><span class="sxs-lookup"><span data-stu-id="c6aff-165">Here is an example *Settings.xml* file:</span></span>

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> <span data-ttu-id="c6aff-166">Un manifiesto de servicio puede contener varios paquetes de código, configuración y datos,</span><span class="sxs-lookup"><span data-stu-id="c6aff-166">A service manifest can contain multiple code, configuration, and data packages.</span></span> <span data-ttu-id="c6aff-167">pudiendo tener cada uno de ellos varias versiones de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="c6aff-167">Each of those can be versioned independently.</span></span>
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

## <a name="describe-an-application"></a><span data-ttu-id="c6aff-168">Describir una aplicación</span><span class="sxs-lookup"><span data-stu-id="c6aff-168">Describe an application</span></span>
<span data-ttu-id="c6aff-169">manifiesto de aplicación Hola describe mediante declaración versión y tipo de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="c6aff-169">hello application manifest declaratively describes hello application type and version.</span></span> <span data-ttu-id="c6aff-170">Especifica metadatos de composición de servicios como nombres estables, esquema de particiones, recuento de instancias/factor de replicación, directiva de seguridad y aislamiento, restricciones de ubicación, reemplazos de configuración y tipos de servicio constituyentes.</span><span class="sxs-lookup"><span data-stu-id="c6aff-170">It specifies service composition metadata such as stable names, partitioning scheme, instance count/replication factor, security/isolation policy, placement constraints, configuration overrides, and constituent service types.</span></span> <span data-ttu-id="c6aff-171">También se describen los dominios de equilibrio de carga de Hello en que se coloca la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c6aff-171">hello load-balancing domains into which hello application is placed are also described.</span></span>

<span data-ttu-id="c6aff-172">Por lo tanto, un manifiesto de aplicación describe los elementos en el nivel de aplicación de Hola y hace referencia a uno o más servicio manifiestos toocompose un tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c6aff-172">Thus, an application manifest describes elements at hello application level and references one or more service manifests toocompose an application type.</span></span> <span data-ttu-id="c6aff-173">Este es un ejemplo sencillo de manifiesto de aplicación:</span><span class="sxs-lookup"><span data-stu-id="c6aff-173">Here is a simple example application manifest:</span></span>

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

<span data-ttu-id="c6aff-174">Al igual que los manifiestos de servicio, **versión** atributos son cadenas no estructuradas y no están analizados por sistema Hola.</span><span class="sxs-lookup"><span data-stu-id="c6aff-174">Like service manifests, **Version** attributes are unstructured strings and are not parsed by hello system.</span></span> <span data-ttu-id="c6aff-175">Atributos de versión también es utilizado tooversion cada componente para las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="c6aff-175">Version attributes are also used tooversion each component for upgrades.</span></span>

<span data-ttu-id="c6aff-176">**ServiceManifestImport** contiene manifiestos de tooservice de referencias que componen este tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c6aff-176">**ServiceManifestImport** contains references tooservice manifests that compose this application type.</span></span> <span data-ttu-id="c6aff-177">Los manifiestos de servicio importados determinan qué tipos de servicio son válidos dentro de este tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c6aff-177">Imported service manifests determine what service types are valid within this application type.</span></span> <span data-ttu-id="c6aff-178">Dentro de hello ServiceManifestImport, se invalidan los valores de configuración en Settings.xml y entorno de variables en archivos de ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="c6aff-178">Within hello ServiceManifestImport, you override configuration values in Settings.xml and environment variables in ServiceManifest.xml files.</span></span> 


<span data-ttu-id="c6aff-179">**DefaultServices** declara instancias de servicio que se crean automáticamente cada vez que se crea una instancia de una aplicación en este tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c6aff-179">**DefaultServices** declares service instances that are automatically created whenever an application is instantiated against this application type.</span></span> <span data-ttu-id="c6aff-180">Los servicios predeterminados son simplemente una comodidad y se comportan como servicios normales en todos los aspectos después de su creación.</span><span class="sxs-lookup"><span data-stu-id="c6aff-180">Default services are just a convenience and behave like normal services in every respect after they have been created.</span></span> <span data-ttu-id="c6aff-181">Se actualizan junto con todos los demás servicios en la instancia de la aplicación hello y también se pueden quitar.</span><span class="sxs-lookup"><span data-stu-id="c6aff-181">They are upgraded along with any other services in hello application instance and can be removed as well.</span></span>

> [!NOTE]
> <span data-ttu-id="c6aff-182">Un manifiesto de aplicación puede contener varias importaciones y servicios predeterminados del manifiesto de servicio.</span><span class="sxs-lookup"><span data-stu-id="c6aff-182">An application manifest can contain multiple service manifest imports and default services.</span></span> <span data-ttu-id="c6aff-183">Cada importación del manifiesto de servicio puede tener varias versiones independientemente.</span><span class="sxs-lookup"><span data-stu-id="c6aff-183">Each service manifest import can be versioned independently.</span></span>
> 
> 

<span data-ttu-id="c6aff-184">toolearn toomaintain otra aplicación y los parámetros de servicio para entornos individuales, vea [administrar parámetros de la aplicación para varios entornos](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="c6aff-184">toolearn how toomaintain different application and service parameters for individual environments, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

<!--
For more information about other features supported by application manifests, refer toohello following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a><span data-ttu-id="c6aff-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c6aff-185">Next steps</span></span>
<span data-ttu-id="c6aff-186">[Empaquetar una aplicación](service-fabric-package-apps.md) y asegúrese de está listo toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c6aff-186">[Package an application](service-fabric-package-apps.md) and make it ready toodeploy.</span></span>

<span data-ttu-id="c6aff-187">[Implementar y quitar aplicaciones] [ 10] describe cómo toouse instancias de la aplicación de toomanage de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6aff-187">[Deploy and remove applications][10] describes how toouse PowerShell toomanage application instances.</span></span>

<span data-ttu-id="c6aff-188">[Administrar parámetros de la aplicación para varios entornos] [ 11] describe cómo tooconfigure parámetros y variables de entorno para las instancias de aplicación diferente.</span><span class="sxs-lookup"><span data-stu-id="c6aff-188">[Managing application parameters for multiple environments][11] describes how tooconfigure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="c6aff-189">[Configurar directivas de seguridad para la aplicación] [ 12] describe cómo toorun servicios con acceso de toorestrict de directivas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="c6aff-189">[Configure security policies for your application][12] describes how toorun services under security policies toorestrict access.</span></span>

<span data-ttu-id="c6aff-190">Los [Modelos de hospedaje de aplicaciones][13] describen la relación entre las réplicas o las instancias de un servicio implementado y el proceso de host de servicio.</span><span class="sxs-lookup"><span data-stu-id="c6aff-190">[Application hosting models][13] describe relationship between replicas (or instances) of a deployed service and service-host process.</span></span>

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
