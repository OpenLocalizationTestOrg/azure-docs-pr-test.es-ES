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
# <a name="manage-application-parameters-for-multiple-environments"></a><span data-ttu-id="daa91-105">Administración de los parámetros de la aplicación en varios entornos</span><span class="sxs-lookup"><span data-stu-id="daa91-105">Manage application parameters for multiple environments</span></span>
<span data-ttu-id="daa91-106">Puede crear clústeres de Azure Service Fabric mediante en cualquier parte de una toomany miles de máquinas.</span><span class="sxs-lookup"><span data-stu-id="daa91-106">You can create Azure Service Fabric clusters by using anywhere from one toomany thousands of machines.</span></span> <span data-ttu-id="daa91-107">Aunque los archivos binarios de aplicación pueden ejecutar sin modificaciones a través de este amplio espectro de entornos, a menudo desea tooconfigure Hola aplicación de manera diferente, según número Hola de máquinas que vaya a implementar.</span><span class="sxs-lookup"><span data-stu-id="daa91-107">While application binaries can run without modification across this wide spectrum of environments, you often want tooconfigure hello application differently, depending on hello number of machines you're deploying to.</span></span>

<span data-ttu-id="daa91-108">A modo de ejemplo simple, considere `InstanceCount` en un servicio sin estado.</span><span class="sxs-lookup"><span data-stu-id="daa91-108">As a simple example, consider `InstanceCount` for a stateless service.</span></span> <span data-ttu-id="daa91-109">Cuando se ejecutan las aplicaciones en Azure, se suele preferir tooset este valor especiales del parámetro toohello "-1".</span><span class="sxs-lookup"><span data-stu-id="daa91-109">When you are running applications in Azure, you generally want tooset this parameter toohello special value of "-1".</span></span> <span data-ttu-id="daa91-110">Esta configuración garantiza que el servicio se ejecuta en cada nodo de clúster de hello (o todos los nodos de tipo de nodo de hello si ha configurado una restricción de selección de ubicación).</span><span class="sxs-lookup"><span data-stu-id="daa91-110">This configuration ensures that your service is running on every node in hello cluster (or every node in hello node type if you have set a placement constraint).</span></span> <span data-ttu-id="daa91-111">Sin embargo, esta configuración no es adecuada para un clúster único equipo ya que no puede tener varios procesos escuchando en hello mismo punto de conexión en un único equipo.</span><span class="sxs-lookup"><span data-stu-id="daa91-111">However, this configuration is not suitable for a single-machine cluster since you cannot have multiple processes listening on hello same endpoint on a single machine.</span></span> <span data-ttu-id="daa91-112">En su lugar, normalmente establece `InstanceCount` demasiado "1".</span><span class="sxs-lookup"><span data-stu-id="daa91-112">Instead, you typically set `InstanceCount` too"1".</span></span>

## <a name="specifying-environment-specific-parameters"></a><span data-ttu-id="daa91-113">Especificación de parámetros concretos del entorno</span><span class="sxs-lookup"><span data-stu-id="daa91-113">Specifying environment-specific parameters</span></span>
<span data-ttu-id="daa91-114">problema de configuración de Hello solución toothis es un conjunto de servicios predeterminados con parámetros y los archivos de parámetros de aplicación que rellenan los valores de parámetro para un entorno determinado.</span><span class="sxs-lookup"><span data-stu-id="daa91-114">hello solution toothis configuration issue is a set of parameterized default services and application parameter files that fill in those parameter values for a given environment.</span></span> <span data-ttu-id="daa91-115">Servicios predeterminados y los parámetros de la aplicación están configurados en la aplicación hello y manifiestos de servicio.</span><span class="sxs-lookup"><span data-stu-id="daa91-115">Default services and application parameters are configured in hello application and service manifests.</span></span> <span data-ttu-id="daa91-116">se instala con hello SDK del servicio de Fabric Hello definición de esquema para archivos de ServiceManifest.xml y ApplicationManifest.xml de Hola y herramientas demasiado*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="daa91-116">hello schema definition for hello ServiceManifest.xml and ApplicationManifest.xml files is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

### <a name="default-services"></a><span data-ttu-id="daa91-117">Servicios predeterminados</span><span class="sxs-lookup"><span data-stu-id="daa91-117">Default services</span></span>
<span data-ttu-id="daa91-118">Las aplicaciones de Service Fabric constan de una colección de instancias de servicio.</span><span class="sxs-lookup"><span data-stu-id="daa91-118">Service Fabric applications are made up of a collection of service instances.</span></span> <span data-ttu-id="daa91-119">Aunque es posible que toocreate una aplicación vacía y, a continuación, crear todas las instancias de servicio de forma dinámica, la mayoría de las aplicaciones tiene un conjunto de servicios básicos que siempre se debe crear cuando se crea una instancia de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="daa91-119">While it is possible for you toocreate an empty application and then create all service instances dynamically, most applications have a set of core services that should always be created when hello application is instantiated.</span></span> <span data-ttu-id="daa91-120">Se trata de tooas que se hace referencia "servicios predeterminados".</span><span class="sxs-lookup"><span data-stu-id="daa91-120">These are referred tooas "default services".</span></span> <span data-ttu-id="daa91-121">Cuando se especifican en el manifiesto de aplicación Hola, con marcadores de posición para la configuración de cada entorno incluido entre corchetes:</span><span class="sxs-lookup"><span data-stu-id="daa91-121">They are specified in hello application manifest, with placeholders for per-environment configuration included in square brackets:</span></span>

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

<span data-ttu-id="daa91-122">Cada uno de los parámetros con nombre de hello debe definirse dentro de elemento de parámetros de Hola Hola del manifiesto de aplicación:</span><span class="sxs-lookup"><span data-stu-id="daa91-122">Each of hello named parameters must be defined within hello Parameters element of hello application manifest:</span></span>

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

<span data-ttu-id="daa91-123">DefaultValue (atributo) Hola especifica Hola valor toobe utilizado en ausencia de Hola de un parámetro más específica para un entorno determinado.</span><span class="sxs-lookup"><span data-stu-id="daa91-123">hello DefaultValue attribute specifies hello value toobe used in hello absence of a more-specific parameter for a given environment.</span></span>

> [!NOTE]
> <span data-ttu-id="daa91-124">No todos los parámetros de instancias de servicio son adecuados para la configuración de cada entorno.</span><span class="sxs-lookup"><span data-stu-id="daa91-124">Not all service instance parameters are suitable for per-environment configuration.</span></span> <span data-ttu-id="daa91-125">En el ejemplo de Hola anterior, Hola LowKey y valores HighKey esquema de partición del servicio de Hola se definen explícitamente para todas las instancias del servicio de hello puesto que el intervalo de partición de hello es una función de dominio de datos de hello, no el entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="daa91-125">In hello example above, hello LowKey and HighKey values for hello service's partitioning scheme are explicitly defined for all instances of hello service since hello partition range is a function of hello data domain, not hello environment.</span></span>
> 
> 

### <a name="per-environment-service-configuration-settings"></a><span data-ttu-id="daa91-126">Opciones de configuración del servicio de cada entorno</span><span class="sxs-lookup"><span data-stu-id="daa91-126">Per-environment service configuration settings</span></span>
<span data-ttu-id="daa91-127">Hola [modelo de aplicaciones de Service Fabric](service-fabric-application-model.md) permite tooinclude paquetes de configuración que contienen pares clave-valor personalizados que son legibles en tiempo de ejecución de servicios.</span><span class="sxs-lookup"><span data-stu-id="daa91-127">hello [Service Fabric application model](service-fabric-application-model.md) enables services tooinclude configuration packages that contain custom key-value pairs that are readable at run time.</span></span> <span data-ttu-id="daa91-128">valores de Hello de estas opciones también se pueden diferenciar entorno especificando un `ConfigOverride` en el manifiesto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="daa91-128">hello values of these settings can also be differentiated by environment by specifying a `ConfigOverride` in hello application manifest.</span></span>

<span data-ttu-id="daa91-129">Suponga que tiene Hola después de la configuración en hello Config\Settings.xml archivo para hello `Stateful1` servicio:</span><span class="sxs-lookup"><span data-stu-id="daa91-129">Suppose that you have hello following setting in hello Config\Settings.xml file for hello `Stateful1` service:</span></span>

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
<span data-ttu-id="daa91-130">toooverride este valor para un par de entorno o aplicación específica, cree un `ConfigOverride` al importar Hola manifiesto del servicio en el manifiesto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="daa91-130">toooverride this value for a specific application/environment pair, create a `ConfigOverride` when you import hello service manifest in hello application manifest.</span></span>

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
<span data-ttu-id="daa91-131">Este parámetro se puede configurar después por entorno, tal como se mostró anteriormente.</span><span class="sxs-lookup"><span data-stu-id="daa91-131">This parameter can then be configured by environment as shown above.</span></span> <span data-ttu-id="daa91-132">Para ello, debe declarar en la sección de parámetros de Hola Hola del manifiesto de aplicación y especificando valores específicos del entorno en los archivos de parámetros de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="daa91-132">You can do this by declaring it in hello parameters section of hello application manifest and specifying environment-specific values in hello application parameter files.</span></span>

> [!NOTE]
> <span data-ttu-id="daa91-133">En caso de hello de valores de configuración de servicio, hay tres lugares donde se puede establecer el valor de Hola de una clave: paquete de configuración de servicio de hello, el manifiesto de aplicación de Hola y el archivo de parámetros de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="daa91-133">In hello case of service configuration settings, there are three places where hello value of a key can be set: hello service configuration package, hello application manifest, and hello application parameter file.</span></span> <span data-ttu-id="daa91-134">Service Fabric se siempre elija Hola parámetro archivo de aplicación en primer lugar (si se especifica), a continuación, Hola manifiesto de aplicación y finalmente Hola paquete de configuración de.</span><span class="sxs-lookup"><span data-stu-id="daa91-134">Service Fabric will always choose from hello application parameter file first (if specified), then hello application manifest, and finally hello configuration package.</span></span>
> 
> 

### <a name="setting-and-using-environment-variables"></a><span data-ttu-id="daa91-135">Establecimiento y uso de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="daa91-135">Setting and using environment variables</span></span> 
<span data-ttu-id="daa91-136">Puede especificar y establecer variables de entorno en el archivo de ServiceManifest.xml de hello y, a continuación, invalidar estas opciones en el archivo ApplicationManifest.xml de hello en por instancia.</span><span class="sxs-lookup"><span data-stu-id="daa91-136">You can specify and set environment variables in hello ServiceManifest.xml file and then override these in hello ApplicationManifest.xml file on a per instance basis.</span></span>
<span data-ttu-id="daa91-137">ejemplo de Hola siguiente muestra dos variables de entorno, uno con un valor establecido y se reemplaza de hello otro.</span><span class="sxs-lookup"><span data-stu-id="daa91-137">hello example below shows two environment variables, one with a value set and hello other is overridden.</span></span> <span data-ttu-id="daa91-138">Puede utilizar valores de variables de entorno tooset Hola misma forma que estos se utilizan para las invalidaciones de configuración de parámetros de aplicación.</span><span class="sxs-lookup"><span data-stu-id="daa91-138">You can use application parameters tooset environment variables values in hello same way that these were used for config overrides.</span></span>

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
<span data-ttu-id="daa91-139">las variables de entorno de toooverride Hola Hola ApplicationManifest.xml, paquete de código de referencia Hola Hola ServiceManifest con hello `EnvironmentOverrides` elemento.</span><span class="sxs-lookup"><span data-stu-id="daa91-139">toooverride hello environment variables in hello ApplicationManifest.xml, reference hello code package in hello ServiceManifest with hello `EnvironmentOverrides` element.</span></span>

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 <span data-ttu-id="daa91-140">Una vez que se crea con el nombre de instancia del servicio de Hola puede tener acceso a las variables de entorno de Hola desde el código.</span><span class="sxs-lookup"><span data-stu-id="daa91-140">Once hello named service instance is created you can access hello environment variables from code.</span></span> <span data-ttu-id="daa91-141">Por ejemplo, en C# puede hacer siguiente Hola</span><span class="sxs-lookup"><span data-stu-id="daa91-141">e.g. In C# you can do hello following</span></span>

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a><span data-ttu-id="daa91-142">Variables de entorno de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="daa91-142">Service Fabric environment variables</span></span>
<span data-ttu-id="daa91-143">Service Fabric tiene variables de entorno integradas que se establecen para cada instancia del servicio.</span><span class="sxs-lookup"><span data-stu-id="daa91-143">Service Fabric has built in environment variables set for each service instance.</span></span> <span data-ttu-id="daa91-144">Hello lista completa de variables de entorno se a continuación, donde hello los en negrita son Hola que va a utilizar en su servicio, Hola otro es utilizado por el tiempo de ejecución de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="daa91-144">hello full list of environment variables is below, where hello ones in bold are hello ones that you will use in your service, hello other being used by Service Fabric runtime.</span></span> 

* <span data-ttu-id="daa91-145">Fabric_ApplicationHostId</span><span class="sxs-lookup"><span data-stu-id="daa91-145">Fabric_ApplicationHostId</span></span>
* <span data-ttu-id="daa91-146">Fabric_ApplicationHostType</span><span class="sxs-lookup"><span data-stu-id="daa91-146">Fabric_ApplicationHostType</span></span>
* <span data-ttu-id="daa91-147">Fabric_ApplicationId</span><span class="sxs-lookup"><span data-stu-id="daa91-147">Fabric_ApplicationId</span></span>
* <span data-ttu-id="daa91-148">**Fabric_ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="daa91-148">**Fabric_ApplicationName**</span></span>
* <span data-ttu-id="daa91-149">Fabric_CodePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="daa91-149">Fabric_CodePackageInstanceId</span></span>
* <span data-ttu-id="daa91-150">**Fabric_CodePackageName**</span><span class="sxs-lookup"><span data-stu-id="daa91-150">**Fabric_CodePackageName**</span></span>
* <span data-ttu-id="daa91-151">**Fabric_Endpoint_[SuNombreDeServicio]TypeEndpoint**</span><span class="sxs-lookup"><span data-stu-id="daa91-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span></span>
* <span data-ttu-id="daa91-152">**Fabric_Folder_App_Log**</span><span class="sxs-lookup"><span data-stu-id="daa91-152">**Fabric_Folder_App_Log**</span></span>
* <span data-ttu-id="daa91-153">**Fabric_Folder_App_Temp**</span><span class="sxs-lookup"><span data-stu-id="daa91-153">**Fabric_Folder_App_Temp**</span></span>
* <span data-ttu-id="daa91-154">**Fabric_Folder_App_Work**</span><span class="sxs-lookup"><span data-stu-id="daa91-154">**Fabric_Folder_App_Work**</span></span>
* <span data-ttu-id="daa91-155">**Fabric_Folder_Application**</span><span class="sxs-lookup"><span data-stu-id="daa91-155">**Fabric_Folder_Application**</span></span>
* <span data-ttu-id="daa91-156">Fabric_NodeId</span><span class="sxs-lookup"><span data-stu-id="daa91-156">Fabric_NodeId</span></span>
* <span data-ttu-id="daa91-157">**Fabric_NodeIPOrFQDN**</span><span class="sxs-lookup"><span data-stu-id="daa91-157">**Fabric_NodeIPOrFQDN**</span></span>
* <span data-ttu-id="daa91-158">**Fabric_NodeName**</span><span class="sxs-lookup"><span data-stu-id="daa91-158">**Fabric_NodeName**</span></span>
* <span data-ttu-id="daa91-159">Fabric_RuntimeConnectionAddress</span><span class="sxs-lookup"><span data-stu-id="daa91-159">Fabric_RuntimeConnectionAddress</span></span>
* <span data-ttu-id="daa91-160">Fabric_ServicePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="daa91-160">Fabric_ServicePackageInstanceId</span></span>
* <span data-ttu-id="daa91-161">Fabric_ServicePackageName</span><span class="sxs-lookup"><span data-stu-id="daa91-161">Fabric_ServicePackageName</span></span>
* <span data-ttu-id="daa91-162">Fabric_ServicePackageVersionInstance</span><span class="sxs-lookup"><span data-stu-id="daa91-162">Fabric_ServicePackageVersionInstance</span></span>
* <span data-ttu-id="daa91-163">FabricPackageFileName</span><span class="sxs-lookup"><span data-stu-id="daa91-163">FabricPackageFileName</span></span>

<span data-ttu-id="daa91-164">Hola belows de código muestra cómo toolist Hola variables de entorno de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="daa91-164">hello code belows shows how toolist hello Service Fabric environment variables</span></span>
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
<span data-ttu-id="daa91-165">Hello siguientes son ejemplos de variables de entorno para un tipo de aplicación denominado `GuestExe.Application` con un tipo de servicio llamado `FrontEndService` cuando se ejecuta en el equipo de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="daa91-165">hello following are examples of environment variables for an application type called `GuestExe.Application` with a service type called `FrontEndService` when run on your local dev machine.</span></span>

* <span data-ttu-id="daa91-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span><span class="sxs-lookup"><span data-stu-id="daa91-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span></span>
* <span data-ttu-id="daa91-167">**Fabric_CodePackageName = Code**</span><span class="sxs-lookup"><span data-stu-id="daa91-167">**Fabric_CodePackageName = Code**</span></span>
* <span data-ttu-id="daa91-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span><span class="sxs-lookup"><span data-stu-id="daa91-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span></span>
* <span data-ttu-id="daa91-169">**Fabric_NodeIPOrFQDN = localhost**</span><span class="sxs-lookup"><span data-stu-id="daa91-169">**Fabric_NodeIPOrFQDN = localhost**</span></span>
* <span data-ttu-id="daa91-170">**Fabric_NodeName = _Node_2**</span><span class="sxs-lookup"><span data-stu-id="daa91-170">**Fabric_NodeName = _Node_2**</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="daa91-171">Archivos de parámetros de la aplicación</span><span class="sxs-lookup"><span data-stu-id="daa91-171">Application parameter files</span></span>
<span data-ttu-id="daa91-172">proyecto de aplicación de Service Fabric Hola puede incluir uno o varios archivos de parámetro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="daa91-172">hello Service Fabric application project can include one or more application parameter files.</span></span> <span data-ttu-id="daa91-173">Cada uno de ellos define valores específicos de Hola para los parámetros de Hola que se definen en el manifiesto de aplicación Hola:</span><span class="sxs-lookup"><span data-stu-id="daa91-173">Each of them defines hello specific values for hello parameters that are defined in hello application manifest:</span></span>

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
<span data-ttu-id="daa91-174">De forma predeterminada, una aplicación nueva incluye tres archivos de parámetros de aplicación, denominados Local.1Node.xml, Local.5Node.xml y Cloud.xml:</span><span class="sxs-lookup"><span data-stu-id="daa91-174">By default, a new application includes three application parameter files, named Local.1Node.xml, Local.5Node.xml, and Cloud.xml:</span></span>

![Archivos de parámetros de la aplicación en el Explorador de soluciones][app-parameters-solution-explorer]

<span data-ttu-id="daa91-176">toocreate un archivo de parámetros, simplemente copie y pegue uno ya existente y asígnele un nombre nuevo.</span><span class="sxs-lookup"><span data-stu-id="daa91-176">toocreate a parameter file, simply copy and paste an existing one and give it a new name.</span></span>

## <a name="identifying-environment-specific-parameters-during-deployment"></a><span data-ttu-id="daa91-177">Identificación de parámetros específicos del entorno durante la implementación</span><span class="sxs-lookup"><span data-stu-id="daa91-177">Identifying environment-specific parameters during deployment</span></span>
<span data-ttu-id="daa91-178">Durante la implementación, deberá toochoose Hola parámetro apropiado archivo tooapply con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="daa91-178">At deployment time, you need toochoose hello appropriate parameter file tooapply with your application.</span></span> <span data-ttu-id="daa91-179">Puede hacerlo a través del cuadro de diálogo de publicación de hello en Visual Studio o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="daa91-179">You can do this through hello Publish dialog in Visual Studio or through PowerShell.</span></span>

### <a name="deploy-from-visual-studio"></a><span data-ttu-id="daa91-180">Implementación desde Visual Studio</span><span class="sxs-lookup"><span data-stu-id="daa91-180">Deploy from Visual Studio</span></span>
<span data-ttu-id="daa91-181">Puede elegir entre lista Hola de archivos de parámetros disponibles cuando se publica la aplicación en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="daa91-181">You can choose from hello list of available parameter files when you publish your application in Visual Studio.</span></span>

![Elija un archivo de parámetros en el cuadro de diálogo de hello publicar][publishdialog]

### <a name="deploy-from-powershell"></a><span data-ttu-id="daa91-183">Implementación a partir de PowerShell</span><span class="sxs-lookup"><span data-stu-id="daa91-183">Deploy from PowerShell</span></span>
<span data-ttu-id="daa91-184">Hola `Deploy-FabricApplication.ps1` script de PowerShell incluido en la plantilla de proyecto de aplicación Hola acepta un perfil de publicación como un parámetro y hello PublishProfile contiene un archivo de parámetros de referencia toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="daa91-184">hello `Deploy-FabricApplication.ps1` PowerShell script included in hello application project template accepts a publish profile as a parameter and hello PublishProfile contains a reference toohello application parameters file.</span></span>

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a><span data-ttu-id="daa91-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="daa91-185">Next steps</span></span>
<span data-ttu-id="daa91-186">toolearn más información acerca de algunos de los conceptos básicos de Hola que se describen en este tema, vea hello [Introducción técnica a Service Fabric](service-fabric-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="daa91-186">toolearn more about some of hello core concepts that are discussed in this topic, see hello [Service Fabric technical overview](service-fabric-technical-overview.md).</span></span> <span data-ttu-id="daa91-187">Para obtener más información sobre otras funcionalidades de administración de aplicaciones disponibles en Visual Studio, vea [Administración de aplicaciones de Service Fabric en Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="daa91-187">For information about other app management capabilities that are available in Visual Studio, see [Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
